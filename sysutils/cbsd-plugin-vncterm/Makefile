# $FreeBSD:$

PORTNAME=	cbsd-plugin-vncterm
PORTVERSION=	0.2
CATEGORIES=	sysutils

MAINTAINER=	olevole@olevole.ru
COMMENT=	CBSD WEB UI

LICENSE=	BSD

LIB_DEPENDS=	libvncserver.so:net/libvncserver \
		libgnutls.so:security/gnutls
RUN_DEPENDS=	cbsd:sysutils/cbsd

USES=		jpeg

GNUTLS_IMPLIES=		GCRYPT
GNUTLS_LIB_DEPENDS=	libgnutls.so:security/gnutls
GNUTLS_CONFIGURE_WITH=	gnutls

SUB_FILES=	pkg-message

PLIST_FILES=	cbsd/modules/vncterm.d/cbsdvnc \
		cbsd/modules/vncterm.d/jvncall \
		cbsd/modules/vncterm.d/securecmd \
		cbsd/modules/vncterm.d/vncterm \
		cbsd/modules/vncterm.d/vncterm-daemon

USE_GITHUB=	yes
GH_ACCOUNT=	cbsd
GH_PROJECT=	cbsd-plugin-vncterm

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/cbsd
	${MKDIR} ${STAGEDIR}${PREFIX}/cbsd/modules
	${MKDIR} ${STAGEDIR}${PREFIX}/cbsd/modules/vncterm.d
	${INSTALL_PROGRAM} ${WRKSRC}/cbsdvnc ${STAGEDIR}${PREFIX}/cbsd/modules/vncterm.d/cbsdvnc
	${CP} ${WRKSRC}/jvncall ${STAGEDIR}${PREFIX}/cbsd/modules/vncterm.d/jvncall
	${CP} ${WRKSRC}/securecmd ${STAGEDIR}${PREFIX}/cbsd/modules/vncterm.d/securecmd
	${CP} ${WRKSRC}/vncterm ${STAGEDIR}${PREFIX}/cbsd/modules/vncterm.d/vncterm
	${CP} ${WRKSRC}/vncterm-daemon ${STAGEDIR}${PREFIX}/cbsd/modules/vncterm.d/vncterm-daemon

.include <bsd.port.mk>
