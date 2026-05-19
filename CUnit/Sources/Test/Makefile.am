## Process this file with automake to produce Makefile.in

if ENABLE_TEST
AM_CPPFLAGS = -I$(top_builddir)/CUnit/Headers -I$(top_srcdir)/CUnit/Headers \
	-DMEMTRACE -DCUNIT_BUILD_TESTS -DCUNIT_DO_NOT_DEFINE_UNLESS_BUILDING_TESTS
testdir=${datadir}/@PACKAGE@/Test

test_PROGRAMS = test_cunit
TESTS = $(test_PROGRAMS)
test_cunit_SOURCES = test_cunit.c test_cunit.h
test_cunit_LDADD = ../libcunit_test.a
test_cunit_LDFLAGS = -L..
DISTCLEANFILES = CUnit-Memory-Dump.xml

endif
