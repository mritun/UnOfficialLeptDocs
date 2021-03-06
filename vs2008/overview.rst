
:version: $RCSfile: overview.rst,v $ $Revision: ab7f322f4578 $ $Date: 2011/02/08 03:40:07 $

.. default-role:: fs

.. _overview:

==========
 Overview
==========

|liblept| is a library of image processing routines written in C. This
document discusses :doc:`linking <building-other-programs>` with
:doc:`pre-built Windows 32-bit binaries <downloading-binaries>` to
create working executables with Microsoft's Visual Studio 2008. A brief
section on using :doc:`Visual Studio 2010 <vs2010-notes>` is also
included.

|liblept| can process a number of image file types. The supplied
static and dynamic libraries support the JPEG, PNG, TIFF, and GIF file
formats.

Also `available
<http://tpgit.github.com/UnOfficialLeptDocs/leptonica/source-downloads.html#microsoft-visual-studio-2008>`_
is a :doc:`Visual Studio 2008 solution <vs2008-solution>` that lets you
build the :doc:`library <building-liblept>` and the :doc:`executables
<building-prog-dir>` in the Leptonica `/prog` directory. It contains a
complete hierarchy of all the `/prog` directory programs listed by type,
category, and filename to make browsing the many files easier.

Detailed :doc:`instructions <building-image-libraries>` are given on
rebuilding the supplied image libraries.

See :doc:`versions` for important information about each new
release.


..
   Local Variables:
   coding: utf-8
   mode: rst
   indent-tabs-mode: nil
   sentence-end-double-space: t
   fill-column: 72
   mode: auto-fill
   standard-indent: 3
   tab-stop-list: (3 6 9 12 15 18 21 24 27 30 33 36 39 42 45 48 51 54 57 60)
   End:
