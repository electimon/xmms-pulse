# $Id: Makefile.am 55 2006-09-03 22:52:01Z lennart $
#
# This file is part of xmms-pulse.
#
# xmms-pulse is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# xmms-pulse is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
# General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with xmms-pulse; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307
# USA.

AM_CFLAGS=$(PTHREAD_CFLAGS)
AM_LIBADD=$(PTHREAD_LIBS)



if BUILD_XMMS
xmmsplugindir=$(XMMS_OUTPUTPLUGINDIR)
xmmsplugin_LTLIBRARIES=libxmms-pulse.la
libxmms_pulse_la_SOURCES=plugin.c
libxmms_pulse_la_LDFLAGS=-module -avoid-version
libxmms_pulse_la_LIBADD=$(AM_LIBADD) $(PULSE_LIBS) $(XMMS_LIBS)
libxmms_pulse_la_CFLAGS=$(AM_CFLAGS) $(PULSE_CFLAGS) $(XMMS_CFLAGS)
XMMS_CFLAGS+= -DHAVE_XMMS=1
endif


if BUILD_BMP
bmpplugindir=$(BMP_OUTPUTPLUGINDIR)
bmpplugin_LTLIBRARIES=libbmp-pulse.la
libbmp_pulse_la_SOURCES=plugin.c
libbmp_pulse_la_LDFLAGS=-module -avoid-version
libbmp_pulse_la_LIBADD=$(AM_LIBADD) $(PULSE_LIBS) $(BMP_LIBS)
libbmp_pulse_la_CFLAGS=$(AM_CFLAGS) $(PULSE_CFLAGS) $(BMP_CFLAGS)
BMP_CFLAGS+= -DHAVE_BMP=1
endif

