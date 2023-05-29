DEBUG = 0

SDKVERSION = 16.2
SYSROOT = $(THEOS)/sdks/iPhoneSimulator16.2.sdk

ARCHS = x86_64
TARGET = simulator:clang

# FULL PATH of the FLEX repo on your own machine
FLEX_ROOT = ../FLEX

# Function to convert /foo/bar to -I/foo/bar
dtoim = $(foreach d,$(1),-I$(d))

# Gather FLEX sources
SOURCES  = $(shell find $(FLEX_ROOT)/Classes -name '*.c')
SOURCES += $(shell find $(FLEX_ROOT)/Classes -name '*.m')
SOURCES += $(shell find $(FLEX_ROOT)/Classes -name '*.mm')
# Gather FLEX headers for search paths
_IMPORTS  = $(shell /bin/ls -d $(FLEX_ROOT)/Classes/*/)
_IMPORTS += $(shell /bin/ls -d $(FLEX_ROOT)/Classes/*/*/)
_IMPORTS += $(shell /bin/ls -d $(FLEX_ROOT)/Classes/*/*/*/)
_IMPORTS += $(shell /bin/ls -d $(FLEX_ROOT)/Classes/*/*/*/*/)
IMPORTS = -I$(FLEX_ROOT)/Classes/ $(call dtoim, $(_IMPORTS))

TWEAK_NAME = libFLEX
$(TWEAK_NAME)_FILES = ../libFLEX.x $(SOURCES)
$(TWEAK_NAME)_FRAMEWORKS = CoreGraphics UIKit ImageIO QuartzCore
$(TWEAK_NAME)_LIBRARIES = sqlite3 z
$(TWEAK_NAME)_CFLAGS += -fobjc-arc -w -Wno-unsupported-availability-guard $(IMPORTS) -g
$(TWEAK_NAME)_CCFLAGS += -std=gnu++11

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
