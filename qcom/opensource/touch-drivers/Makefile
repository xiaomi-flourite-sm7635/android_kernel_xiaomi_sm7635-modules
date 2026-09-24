#
# Makefile for the Goodix gt9xx touchscreen driver.
#

TOUCH_ROOT := $(KERNEL_SRC)/$(M)
KBUILD_OPTIONS := TOUCH_ROOT=$(TOUCH_ROOT) CONFIG_MSM_TOUCH=m
KBUILD_OPTIONS += KBUILD_EXTRA_SYMBOLS=$(M)/../display-drivers/msm/Module.symvers
KBUILD_OPTIONS += KBUILD_EXTRA_SYMBOLS=$(M)/../display-drivers/msm/Module.symvers

.PHONY: all modules modules_install clean

all: modules

modules:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) modules $(KBUILD_OPTIONS)

modules_install:
	$(MAKE) INSTALL_MOD_STRIP=1 -C $(KERNEL_SRC) M=$(M) modules_install $(KBUILD_OPTIONS)

clean:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) clean $(KBUILD_OPTIONS)

obj-$(CONFIG_TOUCHSCREEN_GT9XX)		+= gt9xx.o
obj-$(CONFIG_TOUCHSCREEN_GT9XX_UPDATE)	+= gt9xx_update.o
obj-$(CONFIG_TOUCHSCREEN_GT9XX_DEBUG)	+= goodix_tool.o
