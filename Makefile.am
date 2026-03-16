## Process this file with automake to produce Makefile.in

COMPILE_DIRS = CUnit doc Man Share

if ENABLE_EXAMPLES
EXAMPLE_COMPILE_DIR = Examples
endif 

COMPILE_DIRS += $(EXAMPLE_COMPILE_DIR)

SUBDIRS = ${COMPILE_DIRS}

DIST_BASENAME=cunit-@VERSION@-@RELEASE@
distdir=${DIST_BASENAME}

WD=`pwd`
RPM_BUILD_ROOT=${WD}/BUILD
RPM_SOURCE_DIR=${WD}/SOURCES
#RPM_DEFINES=--define "_topdir ${WD}" --define "_prefix ${RPM_BUILD_ROOT}" --define "_unpackaged_files_terminate_build 0"
RPM_DEFINES=--define "_topdir ${WD}" --define "_unpackaged_files_terminate_build 0" --define "_prefix /usr/local"
RPMFLAGS=--buildroot ${RPM_BUILD_ROOT}
RPM=rpmbuild

PACKAGE_TMPSPEC=./SPECS/@PACKAGE@-@VERSION@-@RELEASE@.spec
SPECFILE=@PACKAGE@".spec"
CHANGELOG="ChangeLog"
SOURCE_GZIP_FILE=${DIST_BASENAME}.tar.gz

RPM_ATHLON=./RPMS/athlon/@PACKAGE@-@VERSION@-@RELEASE@.athlon.rpm
RPM_I386=./RPMS/i386/@PACKAGE@-@VERSION@-@RELEASE@.i386.rpm
RPM_I486=./RPMS/i486/@PACKAGE@-@VERSION@-@RELEASE@.i486.rpm
RPM_I586=./RPMS/i586/@PACKAGE@-@VERSION@-@RELEASE@.i586.rpm
RPM_I686=./RPMS/i686/@PACKAGE@-@VERSION@-@RELEASE@.i686.rpm
RPM_K6=./RPMS/athlon/@PACKAGE@-@VERSION@-@RELEASE@.k6.rpm
RPM_SRC=./SRPMS/@PACKAGE@-@VERSION@-@RELEASE@.src.rpm

EXTRA_DIST=cunit.pc.in
EXTRA_REMOVE=CUnit-Memory-Dump.lst ${SOURCE_GZIP_FILE} \
	*.rpm *.o *.ncb *.plg *.opt *.clw *.ilk *.exe *.pdb *.lib

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = cunit.pc

RPMDIRS=BUILD SOURCES RPMS RPMS/i386 SRPMS SPECS

clean-all: clean
	rm -f ${SOURCE_GZIP_FILE} *.rpm
	rm -rf ${RPMDIRS} `find . -name "Temp"` `find . -name "Debug"`
	for file in ${EXTRA_REMOVE}; do rm -f `find . -name "${file}"`; done	

distclean-all: distclean
	rm -f ${SOURCE_GZIP_FILE} *.rpm
	rm -rf ${RPMDIRS}

# Release archives are generated with `git archive` in CI and release tooling.
# The legacy RPM target is left here commented out for review.
#
# rpm: rpm-package
#
# rpm-package:
# 	# Expects ${SOURCE_GZIP_FILE} from a prior `git archive` step.
# 	rm -rf ${RPMDIRS} && \
# 	mkdir -p ${RPMDIRS} && \
# 	cp ${SPECFILE} ${PACKAGE_TMPSPEC} && \
# 	echo "%changelog" >> ${PACKAGE_TMPSPEC} && \
# 	cat ${CHANGELOG} >> ${PACKAGE_TMPSPEC} && \
# 	export RPM_BUILD_ROOT=${RPM_BUILD_ROOT} && \
# 	cp ${SOURCE_GZIP_FILE} ${RPM_SOURCE_DIR}
# 	${RPM} ${RPM_DEFINES} ${RPMFLAGS} -bb ${PACKAGE_TMPSPEC} && \
# 	( (cp -f ${RPM_ATHLON} .) || (cp -f ${RPM_I386} .) || (cp -f ${RPM_I486} .) \
# 	  || (cp -f ${RPM_I586} .) || (cp -f ${RPM_I686} .) \
# 	  || (cp -f ${RPM_K6} .) || (cp -f ${RPM_NOARCH} .) ) && \
# 	rm -rf ${RPMDIRS}
