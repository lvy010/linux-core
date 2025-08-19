# TUN 设备测试程序

这是一个用于测试 Linux TUN 设备创建和使用的 C 语言程序。

## 功能特性

- 创建 TUN 网络设备
- 监听和分析网络数据包
- 支持 IPv4 数据包解析
- 提供详细的数据包信息显示
- 支持自定义设备名称

## 编译方法

```bash
# 编译程序
make

# 或者直接使用 gcc
gcc -Wall -Wextra -std=c99 -O2 -o tun_test tun_test.c
```

## 使用方法

### 基本用法

```bash
# 需要 root 权限运行
sudo ./tun_test
```

### 命令行选项

```bash
# 显示帮助信息
./tun_test -h

# 指定设备名称
sudo ./tun_test -d mytun

# 仅测试设备创建（不监听数据）
sudo ./tun_test -t
```

## 测试步骤

1. **编译程序**
   ```bash
   make
   ```

2. **运行程序（在终端1中）**
   ```bash
   sudo ./tun_test
   ```

3. **配置网络接口（在终端2中）**
   ```bash
   # 为 TUN 设备分配 IP 地址
   sudo ip addr add 10.0.0.1/24 dev tun0
   
   # 启用网络接口
   sudo ip link set tun0 up
   ```

4. **发送测试数据包**
   ```bash
   # 发送 ping 包测试
   ping 10.0.0.2
   
   # 或者发送到其他地址
   ping 10.0.0.100
   ```

5. **观察输出**
   - 程序会显示接收到的数据包信息
   - 包括源地址、目标地址、协议类型等

## Makefile 目标

```bash
make          # 编译程序
make clean    # 清理编译文件
make test     # 运行测试模式
make run      # 运行完整程序
make help     # 显示程序帮助
make debug    # 编译调试版本
make install  # 安装到系统
make check    # 代码检查（需要 cppcheck）
```

## 注意事项

1. **权限要求**: 程序需要 root 权限才能创建 TUN 设备
2. **内核模块**: 确保系统加载了 `tun` 内核模块
3. **设备文件**: 确保 `/dev/net/tun` 设备文件存在
4. **网络配置**: 需要手动配置 TUN 设备的 IP 地址

## 故障排除

### 常见错误

1. **"Permission denied"**
   - 解决方案: 使用 `sudo` 运行程序

2. **"No such file or directory" (/dev/net/tun)**
   - 解决方案: 加载 tun 模块
   ```bash
   sudo modprobe tun
   ```

3. **"Operation not permitted"**
   - 解决方案: 检查用户权限和系统配置

### 检查系统支持

```bash
# 检查 tun 模块是否加载
lsmod | grep tun

# 检查设备文件是否存在
ls -l /dev/net/tun

# 手动加载 tun 模块
sudo modprobe tun
```

## 代码结构

- `tun_alloc()`: TUN 设备创建函数
- `print_packet()`: 数据包十六进制显示
- `analyze_packet()`: 数据包协议分析
- `test_tun_read()`: 数据包监听循环
- `main()`: 主程序入口和参数解析

## 扩展功能

程序可以进一步扩展以支持：
- 数据包转发
- 更多协议解析（IPv6、ARP等）
- 数据包过滤
- 统计信息收集
- 配置文件支持
