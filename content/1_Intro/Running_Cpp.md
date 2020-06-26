---
id: running-cpp
title: Running C++
author: Nathan Wang, Benjamin Qi, Anthony Wang
description: Options for running C++ both online and locally.
---

Please let us know if these installation instructions do not work for you.

# Using C++ Online

 - [OnlineGDB](https://www.onlinegdb.com/)
   - online compiler with an embedded GDB debugger
   - can be buggy sometimes
   - supports files and file I/O
 - [CSAcademy](https://csacademy.com/workspace/)
   - pretty nice (unless you get "Estimated Queue Time: ...")
   - "saved locally" will not save your code if you close the tab, press Command-S to save.
 - [Ideone](http://ideone.com/)
   - okay ... has the bare minimum you need for running C++
   - make sure your code is not public
   - sometimes erases your code when you first create it (so get in the habit of copying your code first)

You can share code with [pastebin](https://pastebin.com/) or [hastebin](https://hastebin.com/).

# Using an IDE

These often have C++ support already built-in.

 - [Visual Studio Code](https://code.visualstudio.com/)
   - lightweight, fast IDE, but requires some configuration
   - see [PAPC Ch 2.1](http://www.csc.kth.se/~jsannemo/slask/main.pdf) for setup instructions
 - [Visual Studio](https://visualstudio.microsoft.com/vs/)
   - heavier cousin of VS Code, VS Code is better for competitive programming
 - [Geany](https://www.geany.org/)
   - Ben: I used at IOI
 - [Codeblocks](http://www.codeblocks.org/)
   - bad on Mac
 - [XCode](https://developer.apple.com/xcode/)
   - Mac only
 - [CLion](https://www.jetbrains.com/clion/)
   - requires a license, but [free for students](https://www.jetbrains.com/community/education/#students)

# Using Command Line

Alternatively, run C++ from the command line and use a text editor of your choice.

## Text Editors

 - [Sublime Text 3](https://www.sublimetext.com/)
   - fast, lightweight text editor for Windows, Mac, and Linux
   - [Editing Build Settings](https://stackoverflow.com/questions/23789410/how-to-edit-sublime-text-build-settings)
     - no need to do this if you just use command line to compile & run
   - [FastOlympicCoding Addon](https://github.com/Jatana/FastOlympicCoding)
     - see "Debugging" for another way to stress test
   - [Sublime Snippets](https://www.granneman.com/webdev/editors/sublime-text/top-features-of-sublime-text/quickly-insert-text-and-code-with-sublime-text-snippets)
     - Ben - I use to insert templates
   - [Symlink](https://www.sublimetext.com/docs/3/osx_command_line.html) 
     - Ben - Using `/usr/local/bin/subl` instead of `~/bin/subl` worked for me on OS X Mojave.
 - [Atom](https://atom.io/)
   - another text editor for Windows, Mac, and Linux from the makers of Github
 - [Vim](https://www.vim.org/) 
   - classic text editor, usually preinstalled on Mac and Linux, and also available for Windows
   - probably easiest way to print syntax-highlighted code on Mac, see the response to [this post](https://stackoverflow.com/questions/1656914/printing-code-with-syntax-highlighting)

## On Linux

GCC is usually preinstalled on most Linux distros. You can check if it is installed with

```
whereis g++
```

If it is not preinstalled, you can probably install it using your distro's package manager.

## On Windows

### MinGW

One option is [MinGW](http://mingw.org/).

First, download and run the [MinGW installer](https://osdn.net/projects/mingw/downloads/68260/mingw-get-setup.exe/). Once it's installed, open the MinGW Installation Manager, click on Basic Setup on the left, and select `mingw32-gcc-g++-bin` for installation.

[Adding MinGW to PATH](https://www.rose-hulman.edu/class/csse/resources/MinGW/installation.htm)

### WSL

Another good option is Windows Subsystem for Linux (WSL) which is what I (Anthony) personally use, although it may be more difficult to properly set up.

[VSCode Docs for WSL](https://code.visualstudio.com/docs/cpp/config-wsl) (difficult for beginners)

Nathan Wang: If you want to code in (neo)vim, you can install WSL and code through WSL bash.

- Note that WSL has a max stack size of 64MB; I am unsure if this limitation is resolved yet.
- Note that WSL/vim clipboard integration is imperfect.

## On Mac

[Clang](https://en.wikipedia.org/wiki/Clang) is the default compiler for Mac OS X, but you should use [GCC](https://en.wikipedia.org/wiki/GNU_Compiler_Collection)'s g++ since that's what [USACO](http://www.usaco.org/index.php?page=instructions) uses to compile your code.

### Installation

 1. Open the **Terminal** application and familiarize yourself with some basic commands. 

    - [Intro to OS X Command Line](https://blog.teamtreehouse.com/introduction-to-the-mac-os-x-command-line). 
    - [Mac Terminal Cheat Sheet](https://www.makeuseof.com/tag/mac-terminal-commands-cheat-sheet/)

 2. Install XCode command line tools.

    ```
    xcode-select --install
    ```

    If you previously installed these you may need to update them:

    ```
    softwareupdate --list # list updates
    softwareupdate -i -a # installs all updates
    ```

 3. Install [Homebrew](https://brew.sh/). 

 4. Install gcc with Homebrew.

    ```
    brew install gcc
    ```

    According to [this](https://stackoverflow.com/questions/30998890/installing-opencv-with-brew-never-finishes) if `brew` doesn't seem to finish for a long time then 

    ```
    brew install gcc --force-bottle
    ```

    probably suffices.

 5. You should be able to compile with `g++` or maybe `g++-#`, where # is the version number (ex. 9). Running the following command

    ```
    g++-9 --version
    ```

    should display something like this:

    ```
    g++-9 (Homebrew GCC 9.2.0_2) 9.2.0
    Copyright (C) 2019 Free Software Foundation, Inc.
    This is free software; see the source for copying conditions.  There is NO
    warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
    ```

## Running With the Command Line

Consider a simple program such as the following, which we'll save in `name.cpp`.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
  int x; cin >> x;
  cout << "FOUND " << x << "\n";
}
```

It's not hard to [compile & run a C++ program](https://www.tutorialspoint.com/How-to-compile-and-run-the-Cplusplus-program). First, open up Powershell on Windows, Terminal on Mac, or your distro's terminal in Linux. We can compile `name.cpp` into an executable named `name` with the following command:

```
g++ name.cpp -o name
```

Then we can execute the program:

```
./name
```

If you type some integer and then press enter, then the program should produce output. We can write both of these commands in a single line:

```
g++ name.cpp -o name && ./name
```

### Redirecting Input & Output

If you want to read input from `inp.txt` and write to `out.txt`, then use the following:

```
./name < inp.txt > out.txt
```

See "Intro - Introductory Problems" for how to do file input and output within the program.

### Compiler Options (aka Flags)

Use [compiler flags](https://developers.redhat.com/blog/2018/03/21/compiler-and-linker-flags-gcc/) to change the way GCC compiles your code. Usually, we use the following in place of `g++ name.cpp -o name`:
 
`g++ -std=c++17 -O2 name.cpp -o name -Wall -Wextra -Wshadow`

Explanation:

 - `-O2` tells `g++` to compile your code to run more quickly (see [here](https://www.rapidtables.com/code/linux/gcc/gcc-o.html))
 - `-std=c++17` allows you to use features that were added to C++ in 2017. USACO currently uses `-std=c++11`.
 - `-Wall -Wextra -Wshadow` checks your program for common errors. See "General - Debugging" for more information.
 - [Summary of Options](https://gcc.gnu.org/onlinedocs/gcc/Option-Summary.html)

You should always compile with these flags. 

### Adding Shortcuts (Mac and Linux only)

(alternatives for Windows?)

Of course, retyping the flags above can get tedious. You should define shortcuts so you don't need to type them every time!

[Aliases in Terminal](https://jonsuh.com/blog/bash-command-line-shortcuts/)

Open your bash profile with a text editor such as gedit (or sublime text).

```
brew install gedit
gedit ~/.zshenv
```

You can add **aliases** and **functions** here, such as the following to compile and run C++. 

```
co() { g++ -std=c++17 -O2 -o $1 $1.cpp -Wall -Wextra -Wshadow; }
run() { co $1 && ./$1 & fg; }
```

Now you can easily compile and run `name.cpp` from the command line with `co name && ./name` or `run name`. Note that all occurrences of `$1` in the function are replaced with `name`.