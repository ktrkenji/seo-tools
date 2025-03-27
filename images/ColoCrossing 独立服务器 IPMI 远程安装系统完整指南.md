# ColoCrossing 独立服务器 IPMI 远程安装系统完整指南

## 一、准备工作：获取IPMI访问权限

1. **登录ColoCrossing控制面板**  
   通过客户后台查看IPMI信息（也可在服务开通邮件中找到）
   
2. **检测IPMI网络连通性**  
   - 在浏览器输入IPMI地址测试访问
   - 若出现网段冲突，需按提示配置空路由

👉 [【点击查看】2025年最新 ColoCrossing 优惠码及特价云服务器方案汇总](https://bit.ly/ColoCrossing)

## 二、配置IPMI连接环境

### 1. Java环境配置
- 下载推荐版本：Java 8U333（新版可能不兼容）
- 安装后配置安全例外：
  1. 打开Java控制面板
  2. 在"安全"选项卡添加IPMI地址到例外列表

### 2. 连接IPMI控制台
- 通过浏览器访问IPMI地址
- 下载IPMI连接配置文件（.jnlp格式）
- 使用下载的配置文件启动控制台

## 三、系统安装实战步骤

### 方法一：ISO镜像安装
1. **挂载安装镜像**：
   - 推荐使用netboot.xyz工具（解决国外服务器下载慢问题）
   - 在IPMI控制台选择"Virtual Media"挂载ISO

2. **设置启动项**：
   - 重启服务器
   - 按F11进入启动菜单
   - 选择CDROM启动

### 方法二：网络安装（推荐）
bash
# 当出现无IP分配时手动输入：
IP: 您的服务器IP
网关: 对应网关
子网掩码: 255.255.255.0

## 四、系统配置优化

1. **首次登录**：
   - 使用安装时创建的用户凭证SSH登录
   - 通过`su`命令切换root权限

2. **DD系统（可选）**：
bash
wget --no-check-certificate -qO InstallNET.sh 'https://raw.githubusercontent.com/leitbogioro/Tools/master/Linux_reinstall/InstallNET.sh' && chmod a+x InstallNET.sh
bash InstallNET.sh -debian 11

## 五、常见问题解决

- **IPMI连接失败**：检查Java版本和防火墙设置
- **网络安装卡顿**：建议选择离机房较近的镜像源
- **启动项问题**：在BIOS中设置CDROM为第一启动项

> 提示：ColoCrossing独立服务器支持多种操作系统安装，建议根据实际需求选择最适合的安装方式。