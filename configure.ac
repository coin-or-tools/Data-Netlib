# Copyright (C) 2006 International Business Machines.
# All Rights Reserved.
# This file is distributed under the Eclipse Public License.

# Author:  Andreas Waechter            IBM    2006-04-13

#############################################################################
#                       Names and other basic things                        #
#############################################################################

AC_INIT([Netlib],[1.3.0],[https://github.com/coin-or-tools/Data-Netlib/issues/new],[coin-or-netlib],[https://github.com/coin-or-tools/Data-Netlib/])

AC_COPYRIGHT([
Copyright 2006 International Business Machines and others.
All Rights Reserved.
This file is part of the open source package Coin which is distributed
under the Eclipse Public License.])

# List one file in the package so that the configure script can test
# whether the package is actually there.

AC_CONFIG_SRCDIR(configure.ac)

# Do some generic initialization work.

AC_COIN_INITIALIZE

# Check for libz. The hidden assumption is that if libz is present, code will
# use it to read compressed (.gz) files. If it's not present, or disabled with
# --disable-zlib, uncompressed copies of compressed files will be created when
# make is run.

AC_COIN_CHK_ZLIB

#############################################################################
#                        Specify the data files                             #
#############################################################################

AC_COIN_EXAMPLE_FILES([*.mps.gz])

##############################################################################
#                   Finish up by writing all the output                      #
##############################################################################

# Specify the files that configure should generate from template (.in) files.

AC_CONFIG_FILES([Makefile coindatanetlib.pc])

# Finally, let configure write all the output ...

AC_COIN_FINALIZE
