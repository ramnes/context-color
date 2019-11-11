context-color
=============

:rainbow: To each context its own shell color

![gif](demo.gif)

`context-color` is a simple script that, when executed, outputs a color based
on a command output's hash.


Example
-------

Once installed somewhere in your `$PATH`, it allows you to do things like this:

```bash
export PS1="$(context-color -p)$PS1\[\e[0m\]"
```

(where `--prompt/-p` is the switch so that the color is escaped for prompts,
and `\[\e[0m\]` the escape sequence to reset color)

If your prompt does not use colors already, this example would customize it so
that its color changes according to the current context.

The default context command (i.e. the command that is used to generate the
hash) is `whoami; hostname`.  If you would just want the color to change
according to the hostname, you would change the `$CONTEXT` variable environment
(`export CONTEXT="hostname"`) or simply use the `--context/-c` option
(`context-color -c "hostname"`).

Then you could make this customization permanent by adding this line to your
`~/.bashrc`, or to the system-wide `bashrc` file (most likely somewhere in
`/etc/`, depending on your distribution) if you would want all users to benefit
from this.

If you are working with several machines, you could either do that manipulation
on every host, or use something like
[Russell91/sshrc](https://github.com/Russell91/sshrc/).


Install
-------

Something in those lines should do it:

```bash
cd .local/bin/
wget https://raw.githubusercontent.com/ramnes/context-color/master/context-color
chmod a+x context-color
```

This snippet assumes that `~/.local/bin/` is in your `$PATH` environment
variable. If it is not, you can either put `context-color` somewhere else
(`/usr/local/bin/`, for example), or insert `~/.local/bin/` into your `$PATH`,
by adding this line into your bash configuration:

```bash
export PATH="~/.local/bin/:$PATH"
```


Usage
-----

```
usage: context-color [OPTIONS]

Print a color sequence based on a command output's hash.

COMMON OPTIONS:
    --help, -h          Print this help.
    --background, -b    Use a background sequence rather than foreground.
    --id, -i            Print the color id rather than the color sequence.
    --prompt, -p        Declare the sequence as non-printable for prompts.

    --context <command>, -c <command>
                        Define the context command on which result the color
                        will be generated.
                        The default context is "whoami; hostname".

    --exclude <colors>, -e <colors>
                        Comma separated list of color ids not to be used.
                        Multiple --exclude/-e arguments can be specified.
                        The default excluded colors are: "0,7,15"

    --method <method>, -m <method>
                        Choose which hash method to use. "sum" will tend to
                        give adjacent colors for adjacent context outputs.
                        "md5sum" will give more randomization on colors.
                        The default method is: "sum"

DEBUG OPTIONS:
    --debug, -d         Output the sequence as a human-readable string and more
                        useful information.
    --force <color>, -f <color>
                        Ignore the context and force a color id instead.
```

The `-p` option must be used if you use `context-color` inside a prompt. It
makes your shell understand that the color sequence characters won't be used
when it's trying to guess the space left on the current line. See issue
[#8](https://github.com/ramnes/context-color/issues/8) for a good description
of what happens if you do not put `-p` in that situation.


Credits
-------

The original implementation was based on *J Earls* answer on
[this SuperUser question](https://superuser.com/questions/1123671).

He's the real MVP. :ok_hand:


License
-------

GNU GPL v3
