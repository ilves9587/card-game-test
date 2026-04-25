# Godot 4.6 通用项目基座

一个基于 **Godot Engine 4.6** 的标准化项目模板，集成了完整的Git版本控制和Git LFS大文件管理。本项目作为通用开发基座，可在此基础上快速拓展开发各类2D、3D及混合渲染游戏项目。

## 技术栈

### 核心引擎
- **Godot Engine 4.6** - 跨平台游戏引擎，支持2D/3D无缝混合渲染

### 资源开发工具链
- **美术生成**：支持各类主流AI绘画工具
- **精灵与动画**：支持各类精灵表生成与动画制作工具
- **音频生成**：支持各类AI音频生成工具
- **关卡与数据生成**：支持各类程序化生成工具

### 版本控制工具
- **Git + Git LFS** - 分布式版本控制系统与大文件存储

## 项目结构

```
your-project-name/
├── .godot/              # Godot编辑器缓存（自动生成，不纳入版本控制）
├── .gitattributes       # Git LFS配置文件
├── .gitignore           # Git忽略文件
├── README.md            # 项目说明文档
├── project.godot        # Godot项目核心配置文件
│
├── addons/              # Godot插件与第三方扩展
│
├── scripts/             # 脚本代码目录
│   ├── autoload/        # 全局单例与启动初始化脚本
│   ├── core/            # 核心系统模块
│   ├── gameplay/        # 玩法逻辑脚本
│   └── ui/              # UI交互逻辑
│
├── scenes/              # 场景文件目录
│   ├── main/            # 主场景与入口场景
│   ├── levels/          # 关卡与地图场景
│   ├── characters/      # 角色与可交互对象场景
│   └── ui/              # UI组件场景
│
├── assets/              # 资源文件目录（Git LFS管理）
│   ├── raw/             # 原始美术源文件与设计稿
│   ├── textures/        # 纹理与UI素材
│   ├── sprites/         # 精灵表与动画资源
│   ├── audio/           # 音频资源
│   │   ├── voices/      # 语音资源
│   │   ├── sfx/         # 音效资源
│   │   └── bgm/         # 背景音乐
│   ├── models/          # 3D模型资源
│   └── shaders/         # 自定义着色器资源
│
├── data/                # 游戏数据目录
│   ├── config/          # 全局配置文件
│   ├── tables/          # 数值表与静态配置表
│   └── localization/    # 本地化文本与语言包
├── docs/                # 文档目录
│   ├── architecture.md  # 技术架构文档
│   ├── changelog.md     # 版本变更记录
│   └── design/          # 设计文档目录
│
├── builds/              # 导出的游戏构建（不纳入版本控制）
└── tools/               # 辅助工具脚本
```

### 结构设计说明

- `scenes/` 用于存放可实例化的关卡、角色、UI等场景资源，避免把关卡场景混放到 `data/`
- `scripts/` 用于放置可复用脚本；如果某个脚本只服务于单一场景，也可就近放在对应场景目录旁
- `autoload/` 建议用于事件总线、配置管理、存档管理等全局单例，并在 `project.godot` 中注册
- `addons/` 与 `.godot/` 是Godot项目中的常见目录：前者需要纳入版本控制，后者通常应忽略
- `assets/raw/` 保存源文件，`assets/textures`、`assets/sprites`、`assets/models` 等保存可直接进入项目的运行时资源

## 快速开始

### 环境准备

1. **安装Godot Engine 4.6**
   - 从[Godot官网](https://godotengine.org/download/)下载对应系统版本（推荐Apple Silicon/Intel原生版本）
   - 或使用Homebrew安装：`brew install --cask godot`

2. **安装Git与Git LFS**
   - 安装Git：`brew install git`（macOS）或下载[Git安装包](https://git-scm.com/downloads)
   - 安装Git LFS：`brew install git-lfs`（macOS）或下载[Git LFS安装包](https://git-lfs.com/)
   - 初始化Git LFS：`git lfs install`

### 项目设置

1. **克隆仓库**
   ```bash
   git clone https://github.com/your-username/your-project-name.git
   cd your-project-name
   ```

2. **打开项目**
   - 启动Godot Engine
   - 点击"导入"按钮，选择项目根目录下的`project.godot`文件
   - 点击"打开"进入编辑器

3. **验证配置**
   - 运行主场景（F5键）确认项目正常启动
   - 检查Git状态：`git status`，确保没有未跟踪的临时文件
   - 确认 `.godot/` 与 `builds/` 未被提交到版本控制

## 开发规范

### 代码规范
- 使用**GDScript 2.0**编写脚本
- 类名使用**PascalCase**（如`PlayerController`）
- 函数名和变量名使用**snake_case**（如`update_position`）
- 常量使用**UPPER_SNAKE_CASE**（如`MAX_HEALTH`）
- 每个函数添加简短的功能注释
- 复杂逻辑块添加行内注释说明

### 资源规范
- 所有资源使用**小写字母+下划线**命名（如`button_hover.png`）
- 资源文件按类型和用途分类存放
- 可运行场景资源优先放在`scenes/`，纯配置与静态表优先放在`data/`
- 所有资源需经过审核和优化后再入库
- 大文件（>1MB）自动由Git LFS管理

### 提交规范
- 提交信息格式：`类型: 简短描述`
- 类型包括：`feat`（新功能）、`fix`（修复）、`docs`（文档）、`style`（格式）、`refactor`（重构）、`test`（测试）、`chore`（构建/工具）
- 示例：`feat: 添加基础UI框架`、`fix: 修复场景切换时的内存泄漏`

## Git与版本控制

### 分支管理
- `main`：主分支，始终保持稳定可运行状态
- `develop`：开发分支，日常开发在此分支进行
- `feature/xxx`：功能分支，用于开发新功能
- `hotfix/xxx`：热修复分支，用于修复线上问题

### Git LFS使用说明
本项目已配置Git LFS自动管理以下类型的大文件：
- 图片文件：`.png`, `.jpg`, `.jpeg`, `.psd`, `.bmp`
- 音频文件：`.mp3`, `.wav`, `.ogg`, `.flac`
- 3D模型文件：`.glb`, `.gltf`, `.fbx`, `.obj`
- 视频文件：`.mp4`, `.webm`, `.mov`

**注意**：首次克隆仓库后，Git LFS会自动下载所有大文件。如果下载失败，可手动执行：
```bash
git lfs pull
```

## 资源开发指南

### 美术资源
- 概念设计与原画可使用任意工具生成
- 纹理素材建议导出为PNG格式，带透明通道
- 精灵表建议使用统一的网格尺寸和间距
- 3D模型建议导出为GLB格式，包含必要的材质信息

### 音频资源
- 音效建议导出为WAV或OGG格式
- 背景音乐建议导出为MP3或OGG格式
- 语音资源建议导出为MP3格式，采样率44.1kHz

### 数据资源
- 配置文件建议使用JSON或CSV格式
- 关卡主体建议使用Godot场景（`.tscn`）组织；纯数值、刷怪表、对话表等再拆分到`data/`
- 可复用配置资源可优先考虑Godot原生的`.tres`或`.res`格式
- 所有数据文件需保持结构清晰，便于维护

## 部署与导出

### 导出配置
1. 在Godot编辑器中打开"项目"->"导出"
2. 点击"添加"选择目标平台
3. 配置导出选项（推荐使用默认优化设置）
4. 点击"导出项目"，选择导出目录为`builds/`

### 支持平台
- macOS
- Windows
- Linux
- Web (HTML5)
- Android
- iOS

## 贡献指南

1. 从`develop`分支创建新的功能分支：`git checkout -b feature/your-feature-name`
2. 在功能分支上进行开发和提交
3. 完成后提交Pull Request到`develop`分支
4. 代码审核通过后合并到`develop`分支
5. 定期将`develop`分支合并到`main`分支发布新版本

## 许可证

本项目采用 [MIT License](LICENSE) 开源协议。

---

*本项目模板最后更新于：2026年4月*
