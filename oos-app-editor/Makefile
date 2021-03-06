#
# Copyright (C) 2018 Onion Corporation
# 
# Author: Lazar Demin  <lazar@onion.io>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
PKG_NAME:=oos-app-code-editor
PKG_VERSION:=1.0.4
PKG_RELEASE:=1


PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=b2ef139219d2f931465f11306e651d3832262227
PKG_SOURCE_URL:=https://github.com/Codiad/Codiad.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/oos-app-code-editor
	SECTION:=onion
	CATEGORY:=Onion
	SUBMENU:=OS
	TITLE:=Code Editor : File browser and code editor
	DEPENDS:=+php7 +php7-mod-session +php7-fastcgi +php7-mod-json +php7-mod-curl +php7-mod-xml +php7-mod-simplexml +php7-mod-mbstring +php7-mod-openssl +php7-mod-zip
endef


define Package/oos-app-code-editor/description
Code Editor : File browser and code editor
endef

define Build/Compile
        $(CP) ./files/Makefile $(PKG_BUILD_DIR)/makefile
endef

define Package/oos-app-code-editor/install
	# copy the web site files
	$(INSTALL_DIR) $(1)/www/apps/oos-app-code-editor
	$(CP) -r $(PKG_BUILD_DIR)/components/ $(1)/www/apps/oos-app-code-editor/components/
	$(CP) -r $(PKG_BUILD_DIR)/data/ $(1)/www/apps/oos-app-code-editor/data/
	$(CP) -r $(PKG_BUILD_DIR)/js/ $(1)/www/apps/oos-app-code-editor/js/
	$(CP) -r $(PKG_BUILD_DIR)/languages/ $(1)/www/apps/oos-app-code-editor/languages/
	$(CP) -r $(PKG_BUILD_DIR)/lib/ $(1)/www/apps/oos-app-code-editor/lib/
	$(CP) -r $(PKG_BUILD_DIR)/plugins/ $(1)/www/apps/oos-app-code-editor/plugins/
	$(CP) -r $(PKG_BUILD_DIR)/themes/ $(1)/www/apps/oos-app-code-editor/themes/
	$(CP) -r $(PKG_BUILD_DIR)/workspace/ $(1)/www/apps/oos-app-code-editor/workspace/
	$(CP) $(PKG_BUILD_DIR)/*.php $(1)/www/apps/oos-app-code-editor/
	$(CP) $(PKG_BUILD_DIR)/*.json $(1)/www/apps/oos-app-code-editor/
	$(CP) $(PKG_BUILD_DIR)/*.xml $(1)/www/apps/oos-app-code-editor/
	$(CP) -r ./files/www/* $(1)/www/apps/oos-app-code-editor/
endef

define Package/oos-app-code-editor/postinst
#!/bin/sh
# check if we are on real system
if [ -z "$${IPKG_INSTROOT}" ]; then
	uci add_list uhttpd.main.interpreter='.php=/usr/bin/php-fcgi'
	uci set uhttpd.main.index_page='index.php'
	uci commit uhttpd
	/etc/init.d/uhttpd restart
fi
exit 0
endef

# calls to build each package
$(eval $(call BuildPackage,oos-app-code-editor))
