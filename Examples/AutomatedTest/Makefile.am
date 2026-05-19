## Process this file with automake to produce Makefile.in

exampledir=${datadir}/@PACKAGE@/Examples/Automated

if ENABLE_EXAMPLES
if ENABLE_AUTOMATED

example_PROGRAMS = AutomatedTest

AutomatedTest_SOURCES = AutomatedTest.c
AutomatedTest_LDADD = -lcunit -lcunitexamples
AutomatedTest_LDFLAGS = -L.. -lm
AM_CPPFLAGS = -I.. -I$(top_srcdir)/Examples -I$(top_builddir)/CUnit/Headers -I$(top_srcdir)/CUnit/Headers

if ENABLE_CURSES
AutomatedTest_LDADD += -l$(CURSES_LIB)
endif

example_DATA = README
DISTCLEANFILES = TestAutomated-Listing.xml TestAutomated-Results.xml CUnit-Memory-Dump.xml

endif
endif
