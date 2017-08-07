# Constructing a useful bash prompt

This is what my bash prompt looks like at the moment:

![](img/prompt_current.png)

and here is what the various parts refer to:

![](img/prompt_current_annot.png)


## What is a bash prompt?

The bash prompt is found __FILL__


The default bash prompt looks like this:

![](img/prompt_default.png)

so fire up your terminal of choice and see that your bash prompt looks similar. The default prompt shows __FILL__, the current directory path relative to `~` and finally a `$`, which marks the end of the prompt and the start of the area that you can type commands.

## Customising the bash prompt

The `.bashrc`, among other things related to how bash functions, is where you can define a custom bash prompt. `.bashrc` is normally found in the root (`~`) directory. Check if you have a `~/.bashrc` using:

```shell
cat ~/.bashrc
```

If bash says that there is no such file, create one using:

```
touch ~/.bashrc
```

Finally, start editing `.bashrc` using your favourite text editor, e.g. `vim`:

```
vim ~/.bashrc
```

### Super basic

To start with, let's replace the default bash prompt with something really simple like this:

![](img/prompt_min.png)

To achieve this, type the following into your `.bashrc`:

```
PS1='$'
```

Then exit the text editor and enter the following into the terminal, which forces bash to reload `.bashrc`:

```shell
source ~/.bashrc
```

PS1 is actually only one of four bash prompts, with PS1 being the default prompt that is shown most of the time; `PS2`,`PS3`,`PS4` and `PROMPT_COMMAND` are used under special conditions. [This article](http://www.thegeekstuff.com/2008/09/bash-shell-take-control-of-ps1-ps2-ps3-ps4-and-prompt_command/) has a good description of what they're used for.

### Incorporating variables

The simplest way to add a variable (i.e. something which changes depending on conditions like the current working directory) is to use one that bash understands by default, [a full list of which can be found here](http://www.gnu.org/software/bash/manual/bashref.html#Controlling-the-Prompt).

Start by adding the time to our simple `$` prompt:

```
PS1='\T $'
```

Note the space between `\T` and `$`. Adding spaces between variables can help everything to look neater.

Read through the list of available variables and add a few to your own prompt. 


### Colours
To change the colours parts of the bash prompt, wrap the variable in ANSI escape sequences, like so:

```
PS1='\[\e[31m\]\w\[\e[m\] \T $'
```

This makes the directory path appear in red text. `31m` is the section of that sequence that actually defines the colour red. 

ANSI escape sequences can also be used to change the background colour of the text, add underlines, make the text bold, or high contrast. I often refer to both [this wikipedia page on ANSI colour codes](http://en.wikipedia.org/wiki/ANSI_escape_code#colors) and [this blog post on jafrog.com](http://www.jafrog.com/2013/11/23/colors-in-terminal) when choosing colour codes.

A more elaborate example:

```
PS1='\[\e[96;1m\]\w\[\e[m\] \T $'
```

Notice how `[\e[m\]` always needs to be placed at the end of the coloured part of the bash prompt, to return the colours to normal.

### Unicode characters
Another way escape sequences can be used is to add unicode characters to the prompt, whether this is a cool lightning bolt, a tick or a cross.


### Formatting 
Brackets, spaces, hyphens, colons etc.

### Building PS1 incrementally
After a while, if your bash prompt becomes long and complicated, your PS1 code may start to look busy and hard to read, but it's easy to restructure the PS1 code to increase readability. In the example below, a long and complicated prompt is rewritten so each part is on a separate line and spaces are given their own lines to make them easier to see. Additionally, this allows each part to have its own comment, further increasing readability:

```
# Messy one liner
PS1='┏[\T] \u@\h \[\e[31m\]\w\[\e[m\]\n┗$ '

# Tidy on multiple lines
PS1='┏'		# Elbow
PS1+='[\T]'	# Time
PS1+=' '	# Space 
PS1+='\u@\h'	# User@hostname
PS1+=' ' 	# Space
PS1+='\[\e[31m\]\w\[\e[m\]'	# current dir
PS1+='\n'	# New line
PS1+='┗'	# Elbow
PS1+='$'	# $
PS1+=' '	# Space
```

### Conditional statements and functions


### Sourcing external scripts
