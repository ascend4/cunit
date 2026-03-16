# CUnit

[![MSYS2 Build](https://github.com/ascend4/cunit/actions/workflows/msys2-build.yml/badge.svg)](https://github.com/ascend4/cunit/actions/workflows/msys2-build.yml)
[![Ubuntu Build](https://github.com/ascend4/cunit/actions/workflows/ubuntu-build.yml/badge.svg)](https://github.com/ascend4/cunit/actions/workflows/ubuntu-build.yml)

CUnit is a unit testing framework for C.

The basic framework is platform/version independent and should be portable to
all platforms. CUnit provides various interfaces to the framework, some of
which are platform dependent (for example, curses on Unix-like systems).
Building other interfaces should be straightforward with the facilities
provided in the framework.

CUnit is built as either a static or shared library which provides framework
support when linked into user testing code. The framework complies with the
conventional structure of test cases bundled into suites which are registered
with the framework for running. See the documentation for more about the
structure and use of the framework.

Note: the Windows-specific GUI interface is not yet written. It is still
necessary to use either the automated, basic, or console interfaces to CUnit
on Windows at this time.

## Important Note: Changes to CUnit Structure and Interface

As of version 2.0, the interface functions used to interact with the CUnit
framework have changed. The original interface did not attempt to protect user
code from name clashes with public CUnit functions and variables. To minimize
such name clashes, all CUnit public functions are now prefixed with `CU_`.

The old public names are deprecated as of version 2.0, but continue to be
supported with conversion macros. In order to compile older code using the
original interface, it is now necessary to compile with the macro
`-DUSE_DEPRECATED_CUNIT_NAMES` defined. If there are any problems compiling
older code, please file a bug report.

In addition, the DTD and XSL files for output from the automated test
interface have been updated to support both old and new file structure. A List
or Run file generated using the version 1.1 library should be valid under the
version 2 DTDs and formatted correctly by the version 2 XSLs. This has not
been extended to the Memory-Dump DTD and XSL files; memory dumps created using
version 1.1 are ill-formed and incorrectly formatted using the version 2 DTD
and XSL files.

Another exception to backward compatibility occurs if the user has directly
manipulated the global variables in version 1.1. The original CUnit structure
included global variables `error_number` and `g_pTestRegistry` which have been
removed from the global namespace as of version 2.0. Any user code which
directly accessed these variables will break. The variables must be retrieved
using the accessor functions `CU__get_error()` and `CU_get_registry()`.

Similarly, user code retrieving the active test registry and directly
manipulating the `uiNumberOfFailures` or `pResult` members will break. These
members have been moved to the `TestRun.c` part of the framework and are no
longer available in the test registry as of version 2.0.

Another change in version 2.0 is the update of the framework terminology. What
were termed "test groups" in the original structure are now called "suites",
and "test cases" are now just "tests". This change was made to bring CUnit
into conformance with standard testing terminology, and results in a change in
the name of some functions, for example `run_group_tests()` is now
`CU_run_suite()`.

## Building the CUnit Library and Examples

### All Platforms

Jam support has been removed. Use the GNU Autotools build on Unix-like
platforms, or the Visual Studio project files on Windows.

### Linux

The standard GNU build system should succeed in building and installing CUnit:

1. `aclocal` (if necessary)
2. `autoconf` (if necessary)
3. `automake` (if necessary)
4. `chmod u+x configure` (if necessary)
5. `./configure --prefix <installation-prefix>`
6. `make`
7. `make install`

What is installed:

1. `libcunit.a` (library file)
2. CUnit header files
3. DTD and XSL files supporting XML output files in the share directory
4. Man pages in the relevant man directories under the installation path
5. The HTML users guide in the `doc` subdirectory of the installation path
6. Example and test programs in the `share` subdirectory of the install path

### Windows

Jam support has been removed. A set of old VC6 project files is included which
have been partially updated but not tested. If they do not work and you get
them working, the project would be happy to include them in the CUnit
distribution. A set of Visual Studio 2003/VC7 solution and project files has
also been provided in the `VC7` subdirectory. Similarly, a set of Visual
Studio 2005/VC8 solution and project files is located in the `VC8`
subdirectory. The latter should work with all versions of VC 2005, including
the Express edition.

## Release Process

GitHub releases are created from version tags. The release workflow expects
the `VERSION` file to contain the distribution version in the historical
format, for example `2.1-3`, and the Git tag to use the normalized form with
dots, for example `v2.1.3`.

If the tag, `VERSION`, and `packaging/msys2/PKGBUILD` version fields do not
all match, the release workflow fails before publishing any assets.

To publish a release:

1. Update `VERSION` and the packaging metadata.
2. Commit the release changes.
3. Create and push an annotated tag matching `VERSION`, such as `v2.1.3`.

The release workflow publishes both a source tarball and the MSYS2 UCRT64
`.pkg.tar.zst` package for the tagged commit. The source tarball is named
`cunit-<VERSION>.tar.gz` and extracts into `cunit-<VERSION>/`. Release
tarballs are generated with `git archive`; the old manual `make tarball`
path is intentionally disabled.
