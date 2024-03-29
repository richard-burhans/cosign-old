# Process this file with autoconf to produce a configure script.
AC_INIT([cosign],[3.2.0],[cosign@umich.edu]) 
AC_PREREQ([2.69])
AC_COPYRIGHT([Copyright (c) 2001-2002 Regents of The University of Michigan.  All Rights Reserved.])
AC_CONFIG_SRCDIR([version.c.in])
AC_CONFIG_HEADER([common/config.h])

# Checks for programs.
AC_PROG_AWK
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET

AC_CANONICAL_HOST 

# Checks for libraries.
AC_SEARCH_LIBS([inet_ntoa], [nsl])
AC_SEARCH_LIBS([socket], [socket])

AC_ARG_ENABLE(apache1, AS_HELP_STRING([--enable-apache1=path_to_apache1.3-apxs],[enable apache 1.3 filter ]), CHECK_APACHE_1, AC_MSG_RESULT( apache 1.3 not enabled))

AC_ARG_ENABLE(apache2, AS_HELP_STRING([--enable-apache2=path_to_apache2-apxs],[enable apache 2 filter]), CHECK_APACHE2, AC_MSG_RESULT( apache 2 not enabled))

AC_ARG_ENABLE(lighttpd, AS_HELP_STRING([--enable-lighttpd=path_to_lighttpd],[enable lighttpd filter]), CHECK_LIGHTTPD, AC_MSG_RESULT( lighttpd not enabled))

AC_ARG_ENABLE(krb, AS_HELP_STRING([--enable-krb=path_to_krb],[enable kerberos for the cgi and apache filter]), CHECK_LIBKRB, AC_MSG_RESULT( kerberos not enabled))

AC_ARG_VAR([KRB_CFLAGS], [kerberos CFLAGS])
AC_ARG_VAR([KRB_LDFLAGS], [kerberos LDFLAGS])
AC_ARG_VAR([KRB_LIBS], [kerberos LIBS])

AC_ARG_ENABLE(mysql, AS_HELP_STRING([--enable-mysql=path_to_mysql],[enable mysql for guest login support in the cgi]), CHECK_LIBMYSQL, AC_MSG_RESULT( mysql not enabled))

AC_ARG_WITH(gss, AS_HELP_STRING([--with-gss],[enable apache filter
to set up GSSAPI ]), CHECK_GSS, AC_MSG_RESULT( GSSAPI not enabled))

AC_ARG_VAR([GSSAPI_CFLAGS], [GSSAPI CFLAGS])
AC_ARG_VAR([GSSAPI_LDFLAGS], [GSSAPI LDFLAGS])
AC_ARG_VAR([GSSAPI_LIBS], [GSSAPI LIBS])

AC_ARG_WITH(cgiroot, AS_HELP_STRING([--with-cgiroot=DIR],[default cosign cgi root directory]), cgiroot="$withval", cgiroot="$prefix" )
 AC_SUBST(cgiroot)

AC_ARG_WITH(cosigndb, AS_HELP_STRING([--with-cosigndb=DIR],[default cosign database storage]), cosigndb="$withval", cosigndb="/var/cosign/daemon" )
AC_SUBST(cosigndb)

AC_ARG_WITH(cosignconf, AS_HELP_STRING([--with-cosignconf=FILE],[default cosign conf file location]), cosignconf="$withval", cosignconf="/usr/local/etc/cosign.conf" )
AC_SUBST(cosignconf)

AC_ARG_WITH(cosigncadir, AS_HELP_STRING([--with-cosigncadir=DIR],[default cosign CA dir location]), cosigncadir="$withval", cosigncadir="/var/cosign/certs/CA" )
AC_SUBST(cosigncadir)

AC_ARG_WITH(cosigncert, AS_HELP_STRING([--with-cosigncert=FILE],[default cosign
cert file location]), cosigncert="$withval", cosigncert="/var/cosign/certs/cert.pem" )
AC_SUBST(cosigncert)

AC_ARG_WITH(cosignkey, AS_HELP_STRING([--with-cosignkey=FILE],[default cosign
key file location]), cosignkey="$withval", cosignkey="/var/cosign/certs/key.pem" )
AC_SUBST(cosignkey)

AC_ARG_WITH(frienddbhost, AS_HELP_STRING([--with-frienddbhost=NAME],[name of host running friend's mysql db]), frienddbhost="$withval", frienddbhost="localhost" )
AC_SUBST(frienddbhost)

AC_ARG_WITH(frienddblogin, AS_HELP_STRING([--with-frienddblogin=NAME],[username of friend mysql db account]), frienddblogin="$withval", frienddblogin="friend" )
AC_SUBST(frienddblogin)

AC_ARG_WITH(frienddbpasswd, AS_HELP_STRING([--with-frienddbpasswd=PASSWD],[password of friend mysql db account]), frienddbpasswd="$withval", frienddbpasswd="" )
AC_SUBST(frienddbpasswd)

AC_ARG_WITH(ticketcache, AS_HELP_STRING([--with-ticketcache=DIR],[default cosign kerberos ticket cache]), ticketcache="$withval", ticketcache="/ticket" )
AC_SUBST(ticketcache)

AC_ARG_WITH(filterdb, AS_HELP_STRING([--with-filterdb=DIR],[default cosign filter database storage]), filterdb="$withval", filterdb="/var/cosign/filter" )
AC_SUBST(filterdb)

AC_ARG_WITH(proxydb, AS_HELP_STRING([--with-proxydb=DIR],[default cosign proxy authentication database storage]), proxydb="$withval", proxydb="/var/cosign/proxy" )
AC_SUBST(proxydb)

AC_ARG_WITH(cosignhost, AS_HELP_STRING([--with-cosignhost=NAME],[name of host that runs cosignd]), cosignhost="$withval", cosignhost="cosign.example.edu" )
AC_SUBST(cosignhost)

AC_ARG_WITH(cosignlogouturl, AS_HELP_STRING([--with-cosignlogouturl=URL],[default URL to redirect users to upon logout]), cosignlogouturl="$withval", cosignlogouturl="http://cosign.example.edu" )
AC_SUBST(cosignlogouturl)

AC_ARG_WITH(cosignlogoutregex, AS_HELP_STRING([--with-cosignlogoutregex=URL],[regular expression matching valid redirect URLs passed to the logout cgi]), cosignlogoutregex="$withval", cosignlogoutregex="http://.+\.example\.edu" )
AC_SUBST(cosignlogoutregex)

AC_ARG_WITH(cosignloopurl, AS_HELP_STRING([--with-cosignloopurl=URL],[default URL to redirect users to upon detecting an infinite loop]), cosignloopurl="$withval", cosignloopurl="http://cosign.example.edu/looping.html" )
AC_SUBST(cosignloopurl)

AC_ARG_WITH(keytabpath, AS_HELP_STRING([--with-keytabpath=FILE],[path
to keytab]), keytabpath="$withval", keytabpath="" )
AC_SUBST(keytabpath)

CHECK_SSL

AC_CHECK_HEADER([openssl/ssl.h], [], [AC_MSG_ERROR([header file <openssl/ssl.h> is required for this software. 
You may be running RedHat 9.
If so, see the FAQ or the README for further instructions.])])
# Checks for filters:

if test "x_$FILTERS" = "x_" ; then
  AC_MSG_ERROR([No web server found - you must explicitly "enable-apache1"
  or "enable-apache2" or both ])
fi
AC_SUBST(FILTERS)

for i in $FILTERS; do
  FILTER_CONFIG_FILES="$FILTER_CONFIG_FILES $i/Makefile"
done

# Checks for header files.
AC_CHECK_HEADERS([arpa/inet.h fcntl.h netdb.h netinet/in.h sys/file.h syslog.h sys/param.h sys/socket.h sys/time.h utime.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_PID_T
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T

# Checks for library functions.
AC_FUNC_FORK
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_CHECK_FUNCS([dup2 gethostbyname gethostname gettimeofday inet_ntoa memmove memset regcomp select socket strcasecmp strchr strdup strerror strncasecmp strrchr strstr strtol utime])

# Misc.
if test x_$GCC = x_yes; then
    OPTOPTS=${OPTOPTS:-"-Wall -Wextra -Wmissing-prototypes"}
fi
CHECK_UNIVERSAL_BINARIES
AC_SUBST(FILTER_LINKER_OPTS)
AC_SUBST(FILTER_COMPILER_OPTS)
AC_SUBST(UNIVERSAL_OPTOPTS)
AC_SUBST(OPTOPTS)
SET_NO_SASL
AC_CONFIG_SUBDIRS(libsnet)
AC_CONFIG_SUBDIRS(libcgi)

AC_CONFIG_FILES([Makefile
                 version.c
                 cgi/Makefile
                 common/Makefile
                 html/Makefile
                 daemon/Makefile
                 filters/common/cosignpaths.h
                 $FILTER_CONFIG_FILES])

AC_OUTPUT
