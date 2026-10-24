# 经验库

格式：cue（触发情境）/ lesson（教训）/ evidence（证据）/ confidence（置信度）。只收可复用的，流水账在 ledger。

## E01 基础设施令牌必须永不过期
- cue: 在控制台给机器建 SSH 令牌时要选有效期
- lesson: 基础设施用途的令牌一律选 Never。会过期的令牌（如机上那把 macbook-ssh）到期即静默锁死入口，且控制台事后显示不出其登录名，无法补救，只能新建
- evidence: 2026-10-24 盘点发现 macbook-ssh 将于 10-27 到期且登录名不可见；tibo-pool-1~4 全部按 Never 建成
- confidence: 高

## E02 BrowserOS 里 act 点击对本应用时灵时不灵，evaluate 点击可靠
- cue: 经 BrowserOS MCP 操作 InstaBox 控制台
- lesson: act kind=click 有时返回 ok 但页面无变化（Create machine / Create token 均遇过）；用 evaluate 执行 DOM click 一次到位。填 React 受控输入要用原生 value setter + input/change 事件，普通 fill 可能静默失效
- evidence: 2026-10-24 建 4 台机器与 4 把令牌全程实测
- confidence: 高

## E03 令牌只在创建瞬间可见，全程在 Mac 本地闭环捕获
- cue: 新令牌的 SSH 命令只在创建后展示，事后不可再查
- lesson: 捕获动作必须在 Mac 本地进程内完成：页面提取 → 直接写 Mac ~/.ssh/config，只回传哈希指纹做核对。令牌值不经过云端、不进聊天与日志
- evidence: 2026-10-24 tibo-pool-1~4 四把令牌均以此法建成并逐台登录验证
- confidence: 高

## E04 云端直连 InstaBox SSH 被掐，必须经 Mac 两跳
- cue: 从 Tibo 云电脑直接 ssh 网关
- lesson: 固定链路 云端→(ts-proxy 3130)→Mac→(别名)→api.instabox.sh:2222。嵌套 ssh 长会话易断，长任务一律目标机 nohup+日志轮询
- evidence: 2026-10-21 起多次实测；邮件中继门巡检 hook 沿用此链稳定运行
- confidence: 高

## E05 并行冒烟基线
- cue: 需要判断 fanout 是否真并行
- lesson: 同一 300 万次开方求和任务，4 台同时跑各约 0.09~0.10 秒，总墙钟约 2 秒（含四路建连），并行链路成立；建连开销是短任务的主要成本
- evidence: 2026-10-24 打通当日实测（ledger 有流水）
- confidence: 中（样本小，待 T2/T10 复测）

## E06 免费档的节奏参数（控制台实测口径）
- cue: 规划任务时长与唤醒预期时
- lesson: 闲置 30 分钟自动暂停、单次连续运行上限 8 小时、冷唤醒秒级（HTTPS 约 1.6s、SSH 1.5~2.4s）、暂停不占额外费用但占机器额度；快照配额是 5 不是第三方文章说的 10
- evidence: 2026-10-24 控制台 Machines/Snapshots/Usage 三页原文
- confidence: 高

## E07 门房机不可兼重活
- cue: 想顺手把批处理放到 my-cloud-pc 上时
- lesson: my-cloud-pc 已担邮件中继、展示页与两个 API 网关，是唯一不可炸的机器；重活一律走 pool，门房只读探活
- evidence: 2026-10-24 盘点确认 4 个公网口均在役；利用方案定版
- confidence: 高
