# AI 平台 / Infra · 工程作品集

这里的仓库围绕一个方向：**把推理服务从 0 搭到能跑、能监控、能发版**，
以及把 AI 能力接进具体场景（游戏、语音、内容生产）时，**如何用工程手段把它关进笼子**。

下面的链接全部可以匿名打开（2026-10-22 复核）。暂不公开的仓库单独列在最后，
标注「可当面演示」——不放打不开的链接。

---

## 仓库索引

### 推理平台与部署

| 仓库 | 内容 |
|---|---|
| **[k3s-vllm-platform](https://github.com/shenlinyou222-ux/k3s-vllm-platform)** | 单节点 k3s GPU 推理平台的部署 / 管理 / 观测。核心是**发布判据工程**：三层验证（日志 / 功能 / 性能）、模型权重 sha256 指纹校验、失败自动回滚。含 6 份一线运维文档与故障速查 |

### 游戏 × AI

| 仓库 | 内容 |
|---|---|
| **[aigc-game-framework](https://github.com/shenlinyou222-ux/aigc-game-framework)** | 让 AI 安全操作游戏的中间层框架。核心是一个**架构约束**：AI 不侵入游戏主循环，只能用受限接口读记忆、下指令，规则用 mini-CEL 数据化。**223 个单元测试**（`pytest tests -q` 实测 223 passed） |
| **[gdgs-rendering-lab](https://github.com/shenlinyou222-ux/gdgs-rendering-lab)** | Godot 4.7.2 + 3DGS 太空战斗 Demo。基于上游开源 MIT 插件做**渲染后端优化**（修复 Compute 后端 7 个缺陷，单场景 3.047→1.247 ms）；J2000 轨道要素解析日食；无人值守 autotest 验收（PASS 日志在 `logs/`） |
| **[npc-dialogue-service](https://github.com/shenlinyou222-ux/npc-dialogue-service)** | 角色对话 NPC 的**数据工程 / 微调 / 评测**管线：语料清洗去重、按连续发言重切对话、LoRA 训练与格式合规评测。不含模型权重与语料全文 |

### 语音

| 仓库 | 内容 |
|---|---|
| **[voice-intent-agent](https://github.com/shenlinyou222-ux/voice-intent-agent)** | 全离线语音意图管线：ASR → 句向量 → kNN 意图 → 执行，**零训练路线**。规则层先于置信度门；新增命令只改 `intent_config.json`，不重训模型 |

---

## 暂不公开的仓库（可当面演示）

| 仓库 | 内容 | 为什么私有 |
|---|---|---|
| ai-infra-lectures | 16 套源码级技术讲义 / 24 份 PDF / **990 页**（vLLM v1 `core/` 全量讲义 13 章 / **234 页** / 13,294 行） | 学习产出，非交付物 |
| rogue-dshrl | 横板动作 Roguelike 的 AI 导演层：模型只读结构化上下文、只写受限指令，经确定性校验器与双缓冲生效 | 未完成度较高 |
| concept-animator | 概念树 JSON → 自包含 HTML 动画讲解页（零第三方依赖，只用 Python 标准库） | 工具链 |
| tech-research-notes | 3DGS / 星图 / AI 资产生成调研 + 论文精读 + 开发日志 | 调研笔记 |
| godot-avatar-skeleton | Godot 4 纯代码人形骨架：部件化换装 + 解析式双骨 IK + 程序化连招 | 小工具原型 |
| job-market-analyzer | 3530 条真实 JD → 技能需求图谱与投递优先级榜单（含合规取舍说明） | 自用工具 |
| graph-slim | 基于 CloudWeGo eino 的自动化测试编排执行器 | 在补齐测试数据前不对外 |

---

## 技术栈

```
云平台 / DevOps   Docker · Kubernetes（Deployment/Service/Probe/GPU 声明式调度）· Jenkins CI/CD
                  Prometheus + Grafana · Linux / Shell
AI 工程           vLLM 部署与压测 · LoRA 微调（PyTorch / unsloth）· Agent 运行时定制
                  3DGS 高斯泼溅管线 · 本地模型服务化（llama.cpp / ONNX）
语言              Python（主力）· GDScript · Shell
数据              SQLite / JSONL · FastAPI
```

---

## 几条贯穿所有仓库的做法

**① 每个结论都要有 benchmark，每个 benchmark 都要有 workload 定义。**
8GB 卡上同一配置跨 session 可差 2 倍。所以速度数字必须做同 session A/B，并写清负载是什么。

**② 主动写边界。**
每个代码仓库的 README 末尾都有「已知边界 / 未完成」一节。被推翻的早期说法保留在文档里，不悄悄删掉。

**③ 数字要有出处。**
`k3s-vllm-platform` 的性能结论附 `benchmarks/results/` 原始输出，`gdgs-rendering-lab` 附 `docs/evidence/` 实测报告。
查不到出处的就标「未核实」。

**④ 测试要能复现。**
`aigc-game-framework` 的 223 个用例在干净环境 `pip install -r requirements.txt && pytest tests -q` 可复跑；
`voice-intent-agent` 的规则回归（`test_arg_clean.py` / `test_rule_search.py` 等）不依赖模型，纯规则可跑。

---

## 关于 AI 辅助

这些仓库的代码与文档均在**大量 AI 辅助**下完成（Claude Code / DeepSeek Harness 等 agent 工具，
协作方式是「人定方向与验收标准，AI 执行与自查，人逐项核对」）。各仓库的 README 也是同样方式产出。

写这一节不是为了免责，而是因为**这就是它真实的工作方式**，而且它解释了这些仓库的一些特征：

- 每个数字都要求有出处，**查不到就标「未核实」**
- 多处被推翻的早期说法保留在「已知边界」里，没有悄悄删掉
- 交付前做过机器核查，修掉过几处把上游库的能力误写成自己成果的表述

> 判断与把关是人做的，AI 承担执行与自查。

---

## 联系

- Email: **3401237685@qq.com**

<sub>这个 README 里的每个数字都对应仓库里可查证的证据。如果发现哪个对不上，欢迎开 issue。</sub>
