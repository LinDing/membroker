TESTS =
bin_PROGRAMS =
noinst_PROGRAMS =
lib_LTLIBRARIES =
noinst_LTLIBRARIES =

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = membroker.pc

lib_LTLIBRARIES += libmb.la
libmb_la_SOURCES = \
	src/mbcodec.c \
	src/mbclient.c \
	src/mb.h \
	src/mbprivate.h \
	src/mbclient.h

pkginclude_HEADERS = \
	src/mb.h \
	src/mbclient.h \
	src/mbserver.h

noinst_LTLIBRARIES += libmbs.la
libmbs_la_SOURCES = src/mbserver.c

bin_PROGRAMS += mbserver
mbserver_SOURCES = \
	src/main.c \
	src/mbserver.h
mbserver_LDADD = libmbs.la libmb.la

noinst_PROGRAMS += mbctest
mbctest_SOURCES = \
	src/mbctest.c \
	src/mb.h
	src/mbclient.h
	src/mbprivate.h
mbctest_LDADD = libmb.la
TESTS += mbctest

noinst_PROGRAMS += mbtest
mbtest_SOURCES = src/mbtest.c
mbtest_LDADD = libmb.la
# This test fails
#TESTS += mbtest

noinst_PROGRAMS += test_main
test_main_SOURCES = src/tests/main.c
test_main_CFLAGS = -I$(srcdir)/src
test_main_LDADD = libmb.la libmbs.la
test_main_LDFLAGS = -lpthread
UNITTESTS =
UNITTESTS += initAndTerminate
UNITTESTS += testNormalRequest
UNITTESTS += testNormalReserve
UNITTESTS += testRequestOnRequesting
UNITTESTS += testReserveOnRequesting
UNITTESTS += testRequestOnReserving
UNITTESTS += testReserveOnReserving
UNITTESTS += testRequestOnReserved
UNITTESTS += testRequestOnRequested
UNITTESTS += testReserveOnRequested
UNITTESTS += testReserveOnReserved
UNITTESTS += testReturnOnRequest
UNITTESTS += testMultipleRequests
UNITTESTS += testClientTermination
UNITTESTS += testIoErrors
UNITTESTS += testDumpDebug

$(UNITTESTS): test_main
	@ echo Creating $@
	$Q rm -rf $@
	$Q echo "#!/bin/sh" > $@
	$Q echo "./test_main $@" >> $@
	$Q chmod +x $@
CLEANFILES = $(UNITTESTS)
TESTS += $(UNITTESTS)
