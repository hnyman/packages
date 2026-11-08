# This is free software, licensed under the GNU General Public License v2.

include $(TOPDIR)/rules.mk

PKG_NAME:=rrdtool
PKG_VERSION:=1.11.0
PKG_RELEASE:=2

PKG_BUILD_DIR:=$(BUILD_DIR)/rrdtool-$(PKG_VERSION)
PKG_SOURCE:=rrdtool-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/oetiker/rrdtool-1.x/releases/download/v$(PKG_VERSION)
PKG_HASH:=24c345b5c077c1b2b2fcbc1a364f1da051650fb6743ad5213096adc04c862ed4
PKG_MAINTAINER:=Hannu Nyman <hannu.nyman@iki.fi>

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
 not expand over time.
endef

define Package/librrd
$(call Package/rrdtool/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+glib2-gio +libxml2
  CONFLICTS:=librrd1
  TITLE+= management library
endef

define Package/librrd/description
$(call Package/rrdtool/description/Default)
 This package contains a shared library, used by other programs.
endef

define Package/rrdtool
$(call Package/rrdtool/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Database
  DEPENDS:=+librrd
  CONFLICTS:=rrdtool1
  TITLE+= management tools
endef

define Package/rrdtool/description
$(call Package/rrdtool/description/Default)
 This package contains command line tools used to manage RRDs.
endef

CONFIGURE_ARGS += \
	--disable-rrd_graph \
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

define Package/librrd/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/librrd.so.* $(1)/usr/lib/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/rrd.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/librrd*.{a,la,so*} $(1)/usr/lib
	$(INSTALL_DIR)	$(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/librrd.pc $(1)/usr/lib/pkgconfig
endef

$(eval $(call BuildPackage,librrd))
$(eval $(call BuildPackage,rrdtool))

