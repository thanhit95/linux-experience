# JAVA JDK INSTALLATION

## STANDARD METHOD

### Ubuntu

```shell
sudo apt install openjdk
```

### Manjaro

Enable AUR, install package ```java-openjdk-bin```.

---

## MANUAL METHOD

### 1. Instructions

**Step 01.** Download Open JDK as an archive file.

**Step 02.** Extract downloaded archive to ```/usr/lib/jvm```.

Many softwares identify JDK/JRE in ```/usr/lib/jvm```.

Expected result (if I use JDK 16):

```shell
$ ls /usr/lib/jvm
jdk-16

$ ls /usr/lib/jvm/jdk-16
bin  conf  include  jmods  legal  lib  release
```

Tip. In case using more than one JDK (such as using both JDK-8 and JDK-16), we should make a symbolic link ```default-jdk``` that points to the default JDK.

```shell
$ ls -l /usr/lib/jvm
drwxr-xr-x 2 root root 4096 Aug 31 09:38 jdk-16
drwxr-xr-x 2 root root 4096 Aug 31 09:42 jdk-8

$ sudo ln -s /usr/lib/jvm/jdk-16 default-jdk

$ ls -l /usr/lib/jvm
drwxr-xr-x 2 root root 4096 Aug 31 09:38 jdk-16
drwxr-xr-x 2 root root 4096 Aug 31 09:42 jdk-8
lrwxrwxrwx 1 root root   10 Aug 31 09:43 default-jdk -> /usr/lib/jvm/jdk-16
```

**Step 03.** Make ```java``` global executable.

The purpose in detail: Make ```/usr/lib/jvm/default-jdk/bin/java``` global executable.

Edit file ```/etc/environment```, add these lines:

```text
JAVA_HOME=/usr/lib/jvm/default-jdk
PATH="$JAVA_HOME/bin:$PATH"
```

To take effects, please restart computer. Now we verify the result:

```shell
$ java --version
openjdk 16.0.2 2021-07-20
OpenJDK Runtime Environment (build 16.0.2+7-67)
OpenJDK 64-Bit Server VM (build 16.0.2+7-67, mixed mode, sharing)
```

&nbsp;

### 2. Special method for Ubuntu

Tired of making ```java``` public using manual method, or tired of switching between many JDKs? Debian-based distros support command ```update-alternatives``` that might make your life easier.

Take a look at [cmd/update-alternatives.md](cmd/update-alternatives.md)

Do not forget to make ```javac``` public, too.
