# -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

# $Id: configure.ac 57 2007-10-30 17:19:18Z lennart $

# This file is part of xmms-pulse.
#
# xmms-pulse is free software; you can redistribute it and/or modify it
# under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# xmms-pulse is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
# General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with xmms-pulse; if not, write to the Free Software Foundation,
# Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA.

AC_PREREQ(2.57)
AC_INIT([xmms-pulse],[0.9.4],[mzkzzfchyfr (at) 0pointer (dot) de])
AC_CONFIG_SRCDIR([src/plugin.c])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE([foreign 1.9 -Wall])

AC_SUBST(PACKAGE_URL, [http://0pointer.de/lennart/projects/xmms-pulse/])

if type -p stow > /dev/null && test -d /usr/local/stow ; then
   AC_MSG_NOTICE([*** Found /usr/local/stow: default install prefix set to /usr/local/stow/${PACKAGE_NAME}-${PACKAGE_VERSION} ***])
   ac_default_prefix="/usr/local/stow/${PACKAGE_NAME}-${PACKAGE_VERSION}"
fi

# Checks for programs.
AC_PROG_CC
AC_PROG_LN_S
AC_PROG_LIBTOOL

AC_CHECK_FUNCS([gethostname]) 
AC_CHECK_HEADERS([limits.h])
AC_C_CONST
AC_FUNC_MALLOC
AC_TYPE_SIZE_T

PKG_PROG_PKG_CONFIG

if test -d ../pulseaudio ; then
   PULSE_CFLAGS='-I$(top_srcdir)/../pulseaudio/src'
   PULSE_LIBS='-L$(top_srcdir)/../pulseaudio/src/.libs -lpulse'
   echo "*** Found pulseaudio in ../pulseaudio, using that version ***"
else
   PKG_CHECK_MODULES(PULSE, [ libpulse >= 0.9.2 ])
fi

AC_SUBST(PULSE_LIBS)
AC_SUBST(PULSE_CFLAGS)


# XMMS plugin #

AC_ARG_ENABLE([xmms],
    AS_HELP_STRING([--disable-xmms],[Disable optional XMMS pluggin support]),
        [
            case "${enableval}" in
                yes) xmms=true ;;
                no) xmms=false ;;
                *) AC_MSG_ERROR(bad value ${enableval} for --disable-xmms) ;;
            esac
        ],
        [xmms=true])

if test "x${xmms}" != xfalse ; then
    AC_PATH_PROG(XMMS_CONFIG, xmms-config)
    if test "x$XMMS_CONFIG" = "x" ; then
      AC_MSG_ERROR([*** Please install xmms-config of the xmms-dev package into your \$PATH ***])
    fi
    XMMS_CFLAGS=`$XMMS_CONFIG --cflags`
    XMMS_LIBS=`$XMMS_CONFIG --libs`
    XMMS_OUTPUTPLUGINDIR=`$XMMS_CONFIG --output-plugin-dir` 
    
else
    echo "*** XMMS disabled ***"
    XMMS_CFLAGS=
    XMMS_LIBS=
    XMMS_OUTPUTPLUGINDIR=
fi

AC_SUBST(XMMS_CFLAGS)
AC_SUBST(XMMS_LIBS)
AC_SUBST(XMMS_OUTPUTPLUGINDIR)

AM_CONDITIONAL(BUILD_XMMS, test "x$xmms" = xtrue)


# end of xmms #


# BMP plugin #

AC_ARG_ENABLE([bmp],
    AS_HELP_STRING([--enable-bmp],[Enable optional Beep-Media-Player pluggin support]),
        [
            case "${enableval}" in
                yes) bmp=true ;;
                no) bmp=false ;;
                *) AC_MSG_ERROR(bad value ${enableval} for --enable-bmp) ;;
            esac
        ],
        [bmp=false])

if test "x${bmp}" != xfalse ; then
    PKG_CHECK_MODULES(BMP, [ bmp >= 0.9.7 ])
	
    BMP_CFLAGS="$BMP_CFLAGS -I/usr/include/bmp"
    BMP_OUTPUTPLUGINDIR=`pkg-config bmp --variable=output_plugin_dir`

else
    echo "*** BMP disabled ***"
    BMP_CFLAGS=
    BMP_LIBS=
    BMP_OUTPUTPLUGINDIR=
fi

AC_SUBST(BMP_CFLAGS)
AC_SUBST(BMP_LIBS)
AC_SUBST(BMP_OUTPUTPLUGINDIR)

AM_CONDITIONAL(BUILD_BMP, test "x$bmp" = xtrue)

# end of bmp #


# If using GCC specifiy some additional parameters
if test "x$GCC" = "xyes" ; then
   CFLAGS="$CFLAGS -pipe -Wall -W -Wno-unused-parameter"
fi

# LYNX documentation generation
AC_ARG_ENABLE(lynx,
        AS_HELP_STRING(--disable-lynx,Turn off lynx usage for documentation generation),
[case "${enableval}" in
  yes) lynx=yes ;;
  no)  lynx=no ;;
  *) AC_MSG_ERROR(bad value ${enableval} for --disable-lynx) ;;
esac],[lynx=yes])

if test x$lynx = xyes ; then
   AC_CHECK_PROG(have_lynx, lynx, yes, no)

   if test x$have_lynx = xno ; then
     AC_MSG_ERROR([*** Sorry, you have to install lynx or use --disable-lynx ***])
   fi
fi

AM_CONDITIONAL([USE_LYNX], [test "x$lynx" = xyes])

AC_CONFIG_FILES([Makefile src/Makefile doc/Makefile doc/README.html])
AC_OUTPUT
