# 调度台账

一行一件事：时间（CST）/ 智能体 / 机器 / 事项 / 结果。claim 也记在这里，结单时补结果。

| 时间 | 智能体 | 机器 | 事项 | 结果 |
|---|---|---|---|---|
| 2026-10-24 15:20 | muse | 全部 | 额度盘点（控制台实测） | 机器 1/5、快照 0/5、存储 1.8/200 GiB |
| 2026-10-24 15:54 | muse | pool-1~4 | 建机（standard-medium） | 5/5 全部 Running |
| 2026-10-24 16:12 | muse | pool-1~4 | 建令牌 tibo-pool-N 并逐台登录验证 | 全部通过，令牌只存 Mac |
| 2026-10-24 16:15 | muse | pool-1~4 | 并行冒烟：同一计算任务 fanout | 各约 0.1s，总墙钟约 2s |
| 2026-10-25 00:28 | muse-heartbeat | pool-1~4 | T1 唤醒延迟矩阵 claim（预计 <20 分钟） | 部分完成：暖态 connect 1.6–1.8s 已记，冷样本作废（轮前 23:56–58 已有探活），详见 results/2026-10-25-T1.md |
| 2026-10-25 00:29 | muse-heartbeat | 全部 | T0 基线巡检（只读） | 5/5 可达；my-cloud-pc up 1 天；pool-1~4 up 31–33 分钟、load 0、根盘 11G、connect 1.7–1.8s |
| 2026-10-25 00:30 | muse-heartbeat | — | 修 tools/pool wake 不打印 connect 行（内层 ssh 吞 stdin） | 已修（加 < /dev/null）并验证，5 台均出 connect 行 |
| 2026-10-25 00:35 | muse-heartbeat | — | 待推送：Mac 本地提交未推上 GitHub | Mac commit 已成，git push 失败（SSH 会话读不到 github 凭据：could not read Username）；不反复重试、不改凭据配置，待主人本地操作或后续轮次再推 |
