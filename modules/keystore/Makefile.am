keystoredir = $(pluginsdir)/keystore

libmemory_keystore_plugin_la_SOURCES = keystore/memory.c \
	keystore/list_util.c keystore/list_util.h
keystore_LTLIBRARIES = libmemory_keystore_plugin.la

libfile_keystore_plugin_la_SOURCES = keystore/file.c \
	keystore/file_crypt.h \
	keystore/list_util.c keystore/list_util.h
if HAVE_ANDROID
libfile_keystore_plugin_la_SOURCES += keystore/file_crypt_android.c
endif
keystore_LTLIBRARIES += libfile_keystore_plugin.la

libsecret_plugin_la_SOURCES = keystore/secret.c
libsecret_plugin_la_CPPFLAGS = $(AM_CPPFLAGS) $(SECRET_CFLAGS)
libsecret_plugin_la_LDFLAGS = $(AM_LDFLAGS) -rpath '$(keystoredir)'
libsecret_plugin_la_LIBADD = $(SECRET_LIBS)

libkwallet_plugin_la_SOURCES = keystore/kwallet.c
libkwallet_plugin_la_CFLAGS = $(AM_CFLAGS) $(DBUS_CFLAGS)
libkwallet_plugin_la_LIBADD = $(DBUS_LIBS) $(LIBM)
if HAVE_DBUS
keystore_LTLIBRARIES += libkwallet_plugin.la
endif

libkeychain_plugin_la_SOURCES = keystore/keychain.m
libkeychain_plugin_la_OBJCFLAGS = $(AM_CFLAGS) -fobjc-arc
libkeychain_plugin_la_LDFLAGS = $(AM_LDFLAGS) -rpath '$(keystoredir)' -Wl,-framework,Foundation -Wl,-framework,Security

if HAVE_OSX
keystore_LTLIBRARIES += libkeychain_plugin.la
endif

keystore_LTLIBRARIES += \
	$(LTLIBsecret)

EXTRA_LTLIBRARIES += \
	libsecret_plugin.la
