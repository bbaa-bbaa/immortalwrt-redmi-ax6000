#
# Copyright (C) 2014-2021 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libsrt
PKG_VERSION:=1.5.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/Haivision/srt/tar.gz/v1.5.3?
PKG_HASH:=befaeb16f628c46387b898df02bc6fba84868e86a6f6d8294755375b9932d777
PKG_BUILD_DIR:=$(BUILD_DIR)/srt-$(PKG_VERSION)
PKG_MAINTAINER:=bbaa <bbaa@bbaa.fun>
PKG_LICENSE:=MPL-2.0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libsrt
  SECTION:=net
  CATEGORY:=Network
  TITLE:=libsrt
	DEPENDS:=+libpthread +libstdcpp +libopenssl
endef

define Build/InstallDev
	$(INSTALL_DIR) $(2)/bin $(1)/usr/bin $(1)/usr/include $(1)/usr/lib $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/include/srt $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libsrt.{a,so*} $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/haisrt.pc $(1)/usr/lib/pkgconfig/
	$(CP) $(PKG_BUILD_DIR)/srt.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libsrt/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libsrt.so* $(1)/usr/lib/
endef


$(eval $(call BuildPackage,libsrt))
