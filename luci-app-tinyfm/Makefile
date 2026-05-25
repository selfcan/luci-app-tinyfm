# SPDX-License-Identifier: GPL-3.0
#
# Copyright (C) 2022-2025 muink <https://github.com/muink>

include $(TOPDIR)/rules.mk

LUCI_NAME:=luci-app-tinyfilemanager
PKG_VERSION:=2.6
PKG_RELEASE:=20251224

LUCI_TITLE:=LuCI Tiny File Manager
LUCI_DEPENDS:=+php8 +php8-cgi +php8-fastcgi +php8-fpm +php8-mod-session +php8-mod-ctype +php8-mod-fileinfo +php8-mod-zip +php8-mod-iconv +php8-mod-mbstring +coreutils-stat +zoneinfo-asia +bash +curl +tar
LUCI_DESCRIPTION:=This is Tiny File Manager, but for LuCI OpenWrt.
LUCI_MAINTAINER:=OpenWrt Community

PKG_UNPACK=$(CURDIR)/.prepare.sh $(PKG_NAME) $(CURDIR) $(PKG_BUILD_DIR)

define Package/$(LUCI_NAME)/conffiles
/etc/config/tinyfilemanager
endef

define Package/$(LUCI_NAME)/postinst
#!/bin/sh

mkdir -p "$${IPKG_INSTROOT}/www/tinyfm" 2>/dev/null

[ ! -e "$${IPKG_INSTROOT}/www/tinyfm/rootfs" ] && \
ln -s / "$${IPKG_INSTROOT}/www/tinyfm/rootfs"

[ ! -e "$${IPKG_INSTROOT}/www/tinyfm/openclash" ] && \
ln -s /etc/openclash "$${IPKG_INSTROOT}/www/tinyfm/openclash"

memory_limit=16M
total_size_limit=5G
single_size_limit=2G
otime_uploads_limit=200

sed -Ei "s|^(memory_limit) *=.*$$|\1 = $$memory_limit|; \
         s|^(post_max_size) *=.*$$|\1 = $$total_size_limit|; \
         s|^(upload_max_filesize) *=.*$$|\1 = $$single_size_limit|; \
         s|^(max_file_uploads) *=.*$$|\1 = $$otime_uploads_limit|" \
"$${IPKG_INSTROOT}/etc/php.ini"

# unpack
tar -C "$${IPKG_INSTROOT}/www/tinyfm" -xzf "$${IPKG_INSTROOT}/www/tinyfm/index.tgz"

rm -f "$${IPKG_INSTROOT}/www/tinyfm/index.tgz"

endef

define Package/$(LUCI_NAME)/prerm
#!/bin/sh

if [ -d /www/tinyfm ]; then
    rm -rf /www/tinyfm
fi

endef

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
