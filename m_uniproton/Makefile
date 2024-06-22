
############################定义一些全局变量#################################

#########################路径##########################

# Makefile文件所在的绝对路径
TOP_DIR:= $(patsubst %/,%, $(dir $(abspath $(firstword $(MAKEFILE_LIST)))))
# 调用Makfile 时所在的绝对路径
CUR_DIR:= $(CURDIR)
# 源码所在的绝对路径
SRC:= $(TOP_DIR)/src
# 生成的目标代码所在的绝对路径
BUILD:= $(TOP_DIR)/build

#########################工具##########################

# 交叉编译器前缀
CROSS_COMPILE:= riscv64-linux-gnu-
# C编译器
CC:= $(CROSS_COMPILE)gcc
# CFLAG
CCFLAGS := 
# ...
# ...
# ...

SRC_FILE:= $(shell find $(SRC) -name "*.s")
SRC_FILE+= $(shell find $(SRC) -name "*.c")

OBJECTS:= $(patsubst $(SRC)/%.c, $(BUILD)/%.o, $(SRC_FILE))
OBJECTS:= $(patsubst $(SRC)/%.s, $(BUILD)/%.o, $(OBJECTS))


rtos.elf: $(OBJECTS)
	@mkdir -p $(dir $@)
	$(CC) $(OBJECTS) --freestanding --entry=_start -Ttext=0x80000000 -o $@

$(BUILD)/%.o : $(SRC)/%.s
	@mkdir -p $(dir $@)
	$(CC) $(CCFLAGS) -c $< -o $@

$(BUILD)/%.o : $(SRC)/%.c
	@mkdir -p $(dir $@)
	$(CC) $(CCFLAGS) -c $< -o $@

clean:
	rm -rf $(BUILD)
	rm -rf *.elf

debug:
	@echo "${OBJECTS}"

.PHONY: debug clean