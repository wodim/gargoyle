#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=ca-certificates
PKG_VERSION:=20150426

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://ftp.debian.org/debian/pool/main/c/ca-certificates
PKG_MD5SUM:=717455f13fb31fd014a11a468ea3895d

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/ca-certificates-combined
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=System CA certificates in one combined file at /etc/ssl/certs/ca-certificates.crt
endef

define Build/Install
	mkdir -p \
		$(PKG_INSTALL_DIR)/usr/sbin \
		$(PKG_INSTALL_DIR)/usr/share/ca-certificates
	$(call Build/Install/Default,)
	cat $(PKG_INSTALL_DIR)/usr/share/ca-certificates/*/*.crt >$(PKG_INSTALL_DIR)/usr/share/ca-certificates.tmp
	mv $(PKG_INSTALL_DIR)/usr/share/ca-certificates.tmp $(PKG_INSTALL_DIR)/usr/share/ca-certificates.crt
endef

define Package/ca-certificates-combined/install
	$(INSTALL_DIR) $(1)/etc/ssl/certs
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/ca-certificates.crt $(1)/etc/ssl/certs/ca-certificates.crt
endef

$(eval $(call BuildPackage,ca-certificates-combined))
