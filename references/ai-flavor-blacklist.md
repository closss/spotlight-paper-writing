# AI 味与防御性写作黑名单

写完每一节后扫描一遍。这不是绝对禁用表：个别词在确切含义下可以用（例如 robust 指鲁棒性实验时），oral 论文里也能找到 notably、crucial。管的是密度和空洞修饰——同一个词全文出现超过一两次，或者只起修饰作用时，就要改。

## 0. 次数预算

下表的实测数据来自六篇 oral（DPO、Genie、NSA、VGGT、Gated Attention、D4RT）的正文，每篇约 5–6k 词。预算取在实测中位数或更低，因为目标是比一般论文更干净。

| 词或句式 | 六篇实测（每篇次数） | 预算（全文） |
|---|---|---|
| 句首 Notably / Importantly / Crucially / Remarkably / More importantly | 1–6，中位数 3 | ≤ 3，且后面紧跟具体事实或数字 |
| we emphasize / it is crucial to note 等元强调 | 0–1 | 0 |
| significant(ly)（非统计意义） | 4–16，中位数 7 | ≤ 5，且同一句给出数字；能换成 substantially 或 by X points 更好 |
| Moreover / Furthermore / Additionally | 0–9，中位数 2.5 | ≤ 3，不连续使用 |
| leverage / harness / unlock | 1–8，中位数 3 | ≤ 3 |
| comprehensive / extensive | 0–5，中位数 1.5 | ≤ 2 |
| crucial（形容词） | 0–7，中位数 1 | ≤ 2 |
| 自夸式 novel（"a novel method"） | 0–3，中位数 0 | ≤ 1 |
| underscore / showcase | 0–4，中位数 0.5 | ≤ 1 |
| delve / seamlessly / tapestry | 0–1 | 0 |
| "this does not imply" 类免责句 | 0 | ≤ 1–2 |
| 破折号 | 0–3 | 每段 ≤ 1 |

## 1. 词汇

| 避免 | 通常的替代做法 |
|---|---|
| delve into / dive into | study, analyze, examine，或直接删 |
| crucial, pivotal, paramount, vital | 删掉，用事实说明为什么重要 |
| notably, importantly, it is worth noting that, it is important to note | 删掉，直接陈述 |
| seamlessly, effortlessly | 删掉，或给出具体的集成成本 |
| comprehensive, extensive（修饰实验时） | 说清楚做了几个数据集、几个 baseline |
| novel（全文超过 1–2 次） | 删掉，新颖性靠内容体现 |
| remarkable, impressive, significant（非统计意义时） | 给数字 |
| leverage, harness, unlock, empower | use, exploit, enable，或改写句子 |
| landscape, realm, tapestry | 删掉或换成具体领域名 |
| paradigm | 只在明确写出"从 X 转向 Y"、且 X 和 Y 都是具体技术做法时使用；否则删掉 |
| shed light on, pave the way, open new avenues | 删掉或写具体结论 |
| underscore, showcase, highlight（作动词反复使用） | show, indicate |
| intricate, meticulous, holistic, nuanced | 删掉或换成具体描述 |
| a myriad of, a plethora of | many, several，或给数量 |
| robust（泛泛修饰） | 说清楚对什么扰动鲁棒 |

## 2. 句式

- **连续的 Moreover / Furthermore / Additionally**：多数情况下删掉连接词，靠段落逻辑衔接。
- **"not only X but also Y"**：改成两个陈述，或 "X and Y"。
- **三连排比**（"efficient, scalable, and robust"）：只保留有证据支撑的那一两个。
- **句尾分词短语**（"…, highlighting the effectiveness of our method." / "…, demonstrating…"）：删掉或改成独立的陈述句，并给出具体结论。
- **破折号插入语**：一段内最多一处，优先改成逗号或拆句。
- **"This is not X, but Y" / "Rather than X, we Y" 的对照句**：偶尔可以，频繁出现就是 AI 味。
- **冒号揭晓式**（"The answer is simple: …"）：删。
- **设问句**：段落中间用来制造悬念的设问句删掉。例外是 intro 里一个框定全文的研究问题（"we ask whether …" / "What if …"），而且论文给出了回答，全文最多一处。写成问句的实验小标题（DPO），以及 Limitations 里用问句列出的开放问题，不计入这个上限。
- **正文加粗短语、段内 bullet list**：改回段落。contribution 列表除外；段首的 run-in 小标题（如 **Training setup.**）也不在此列。
- **万能开头**："In recent years, X has attracted increasing attention" / "LLMs have achieved remarkable success"：直接从具体问题开始。

## 3. 防御性句式（全文最多 1–2 处）

典型形式：

- "…, but this does not imply / mean that…"
- "We do not claim that…"
- "It should be noted that … may not …"
- "While our method has limitations, …"
- "We caution that…" / "Note that this is not…"
- "…, although further investigation is needed."（挂在主结果句末尾时算防御；放在讨论、局限或附录里描述真正的开放问题时不算）

处理顺序：先**收窄 claim**，把 claim 写到它真正成立的范围；真正需要交代的局限**集中到 Limitations 段**；剩下的**直接删**。

改写示例：

- 原：Our results suggest that M improves robustness, but this does not imply that M is robust to all perturbations.
- 改：M reduces the accuracy drop under Gaussian noise and blur from 12.4% to 3.1%.

## 4. 强调方式

斜体用于三种情况：首次定义命名概念；少量单个对比词（*all*、*not*、*directly*，大约一页不超过一处）；分析型论文每节末尾至多一句斜体结论。加粗只用于段首 run-in 小标题和表格高亮。

- 原：Importantly, we emphasize that our method requires no additional training.
- 改：Our method requires no additional training.

- 原：Notably, M achieves a significant improvement.
- 改：M improves accuracy by 4.2 points over the strongest baseline.
