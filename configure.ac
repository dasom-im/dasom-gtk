dnl Process this file with autoconf to produce a configure script.

AC_INIT(dasom-gtk, 1.2, https://github.com/dasom-im/dasom-gtk/issues)

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])

AM_INIT_AUTOMAKE([-Wall -Werror])
AM_MAINTAINER_MODE([disable])
AM_SILENT_RULES([yes])

AM_PROG_AR
AC_PROG_CC

dnl ***************************************************************************
dnl Internationalization
dnl ***************************************************************************

IT_PROG_INTLTOOL(0.35.0)
GETTEXT_PACKAGE=dasom-gtk
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE, "$GETTEXT_PACKAGE", [gettext package name])
AC_SUBST(GETTEXT_PACKAGE)
AM_GLIB_GNU_GETTEXT
AM_GLIB_DEFINE_LOCALEDIR(DASOM_LOCALE_DIR)

LT_INIT([disable-static])

PKG_CHECK_MODULES(DASOM, [dasom])
PKG_CHECK_MODULES(GTK3, [gtk+-3.0])
PKG_CHECK_MODULES(GTK2, [gtk+-2.0])

case `uname -m` in
  x86_64)
    BITS=64
    ;;
  *)
    BITS=32
    ;;
esac

GTK3_LIBDIR=`pkg-config --variable=libdir gtk+-3.0`
GTK3_BINARY_VERSION=`pkg-config --variable=gtk_binary_version gtk+-3.0`
AC_SUBST(GTK3_LIBDIR)
AC_SUBST(GTK3_BINARY_VERSION)
AC_PATH_PROGS([GTK_QUERY_IMMODULES3],
              [gtk-query-immodules-3.0 gtk-query-immodules-3.0-$BITS], [no],
              [/usr/bin:$GTK3_LIBDIR/libgtk-3-0])
if test "x$GTK_QUERY_IMMODULES3" = "xno"; then
  AC_MSG_ERROR([gtk-query-immodules-3.0 or gtk-query-immodules-3.0-$BITS not found])
fi

GTK2_LIBDIR=`pkg-config --variable=libdir gtk+-2.0`
GTK2_BINARY_VERSION=`pkg-config --variable=gtk_binary_version gtk+-2.0`
AC_SUBST(GTK2_LIBDIR)
AC_SUBST(GTK2_BINARY_VERSION)
AC_PATH_PROGS([GTK_QUERY_IMMODULES2],
              [gtk-query-immodules-2.0 gtk-query-immodules-2.0-$BITS], [no],
              [/usr/bin:$GTK2_LIBDIR/libgtk2.0-0])
if test "x$GTK_QUERY_IMMODULES2" = "xno"; then
  AC_MSG_ERROR([gtk-query-immodules-2.0 or gtk-query-immodules-2.0-$BITS not found])
fi

AC_PATH_PROGS([GTK_UPDATE_ICON_CACHE],
              [gtk-update-icon-cache-3.0 gtk-update-icon-cache], [no],
              [/usr/bin:$GTK3_LIBDIR/libgtk-3-0:$GTK2_LIBDIR/libgtk2.0-0])
if test "x$GTK_UPDATE_ICON_CACHE" = "xno"; then
  AC_MSG_ERROR([gtk-update-icon-cache-3.0 or gtk-update-icon-cache not found])
fi

GLIB_GSETTINGS

AC_OUTPUT([
  Makefile
  src/Makefile
  po/Makefile.in
])
