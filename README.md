# v2rayN (zergfff 定制优化版)

基于 [2dust/v2rayN](https://github.com/2dust/v2rayN) 的 Windows x64 定制版，针对性能精简。

## 与原版的差异

### 性能优化
- **ReadyToRun 预编译** — 冷启动 ~0.6s（原版 ~5.4s）
- **TieredPGO** + Workstation GC
- **SQLite WAL** 模式 + NORMAL 同步 + 20MB 页缓存
- **TCPing 全量并发**（取消分批）
- **真连接测速批间延迟 1s → 100ms**
- **日志截断**：超限保留最近一半，后台长跑内存不涨
- **统计服务空闲降频**：核心未运行时空转 1s → 5s
- **迁移任务/建表并行化**，不阻塞启动

### 功能裁剪
- ❌ 订阅功能（分组胶囊、订阅菜单、导入订阅URL）—— 节点用剪贴板批量导入或手动添加
- ❌ 帮助 / 推广菜单
- ❌ 程序自更新（防止覆盖定制版）
- ✅ **内核更新保留**（sing-box / xray 等仍可在检查更新里升级）

## 使用

从 [Releases](https://github.com/zergfff/v2rayN/releases) 下载 zip，解压后把 `v2rayN.exe` 和 4 个 dll 放进你的 v2rayN 目录（或直接解压到空目录使用），需要 `bin/sing_box/sing-box.exe` 等核心文件。

节点导入：复制 vmess://vless://trojan://ss://hy2:// 链接后在主界面按 Ctrl+V。

## 自动构建

推送到 master 自动触发 GitHub Actions 编译 win-x64 R2R 版本并发布到 Releases（保留最近 3 个）。

本地编译：
```bash
dotnet publish v2rayN/v2rayN.Desktop/v2rayN.Desktop.csproj -c Release -r win-x64
```

## License

GPL-3.0（继承自上游）
