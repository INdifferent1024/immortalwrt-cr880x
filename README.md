# Xiaomi CR880x (IPQ5000) OpenWrt 编译指南

## 路由器信息
- **处理器**: Qualcomm IPQ5000 (IPQ5018)
- **型号**: Xiaomi CR880x (M79) - 适用于 CR8806/CR8808/CR8809
- **固件**: ImmortalWrt 24.10 (基于 OpenWrt)

## 包含的软件包
- UA3F (HTTP User-Agent 修改工具，用于校园网多设备检测绕过)
- LuCI Web 界面
- 常用工具 (ttyd, ddns, upnp, wol 等)
- WiFi 驱动 (ATH10K)

## 使用方法

### 步骤 1: 创建 GitHub 仓库

1. 登录 GitHub 账户
2. 创建新仓库 (New repository)
3. 仓库名称: `immortalwrt-cr880x` (可自定义)
4. 选择 "Public"
5. 点击 "Create repository"

### 步骤 2: 上传配置文件

将以下文件上传到仓库根目录:
- `.github/workflows/build.yml`
- `.config`

### 步骤 3: 触发编译

1. 进入仓库页面
2. 点击 "Actions" 标签
3. 在左侧选择 "Build ImmortalWrt for Xiaomi CR880x"
4. 点击 "Run workflow" 按钮
5. 等待编译完成 (首次约 2-4 小时)

### 步骤 4: 下载固件

1. 编译完成后，点击对应的 workflow 运行
2. 在 "Artifacts" 部分下载固件
3. 解压获取以下文件:
   - `*-squashfs-factory*.bin` - 适用于从原厂固件刷入
   - `*-squashfs-sysupgrade*.bin` - 适用于从 OpenWrt 升级

### 步骤 5: 刷入固件

#### 方法 A: 通过 UBoot 刷入 (推荐)
1. 路由器断电
2. 按住 Reset 按钮通电
3. 等待指示灯变为黄色闪烁
4. 电脑连接路由器 LAN 口
5. 访问 http://192.168.1.1 上传固件

#### 方法 B: 通过 SSH 刷入
```bash
cd /tmp
curl -o firmware.bin <固件URL>
sysupgrade -n firmware.bin
```

## 登录信息
- 地址: http://192.168.1.1
- 用户名: root
- 密码: (无密码，首次登录后建议设置)

## UA3F 配置

固件已预装 UA3F，配置方法:

1. 登录 LuCI
2. 进入 "服务" -> "UA3F"
3. 启用并配置:
   - 服务模式: REDIRECT (推荐)
   - 端口: 1080
   - UA: FFF (默认)
   - 策略: GLOBAL

详细配置请参考: https://sunbk201public.notion.site/UA3F-2a21f32cbb4b80669e04ec1f053d0333

## 注意事项

1. 首次编译时间较长，请耐心等待
2. 编译可能失败，如遇问题请检查 Actions 日志
3. 刷机有风险，请仔细阅读相关教程后再操作
4. 建议先备份原厂固件

## 相关链接

- [Redmi AX3000 ImmortalWrt 项目](https://github.com/kmiit/Redmi_AX3000_immortalwrt)
- [UA3F GitHub](https://github.com/SunBK201/UA3F)
- [OpenWrt for Redmi AX3000](https://github.com/hzyitc/openwrt-redmi-ax3000)
