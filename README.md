context-color
=============

:rainbow: To each context its own shell color

![gif](demo.gif)


Description
-----------

`context-color` is simple script that, when executed, outputs a color based on
a command output's hash.

For example, once installed somewhere in your `$PATH`, it allows you to do
things like this:

```bash
export PS1="$(context-color -p)$PS1\[\e[0m\]"
```

(where `--prompt/-p` is the switch so that the color is escaped for prompts,
and `\[\e[0m\]` the escape sequence to reset color)

By default, the command used to generate the hash is `whoami; hostname`.  If
you would just want the color to change according to the hostname, you would
change the `$CONTEXT` variable environment (`export CONTEXT="hostname"`) or
simply use the `--context/-c` option (`context-color -c "hostname"`).


Install
-------

Something in those lines should do it:

```bash
cd .local/bin/
wget https://github.com/ramnes/context-color/blob/master/context-color
chmod a+x context-color
```


Usage
-----

```
usage: $PROGNAME [OPTIONS]

Print a color sequence based on different context informations.

OPTIONS:
    --help, -h          Print this help.
    --background, -b    Use a background sequence rather than foreground.
    --prompt, -p        Declare the sequence as non-printable for prompts.

    --context <command>, -c <command>
                        Define the context command on which result the color
                        will be generated.
                        The default context is "whoami; hostname".
```


Credits
-------

The original implementation was based on *J Earls* answer on
[this SuperUser question](https://superuser.com/questions/1123671).

He's the real MVP. :ok_hand:


License
-------

GNU GPL v3
