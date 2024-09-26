#
# Copyright (C) 2014-2021 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=srt-live-server
PKG_VERSION:=1.4.8
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/Edward-Wu/srt-live-server/tar.gz/V1.4.8?
PKG_HASH:=3526a65e1d581b9ec62627d733d62a90dc074ae830e9bd7abe3f3b0a152b2786
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_MAINTAINER:=bbaa <bbaa@bbaa.fun>
PKG_LICENSE:=MIT

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += -Wno-error=format-security
TARGET_CXXFLAGS += -Wno-error=format-security

define Package/srt-live-server
  SECTION:=net
  CATEGORY:=Network
  TITLE:=srt-live-server
	DEPENDS:=+libpthread +libsrt +zlib
endef

define Package/srt-live-server/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/slc $(1)/usr/bin/slc
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/sls $(1)/usr/bin/sls
endef

$(eval $(call BuildPackage,srt-live-server))
