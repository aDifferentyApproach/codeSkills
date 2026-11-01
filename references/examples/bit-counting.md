# 位运算计数（三态掩码）

| 项 | 内容 |
|---|---|
| 归属 | 性能高效（SKILL.md） |
| 信号 | 计数只取模 k（出现 k 次找单个）；成对消去 |
| 形态 | 逐位统计 → 状态压缩为 k 态机 → 双掩码字并行；模 k 泛化按同推导链扩展掩码数 |

## 正反对照

### 统计方式

❌ 反例：

```python
ans = 0
for i in range(32):
    count = sum((x >> i) & 1 for x in nums)  # 32 趟 Python 层循环，每台状态机逐个输入推进
    ans |= (count % 3) << i
```

问题：O(32n)，解释器循环常数大——实测较正例慢 13 倍（n=10⁵）

✅ 正例：

```python
ones = twos = 0
for n in nums:
    ones = (ones ^ n) & ~twos  # 32 台状态机一次字级运算全体推进
    twos = (twos ^ n) & ~ones
return ones
```

不变量：ones 记"该位 1 已见 1 次（mod 3）"，twos 记"已见 2 次"；新输入先在 ones 登记，twos 已登记的位本轮屏蔽。正例与反例同复杂度档（O(n)），差距纯为常数层字并行。
