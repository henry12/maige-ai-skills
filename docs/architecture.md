# 项目结构

采用一个总仓库、多个独立 Skill。按交付任务组织 Skill，不按组件数量拆分 Skill。

## 当前实际目录

```text
maige-ai-skills/
├── README.md                 # 中文入口、当前状态和能力目录
├── LICENSE                   # 当前原创内容的 MIT 许可
├── NOTICE.md                 # 来源与第三方材料边界
├── CONTRIBUTING.md           # 贡献要求
├── CHANGELOG.md              # 已发生的版本变化
├── .gitignore                # 排除密钥、本机状态、缓存、渲染产物
├── .github/
│   ├── ISSUE_TEMPLATE/       # 问题、需求、实际使用反馈
│   └── pull_request_template.md
├── docs/
│   ├── architecture.md       # 本文
│   ├── getting-started.md    # 当前可用性与未来首次成功流程
│   ├── compatibility.md      # 实测环境和证据
│   ├── roadmap.md            # 优先级与进入条件
│   ├── release-checklist.md  # 发布前检查
│   └── animation/           # 动画能力专属文档
│       └── handoff.md       # 给动画实现会话的接入要求
├── skills/
│   └── README.md             # 只登记真正接入的 Skill
├── examples/
│   └── README.md             # 案例展示与证据规范
└── templates/
    └── skill-package.md      # 接入参考，不是可安装 Skill
```

## 动画接入后的目标目录（尚未创建）

```text
skills/maige-animation/
├── SKILL.md                  # 触发条件、输入、流程、输出、边界
├── README.md                 # 人类可读的安装、使用和修改说明
├── references/               # 按需读取的动画和内容指导
├── scripts/                  # 必要的检查、预览、导出入口
└── assets/
    └── remotion-starter/     # 自包含的可运行动画工程
        ├── package.json
        ├── <对应包管理器的锁文件>
        ├── src/
        │   ├── components/  # 可复用组件
        │   └── scenes/      # 场景组合
        ├── public/          # 可公开再分发的素材
        └── examples/        # 独立安装也能运行的最小样例

examples/animation/<case-slug>/
├── README.md                 # 任务、输入来源、运行条件、修改说明
├── input/                    # 获准公开或模拟输入
├── preview/                  # 小体积截图或短预览
└── results.md                # 输出文件链接、版本、验证和人工处理记录
```

上述为目标布局，实际接入时可删去不需要的目录。不创建只有占位文件的空工程。

## 目录职责

- `skills/` 是唯一可安装能力的入口。没有可执行流程时不创建 `SKILL.md`。
- 每个 Skill 的运行依赖和最小样例应在其目录内，或作为明确声明、锁定版本的外部依赖；不隐式依赖仓库根目录、兄弟 Skill 或作者电脑路径。
- 动画组件先放在动画 Skill 内。只有至少两个真实消费者需要共享时，才考虑独立共享包。
- `examples/` 服务展示和复现记录，不能成为安装单个 Skill 后缺失的运行依赖。最小样例以 Skill 内版本为准，案例文档指向它，避免重复维护。
- `templates/` 只存接入规范，不放可被安装器误识别的伪 Skill。
- `docs/` 根目录记录跨 Skill 的项目约定；能力专属的接入、设计和维护文档放入 `docs/<能力>/`，例如 `docs/animation/`。PPT 等能力有实际文档时再创建对应目录。
- 安装和运行所必需的说明仍随对应 Skill 分发；不能依赖用户同时下载 `docs/`。
- 先不创建 `apps/`、`website/`、`packages/` 或通用安装器；需求出现后再增加。

## 版本与交付

筹备骨架不发布可安装版本。首个可运行包通过检查后再建立发布标签，并在发布说明列出每个 Skill 的状态、依赖和变化。早期统一仓库版本；只有发布节奏确实分离后才引入独立版本。

源码、锁文件、小型样例进入 Git；大体积视频和分发压缩包放在对应版本的 Release 中。案例引用固定版本，不依赖会不断改变的主分支结果。
