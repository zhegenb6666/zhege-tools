# 哲哥工具 · ZhegeTools

Android 液态玻璃风格的工具聚合 App（中文）。

- 包名 `com.zhege.tools`，minSdk 24（Android 7.0+），targetSdk 34
- 9 个功能：QQ 免费机器人、加入官方、QQ 群短链接、网易云音乐、网页测速、快手无水印、抖音无水印、免费 AI 集合、2 元 TG 号

## 安装

从 [Releases](../../releases) 下载最新 `ZhegeTools-v*.apk` 安装即可。

首次安装若提示「未知来源」，按系统引导给本 App 开一次「允许安装未知应用」权限。

## 自动更新

App 每次启动会读取仓库根目录的 [`version.json`](/version.json)，
用其中的 `versionCode` 与本地比较；有新版时弹出**强制更新**窗口，
点「立即更新」后台下载 APK 并自动调起安装。

版本信息来源（并行查询，取最大的 `versionCode`）：

1. `raw.githubusercontent.com`
2. `cdn.jsdelivr.net/gh/...`
3. `ghfast.top` 加速镜像

> 之所以查多个源并取最大值：`raw.githubusercontent.com` 的 CDN 缓存很顽固，
> 提交新版本后一段时间（加 `?t=` 参数也无效）仍可能返回旧内容，
> 只认一个源会把新版本「藏起来」。

## 发布新版本（维护者）

1. 改两处且**必须一致**：
   - `app/build.gradle.kts` 的 `versionCode` / `versionName`
   - `app/src/main/java/com/zhege/tools/Net.kt` 里的 `Cfg.VERSION_CODE` / `Cfg.VERSION`
2. 出包（zipalign → apksigner，签名需 v2/v3）
3. 在 GitHub 发 Release：tag 用 `v<版本名>`，上传 APK 资产
4. 更新仓库根目录 `version.json`：

```json
{
  "version": "1.0.2",
  "versionCode": 3,
  "url": "https://github.com/zhegenb6666/zhege-tools/releases/download/v1.0.2/ZhegeTools-v1.0.2.apk",
  "urlBackup": "https://ghfast.top/https://github.com/zhegenb6666/zhege-tools/releases/download/v1.0.2/ZhegeTools-v1.0.2.apk",
  "notes": "更新说明",
  "force": true,
  "size": 13401045
}
```

`versionCode` 必须是**严格递增的整数**，否则已安装用户不会被提示更新。

## 注意

仓库是公开的，因为 App 需要匿名读取 `version.json` 和 APK 才能自动更新。
