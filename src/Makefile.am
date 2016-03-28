distdir = $(top_srcdir)/$(PACKAGE)-$(VERSION)/src
# consider headers:
#   - include_HEADERS
#   - nobase_include_HEADERS
#   - pkginclude_HEADERS
#   - dist_HEADERS
#   - nodist_HEADERS
#   - noinst_HEADERS
dist_HEADERS =

BUILT_SOURCES = diag.c diag.h
EXTRA_DIST = diag.txt gen-diag
CLEANFILES = $(BUILT_SOURCES) *.core core
#CLEANFILES += *.in
AM_MAKEFLAGS = -s

lib_LTLIBRARIES = libmrkyaml.la

nobase_include_HEADERS = mrkyaml.h

noinst_HEADERS =

libmrkyaml_la_SOURCES = mrkyaml.c
nodist_libmrkyaml_la_SOURCES = diag.c

if DEBUG
DEBUG_FLAGS = -g -O0 @CC_DEBUG@
else
DEBUG_FLAGS = -DNDEBUG -O3
endif

libmrkyaml_la_CFLAGS = $(DEBUG_FLAGS) -Wall -Wextra -Werror -std=c99 @_GNU_SOURCE_MACRO@ -I$(top_srcdir)/src -I$(top_srcdir) -I$(includedir)

libmrkyaml_la_LDFLAGS = -version-info 0:0:0 -L$(libdir) -lmrkcommon -lyaml
#libmrkyaml_la_LDFLAGS = -version-info 0:0:0

SUBDIRS = .

diag.c diag.h: diag.txt
	$(AM_V_GEN) /bin/sh ./gen-diag mrkyaml

run: all
	for i in $(bin_PROGRAMS); do if test -x ./$$i; then LD_LIBRARY_PATH=$(libdir) ./$$i; fi; done;

testrun:
	for i in $(SUBDIRS); do if test "$$i" != "."; then cd $$i && $(MAKE) testrun && cd ..; fi; done;