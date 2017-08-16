# ADS

* [Setup](#setup)
    * [Remote Display](#remote-display)
    * [Ping from PI](#ping-from-pi)
    * [About Socket](#about-socket)
* [Cursor](#cursor)
* [Directions](#directions)
    * [above](#above)
    * [below](#below)
* [Editor](#editor)
* [File](#file)
* [Line](#line)
* [Location](#location)
* [Redaktilo](#redaktilo)
* [Text](#text)

## Setup

preliminary stuff.

### Remote Display

Refer to following for remote access to CX5020:
* [Enabling a remote display](https://infosys.beckhoff.com/english.php?content=../content/1033/cx9020_hw/2674624779.html&id=)
* [Remote Display](https://infosys.beckhoff.com/english.php?content=../content/1033/sw_os/2018363019.html&id=)
* [Web Services](https://infosys.beckhoff.com/english.php?content=../content/1033/cx8091_hw/2067825419.html&id=)
* Download `CreHost`.zip/exe

more

### Ping from PI

Set up as following:
* wifi (internet)
* eth0 (EtherCAT master): default
* eth1 (Windows PC, USB-Ethernet Adapter): static ip_address=10.0.0.2
* (use `etc/dhcpcd.conf`, not `/etc/network/interfaces`.)
* [Configure the Windows firewall to allow pings](https://kb.iu.edu/d/aopy)
* `public`: File and Printer Sharing (Echo Request - ICMPv4-In).
* If necessary, [Setup a DHCP server for PI](http://www.dhcpserver.de/cms/running_the_server/)
* (ATTN: in Raspberry-Pi, setup DHCP-IP may affect routing to wifi!!!, so static-IP is preferred!)

more

### About Socket

Refer to:
* [Sockets Tutorial in Linux](http://www.linuxhowtos.org/C_C++/socket.htm)
* [Running the Winsock Client and Server Code Sample](https://msdn.microsoft.com/en-us/library/windows/desktop/ms737889(v=vs.85).aspx)

more

## Cursor

Also used to mean the current line.

An indicator used to know the position in the text.

This is useful when a pattern occurs many times in the text: it enables the
editor to select the wanted one.

The cursor also enables to manipulate the selected element.

## Directions

Here's the vocabulary to locate something relatively in a collection of lines.

### above

Should be prefered over the words `over`, `before`, `previous` or `up`.

### below

Should be prefered over the words `under`, `after`, `next` or `down`.

## Editor

Also called "text editor".

A piece of software which is able to change the content of a text.
In the case of Redaktilo, the editor is an object provided by a library.

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

## Location

The given line number, to which you can relatively search or do something.

## Redaktilo

This means `editor` in esperanto. Technically `Tekstoredaktilo` should have been
used (`text editor`), but it was a bit too long for a project name.

## Text

Can contain:

* plain text
* JSON
* YAML
* PHP
* etc...

## Next readings

* [Extending](05-extending.md)
* [Exceptions](06-exceptions.md)

## Previous readings

* [README](../README.md)
* [Tutorial](01-tutorial.md)
* [Use cases](02-use-cases.md)
* [Reference](03-reference.md)
