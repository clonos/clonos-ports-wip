# $FreeBSD:$

PORTNAME=	cbsd-plugin-wsqueue
PORTVERSION=	0.2
CATEGORIES=	sysutils

MAINTAINER=	olevole@olevole.ru
COMMENT=	CBSD WEB UI

LICENSE=	BSD
RUN_DEPENDS=	cbsd:sysutils/cbsd
USES=		go

SUB_FILES=	pkg-message

PLIST_FILES=	cbsd/modules/cbsd_queue.d/cbsd-plugin-wsqueue

USE_GITHUB=	yes
GH_TAGNAME=	4a90f67
GH_ACCOUNT=	cbsd
GH_PROJECT=	cbsd-plugin-wsqueue

GH_TUPLE=	go-logfmt:logfmt:v0.6.0:go_logfmt/src/github.com/go-logfmt/logfmt \
		gorilla:websocket:v1.5.0:websocket/src/github.com/gorilla/websocket

post-extract:
	${LN} -sf ${WRKSRC}/src ${WRKDIR}
	${LN} -sf ${WRKSRC} ${WRKDIR}/src/${PORTNAME}

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/cbsd
	${MKDIR} ${STAGEDIR}${PREFIX}/cbsd/modules
	${MKDIR} ${STAGEDIR}${PREFIX}/cbsd/modules/cbsd_queue.d
	${INSTALL_PROGRAM} ${WRKDIR}/bin/${PORTNAME} ${STAGEDIR}${PREFIX}/cbsd/modules/cbsd_queue.d/cbsd-plugin-wsqueue

.include <bsd.port.mk>
