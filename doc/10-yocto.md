# Yocoto-SDK BBB DTS

* [Build Image and SDK](#build-image-and-sdk)
    * [insert](#insert)
* [Deploy](#deploy)
* [Netboot](#netboot)
* [Install SDK](#install-sdk)
* [Make Modules](#make-modules)   
    * [Make Scripts](#make-scripts)
* [Make DTB](#make-dtb)    
    * [Link to Include Folder](#link-to-include-folder)
* [File](#file)
* [Line](#line)

## Build Image and SDK

Here's the vocabulary for the possible actions on a line.

### insert

Should be prefered over the word `add`.

## Deploy

Also called "text file", to be opposed to "binary file".

## Netboot

Also called "text file", to be opposed to "binary file".

## Install SDK

Also called "text file", to be opposed to "binary file".

## Make Modules

Also called "text file", to be opposed to "binary file".

## Make DTB

Also called "text file", to be opposed to "binary file".

## File

Also called "text file", to be opposed to "binary file".

See [Text](#text).

## Line

The unit with which **Redaktilo** works. It's a simple string which ends at the
line break:

* `\r\n` for texts created on Windows
* `\n` for texts created on the other operating systems

To make it easier for the developers, **Redaktilo** takes care of the line
break, so you should only provide it with a string stripped of it.


## Next readings

* [Extending](05-extending.md)
* [Exceptions](06-exceptions.md)

## Previous readings

* [README](../README.md)
* [Tutorial](01-tutorial.md)
* [Use cases](02-use-cases.md)
* [Reference](03-reference.md)
