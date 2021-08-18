#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=speedtest-go
PROJECT_NAME:=speedtest-go
PKG_VERSION:=1.1.3
PKG_RELEASE:=1
PKG_SOURCE_URL:=https://github.com/librespeed/speedtest-go/releases/download/v$(PKG_VERSION)/
PKG_HASH:=83cc83200c4de881780b834dfdd7a6b310fa9d0bea7e983c3384d8feb539eae7

ifeq ($(ARCH),i386)
	TARGET_CPU:=386
else ifeq ($(ARCH),x86_64)
	TARGET_CPU:=amd64
else ifeq ($(ARCH),mipsel)
	TARGET_CPU:=mipsle
else ifeq ($(ARCH),mips)
	TARGET_CPU:=mips_softfloat
else ifeq ($(ARCH),arm)
	ifeq ($(findstring cortex-a7,$(ARCH_PACKAGES)),cortex-a7)
		TARGET_CPU:=armv7
	endif
else ifeq ($(ARCH),arm64)
	TARGET_CPU:=arm64
else ifeq ($(ARCH),aarch64)
	TARGET_CPU:=arm64
endif
PKG_SOURCE:=speedtest-go_$(PKG_VERSION)_linux_$(TARGET_CPU).tar.gz

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Speedtest Go
	URL:=https://github.com/librespeed/speedtest-go
endef

define Package/$(PKG_NAME)/description
Go backend for LibreSpeed.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	tar -zxvf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/speedtest-backend $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/speedtest-go.init $(1)/etc/init.d/speedtest-go

	$(INSTALL_DIR) $(1)/etc/speedtest-go/assets
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/settings.toml $(1)/etc/speedtest-go
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/assets/* $(1)/etc/speedtest-go/assets

endef

$(eval $(call BuildPackage,$(PKG_NAME)))
