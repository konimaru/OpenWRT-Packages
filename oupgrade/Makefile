#
# Copyright (C) 2015 Onion Corporation
#
# Author: Lazar Demin  <lazar@onion.io>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
PKG_NAME:=oupgrade
PKG_VERSION:=0.4
PKG_RELEASE:=3


PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=HEAD
PKG_SOURCE_URL:=https://github.com/OnionIoT/oupgrade.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=onion
	CATEGORY:=Onion
	SUBMENU:=Utilities
	TITLE:=Tool to upgrade device firmware with latest from Onion repo
	DEPENDS:=+wget
endef


define Package/$(PKG_NAME)/description
Tool to upgrade device firmware with latest from Onion repo
endef

#define Package/$(PKG_NAME)/Build/Compile
#	$(MAKE) -C $(PKG_BUILD_DIR)
#endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/oupgrade.sh $(1)/usr/bin/oupgrade
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/init.d/oupgrade $(1)/etc/init.d/oupgrade
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
