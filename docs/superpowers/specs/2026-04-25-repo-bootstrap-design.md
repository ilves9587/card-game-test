# 仓库首步落地设计

## 背景

当前仓库只有 `base.md`，已经明确了 Godot 4.6 通用项目模板的目标目录结构，但尚未真正建立目录、约定文件和版本控制规则。本设计用于指导首步落地，使仓库从“结构说明文档”进入“可直接扩展开发的模板骨架”状态。

## 目标

- 按 `base.md` 当前约定建立项目目录骨架
- 新增 `plans/` 目录，用于在仓库内持久记录每次开发计划
- 在根目录与关键一级目录放置精简版 `AGENTS.md`
- 通过相对 Markdown 链接建立目录说明之间的跳转关系
- 补齐更完整的 `.gitignore` 与 `.gitattributes`

## 非目标

- 不创建具体 Godot 场景、脚本或资源内容
- 不在本轮实现 `project.godot`、自动加载配置或导出预设
- 不为所有二级目录铺设 `AGENTS.md`

## 目标目录结构

```text
unity-sample/
├── .gitattributes
├── .gitignore
├── AGENTS.md
├── README.md
├── base.md
├── addons/
├── assets/
│   ├── AGENTS.md
│   ├── audio/
│   │   ├── bgm/
│   │   ├── sfx/
│   │   └── voices/
│   ├── models/
│   ├── raw/
│   ├── shaders/
│   ├── sprites/
│   └── textures/
├── builds/
├── data/
│   ├── AGENTS.md
│   ├── config/
│   ├── localization/
│   └── tables/
├── docs/
│   ├── AGENTS.md
│   ├── design/
│   └── superpowers/
│       └── specs/
├── plans/
│   └── AGENTS.md
├── scenes/
│   ├── AGENTS.md
│   ├── characters/
│   ├── levels/
│   ├── main/
│   └── ui/
├── scripts/
│   ├── AGENTS.md
│   ├── autoload/
│   ├── core/
│   ├── gameplay/
│   └── ui/
└── tools/
```

说明：

- `.godot/` 由 Godot 自动生成，不预创建，也不纳入版本控制
- `builds/` 作为导出产物目录可预留空目录，但应被 `.gitignore` 忽略
- `README.md` 若当前不存在，则一并创建占位文件，避免根结构入口缺失

## AGENTS 放置策略

采用“根目录 + 关键一级目录”的精简方案：

- 根目录：`AGENTS.md`
- 一级目录：`scripts/AGENTS.md`、`scenes/AGENTS.md`、`assets/AGENTS.md`、`data/AGENTS.md`、`docs/AGENTS.md`、`plans/AGENTS.md`

不在本轮新增二级目录 `AGENTS.md`，原因：

- 当前仓库仍处于模板初始化阶段
- 一级目录已经足以表达职责边界和协作入口
- 过早细化到二级目录会带来较高的维护成本

## AGENTS 内容结构

每个 `AGENTS.md` 使用统一结构，便于扫描和后续扩展：

1. 目录用途
2. 当前应放入的内容
3. 不应放入的内容
4. 命名与组织约定
5. 相关目录跳转

### 根 AGENTS

根 `AGENTS.md` 负责提供总导航与跨目录规则，至少包含：

- 仓库定位：Godot 4.6 通用项目基座
- 一级目录导览
- 命名约定总览
- 文档关系说明：
  - 长期设计与架构说明进入 `docs/`
  - 每次开发计划进入 `plans/`
  - 实际实现进入对应功能目录
- 到各一级目录 `AGENTS.md` 的相对链接

### scripts/AGENTS.md

- 说明 `scripts/` 保存可复用脚本和系统逻辑
- 强调 `autoload/` 用于全局单例与初始化脚本
- 说明只服务单一场景的脚本可与场景近邻放置，不强制全部进入 `scripts/`
- 链接到 `../scenes/AGENTS.md` 和 `../AGENTS.md`

### scenes/AGENTS.md

- 说明 `scenes/` 保存 `.tscn` 为主的可实例化资源
- 区分 `main/`、`levels/`、`characters/`、`ui/`
- 强调关卡主体在 `scenes/`，而不是 `data/`
- 链接到 `../scripts/AGENTS.md`、`../data/AGENTS.md` 和 `../AGENTS.md`

### assets/AGENTS.md

- 说明 `raw/` 为源素材，其他目录为可进入项目的运行时资源
- 标明音频、模型、纹理、精灵、着色器的归档位置
- 提醒大文件需遵循 Git LFS 规则
- 链接到 `../data/AGENTS.md` 和 `../AGENTS.md`

### data/AGENTS.md

- 说明 `config/`、`tables/`、`localization/` 的职责
- 强调 `data/` 存放配置和静态表，不承载关卡主场景
- 提醒优先使用结构清晰、可审阅的文本格式，必要时使用 `.tres` 或 `.res`
- 链接到 `../scenes/AGENTS.md` 和 `../AGENTS.md`

### docs/AGENTS.md

- 说明 `docs/` 用于长期保留的架构、设计、变更说明
- 说明 `docs/design/` 与 `docs/superpowers/specs/` 的使用边界
- 链接到 `../plans/AGENTS.md` 和 `../AGENTS.md`

### plans/AGENTS.md

- 说明 `plans/` 用于记录每一次开发计划，并纳入版本控制
- 推荐文件命名格式：`YYYY-MM-DD-<topic>-plan.md`
- 说明计划内容至少包含目标、范围、实施步骤、验证方式
- 说明计划完成后不删除，只随项目演进持续保留
- 链接到 `../docs/AGENTS.md` 和 `../AGENTS.md`

## 跳转链接规则

所有 `AGENTS.md` 使用相对路径链接，避免依赖仓库外环境。

示例：

- 根到脚本说明：`[脚本约定](scripts/AGENTS.md)`
- 脚本回根：`[返回仓库导航](../AGENTS.md)`
- 场景到数据说明：`[查看数据目录约定](../data/AGENTS.md)`
- 文档到计划说明：`[查看计划记录约定](../plans/AGENTS.md)`

链接设计目标：

- 任意一级目录说明都能在 1 次跳转内返回根导航
- 任意强相关目录都能在 1 次跳转内到达彼此说明
- 减少“只知道当前目录，不知道整体结构”的情况

## .gitignore 设计

根目录新增较完整的 `.gitignore`，覆盖以下类型：

- Godot 自动生成目录与缓存：
  - `.godot/`
  - 导入缓存和编辑器临时文件
- 构建产物：
  - `builds/`
  - 常见导出包与压缩产物
- 系统垃圾文件：
  - `.DS_Store`
  - `Thumbs.db`
- 编辑器与 IDE 文件：
  - `.idea/`
  - `.vscode/` 中不应共享的用户级配置
- 日志和临时文件：
  - `*.log`
  - `*.tmp`
  - `*.import`

设计原则：

- 忽略可再生缓存与本地产物
- 保留团队协作所需的项目结构与文档
- 不忽略 `plans/`、`docs/`、`scripts/`、`scenes/` 等源目录

## .gitattributes 设计

根目录新增更完整的 `.gitattributes`，包含两类规则：

### 文本文件规则

- 为 Markdown、GDScript、场景文本、配置文本等启用标准文本处理
- 保持跨平台换行行为稳定

### Git LFS 规则

对以下大文件或二进制资源启用 Git LFS：

- 图片：`*.png`、`*.jpg`、`*.jpeg`、`*.psd`、`*.bmp`、`*.tga`、`*.exr`
- 音频：`*.mp3`、`*.wav`、`*.ogg`、`*.flac`
- 模型：`*.glb`、`*.gltf`、`*.fbx`、`*.obj`、`*.blend`
- 视频：`*.mp4`、`*.mov`、`*.webm`
- 可选源文件：`*.kra`、`*.aseprite`

设计原则：

- 优先把审阅成本高、体积大的二进制资源交给 LFS
- 不把普通脚本、Markdown、JSON、CSV 等文本文件放入 LFS

## 实施步骤

1. 创建根目录占位文件与主目录骨架
2. 创建关键子目录
3. 编写根与一级目录 `AGENTS.md`
4. 创建或补全 `README.md`
5. 写入 `.gitignore`
6. 写入 `.gitattributes`
7. 复核目录是否与 `base.md` 一致
8. 检查 Markdown 文件的链接与可读性

## 验证方式

- 使用目录列表确认目录结构完整
- 抽样检查 `AGENTS.md` 相对链接是否正确
- 检查 `.gitignore` 是否包含 `.godot/` 与 `builds/`
- 检查 `.gitattributes` 是否覆盖图片、音频、模型、视频等典型大文件
- 确认 `plans/` 被纳入版本控制且未被忽略

## 风险与控制

### 风险 1：目录建立后与文档漂移

控制：

- 以 `base.md` 当前结构为主
- 先落地一级目录，不在本轮扩散到更多层级

### 风险 2：AGENTS 过多造成维护成本

控制：

- 本轮仅在根和一级目录放置
- 二级目录按未来实际复杂度再增补

### 风险 3：忽略规则过宽误伤源文件

控制：

- `.gitignore` 只忽略缓存、构建产物和临时文件
- 文本源文件与计划文档保持可追踪
