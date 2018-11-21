# Copyright (c) 2014, AllSeen Alliance. All rights reserved.
#
#    Permission to use, copy, modify, and/or distribute this software for any
#    purpose with or without fee is hereby granted, provided that the above
#    copyright notice and this permission notice appear in all copies.
#
#    THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
#    WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
#    MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
#    ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
#    WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
#    ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
#    OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=uboot-ramips
PKG_VERSION:=1.0.1
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/uboot-ramips

include $(INCLUDE_DIR)/package.mk

define Package/uboot-ramips
 SECTION:=boot
 CATEGORY:=Boot Loaders
 TITLE:=U-Boot for MT7620x platform
 DEPENDS:=@TARGET_ramips
 VARIANT:=$(1)
endef

define Package/uboot-ramips/description
	 MTK MT7620x ramips uboot
endef

ifdef BUILD_VARIANT
$(eval $(call uboot/$(BUILD_VARIANT)))
UBOOT_CONFIG:=$(if $(CONFIG),$(CONFIG),$(BUILD_VARIANT))
UBOOT_IMAGE:=$(if $(IMAGE),$(IMAGE),openwrt-$(BOARD)-$(BUILD_VARIANT)-u-boot.bin)
endif

define Build/Prepare
 	$(call Build/Prepare/Default)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/u-boot CROSS_COMPILE=$(PKG_BUILD_DIR)/toolchain/bin/mipsel-linux-
endef

define Build/Clean
	rm -rf $(PKG_BUILD_DIR)
endef

define Package/uboot-ramips/install
	$(INSTALL_DIR) $(BIN_DIR)/uboot-ramips
	$(CP) $(PKG_BUILD_DIR)/u-boot/uboot.bin $(BIN_DIR)/uboot-ramips/.
endef

$(eval $(call BuildPackage,uboot-ramips))
