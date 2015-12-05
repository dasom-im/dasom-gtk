gsettings_SCHEMAS = org.freedesktop.Dasom.clients.gtk.gschema.xml
@GSETTINGS_RULES@

AM_CFLAGS = -Wall -Werror -DG_LOG_DOMAIN=\"dasom\" $(DASOM_CFLAGS)

# for gtk3

gtk3_im_moduledir = $(GTK3_LIBDIR)/gtk-3.0/$(GTK3_BINARY_VERSION)/immodules
gtk3_im_module_LTLIBRARIES = im-dasom-gtk3.la

im_dasom_gtk3_la_SOURCES = im-dasom.c
im_dasom_gtk3_la_CFLAGS  = $(AM_CFLAGS) $(GTK3_CFLAGS)
im_dasom_gtk3_la_LDFLAGS = -avoid-version -module $(GTK3_LIBS) $(DASOM_LIBS)

# for gtk2

gtk2_im_moduledir = $(GTK2_LIBDIR)/gtk-2.0/$(GTK2_BINARY_VERSION)/immodules
gtk2_im_module_LTLIBRARIES = im-dasom-gtk2.la

im_dasom_gtk2_la_SOURCES = im-dasom.c
im_dasom_gtk2_la_CFLAGS  = $(AM_CFLAGS) $(GTK2_CFLAGS)
im_dasom_gtk2_la_LDFLAGS = -avoid-version -module $(GTK2_LIBS) $(DASOM_LIBS)

DISTCLEANFILES = Makefile.in

install-data-hook:
	chmod -x $(DESTDIR)$(gtk3_im_moduledir)/im-dasom-gtk3.so
	chmod -x $(DESTDIR)$(gtk2_im_moduledir)/im-dasom-gtk2.so
	rm -f $(DESTDIR)$(gtk3_im_moduledir)/im-dasom-gtk3.la
	rm -f $(DESTDIR)$(gtk2_im_moduledir)/im-dasom-gtk2.la

uninstall-hook:
	rm -f $(DESTDIR)$(gtk3_im_moduledir)/im-dasom-gtk3.so
	rm -f $(DESTDIR)$(gtk2_im_moduledir)/im-dasom-gtk2.so
	$(GTK_QUERY_IMMODULES2) --update-cache
	$(GTK_QUERY_IMMODULES3) --update-cache