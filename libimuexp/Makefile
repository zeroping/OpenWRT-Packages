# Copyright (C) 2017 Onion Corporation
# 
# Author: Gabriel Ongpauco <gabriel@onion.io>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
PKG_NAME:=libimuexp
PKG_VERSION:=0.1
PKG_RELEASE:=1


PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=HEAD
PKG_SOURCE_URL:=https://github.com/OnionIoT/imu-exp.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

# Package definition
define Package/$(PKG_NAME)
	SECTION:=onion
	CATEGORY:=Onion
	SUBMENU:=Libraries
	TITLE:=C library for the Onion IMU Expansion
	DEPENDS:=+liboniondebug +libonioni2c
endef

define Package/$(PKG_NAME)/description
C library for the Onion IMU Expansion
endef

# Enable position independent code for shared libraries
TARGET_CFLAGS += $(FPIC)

# Compiling
define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	LIB="$(TARGET_LIBS)" \
endef

# InstallDev section required for libraries
define Build/InstallDev
	mkdir -p $(1)/usr/include $(1)/usr/lib
	$(CP)   $(PKG_BUILD_DIR)/include/imu-exp.h $(1)/usr/include/
	$(CP)	$(PKG_BUILD_DIR)/lib/libonionimuexp.so $(1)/usr/lib/
	# $(CP)   $(PKG_BUILD_DIR)/include/onion-i2c.h $(1)/usr/include/
	# $(CP)	$(PKG_BUILD_DIR)/lib/libonioni2c.so $(1)/usr/lib/
	# $(CP)   $(PKG_BUILD_DIR)/include/onion-mcp23008-driver.h $(1)/usr/include/
	# $(CP)	$(PKG_BUILD_DIR)/lib/libonionmcp23008.so $(1)/usr/lib/
	# $(CP)   $(PKG_BUILD_DIR)/include/pwm-exp.h $(1)/usr/include/
	# $(CP)	$(PKG_BUILD_DIR)/lib/libonionpwmexp.so $(1)/usr/lib/
	# $(CP)   $(PKG_BUILD_DIR)/include/relay-exp.h $(1)/usr/include/
	# $(CP)	$(PKG_BUILD_DIR)/lib/libonionrelayexp.so $(1)/usr/lib/
	# $(CP)   $(PKG_BUILD_DIR)/include/oled-exp.h $(1)/usr/include/
	# $(CP)	$(PKG_BUILD_DIR)/lib/libonionoledexp.so $(1)/usr/lib/
endef