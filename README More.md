## *Simpulse* Readme More

As the *simpulse* document said, it is a C++/python library for simulating FRB's and pulsars.

https://github.com/kmsmith137/simpulse/tree/master

However, in the author's README, there aren't enough instructions, especially for Mac with Apple silicon 🤯

So, I wrote this brief document as a supplement, perhaps it could be helpful for your installation.

###### Two general tips:

1. Python2 environment

2. X86_64 architecture

My device: MacBook Air 2020 (M1), MacOS 14.1.2 

Terminal: Version 2.14, zsh shell with Command Line Tools15

**Friendly reminder**:

I'm a beginner, so please forgive my mistake if it is occur.

----

##### 1. Python2 environment

Python2 is easy for installing even you have installed python3.

However if you want to use python2 in the notebook of Jupyter, you need set up an virtual environment and py2 kernel.

It is not a hard work, 

----

##### 2. Architecture

- **Enter Rosetta !!!**

❗️*IMPORTANT❗️*

The *Simpulse* can't install under arm64 with M1.

Set Terminal in the application folder/utilities, open using Rosetta

- **Check environment **

Type the code in Terminal

```shell
uname -m
```

and it will show 

```shell
x86_64
```

If you solve this problem, I guess half of the installation work is already done 👍

- **Install brew under x86**

Need to uninstall the brew in the original path, perhaps is /opt/homebrew. Then install under Rosetta x86_64.

```shell
sudo rm -rf /opt/homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Maybe also need to give permissions, and checking the version of brew.

```shell
sudo chown -R $(whoami) /usr/local
brew --version
```

- **Install FFTW**

Using brew to install, just like regular situation. Maybe need to uninstall the old version first.

```shell
brew uninstall fftw
brew install fftw
```

- **Change paths you need**

Maybe need to change/add paths in both of them

```shell
vim ~/.zprofile
vim ~/.bash_profile 
```

Here is mine

```shell
export PATH=$PATH:/usr/local/Cellar/fftw/3.3.10_1/include
export PATH=$PATH:/usr/local/Cellar/fftw/3.3.10_1/bin
export PATH=$PATH:/usr/local/Cellar/fftw/3.3.10_1/lib/pkgconfig
export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/Cellar/fftw/3.3.10_1/lib
export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/Cellar/fftw/3.3.10_1/lib/cmake/fftw3
```

Need refresh paths

```shell
source ~/.bash_profile
source ~/.zprofile
```

It shoud be noted that when adding the *FFTW3* library files, simply linking to the *lib* folder is not sufficient. You also need to locate its subfolders, /cmake/fftw3. Meanwhile, *cmake* folder is in many lib files, which is easy to miss, especially when you are sorting by file type 😅

- **Make install**

```shell
make all install
```

Perhaps need (I needed)

```shell
sudo make install
```

Finally, then everything goes well! ✌️

Meanwhile, if the makefile has completed, and the *simpulse* module has added in python, Terminal doesn't need to run under Rosetta.
