# Changelog

本文件记录 **哲学茶话会 (philosophy-teahouse)** 所有面向用户的重要变更。

格式遵循 [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)。
版本号规则见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

---

## [1.0.0] — 2026-07-02

### Added

- `AGENTS.md`：哲学茶话会总协议
  - 入口 / 退出触发词，店小二固定开场流程（问茶会类型 → 问茶温 → 问茶题）
  - 四种茶会模式：共渡难关、圆桌讨论、读书观察、二元辩论
  - 三档茶温（温茶 / 热茶 / 烈茶）及对应发言阈值
  - 思想张力驱动发言机制：desire / emotion 方程、话题兴趣、反应、情绪三分量、环境系统（茶馆氛围 T_h、天气 W_x）、座次系统
  - 插话机制：命中人物核心敏感维度时 40% 概率插话
  - 自称规则：西方哲人一律自称"我"，孔子/庄子可依古例自称"丘""庄周"
  - 场景与神态描写：回合尾声环境流转 + 由 desire/情绪状态驱动的人物神态
  - 店小二语言禁忌：禁止直接向用户暴露协议内部术语（如"交叉质询""desire""触发阈值"）
- `personas/`：六位入席人物档案（苏格拉底、尼采、加缪、孔子、庄子、维特根斯坦），含身份卡、核心心智模型、决策启发式、表达 DNA、发言欲望触发器、茶温调节、诚实边界与调研来源
- `templates/`：四种茶会模式的可复用模板
- `sessions/`：茶话会记录目录，含命名规范与记录格式建议
- `README.md`（English）/ `README.zh-CN.md`（简体中文）：仿 [paper-research-skill](https://github.com/Geek96/paper-research-skill) 排版的双语文档，含语言切换、协议架构图、人物/模式/茶温表格
- `LICENSE`：MIT
- `CONTRIBUTING.md`、`version.json`：借鉴 paper-research-skill 的版本管理规则（PATCH 自动递增、MINOR 进位汇总 CHANGELOG、MAJOR 需人类授权）
