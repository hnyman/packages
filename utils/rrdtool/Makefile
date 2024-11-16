#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rrdtool
PKG_VERSION:=1.8.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/rrdtool-$(PKG_VERSION)
PKG_SOURCE:=rrdtool-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:= \
	https://github.com/oetiker/rrdtool-1.x/releases/download/v$(PKG_VERSION) \
	https://oss.oetiker.ch/rrdtool/pub/archive
PKG_HASH:=bd37614137d7a8dc523359648eb2a81631a34fd91a82ed5581916a52c08433f4
PKG_MAINTAINER:=

PKG_FIXUP:=autoreconf gettext-version
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/rrdtool/Default
  TITLE:=Round Robin Database (RRD) new version
  URL:=https://oss.oetiker.ch/rrdtool/
endef

define Package/rrdtool/description/Default
 RRD is the acronym for Round Robin Database. RRD is a system to store and
 display time-series data (i.e. network bandwidth, machine-room temperature,
 server load average). It stores the data in a very compact way that will
 not expand over time, and it presents useful graphs by processing the data
 to enforce a certain data density. It can be used either via simple wrapper
 scripts (from shell or Perl) or via frontends that poll network devices and
 put friendly user interface on it.
endef

define Package/librrd
$(call Package/rrdtool/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+glib2 +libxml2 +libpng +libcairo +libpango +dejavu-fonts-ttf-DejaVuSansMono
  TITLE+= management library
endef

define Package/librrd/description
$(call Package/rrdtool/description/Default)
 This package contains a shared library, used by other programs.
endef

define Package/rrdcgi
$(call Package/rrdtool/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Database
  DEPENDS:=+librrd
  TITLE+= CGI graphing tool
endef

define Package/rrdcgi/description
$(call Package/rrdtool/description/Default)
 This package contains the rrdcgi tool used to create web pages containing
 RRD graphs based on templates.
endef

define Package/rrdtool
$(call Package/rrdtool/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Database
  DEPENDS:=+librrd
  TITLE+= management tools
endef

define Package/rrdtool/description
$(call Package/rrdtool/description/Default)
 This package contains command line tools used to manage RRDs.
endef

CONFIGURE_ARGS += \
	--disable-docs \
	--disable-examples \
	--disable-rrdcached \
	--disable-rrdcgi \
	--disable-libdbi \
	--disable-librados \
	--disable-libwrap \
	--disable-lua \
	--disable-perl \
	--disable-python \
	--disable-ruby \
	--disable-tcl

define Package/rrdtool/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/rrd{tool,update} $(1)/usr/bin/
endef

define Package/rrdcgi/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/rrdcgi $(1)/usr/bin/
endef

define Package/librrd/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/librrd.so.* $(1)/usr/lib/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/rrd.h $(1)/usr/include/
	$(INSTALL_DIR)  $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/librrd*.{a,la,so*} $(1)/usr/lib
	$(INSTALL_DIR)	$(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig $(1)/usr/lib/
endef

$(eval $(call BuildPackage,librrd))
$(eval $(call BuildPackage,rrdcgi))
$(eval $(call BuildPackage,rrdtool))

