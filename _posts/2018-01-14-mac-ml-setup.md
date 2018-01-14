---
layout: post
title: "Mac Machine Learning Research & Dev Setup"
excerpt: "A summary of setting up a clean mac for pythonic machine learning research and development."
date: 2018-01-14
disqus_identifier: 20180114
mathjax: true
---

Every year I do a clean install of the latest macOS, to mostly get rid of the things I accumulated throughout the year that I no longer use and force myself to do some house keeping. 
Whether after a clean install or just getting my hands on a new Mac, I find myself doing the same setup process every time - I mostly rely on a python 2 setup.
In this post, I document this workflow for my future self and hopefully for the benefit of others. 

# Before

Back in the day, backing up all my data just before a clean install was a painful process but thanks to iCloud, which now takes care of backing up my bookmarks, passwords, etc, it is now a straightforward step.
All I have to do is copy my files in `~/[username]` to an external hard drive. 
P.S. I do this in addition to the Time Machine backup just in case!

# Format

Prepare a bootable macOS installer, erase the main drive, and install the OS.
A nice guide for this can be found [here](https://www.macrumors.com/how-to/macos-sierra-clean-install/).

# Setup

## Xcode

First, we'll install Xcode and the Command Line Tools from the App Store. 
Don't forget to accept the license agreement after installation before moving on.

## Settings & Software

Second, while Xcode is installing, copy your files back and change the trackpad, keyboard, users, etc. settings to your liking. 
I also have a bunch of dot files that contain paths, aliases, etc. to make things easier. 
[I keep these files in this Github repository](https://github.com/haythamfayek/ConfigFiles), some of these files might be useful.

Also, install your favorite text editor, TeX / iWork / Office, and other software you regularly rely on;
as well as, themes and colors.

## Package Manager

The remainder of the workflow will be run from the terminal.

Install a package manager, [Brew](https://brew.sh) (or [Macports](https://www.macports.org)): 

{% highlight shell %}
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
{% endhighlight %}

## Some Standard Packages

A version control system - [Git](https://git-scm.com/) (or preferred alternative): 

{% highlight shell %}
brew install git
git config --global user.name "Your Name Here"
git config --global user.email "your_email@youremail.com"
git config --global credential.helper osxkeychain
{% endhighlight %}

Python:

{% highlight shell %}
brew install python
{% endhighlight %}

We'll need to add the new python to the path: `PATH="/usr/local/opt/python/libexec/bin:$PATH"`

The world's best text editor :) - [Vim](http://www.vim.org): 

{% highlight shell %}
brew install vim
{% endhighlight %}

[Pathogen](https://github.com/tpope/vim-pathogen) makes it easy to install vim plugins:

{% highlight shell %}
mkdir -p ~/.vim/autoload ~/.vim/bundle && curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
{% endhighlight %}

Some minimal [sensible](https://github.com/tpope/vim-sensible.git) vim settings:

{% highlight shell %}
cd ~/.vim/bundle
git clone git://github.com/tpope/vim-sensible.git
{% endhighlight %}

It's almost always useful to have Node installed:

{% highlight shell %}
brew install node
sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer
{% endhighlight %}

This website is built with jekyll and like Node, it's useful to a have Ruby and RVM installed:

{% highlight shell %}
curl -L https://get.rvm.io | bash -s stable --ruby
gem install jekyll
{% endhighlight %}

## Scientific Stack

A C compiler - [GCC](https://gcc.gnu.org); this is also a dependency for later packages:

{% highlight shell %}
brew install gcc
{% endhighlight %}

[Virtualenv](https://virtualenv.pypa.io/en/stable/) is a tool to create isolated environments that is very handy in managing multiple python projects that require different dependencies:

{% highlight shell %}
pip install virtualenv
{% endhighlight %}

[IPython](http://ipython.readthedocs.io) and [Jupyter](http://jupyter.org) are two great tools for interactive python:

{% highlight shell %}
brew install zeromq
brew install pyqt
pip install ipython
pip install jupyter
{% endhighlight %}

The usual suspects [NumPy](http://www.numpy.org), [SciPy](https://www.scipy.org), [MatPlotLib](https://matplotlib.org):

{% highlight shell %}
pip install numpy
pip install scipy
pip install matplotlib
{% endhighlight %}

(While you're at it, do consider donating :) to the open-source community.)

Finally, the machine learning toys - [tensorflow](https://www.tensorflow.org) and [scikit-learn](http://scikit-learn.org): 

{% highlight shell %}
pip install tensorflow
pip install scikit-learn
{% endhighlight %}

We'll have to visit [PyTorch](http://pytorch.org)'s website to install the latest PyTorch; or the current preferred tool.

# End

That's All Folks!
I find this to be a minimal setup to get up and running.
Other tools can be installed later when needed and probably within the project scope.
