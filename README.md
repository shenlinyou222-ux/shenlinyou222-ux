# AI 平台 / Infra · 工程作品集

这里的仓库围绕一个方向：**把推理服务从 0 搭到能跑、能监控、能发版**，
以及把 AI 能力接进具体场景（游戏、岗位分析、内容生产）时，**如何用工程手段把它关进笼子**。

每个仓库都有独立的 `## 已知边界 / 未完成` 一节 —— 写清楚没做到什么，比让读者自己发现要好。

---

## 仓库索引

### 推理平台与 MLOps

| 仓库 | 内容 |
|---|---|
| **[k3s-vllm-platform](https://github.com/shenlinyou222-ux/k3s-vllm-platform)** | 单节点 k3s GPU 推理平台的部署 / 管理 / 观测。核心是**发布判据工程**：三层验证（日志/功能/性能）、模型权重 sha256 指纹校验、失败自动回滚；Jenkins 已跑 34 次构建 / 30 次成功。含 6 份一线运维文档与故障速查 |
| **[ai-infra-lectures](https://github.com/shenlinyou222-ux/ai-infra-lectures)** | 16 套源码级技术讲义 / 24 份 PDF / 983 页。含 vLLM v1 `core/` 全量代码讲义（13 章 / 13,294 行 / 231 页），按源码文件的真实边界切章 |

### 游戏 × AI

| 仓库 | 内容 |
|---|---|
| **[gdgs-rendering-lab](https://github.com/shenlinyou222-ux/gdgs-rendering-lab)** | Godot 4.7.2 + 3DGS 太空战斗 Demo。基于上游开源 MIT 插件做**渲染后端优化**（修复 Compute 后端 7 个缺陷，单场景 3.047→1.247 ms）；J2000 轨道要素解析日食；无人值守 autotest 验收 |
| **[aigc-game-framework](https://github.com/shenlinyou222-ux/aigc-game-framework)** | 让 AI 安全操作游戏的中间层框架。核心是一个**架构约束**：AI 不侵入游戏主循环，只能用受限接口读记忆、下指令，规则用 mini-CEL 数据化（**223 个单元测试全通过**） |
| **[rogue-dshrl](https://github.com/shenlinyou222-ux/rogue-dshrl)** | 横板动作 Roguelike 的 AI 导演层。设计原则：**模型是脑子，不是手** —— 只读结构化上下文、只写受限指令，经确定性校验器与双缓冲生效 |
| **[godot-avatar-skeleton](https://github.com/shenlinyou222-ux/godot-avatar-skeleton)** | Godot 4 纯代码人形骨架原型：部件化换装 + 双骨 IK + 程序化连招 |

### 工具与文档

| 仓库 | 内容 |
|---|---|
| **[job-market-analyzer](https://github.com/shenlinyou222-ux/job-market-analyzer)** | 把 3530 条真实 JD 归一化后做**技术栈需求统计**与**加权匹配打分**，产出投递优先级榜单。含合规取舍说明（源 47 个脚本中主动排除 37 个） |
| **[concept-animator](https://github.com/shenlinyou222-ux/concept-animator)** | 概念树 JSON → 自包含 HTML 动画讲解页。零第三方依赖，只用 Python 标准库 |
| **[tech-research-notes](https://github.com/shenlinyou222-ux/tech-research-notes)** | 3DGS / 星图 / AI 资产生成调研 28 篇 + 8 篇论文精读 + AIGC 游戏设计与开发日志 |

---

## 技术栈

```
云平台 / DevOps   Docker · Kubernetes (Deployment/Service/Probe/GPU 声明式调度) · Jenkins CI/CD
                  Prometheus + Grafana · Linux/Shell
AI 工程           vLLM 部署与压测 · LoRA 微调 (PyTorch/unsloth) · Agent 运行时定制
                  3DGS 高斯泼溅管线 · 本地模型服务化
语言              Python（主力）· Go · TypeScript · GDScript · Shell · SQL · C/C++（了解）
数据 / 后端       MongoDB · Redis · MySQL · FastAPI / Flask · RESTful API
```

---

## 几条贯穿所有仓库的做法

**① 每个结论都要有 benchmark，每个 benchmark 都要有 workload 定义。**
8GB 卡上同一配置跨 session 可差 2 倍。所以速度数字必须做同 session A/B，并写清负载是什么。

**② 主动写边界。**
所有仓库的 README 末尾都有「已知边界 / 未完成」一节。被推翻的早期说法保留在文档里，不悄悄删掉。

**③ 数字要有出处。**
`k3s-vllm-platform` 的性能结论附 `benchmarks/results/` 原始输出，`gdgs-rendering-lab` 附 `docs/evidence/` 实测报告。
查不到出处的就标「未核实」。

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
