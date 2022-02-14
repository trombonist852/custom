#
# Copyright (C) 2019 OpenWrt.org
#
# KFERMercer <KFER.Mercer@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=MosDNS
PKG_VERSION:=v3.1.2
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=MosDNS is a low laterncy DNS client support DoH/DoT
	URL:=https://github.com/IrineSistiana/mosdns
endef


define Package/$(PKG_NAME)/description
MosDNS is a low laterncy DNS client support DoH/DoT
endef

# 禁止OpenWrt对二进制文件进行strip
STRIP:=true

ifeq ($(ARCH),i386)
	PKG_ARCH_MOSDNS:=86
	PKG_HASH:=skip
endif

ifeq ($(ARCH),x86_64)
	PKG_ARCH_MOSDNS:=amd64
	PKG_HASH:=02f0701897e9da20f40ee317cd5158e6ba3c9008a2f488a55f69cef7da25c7d9
endif

ifeq ($(ARCH),mips64el)
	PKG_ARCH_MOSDNS:=mips64-hardfloat
	PKG_HASH:=skip
endif

ifeq ($(ARCH),mipsel)
	PKG_ARCH_MOSDNS:=mipsle-softfloat
	PKG_HASH:=bdddd7993625032d4300d52e9df3bf3b9422f29ee4852039f86fce4df8f05c29
endif

ifeq ($(ARCH),mips)
	PKG_ARCH_MOSDNS:=mipsle-softfloat
	PKG_HASH:=c9de4ee0e8cfb1c61238865aa6016c851e52dabe6c3e65523b2950a2e4670759
endif

ifeq ($(ARCH),arm)
	PKG_ARCH_MOSDNS:=arm-7
	PKG_HASH:=skip
endif

ifeq ($(ARCH),aarch64)
	PKG_ARCH_MOSDNS:=arm64
	PKG_HASH:=skip
endif


PKG_SOURCE:=mosdns-linux-$(PKG_ARCH_MOSDNS).zip

# https://github.com/IrineSistiana/mosdns/releases/download/v1.0.0-rc1/mos-chinadns-linux-mipsle-softfloat.zip
PKG_SOURCE_URL:=https://github.com/IrineSistiana/mosdns/releases/download/$(PKG_VERSION)/

UNZIP_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/$(PKG_NAME)-unzip


define Build/Prepare
	mkdir -vp $(UNZIP_DIR)
	unzip -od $(UNZIP_DIR) $(DL_DIR)/$(PKG_SOURCE)
	wget -O $(UNZIP_DIR)/geosite.dat https://cdn.jsdelivr.net/gh/Loyalsoldier/v2ray-rules-dat@release/geosite.dat
	wget -O $(UNZIP_DIR)/geoip.dat https://raw.githubusercontent.com/Loyalsoldier/v2ray-rules-dat/release/geoip.dat
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	mkdir $(1)/usr/bin/$(PKG_NAME)
	$(INSTALL_BIN) $(UNZIP_DIR)/mosdns $(1)/usr/bin/$(PKG_NAME)/$(PKG_NAME)
	cp $(UNZIP_DIR)/geosite.dat $(1)/usr/bin/$(PKG_NAME)/geosite.dat
	cp $(UNZIP_DIR)/geoip.dat $(1)/usr/bin/$(PKG_NAME)/geoip.dat
	chmod 755 $(1)/usr/bin/$(PKG_NAME)
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
