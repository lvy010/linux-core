# TUN 设备测试程序 Makefile

CC = gcc
CFLAGS = -Wall -Wextra -std=c99 -O2
TARGET = tun_test
SOURCE = tun_test.c

# 默认目标
all: $(TARGET)

# 编译目标
$(TARGET): $(SOURCE)
	$(CC) $(CFLAGS) -o $(TARGET) $(SOURCE)
	@echo "编译完成: $(TARGET)"

# 清理编译生成的文件
clean:
	rm -f $(TARGET)
	@echo "清理完成"

# 安装（复制到 /usr/local/bin）
install: $(TARGET)
	sudo cp $(TARGET) /usr/local/bin/
	@echo "安装完成: /usr/local/bin/$(TARGET)"

# 卸载
uninstall:
	sudo rm -f /usr/local/bin/$(TARGET)
	@echo "卸载完成"

# 运行测试（仅创建设备）
test: $(TARGET)
	@echo "运行测试模式..."
	sudo ./$(TARGET) -t

# 运行完整测试（需要手动停止）
run: $(TARGET)
	@echo "运行完整测试（按 Ctrl+C 停止）..."
	sudo ./$(TARGET)

# 显示帮助
help: $(TARGET)
	./$(TARGET) -h

# 检查代码风格
check:
	@echo "检查代码风格..."
	cppcheck --enable=all --std=c99 $(SOURCE) 2>/dev/null || echo "cppcheck 未安装，跳过检查"

# 调试版本
debug: CFLAGS += -g -DDEBUG
debug: $(TARGET)
	@echo "调试版本编译完成"

.PHONY: all clean install uninstall test run help check debug
