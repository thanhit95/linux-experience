# COMMAND: UPDATE-ALTERNATIVES

## Description

```update-alternatives``` is a symbolic link management system for Linux. It is supported by default in Debian-based distros.

```update-alternatives```, in a simply put, helps we make a command ```X``` global executable and manages all alternatives of ```X```.

In this article, supposed that we install Java JDK and make ```java``` global executable.

&nbsp;

## List of commands

### 1. Display all alternatives of ```java``` command

```shell
$ sudo update-alternatives --display java

java - auto mode
  link best version is /home/vmadmin/Downloads/jdk-16.0.2/bin/java
  link currently points to /home/vmadmin/Downloads/jdk-16.0.2/bin/java
  link java is /usr/bin/java
/home/vmadmin/Downloads/java-se-8u41-ri/bin/java - priority 800
/home/vmadmin/Downloads/jdk-16.0.2/bin/java - priority 1600
```

### 2. Make JDK public (i.e. to add a "java" alternative)

```update-alternatives --install <link> <name> <path> <priority>```, where:

- ```link```: should be ```/usr/bin/java```
- ```name```: should be ```java```, i.e. the global command name.
- ```path```: path to executable ```java``` in JDK directory.
- ```priority```: should be the same as JDK SE version.

For an example:

```sudo update-alternatives --install /usr/bin/java java jdk-path/bin/java 1600```

### 3. Remove an alternative

```sudo update-alternatives --remove java /jdk-path/bin/java```

### 4. Configure the alternative

This command help we choose a default ```java``` command:

```shell
$ sudo update-alternatives --config java

There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                              Priority   Status
------------------------------------------------------------
* 0            /home/vmadmin/Downloads/jdk-16.0.2/bin/java        1600      auto mode
  1            /home/vmadmin/Downloads/java-se-8u41-ri/bin/java   800       manual mode
  2            /home/vmadmin/Downloads/jdk-16.0.2/bin/java        1600      manual mode

Press <enter> to keep the current choice[*], or type selection number:
```

&nbsp;

## What does ```update-alternatives --install``` do?

- Firstly, it creates a symbolic link to original execute JDK in ```/etc/alternatives```.
  - For an example, it creates ```/etc/alternatives/java``` that links to ```/home/vmadmin/Downloads/jdk-16.0.2/bin/java```.
- Secondly, it creates a symbolic link ```/usr/bin/java``` that links to ```/etc/alternatives/java```.

The diagram is:

```/usr/bin/java --> /etc/alternatives/java --> /home/vmadmin/Downloads/jdk-16.0.2/bin/java```

If we want to change JDK, ```update-alternatives --config``` will update the link of ```/etc/alternatives/java```.
