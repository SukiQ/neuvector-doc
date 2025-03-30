# 概述



## 发展历史



- **2015年**：NeuVector 由 **Fei Huang（黄飞）** 和 **Gary Duan（段赛）** 在美国硅谷创立，目标是解决容器和微服务环境的安全挑战
- **2016年**：推出 **首个容器防火墙**（Container Firewall），专注于 Kubernetes 和 Docker 环境的实时网络防护
- **2017年**：发布 **NeuVector 1.0**，提供容器运行时安全、漏洞扫描和合规检查功能

- **2018年**：推出 **自动策略生成（Auto Policy Learning）**，通过行为分析自动构建安全基线
- **2019年**：增强 **CIS Benchmark 合规检查**，帮助企业满足金融、医疗等行业监管要求
- **2020年**：发布 **NeuVector 4.0**，新增 **零信任网络微隔离（Zero Trust Micro-Segmentation）** 功能
- **2021年**：**SUSE（全球领先的开源软件公司）宣布收购 NeuVector**，以增强其 Kubernetes 安全能力
- **2022年**：NeuVector **完成开源**，成为业界首个端到端的开源容器安全平台，同年发布 **NeuVector 5.0**
- **2023年**：新增 **AI 驱动的异常检测**，减少误报率



## 功能特性

NeuVector 提供强大的端到端容器安全平台。这包括对容器、Pod 和主机的端到端漏洞扫描和完整的运行时保护，包括：

- CI/CD 漏洞管理和准入控制，使用 Jenkins 插件扫描镜像、扫描注册表并强制实施准入控制规则以将其部署到生产环境中
- 违规保护，发现行为并创建基于白名单的策略来检测违反正常行为的行为
- 威胁检测，检测容器上的常见应用程序攻击，例如 DDoS 和 DNS 攻击
- DLP 和 WAF 传感器。检查网络流量以防止敏感数据丢失，并检测常见的 OWASP Top10 WAF 攻击
- 运行时漏洞扫描。扫描注册表、镜像和正在运行的容器编排平台和主机以查找常见 (CVE) 以及特定于应用程序的漏洞
- 合规与审计。自动运行 Docker Bench 测试和 Kubernetes CIS Benchmarks
- 端点/主机安全。检测权限升级，监控主机和容器内的进程和文件活动，并监控容器文件系统的可疑活动
- 多集群管理。从单个控制台监控和管理多个 Kubernetes 集群



## 安全架构

<img src="overview-0.png"  width="800" alt="overview-0.png"/>

- **Controller**：NeuVector的中央管理组件，负责协调整个安全系统，存储所有安全策略和配置信息，也是API的入口
- **Enforcer**：用于安全策略部署下发和执行
- **Manager**：提供 Web UI（仅 HTTPS）控制台
- **All-in-One**：集成了 `Controller` , `Enforcer` 和 `Manager` ，适用于轻量化部署
- **Scanner**：容器镜像漏洞扫描组件
- **Updater**：自动更新 NeuVector 的 CVE 漏洞库