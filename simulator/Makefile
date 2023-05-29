DEBUG = 0

SDKVERSION = 16.2
SYSROOT = $(THEOS)/sdks/iPhoneSimulator16.2.sdk

ARCHS = x86_64
TARGET = simulator:clang

TWEAK_NAME = FLEXing
$(TWEAK_NAME)_GENERATOR = internal
$(TWEAK_NAME)_FILES = ../Tweak.xm ../SpringBoard.xm
$(TWEAK_NAME)_CFLAGS += -fobjc-arc -w

include $(THEOS)/makefiles/common.mk
include $(THEOS_MAKE_PATH)/tweak.mk

sim::stage
	rm -f /opt/simject/$(TWEAK_NAME).dylib
	rm -f /opt/simject/$(TWEAK_NAME).plist
	cp .theos/_/Library/MobileSubstrate/DynamicLibraries/$(TWEAK_NAME).dylib /opt/simject/$(TWEAK_NAME).dylib
	cp -f ./$(TWEAK_NAME).plist /opt/simject/$(TWEAK_NAME).plist
	ldid -S /opt/simject/$(TWEAK_NAME).dylib
	/opt/simject/bin/resim
clean::clean all
	rm -f /opt/simject/$(TWEAK_NAME).dylib
	rm -f /opt/simject/$(TWEAK_NAME).plist
