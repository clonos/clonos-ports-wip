# $FreeBSD:$

PORTNAME=	clonos
PORTVERSION=	19.09
CATEGORIES=	www
GTAG=		740c3dd
DISTNAME=	control-pane-${GTAG}

MAINTAINER=	olevole@olevole.ru
COMMENT=	CBSD WEB UI

LICENSE=	BSD

LIB_DEPENDS=	libvncserver.so:net/libvncserver \
		libgnutls.so:security/gnutls \
		libsqlite3.so:databases/sqlite3

RUN_DEPENDS=	bash:shells/bash \
		npm:www/npm \
		nginx:www/nginx \
		git:devel/git \
		supervisord:sysutils/py-supervisor \
		cbsd:sysutils/cbsd \
		${LOCALBASE}/share/certs/ca-root-nss.crt:security/ca_root_nss \
		${LOCALBASE}/cbsd/modules/cbsd_queue.d/cbsd-plugin-wsqueue:sysutils/cbsd-plugin-wsqueue \
		${LOCALBASE}/cbsd/modules/forms.d/clonos_database/initforms.sh:sysutils/cbsd-plugin-clonos-database \
		${LOCALBASE}/cbsd/modules/vncterm.d/vncterm:sysutils/cbsd-plugin-vncterm \
		${LOCALBASE}/cbsd/modules/convectix.d/securecmd:sysutils/cbsd-plugin-convectix \
		${LOCALBASE}/cbsd/modules/puppet.d/puppet:sysutils/cbsd-plugin-puppet \
		${LOCALBASE}/cbsd/modules/forms.d/memcached/initforms.sh:sysutils/cbsd-plugin-forms-memcached \
		${LOCALBASE}/cbsd/modules/forms.d/redis/initforms.sh:sysutils/cbsd-plugin-forms-redis \
		${LOCALBASE}/cbsd/modules/forms.d/php/initforms.sh:sysutils/cbsd-plugin-forms-php \
		${LOCALBASE}/bin/clonos-ws:sysutils/clonos-ws \
		node:www/node \
		sudo:security/sudo \
		sqlite3:databases/sqlite3 \
		beanstalkd:net/beanstalkd

USES=		php python

USE_PHP=	session zip sqlite3 pdo_sqlite opcache json hash

WRKSRC=		${WRKDIR}/web
NO_BUILD=	yes

SUB_FILES=	pkg-message

USE_GITHUB=	yes
GH_ACCOUNT=	clonos
GH_PROJECT=	control-pane
GH_TAGNAME=	${GTAG}

do-install:
	@${MKDIR} ${STAGEDIR}${WWWDIR}
	@${MKDIR} ${STAGEDIR}/root/bin
	@${MKDIR} ${STAGEDIR}/var/db/clonos
	@${MKDIR} -p ${STAGEDIR}/usr/local/etc/nginx/streams-enabled
	@${MKDIR} -p ${STAGEDIR}/usr/local/etc/nginx/sites-enabled/
	${CP} -a ${WRKDIR}/control-pane-${GTAG}/logs ${STAGEDIR}${WWWDIR}
	${CP} -a ${WRKDIR}/control-pane-${GTAG}/node ${STAGEDIR}${WWWDIR}
	${CP} -a ${WRKDIR}/control-pane-${GTAG}/media_import ${STAGEDIR}${WWWDIR}
	${CP} -a ${WRKDIR}/control-pane-${GTAG}/php ${STAGEDIR}${WWWDIR}
	${CP} -a ${WRKDIR}/control-pane-${GTAG}/public ${STAGEDIR}${WWWDIR}
	${CHOWN} -R ${WWWOWN}:${WWWGRP} ${STAGEDIR}${WWWDIR}/public/novnc

post-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/supervisor.d /var/log/supervisor
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/sudoers.d
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/nginx/streams-enabled
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/nginx/conf.stream.d
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/nginx/sites-enabled
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/php-fpm.d
	${MKDIR} /var/log/nginx ${STAGEDIR}${PREFIX}/etc/nginx/streams-enabled ${STAGEDIR}${PREFIX}/etc/nginx/sites-enabled
	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/nginx.conf.sample \
		${STAGEDIR}${PREFIX}/etc/nginx/nginx.conf.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/10_www.sample \
		${STAGEDIR}${PREFIX}/etc/sudoers_10_www.clonos.sample

	${CHMOD} 0440 ${STAGEDIR}${PREFIX}/etc/sudoers_10_www.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/cbsdweb.conf.sample \
		${STAGEDIR}${PREFIX}/etc/nginx/sites-enabled/cbsdweb.conf.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/program_vnc2wss.conf.sample \
		${STAGEDIR}${PREFIX}/etc/supervisor.d/program_vnc2wss.conf.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/program_ws.conf.sample \
		${STAGEDIR}${PREFIX}/etc/supervisor.d/program_ws.conf.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/program_wsclonos.conf.sample \
		${STAGEDIR}${PREFIX}/etc/supervisor.d/program_wsclonos.conf.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/supervisord.conf.sample \
		${STAGEDIR}${PREFIX}/etc/supervisord.conf.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/php.ini.sample \
		${STAGEDIR}${PREFIX}/etc/php.ini.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/www-php-fpm.conf.sample \
		${STAGEDIR}${PREFIX}/etc/php-fpm.d/www-php-fpm.conf.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/php-fpm.conf.sample \
		${STAGEDIR}${PREFIX}/etc/php-fpm.conf.clonos.sample

	${INSTALL_DATA} ${WRKDIR}/control-pane-${GTAG}/examples/cbsd-modules.conf.sample \
		${STAGEDIR}${PREFIX}/etc/cbsd-modules.conf.clonos.sample

	@${ECHO_CMD} "@owner ${WWWOWN}" >> ${TMPPLIST}
	@${ECHO_CMD} "@group ${WWWGRP}" >> ${TMPPLIST}
	@${FIND} -s ${STAGEDIR}${WWWDIR} -not -type d | ${SORT} | \
		${SED} -e 's#^${STAGEDIR}${PREFIX}/##' >> ${TMPPLIST}
	@${ECHO} @dir ${WWWDIR} >> ${TMPPLIST}
	@${ECHO} @dir /var/db/clonos >> ${TMPPLIST}
	@${ECHO} @dir /usr/local/etc/nginx/streams-enabled >> ${TMPPLIST}
	@${ECHO} @dir /usr/local/etc/nginx/sites-enabled >> ${TMPPLIST}
	@${ECHO_CMD} "@group" >> ${TMPPLIST}
	@${ECHO_CMD} "@owner" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/nginx/nginx.conf.clonos.sample etc/nginx/nginx.conf" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/nginx/sites-enabled/cbsdweb.conf.clonos.sample etc/nginx/sites-enabled/cbsdweb.conf" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/sudoers_10_www.clonos.sample etc/sudoers.d/10_www" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/supervisor.d/program_vnc2wss.conf.clonos.sample etc/supervisor.d/program_vnc2wss.conf" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/supervisor.d/program_ws.conf.clonos.sample etc/supervisor.d/program_ws.conf" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/supervisor.d/program_wsclonos.conf.clonos.sample etc/supervisor.d/program_wsclonos.conf" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/supervisord.conf.clonos.sample etc/supervisord.conf" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/php.ini.clonos.sample etc/php.ini" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/php-fpm.conf.clonos.sample etc/php-fpm.conf" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/cbsd-modules.conf.clonos.sample" >> ${TMPPLIST}
	@${ECHO_CMD} "@sample etc/php-fpm.d/www-php-fpm.conf.clonos.sample etc/php-fpm.d/www.conf" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(${WWWOWN},${WWWGRP},) ${WWWDIR}/public/novnc" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(${WWWOWN},${WWWGRP},) ${WWWDIR}/public/novnc/utils" >> ${TMPPLIST}

.include <bsd.port.mk>
