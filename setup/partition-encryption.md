# PARTITION ENCRYPTION

In this document, I use `cryptsetup` with LUKS2.

## Term

An encrypted partition has the following structure:

- A "wrapper" partition. Its file system is LUKS.
- An "inner" partition. It is the true partition storing our data. Its file system should be any (I choose ext4 because it is popular now).

Example layout of the whole disk:

```shell
lsblk -f

# Output example:
NAME              FSTYPE      FSVER LABEL       UUID                                 FSAVAIL FSUSE% MOUNTPOINTS
zram0                                                                                               [SWAP]
nvme0n1
├─nvme0n1p1       vfat        FAT16 LI_EFI      B449-8F2A                             480.3M     4% /boot/efi
├─nvme0n1p2       ext4        1.0   os          ac60da0f-076c-435a-99b0-c1764259cd6c   32.8G    23% /
├─nvme0n1p3       swap        1     swap        3407b980-14e4-42dd-b88a-b463f565a320                [SWAP]
├─nvme0n1p4       ext4        1.0   home        f1fe0e4f-aa3e-46ef-b0fc-097ec2d8e9d9   85.2G     6% /home
└─nvme0n1p5       crypto_LUKS 2                 9736256c-2bc3-48f1-b3e0-5921b9e2bc1b
  └─m_encdata     ext4        1.0   encdata     1d26be04-8c4b-4c13-a9c7-30efb2b93be9  529.7M     0% /mnt/encdata
```

The the example above, we can see that `/dev/nvme0n1p5` is an encrypted partition:

- The "wrapper" partition is `/dev/nvme0n1p5`
- The "inner" partition is `/dev/mapper/m_encdata`
- This partition is mounted at `/mnt/encdata`
- There is a name for the inner partition (`m_encdata`).

It is possible that a "wapper" partition can contain more than one "inner" partition. However, in my experience it is hard to setup and manage.

&nbsp;

## Basic Setup

**Step1.** Check and identify the partition you want to encrypt (for example: `/dev/nvme0n1p5`, `/dev/sda3`):

```shell
sudo fdisk -l
lsblk -f
```

**Step2.** (Optional) Please make sure that the partition to encrypt has been already unmounted.

```shell
# Check if /dev/nvme0n1p5 is mounted
lsblk -f

# If it is mounted, then...
# sudo umount <partition>
sudo umount /dev/nvme0n1p5
```

**Step3.** Setup variables

For convenience, I define 4 variables for the whole progress:

```shell
MY_DEV_CRYPT=/dev/nvme0n1p5
MY_DEVMP_CRYPT_NAME=m_encdata
MY_PARTITION_LABEL=encdata
MY_MOUNTED_PATH=/mnt/encdata
```

In the example above:

- `/dev/nvme0n1p5` is the paritition I want to encrypt.
- `m_encdata` is the name of the inner partition.

**Step4.** Format and open the partition

```shell
sudo cryptsetup luksFormat --type luks2 $MY_DEV_CRYPT
# You will specify the passphrase to encrypt/decrypt this partition
```

The formatted partition is "closed". I must "open" it (using the passphrase/key...) for usage.

```shell
sudo cryptsetup luksOpen $MY_DEV_CRYPT $MY_DEVMP_CRYPT_NAME
```

**Step5.** Format the "inner" partition

```shell
sudo mkfs.ext4 -L $MY_PARTITION_LABEL /dev/mapper/$MY_DEVMP_CRYPT_NAME
```

**Step6.** Mount and setup the "inner" partition in a simple way

```shell
sudo mkdir $MY_MOUNTED_PATH
sudo mount /dev/mapper/$MY_DEVMP_CRYPT_NAME $MY_MOUNTED_PATH
sudo chown -R $USER:$USER $MY_MOUNTED_PATH
```

&nbsp;

## Extra Setup

**Step1.** Add a key file into encrypted partition

```shell
# Generate the key file first
# The cmd below will output to a file named "enc-key.key"
openssl genrsa -out ./enc-key.key 2048

# Add the key into the partition
sudo cryptsetup luksAddKey $MY_DEV_CRYPT ./enc-key.key
```

**Step2.** Setup auto-mounting using the key file

Edit file `/etc/crypttab` and add a line:
```text
# Use Syntax1 or Syntax2
# Syntax1: Auto-mounting using a key file
<MY_DEVMP_CRYPT_NAME> UUID=<uuid_of_luks_wrapper_partition> <key_file_path> luks,noauto,discard
# Syntax2: Auto-mounting but it requires the user to enter passphrase during booting OS
<MY_DEVMP_CRYPT_NAME> UUID=<uuid_of_luks_wrapper_partition> none            discard

# Example
m_encdata UUID=9736256c-2bc3-48f1-b3e0-5921b9e2bc1b /home/user/enc-key.key luks,noauto,discard
luks-b1c8 UUID=75d77918-c9cb-4dab-88d4-66a3d73cb1c8 none                   discard
```

Edit file `/etc/fstab` and add a line:
```text
# Use Syntax1 or Syntax2
# Syntax1
/dev/mapper/<MY_DEVMP_CRYPT_NAME>    <MY_MOUNTED_PATH>    ext4    auto,rw,async,nouser    0 0
# Syntax2
UUID=<uuid_of_inner_partition>       <MY_MOUNTED_PATH>    ext4    auto,rw,async,nouser    0 0

# Example
/dev/mapper/m_encdata                     /mnt/encdata    ext4    auto,rw,async,nouser    0 0
UUID=e1f4d677-f2a7-4a85-b80b-5815f527342a /home           ext4    defaults                0 0
```

&nbsp;

## Misc

**View partition info**

```shell
sudo cryptsetup -v status $MY_DEVMP_CRYPT_NAME
/dev/mapper/m_encdata is active and is in use.
  type:    LUKS2
  cipher:  aes-xts-plain64
  keysize: 512 bits
  key location: keyring
  device:  /dev/nvme0n1p5
  sector size:  512
  offset:  32768 sectors
  size:    1224704 sectors
  mode:    read/write
  flags:   discards
Command successful.
```

**Open and close the partition**

```shell
# Open using passphrase
sudo cryptsetup luksOpen $MY_DEV_CRYPT $MY_DEVMP_CRYPT_NAME

# Open using key file
sudo cryptsetup luksOpen $MY_DEV_CRYPT $MY_DEVMP_CRYPT_NAME --key-file=./enc-key.key

# Close
sudo cryptsetup luksClose $MY_DEV_CRYPT /dev/mapper/$MY_DEVMP_CRYPT_NAME
```

**Check if passphrase matches with a key slot index**

Method 1:

```shell
# Check if passphrase matches with key slot index = 0
sudo cryptsetup luksOpen --test-passphrase --key-slot 0 $MY_DEV_CRYPT && echo correct
```

Method 2:

```shell
sudo cryptsetup --verbose open --test-passphrase $MY_DEV_CRYPT

# Output:
# Enter passphrase for /dev/nvme0n1p5:
# Key slot 2 unlocked.
```

**Add a passphrase into an existing partition**

```shell
sudo cryptsetup luksAddKey $MY_DEV_CRYPT
# Need to enter a valid passphrase first to process
```

**Dump info of the wrapper partition**

```shell
# Method 1
sudo cryptsetup luksDump $MY_DEV_CRYPT
# Method 2
# <path_to_dump_header_file> can be $MY_PARTITION_LABEL.luks2.bin
sudo cryptsetup luksDump <path_to_dump_header_file>


# Output example:
LUKS header information
Version:       	2
Epoch:         	4
Metadata area: 	16384 [bytes]
Keyslots area: 	16744448 [bytes]
UUID:          	9736256c-2bc3-48f1-b3e0-5921b9e2bc1b
Label:         	(no label)
Subsystem:     	(no subsystem)
Flags:       	(no flags)

Data segments:
  0: crypt
	offset: 16777216 [bytes]
	length: (whole device)
	cipher: aes-xts-plain64
	sector: 512 [bytes]

Keyslots:
  0: luks2
	Key:        512 bits
	Priority:   normal
	Cipher:     aes-xts-plain64
	Cipher key: 512 bits
	PBKDF:      argon2id
	Time cost:  6
	Memory:     1048576
	Threads:    4
	Salt:       8b 02 bc 2c 49 2a 35 b2 51 79 02 ff 73 49 9f 98
	            71 d4 52 30 cb d2 78 62 eb 40 73 5c 89 f0 46 ea
	AF stripes: 4000
	AF hash:    sha256
	Area offset:32768 [bytes]
	Area length:258048 [bytes]
	Digest ID:  0
  1: luks2
	Key:        512 bits
	Priority:   normal
	Cipher:     aes-xts-plain64
	Cipher key: 512 bits
	PBKDF:      argon2id
	Time cost:  6
	Memory:     1048576
	Threads:    4
	Salt:       3a 50 c4 53 26 9b 0c 4e 51 58 f2 13 6d b9 84 12
	            7d da ac 4f 25 1c 13 ab 6a c8 fe 5f a8 4f d3 f5
	AF stripes: 4000
	AF hash:    sha256
	Area offset:290816 [bytes]
	Area length:258048 [bytes]
	Digest ID:  0
Tokens:
Digests:
  0: pbkdf2
	Hash:       sha256
	Iterations: 118724
	Salt:       1e f5 a7 5e cd 51 7d 43 3a 54 87 e8 a8 eb 46 9d
	            a9 dd e6 76 c9 62 7e f4 a7 56 16 c6 fb 50 da 81
	Digest:     90 8e 83 05 7c 89 ca cf e7 dc 16 09 4d fe 97 41
	            2b 31 12 72 79 8e 63 fc ab 0b b0 b8 9f 03 fc 72
```

**Backup and restore header**

Backup header:

```shell
# Syntax: sudo cryptsetup luksHeaderBackup $MY_DEV_CRYPT --header-backup-file <output_header_file_path>
sudo cryptsetup luksHeaderBackup $MY_DEV_CRYPT --header-backup-file ./$MY_PARTITION_LABEL.luks2.bin

sudo chmod 644 ./$MY_PARTITION_LABEL.luks2.bin
sudo chown $USER:$USER ./$MY_PARTITION_LABEL.luks2.bin
```

Restore header:

```shell
# Syntax: sudo cryptsetup luksHeaderRestore $MY_DEV_CRYPT --header-backup-file <input_header_file_path>
sudo cryptsetup luksHeaderRestore $MY_DEV_CRYPT --header-backup-file ./$MY_PARTITION_LABEL.luks2.bin
```
