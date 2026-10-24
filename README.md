# fleet-dispatch

多智能体共享的机队调度层：规则、注册表、工具、测试与经验。

## 为什么有这个仓库

主人 2026-10-24 的定性：

> 5 台机器本身不算什么有价值的资源，能把这 5 台（乃至将来更多）机器充分利用和调度起来的**调度层**才是最有价值的资源。现在是 Tibo 专用，将来多个云端智能体交替使用、协调使用，才能把硬件价值最大发挥，而前提就是调度规则和调度层的设计。

机器会增减、平台会变价、规格会过时；调度规则、实测数据和经验教训不会。本仓库沉淀的就是后者。

## 现有家底

- 机队：5 台 InstaBox（Personal 免费档），每台 4 vCPU / 8 GiB / 20 GiB，见 `registry/machines.yaml`
- 分工与利用方案：`~/workspace/guides/instabox-utilization-plan.md`（本仓是它的执行层）
- 上新服务的安全检查表：`~/workspace/guides/instabox-new-service-checklist.md`（往任何一台加服务前必过）

## 仓库结构

- `docs/DISPATCH_RULES.md` — 调度规则 v0.1（准入、分派、生命周期、多智能体协调、安全边界）
- `registry/machines.yaml` — 机器注册表（只记元数据，**令牌值永不入仓**）
- `tools/pool` — 调度工具：status / run / fanout / wake，经 Mac 两跳 SSH 派活
- `TESTPLAN.md` — 组合测试计划（心跳轮转执行）
- `EXPERIENCE.md` — 经验库：cue / lesson / evidence / confidence，可复用的教训才进
- `ledger/` — 调度台账与测试结果（`LEDGER.md` 流水、`results/` 每轮测试记录、rotation.txt 轮转指针）
- `AGENT_INSTRUCTIONS.md` — 给其他智能体的接入说明（怎么认领机器、怎么记录、边界在哪）

## 谁在维护

Tibo 以心跳（约每 2 小时一轮）轮转执行组合测试、更新台账与经验库、无事不打扰主人。其他智能体接入前先读 `AGENT_INSTRUCTIONS.md` 与 `docs/DISPATCH_RULES.md`。

## 协议与最近动态

本仓自 2026-10-24 起执行《InstaBox 调度层实验协议》v1.1（见 PROTOCOL.md）：双账号（两名云端智能体各绑一账号）并行测试、配对复制、结论只引用实验编号、最终交付 scheduler-spec.md。本仓为其中一个账号的仓库，另一智能体的仓库独立维护，双方通过公开仓库互读 CLAIMS 与结论防重复。

最近动态：
- 2026-10-24：协议 v1.1 落仓；仓库结构对齐协议；心跳改为约每小时一轮（流程按协议第 7 节）；本仓账号标签待人类指定（A/B）。
- 2026-10-24：协议前基线完成（5 台打通、并行冒烟、T1 暖态唤醒数据），见 ledger/。
