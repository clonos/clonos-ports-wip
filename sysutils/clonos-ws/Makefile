PORTNAME=	clonos-ws
DISTVERSION=	0.1
CATEGORIES=	sysutils

MAINTAINER=	fbsd-ports@convectix.com
COMMENT=	ClonOS WebSocket Server
WWW=		https://github.com/clonos/clonos-ws

LICENSE=	BSD2CLAUSE

USES=		go

USE_GITHUB=	yes
GH_ACCOUNT=	clonos
GH_PROJECT=	clonos-ws
GH_TAGNAME=	045a274

GH_TUPLE=	gorilla:websocket:v1.5.3:gorilla_websocket/vendor/github.com/gorilla/websocket

PLIST_FILES=	bin/clonos-ws \
	"@sample etc/clonos-channel.json.sample"

do-install:
	${INSTALL_PROGRAM} ${WRKDIR}/bin/clonos-ws ${STAGEDIR}${PREFIX}/bin/clonos-ws
	${INSTALL_DATA} ${WRKSRC}/clonos-channel.json \
	${STAGEDIR}${PREFIX}/etc/clonos-channel.json.sample

.include <bsd.port.mk>
