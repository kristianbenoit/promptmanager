promptmanager
=============

A bash prompt manager with themes, colors and dynamic elements like python
virtualenv.

Try
---

To try, from bash, you can source like so:
$ source promptmanager
$ source promptrc

Install
-------

To install, copy promptmanager and promptrc to /etc and userpromptrc to
"/etc/skel/".

$ sudo cp promptmanager promptrc /etc/
$ sudo cp userpromptrc /etc/skel/.skel

Instead of having it's own file in the skel, you add userpromptrc to
"/etc/skel/.bashrc".

$ sudo bash -c 'cat userpromptrc >> /etc/skel/.bashrc'

You can also copy it to $HOME/.promptrc.

$ cp userpromptrc $HOME/.promptrc

Now you need to source /etc/promptmanager from /etc/profile and that depends on
you distribution.

Configure
---------

### Set a default prompt ###

```bash
PS1_Clear
PS1_Push_Widget '\[$PS1_COLOR_LOW\]\d (\[$PS1_COLOR_MEDIUM\]\@\[$PS1_COLOR_LOW\]) on tty\l'
PS1_Push_Widget '\[$PS1_COLOR_HIGH\]$?\[$PS1_COLOR_BRACKET\]|\[$PS1_COLOR_HIGH\]\j\[$PS1_COLOR_LOW\]zZ'
PS1_Push_Dynamic_Content
PS1_Push_NewLine
PS1_Push_Widget '\[$PS1_COLOR_USER\]\u\[$PS1_COLOR_BRACKET\]@\[$PS1_COLOR_HOST\]\h \[$PS1_COLOR_MEDIUM\]\W'
```

### Also set a PS2 ###

```bash
PS1_PS2='"\[$PS1_COLOR_BRACKET\][\[$PS1_COLOR_LOW\]*\[$PS1_COLOR_BRACKET\]>\[$rst\] "'
```

### Then choose a theme or Render ###

```bash
PS1_Theme Kristian
PS1_Theme Hulk
PS1_Theme Bunny
PS1_Theme Princess
PS1_Theme Tux
PS1_Theme BnW
PS1_Theme Plain
PS1_Render
```
