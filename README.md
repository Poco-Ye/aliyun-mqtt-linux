#阿里云移植进入ARM9平台
## 1、可以先配置src/configs/config.arm-linux.demo

配置完
.config的配置为

CONFIG_src/utils = y
CONFIG_src/tls = y
CONFIG_src/tfs = y
CONFIG_src/system = y
CONFIG_src/shadow = y
CONFIG_src/sdk-tests = y
CONFIG_src/sdk-impl = y
CONFIG_src/platform = y
CONFIG_src/ota = y
CONFIG_src/mqtt = y
CONFIG_src/log = y
CONFIG_src/http = y
CONFIG_src/guider = y
CONFIG_src/coap = y
CONFIG_sample = y
# Automatically Generated Section End

# VENDOR :   arm-linux
# MODEL  :   demo
CONFIG_ENV_CFLAGS = -Wall

OVERRIDE_CC = arm-linux-gnueabi-gcc
OVERRIDE_AR = arm-linux-gnueabi-gcc-ar

#CONFIG_src/platform =
#CONFIG_sample =
CONFIG_src/sdk-tests =

##2、编译完成之后进入output/release/src

修改Makefile的编译器arm-hisiv300-linux-uclibcgnueabi-gcc（什么平台对应什么编译器，不能直接-static直接编译，因为阿里云开始开发时是就是在gcc的库上进行）

##3、编完之后查看库是否一致
file ext.mqtt
 
ext.mqtt: ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), dynamically linked, interpreter /lib/ld-uClibc.so.0, not stripped

看看/lib/ld-uClibc.so.0 是否与板子上面跑的linux /lib  或者/usr/lib 一致，一致就可以了。


arm-linux-gnueabi-readelf ext.mqtt -a >a

vim a


Dynamic section at offset 0x50014 contains 22 entries:
  Tag        Type                         Name/Value
 0x00000001 (NEEDED)                     Shared library: [libc.so.0]
 0x00000001 (NEEDED)                     Shared library: [ld-uClibc.so.0]


可以了

