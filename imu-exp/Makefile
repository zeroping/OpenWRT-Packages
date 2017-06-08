# Copyright (C) 2017 Onion Corporation
# 
# Author: Gabriel Ongpauco <gabriel@onion.io>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# This package will install the following:
# * The IMU Expansion C library
# * The imu-exp command line program
# * An example program to showcase the library functions

include $(TOPDIR)/rules.mk
PKG_NAME:=imu-exp
PKG_VERSION:=0.1
PKG_RELEASE:=1


PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=HEAD
PKG_SOURCE_URL:=https://github.com/OnionIoT/imu-exp.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

# Package definitions
## library
define Package/libonionimuexp
	SECTION:=onion
	CATEGORY:=Onion
	SUBMENU:=Libraries
	TITLE:=C library for the Onion IMU Expansion
	DEPENDS:=+liboniondebug +libonioni2c
endef

define Package/libonionimuexp/description
C library for the Onion IMU Expansion
endef

## example program
define Package/imu-exp-test
	SECTION:=onion
	CATEGORY:=Onion
	SUBMENU:=Drivers
	TITLE:=Example IMU Expansion program
	DEPENDS:=+liboniondebug +libonioni2c +libonionimuexp
endef

define Package/imu-exp-test/description
Example IMU Expansion program
endef

# Enable position independent code for shared libraries
TARGET_CFLAGS += $(FPIC)
TARGET_LIBS = -loniondebug -lonioni2c # is this correct?

# Compiling
define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	LIB="$(TARGET_LIBS)"
endef

# InstallDev section required for libraries
define Build/InstallDev
	mkdir -p $(1)/usr/include $(1)/usr/lib
	$(CP)   $(PKG_BUILD_DIR)/include/imu-exp.h $(1)/usr/include/
	$(CP)	$(PKG_BUILD_DIR)/lib/libonionimuexp.so $(1)/usr/lib/
endef

# install instructions
## library
define Package/libonionimuexp/install
	# install the static library object
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) 	$(PKG_BUILD_DIR)/lib/libonionimuexp.so $(1)/usr/lib/
endef

## test program
define Package/imu-exp-test/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/imu-exp-test $(1)/usr/sbin/
endef

# build the things
$(eval $(call BuildPackage,libonionimuexp))
$(eval $(call BuildPackage,imu-exp-test))