#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libxml2
PKG_VERSION:=2.9.10
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://xmlsoft.org/sources/
PKG_HASH:=aafee193ffb8fe0c82d4afef6ef91972cbaf5feea100edc2f262750611b4be1f

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:xmlsoft:libxml2

PKG_MAINTAINER:=Michael Heimpold <mhei@heimpold.de>

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=0

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/libxml2
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Gnome XML library
  URL:=http://xmlsoft.org/
  DEPENDS:=+libpthread +zlib
endef

define Package/libxml2/description
  A library for manipulating XML and HTML resources.
endef

define Package/libxml2-dev
  SECTION:=devel
  CATEGORY:=Development
  SUBMENU:=Libraries
  TITLE:=Development files for libxml2
  URL:=http://xmlsoft.org/
  DEPENDS:=+libxml2
endef

define Package/libxml2-dev/description
  A library for manipulating XML and HTML resources.

  This package contains the headers and xml2-config binary.
endef

define Package/libxml2-utils
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=XML command line utilities (xmllint...)
  URL:=http://xmlsoft.org/
  DEPENDS:=+libxml2
endef

define Package/libxml2-utils/description
  This package contains the binaries xmllint and xmlcatalog
  from libxml2, a library for manipulating XML and HTML resources.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \
	--with-c14n \
	--without-catalog \
	--with-debug \
	--without-docbook \
	--with-html \
	--without-ftp \
	--without-http \
	--without-iconv \
	--without-iso8859x \
	--without-legacy \
	--with-output \
	--without-pattern \
	--without-push \
	--without-python \
	--with-reader \
	--without-readline \
	--without-regexps \
	--with-sax1 \
	--with-schemas \
	--with-threads \
	--with-tree \
	--with-valid \
	--with-writer \
	--with-xinclude \
	--with-xpath \
	--with-xptr \
	--with-zlib=$(STAGING_DIR)/opt \
	--without-lzma

HOST_CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \
	--with-c14n \
	--without-catalog \
	--with-debug \
	--without-docbook \
	--with-html \
	--without-ftp \
	--without-http \
	--without-iconv \
	--without-iso8859x \
	--without-legacy \
	--with-output \
	--without-pattern \
	--without-push \
	--without-python \
	--with-reader \
	--without-readline \
	--without-regexps \
	--with-sax1 \
	--with-schemas \
	--with-threads \
	--with-tree \
	--with-valid \
	--with-writer \
	--with-xinclude \
	--with-xpath \
	--with-xptr \
	--with-zlib \
	--without-lzma

define Build/InstallDev
	$(INSTALL_DIR) $(2)/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/xml2-config \
		$(2)/bin/$(GNU_TARGET_NAME)-xml2-config
	$(SED) 's,^\(prefix\|exec_prefix\)=.*,\1=$(STAGING_DIR)/opt,g' \
		$(2)/bin/$(GNU_TARGET_NAME)-xml2-config
	$(LN) $(GNU_TARGET_NAME)-xml2-config $(2)/bin/xml2-config

	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/libxml2 $(1)/opt/include/

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libxml2.{la,a,so*} $(1)/opt/lib/

	$(INSTALL_DIR) $(1)/opt/lib/cmake/libxml2
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/cmake/libxml2/libxml2-config.cmake \
		$(1)/opt/lib/cmake/libxml2

	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libxml-2.0.pc $(1)/opt/lib/pkgconfig/

	$(INSTALL_DIR) $(2)/share/aclocal/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/aclocal/* $(2)/share/aclocal
endef

define Host/Install
	$(call Host/Install/Default)
	mv $(1)/bin/xml2-config $(1)/bin/$(GNU_HOST_NAME)-xml2-config
	$(LN) $(GNU_HOST_NAME)-xml2-config $(1)/bin/xml2-config
endef

define Package/libxml2/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libxml2.so.* $(1)/opt/lib/
endef

define Package/libxml2-dev/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/xml2-config $(1)/opt/bin/
	$(SED) "s,$(STAGING_DIR),,g" $(1)/opt/bin/xml2-config

	$(INSTALL_DIR) $(1)/opt/include/
	$(CP) $(PKG_INSTALL_DIR)/opt/include/* $(1)/opt/include/

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libxml2.so $(1)/opt/lib/

	$(INSTALL_DIR) $(1)/opt/lib/{cmake,pkgconfig}
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/{cmake,pkgconfig} $(1)/opt/lib/
	$(SED) "s,$(STAGING_DIR),,g" $(1)/opt/lib/pkgconfig/*.pc

	$(INSTALL_DIR) $(1)/opt/share/aclocal
	$(CP) $(PKG_INSTALL_DIR)/opt/share/aclocal/* $(1)/opt/share/aclocal
endef

define Package/libxml2-utils/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/xmllint $(1)/opt/bin/
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/xmlcatalog $(1)/opt/bin/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,libxml2))
$(eval $(call BuildPackage,libxml2-dev))
$(eval $(call BuildPackage,libxml2-utils))
