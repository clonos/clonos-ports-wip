# $FreeBSD:$

PORTNAME=	cbsd-plugin-clonos-database
PORTVERSION=	0.1
CATEGORIES=	sysutils

MAINTAINER=	olevole@olevole.ru
COMMENT=	CBSD WEB UI

LICENSE=	BSD

RUN_DEPENDS=	cbsd:sysutils/cbsd

SUB_FILES=	pkg-message

PLIST_FILES=	cbsd/modules/forms.d/clonos_database/auth_list.schema \
		cbsd/modules/forms.d/clonos_database/auth_user.schema \
		cbsd/modules/forms.d/clonos_database/initforms.sh \
		cbsd/modules/forms.d/clonos_database/sys_helpers_list.schema

USE_GITHUB=	yes
GH_TAGNAME=	c5be89c
GH_ACCOUNT=	cbsd
GH_PROJECT=	cbsd-plugin-clonos-database

NO_BUILD=	yes
NO_ARCH=	yes
TARGET_DIR=	${PREFIX}/cbsd/modules/forms.d/clonos_database

do-install:
	${MKDIR} ${STAGEDIR}${TARGET_DIR}
	cd ${WRKSRC} && ${RM} .gitignore .gitmodules .travis.yml
	cd ${WRKSRC} && ${COPYTREE_SHARE} . ${STAGEDIR}${TARGET_DIR}


.include <bsd.port.mk>
