:version: $RCSfile: building-prog-dir.rst,v $ $Revision: 3acf4ffa8d4b $ $Date: 2011/03/10 16:02:55 $

.. default-role:: fs

========================================
 Building the `prog` directory programs
========================================

There are three ways to build the programs in the `leptonica-`\
|versionF|\ `\\prog directory`. The quickest way is to use the :cmd:`cl`
command from a Windows Command Prompt. However, if you plan to spend a
lot of time investigating how a particular `prog` program works, it's
better to :ref:`create a new Visual Studio Project
<building-prog-programs-vs2008>` for it.

We'll assume that you are going to build `ioformats_reg.c`. This is an
excellent program to run if you want to be sure the main image libraries
were built correctly (it doesn't test `giflib`, see :ref:`this section
<testing-giflib>` to test that).

|Leptonica| will write temporary files to your temp directory. This is
normally `C:\\Documents and Settings\\<username>\\Local Settings\\Temp`
but can be changed by setting the ``TEMP`` and ``TMP`` environment
variables.

.. _building-prog-programs-commandline:

Building `prog` programs from the command line
==============================================

First, set up the proper environment variables for running the Visual
Studio 2008 compiler from the command line by executing `C:\\Program
Files\\Microsoft Visual Studio 9.0\\VC\\bin\\vcvars32.bat`.

To avoid cluttering the prog directory with object and executable
files, make subdirectories for Debug and Release builds:

.. parsed-literal::

   cd BuildFolder\\leptonica-|version|\\prog
   md Debug
   md Release
   cd BuildFolder\\leptonica-|version|\\prog\\Debug

Then copy and paste the following :cmd:`cl` command to build a Debug
version of `ioformats_reg.exe`::

   cl /Od /MDd /EHsc /W3 /RTC1 /Z7 /I ..\..\src /D WIN32 /D _DEBUG /D _CONSOLE ..\ioformats_reg.c /link /LIBPATH:"..\..\..\lib" zlib125-static-mtdll-debug.lib libpng143-static-mtdll-debug.lib libjpeg8c-static-mtdll-debug.lib libtiff394-static-mtdll-debug.lib giflib416-static-mtdll-debug.lib liblept168-static-mtdll-debug.lib

If you've decided to make simplified library filenames by using NTFS
hardlinks as described in :ref:`about-version-numbers`, you can
using the following command instead::

   cl /Od /MDd /EHsc /W3 /RTC1 /Z7 /I ..\..\src /D WIN32 /D _DEBUG /D _CONSOLE ..\ioformats_reg.c /link /LIBPATH:"..\..\..\lib" zlibd.lib libpngd.lib libjpegd.lib libtiffd.lib giflibd.lib libleptd-static.lib

To try it out do the following::

   cd ..
   Debug\ioformats_reg

If you are doing this a lot it's probably easier to set up some
environmental variables in a batch file for the compiler and linker (see
`Setting the Path and Environment Variables for Command-Line Builds
<http://msdn.microsoft.com/en-us/library/f2ccy3wt.aspx>`_
for more information)::

   SET INCLUDE=C:\BuildFolder\include;C:\BuildFolder\include\leptonica;%INCLUDE%
   SET LIB=C:\BuildFolder\lib;%LIB%
   SET PATH=C:\BuildFolder\lib;%PATH%

For Debug builds set the following compiler options::

   SET CL=/Od /MDd /EHsc /W3 /RTC1 /Z7 /D WIN32 /D _DEBUG /D _CONSOLE

For Release builds set the following compiler options::

   SET CL=/O2 /MD /EHsc /W3 /D WIN32 /D NDEBUG /D _CONSOLE

For static Debug builds set the following linker options:

.. parsed-literal::

   SET LINK=zlib125-static-mtdll-debug.lib libpng143-static-mtdll-debug.lib libjpeg8c-static-mtdll-debug.lib libtiff394-static-mtdll-debug.lib giflib416-static-mtdll-debug.lib liblept\ |vnum|\ -static-mtdll-debug.lib

For static Release builds set the following linker options:

.. parsed-literal::

   SET LINK=zlib125-static-mtdll.lib libpng143-static-mtdll.lib libjpeg8c-static-mtdll.lib libtiff394-static-mtdll.lib giflib416-static-mtdll.lib liblept\ |vnum|\ -static-mtdll.lib`

For dynamic Debug builds set the following linker options:

.. parsed-literal::

   SET LINK=liblept\ |vnum|\ d.lib

For dynamic Release builds set the following linker options:

.. parsed-literal::

   SET LINK=liblept\ |vnum|\ .lib

Then all you have to do to build `ioformats_reg.exe` is::

   cd Debug
   cl ..\ioformats_reg

You can use the Visual Studio 2008 debugger even for executables built
from the command line. See `How to: Debug an Executable Not Part of a
Visual Studio Solution
<http://msdn.microsoft.com/en-us/library/0bxe8ytt.aspx>`_ for more
information. Once you've imported `ioformats_reg.exe` into the
|liblept| solution by creating an EXE project for it, you can
right-click `ioformats_reg.exe` and the choose :menuselection:`Debu&g
--> &Start new instance` or :menuselection:`Debu&g --> Step &Into new
instance` from the context menu. You can even set breakpoints in
`ioformats_reg.c` before you do this.


.. _building-prog-programs-vs2008:

Building `prog` programs using Visual Studio 2008
=================================================

For anything other than just quickly trying out a `leptonica-`\
|versionF|\ `\\prog` program, you should create a Visual Studio 2008
project for it.

I tried to make the process simpler by creating a Project Template but
Visual Studio 2008 doesn't seem to support them for Visual C++. Instead
you have two ways to build a `prog` program: manually create a Project
for it, or use my Addin that automatically performs the steps of the
manual method.


Set up the "template" `ioformats_reg` project
---------------------------------------------

First of all, no matter if you decide to use my Addin or create the
`prog` Project manually, you have to correctly set up the
`ioformats_reg` project. We use this as the basis for new `prog` program
projects (you only have to do this once):

1. The working directory is stored in a machine/user specific file so it
   can't be distributed. You have to set this yourself. First
   right-click the `prog_projects\\ioformats_reg` project and choose
   :menuselection:`P&roperties` from the context menu.

#. Set :guilabel:`&Configuration:` to be :guilabel:`All Configurations`.

#. Change :guilabel:`Configuration Properties | Debugging | Working
   Directory` to::

      ..\..\..\prog

#. Change :guilabel:`Configuration Properties | Debugging | Environment`
   to::

      PATH=..\..\lib;%PATH%

   so that Visual Studio knows where to find `liblept`\ |vnumF|\ `d.dll`
   when debugging applications that link with the DLL version of
   |liblept|.

#. Click :guilabel:`OK`.

#. Exit and restart Visual Studio (or close and reopen the |liblept|
   solution).

.. _using-create-prog-project-addin:

Using the Create Leptonica `prog` Project AddIn
-----------------------------------------------

Before you can use my "Create Leptonica `prog` Project AddIn" for Visual
Studio 2008 you have to install it:

#. Move `vs2008\\CreateLeptonicaProgProjects.AddIn` and
   `vs2008\\CreateLPP.dll` to your Visual Studio 2008 Addins folder
   (normally `C:\\My Documents\\Visual Studio 2008\\Addins\\`).

#. Restart Visual Studio 2008.

To create a Visual Studio Project for a program in the `leptonica-`\
|versionF|\ `\\prog\\` directory:

#. Select a file (or files) within the :guilabel:`prog_files` Solution
   Folder.

#. Right-click the selected file(s), and choose :menuselection:`Create
   &Project for Leptonica Prog program` from the context menu:

   .. image:: images/create-project-popup.png
      :align: center
      :alt: "Create Project for Leptonica Prog program" popup menu

   The following image shows the result:

   .. image:: images/newly-created-project.png
      :align: center
      :alt: Newly created project

   The popup context menu will only contain the :menuselection:`Create
   &Project for Leptonica Prog program` choice for `leptonica.sln` and
   only for items within the :guilabel:`prog_files` Solution Folder.

   .. _set-startup-project:

#. Right-click your new project, and choose :menuselection:`Set as
   St&artup Project`.  This makes your new project the default project
   for building and debugging.

#. If the program needs command line arguments, right-click the project
   and set :menuselection:`P&roperties` :guilabel:`| Configuration
   Properties | Debugging | Command Arguments`.

The easiest way to build all the `prog\\` programs is to open the
:guilabel:`prog_files\\ByFilename` folder. This contains all the `prog`
programs, so just select them all and use the Addin to create Projects
for them. When it's done (it will take awhile), right-click the
:guilabel:`prog_projects` Solution Folder and choose
:menuselection:`B&uild`.

[I should be able to build the entire Solution by choosing
:menuselection:`&Build --> &Build Solution` (:kbd:`F6`), but for some
reason I get "Project not selected to build for this solution
configuration" messages for all the newly added Projects.  When I choose
:menuselection:`&Build --> C&onfiguration Manager...`, I can see that
all these Projects aren't selected to build by default. Seems to me this
used to work before I changed the names of my initial configurations to
:guilabel:`LIB Debug` and :guilabel:`LIB Release`. Oh, well.]


.. Tip:: Debugging Console Applications

   When debugging console apps like the ones in the `prog`
   directory, put a breakpoint on the very last line in ``main()`` or on
   any ``exit()`` statements. That way you can view the program output
   in the Command Prompt window before it automatically disappears when
   the program exits.

   Alternatively, if you just want to see the program output and don't
   need to debug, make sure the Project is the :ref:`startup project
   <set-startup-project>`, and choose :menuselection:`&Debug --> Start
   Wit&hout Debugging` (:kbd:`Ctrl+F5`). A "Press any key to
   continue..."  message will appear when the program finishes.

.. note::
   The Addin has only been tested on Windows XP Pro SP3.

   The c# sources for the Addin are in
   `vs2008\\CreateLeptonicaProgProjects.zip`.

.. note::
   
   The free Express editions of Visual Studio do **not** support
   Addins. You have to use the following manual method.

The manual method for creating `prog` program projects
------------------------------------------------------

If for some reason my Addin doesn't work or you decide not to use it,
you can always create projects for `leptonica-`\ |versionF|\ `\\prog`
programs manually by following the steps outlined here.

1. Make a copy of the `BuildFolder\\leptonica-`\ |versionF|\
   `\\vs2008\\prog_projects\\ioformats_reg` directory.

#. Rename that directory to the name of the `leptonica-`\ |versionF|\
   `\\prog` program you are trying to run (in the following it will be
   shown as `<progname>`). The renamed copy of `ioformats_reg` must be
   in the same folder as the original since the project uses relative
   paths to find the `prog` directory.

#. Delete the `<progname>\\LIB Debug`, `<progname>\\LIB Release`,
   `<progname>\\DLL Debug`, and `<progname>\\DLL Release` directories if
   they exist.

#. Rename `ioformats_reg.vcproj` to `<progname>.vcproj`.

#. Edit `<progname>.vcproj` and change all occurrences of ``ioformats_reg``
   to ``<progname>``.

#. Rename `ioformats_reg.vcproj.<MACHINENAME>.<username>.user` to
   `<progname>.vcproj.<MACHINENAME>.<username>.user`.

#. Right-click the `prog_projects folder` in Solution Explorer. Choose
   :menuselection:`A&dd --> &Existing Project...` from the context
   menu. Select the `<progname>.vcproj` you just created.

#. Do the :ref:`last two steps <set-startup-project>` of the automatic
   method if desired.

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
