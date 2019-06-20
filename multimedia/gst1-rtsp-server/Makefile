include $(TOPDIR)/rules.mk

PKG_NAME:=gst1-rtsp-server
PKG_VERSION:=1.16.0
PKG_RELEASE:=1

PKG_MAINTAINER:= Sindre Hansen <sindre.hansen@blueye.no> \
		Erlend Eriksen <erlend.eriksen@blueye.no>

PKG_SOURCE:=gst-rtsp-server-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://gstreamer.freedesktop.org/src/gst-rtsp-server
PKG_HASH:=198e9eec1a3e32dc810d3fbf3a714850a22c6288d4a5c8e802c5ff984af03f19

PKG_LICENSE:=LGPLv2 GPLv2
PKG_LICENSE_FILES:=COPYING.LIB COPYING

PKG_BUILD_DIR:=$(BUILD_DIR)/gst-rtsp-server-$(PKG_VERSION)

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

GST_VERSION:=1.0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/gst1-rtsp-server/Default
	CATEGORY:=Multimedia
	SECTION:=multimedia
	TITLE:=Gstreamer RTSP Server
	URL:=https://gstreamer.freedesktop.org/modules/gst-rtsp-server.html
endef

define Package/gst1-rtsp-server
	$(call Package/gst1-rtsp-server/Default)
	DEPENDS:=+libgst1-rtsp-server
endef

define Package/gst1-rtsp-server/description/Default
	RTSP server library based on GStreamer
endef

define Package/gst1-rtsp-server/description
	$(call Package/gst1-rtsp-server/description/Default)
endef

define Package/libgst1-rtsp-server
	$(call Package/gst1-rtsp-server/Default)
	DEPENDS:=+glib2 +gstreamer1 +libgst1app +libgst1rtp +libgst1rtsp +libgst1sdp
endef

define Package/libgst1-rtsp-server/description
	$(call Package/gst1-rtsp-server/description/Default)
endef

CONFIGURE_ARGS += \
	--disable-Bsymbolic \
	--disable-fatal-warnings \
	--disable-glib-asserts \
	--disable-gobject-cast-checks \
	--disable-gtk-doc-html \
	--disable-introspection \
	--without-libiconv-prefix \
	--without-libintl-prefix \
	--disable-valgrind \
	--disable-rpath \
	--disable-tests \
	--disable-zlib \
	--enable-gettext=no

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/gstreamer-$(GST_VERSION)
	( cd $(PKG_INSTALL_DIR); $(CP) \
		./usr/include/gstreamer-$(GST_VERSION)/* \
		$(1)/usr/include/gstreamer-$(GST_VERSION)/ \
	)
	$(INSTALL_DIR) $(1)/usr/lib
	( cd $(PKG_INSTALL_DIR); $(CP) \
		./usr/lib/libgst*-$(GST_VERSION).{la,so*} \
		$(1)/usr/lib/ \
	)
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	( cd $(PKG_INSTALL_DIR); $(CP) \
		./usr/lib/pkgconfig/gstreamer*-$(GST_VERSION).pc \
		$(1)/usr/lib/pkgconfig/ \
	)
endef

define Package/gst1-rtsp-server/install
	true
endef

define Package/libgst1-rtsp-server/install
	$(INSTALL_DIR) $(1)/usr/lib
	( cd $(PKG_INSTALL_DIR); $(CP) \
		./usr/lib/libgstrtspserver-$(GST_VERSION).so.* \
		$(1)/usr/lib/ \
	)
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/examples/.libs/test-launch \
		$(1)/usr/bin/gst-rtsp-launch
endef

$(eval $(call BuildPackage,libgst1-rtsp-server))
$(eval $(call BuildPackage,gst1-rtsp-server))
