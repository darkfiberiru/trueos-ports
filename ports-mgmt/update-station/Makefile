# New ports collection makefile for: update-station
# Date created:        Sunday, April 17 2016
# Whom:                ericturgeon@ghostbsd.com
#
# $FreeBSD$
#

PORTNAME=	update-station
PORTVERSION=	2.0
PORTREVISION=	1
CATEGORIES=	ports-mgmt
MASTER_SITES=	https://github.com/GhostBSD/${PORTNAME}/archive/

MAINTAINER=	ericturgeon@ghostbsd.com
COMMENT=	Tool to update FreeBSD/GhostBSD software and system.
LICENSE =	BSD

RUN_DEPENDS=	sudo:security/sudo \
		fbsdpkgupdate:ports-mgmt/fbsdpkgupdate \
		${LOCALBASE}/etc/pkg/repos/GhostBSD.conf:misc/ghostbsd-pkg-conf

USE_GITHUB=	yes
GH_ACCOUNT=	GhostBSD

USES =		python:3.6+
USE_PYTHON=	distutils
USE_GNOME=	pygobject3

.include <bsd.port.mk>
