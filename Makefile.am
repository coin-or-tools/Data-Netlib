# Copyright (C) 2006 International Business Machines and others.
# All Rights Reserved.
# This file is distributed under the Eclipse Public License.

## $Id$

# Author:  Andreas Waechter           IBM    2006-04-13

AUTOMAKE_OPTIONS = foreign

########################################################################
#                List files that should be distributed                 #
########################################################################

EXTRA_DIST = $(EXAMPLE_DIST_FILES)

datacoindir = $(pkgdatadir)

# If zlib is available, install compressed files. If zlib is not available,
# install uncompressed copies of compressed files. EXAMPLE_DIST_FILES and
# EXAMPLE_UNCOMP_FILES are identical except that any `.gz' suffixes are
# stripped from names in EXAMPLE_UNCOMP_FILES. EXAMPLE_CLEAN_FILES (below)
# is exactly the set of names that have been stripped of `.gz'.

if COIN_HAS_ZLIB
datacoin_DATA = $(EXAMPLE_DIST_FILES)
else
datacoin_DATA = $(EXAMPLE_UNCOMP_FILES)
endif

pkgconfiglibdir = $(libdir)/pkgconfig
pkgconfiglib_DATA = coindatanetlib.pc

include BuildTools/Makemain.inc

test:
	@echo "No test available."

########################################################################
#           Build and clean actions                                    #
########################################################################

# We always need to clean these files, which are uncompressed copies of
# compressed files, created when zlib is not available.

CLEANFILES = $(EXAMPLE_CLEAN_FILES)

# If this is a VPATH build, we'll create links in the build directory from
# files in the source directory, and we'll need to clean them up when we're
# done.

if COIN_VPATH_BUILD
CLEANFILES += $(EXAMPLE_DIST_FILES)
endif

# The files of EXAMPLE_DIST_FILES must be phony targets.  Otherwise, make
# considers the file found in the source directory to be sufficient and doesn't
# create the link.  This becomes a problem because `make install' now feels
# it should invoke the rule for each file prior to installation. Hence the
# guard to check if the file is already present.

if COIN_VPATH_BUILD
$(EXAMPLE_DIST_FILES):
	@test -f $@  || $(LN_S) $(srcdir)/$@ $@

MORE_PHONY = $(EXAMPLE_DIST_FILES)
endif

########################################################################
#           Extra uninstall actions                                    #
########################################################################

# Remove the directory created at installation

uninstall-local:
	@if test -d $(datacoindir) ; then rmdir $(datacoindir) ; fi

########################################################################
#           Extra targets for uncompressing the .gz files              #
########################################################################

# If configure has determined that libz can be used, compressed files can
# be read and we don't have to uncompress. Otherwise, uncompress the files.
# EXAMPLE_CLEAN_FILES contains just the names of compressed files, stripped
# of the .gz suffix. This will trigger creation of an uncompressed copy.
# This target creates uncompressed files without deleting the original
# compressed files.

$(EXAMPLE_CLEAN_FILES):
	gzip -d -c $(srcdir)/$@.gz > $@

.PHONY: $(MORE_PHONY)

