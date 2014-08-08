AUTOMAKE_OPTIONS = subdir-objects
ACLOCAL_AMFLAGS = ${ACLOCAL_FLAGS}

lib_LTLIBRARIES = libsm3.la
libsm3_la_SOURCES = src/byteorder.h src/sm3.h src/sm3.c src/hmac_sm3.c

libsm3_includedir = $(includedir)/
libsm3_include_HEADERS = src/sm3.h src/hmac_sm3.h
libsm3_libincludedir = $(libdir)/


bin_PROGRAMS = sm3
sm3_SOURCES = src/sm3dgst.c
sm3_LDADD = libsm3.la

noinst_PROGRAMS = sm3test
sm3test_SOURCES = src/sm3test.c
sm3test_LDADD = libsm3.la

