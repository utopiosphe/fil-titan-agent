# Fil-Titan Agent
[English](README.md) | [中文](README_zh.md)

[![Go Version](https://img.shields.io/badge/Go-1.22.5+-blue.svg)](https://golang.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

---

## 项目里程碑

### 里程碑 01：基础架构与核心引擎开发
**预算：** $50,000 USD  
**状态：** 进行中

**目标：** 验证核心概念，完成项目的技术基石，并交付可通过命令行验证的后端系统。

**关键交付物：**
- **智能合约开发：** 核心逻辑的开发和部署
- **Fil-Titan Agent 客户端（CLI）：** 核心功能的命令行版本开发  
- **测试基础设施与费用：** 基础测试环境设置已完成
- **技术文档：** 完成初始架构和 API 设计文档

## 快速开始

要开始使用 Fil-Titan Agent，请参阅我们的运行教程和安装指南。

### 依赖

- **multipass** (windows, macos, linux)
- **virtualbox** (windows)



📖 **详细运行教程：** [各设备类型运行教程](https://titannet.gitbook.io/titan-network-cn/4-ce-jia-li-le-ce-shi-wang/titan-agent-an-zhuang-jiao-cheng)

📖 **快速运行教程：** 

#### 1. 准备工作

- **下载 Titan Agent 安装包：(以linux/amd64为例)**
    - [agent-linux.zip](https://pcdn.titannet.io/test4/latest/agent-linux.zip)
    

#### 2. 获取 Key

- **Key 获取教程：**
  - [Titan Network Key 获取教程](https://titannet.gitbook.io/titan-network-cn/4-ce-jia-li-le-ce-shi-wang/ru-he-huo-qu-key)

- 示例 Key（请替换为实际值）：

  ```bash
  key=w**********k
  ```

#### 3. 设备端安装步骤

##### 解压与准备

```bash
# 创建安装目录
mkdir -p /data/.titannet

# 复制安装包到目标目录（根据实际批量部署方式调整路径）
cp /安装包位置/agent-linux.zip /data/.titannet/

# 解压安装包
cd /data/.titannet
unzip agent-linux.zip
```

##### 设置权限

```bash
chmod +x /data/.titannet/agent
```

##### 启动 Titan Agent

```bash
nohup /data/.titannet/agent --working-dir=/data/.titannet \
                            --server-url=https://test4-api.titannet.io \
                            --key=w3fDCW5XkOwk > /dev/null 2>&1 &
```

##### 验证进程是否在运行

```bash
ps | grep agent
```

##### 如果需要停止 Agent

```bash
# 查找进程 ID
ps | grep agent

# 停止进程
kill <进程ID>
```

#### 4. 开机自启动方案

##### 1. 创建systemd服务文件

```bash
sudo tee /etc/systemd/system/titan-agent.service <<EOF
[Unit]
Description=Titan Network Agent
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/data/.titannet
ExecStart=/data/.titannet/agent \\
    --working-dir=/data/.titannet \\
    --server-url=https://test4-api.titannet.io \\
    --key=w**********k
Restart=always
RestartSec=30
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=titan-agent

[Install]
WantedBy=multi-user.target
EOF
```

##### 2. 设置权限

```bash
sudo chmod 644 /etc/systemd/system/titan-agent.service
```

##### 3. 启用并启动服务

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now titan-agent
```

##### 4. 服务管理命令

```bash
启动服务	sudo systemctl start titan-agent
停止服务	sudo systemctl stop titan-agent
重启服务	sudo systemctl restart titan-agent
查看状态	sudo systemctl status titan-agent
查看日志	sudo journalctl -u titan-agent -f
```

##### 5. 验证部署

```bash
# 检查进程是否运行
ps | grep agent

# 查看日志（如果有）
cat /data/.titannet/agent.log
```


### 许可证

MIT 许可证 - 详情请参阅 [LICENSE](LICENSE) 文件