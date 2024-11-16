#
# Copyright (C) 2008-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cairo
PKG_VERSION:=1.18.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://cairographics.org/releases/
PKG_HASH:=a62b9bb42425e844cc3d6ddde043ff39dbabedd1542eba57a2eb79f85889d45a
PKG_FIXUP:=libtool

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

PKG_INSTALL:=1

define Package/libcairo
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Video
  TITLE:=Multi-platform 2D graphics library
  DEPENDS:=+fontconfig +libpng +pixman
  URL:=https://www.cairographics.org/
endef

define Package/libcairo/description
Cairo is a 2D graphics library. The cairo API provides operations similar
to the drawing operators of PostScript and PDF. Operations in cairo
include stroking and filling cubic Bezier splines, transforming and
compositing translucent images, and antialiased text rendering. All
drawing operations can be transformed by any affine transformation
(scale, rotation, shear, etc.).
endef

MESON_ARGS += \
	-Db_lto=true \
	-Dfontconfig=enabled \
	-Dfreetype=enabled \
	-Ddwrite=disabled \
	-Dquartz=disabled \
	-Dtee=disabled \
	-Dxcb=disabled \
	-Dxlib=disabled \
	-Dzlib=disabled \
	-Dtests=disabled \
	-Dglib=disabled \
	-Dspectre=disabled \
	-Dsymbol-lookup=disabled \
	-Dgtk_doc=false

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* $(1)/usr/lib/pkgconfig/
	$(INSTALL_DIR) $(1)/usr/include/cairo/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/cairo/* $(1)/usr/include/cairo/
endef

define Package/libcairo/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libcairo))

