# 使用IPMI在ColoCrossing独立服务器上安装Debian 12系统指南

## 准备工作
1. **登录ColoCrossing后台**  
   - 进入DEVICES页面查看您的独立服务器列表
   - 选择需要安装系统的服务器

2. **启用IPMI功能**  
   - 点击"LIFT MULL ROUTE"并确认
   - IPMI默认有效期为4小时，可通过"RENEW LIFT"延长

👉 [【点击查看】2025年最新 ColoCrossing 优惠码及特价云服务器方案汇总](https://bit.ly/ColoCrossing)

## IPMI连接与配置
1. **获取登录信息**  
   - 服务器开通后会收到包含IPMI登录信息的邮件
   - 也可在账户管理页面查看"WELCOME MESSAGE"获取详细信息

2. **登录IPMI控制台**  
   - 浏览器访问IPMI IP地址
   - 输入账号密码登录
   - 导航至Remote Control > Console Redirection

3. **启动控制台**  
   - 点击Launch Console下载launch.jnlp文件
   - 需安装Java 7U79版本（注意：最新版本不兼容）

## 系统安装步骤
### 1. 挂载安装镜像
- 进入Virtual Media > Virtual Storage
- 选择并挂载Debian 12安装ISO
- 确保点击"Plug in"完成挂载

### 2. 启动到安装界面
- 重启服务器
- 按DEL键进入BIOS（若已有系统）
- 选择"IPMI Virtual Disk 3000"启动项
- 或按F11选择"IPMI Virtual CDROM 3000"

### 3. Debian安装配置
1. **基础设置**  
   - 选择"Install"（非图形安装）
   - 配置语言、区域和键盘布局

2. **网络配置**  
   - 选择网卡eno1（第二个无网络）
   - 手动配置IP信息（参考ColoCrossing提供的网络参数）
   - 将DNS服务器改为8.8.8.8或1.1.1.1

3. **系统设置**  
   - 设置root密码
   - 创建新用户（可选）
   - 配置时区（建议选择UTC）

4. **磁盘分区**  
   - 选择"Guided - use entire disk"
   - 确认分区方案并写入更改

5. **软件选择**  
   - 最小化安装（根据需求可选桌面环境）
   - 安装GRUB引导程序（必须选择"Yes"）

## 完成安装
- 安装完成后卸载ISO镜像
- 重启服务器
- 使用配置的账号密码登录新系统

## 注意事项
- 确保Java版本正确（7U79）
- 网络配置错误会导致安装失败
- 如遇问题可联系ColoCrossing技术支持