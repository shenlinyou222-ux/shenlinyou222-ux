# 👋 申淋友 / Shen Linyou

**AI 平台 / Infra 工程师** —— 云平台工程与质量体系出身，正在往 AI 基础设施方向做深度工程实践。

> 我的定位是「**既懂测试质量体系，又能碰 AI 基础设施**」：
> 能把一个服务从 0 搭到能跑、能监控、能发版，并且**坚持每个结论都要有可复现的证据**。
> 不写自己没有亲手跑过的数字。

---

## 🔧 在做什么

目前在做三件事：

**1. 单节点 GPU 推理平台（k3s + vLLM）**
在 8GB 单卡上跑生成式 LLM、向量服务与语音识别三个推理服务，配一整套「推送即部署」的发布系统。
重点不在「我跑了 vLLM」，而在**发布判据工程**：三层验证、模型权重指纹校验、失败自动回滚，以及踩过的几个会静默失败的坑。

**2. 游戏 × AI 的技术验证**
用 Godot 做可玩的 Demo，把 3DGS 高斯泼溅做成可碰撞的场景、把模型塞进游戏决策链路（**模型只写受限指令，由确定性校验器裁决**）。

**3. 源码级技术讲义**
对着真实源码写讲义，把关键文件按「机制 → 代码 → 为什么这样设计」重排。目前已积累 16 套 / 983 页。

---

## 📌 代表仓库

| 仓库 | 一句话 |
|---|---|
| **[k3s-vllm-platform](https://github.com/shenlinyou222-ux/k3s-vllm-platform)** | 单节点 GPU 推理平台的部署 / 管理 / 观测。含三层发布判据、模型权重 sha256 指纹校验、失败自动回滚；Jenkins 已跑 34 次构建 / 30 次成功 |
| **[gdgs-rendering-lab](https://github.com/shenlinyou222-ux/gdgs-rendering-lab)** | Godot 太空战斗 Demo。自研 3DGS 管线（splat 解码 → GPU 体素化 → 网格化，让高斯点场景可碰撞）；无人值守 autotest 验收通过 |
| **[ai-infra-lectures](https://github.com/shenlinyou222-ux/ai-infra-lectures)** | 16 套源码级讲义 / 24 份 PDF / 983 页，含 vLLM v1 `core/` 全量代码讲义（13 章 / 231 页） |
| **[rogue-dshrl](https://github.com/shenlinyou222-ux/rogue-dshrl)** | Godot 横板动作 Roguelike。AI 导演层设计原则：**模型是脑子，不是手**——只读结构化上下文、只写受限指令，经确定性校验器生效 |
| **[tech-research-notes](https://github.com/shenlinyou222-ux/tech-research-notes)** | 3DGS / 星图 / AI 资产生成调研 28 篇 + 8 篇论文精读 + AIGC 游戏设计文档 |
| **[concept-animator](https://github.com/shenlinyou222-ux/concept-animator)** | 概念树 JSON → 自包含 HTML 动画讲解页 |

---

## 🧰 技术栈

```
云平台 / DevOps   Docker · Kubernetes (Deployment/Service/Probe/GPU 调度) · Jenkins CI/CD
                  Prometheus + Grafana · Linux/Shell
AI 工程           vLLM 部署与压测 · LoRA 微调 (PyTorch/unsloth) · Agent 运行时定制
                  3DGS 高斯泼溅管线 · 本地模型服务化
语言              Python（主力）· Go · TypeScript · GDScript · Shell · SQL · C/C++（了解）
数据 / 后端       MongoDB · Redis · MySQL · FastAPI / Flask · RESTful API
```

---

## 📐 我信奉的两条工程纪律

**① 每个结论都要有 benchmark，每个 benchmark 都要有 workload 定义。**
8GB 卡上同一配置跨 session 可差 2 倍。所以任何速度数字都必须做同 session A/B，并且写清负载是什么。

**② 主动写边界。**
我的每个仓库 README 末尾都有「已知边界 / 未完成」一节。把没做到的事写清楚，比让读者自己发现要好——而且这本来也是工程的一部分。

---

## 📫 联系

- Email: **3401237685@qq.com**
- 简历 PDF：见 [个人主页](https://github.com/shenlinyou222-ux/shenlinyou222-ux) 或直接邮件索取

---

<sub>这个 README 里的每个数字都对应仓库里可查证的证据。如果你发现哪个数字对不上，欢迎开 issue —— 那说明我写错了。</sub>
