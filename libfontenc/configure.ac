#  Copyright 2005 Red Hat, Inc.
#
#  Permission to use, copy, modify, distribute, and sell this software and its
#  documentation for any purpose is hereby granted without fee, provided that
#  the above copyright notice appear in all copies and that both that
#  copyright notice and this permission notice appear in supporting
#  documentation, and that the name of Red Hat not be used in
#  advertising or publicity pertaining to distribution of the software without
#  specific, written prior permission.  Red Hat makes no
#  representations about the suitability of this software for any purpose.  It
#  is provided "as is" without express or implied warranty.
#
#  RED HAT DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE,
#  INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS, IN NO
#  EVENT SHALL RED HAT BE LIABLE FOR ANY SPECIAL, INDIRECT OR
#  CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE,
#  DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER
#  TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR
#  PERFORMANCE OF THIS SOFTWARE.
#

# Initialize Autoconf
AC_PREREQ([2.60])
AC_INIT([libfontenc], [1.1.3],
        [https://bugs.freedesktop.org/enter_bug.cgi?product=xorg], [libfontenc])
AC_CONFIG_SRCDIR([Makefile.am])
AC_CONFIG_HEADERS([config.h])

# Initialize Automake
AM_INIT_AUTOMAKE([foreign dist-bzip2])

# Initialize libtool
AC_PROG_LIBTOOL

# Require X.Org macros 1.8 or later
m4_ifndef([XORG_MACROS_VERSION],
          [m4_fatal([must install xorg-macros 1.8 or later before running autoconf/autogen])])
XORG_MACROS_VERSION(1.8)
XORG_DEFAULT_OPTIONS

# Require X.Org's font util macros 1.1 or later for XORG_FONTROOTDIR
m4_ifndef([XORG_FONT_MACROS_VERSION],
	  [m4_fatal([must install X.Org font-util 1.1 or later before running autoconf/autogen])])
XORG_FONT_MACROS_VERSION(1.1)
XORG_FONTSUBDIR([ENCODINGSDIR], [encodingsdir], [encodings])

# zlib
AC_CHECK_HEADER([zlib.h], [],
                AC_MSG_FAILURE([zlib.h is required to compile libfontenc]))
AC_CHECK_LIB(z, gzclose, [],
             AC_MSG_FAILURE([zlib is required to compile libfontenc]))

# Obtain compiler/linker options for depedencies
PKG_CHECK_MODULES(FONTENC, xproto)

# Allow checking code with lint, sparse, etc.
XORG_WITH_LINT
LINT_FLAGS="${LINT_FLAGS} ${FONTENC_CFLAGS}"

AC_CONFIG_FILES([Makefile
		src/Makefile
		fontenc.pc])
AC_OUTPUT
