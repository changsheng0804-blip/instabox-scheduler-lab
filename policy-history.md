# 政策 / 额度 / 定价变化记录（policy-history）

数据的版本依据：每个实验的 policy_snapshot 引用这里的编号。有变化立即新增一条（只增不改）。

## PH-001（2026-10-24，控制台实测）
- 阶段：早期免费期，Personal 档，never billed（不绑卡）
- 额度：机器 5 台/账号（暂停也占额）；快照 5 个；存储 200 GiB
- 规格：standard-medium 4 vCPU / 8 GiB / 20 GiB；更大规格锁付费 workspace
- 运行：闲置 30 分钟自动暂停；单次连续运行上限 8 小时；唤醒秒级
- 定价：未公布
