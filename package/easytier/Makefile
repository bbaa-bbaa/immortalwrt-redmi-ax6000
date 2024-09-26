# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2023 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=easytier
PKG_VERSION:=1.2.3
PKG_RELEASE:=2

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=https://codeload.github.com/EasyTier/EasyTier/tar.gz/v$(PKG_VERSION)?
#PKG_HASH:=5f78fa2f6b8f9d615eb79a88ccc2f3eb39ff68e5487746410dae36f9573dd342
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/EasyTier/EasyTier.git
PKG_SOURCE_VERSION:=7b4a01e7fbdd45480b2f162bb6322fc312594557
PKG_SOURCE_SUBDIR:=EasyTier-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/EasyTier-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=rust/host
PKG_BUILD_PARALLEL:=1


include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/../feeds/packages/lang/rust/rust-package.mk

define Build/Prepare
$(call Build/Prepare/Default)
	cd $(PKG_BUILD_DIR)
	git init
	git remote add origin $(PKG_SOURCE_URL) || true
	git fetch -v
	git reset origin/main
endef

define Build/Compile
	$(call Build/Compile/Cargo,easytier)
endef

define Package/easytier/install
	$(INSTALL_DIR) $(1)/etc/easytier
	$(INSTALL_CONF) $(CURDIR)/files/config.toml $(1)/etc/easytier/config.toml

	$(INSTALL_DIR) $(1)/etc/config/
	$(INSTALL_CONF) $(CURDIR)/files/easytier.conf $(1)/etc/config/easytier
	
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(CURDIR)/files/easytier.init $(1)/etc/init.d/easytier

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/easytier-cli $(1)/usr/bin/easytier-cli
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/easytier-core $(1)/usr/bin/easytier-core

endef

define Package/easytier
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Mesh VPN
  TITLE:=Mesh VPN
  URL:=https://github.com/EasyTier/EasyTier
  DEPENDS:=+ca-bundle +kmod-tun
endef

$(eval $(call RustBinPackage,easytier))
$(eval $(call BuildPackage,easytier))
