# $FreeBSD$

PORTNAME=	userland-docs
PORTVERSION=	${BASEPKG_PORTVERSION}
CATEGORIES=	os
PKGNAMEPREFIX=	${OS_PKGNAMEPREFIX}
DISTFILES=
EXTRACT_ONLY=

MAINTAINER=	kmoore@FreeBSD.org
COMMENT=	FreeBSD userland documentation and man pages

BUILD_DEPENDS=  ${OS_WORLDDIST}:os/buildworld@${OS_FLAVOR}

USES=	os:flavors
PREFIX=/
NEED_ROOT=	yes

.include <bsd.port.pre.mk>

do-build:
	@${MKDIR} ${STAGEDIR}
	${ECHO_MSG} "==> ${OS_WORLDDIST}..."
	${TAR} xpf ${OS_WORLDDIST} -C ${STAGEDIR}

do-install:
	${ECHO_MSG} "==> Generating plist..."
	(cd ${STAGEDIR}; ${FIND} ./usr/share/doc ./usr/share/man \( -type f -o -type l \) \
		| ${SED} -e 's,^\./,,g' \
		| ${AWK} '{print length, $$0}' | ${SORT} -rn \
		| ${AWK} '{print $$2 }' \
		>> ${TMPPLIST})
	(cd ${STAGEDIR}; ${FIND} ./usr/share/doc ./usr/share/man \( -type d \) \
		| ${SED} -e 's,^\./,,g' \
		| ${AWK} '{print length, $$0}' | ${SORT} -rn \
		| ${AWK} '{print $$2 }' \
		| ${GREP} -v -x '/' \
		| ${XARGS} -I '{}' echo "@dir {}" \
		| ${GREP} -v -x '@dir ' \
		| ${CAT} >> ${TMPPLIST})
	${SH} ${PORTSDIR}/os/userland-base/files/scrubplist.sh \
		${PORTSDIR}/os/userland-base/files/configs \
		${TMPPLIST} ${STAGEDIR}

clean:
	if [ -d ${WRKDIR} ]; then \
		if [ -w ${WRKDIR} ]; then \
			${ECHO_MSG} "===> Cleaning for ${PKGNAME}"; \
			${CHFLAGS} -R noschg ${WRKDIR} ; \
			${RM} -r ${WRKDIR}; \
		else \
			${ECHO_MSG} "===>   ${WRKDIR} not writable, skipping"; \
		fi; \
	fi

.include "../Makefile.common"
.include <bsd.port.post.mk>
