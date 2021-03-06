Another PDF Tool
================

Another PDF Tool helps you quickly operate on PDF files with actions such as rotate, 
merging, and splitting pages from the command-line.

This project is in it's early stages of development, it currently only supports one 
operation.

Please stay tuned or open an issue or pull request if you'd like to help me out! I do
have a day job so I'm only working on this in my free time, development will likely be
slow.

Author: Brandon Villagran <bvillagran.dev@gmail.com>

Repository: https://github.com/bvillagran/apdft

License: MIT

**Table of Contents**
- [Another PDF Tool](#another-pdf-tool)
  - [Download](#download)
  - [Usage](#usage)
    - [Merge](#merge)
  - [Author's Note](#authors-note)

Download
--------
**Requires Python 3.6 or higher.** I am investigating packaging options for end users
without needing Python to be pre-installed.

You can clone this repository and build it yourself with
[`poetry`](https://python-poetry.org/docs/), or get it with `pip`. If you are
downloading it I'll assume you already know how to use Python modules, and `pip`, 
specifically on your operating system.

```terminal
python -m pip install bvill.apdft --user
```

Why `bvill.apdft`? Because just `apdft` [is already taken](https://pypi.org/project/apdft/) :(
Formally this project should be known as *Another PDF Tool* or `apdft` to refer to the
command-line script name.

Usage
-----

At the moment, the only operation supported is to merge multiple `.pdf` files into one.
More is on its way :)

Run the application in the terminal emulator of your choice.

```terminal
apdft --version
apdft --help
apdft merge --help
```

### Merge

The PDF files will be merged in the same order they are specified in the source arguments

You can specify multiple `.pdf` files to merge into one output file

```terminal
apdft path/to/your/file1.pdf path/to/your/file2.pdf path/to/out.pdf
```

You can also specify directories containing `.pdf` files as your source input

```terminal
apdft path/to/your/file1.pdf path/to/dir/with/pdfs path/to/out.pdf
```

By default if one or more of your sources is a directory, then it is searched
recursively until all `.pdf` files are found. Then it will sort all `.pdf` files
alphanumerically by their filenames. Sorting only occurs at the position where the 
directory is specified.

For example, imagine this is the contents of `./dir`:

```
./dir
|-- 0
|   `-- 3.pdf
|-- 1.pdf
`-- 2.pdf
```

If you run `apdft merge` like this:

```terminal
apdft merge b.pdf dir a.pdf dest.pdf
```

The result will effectively be calling it like this:

```terminal
apdft merge b.pdf dir/1.pdf dir/2.pdf dir/0/3.pdf a.pdf dest.pdf
````

You can disable this behavior with the `-d` flag, and it will default to the natural
search order defined by the OS (`os.listdir`). Note that this will still not change
the position of the SRC argument when it is a directory.

Author's Note
-------------
First and foremost, this project is intended to be a learning exercise in developing,
packaging, and distributing a modern Python-based desktop GUI application. That has been
my goal since the beginning, but I decided I should take an *Agile* approach by delivering
small, incremental releases to the public. Although the project is still in it's initial
development stage, this will help set the foundation for a consistent release cycle if I
decide to do more with it in the future.

The concept for *Another PDF Tool* came to me because I realized that often I need to
quickly concatenate multiple PDF files together, or to break one up into seperate files.
Of course I'm aware that there are a ton of free online PDF tools that do this already
(seriously, just go to Google and search *PDF Tool*). But whenever I would use one of 
those I always had a nagging feeling that my data was not kept private, which is mostly
a concern only when my PDF files contain sensitive personal information. It's also 
surprising that the most common, free PDF viewing tools don't support the functionality 
I desire. Regardless, an open source desktop PDF editing tool sounded like a great 
first Python project to do on the weekends, that is not just an ad-hoc script of sorts.

My idea is to write out an uncomplicated backend utilizing the PyPDF2 library and
build on top of it by first creating a stupidly-simple command-line interface, then a 
GUI for the primary end-userbase with something like wxPython or Electron, and possibly 
a HTTP REST API which might be a requirement for an Electron or other web-based frontend
`anyway.
