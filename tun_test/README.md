# TUN 设备网络工具套件

这是一个功能完整的 Linux TUN 设备网络工具套件，包含 TUN 设备创建、路由配置、防火墙管理和 VPN 服务器功能。

## 🚀 项目概述

本项目提供了一套完整的 TUN 设备网络解决方案，包括：

- **基础 TUN 设备操作** - 创建、配置和监听 TUN 设备
- **高级路由功能** - 自动路由配置和管理
- **防火墙集成** - iptables 规则自动配置
- **VPN 服务器** - 完整的 VPN 服务器解决方案
- **网络诊断** - 全面的网络功能测试工具

## 📁 项目结构

```
tun_test/
├── 核心程序
│   ├── tun_test.c          # 基础 TUN 设备测试程序
│   ├── tun_router.c        # 高级 TUN 路由器程序
│   ├── network_utils.c     # 网络工具函数库
│   └── network_utils.h     # 网络工具头文件
├── 可执行文件
│   ├── tun_test           # 编译后的基础测试程序
│   └── tun_router         # 编译后的路由器程序
├── 自动化脚本
│   ├── setup_vpn_server.sh    # VPN 服务器自动设置脚本
│   ├── network_test.sh        # 网络功能全面测试脚本
│   ├── test_demo.sh           # 基础功能演示脚本
│   └── cleanup_network.sh     # 网络配置安全清理脚本
├── 构建工具
│   └── Makefile              # 构建和管理工具
└── 文档
    └── README.md             # 项目说明文档
```

## ✨ 功能特性

### 基础功能 (tun_test)
- ✅ TUN 设备创建和管理
- ✅ 网络数据包监听和分析
- ✅ IPv4 数据包协议解析
- ✅ 实时数据包信息显示
- ✅ 自定义设备名称支持
- ✅ 非阻塞模式数据处理

### 高级功能 (tun_router)
- 🌐 **路由管理**
  - 自动路由表配置
  - 静态路由添加/删除
  - 默认网关配置
  - 多接口路由支持

- 🔥 **防火墙集成**
  - iptables 规则自动配置
  - NAT 和端口转发
  - 流量过滤和转发
  - 安全策略管理

- 🛡️ **VPN 功能**
  - 完整的 VPN 服务器
  - 客户端连接管理
  - 加密隧道支持
  - 多用户接入

- 📊 **网络诊断**
  - 连通性测试
  - 性能监控
  - 流量统计
  - 错误诊断

## 🔧 安装和编译

### 系统要求
- Linux 操作系统 (内核 2.6+)
- GCC 编译器
- root 权限 (用于网络配置)
- 以下工具包：
  ```bash
  # Ubuntu/Debian
  sudo apt-get install build-essential iproute2 iptables
  
  # CentOS/RHEL
  sudo yum install gcc iproute2 iptables
  ```

### 编译方法

```bash
# 编译所有程序
make all

# 或者分别编译
make tun_test      # 编译基础测试程序
make tun_router    # 编译路由器程序

# 清理编译文件
make clean

# 安装到系统
sudo make install

# 卸载
sudo make uninstall
```

## 🎯 使用指南

### 1. 基础 TUN 设备测试

```bash
# 显示帮助信息
./tun_test -h

# 基本设备创建测试
sudo ./tun_test -t

# 创建自定义名称设备
sudo ./tun_test -d mytun -t

# 启动数据包监听
sudo ./tun_test
```

#### 完整测试流程
```bash
# 终端 1: 启动监听程序
sudo ./tun_test

# 终端 2: 配置网络接口
sudo ip addr add 10.0.0.1/24 dev tun0
sudo ip link set tun0 up

# 终端 3: 发送测试数据
ping 10.0.0.2
```

### 2. 高级路由器功能

```bash
# 显示所有选项
./tun_router -h

# 基本路由器配置
sudo ./tun_router -r -f -e eth0 -n 10.0.0.0/24

# 带 NAT 的路由器
sudo ./tun_router -r -N -f -e eth0 -n 10.0.0.0/24

# 带端口转发的路由器
sudo ./tun_router -r -N -f -e eth0 -p 8080 -t 10.0.0.100 -P 80 -T tcp

# 仅配置模式（不运行转发服务）
sudo ./tun_router -r -N -f -e eth0 -c

# 显示当前网络状态
./tun_router -s
```

#### 路由器选项说明
- `-d <设备名>` - TUN 设备名称
- `-i <IP地址>` - TUN 接口 IP 地址
- `-m <子网掩码>` - 子网掩码
- `-e <外部接口>` - 外部网络接口
- `-n <内部网络>` - 内部网络段
- `-r` - 启用路由功能
- `-N` - 启用 NAT 功能
- `-f` - 启用 IP 转发
- `-p <端口>` - 端口转发外部端口
- `-t <IP>` - 端口转发目标 IP
- `-P <端口>` - 端口转发目标端口
- `-T <协议>` - 转发协议 (tcp/udp)

### 3. 自动化脚本

#### VPN 服务器设置
```bash
# 自动设置 VPN 服务器
sudo ./setup_vpn_server.sh

# 启动 VPN 服务器
sudo ./start_vpn_server.sh

# 停止 VPN 服务器
sudo ./stop_vpn_server.sh

# 检查 VPN 状态
./vpn_status.sh
```

#### 网络功能测试
```bash
# 运行全面的网络功能测试
sudo ./network_test.sh

# 运行基础演示
sudo ./test_demo.sh
```

#### 网络配置清理
```bash
# 安全清理所有测试配置
sudo ./cleanup_network.sh
```

## 🛠️ Makefile 目标

| 目标 | 功能 | 用法 |
|------|------|------|
| `all` | 编译所有程序 | `make` |
| `clean` | 清理编译文件 | `make clean` |
| `test` | 运行基本测试 | `make test` |
| `test-network` | 运行网络测试 | `make test-network` |
| `setup-vpn` | 设置 VPN 服务器 | `make setup-vpn` |
| `install` | 安装到系统 | `make install` |
| `uninstall` | 从系统卸载 | `make uninstall` |
| `help` | 显示程序帮助 | `make help` |
| `check` | 代码风格检查 | `make check` |

## ⚠️ 重要注意事项

### 权限要求
- **必须使用 root 权限** 运行所有网络配置相关的程序
- TUN 设备创建需要 `CAP_NET_ADMIN` 权限
- iptables 配置需要管理员权限

### 系统要求
1. **内核模块**: 确保加载了 `tun` 模块
   ```bash
   sudo modprobe tun
   lsmod | grep tun
   ```

2. **设备文件**: 确保存在 `/dev/net/tun`
   ```bash
   ls -l /dev/net/tun
   ```

3. **网络工具**: 确保安装了 `iproute2` 和 `iptables`

### 安全考虑
- 测试完成后请使用 `cleanup_network.sh` 清理配置
- 不要在生产环境中直接使用测试配置
- 建议在虚拟机或隔离环境中进行测试

## 🔍 故障排除

### 常见错误及解决方案

#### 1. 权限错误
```
错误: Permission denied
解决: sudo ./程序名
```

#### 2. TUN 设备不存在
```
错误: No such file or directory (/dev/net/tun)
解决: sudo modprobe tun
```

#### 3. 编译错误
```
错误: 找不到头文件
解决: sudo apt-get install linux-headers-$(uname -r)
```

#### 4. 网络配置冲突
```
错误: 路由已存在
解决: sudo ./cleanup_network.sh
```

### 系统检查命令
```bash
# 检查 TUN 支持
cat /proc/modules | grep tun

# 检查网络接口
ip addr show

# 检查路由表
ip route show

# 检查防火墙规则
sudo iptables -L -n

# 检查 IP 转发
cat /proc/sys/net/ipv4/ip_forward
```

## 📈 性能特性

- **低延迟**: 优化的数据包处理路径
- **高吞吐**: 支持高速网络数据转发
- **内存效率**: 最小化内存使用和拷贝
- **CPU 友好**: 非阻塞 I/O 和事件驱动架构

## 🔮 扩展功能

项目支持以下扩展：

### 已实现功能
- ✅ 基础 TUN 设备操作
- ✅ 路由表管理
- ✅ iptables 集成
- ✅ NAT 和端口转发
- ✅ 网络状态监控
- ✅ 自动化配置脚本

### 可扩展功能
- 🔄 IPv6 支持
- 🔄 加密隧道 (IPSec/OpenVPN 集成)
- 🔄 负载均衡
- 🔄 QoS 流量控制
- 🔄 Web 管理界面
- 🔄 日志和监控系统
- 🔄 多租户支持

## 📚 代码结构说明

### 核心模块

#### tun_test.c - 基础功能
- `tun_alloc()` - TUN 设备创建
- `print_packet()` - 数据包十六进制显示
- `analyze_packet()` - 协议分析
- `test_tun_read()` - 数据监听循环

#### tun_router.c - 路由器功能
- `configure_tun_router()` - 路由器配置
- `handle_packet_forwarding()` - 数据包转发
- `cleanup_network_config()` - 配置清理
- `signal_handler()` - 信号处理

#### network_utils.c - 网络工具库
- **接口配置**: `configure_interface()`, `set_interface_ip()`
- **路由管理**: `add_route()`, `delete_route()`
- **防火墙**: `add_iptables_rule()`, `setup_nat_masquerade()`
- **诊断工具**: `ping_host()`, `check_connectivity()`

## 🤝 贡献指南

欢迎贡献代码和改进建议！

### 开发环境设置
```bash
git clone <repository>
cd tun_test
make all
sudo make test-network
```

### 代码风格
- 使用 C99 标准
- 遵循 Linux 内核代码风格
- 添加适当的注释和文档

## 📄 许可证

本项目采用开源许可证，详见 LICENSE 文件。

## 🆘 支持和帮助

如果遇到问题或需要帮助：

1. 查看本 README 的故障排除部分
2. 运行 `sudo ./network_test.sh` 进行系统检查
3. 使用 `sudo ./cleanup_network.sh` 清理配置
4. 查看日志文件获取详细错误信息

---

**⚡ 快速开始**: `make all && sudo make test`

**🔧 完整测试**: `sudo make test-network`

**🌐 VPN 服务器**: `sudo make setup-vpn`

**🧹 清理配置**: `sudo ./cleanup_network.sh`