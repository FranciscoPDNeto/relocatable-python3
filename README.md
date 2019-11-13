
Introduction
============

This project builds a portable Python interpreter, along with all the shared libraries it depends on.
The build system itself is written in Python, based on zc.buildout and some recipes.

The sources are downloaded from the Internet, stored locally and then built.

The current supported platforms are: Linux, OS X, Windows, Solaris and AIX.

In order to build python, execute:

    pip install zc.buildout
    buildout bootstrap
    bin/buildout
    bin/build

Build environment
=================

For building on Mac OS X, you'll need to install first:
* Xcode command line tools
* Homebrew
* autoconf, automake, libtool, pkgconfig

For Ubuntu, you'll need to install:
* build-essential

For Windows, use a provided vm or image from microsoft:
https://developer.microsoft.com/en-us/windows/downloads/virtual-machines

Or install on a machine:
* Microsot Visual Studio 2017
* Perl
* Python


Caveats and Heads up
====================

* cyrus-sasl is compiled without GSSAPI support on solaris systems
* gnutls, gcryct, gpg-error, nettle, gmp have been removed, now using only openssl as SSL backend
* Link time optimiziation is used on platforms with gcc >4.9.
* Profile Guided Optimization (PGO) is used in all platforms*.
* Solaris and macos platforms don't support ossaudiodev in python3
* UUID capabilites is provided by a 3rd-party library extract from linux-utils
* SuSE ships with an /etc/inputrc that is not compliant with readline, python start with readline: /etc/inputrc: line 18: term: unknown variable name.
this can be fixed by removing 'set term xy' from your ~/inputrc file. For more information on how to fix that:
https://unix.stackexchange.com/questions/432763/suse-linux-enterprise-python3-error-with-readline-in-etc-inputrc
* Gettext is linked against /usr/lib libgcc and libidmap (this was also the case in previous releases as the --enable-relocatable flag leads to a faulty code)
* OSX lion and above doesn't come with SPWD (The shadow password database) so currently python is built without it.
* Some Solaris libraries are linked against /usr: libgcc libidmap and libcrypt
