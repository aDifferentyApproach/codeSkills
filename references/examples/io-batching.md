# I/O 批量化

| 项 | 内容 |
|---|---|
| 归属 | 性能高效"原则"条（SKILL.md） |
| 信号 | 公式中 I/O 往返项主导（多次查询 / 多次写出） |
| 形态 | 合并为批量操作——IN 查询、writelines、按块读写 |

## 正反对照

### 按 id 集合查询

❌ 反例：

```python
users = []
for uid in user_ids:
    row = db.query("SELECT id, name, email FROM users WHERE id = ?", uid)
    users.append(row)
```

问题：往返次数 = n，每次毫秒级延迟被放大 n 倍（N+1）

✅ 正例：

```python
rows = db.query("SELECT id, name, email FROM users WHERE id IN (?)", user_ids)  # 往返 = 1
```

### 写出多行

❌ 反例：

```python
with open(out_path, "w") as f:
    for u in users:
        f.write(f"{u.id},{u.name},{u.email}\n")
```

问题：每行一次系统调用，10⁵ 行 = 10⁵ 次调用

✅ 正例：

```python
with open(out_path, "w") as f:
    f.writelines(f"{u.id},{u.name},{u.email}\n" for u in rows)  # 合并写出
```
