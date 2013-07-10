promptmanager
=============

A bash prompt manager with themes, colors and dynamic elements.
This is useful so that your prompt reflect the environment you are in like
debug mode or python virtualenv. Usually, these just add element to your PS1,
no colors, no question where to add it. That's where the prompt manager is
useful.

Example use
-----------

### Currently ###

Suppose your have such prompt :

```bash
[username@hostname:~]$
```

Then you activate a python virtualenv named pydev, your prompt look like so
without color to (pydev) :

```bash
(pydev)[username@hostname:~]$
```
### With promptmanager ###

Since the default might not be what you want, promptmanager give the tools to
get what you want. If you tweek the activate script, your prompt might be
colored including the pydev and look
like so :

```bash
[username@hostname:~][pydev]$
```

It can be easily set to your liking, but by default the prompt is configured
like so :

```bash
[Mer nov 07 (04:38 ) on tty0][0|1zZ]
[username@hostname ~]$
```

If you source the above mentioned virtualenv activate script and some other
script that set you in debug mode you'll end up with a prompt like so :

```bash
[Mer nov 07 (04:38 ) on tty0][0|1zZ][pydev][debug]
[username@hostname ~]$
```

Try
---

To try, from bash, you can source like so:

```bash
source promptmanager
source promptrc
```

Add a DEBUG element to your prompt :

```bash
PS1_Push_Element debug DEBUG
```

Change your theme :

```bash
PS1_Theme Hulk
```

Remove the debug element:

```bash
PS1_Pop_Element debug
```

Usage (Interface)
-----------------

When you want to set a state in the prompt, use these methods to add/remove
elements dynamically from your script. This will add support for promptmanager.

```bash
# Add element
if `declare -f PS1_Push_Element > /dev/null`
then
    PS1_Push_Element debug DEBUG
else
    _old_PS1=$PS1
    PS1="(stuff you want to add)$PS1"
fi

#Remove Element
if `declare -f PS1_Pop_Element > /dev/null`
then
    PS1_Pop_Element debug
else
    PS1=$_old_PS1
fi
```


Configure
---------

### Set a default prompt ###
This is the prompt you will get by default

```bash
PS1_Clear
PS1_Push_Widget '\[$PS1_COLOR_LOW\]\d (\[$PS1_COLOR_MEDIUM\]\@\[$PS1_COLOR_LOW\]) on tty\l'
PS1_Push_Widget '\[$PS1_COLOR_HIGH\]$?\[$PS1_COLOR_BRACKET\]|\[$PS1_COLOR_HIGH\]\j\[$PS1_COLOR_LOW\]zZ'
PS1_Push_Dynamic_Content
PS1_Push_NewLine
PS1_Push_Widget '\[$PS1_COLOR_USER\]\u\[$PS1_COLOR_BRACKET\]@\[$PS1_COLOR_HOST\]\h \[$PS1_COLOR_MEDIUM\]\W'
```

### Also set a PS2 ###
Not yet themable except for colors, but no one really want to add content dynamically to PS2

```bash
PS1_PS2='"\[$PS1_COLOR_BRACKET\][\[$PS1_COLOR_LOW\]*\[$PS1_COLOR_BRACKET\]>\[$rst\] "'
```

### Then choose a theme ###

```bash
PS1_Theme Kristian
PS1_Theme Hulk
PS1_Theme Bunny
PS1_Theme Princess
PS1_Theme Tux
PS1_Theme BnW
PS1_Theme Plain
```

### Or use default set in /etc/promptrc ###
```bash
PS1_Render
```

Themes
------

To define a new theme named BlueSea, according to the colors used in the default prompt, you
need to define a function like so :

```bash
function __PS1_Theme_Blue {
    PS1_COLOR_BRACKET=$BLUE
    PS1_COLOR_LOW=$blu
    PS1_COLOR_MEDIUM=$gre
    PS1_COLOR_HIGH=$GRE
    PS1_COLOR_ROOT=$RED
    PS1_COLOR_USER=$PS1_COLOR_LOW
    PS1_COLOR_HOST=$PS1_COLOR_LOW
    PS1_COLOR_PROMPT=$PS1_COLOR_HIGH
    PS1_BRACKET_OPEN="{"
    PS1_BRACKET_CLOSE="}"
    function PS1_Format_Widget {
        echo "\[$PS1_COLOR_BRACKET\]$PS1_BRACKET_OPEN\[$PS1_COLOR_HIGH\]$1\[$PS1_COLOR_BRACKET\]$PS1_BRACKET_CLOSE"
    }
}
```

This can be done globally in /etc/promptrc or per user in $HOME/.promptrc

Install
-------

To install, copy promptmanager and promptrc to /etc and userpromptrc to
"/etc/skel/".

```bash
sudo cp promptmanager promptrc /etc/
sudo cp userpromptrc /etc/skel/.skel
```

Instead of having it's own file in the skel, you add userpromptrc to
"/etc/skel/.bashrc".

```bash
sudo bash -c 'cat userpromptrc >> /etc/skel/.bashrc'
```
 
You can also copy it to $HOME/.promptrc.

```bash
cp userpromptrc $HOME/.promptrc
```

Now you need to source /etc/promptmanager from /etc/profile and that depends on
you distribution, but look at where it sets PS1 and replace that.
