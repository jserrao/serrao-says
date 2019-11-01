# Python Package Management and Virtual Environments 101

## Package Manager - 

[Pip](https://pypi.org/project/pip/) is the Python package manager. If you're coming from JS like me, `pip` is a rough equivalent of `npm`. Python demands a bit more of you to get a real runtime going however, so just a plain package manager usually isn't enough - you'll need a virtual environment. 

## Why does Python need these virtual environments?

If you're coming from a JS background, your first instinct might be to straight up wonder why you would need these Python virtual environments in the first place? Normally, `npm install` will read a `package.json` file and build a `node_modules` folder with all of your dependencies. These don't spread across projects.

Python mixes system packages (those core to the Python library itself) and site packages (those contributed by other developers) into one space on your computer. So, every time you run `pip install whatever` to add a nice package to one of your projects, you're **basically polluting the entire Python library**. 

You can see the shared file structure for yourself with a few commands
```py
# you can run this from anywhere in your terminal
$ python 
>>> import sys
>>> sys.prefix # output will be your python system folder
>>> import site
>>> site.getsitepackages() #output will be your python site packages folder
```

Consider scenarios where you build Django-based site three years ago, and are rolling out a new Flask-based site today. Would you want to use the same packages on both? You are forced to use the same packages unless you spin up a virtual environment to contain all of your site-specific code.

Good resource to explore more fully: [Real Python - A Virtual Environment Primer](https://realpython.com/python-virtual-environments-a-primer/). 


## `virtualenv` vs `venv` vs `pipenv` vs `conda`

When you explore the ecosystem around Python web dev, you'll see a pretty big split on how people are handling virtual environments. 

If you're using Python2, `virtualenv` is the way to go, as most of the other tools have moved over to Python3 by now. `virtualenv` is a Python2 system package, so you'll have it available without needing to download anything.

For newer projects, you'll see mentions of `venv`, `pipenv`, and `conda` frequently. 

Python3 offers `venv` as a core part of the language, which replaces `virtualenv`. Spinning up a `venv` is very easy. Again, you don't need to download anything because it's included with your system by default.

```py
# spins up your virtual environment
$ python -m venv your-environment-folder 
>>> 
```

This produces a folder, called `your-environment-folder`, that contains all the files in your virtual environment.

`pipenv` is an open-source project that tries to wrap a bunch of tooling together for you:
- creation of a virtual environment (like `venv`)
- package management (like `pip`)
- virutal environment management (like `virtualenvwrapper`)

That's where [Conda](https://docs.conda.io/en/latest/) comes in. 


[Anaconda](https://www.anaconda.com/distribution/) is the data science tool - it's like a wrapper around R, the Python stats package. As such, it's grown tremendously and has spawn Conda - gotta love the snake references I guess. Conda manages dependencies, libraries and virtual environments, all in one. 









https://stackoverflow.com/questions/20994716/what-is-the-difference-between-pip-and-conda



## So what should I use?

