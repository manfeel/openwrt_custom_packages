include $(TOPDIR)/rules.mk
PKG_SOURCE_URL:=https://github.com/meyerd/n2n
PKG_NAME:=n2n
PKG_RELEASE:=1
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_SOURCE_PROTO:=git
#PKG_SOURCE_VERSION:=1
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
CMAKE_SOURCE_SUBDIR:=n2n_v2

define Package/n2n/Default
	SECTION:=net
	CATEGORY:=Network
	VERSION:=2
	TITLE:=N2N VPN tunneling daemon(V2)
	URL:=http://www.ntop.org/n2n/
	SUBMENU:=VPN
	DEPENDS:=+kmod-tun +resolveip +libopenssl
endef

define Package/n2n-edge
$(call Package/n2n/Default)
endef

define Package/n2n-supernode
$(call Package/n2n/Default)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	$(TARGET_CONFIGURE_OPTS) \
	CFLAGS="$(TARGET_CFLAGS)" \
	INSTALL_PROG=":"
endef

define Package/n2n-edge/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/edge $(1)/usr/sbin/
	#$(INSTALL_DIR) $(1)/lib/netifd/proto
	#$(INSTALL_BIN) ./files/n2n.sh $(1)/lib/netifd/proto
endef

define Package/n2n-supernode/conffiles
/etc/config/n2n
endef

define Package/n2n-supernode/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/supernode $(1)/usr/sbin/
	#$(INSTALL_DIR) $(1)/etc/init.d
	#$(INSTALL_BIN) ./files/n2n.init $(1)/etc/init.d/n2n
	#$(INSTALL_DIR) $(1)/etc/config
	#$(INSTALL_DATA) ./files/n2n.config $(1)/etc/config/n2n
endef
$(eval $(call BuildPackage,n2n-edge))
$(eval $(call BuildPackage,n2n-supernode))
