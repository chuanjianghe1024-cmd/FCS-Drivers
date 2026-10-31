# FCS Releases

FluentControl 配套固件与网关的公开发行入口。仓库仅保留本说明；固件、安装包、恢复包、补丁及校验文件全部作为 Release 附件发布，开发源码继续私有。

Public firmware and gateway distribution for FluentControl. This repository keeps only this README; firmware, installers, recovery packages, patches and checksums are Release assets. Development sources remain private.

[发行列表 / Releases](https://github.com/chuanjianghe1024-cmd/FCS-Releases/releases) · [FC](https://github.com/chuanjianghe1024-cmd/FluentControl) · [硬件模型 / Hardware models](https://github.com/chuanjianghe1024-cmd/fc-sensor-models)

**当前仅完成发行仓库初始化，尚无可下载的正式固件。下列版本及文件名均为规则示例，不代表已经发布。**

**The distribution repository is initialized; no production firmware is available yet. Versions and filenames below are naming examples, not published releases.**

## 短名称 / Short names

按功能、形态或稳定特征命名，不把主控、传感器列表、接线、日期堆进文件名。名称用短小写英文词，尽量一个词；品牌展示可用首字母大写。同一名称一旦发布，就固定指向同一产品系列，不复用于无关硬件。

Name products by function, form or a stable characteristic. Do not concatenate MCUs, sensor lists, pin assignments or dates. Prefer one short lowercase English word; capitalize it for display. Once released, a name identifies a stable product family and must not be reused for unrelated hardware.

| 名称 / Name | 定位 / Purpose | 文件示例 / Example asset |
|---|---|---|
| **Lux** (`lux`) | 当前环境光传感器固件 / Current ambient-light sensor firmware | `lux-v0.1.0.zip` |
| **Gateway** (`gateway`) | 独立网关发行系列 / Standalone gateway distribution family | `gateway-v0.1.0-win-x64.zip` |

Lux 当前目标是 ESP32-C3 SuperMini + BH1750/GY-302；这只是产品目标，不代表完整固件已完成实机验收。具体板型、闪存和固件基础版本由对应 Release 与包内清单明确限定，不凭名称推断兼容。

Lux currently targets ESP32-C3 SuperMini + BH1750/GY-302. This identifies the target, not completed hardware acceptance. Each Release and package manifest must specify exact board revisions, flash requirements and runtime/base firmware; the name alone does not establish compatibility.

## 版本与附件 / Versions and assets

- 版本为 `主.次.修订`：不兼容的协议、配置或安装/升级变化升主版本；兼容的新功能升次版本；兼容修复升修订号。升前一位时后位归零。开发阶段从 `0.1.0` 起，首个满足明确验收范围的稳定版再用 `1.0.0`；0.x 的不兼容变更升次版本并明确说明。
  
  Use `major.minor.patch`: bump major for incompatible protocol, configuration or install/upgrade changes; minor for compatible features; patch for compatible fixes. Reset lower components when bumping. Begin development at `0.1.0`; use `1.0.0` for the first stable release meeting its stated acceptance scope. During 0.x, bump minor for breaking changes and document them.

- Release 标题：`Lux v0.1.0`；Git tag：`lux/v0.1.0`；默认附件：`lux-v0.1.0.zip`。各产品独立编号，不与 FC 桌面端或外壳版本强行同步。
  
  Release title: `Lux v0.1.0`; Git tag: `lux/v0.1.0`; default asset: `lux-v0.1.0.zip`. Products version independently from the FC desktop app and enclosure revisions.

- 初装/恢复尽量放在一个完整包中，避免重复文件；确需单独产物才加短后缀，如 `lux-v0.1.0-recovery.bin`。扩展名必须匹配真实格式，不能把 Python 包改成 .bin。
  
  Prefer one complete package for installation/recovery. Add a short suffix only for a genuinely separate artifact, such as `lux-v0.1.0-recovery.bin`. Extensions must match real formats; a Python package cannot simply be renamed .bin.

- 测试版用 `v0.2.0-rc.1`，GitHub 标记 Pre-release；正式版不带测试后缀。文件名用连字符和点，不使用空格、中文或日期。
  
  Use `v0.2.0-rc.1` for a release candidate and mark it as a GitHub prerelease. Stable versions have no prerelease suffix. Use hyphens and dots, not spaces, Chinese characters or dates in filenames.

- 一版只修了问题，也发布新修订号和完整包，不覆盖旧附件。只有确有增量更新机制时才发布补丁，例如 `lux-v0.1.1-patch.zip`；简介与清单必须列允许的源版本、目标版本及恢复办法。
  
  Publish a new patch version and full package for fixes; never overwrite old assets. Only provide an incremental patch when an actual patch mechanism exists, e.g. `lux-v0.1.1-patch.zip`. Notes and manifest must identify allowed source versions, target version and recovery procedure.

- 同功能有不兼容硬件变体时，不能都叫同一个下载文件。优先让一个包带明确选择/识别机制；否则分配短且永久的变体别名，如 `lux-mini`、`lux-pro`（仅举例，不能暗示未实现功能），分别编号。平台/架构仅在网关等确实需要区分时加后缀。
  
  Incompatible hardware variants must not share an ambiguous download name. Prefer one package with explicit selection/identification; otherwise assign short permanent aliases such as `lux-mini` or `lux-pro` (examples only, not feature claims), with independent versions. Add platform/architecture suffixes only where needed, such as gateway binaries.

## 每版简介与清单 / Release notes and manifest

接线在硬件定型时确定，发行说明与包内清单不重复记录；相关资料由开发或装配文档维护。

Wiring is fixed when the hardware design is finalized and is not repeated in Release notes or package manifests; development or assembly documentation maintains those details.

每个 Release 用中英双语简介，写清以下信息；包内 `manifest.json` 保留相同兼容数据供工具读取。不要在仓库根目录另存每版文件。单个裸固件无法内含清单时，作为同版附件提供产品专属清单。

Use bilingual Release notes with the following information, and repeat compatibility data in a package-level `manifest.json` for tooling. Do not keep per-version files in the repository tree. For a bare firmware image, provide a product-specific manifest as a sibling Release asset.

| 内容 / Field | 要求 / Requirement |
|---|---|
| 功能 / Function | 用途、实际支持功能 / Purpose and implemented capabilities |
| 硬件 / Hardware | 主控、精确板型/硬件修订、传感器、闪存要求 / MCU, exact board/revision, sensors, flash requirements |
| 依赖与兼容 / Dependencies | 基础固件/运行时、协议及已验证的 FC/FCS 范围 / Base firmware/runtime, protocol and tested FC/FCS range |
| 安装与升级 / Install and upgrade | 初装、升级、保留/清除配置、恢复；补丁源版本 / First install, upgrade, configuration retention/reset, recovery and patch source versions |
| 验证 / Validation | 实测设备、已测/未测项及限制 / Tested hardware, completed/pending checks and limitations |
| 来源与完整性 / Provenance | 私有构建的可追溯编号、产物版本、SHA-256 / Traceable private build identifier, artifact version and SHA-256 |
| 使用条款 / Terms | 该产物的许可证或分发条款 / Artifact-specific license or distribution terms |

只上传审核过的发行产物和 `SHA256SUMS.txt`，不上传源码归档、凭据、个人配置或内部日志。发行仓库的 tag 只标记公开发布记录，真实构建来源单独追踪；GitHub 自动生成的 Source code ZIP/TAR 只包含本说明，不是固件。发布包若包含 .py，它本身就是可见代码，必须在发布前确认范围。

Upload only reviewed release artifacts and `SHA256SUMS.txt`, not source archives, credentials, personal configuration or internal logs. Tags in this distribution repository identify public release records; track the actual build source separately. GitHub's automatically generated Source code ZIP/TAR contains this README, not firmware. Any .py files included in a package are visible code and must be reviewed for publication.

多产品共享本仓库时不要把全局 Latest 当成每个产品的最新版；按产品 tag 前缀查找对应稳定版。已发布标签和附件不可改写；更新使用新版本。公开下载不自动授予商业使用权，以每版实际附带条款为准。

For multiple products, do not interpret the repository-wide Latest as the latest version of every product; select stable releases by product tag prefix. Never rewrite published tags or assets; publish a new version. Public download does not itself grant commercial-use rights; consult the terms shipped with each release.
