# $FreeBSD$

PORTNAME=	parity-ethereum
DISTVERSIONPREFIX=	v
DISTVERSION=	2.5.12
PORTREVISION=	1
CATEGORIES=	net-p2p

MAINTAINER=	ale@FreeBSD.org
COMMENT=	Fast and advanced Ethereum client

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/LICENSE

BROKEN_i386=		fails to build
BROKEN_FreeBSD_11=	fails to build

USES=		cargo

USE_GITHUB=	yes
GH_ACCOUNT=	paritytech

PLIST_FILES=	bin/parity

CARGO_FEATURES=	final
CARGO_TEST=	yes

.include "${.CURDIR}/Makefile.crates"

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/parity

.include <bsd.port.mk>
