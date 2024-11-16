include $(TOPDIR)/rules.mk

PKG_NAME:=harfbuzz
PKG_VERSION:=10.0.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/harfbuzz/harfbuzz/releases/download/$(PKG_VERSION)/
PKG_HASH:=c2dfe016ad833a5043ecc6579043f04e8e6d50064e02ad449bb466e6431e3e04

PKG_MAINTAINER:=
PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

TARGET_CPPFLAGS += -DHB_MINI

MESON_ARGS += \
	-Db_lto=true \
	-Dglib=disabled \
	-Dgobject=disabled \
	-Dcairo=disabled \
	-Dchafa=disabled \
	-Dicu=disabled \
	-Dtests=disabled \
	-Dintrospection=disabled \
	-Ddocs=disabled \
	-Dutilities=disabled \
	-Dbenchmark=disabled

define Package/harfbuzz
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Video
  TITLE:=Text shaping engine, supports OpenType
  URL:=http://www.harfbuzz.org/
  DEPENDS:=+libfreetype
endef

define Package/harfbuzz/description
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc $(1)/usr/lib/pkgconfig/
endef

define Package/harfbuzz/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,harfbuzz))
