# This is free software, licensed under the Apache License, Version 2.0
#
# Copyright (C) 2025 Maizil <https://github.com/maizil41>

include $(TOPDIR)/rules.mk

LUCI_TITLE:=LuCI support for Tiny File Manager.
LUCI_DEPENDS:=+luci +libc +php8 +php8-cgi +php8-mod-session +php8-mod-ctype +php8-mod-fileinfo +php8-mod-zip +php8-mod-iconv +coreutils-stat +php8-mod-mbstring +zoneinfo-asia
LUCI_DESCRIPTION:=This is Tiny File Manager, but for LuCI OpenWrt.
LUCI_MAINTAINER:=Maizil41 <https://github.com/maizil41>

PKG_VERSION:=2.5
PKG_RELEASE:=1
PKG_LICENSE:=Apache-2.0
PKG_ARCH:=all

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
