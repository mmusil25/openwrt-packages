include $(TOPDIR)/rules.mk

PKG_NAME:=detectGoogle
PKG_VERSION:=1.0
PKG_RELEASE:=2

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git@github.com:mmusil25/openwrt-detect-google.git
PKG_SOURCE_VERSION:=7a6c9a124d53da117622e598bc5689264523b433
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_BUILD_DEPENDS:=libpcap libgpiod 

include $(INCLUDE_DIR)/package.mk

define Package/detectGoogle
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Detect Google Access
	DEPENDS:=+libpcap +libgpiod +libstdcpp 
endef

define Package/detectGoogle/description
	Detects access to www.google.com and outputs a message.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	rm -rf $(PKG_BUILD_DIR)/$(PKG_NAME)
	git clone $(PKG_SOURCE_URL) $(PKG_BUILD_DIR)/$(PKG_NAME)
	cd $(PKG_BUILD_DIR)/$(PKG_NAME) && git checkout $(PKG_SOURCE_VERSION)
	git archive --format=tar.gz --output=$(PKG_NAME)-$(PKG_VERSION).tar.gz HEAD
	mv $(PKG_NAME)-$(PKG_VERSION).tar.gz $(PKG_BUILD_DIR)/
endef

define Build/Compile
    $(TARGET_CC) $(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include -o $(PKG_BUILD_DIR)/detectGoogle/detectGoogle $(PKG_BUILD_DIR)/$(PKG_NAME)/detectGoogle.cpp $(TARGET_LDFLAGS) -L$(STAGING_DIR)/usr/lib -lpcap -lgpiod -lstdc++
endef


define Package/detectGoogle/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/detectGoogle/detectGoogle $(1)/usr/bin/
endef

$(eval $(call BuildPackage,detectGoogle))
