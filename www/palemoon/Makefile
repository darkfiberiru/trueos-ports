# Created by: Zhihao Yuan <lichray@gmail.com>
# $FreeBSD$

PORTNAME=	palemoon
DISTVERSION=	27.9.4
DISTVERSIONSUFFIX=_Release
PORTREVISION=	6
CATEGORIES=	www ipv6

MAINTAINER=	lichray@gmail.com
COMMENT=	Open Source Goanna-based web browser

BROKEN_FreeBSD_13_amd64=	xpcshell crashes after base Clang updated to 8.0.0

BUILD_DEPENDS=	nspr>=4.15:devel/nspr \
		nss>=3.31.1:security/nss \
		libevent>=2.0.22:devel/libevent \
		harfbuzz>=1.4.3:print/harfbuzz \
		graphite2>=1.3.10:graphics/graphite2 \
		png>=1.6.16:graphics/png \
		libvpx>=1.5.0:multimedia/libvpx \
		sqlite3>=3.19.3:databases/sqlite3 \
		${PYTHON_PKGNAMEPREFIX}sqlite3>0:databases/py-sqlite3@${PY_FLAVOR} \
		autoconf-2.13:devel/autoconf213 \
		yasm:devel/yasm \
		zip:archivers/zip

USE_GITHUB=	yes
GH_ACCOUNT=	MoonchildProductions
GH_PROJECT=	Pale-Moon

USE_GECKO=	gecko
MOZ_PKGCONFIG_FILES=	# empty
USE_MOZILLA=	-webp

PM_ICON=	${PORTNAME}.png
PM_ICON_SRC=	${PREFIX}/lib/${PORTNAME}/browser/icons/mozicon128.png
PM_DESKTOP=	${WRKSRC}/browser/branding/official/${PORTNAME}.desktop
MOZ_OPTIONS=	--enable-application=browser \
		--enable-devtools \
		--enable-jemalloc \
		--enable-jemalloc-lib

OPTIONS_DEFAULT=	GTK2
OPTIONS_EXCLUDE=	JACK TEST WAYLAND

.include "${.CURDIR}/../../www/firefox/Makefile.options"

# Inconsistent fallback order (libcubeb vs. audio_device)
SNDIO_PREVENTS=		${OPTIONS_MULTI_AUDIO:NSNDIO}

post-patch:
	@${REINPLACE_CMD} -e 's|%%LOCALBASE%%|${LOCALBASE}|g' \
		${WRKSRC}/browser/app/nsBrowserApp.cpp

pre-configure:
	(cd ${WRKSRC} && ${LOCALBASE}/bin/autoconf-2.13)
	(cd ${WRKSRC}/js/src/ && ${LOCALBASE}/bin/autoconf-2.13)

post-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/share/pixmaps
	${INSTALL_DATA} ${PM_DESKTOP} ${STAGEDIR}${PREFIX}/share/applications/
	${LN} -sf ${PM_ICON_SRC} ${STAGEDIR}${PREFIX}/share/pixmaps/${PM_ICON}

.include <bsd.port.mk>
