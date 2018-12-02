# $FreeBSD:$

PORTNAME=	cbsd-plugin-convectix
PORTVERSION=	0.1
CATEGORIES=	sysutils

MAINTAINER=	olevole@olevole.ru
COMMENT=	CBSD WEB UI

LICENSE=	BSD

RUN_DEPENDS=	cbsd:sysutils/cbsd

SUB_FILES=	pkg-message

USE_GITHUB=	yes
GH_TAGNAME=	84e6254
GH_ACCOUNT=	cbsd
GH_PROJECT=	cbsd-plugin-convectix

NO_BUILD=	yes
NO_ARCH=	yes
TARGET_DIR=	${PREFIX}/cbsd/modules/convectix.d

do-install:
	${MKDIR} ${STAGEDIR}${TARGET_DIR}
	cd ${WRKSRC} && ${RM} .gitignore .gitmodules .travis.yml
	cd ${WRKSRC} && ${CP} -a . ${STAGEDIR}${TARGET_DIR}/

post-install:
	@${FIND} -s ${STAGEDIR}${TARGET_DIR} -not -type d | ${SORT} | \
		${SED} -e 's#^${STAGEDIR}${PREFIX}/##' >> ${TMPPLIST}


.include <bsd.port.mk>
