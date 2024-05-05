include $(TOPDIR)/rules.mk

PKG_NAME:=detectGoogle
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git@github.com:mmusil25/openwrt-detect-google.git
PKG_SOURCE_VERSION:=d46629327c1da31d7df179d7a72f5100c1e16222
PKG_SOURCE:=$(PKG_NAME).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_BUILD_DEPENDS:=libpcap

include $(INCLUDE_DIR)/package.mk

define Package/detectGoogle
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Detect Google Access
	DEPENDS:=+libpcap
endef

define Package/detectGoogle/description
	Detects access to www.google.com and outputs a message.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	git clone $(PKG_SOURCE_URL) $(PKG_BUILD_DIR)
	cd $(PKG_BUILD_DIR) && git checkout $(PKG_SOURCE_VERSION)
	cd $(PKG_BUILD_DIR) && git archive --format=tar.gz --output=$(PKG_NAME).tar.gz HEAD
	$(CP) $(PKG_BUILD_DIR)/$(PKG_SOURCE) $(PKG_BUILD_DIR)/
endef


define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/detectGoogle $(PKG_BUILD_DIR)/detectGoogle.cpp $(TARGET_LDFLAGS) -lpcap
endef

define Package/detectGoogle/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/detectGoogle $(1)/usr/bin/
endef

$(eval $(call BuildPackage,detectGoogle))
