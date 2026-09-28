# AI 味与防御性写作黑名单

写完每一节后扫描一遍。这不是绝对禁用表——个别词在确切含义下可以用（例如 robust 指鲁棒性实验时），但出现频率高、或者只起修饰作用时就要改。

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
| landscape, paradigm, realm, tapestry | 删掉或换成具体领域名 |
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
- **冒号揭晓式**（"The answer is simple: …"）和**设问句**：删。
- **正文加粗短语、段内 bullet list**：改回段落（contribution 列表除外）。
- **万能开头**："In recent years, X has attracted increasing attention" / "LLMs have achieved remarkable success"：直接从具体问题开始。

## 3. 防御性句式（全文最多 1–2 处）

典型形式：

- "…, but this does not imply / mean that…"
- "We do not claim that…"
- "It should be noted that … may not …"
- "While our method has limitations, …"
- "We caution that…" / "Note that this is not…"
- "…, although further investigation is needed."

处理顺序：先**收窄 claim**，把 claim 写到它真正成立的范围；真正需要交代的局限**集中到 Limitations 段**；剩下的**直接删**。

改写示例：

- 原：Our results suggest that M improves robustness, but this does not imply that M is robust to all perturbations.
- 改：M reduces the accuracy drop under Gaussian noise and blur from 12.4% to 3.1%.

## 4. 强调方式

- 原：Importantly, we emphasize that our method requires no additional training.
- 改：Our method requires no additional training.

- 原：Notably, M achieves a significant improvement.
- 改：M improves accuracy by 4.2 points over the strongest baseline.
