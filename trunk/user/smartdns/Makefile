include $(ROOTDIR)/rules.mk

PKG_NAME:=smartdns
PKG_VERSION:=47.1
PKG_SOURCE:=smartdns-Release$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/pymumu/smartdns/archive/refs/tags/
PKG_SOURCE_URL_FILE:=Release$(PKG_VERSION).tar.gz
PKG_HASH:=0a143ee81ccb7a31b7b7b0c29d6a6ee41a54331da75477719925592af124ec97
PKG_BUILD_DIR:=$(BUILD_DIR)/smartdns-Release$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) -j$(HOST_NCPU) \
		CC="$(CC)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS) -static"
	upx --best --lzma $(PKG_BUILD_DIR)/src/smartdns
endef

$(eval $(call BuildPackage,smartdns))

romfs:
	$(INSTALL_DIR) $(ROMFSDIR)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/smartdns $(ROMFSDIR)/usr/bin/smartdns
	$(INSTALL_BIN) ./smartdns.sh $(ROMFSDIR)/usr/bin/smartdns.sh
	$(INSTALL_DIR) $(ROMFSDIR)/etc_ro/smartdns
	[ ! -d ./conf/default ] || $(INSTALL_DATA) ./conf/default/*.conf $(ROMFSDIR)/etc_ro/
	[ ! -d ./conf/rules ] || $(INSTALL_DATA) ./conf/rules/* $(ROMFSDIR)/etc_ro/smartdns/
