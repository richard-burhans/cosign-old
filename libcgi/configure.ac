AC_INIT([libcgi],[VERSION],[mprint@umich.edu])
AC_PREREQ([2.69])
AC_ARG_ENABLE(debug, AS_HELP_STRING([--enable-debug],[enables debug logging to standard out]), debug="-DEBUG", debug="" )
AC_SUBST(debug)

# Checks for programs.
AC_PROG_CC

AC_CANONICAL_HOST

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([fcntl.h limits.h stdlib.h string.h unistd.h])

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_MEMCMP
AC_FUNC_REALLOC
AC_CHECK_FUNCS([memchr memmove memset strcasecmp strchr strdup strerror strncasecmp strstr strtol])

CHECK_UNIVERSAL_BINARIES

# Miscellaneous:
if test x_$GCC = x_yes; then
    OPTOPTS=${OPTOPTS:-"-Wall -Wextra -Wmissing-prototypes"}
fi
AC_SUBST(OPTOPTS)

AC_CONFIG_FILES(Makefile)
AC_OUTPUT
