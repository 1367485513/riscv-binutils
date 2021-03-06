# Copyright (C) 1989-2019 Free Software Foundation, Inc.

# This file is part of GDB.

# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

prefix = /home/majiahao/ddddd/riscv-binutils-install
exec_prefix = ${prefix}

host_alias = x86_64-pc-linux-gnu
target_alias = riscv64
program_transform_name = s&^&riscv64-&
bindir = ${exec_prefix}/bin
libdir = ${exec_prefix}/lib
tooldir = $(libdir)/$(target_alias)

datadir = ${datarootdir}
localedir = ${datarootdir}/locale
mandir = ${datarootdir}/man
man1dir = $(mandir)/man1
man2dir = $(mandir)/man2
man3dir = $(mandir)/man3
man4dir = $(mandir)/man4
man5dir = $(mandir)/man5
man6dir = $(mandir)/man6
man7dir = $(mandir)/man7
man8dir = $(mandir)/man8
man9dir = $(mandir)/man9
infodir = ${datarootdir}/info
datarootdir = ${prefix}/share
docdir = ${datarootdir}/doc/${PACKAGE_TARNAME}
htmldir = ${docdir}
pdfdir = ${docdir}
includedir = ${prefix}/include

SHELL = /bin/bash
EXEEXT = 

INSTALL = /usr/bin/install -c
INSTALL_PROGRAM = /usr/bin/install -c
INSTALL_DATA = /usr/bin/install -c -m 644

DESTDIR =

AR = ar
AR_FLAGS = qv
RANLIB = ranlib
DLLTOOL = @DLLTOOL@

SUBDIRS = import
CLEANDIRS = $(SUBDIRS)
REQUIRED_SUBDIRS = $(SUBDIRS)

CC=gcc

# Directory containing source files.
srcdir = ../../../gdb/gnulib
VPATH = ../../../gdb/gnulib

CC_LD=$(CC)

# CFLAGS is specifically reserved for setting from the command line
# when running make.  I.E.  "make CFLAGS=-Wmissing-prototypes".
CFLAGS = -g -O2

# LDFLAGS is specifically reserved for setting from the command line
# when running make.
LDFLAGS = -static-libstdc++ -static-libgcc 

FLAGS_TO_PASS = \
	"prefix=$(prefix)" \
	"exec_prefix=$(exec_prefix)" \
	"infodir=$(infodir)" \
	"datarootdir=$(datarootdir)" \
	"docdir=$(docdir)" \
	"htmldir=$(htmldir)" \
	"pdfdir=$(pdfdir)" \
	"libdir=$(libdir)" \
	"mandir=$(mandir)" \
	"datadir=$(datadir)" \
	"includedir=$(includedir)" \
	"against=$(against)" \
	"DESTDIR=$(DESTDIR)" \
	"AR=$(AR)" \
	"AR_FLAGS=$(AR_FLAGS)" \
	"CC=$(CC)" \
	"CFLAGS=$(CFLAGS)" \
	"CXX=$(CXX)" \
	"CXXFLAGS=$(CXXFLAGS)" \
	"DLLTOOL=$(DLLTOOL)" \
	"LDFLAGS=$(LDFLAGS)" \
	"RANLIB=$(RANLIB)" \
	"MAKEINFO=$(MAKEINFO)" \
	"MAKEINFOFLAGS=$(MAKEINFOFLAGS)" \
	"MAKEINFO_EXTRA_FLAGS=$(MAKEINFO_EXTRA_FLAGS)" \
	"MAKEHTML=$(MAKEHTML)" \
	"MAKEHTMLFLAGS=$(MAKEHTMLFLAGS)" \
	"INSTALL=$(INSTALL)" \
	"INSTALL_PROGRAM=$(INSTALL_PROGRAM)" \
	"INSTALL_DATA=$(INSTALL_DATA)" \
	"RUNTEST=$(RUNTEST)" \
	"RUNTESTFLAGS=$(RUNTESTFLAGS)"

all installcheck check info install-info clean-info dvi pdf install-pdf html install-html: force
	@$(MAKE) $(FLAGS_TO_PASS) DO=$@ "DODIRS=$(SUBDIRS)" subdir_do

# Traditionally "install" depends on "all".  But it may be useful
# not to; for example, if the user has made some trivial change to a
# source file and doesn't care about rebuilding or just wants to save the
# time it takes for make to check that all is up to date.
# install-only is intended to address that need.
install: all
	@$(MAKE) $(FLAGS_TO_PASS) install-only

install-only: $(CONFIG_INSTALL)
	@$(MAKE) DO=install "DODIRS=$(SUBDIRS)" $(FLAGS_TO_PASS) subdir_do

uninstall: force $(CONFIG_UNINSTALL)
	@$(MAKE) DO=uninstall "DODIRS=$(SUBDIRS)" $(FLAGS_TO_PASS) subdir_do

# Convenience rule to handle recursion.
$(LIBGNU) $(GNULIB_H): all-lib
all-lib: import/Makefile
	@$(MAKE) $(FLAGS_TO_PASS) DO=all DODIRS=import subdir_do
.PHONY: all-lib

clean mostlyclean: $(CONFIG_CLEAN)
	@$(MAKE) $(FLAGS_TO_PASS) DO=clean "DODIRS=$(CLEANDIRS)" subdir_do

distclean: clean
	@$(MAKE) $(FLAGS_TO_PASS) DO=distclean "DODIRS=$(CLEANDIRS)" subdir_do
	rm -f config.status config.h stamp-h
	rm -f config.log config.cache
	rm -f Makefile
	rm -rf $(DEPDIR)

maintainer-clean: local-maintainer-clean do-maintainer-clean distclean
realclean: maintainer-clean

local-maintainer-clean:
	@echo "This command is intended for maintainers to use;"
	@echo "it deletes files that may require special tools to rebuild."
	rm -f config.status

do-maintainer-clean:
	@$(MAKE) $(FLAGS_TO_PASS) DO=maintainer-clean "DODIRS=$(CLEANDIRS)" \
		subdir_do

subdir_do: force
	@for i in $(DODIRS); do \
		case $$i in \
		$(REQUIRED_SUBDIRS)) \
			if [ ! -f ./$$i/Makefile ] ; then \
				echo "Missing $$i/Makefile" >&2 ; \
				exit 1 ; \
			fi ;; \
		esac ; \
		if [ -f ./$$i/Makefile ] ; then \
			if (cd ./$$i; \
				$(MAKE) $(FLAGS_TO_PASS) $(DO)) ; then true ; \
			else exit 1 ; fi ; \
		else true ; fi ; \
	done

Makefile: Makefile.in config.status
	# Regenerate the Makefile.
	CONFIG_FILES="Makefile" \
	  CONFIG_COMMANDS= \
	  CONFIG_HEADERS= \
	  $(SHELL) config.status

gnulib/Makefile: gnulib/Makefile.in config.status
	CONFIG_FILES="gnulib/Makefile" \
	  CONFIG_COMMANDS="depfiles" \
	  CONFIG_HEADERS= \
	  CONFIG_LINKS= \
	  $(SHELL) config.status

config.h: stamp-h ; @true
stamp-h: $(srcdir)/config.in config.status
	CONFIG_HEADERS=config.h:config.in \
	  CONFIG_COMMANDS="default depdir" \
	  CONFIG_FILES= \
	  CONFIG_LINKS= \
	  $(SHELL) config.status

config.status: $(srcdir)/configure
	$(SHELL) config.status --recheck

ACLOCAL = aclocal
ACLOCAL_AMFLAGS = -I import/m4 -I ../../config

include $(srcdir)/aclocal-m4-deps.mk

$(srcdir)/aclocal.m4: # configure.ac $(aclocal_m4_deps)
	cd $(srcdir) && $(ACLOCAL) $(ACLOCAL_AMFLAGS)

AUTOCONF = autoconf
configure_deps = $(srcdir)/configure.ac $(srcdir)/aclocal.m4
$(srcdir)/configure: # $(configure_deps)
	cd $(srcdir) && $(AUTOCONF)

AUTOHEADER = autoheader
$(srcdir)/config.in: # $(configure_deps)
	cd $(srcdir) && $(AUTOHEADER)
	rm -f stamp-h
	touch $@

# automatic rebuilding in automake-generated Makefiles requires
# this rule in the toplevel Makefile, which, with GNU make, causes
# the desired updates through the implicit regeneration of the Makefile
# and all of its prerequisites.
am--refresh:
	@:

force:

force_update:

# GNU Make has an annoying habit of putting *all* the Makefile variables
# into the environment, unless you include this target as a circumvention.
# Rumor is that this will be fixed (and this target can be removed)
# in GNU Make 4.0.
.NOEXPORT:

# GNU Make 3.63 has a different problem: it keeps tacking command line
# overrides onto the definition of $(MAKE).  This variable setting
# will remove them.
MAKEOVERRIDES=

# Disable implicit make rules.
include $(srcdir)/../disable-implicit-rules.mk

### end of the libgnu Makefile.in.
