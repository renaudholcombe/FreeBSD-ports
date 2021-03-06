# Created by: Ed Schouten <ed@FreeBSD.org>
# $FreeBSD$

PORTNAME=	arpc
DISTVERSIONPREFIX=	v
DISTVERSION=	0.6
PORTREVISION=	1
CATEGORIES=	devel

MAINTAINER=	ed@FreeBSD.org
COMMENT=	GRPC-like RPC library that supports file descriptor passing

LICENSE=	BSD2CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pyPEG2>=2.15.2:textproc/py-pyPEG2@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}toposort>=1.5:devel/py-toposort@${PY_FLAVOR}
LIB_DEPENDS=	libargdata.so:devel/argdata
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pyPEG2>=2.15.2:textproc/py-pyPEG2@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}toposort>=1.5:devel/py-toposort@${PY_FLAVOR}

BROKEN_armv6=		fails to build: *** Signal 11
BROKEN_armv7=		fails to build: *** Signal 11

USES=		cmake localbase:ldflags python:3.4+ shebangfix tar:xz
python_OLD_CMD=	"/usr/bin/env python3"
SHEBANG_FILES=	scripts/aprotoc.py
USE_LDCONFIG=	yes
USE_GITHUB=	yes
GH_ACCOUNT=	NuxiNL

PLIST_FILES=	bin/aprotoc include/arpc++/arpc++.h \
		lib/libarpc.so lib/libarpc.so.1

.include <bsd.port.pre.mk>

.if ${OPSYS} == FreeBSD && ${OSVERSION} < 1100511
IGNORE=		requires various C++17 features
.endif

# Require the unit tests to pass prior to installing.
post-build:
	@trap '' PIPE && ${WRKSRC}/arpc_tests

.include <bsd.port.post.mk>
