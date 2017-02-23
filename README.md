# extended_bashrc
## Git branch
This bashrc shows on which repo I am working (and at which branch).

To use this extension, run the following:
<pre>
curl -L https://raw.github.com/git/git/master/contrib/completion/git-prompt.sh > ~/.git-prompt.sh
</pre>
or copy the file .git-prompt.sh from this repo to ~/

Copy the file bashrc_ext to ~/bashrc_ext

Then, alter your .bashrc:

<pre>
vim ~/.bashrc
</pre>

Allow for color prompt in bash. Search for the following lines and alter it accordingly:
<pre>
# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
	# We have color support; assume it's compliant with Ecma-48
	# (ISO/IEC-6429). (Lack of such support is extremely rare, and such
	# a case would tend to support setf rather than setaf.)
	color_prompt=yes
    else
	color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
   PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\[\033[01;31m\]$(__git_ps1 "\n@%s")\[\033[00m\]\$ '
else
   PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac
</pre>

In your ~/.bashrc add the following line after the previous lines:
<pre>
# Overwrites PS1
source ~/.git-prompt.sh
source ~/bashrc_ext
</pre>

## cdp 
cdp enables you to create a config file with directory shorthands, to for example project directories. 
By typing cdp <shorthand> (or by using tab completion) you can quickly change to the configured directory.

In order to use the cd shorthand function, create a config file:

<pre>
~/.cdp.config
</pre>

This is an example cdp.config file:

<pre>
# Config file for cdp shorthand, see https://github.com/mathijsdelangen/extended_bashrc
# Shorthands are only reloaded when bash is reloaded!

# Do not use ~, use $HOME instead
project_paths["home"]="$HOME"
project_paths["project1"]="/data/projects/project1/work"
project_paths["project1-n"]="$HOME/projects/company3/project1/Rxx"
project_paths["paard-docs"]="/data/projects/paard/docs/work"
</pre>


