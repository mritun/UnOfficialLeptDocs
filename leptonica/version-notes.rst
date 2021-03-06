:version: $RCSfile: version-notes.rst,v $ $Revision: 76e0bf38aaba $ $Date: 2011/03/22 00:48:41 $

.. default-role:: fs

.. _version-notes:

=============================
 Version Notes for Leptonica
=============================

.. Note:: The following are highlights of the changes in each version.
          They are *not* a complete listing of the modifications.

1.68 --  14 Mar 11
==================

* Fixed windows issues with passing pointers across C-runtime boundaries
  when using DLLs, by providing special functions (e.g.,
  :doxyfunc:`lept_fopen()`).

* Proper version numbers are now set with :cmd:`automake`.

* New utility (:doxyfile:`quadtree.c`) for generating quadtree statistics.

* New utility (in :doxyfile:`colorspace.c`) for conversions to and from
  YUV.

* Refactored functions for assembling image data for generating either
  PS or PDF images using g4, jpeg or flate encoding.

* Better tempfile names, using current time in microseconds.

* Functions for getting resolution from jpeg and png files.

* Use ``size_t`` throughout for reading and writing binary data.

* Deprecate ``arrayRead*()`` and ``arrayWrite()`` functions; replace in
  the library with ``l_binaryRead*()`` and :doxyfunc:`l_binaryWrite()`.

* Better handling of colormap images for in-place rasterop and shear.

* New utility (:doxyfile:`bytearray.c`) for parsing and handling binary
  data; used for generating PDF files.

* New utility (:doxyfile:`pdfio.c`) for generating PDF files.

* Refactored ``regutils`` functions to make them simpler to use.

* Top-level deskew now works on any image.

* Added functions in :doxyfile:`utils.c` for cross-platform development,
  mostly for functions that make and remove directories, copy, move and
  delete files, etc.  It should now be straightforward to write programs
  that will compile and run on windows.

* Reg tests have better printout; all give timings.

* New utility program: :doxyfile:`convertfilestopdf.c`.


1.67 --  9 Nov 10
=================

* **Autoconf**: now built with James Cuirot's config files that build the
  library and all 200 progs.

* New sudoku solver.  Just a game, but there are interesting aspects.

* Modified :doxyfile:`parseprotos.c` to reject a type of "``extern``"
  decl.

* Add faster implementation for very small gray morphology operations
  (3x1, 1x3, 3x3).

* Eliminate warnings on recent gcc if you don't check return values from
  ``fread``, ``fscanf``, ``fgets``, ``system``, etc.

* **Convolution**: new functions for windowed variance and stdev; allow
  non-square kernel for windowed mean square.

* Put `stdio.h` and `stdlib.h` in `alltypes.h`, so they're not required
  in any `.c` files.

* Replace ``numaConvolve()``, which is just a windowed mean, by windowed
  statistics functions (mean, mean square, variance).

* Generalize :doxyfunc:`pixExtractOnLine()` for arbitrary lines.

* Add pix interface to webp (:doxyfile:`webpio.c`,
  :doxyfile:`webpiostub.c`). This is a new open source codec, based on
  the video codec vpx (webm).

* Serialization of ``FPix`` and ``DPix``.

* Interconversion between ``FPix`` and ``DPix``.

* Integer scaling of ``FPix`` and ``DPix``; includes the last row and
  column.

* New :doxyfile:`convertfiles.c`: depth conversion on files in a directory.

* Testing programs in `prog`:

  * :doxyfile:`convolve_reg.c`, :doxyfile:`numa_reg.c`: expanded test
    set
  
  * :doxyfile:`projection_reg.c` (tests :doxyfunc:`pixRowStats()`,
    :doxyfunc:`pixColumnStats()`)

  * :doxyfile:`dewarptest.c`: output ps and pdf files

  * :doxyfile:`writemtiff.c`: simple driver to write images to a single
    file


1.66 -- 3 Aug 10
================

* More tweaks for including (or not) bounding box hints for PS wrapping.
  Default is to write b.b., but not in functions that wrap images as
  full pages (:doxyfile:`psio1.c`, :doxyfile:`psio2.c`)

* `pix4.c` split in two files, and added function to identify c.c.  that
  are sufficiently similar in shape to rectangles (:doxyfile:`pix5.c`)

* Modify 2 and 4 bit setters to clip the input value so that it can only
  affect the pixel requested (:doxyfile:`arrayaccess.c`,
  :doxyfile:`arrayaccess.h`)

* New pseudorandom sequence functions (:doxyfile:`numafunc1.c`)

* Dewarping camera-based images using textlines (:doxyfile:`dewarp.c`,
  `prog/dewarp\*`)

* Geometrical function for aggregating overlapping bounding boxes.

* Programs to generate figures for book :chapter-title:`"Document Image
  Applications"` in :title:`Mathematical Morphology: theory and
  applications` (see: :doc:`document-image-analysis`) (`prog/livre\*.c`)

* Functions that do affine and other operations in images with alpha
  blending at edges: ``pix*WithAlpha()``.  Also do this with a
  gamma/inverse-gamma wrapper to further reduce edge aliasing.
  (:doxyfile:`rotate.c`, :doxyfile:`scale.c`, :doxyfile:`projective.c`,
  :doxyfile:`affine.c`, :doxyfile:`bilinear.c`,
  :doxyfile:`prog/alphaxform_reg.c`)

* Improved color segmentation (fixed bugs; made faster)

* Higher order least square fits: quadratic, cubic, quartic. (`pts.c`)

* Various mods for otsu binarization and the ``*SplitDistribution*()``
  functions (:doxyfile:`numafunc2.c`, :doxyfile:`prog/otsutest2.c`)

* Control sampling in convolution output (:doxyfile:`convolve.c`,
  :doxyfile:`prog/fpix_reg.c`)

* Morphological operations on numas (:doxyfile:`numafunc1.c`,
  :doxyfile:`numafunc2.c`, :doxyfile:`prog/numa_reg.c`)

* Pix serialization wrapped so we can use :doxyfunc:`pixRead()`, etc on
  these files (:doxyfile:`spixio.c`, :doxyfile:`readfile.c`,
  :doxyfile:`writefile.c`)

* `GIF` read/write to memory fixed (and cheated --- using files)
  (:doxyfile:`gifio.c`)

* New ``FPIX`` and ``DPIX`` accessors; contour rendering on ``FPIX``
  (:doxyfile:`fpix1.c`, :doxyfile:`fpix2.c`)

* Various functions for linearly mapping colors and displaying arrays of
  colors (:doxyfile:`pix4.c`, :doxyfile:`blend.c`,
  :doxyfile:`prog/rankhisto_reg.c`)

* Functions for getting approximate ranges of colors and color
  components in an image (:doxyfile:`pix4.c`, :doxyfile:`colormap.c`)

* Cleaned up windows platform and compiler defines and macros.


1.65 -- 5 Apr 10
================

* Added regression test utility functions for standardizing and
  automating construction and running of regression tests.  Makes the
  golden files when the 2nd arg to the reg test is 'generate'.
  (`regutils.{c,h}`)
 
  Converted 22 reg tests in `prog` to use this; invoked with
  :doxyfile:`alltests_reg`.  Goal is to put all `prog/\*_reg.c` into
  this format and put a set of golden files on the web.

* Small fixes in :doxyfile:`gifio.c` for handling streams properly.

* New functions for shifting colors, hue invariant transforms, etc
  (:doxyfile:`blend.c`)

* `prog/dwamorph\*.c`: rename `\*1_reg.c` to :doxyfile:`dwalineargen.c`;
  others converted to standard reg tests.

* New rgb convolution functions.

* For `PS` output, write all images with a bounding box hint and with
  page numbers, which works for both embedded (e.g., in tex) and full
  page generated `PS`.  Once converted to pdf, this is fine in all
  situations.

* New functions for initialization and random insertion with
  :doxyfile:`pixcomp.c`.

* For color quantization, make the lightest color white if sufficiently
  close; ditto for black (:doxyfile:`colorquant1.c`,
  :doxyfile:`colorquant2.c`).

* Rank binning of 8 bpp and rgb images (:doxyfile:`numafunc2.c`,
  :doxyfile:`pix4.c`)

* A function to rank colors by the intensity of the minimum comp
  (:doxyfile:`pix4.c`)

* New :doxyfunc:`pixRotateBinaryNice()`, rotates 1 bpp pix in such a way
  that the shear lines aren't visible. (:doxyfile:`rotate.c`)

* New :doxyfunc:`pixSaveTiledWithText()`, a convenience function to
  append text to images that are being tiled. (:doxyfile:`writefile.c`)

* Stereoscopic warping functions and stereo pair functions
  (:doxyfile:`warper.c`)

* Linear interpolated shear --- better than rasterop shear
  (:doxyfile:`shear.c`)

* Option to use higher quality chroma (U,V) sampling in jpeg
  (:doxyfile:`jpegio.c`)

* Rename ``Bmf`` --> ``L_Bmf``.

* New tests in prog:
 
     :doxyfile:`alltests_reg.c`, :doxyfile:`alphaclean_reg.c`,
     :doxyfile:`psio_reg.c`, :doxyfile:`rankbin_reg.c`,
     :doxyfile:`rankhisto_reg.c`, :doxyfile:`warpertest.c`


1.64 -- 3 Jan 10
================

* Easy setup for standard byte processing on 8 bpp pix (:doxyfile:`pix2.c`)

* Evaluation of difference between similar images; test for similar
  images and (:doxyfile:`compare.c`)

* Subpixel scaling, with color input and separate scale factors
  (:doxyfile:`pixconv.c`)

* Fix `TIFF` header reader to get correct format (:doxyfile:`tiffio.c`)

* Enable :doxyfunc:`pixDisplay()` to work with :cmd:`i_view` (Windows)
  and with :cmd:`xzgv` and :cmd:`xli` as well as :cmd:`xv`; allow
  application to choose which to use (:doxyfile:`writefile.c`).

* Use a mask to specify regions that are changed by a morphological
  operation (:doxyfile:`morphapp.c`).

* Improve the default sharpening for scaling (:doxyfile:`scale.c`)

* Function to test for equivalence of file data (:doxyfile:`utils.c`)

* Select and read image files with embedded index
  (:doxyfile:`readfile.c`)

* Fix box size calculation in :doxyfunc:`pixEmbedForRotation()`;
  solution provided by Brent Sundheimer.

* New :doxyfunc:`pixDisplayMultiple()`, instead of calling :cmd:`gthumb`
  directly; this is now set up to use :cmd:`i_view` for Windows.

* Changed criteria for determining if an image is color
  (:doxyfile:`colorcontent.c`, `colorquant{1,2}.c`)

* Optional mode where the filename extension is automatically written to
  output image files; particularly useful for Windows.

* Initialize ``BOXA`` and ``PIXA`` as full, with minimal placeholders.

* Get rank valued numbers and boxes in ``NUMA`` and ``BOXA``.

* Cute implementation for finding largest solid rectangle
  (:doxyfile:`maze.c`)

* New median cut quantization for mixed (color/gray) images
  (:doxyfile:`colorquant2.c`)

* Many changes to allow the library and applications to be built easily
  in Windows. There is now a thorough windows readme, written by Tom
  Powers, for doing this.  The Windows build information and project
  files are now in a new vs2008 directory.


1.63 -- 8 Nov 09
================

* Added :doxyfunc:`pixScaleToGrayFast()`, a faster version with very
  similar quality.

* Fixed :doxyfunc:`scaleGrayLILow()` to handle edge pixels more accurately.

* Text processing:

  * new text application (:doxyfile:`finditalic.c`,
    :doxyfile:`prog/finditalic.c`) for locating words in italic type
    style.
 
  * Easier to add text to a pix using the bitmap font stored in the font
    directory; see, e.g., :doxyfile:`prog/writetext_reg.c`.

* Blending of 2 images with an alpha channel:
  :doxyfunc:`pixBlendWithGrayMask()`.

* Fixed bug in color segmentation; it now (again) works properly.

* New utility (:doxyfile:`pixcomp.c`) for handling compressed pix arrays
  in memory; new ``PixComp`` and ``PixaComp`` structs.

* Fast serialization of pix without compressing
  (:doxyfunc:`pixSerializeToMemory()` and
  :doxyfunc:`pixDeserializeFromMemory()`); required serialized colormaps

* File I/O: new functions for reading file headers.

  * PostScript generation modernized; split `psio.c` into
    :doxyfile:`psio1.c` and :doxyfile:`psio2.c`; added level 3 (flate)
    encoding.

  * new functions for reading and writing multipage tiffs, for arbitrary
    input images.  For writing, compression is lossless (either g4 or
    zip)

  * update all I/O stub files

* Miscellaneous: new :doxyfunc:`pixaAddBorderGeneral()`; new functions
  in :doxyfile:`pix3.c` for counting fg pixels and summing 8 bpp pixels
  by column and row; new :doxyfunc:`numaUniformSampling()` for
  resampling with interpolation; subpixel scaling.

* New or improved regression tests in prog:

     :doxyfile:`extrema_reg`, :doxyfile:`pixalloc_reg`,
     :doxyfile:`blend2_reg`, :doxyfile:`rotateorth_reg`,
     :doxyfile:`ioformats_reg`, :doxyfile:`colorseg_reg`,
     :doxyfile:`pixcomp_reg`, :doxyfile:`pixserial_reg`,
     :doxyfile:`writetext_reg`, :doxyfile:`psioseg_reg`,
     :doxyfile:`subpixel_reg`.

* Interface changes:

  * :doxyfunc:`findFileFormat()` and :doxyfunc:`findFileFormatBuffer()`:
    now returns format using input ptr. The function return value is 0
    if OK; 1 on error

  * rename: ``pixThresholdPixels()`` -->
    :doxyfunc:`pixThresholdPixelSum()`


1.62 -- 26 Jul 09
=================

* Expanded composite Dwa implementation as a sequence of operations, so
  that it now works beyond a size of 63.  It's typically about 2x faster
  than the composite rasterop implementation (with help from Ankur
  Jain).  Also use data transfer instead of data copy whenever possible.
  Thorough tests with `binmorph4_reg` and `binmorph5_reg`.

* New functions in :doxyfile:`colorseg.c` for masking and histogramming
  in HSV color space.

* Treat string constants rigorously as ``const char*``, initializing to
  ``char[]`` if to be used as non-const, or in some cases casting to
  ``char*``.  This avoids compiler warnings.

* Improved color quantization using existing colormap for octcubes and a
  new version for grayscale.  This will rigorously map most black and
  most white octcubes (rsp) to black and white if they exist in the
  colormap.

* Fast quantization to an existing colormap for color and grayscale.

* Fixed some bugs; e.g., in :doxyfunc:`pixAffineSampled()` for 1 bpp
  with ``L_BRING_IN_BLACK``; reading and writing pnm for 2 and 4 bpp.

* In :doxyfile:`pngio.c`, enable compile time control over these
  settings:

  * converting 16 bpp --> 8 bpp on read

  * removing alpha channel on read

  * setting zlib compression on write

* For general scaling, allow sharpening to be optional, and provided
  faster sharpening operations.

* Improve support for 16 bpp grayscale.

* For ``scaleToGray*`` functions, reduce the width truncation.

* In :doxyfile:`psio1.c`, new functions for converting segmented page
  images (text and image) into level 2 PostScript.

* Removed all implicit casting to ``const char*``.

* New custom pix memory allocator, designed for large pix whose memory
  needs to be reused many times.

* In `xtractprotos`, we now allow prepending an arbitrary string to each
  prototype.

* In :doxyfile:`environ.h`, additions for MSVC to work with VC++6,
  including prototype strings for dll import and export (thanks to Ray
  Smith).

* In :doxyfile:`colorseg.c`, new functions for building HSV histograms,
  finding peaks, and generating masks based on the peaks.

* New or improved regression tests:

    :doxyfile:`pixalloc_reg`, :doxyfile:`binmorph4_reg`,
    :doxyfile:`binmorph5_reg`, :doxyfile:`conversion_reg`,
    :doxyfile:`scale_reg`, :doxyfile:`cmapquant_reg`.


1.61 -- 26 Apr 09
=================

* New histo-based grayscale quantization:
  :doxyfunc:`pixGrayQuantFromHisto()`, that is used in new
  :doxyfunc:`pixQuantizeIfFewColors()`.

* Made final fix in :doxyfunc:`pixBlockconv()`.  No underflows; no more
  overflows!

* More efficient rgb write with pnm.

* Add proto to :doxyfile:`jpegiostub.c`, allowing proper use of the
  stubber.

* Fix several filter functions to use proper test on filter size; viz.,
  :doxyfunc:`pixMinMaxTiles()`, several functions in
  :doxyfile:`convolve.c`.

* Redo shear implementation to handle arbitrary angles, to handle
  colormapped images, and to avoid the singularity at pi/2.

* Removed both static vars from :doxyfunc:`pixSaveTiled()`.

* Generalized :doxyfunc:`pixRotate()` to handle colormapped images, and
  to use :doxyfunc:`pixRotateBySampling()` in place of the removed
  ``pixRotateEuclidean()``.

* New skew finder for full angle range,
  :doxyfunc:`pixFindSkewOrthogonalRange()`.

* For skew detection, now allow shear about image center as well as
  about the UL corner.

* New rotation reg tests: :doxyfile:`rotate1_reg.c` and
  :doxyfile:`rotate2_reg.c`.

* Better serialization format for ``boxaa``; introduce new version
  numbers for ``boxaa``, ``pixa``, and ``boxa``, as required.

* Proper init in :doxyfunc:`boxGetGeometry()`,
  :doxyfunc:`boxaGetBoxGeometry()`, and the accessors in
  :doxyfile:`sel1.c` and :doxyfile:`kernel.c`.

* Improved Numa functions in :doxyfile:`numafunc1.c` and
  :doxyfile:`numafunc2.c`; in particular,
  :doxyfunc:`numaMakeHistogramAuto()` and
  :doxyfunc:`numaGetStatsUsingHistogram()`.

  * With all histo generators, make sure the start and binsize params
    are properly set and are used.

  * Interface change: Use these parameters implicitly in
    :doxyfunc:`numaHistogramGetRankFromVal()` and
    :doxyfunc:`numaHistogramGetValFromRank()`.

* Interface change to :doxyfunc:`ptaGetLinearLSF()`: add 1 optional
  parameter.

* In several ``pixaDisplay*()`` functions, handle colormaps properly.

* `pixafunc.c` split to :doxyfile:`pixafunc1.c` and
  :doxyfile:`pixafunc2.c`.

  * New connected component selections and options in
    :doxyfunc:`pixaSort()`.

* Patch from Tony Dovgal for reading tiff rgba files.

* Added new logical operation options for numas.

* New :doxyfunc:`pixConvertRGBToGrayMinMax()` that chooses min or max of
  3 components.

* Computation of pixelwise aligned stats between multiple images of the
  same size (e.g., video), in :doxyfile:`pix4.c`.

* Very fast binsort implemented for ``boxa`` and ``pixa``.

* Cleanup and rename stack, queue, heap and ptra functions:

  * all structs and typedefs start with ``L_``

  * all functions start with ``l``

* Sel creation for crosses and T junctions.

* New thresholding operations to binary; split out from
  :doxyfile:`adaptmap.c` into :doxyfile:`binarize.c`.

* Implementation of sauvola binarization, including use of pixtiling.

* Added composite parallel union and intersection morphological operations.

* Small changes to scaling and rotation to improve accuracy; only
  visible on very tiny, symmetric images.

* Implemented DPix (double precision data); useful for the mean square
  accumulator for sauvola binarization.

* New fast hybrid grayscale seedfill, in addition to the interative
  version (contributed by Ankur Jain).

* New or improved regression tests:

    :doxyfile:`rotate1_reg`, :doxyfile:`rotate2_reg`,
    :doxyfile:`shear_reg`, :doxyfile:`numa_reg`, :doxyfile:`skew_reg`,
    :doxyfile:`ptra1_reg`, :doxyfile:`ptra2_reg`, :doxyfile:`paint_reg`,
    :doxyfile:`smallpix_reg`, :doxyfile:`pta_reg`,
    :doxyfile:`pixmem_reg`, :doxyfile:`binarize_reg`,
    :doxyfile:`grayfill_reg`.


1.60 -- 19 Jan 09
=================

* Fixed bug in :doxyfunc:`pixBlockconv()`, introduced in 1.59, that
  causes overflow when convolving with an image that has white (255) at
  the edges.  [quickly found by Dave Bryan]

* Include function to display freetype fonts in a pix.

* The files :doxyfile:`freetype.c` and :doxyfile:`freetype.h` are in the
  distribution, but are not yet linked into the library.  This is
  contributed by Tony Dovgal, and this version works only for MSVC.

* Found that the problems with binary compression in `giflib` are fixed
  with `giflib` 4.1.6.


1.59 -- 11 Jan 09
=================

* Lots of changes since 1.58.

* New files: :doxyfile:`affinecompose.c`, :doxyfile:`ptra.c`,
  :doxyfile:`warper.c`, `watershed.{h,c}`.
 
  * Split: `boxfunc.c` --> (:doxyfile:`boxfunc1.c`,
    :doxyfile:`boxfunc2.c`, :doxyfile:`boxfunc3.c`)

* Improved connected component filtering, with logical functions applied
  to indicator arrays (:doxyfile:`pix4.c`, :doxyfile:`pixafunc1.c`,
  :doxyfile:`numafunc1.c`).

* Function to determine if an image can be quantized nicely with only a
  few colors (:doxyfile:`colorcontent.c`, :doxyfile:`pixconv.c`).

* New gray seed-filling functions (:doxyfile:`seedfill.c`,
  :doxyfile:`seedfilllow.c`).

* Fixed bugs in tophats and hdome, due to misuse of
  :doxyfunc:`pixSubtractGray()` (:doxyfile:`morphapp.c`).

* New function for improving contrast (:doxyfile:`adaptmap.c`)

* Watershed transform (still slightly buggy) (`watershed.c,h`).

* Fast random access into a pix using line pointers (:doxyfile:`pix1.c`,
  `arrayaccess.\*`)

* Conversions of colormaps from gray to color and
  v.v. (:doxyfile:`colormap.c`)

* Seedfill function that applies an upper limit to the fill distance
  (:doxyfile:`seedfill.c`)

* New function for warping images with random harmonic distortion
  (with help from Tony Dovgal).

* New generic ptr array utility: all O(1) functions of a stack plus
  random replace, insert and delete (:doxyfile:`ptra.c`).

* Simple functions for colorizing a grayscale image with an arbitrary
  color (:doxyfile:`pixconv.c`, :doxyfile:`colormap.c`)

* Flexible affine transforms (translation, scale, rotation) on ``pta``
  and ``boxa`` (:doxyfile:`affinecompose.c`).

* Clipping of foreground (both exact and approximate) starting from
  within a rectangular region of the image (:doxyfile:`pix4.c`)

* Blending a colored rectangle over an image (:doxyfile:`pix2.c`,
  :doxyfile:`boxfunc3.c`)

* Generation of rectangle covering of mask components
  (:doxyfile:`boxfunc3.c`).

* Block convolution using tiles (for very large images)
  (:doxyfile:`convolve.c`)

* New or improved regression tests in `prog`:

     :doxyfile:`locminmax_reg`, :doxyfile:`lowaccess_reg`,
     :doxyfile:`grayfill_reg`, :doxyfile:`adaptnorm_reg`,
     :doxyfile:`xformbox_reg`, :doxyfile:`warper_reg`,
     :doxyfile:`cmapquant_reg`, :doxyfile:`compfilter_reg`,
     :doxyfile:`splitcomp_reg`, :doxyfile:`affine_reg`,
     :doxyfile:`bilinear_reg`, :doxyfile:`projective_reg`

* Acknowledgments:

  (1) Big thanks to Tony Dovgal for helping with the warping (e.g. for
      captcha).  Tony also provided an implementation that allows
      rendering truetype fonts into a ``PIX`` on Windows.  This is not
      yet incorporated, because it opens a huge "can of worms," which is
      OK if you're going fishing but maybe not if you're trying to
      support leptonica on many platforms.  TBD.

  (2) David Shao provided a `libtools` build system that includes
      building the `prog` directory!  I believe this will work, but it
      is is not yet included because of problems I continue to have with
      macros in version 2.61 of gnu libtools.

  (3) Steve Rogers is working on a MSVC build for the `prog` directory.
      I hope to have this available for 1.60.


Earlier Versions
================

::

 1.58   27 Sept 08
        Added serialization for numaa.
        New octree quantizer pixOctreeQuantByPopulation(), that uses a
        mixture of level2 and level4 octcubes.  Renamed many functions
        in colorquant1.c, and arranged/documented them more carefully.
        Revised documentation in leptonica.org/papers/colorquant.pdf.
        Simplified customization for I/O libraries and fmemopen() in environ.h.
        Fixed bugs in colormap.c, viewfiles.c, pixarith.c.
        Verified Adam Langley's jbig2enc (encoding jbig2 and generating pdf from
        these encoded files) works properly with the current version -- see
        Section 24 of README.html for usage and build hints.
        New separable convolution; let pixConvolve() take 8, 16 and 32 bpp input.
        New floating pt pix (FPix) utility, which allows convolution and
        arithmetic operations on FPix; also interconversion to Pix.
        Ability to read headers on multipage tiff.
        More robust updown text detection in flipdetect.c.
        Use of sharpening to improve scaling when the scale factor is near 1.0.
        See prog/fpix_reg.c for regression test and usage.
        See prog/blend_reg.c for blending regression test, with new functions.

 1.57   13 Jul 08
        New Debian distribution for 1.57 (thanks to Jeff Breidenbach).
        Improved the Otsu-type approach for finding a binarization threshold,
        by choosing the min in the histogram subject to constraints
        (numafunc2.c, adaptmap.c)
        New function pixSeedspread() in seedfill.c, similar to a voronoi tiling,
        that is used for adaptive thresholding in pixThresholdSpreadNorm().
        In the process, fixed a small bug in pixDistanceFunction().
        (The approach was suggested by Ray Smith, and uses the fast
        Vincent distance function method to expand each seed.)
        Generalized the functions in kernel.c to use float weights
        for general convolution (Version 2 for kernel), and added
        gaussian kernel generation.
        Put all jpeg header functions into jpegio.c, where they belong.
        Fixed bugs in pixaInsertPix() and pixaRemovePix().
        Added read/write serialization for Numaa.
        New functions for comparing two images using bounding boxes (classapp.c).

 1.56   12 May 08
        Added several new 1d barcode decoders.  The functional interface
        is still in flux.
        Autoconf!   To get this working, it was necessary to: determine and
        set the endian flag; select which libraries are to be linked;
        determine if stream-based memory I/O is enabled.
        This required a major cleanup of the include files, minimizing
        dependencies on external library header files, and getting everything
        to work with both autoconf (HAVE_CONFIG_H) and the old
        customized makefile.  Customization is now all in environ.h.
        pixSaveTiled(): a new way to display tiled images.
        pixtiling.c: interface for splitting an image into a set of
        overlapping tiles, using mirrored borders for tiles touching the
        image boundary.
        pixBlendHardLight(): new blending mode with nice visual effects.
        pixColorFraction(): determines extent of color in image
        Both octree and median-cut color quantization check first if
        image is essentially grayscale; improvements to both algorithms.
        box*TransformOrdered(): general sequence of linear transforms.
        colorquant_reg.c, xformbox_reg.c, hardlight_reg.c: new regr tests.

 1.55   16 Mar 08
        New functions for combining two images arbitrarily through a mask,
        including mirrored tiling (pix3.c)
        Modify pixSetMasked*() to work on all images (pix3.c)
        New functions for extracting masked regions such as pixClipMasked()
        (pix3.c) and pixMaskConnComp() and pixMaskBoxa() (boxfunc.c).
        New functions to separate fg from bg (pix3.c), one of which is supported
        by numaSplitDistribution (numafunc.c).
        Modify sobel edge detector to take another parameter (edge.c)
        Support for 4 bpp cmyk color space in jpeg (jpegio.c)
        Modified median cut color quantization (colorquant2.c)
        Renamed colorquant.c (for octree quant) --> colorquant1.c.
        Absorbed conncomp.h and colorquant.h into specific files that
        depend on them (colorquant1.c, conncomp.c, pix.h)
        General convolution with utility for building kernels
        (convolve.c, kernel.c)
        Initial implementation of 1D barcode reader.  So far, we just have the
        signal processing to locate barcodes on a page, deskew them, and
        find the bar widths, along with decoders for two formats.
        (readbarcode.*, prog/barcodetest.c)
        Made the default to stub out read/write for non-tiff image formats
        to memory; it doesn't work on Macs & they were complaining (*io.c)
        Include MSVC project files for building leptonlib under
        windows (leptonlib.*)

 1.54   21 Jan 08
        Histogram equalization (enhance.c).
        New functions for pixaa: serialization (r/w), creation
        from pixa, and a tiled/scaled display into a pixa (pixabasic.c,
        pixafunc.c).
        Read/write of tiff to memory (instead of a file, using
        the TIFFClientOpen() callback interface), contributed by Adam
        Langley (tiffio.c, testing in prog/ioformats_reg).
        Improved image statistics functions, both over tiles and
        through a mask over the entire image.  Added standard deviation
        and variance; enable statistics for rgb and colormapped images,
        in addition to 8 bpp grayscale (pix3.c).  New function to
        extract rgb components from a colormapped image (pix2.c).
        Fix pixWriteStringPS() to work with all depths and colormap (psio.c)
        Enable all non-tiff formats to also write and read to/from memory (*io.c)
        Added support for read/write to gif, contributed by Tony Dovgal
        (gifio.c, gifiostub.c, imageio.h).  See Makefile for instructions
        on enabling this.

 1.53   29 Dec 07
        Add 4th arg to pixDistanceFunction() to specify b.c.,
        and fixed output to 16 bpp grayscale pix. (seedfill*.c)
        New un-normalized block grayscale convolution (convolve.c)
        Fixed bug in getLogBase2(), so that pixMaxDynamicRange() works
        properly.  This is useful for displaying a 16 bpp pix as
        8 bpp (pixarith.c).  New function for getting rank val for
        rgb over a region specified by a mask (pix3.c).  New function
        for extremem values of rgb colormap (colormap.c).  New
        function pixGlobalNormNoSatRGB(), a variant of pixGlobalNormRGB()
        that prevents saturation for any component above a specified
        rank value (adaptmap.c).  Added mechanism for memory
        management of pix (pix1.c).  Added selective morphology by
        region given by a mask (morphapp.c).  Fixed prototype extracdtion
        to work properly with function prototypes as args; released
        version 1.2 of xtractprotos (parseprotos.c, xtractprotos.c).
        Add a boxa field for pixaa, along with serialization (pixabasic.c),
        and modified display of pixaa to include this (pixafunc.c).
        Coalesced the version numbers for pixa, pixaa, boxa, and boxaa
        serialization (pix.h).
        New progs: modifyhuesat displays modified versions on a grid;
        textlinemask shows simple methods for extracting textline masks.

 1.52   25 Nov 07
        Implemented Breuel's whitespace partitioning algorithm (partition.c).
        Generalized pixColorMagnitude() to allow different methods
        for computing the color amount of a pixel (colorcontent.c).
        New methods for computing overlap of boxes (boxfunc.c).
        New methods for painting (solid) and drawing (outline) of boxes,
        replacing boxaDisplay() with pixDrawBoxa*() and pixPaintBoxa*()
        (pix2.c, boxfunc.c).
        Ray Smith fixed bug in the distance function (seedfilllow.c).
        For pixConvertTo1() and pixConvertTo8(), treat input pixs as a
        const and never return a clone or altered cmap (pixconv.c).
        Make pixGlobalNormalRGB() crash-proof (adaptmap.c).
        Tony Dovgal added ability to read jpeg comment (jpegio.c).

 1.51   21 Oct 07
        Improved histogramming of gray and color images (pix3.c)
        Histogram statistics (numafunc.c).  Better handling of tiff
        formats, testing rle and packbits output and improving
        level 2 postscript conversion efficiency (readfile.c, psio.c).
        Test program for r/w and display of Sels (prog/seliotest.c).
        Use endiantest to determine automatically which flags to set
        when compiling for big- or little-endians (endiantest.c)
        Compute a color magnitude for each rgb pixel (colorcontent.c).
        Allow separate modification of hue and saturation (enhance.c).
        Global transform of color image for arbitrary white point (adaptmap.c).

 1.50   07 Oct 07
        |||||||||||||||||||||||||||||||||||||||||||||||||||||||||
        NOTE CAREFULLY: The  image format enum in imageio.h has
        changed.  This is an ABI change, and it requires
        recompilation of the library.
        |||||||||||||||||||||||||||||||||||||||||||||||||||||||||
        Suggestions by David Bryan again resulted in several changes,
        including improvements to the dwa generating functions and interfaces.
        Major improvements for dwa code generation, including an
        optional filename for the output code, adding function prototypes
        to the code so it can easily be linked outside the library.
        Addition of 2-way composable dwa functions for bricks, with
        code addition to the library, and a new interpreter for dwa
        composable brick sequences  (fmorphauto.c, fhmtauto.c,
        morphtemplate1.c, hmttemplate1.c, morphdwa.c, dwacomb*.2.c, morphseq.c)
        Exhaustively tested in six programs (prog/binmorph*_reg,
        prog/dwamorph*_reg).
        New input modes for Sels, from both color bitmap editors
        and a simple file format (sel1.c).
        Better Sel generation functions in sel2.c, including combs for
        composable brick operations and linear bricks for comparison.
        Removed unnecessary copies for more efficient border add'n & removal. 
        Added RLE basline enc/dec for tiff.
        Binary morphology documentation on the web page updated for these
        changes/additions.
        William Rucklidge unrolled inner loops and added LUTs to
        speed up several more functions, including correlation
        (correlscore.c), centroid calculation (morphapp.c),
        2x linear interp grayscale scanning (scalelow.c),
        thresholding to binary (grayquantlow.c), and removal
        of colormaps to gray (pixconv.c).

 1.49   23 Sep 07
        |||||||||||||||||||||||||||||||||||||||||||||||||||||||||
        NOTE CAREFULLY: The  image format enum in imageio.h has
        changed.  This is an ABI change, and it requires
        recompilation of the library.
        |||||||||||||||||||||||||||||||||||||||||||||||||||||||||
        Suggestions by David Bryan resulted in several changes.
        pixUnpackBinary() unpacks to all depths.
        Can now write and read tiff in LZW and ZIP (gzip) formats.
        These, like uncompressed tiff, work on all bit depths.
        Also enabled pnm 16 bpp r/w, both non-ascii and ascii.
        ioFormatTest() now has better coverage and clarity; this is
        used in prog/ioformats_reg.c.
        Rewrite of morphautogen code to implement opening and closing atomically.
        Cleaner interaction with new text templates (fmorphauto.c,
        fhmtauto.c, sarray.c, *template*.txt,).
        More regression testing (e.g., binmorph1_reg.c, binmorph3_reg.c).

 1.48   30 Aug 07
        William Rucklidge sped up pixCorrelationScore() by in-lining
        all bit operations (jbclass.c).
        Generalized rank filtering from 8 bpp to color (rank.c).
        Fixed many functions that take a dest pix so that they don't fail if
        the dimensions or depth are not consistent with the src pix.
        The underlying change for this is to pixCopy() (pix1.c).
        Improved display of Sel as a pix; added selaDisplayInPix() to
        display all Sels in a Sela, orthogonal rotations of Sels (sel1.c).
        New functions for thinning and thickening while preserving connectivity
        and avoiding both free end erosion and dendritic cruft (ccthin.c,
        prog/ccthin1_reg.c, prog/ccthin2_reg.c).
        New function pixaDisplayTiledInRows() for compactly tiling pix
        in a pixa, plus documentation of different existing methods. (pixafunc.c)

 1.47   22 Jul 07
        New brick rank order filter (rank.c, prog/ranktest.c, prog/rank_reg.c).
        Use mirror reflection b.c. to avoid special processing at
        boundaries (pix2.c).  Simple sobel edge detector (edge.c).
        Utility for assempling level 2 compressed images in PostScript
        (psio.c, prog/convertfilestops.c).  Enable read/write of 16 bpp,
        grayscale tiff (tiffio.c, pix2.c).
        New function for finding the number of c.c., which is a bit
          faster than finding the b.b. or the component images (conncomp.c)
        New functions for finding local extrema in grayscale image (seedfill.c)

 1.46   28 Jun 07
        Added interpreted mode for color morphology (morphseq.c).
        In functions, make effort to consistently do early initialization
        of ptrs to objects returned on the heap.  This is to try to
        avoid letting functions return uninitialized objects, even if
        the return early because of bad input.
        Split pixa.c into 2 files; revised the component filtering
        in both pixafunc.c and boxfunc.c.  Added component filtering
        for "thin" components.
        Added subsampling functions for numa and pta.
        Word segmentation now works at both full and half resolution.
        Better methods for displaying and tiling (for debugging),
        using pixDisplayWrite(), pixaReadFiles() and pixaDisplayTiledAndScaled().

 1.45   27 May 07
        Further improvements of orientation and mirror flip detection
        (flipdetect.c).  Added 2x rank downscaling and general integer
        replicative expansion (scale.c).  Simplified interface for
        averaging, and included tiled averaging, which is yet another
        integer reduction scaling function (pix3.c).

 1.44   1 May 07
        Split pix2.c into (pix2.c, pix3.c), with basic housekeeping
        functions (e.g., ops on borders, padding) in pix2.c.
        Split numarray.c into (numabasic.c, numafunc.c), with
        constructors and accessors in numabasic.c.  Added a number
        of histogram, rank value and interpolation functions to numafunc.c.
        Add rms and rank difference comparison functions (compare.c).
        Separated orientation and mirror flip detection; fixed the latter
        (flipdetect.c).

 1.43   24 Mar 07
        New and fixed functions for handling word boxes (classapp.c)
        More consistent use of L_* flags (e.g., sarray.h, morph.h)
        Morphology on color images (gray ops on each component) (colormorph.c)
        New methods for generating sels; we now have five methods in
        sel1.c and 3 others in selgen.c.  Also a function that
        displays Sels as an image, for use in documentation (sel1.c)
        New high-level converters, such as pixConvertTo8(), pixConvertTo32(),
         pixConvertLossless()   (pixconv.c)
        Identify regression tests, and rename them as prog/*_reg.c.
        Complete revision of plotting package (gplot.c)
        New functions for comparing pix (compare.c)
        New morph application functions, such as the ability to run a
        morph sequence separately on selected c.c. in an image, and
        a fast, quasi-tophat function (morphapp.c)
        Cleanup and new interfaces to border representations of c.c. (ccbord.c)
        Page segmentation application (pageseg.c)
        Better serialization with version control for all major structs.
        Morphological brick operations with 2-way composite sels (morph.c)

 1.42   26 Dec 06
        New sorting functions, including 2-d sorting, for boxa and pixa,
        and functions that sort by index (e.g., pixa --> pixa and
        for 2d, pixa --> pixaa; ditto for boxa).  
        New accessors for pix dimensions.  A new strtokSafe() to
        substitute for strtok_r (utils.c).
        Page flip detection, using both rasterop and dwa morphology
        (flipdetect.c), with dwa generation (fliphmtgen.c) and testing
        (prog/fliptest.c).
        Increased basic sels from 42 to 52 (sel2.c).
        Better high-level interfaces for binary morphology with
        brick (separable) sels, both for rasterop (morph.c) and for
        dwa (morphdwa.c); fully tested for both asymmetric and
        symmetric b.c. (prog/morphtest3.c).  Faster area mapping
        reduction for power-of-2 scaling.

 1.41   5 Nov 06
        Simplified morph enums, removing all unused ones (morph.h).
        Added new high-level interfaces for adaptive mapping (adaptmap.c).
        New method to extract color content of images (colorcontent.c).
        New method to generate sels from text strings, and to identify
        roman text that is not properly oriented (thanks to Adam Langley).
        Fast grayscale min/max (rank) scale reduction by integer factors.
        New accessors for box and sel, that should be used when possible.
        Thresholding grayscale mask by bandpass (grayquant.c).
        Use of strtok_r() for thread safety.

 1.40   15 Oct 06
        Fixed xtractprotos for cygwin.  Minor fixes and improved documentation
        (baseline.c, conncomp.c, pix2.c, morphseq.c, pts.c, numarray.c,
        utils.c, skew.c).  Add ability to quantize an rgb image to a
        specified colormap (colorquant.c); tested in prog/cmapquanttest.c.
        Modifications to allow conditional compilation on MS VC++,
        and to allow I/O calls to be stubbed out (new files: *iostub.c,
        zlibmemstub.c, pstdint.h, arrayaccess.h.ms60)

 1.39   31 Aug 06
        |||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
        NOTE CAREFULLY:  There has been an interface change to make
        affine, bilinear and projective transforms more general.
        The implementation has been changed to allow them to handle
        all image types and to make them faster (esp. with both sampled
        and interpolated mapping on color images).
        |||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
        Added prog/Makefile.mingw to build executables.  This is still
        in a relatively raw state.  It is necessary to download
        gnuwin32 packages for 4 libraries (jpeg, png, zlib, tiff)
        to link with leptonlib and the main, and I still have not
        been able to build static executables (they require jpeg2b.dll, etc.).

 1.38   8 Aug 06
        |||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
        NOTE CAREFULLY: There has been an interface change to both
        simplify and generalize the grayscale morphology operations:
            pixErodeGray(), pixDilateGray(), pixOpenGray(),
            pixCloseGray(), pixTophat() and pixMorphGradient().
        The prototypes are not changed; old code will compile, but
        it will be wrong!  The old interface had a size and a type
        (horizontal, vertical, square).  The new interface takes
        horizontal and vertical Sel dimensions.
        |||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||
        For cross-compilation to make windows programs, you can use
        src/Makefile.mingw to make a windows version of the library.
        6x scale-to-gray function donated by Alberto Accomazzi.
        Interpreter added for sequence of grayscale morphological
        operations, including the tophat (morphseq.c).
        Pixacc container added to simplify the interface
        for accumulator arithmetic using Pix.
        Removed fmorph.c and fmorphlow.c from the library.  These are
        very limited and were deprecated in favor of fmorphauto(), which
        autogens the code from (nearly) any Sel.
        Fixed some of the gray morphology operations, which had errors
        on the boundary.  All gray morph ops should now be rigorously
        OK (graymorph.c).  For testing of graymorph dualities, the 
        the graymorph interpreter, etc., see prog/morphgraytest.c. 

 1.37   10 Jul 06
        [After v.36 was released, Jeff Breidenbach built a Debian
        distribution of Leptonica based on v.36, and you can now get Leptonica
        as a Debian package.  Use "apt-cache search leptonica" to see
        what is available.]  The libraries are now combined into a single
        library (liblept.a, liblept.so) and the function prototypes are
        also in a single file (leptprotos.h).  cextract was found not
        to work on recent versions of linux that support 64 bit data types,
        and it is no longer distributed with leptonica.  Instead, I wrote
        a prototype extractor in leptonica (xtractprotos).  When you
        'make allprotos', it now uses this program.  The shared libraries
        now have major and minor numbers corresponding to the version.

 1.36   17 Jun 06
        Line graphics generation (graphics.c) reorganized; separated out pta
        generation from rendering.  Can now render with alpha blending.
        Examples of use are given in prog/graphicstest.c.
        Sort functions for basic geometrical objects now have the option
        of returning a numa giving the sort order on the original array.
        The pixa sort can sort with either clones or copies of the pix.

 1.35   21 May 06
        The efficiency of the multipage jbig unsupervised classifier is
        significantly improved due to a NumaHash struture implemented
        by Adam Langley.  Functions for computing runlength in 1 bpp
        images have been added.

 1.34   7 May 06
        Completely rewrote the jbig unsupervised classifier.
        It now works on multiple pages, and is more accurate in performing
        visually lossless substitutions.  You can classify by connected
        components, characters, or words.  The old data structures
        and interfaces have been removed.  New unpackers from 1 to 2 and
        1 to 4 bpp, with and without colormaps in the dest.

 1.33   18 Mar 06
        Generalized color snap to have different src and target colors,
        and to include colormaps (blend.c).  Distribute into root directory
        that specifies the version number (e.g., 1.33).  Add color
        space conversion between rgb and hsv.  Re-bundle thresholding
        code from (binarize*.c, dibitize*.c) to grayquant*.c.
        pixThreshold8() now also quantizes 8 bpp --> 8 bpp.
        High-level pixRotate() that optionally expands image sufficiently
        so that no pixels are lost in any sequence of rotations (rotate.c).
        Generalize shear to specify color of pixels brought in, including
        for in-place operation (shear.c, rotateshear.c).  Faster version of
        color rotation by area mapping, both about center and about UL corner.
        You can now use the standard color rotator (pixRotateAM) and get
        nearly the same speed as with the "Fast" one.

 1.32   4 Feb 06
        Ability to specify a sequence of binary morphological
        (& binary reduction/expansion) operations in a single
        function (morphseq.c).  Fast downscaling combined with conversion
        from rbg to gray and to binary (scale.c).  Utility for
        segmenting images by color (colorseg.c).

 1.31   7 Jan 06
        Remove more complicated functions that threshold to 2 bpp, 
        retaining the simplest interface.  Retest all thresholding and
        dithering.  Add "ascii" write of PNM.  Improve graphics writing
        of lines; generalize to colormaps.  New colorization functions
        (paintcmap.c, blend.c).

 1.30   22 Dec 05
        Remove most instances of fprintf(stderr, ...), except within
        DEBUG or encapsulated in error, warning or info macros. 
        As a result, there is no output to stderr if NO_CONSOLE_IO is defined. 
        Adaptive mapping to make bg uniform (adaptmap.c).  A few bug fixes.
        New PostScript output functions for embedding PS files
        (prog/converttops).  Generalized some image enhancement functions.
        New functions for generating hit-miss sels.

 1.29   12 Nov 05
        More flexible blending of two images, with and without colormaps
        (see blend.c).  Painting colormapped images through masks, etc
        (see paintcmap.c).  More flexible interface for gamma and
        contrast enhancement (see enhance.c).

 1.28   8 Oct 05
        Removed all pix colormaps for 1 bpp.  Allow programmatic resetting
        of binary morphology boundary conditions.  Added (yet) another
        simple octcube color quantizer.  New colormap operations.

 1.27   24 Sep 05
        Renamed many of the enums and typedefs to avoid namespace
        collisions.  This includes structs and typedefs for BMP.
        Interface change to pixClipRectangle(); apologies to everyone
        whose code is broken by these changes -- I hope it's worth it.
        Removed colormap.h; simplified all colormap usage, hiding details
        from all but a few colormap functions.  Am now saving file format
        in the pix when an image is read, and can by default write
        out in this format.  Resolution info added for jpeg and png.
        Added L_INFO* macros and l_info* fctns for printing
        (e.g., debugging) info.  Suggestions and code kindly
        supplied by Dave Bryan, who helped solve compatibility issues
        with MINGW32 (e.g., in timing and directory functions).
        Added some blending and linear TRC functions.
        Generalized pixEqual() to include all cases with and without
        colormaps.  New regression tests in prog: ioformats, equaltest.

 1.26   24 Jul 05
        Generalized affine pointwise to do interpolation as well as
        sampling.  For both projective and bilinear transforms,
        implemented using both sampling and interpolation.
        Added function to remove keystoning by computing the necessary
        projective transform and doing it.  Also find baselines in text images.
        Added downscaling using accurate area-mapping over subpixels.

 1.25   25 Jun 05
        Better endian conversion fctns for 2 and 4 byte words.
        Remove colormaps before converting by thresholds.
        Added functions to read header parameters for png and tiff.

 1.24   5 Jun 05
        Added image splitting to allow printing in tiles (as several pages).
        Added new octree quantization function to generate 4 and 8 bpp
        colormapped output (not dithered).  Fixed bmp resolution.
        Added new flag for colormap removal (using dest depth based on
        src colormap).  Added I/O tests (prog/ioformats.c)

 1.23   10 Apr 05
        Added thresholding from 8 bpp to 2 and 4 bpp, allowing specification
        of both the number of output levels and whether or not a colormap
        is made.

 1.22   27 Mar 05
        Add pointer queue facility.  To demonstrate it, you can now
        generate a binary maze using a cellular automaton and find
        the shortest path between two points in the maze.  Add heap
        of pointers (keyed on the first field), which is used to
        implement a priority queue.  This is applied to search for
        a "least cost" path on a grayscale image (a generalization
        of a binary maze).

 1.21   28 Feb 05
        Read/write of colormaps to file.  For gplot, add a new
        latex output terminal.  Bring ptrs into 21st century by
        including stdint.h, and using uintptr_t for the ptr address
        arithmetic in arrayaccess.*.  This seems to be OK back to
        RH 7.0, but if you run into trouble with an earlier
        C compiler, let me know.  Also, use enums for global
        constants whenever possible, and qualify named constants
        (e.g., ADD --> ARITH_ADD, HORIZ --> MORPH_HORIZ) to avoid
        possible interactions with other libraries.

 1.20   31 Jan 05
        Speed up of tiffio and pngio with byte swap generating new pix.
        In textops.c, ability to split string into paragraphs, 
        in preparation for more general typesetting.
        Automatic hit-miss Sel generation for pattern matching.
        Fast downscaling using a lowpass filter and subsampling.
        Generalization of several grayscale and color operations
        to work on colormapped images.  Improved scale-to-gray and
        scaling reduction operations to be antialiased for best results.

 1.19   30 Nov 04
        Additions to fileIO: (1) new jpeg reading options, such as
        returning warnings and scaled raster; (2) ability to write
        custom tiff flags.  Better tiling functions.
        Edge extraction, both with grayscale morphology
        and clipped convolution filters.  More general painting
        through a binary mask: pixSetMaskedGeneral().
        Unpacking from binary to 8, 16 and 32 bpp.  Thresholding
        and dithering from 8 bpp to 2 bpp ("dibitization").  New bitmap
        font facility, using a single rendered font in a variety of
        sizes: allows painting the text on an image (binary, gray, RGB).
        (People have asked for the ability to write text on images).

 1.18   25 Aug 04
        Changed typedefs of built-in types to avoid possible conflicts.
        Cleaned up and tested all programs in the prog directory.
        Simplified and fixed the pixSetMasked() and pixCombineMasked()
        functions.

 1.17   31 May 04
        Implemented distance function for 16 bpp.  We can now generate
        out 16 bpp PNG.  Simple programs for generating PS from a
        directory of g4tiff or jpeg images.  Changed implementation of
        erosion to allow either asymmetric or symmetric boundary conditions.
        The distinction is described on the binary morphology web page.
        Allow read/write of multipage TIFF files.  Implemented
        read/write of PNM files.

 1.16   31 Mar 04
        New depth conversion functions, improved conversion to false color,
        new contour rendering (onto 1 bpp or onto the src grayscale image),
        new orthogonal rotations, better interface for doing arithmetic
        on 2-d arrays using a pix, improved distance function.

 1.15   31 Jan 04
        Fast interpolated color rotation with 4x4 subpixels; has
        nearly the accuracy of the slower method using 16x16 subpixels.
        Demonstration of line removal from grayscale sketch in
        prog/lineremoval.c.  Conversion of grayscale to false color.
        Fixed shear and rotation functions to handle angle = 0.0 properly.
        Other small fixes and interface improvements.

 1.14   30 Nov 03
        Small implementation changes to list.c.  Better sorting
        routines for number arrays (numa), plus sorting for box
        arrays (boxa) and pix arrays (pixa).  PostScript wrapper
        for jpeg.  Better handling of colormaps, and a simple
        function to convert an RGB pix with not more than 256
        colors to the smallest colormapped pix.  PS output wrappers
        for JFIF JPEG and TIFF G4 files.  Comments compatible
        with doxygen for automatic documentation.

 1.13   31 Oct 03
        Cleaned up documentation in src.  Made libraries and test programs
        ANSI C++ compliant.  Added special cases to rasterops for
        alignment to word boundaries.  Fixed pngio.c to work with
        most recent libpng (1.2.5).

 1.12   30 Jun 03
        Implemented border chain representation from a binary image,
        writes/reads a compressed version, and renders the original
        image back from the borders.   Also writes outline file out
        in svg format.  Number arrays (numa) and point arrays (pta)
        are also extended to 2nd level arrays (numaa, ptaa).
        Serialized I/O for boxa, pta, and pixa.

 1.11   31 May 03
        Implemented generic list handling, for doubly-linked
        list cons cells and arbitrary objects.

 1.10   14 Apr 03
        Implemented simple image enhancements in gray and color:
        gamma correction, contrast enhancement, unsharp masking.
        Extended smoothing via block convolution to color.
        Implemented auto-gen'd DWA version of hit-miss transform;
        the code for generating these hmt routines is very similar to
        that for DWA auto-gen'd erosion and dilation.

 1.9    28 Feb 03
        Implemented a safe, expandable byte queue.  As an example of
        its use, implemented memory-to-memory compression and decompression
        using zlib.  Generalized PS write to include RGB color.
        Implemented a method to find image skew.

 1.8    31 Jan 03
        Implemented a simple 1-pass color quantization with dithering,
        and improved the 2-pass octree color quantization.
        Documented with an application page, that includes jbig2.
        Added new general sampling operations and made a table
        that summarizes the available scaling operations.

 1.7    31 Dec 02
        Added pixHtmlViewer(), a formatter that allows portable viewing of
        a set of images (like a slide show) in a browser.
        Implemented better octree color quantization, with variable
        number of colors, pruning the octree for good color clusters,
        and fast traversal for pixel assignment to colormap.

 1.6    30 Nov 02
        Generalized shear and shear rotation to arbitrary locations
        about which the operation is performed.  Implemented in-place
        translation using pixRasteropIP().  Implemented arbitrary
        affine transform of image two ways: pointwise and sequential.
        Added binarization by error diffusion.  Added simple color
        quantization by octree.

 1.5    31 Oct 02
        Put jpeglib.h in local directory.  This, along with the jmorecfg.h
        file there prevents compiler warnings about redefined typedefs.
        Compiled everything with g++ to make strictly ansi C compatible.
        Added interface gplotFromFile() for simple file-based plotting with 
        gnuplot 3.7.2.   Added functions to convert 2, 4 and 8 bpp
        color-mapped (i.e., palletted) images to 24 bpp color or
        8 bpp grayscale.  Added several jbig2 application cores that
        only require a simple wrapper to make into programs.

 1.4    30 Sep 02
        Added interface to gnuplot 3.7.2 and to x11 display of images. 
        Added new functions with arrays of images for use in applications
        such as jbig2 encoders, along with a simple jbig2 implementation
        using either hausdorff or correlation scoring.  Added centroid
        finder for images.  For accessing image arrays from arrays of
        image arrays, added a "new reference" (NEW_REF) flag, with a
        ref count attached to the array.  Added power-of-2 binary
        expansion and reduction.

 1.3    30 Jun 02
        Extended connected components to 8.  Added morphological
        operations tophat and hdome, along with clipped arithmetic
        operators on grayscale images.  Fixed memory error in
        rasteropGeneralLow() that was found using valgrind.
        Tested most operations with valgrind for memory errors.
        Replaced integer arrays with number arrays, to include floats.
        Added arithmetic functions on grayscale images.

 1.2    30 May 02
        Added connected component utility, stack utility, pix arrays,
        line drawing and seed filling.  Binary reconstruction,
        both morphological and raster-oriented, are now supported
        for 4 and 8 connected fills.  Added the distance function
        on binary images, grayscale reconstruction, and grayscale
        morphology using the Gil-Werman method.

 1.1    30 Apr 02
        Added orthogonal rotations, binary scaling, PS output,
        binary reconstruction, integer arrays, structuring element
        input/output.

 1.0    25 Feb 02
        Initial distribution, with rasterops, binary morphology (two
        implementations: rasterops and dwa), affine transforms
        (translation, shear, scaling, rotation), fast convolution,
        and basic i/o (BMP, PNG and JPEG).

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
