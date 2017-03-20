Writing Todo:

==================

! and history in general
* and **
?, ^, &&, |
{,}      # examples diffing, ‘sudo ln -s /etc/nginx/sites-{available,enabled}/pk.local’
find and grep
ss

$PAGER
$EDITOR
History, Substitution, Navigation, Utilities, Redirection. PATH and CDPATH Omitting variables and control structures.


==================


# A Brief Introduction to the Shell for Novice Developers

©2017 Patrick 'Kai' Leahy. Licensed CC0, but attribution would be polite.

## Intended Audience

This guide is specifically written for my classmates at Epicodus. I started there a week ago (3/13/17) and it became clear that some supplementary material to the coursework would be appreciated.

## #Assumed Knowledge

(This page, essentially)[https://www.learnhowtoprogram.com/intro-to-programming/getting-started-with-intro-to-programming/introduction-to-the-command-line]. You should know what cd, ls, touch, mkdir, mv and rm do. Also, this guide uses
```shell
$
````
to represent the shell.

## Summary of Content

This guide will cover basic shell concepts and some recommendations for configuration. It will not cover scripting concerns or programming concepts such as loops and other control structures, and it will not cover variable/string manipulation. Those are extremely powerful features but if there's any truth to the (classic quip by jwz)[http://regex.info/blog/2006-09-15/247] about the challenges of regular expressions, that goes double for Bash. This guide will also omit a full description of regular expressions.

## About the Author

Hi, I'm Kai. I'm originally from rural Alaska, I've bounced around the States and spent four years or so in Central America. I really wanted to stay down there and so I talked my way into a programming job and taught myself what I needed to know as I went. That worked out more or less okay but in the six years since then I've been mostly stuck working on horrible legacy PHP projects, and Central America didn't turn out to be a good way to meet business contacts. Other than that I've used Linux exclusively for about ten years now, and messed around with Ruby to the tune of reading six or seven books and playing with rails and pry. I am currently attending Epicodus and I think that will be a necessary part of my skills development, but I'm also having a bit of an issue making rent so any sort of assistance, advice or job leads would help keep me housed.

## Starting Out With the Shell

![Bash command prompt][prompt1]
Welcome to the command line. The shell, like git, is a tool that developers love to hate. They both have complicated syntax and a tendency to punish errant keystrokes. However, they're useful enough that we put up with the rough edges, and the larger the codebase you're working with, the more important they become. It becomes clear pretty quickly that things like mkdir and touch are much faster than trying to create file and directory structures, but the rest of the shell doesn't exactly go out of its way to teach you what you can do with it, and the Advanced Bash Scripting Guide is not exactly light reading. This is also not light reading but should provide a practical introduction to most concepts and some example usage.

Learning the shell has been a ten-year process for me, and I still do not consider myself truly expert. Here's hoping I can save some time for other people.

## #What is a shell?

The shell is the thing that executes commands and spits text back at you. You generally use this through a terminal program like OSX's Terminal.app. In more general terms, the shell is an interpreter, which means that it's actually a complete programming language of its own. You'll also see the acronym "CLI" thrown around, that stands for "command line interface" as opposed to a "GUI" or "graphical user interface". Either way it's a way to talk to the computer in a fairly direct manner.

That is a warning, by the way. The problem with programming is that the computer always does exactly what you tell it to. There is a mistake you can make which is worth explaining before we even get past the introduction. So you want to remove all the files and folders in some directory, and what you intended to type was this:
```shell
$ rm -rf /some/path/to/a/file
```
But you make a small typo:
```shell
$ rm -rf / some/path/to/a/file
```
This will remove every file that you have access to. If you have administrator rights you can wipe the whole machine, and OSX will not stop you from doing this. Be careful what you type. Test commands to see what they do (for example, with `:p`) before trying them for real. Most of the time the only risk you'll run is having to restore something from source control or backups, but of course that requires you to use those things. And of course the flip side of this is that if you ever do want to do something crazy like type eight characters and wipe the whole machine, you totally can. Just remember, with great power comes great responsibility. And yes, that's a line worth stealing :)

## ## Bash vs zsh

By default on most systems the shell interpreter is a program called Bash. This is basically due to inertia at this point: if you're a shell script writer and don't know in what sort of environment your code will run in, it's best to target Bash since it's the default. You as a developer should probably use something that sucks somewhat less. My recommendation is to use zsh in combination with the excellent framework (Prezto)[prezto]. This guide will note differences between the two where appropriate, but my advice is to just learn zsh.

Bash as a programming language is primitive and ugly as sin, but it will probably run on any Unix-based system without modification. If you really need to be sure of the broadest possible compatibility, there's an even more primitive version of Bash called POSIX, of which you need to know only that it exists and that if you have to worry about what exactly it is you should probably seek another solution.

## Navigation

You probably know that you can press the arrow keys up and down to go through commands you've entered before, but there are some other keyboard commands that do useful things. The way these are typically written is with a caret (^) substituting for the Control key (Windows) or Command key (Mac). There's a reason for that, but it's kinda arcane.

The first one you should know is `^C` (ctrl+C). This stops whatever command is currently executing, unless you've locked the system up. If that happens you can probably still use the `kill` command, but you may also contemplate the failures in life that have brought you that point, your worth as a human being, and the fate of your homework assignment before hitting that panic button.

Usually holding CTRL/CMD and pressing right or left will scroll by word instead of by character. Here are a few more commands

* `^D` : this technically means 'end of file' but you use it to get out of things. If you're using zsh but bash is your default shell, pressing this will get you out of zsh and back to bash. This is also what you use to close SSH connections.
* `^A` : jumps to the beginning of the line. You use this when you forget something at the beginning of a command
* `^E` : jumps to the end of the line.
* `^P` and `^N` move backwards and forwards (respectively) in history.
* `^L` : clears the screen
* `^R` : searches your history backwards. This is amazing. My typical use case is when I try a command and it doesn't work, then I spend some time debugging why, then whenever I get done I don't want to hit up a bunch of times looking for that previous command. Hit ^G or escape to stop searching.

You can also search forwards in history, but the default command for this (`^S`) is usually bound to something else. So in order to do that, you need to have the following in your `.bashrc` or `.zshrc` configuration file.
`stty -ixon`

For a fuller discussion of the configuration files, see [Configuration].

## Syntax (strings, variables)

Bash actually doesn't have a lot of syntax. Pretty much things are commands, strings, or variables.

## #Variables
Variables are declared like so:
```shell
$ FOO="some string"
```
and used like this:
```shell
$ echo $FOO
some string
```
or
```shell
$ echo ${FOO}
some string
```

And you think, variables, great! I'm a programmer, I use those all the time! Well, not in shell scripts you don't, because you're not developing code that way (hopefully). Variables are mentioned here for completeness and so you know what they look like. Try to avoid needing to use them.

## #Strings

There are several ways to write strings on the command line. Using single quotes:
```shell
$ 'this is a string!'
```
Double quotes
```shell
$ "This is also a string"

```
Heredoc
```shell
$ <<EOM
This is a multi-line string. It's closed by 'EOM' on a line by itself
  EOM <-- this does not end the string!
EOM
```
Strings enclosed in single quotes are evaluated literally (no interpolation or substitution is performed).
```shell
$ FOO='bar'
$ echo 'This string has a $FOO'
This string has a $FOO
```
Double quoted strings will do interpolation and/or substitution
## Redirection

## History

## Substitution

## Environment Variables

## Configuration

## Cheat Sheet

It is strongly recommended that you create your own. This will firm up memory associations.

[prezto]: https://github.com/sorin-ionescu/prezto
[prompt1]: prompt1.png
