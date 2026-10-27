# 示例：Linux 内核源码

项目：[torvalds/linux](https://github.com/torvalds/linux)。

本次查阅的固定提交：[`83f32c773255720a661aa45d83e36278135f23f5`](https://github.com/torvalds/linux/tree/83f32c773255720a661aa45d83e36278135f23f5)。以下结论只对应这次核对的实现；不推断所有版本和配置都一致。

![Linux 内核源码荒诞手绘梗图](../assets/example-linux-kernel.png)

## 用户输入

```text
用 $draw-project-meme 画这个开源项目：https://github.com/torvalds/linux
示例直接用 Linux 内核源代码。
参考那种白底黑线的现代基础设施梗图：体量悬殊、临时拼装、冷旁注，
要有源码里的具体怪事，不要架构宣传图、表情包气泡或“全靠这玩意”的解释。
```

## 原理与主反差

Linux 内核管理硬件和系统资源，并为其他软件提供基础服务。[仓库 README](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/README#L1-L5)

图中庞大的灰色装置代表多个内核子系统，底部把常见的数据结构、同步和地址管理机制夸张为寒酸的小连接件。它强调“复杂系统建立在朴素机制上”，**不声称 Linux 仅由两根指针、链表、C 语言或某个循环实现**。

`fs/`、`net/`、`drivers/`、`mm/`、`kernel/` 是源码目录识别点。堆叠顺序不是调用顺序或依赖方向，块体大小不是代码行数统计。C 地基是语言比喻，不表示内核没有汇编或 Rust 代码。

## 每个物件的源码依据

| 画面物件 | 核实事实 | 固定源码 |
| --- | --- | --- |
| `list_head`、`next/prev` 两根细支撑 | `struct list_head` 包含两个同类型指针；它用于任务列表及亲属列表。链表不等于整个调度算法。 | [类型定义](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/include/linux/types.h#L206-L208)、[链表操作](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/include/linux/list.h#L12-L55)、[task_struct.tasks](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/include/linux/sched.h#L973-L980)、[children/sibling](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/include/linux/sched.h#L1100-L1105) |
| 微小的“锁”“页表”支撑 | 调度路径使用运行队列锁，地址空间管理涉及页表；它们是协作机制，不是链表的装饰。 | [调度锁语境](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/kernel/sched/core.c#L5400-L5444)、[页表占用计入资源评分](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/mm/oom_kill.c#L222-L237) |
| OOM 切掉带 `oom_score` 牌子的进程块 | 常规路径按资格与评分选候选者，随后发送 SIGKILL；不是随机抽签，也不是卸载内核模块。 | [oom_badness](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/mm/oom_kill.c#L190-L237)、[候选选择](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/mm/oom_kill.c#L299-L370)、[发送 SIGKILL](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/mm/oom_kill.c#L905-L940) |
| MacBook5 外接“专用重启”按钮 | x86 重启代码按 DMI 匹配 MacBook5，选择特殊 PCI 重启方式。 | [set_pci_reboot](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/arch/x86/kernel/reboot.c#L139-L150)、[MacBook5 特判](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/arch/x86/kernel/reboot.c#L185-L193) |
| 精密秒表对着空凳 | `play_idle_precise(duration_ns, latency_ns)` 设置高精度计时器并进入空闲路径；“纳秒级发呆”是对空闲注入的旁注。 | [play_idle_precise](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/kernel/sched/idle.c#L411-L445) |

### 不要误读

- OOM 的图只讽刺常规评分选择路径。另有配置和特殊情况，例如选择正在申请内存的任务；不能总结成“永远杀最大的进程”。见[配置分支](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/mm/oom_kill.c#L1138-L1145)。图上的 `oom_score` 是评分概念的短标签，不是完整的内部计算公式。
- MacBook5 按钮是兼容分支的物理比喻，不是实际需要外接按钮，也不泛指所有 Apple 设备。
- 精确空闲注入是特定功能，不能当作全部 CPU 调度或内核的核心执行循环。
- 研究时还发现 idle task 的“不许 sleep”注释，但最终图没有采用这句话。它指任务不能阻塞出队，不是禁止 CPU 节能休眠。见[原注释及处理](https://github.com/torvalds/linux/blob/83f32c773255720a661aa45d83e36278135f23f5/kernel/sched/idle.c#L519-L530)。

## 构图与修正

取用户原图的细黑线、灰色质量块、离谱连接与冷标签，不复用原图的品牌组合。移除早期示例中的大标题、火柴人、汗滴、对白和“全靠这玩意”。

实际制作采用内置图像生成，随后做两轮有明确目标的局部修正：

1. 让 OOM 真正切掉侧面的进程块，删除解释性旁注，移除会误导成网络依赖的空闲装置连接线。
2. 修正 `next/prev` 的接触点，避免它们只是在巨塔下面悬空陈列。

最终图保留“锁”和“页表”等其他支撑；不为了制造单点笑话牺牲事实边界。验图检查了标签、承重接触、OOM 处理对象和三个旁梗的位置；这不是对“好笑程度”的客观保证。

完整实际提示词见[生成记录](linux-kernel-prompts.md)。首次制作使用用户提供的原图作为视觉参考，该参考图不在仓库中。复用文中的场景描述仍可独立生成，但不能逐像素复现。

## 图下配文

> Linux：一大堆认真工作的子系统，旁边还有一台认真到纳秒的发呆装置。

详细的原理边界放在本页，不把长篇解释挤进梗图。
