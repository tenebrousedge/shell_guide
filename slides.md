# How to be Awesome at the Shell
by Kai

---

## About Kai

  * weird
  * from the Internet
  * mostly harmless
  * unreasonably familiar with Linux

---

## Why learn the shell?

The point of programming is to save labor, and saving our own labor has exponential returns. The more time you can spend **thinking** instead of **typing**, the more you can achieve as a programmer, and the more you can change the world.

note: 
That holds true for many other tools as well, but the shell is something that you use every day, and as far as I can tell there's no formal instruction in the shell to be had anywhere.

---

## Bash

Bash is:

  * a command-line interpreter <!-- .element: class="fragment" -->
  * a complete programming language <!-- .element: class="fragment" -->
  * a ridiculous holdover from the 1970s that no one should ever use <!-- .element: class="fragment" -->

note:
Bash is both a bad programming language and a bad interpreter. Use bash to save keystrokes and construct commands. Do not use it for general purpose programming or automating systems processes. bash is great for structured text, preferably many different kinds of structured text

---

## Zsh and Prezto

Do not leave $HOME without them!

* tab complete all the things
  -- partial file names
  -- git branches
  -- rake commands
  -- and more!

* syntax highlighting as you type
* pretty prompts
* useful aliases

---

## Controls

---

## Navigation:

  * up, down : scroll through history
  * Ctrl-A : jump to beginning of line
  * Ctrl-E : jump to end of line
Search:
  * Ctrl-R : search backwards through history.
  * Ctrl-S : search forwards through history

---

## Substitution 

---

## Aliases

These are strings which are expanded when you enter them into the terminal.
Use them to shorten commands:

```shell
$ alias gpo='git push origin HEAD'
$ alias gcm='git checkout master'
```

---

## Curly Brace Substitution

This expands both strings and ranges within curly braces.

```shell
$ echo {string1,string2}/abc
string1/abc string2/abc
```
or
```shell
$ echo {0..3}/{c..f}
0/c 0/d 0/e 0/f 1/c 1/d 1/e 1/f 2/c 2/d 2/e 2/f 3/c 3/d 3/e 3/f
```

---

## Examples

```shell
$ mkdir -p project_name/{img,css,js}
```

```shell
$ ln -s /etc/nginx/sites-{available,enabled}/my_site_config
```

---

## Caret Substitution

Use this when you want to edit one word in the previous command.

```shell
$ echo "some thing"
some thing
$ ^thing^foo^
some foo
```

You can use this to fix typos or if the command you want differs from the previous one by only one word.

---

## Global Substitution

When you want to replace all instances of a string in the previous command, you can use global substitution:

```shell
$ echo 'spam sausage spam spam bacon spam tomato and spam'
spam sausage spam spam bacon spam tomato and spam
$ !!:gs/spam/meow/
meow sausage meow meow bacon meow tomato and meow
```

note:
I have no solid use cases for this, but it's good to know it exists.

---

## History

Bash keeps a record of everything you type, just like Google and the NSA.
You can access this history in various ways. The most important ones are:

* `!!` : the entire previous line
* `!$` : the last word of the previous line
* `!`number : the line of history with the matching number

note:
also introduce history command, !-n notation, and !!:$ !!:^ !!:0

---

## Redirection

---

## Pipes

One of the more significant inventions in programming history. This guy is the heart and soul of the command line.

```shell
$ 
```
---

## Redirection - stderr

---

## Redirection - File IO

---
