
# Copyright (C) 2016 Onion Corporation
# 
# Author: Scott Gilliland <zeroping@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
PKG_NAME:=omega2-pwm
PKG_VERSION:=0.3
PKG_RELEASE:=2


PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=HEAD
PKG_SOURCE_URL:=https://github.com/zeroping/omega2-pwm.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

TARGET_CXXFLAGS += -FPIC


define Package/$(PKG_NAME)
	SECTION:=onion
	CATEGORY:=Onion
	SUBMENU:=Utilities
	TITLE:=Utility to control the Omega2 PWM hardware
endef

define Package/$(PKG_NAME)/description
	Utility to control the Omega2's PWM hardware
endef


define Build/Prepare
	$(Build/Prepare/Default)
	mkdir -p $(PKG_BUILD_DIR)
	#tar xvf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)
	#mkdir -p $(PKG_BUILD_DIR)/BUILD

	#$(CP) ./* $(PKG_BUILD_DIR)/
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/omega2-pwm $(1)/usr/bin/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
