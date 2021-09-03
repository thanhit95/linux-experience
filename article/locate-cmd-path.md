# LOCATE COMMAND PATH

For a long time, `which` is used for looking for the path to an executable. However, we should avoid `which`. The reason comes from the history, that `which` has different behaviour, different syntax in various Linux distros.

Nowadays, `type` and `command -v` are ubiquitous in all the Bourne-like shells.

Have a look at my example:

```shell
$ type ls
ls is /usr/bin/ls

$ command -v ls
/usr/bin/ls

$ type java
java is /usr/lib/jvm/jdk-16/bin/java

$ command -v java
/usr/lib/jvm/jdk-16/bin/java
```

Another example that is useful for me:

```shell
$ alias ll="ls -l"

$ type ll
ll is an alias for ls -l

$ command -v ll
alias ll='ls -l'
```

&nbsp;

Of course, today we can still use `which` and several utilities acting the same as `type` and `command -v`.

```shell
$ which ls
/usr/bin/ls

$ which ll
ll: aliased to ls -l

$ where ls
/usr/bin/ls

$ whence ls
/usr/bin/ls

$ hash -v ls
ls=/usr/bin/ls

$ whereis ls
ls: /usr/bin/ls /usr/share/man/man1p/ls.1p.gz /usr/share/man/man1/ls.1.gz
```
