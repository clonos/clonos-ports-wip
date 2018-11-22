# $FreeBSD:$

PORTNAME=	clonos-ws
PORTVERSION=	0.1
CATEGORIES=	sysutils

MAINTAINER=	olevole@olevole.ru
COMMENT=	CBSD WEB UI

LICENSE=	BSD
RUN_DEPENDS=	cbsd:sysutils/cbsd
USES=		go

SUB_FILES=	pkg-message

PLIST_FILES=	bin/clonos-ws

USE_GITHUB=	yes
GH_TAGNAME=	9df756c
GH_ACCOUNT=	clonos
GH_PROJECT=	clonos-ws

GH_TUPLE=	go-logfmt:logfmt:v0.3.0:go_logfmt/src/github.com/go-logfmt/logfmt \
		gorilla:websocket:v1.4.0:websocket/src/github.com/gorilla/websocket

post-extract:
	${LN} -sf ${WRKSRC}/src ${WRKDIR}
	${LN} -sf ${WRKSRC} ${WRKDIR}/src/${PORTNAME}

do-install:
	${INSTALL_PROGRAM} ${WRKDIR}/bin/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/clonos-ws


.include <bsd.port.mk>
