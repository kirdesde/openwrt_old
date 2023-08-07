include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=tmon
PKG_VERSION:=$(shell basename $(LINUX_DIR) | sed 's/linux-//')
PKG_RELEASE:=1

PKG_BUILD_PARALLEL:=1
PKG_MAINTAINER:=Florian Eckert <fe@dev.tdt.de>
PKG_LICENSE:=GPL-2.0-only

PKG_BUILD_DEPENDS:=ncurses

include $(INCLUDE_DIR)/package.mk

define Package/tmon
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=Linux thermal monitoring and testing tool
  VERSION:=$(LINUX_VERSION)-$(PKG_RELEASE)
  URL:=http://www.kernel.org
endef

define Package/tmon/description
  A Monitoring and Testing Tool for Linux kernel thermal subsystem
endef

MAKE_FLAGS = \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	CC="$(TARGET_CC)" \
	LD="$(TARGET_CROSS)ld" \
	EXTRA_CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS) -static" \
	$(if $(findstring c,$(OPENWRT_VERBOSE)),V=1,V='') \
	prefix=/usr

define Build/Compile
	-$(MAKE) clean \
		-C $(LINUX_DIR)/tools/thermal/tmon
	+$(MAKE_FLAGS) $(MAKE) \
		-C $(LINUX_DIR)/tools/thermal/tmon
endef

define Package/tmon/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(LINUX_DIR)/tools/thermal/tmon/tmon \
		$(1)/usr/bin/
endef

$(eval $(call BuildPackage,tmon))
