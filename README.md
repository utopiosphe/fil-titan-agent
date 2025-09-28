# Fil-Titan Agent
[English](README.md) | [中文](README_zh.md)

[![Go Version](https://img.shields.io/badge/Go-1.22.5+-blue.svg)](https://golang.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

---

## Project Milestones

### Milestone 01: Foundational Infrastructure & Core Engine Development
**Budget:** $50,000 USD  
**Status:** In Progress

**Goal:** To validate the core concept, complete the project's technical cornerstone, and deliver a backend system verifiable via command line.

**Key Deliverables:**
- **Smart Contract Development:** Development and deployment of core logic
- **Fil-Titan Agent Client (CLI):** Development of the command-line version for core functionalities  
- **Testing Infrastructure & Expenses:** Basic testing environment setup is complete
- **Technical Documentation:** Completion of initial architecture and API design documents

## Quick Start

To get started with Fil-Titan Agent, please refer to our running tutorials and installation guides.

### Dependencies

- **multipass** (windows, macos, linux)
- **virtualbox** (windows)

📖 **Detailed Running Tutorials:** [Multi-Device Type Running Tutorials](https://titannet.gitbook.io/titan-network-cn/4-ce-jia-li-le-ce-shi-wang/titan-agent-an-zhuang-jiao-cheng)

📖 **Quick Running Tutorial:** 

#### 1. Preparation

- **Download Titan Agent installation package: (using linux/amd64 as example)**
    - [agent-linux.zip](https://pcdn.titannet.io/test4/latest/agent-linux.zip)
    

#### 2. Get Key

- **Key acquisition tutorial:**
  - [Titan Network Key Acquisition Tutorial](https://titannet.gitbook.io/titan-network-cn/4-ce-jia-li-le-ce-shi-wang/ru-he-huo-qu-key)

- Example Key (please replace with actual value):

  ```bash
  key=w**********k
  ```

#### 3. Device Installation Steps

##### Extract and Prepare

```bash
# Create installation directory
mkdir -p /data/.titannet

# Copy installation package to target directory (adjust path based on actual batch deployment method)
cp /installation-package-location/agent-linux.zip /data/.titannet/

# Extract installation package
cd /data/.titannet
unzip agent-linux.zip
```

##### Set Permissions

```bash
chmod +x /data/.titannet/agent
```

##### Start Titan Agent

```bash
nohup /data/.titannet/agent --working-dir=/data/.titannet \
                            --server-url=https://test4-api.titannet.io \
                            --key=w3fDCW5XkOwk > /dev/null 2>&1 &
```

##### Verify Process is Running

```bash
ps | grep agent
```

##### If You Need to Stop Agent

```bash
# Find process ID
ps | grep agent

# Stop process
kill <process_id>
```

#### 4. Auto-start on Boot Solution

##### 1. Create systemd service file

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

##### 2. Set Permissions

```bash
sudo chmod 644 /etc/systemd/system/titan-agent.service
```

##### 3. Enable and Start Service

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now titan-agent
```

##### 4. Service Management Commands

```bash
Start service	sudo systemctl start titan-agent
Stop service	sudo systemctl stop titan-agent
Restart service	sudo systemctl restart titan-agent
Check status	sudo systemctl status titan-agent
View logs	sudo journalctl -u titan-agent -f
```

##### 5. Verify Deployment

```bash
# Check if process is running
ps | grep agent

# View logs (if any)
cat /data/.titannet/agent.log
```


### License

MIT License - see the [LICENSE](LICENSE) file for details