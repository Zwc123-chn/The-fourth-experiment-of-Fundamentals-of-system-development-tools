# The-fourth-experiment-of-Fundamentals-of-system-development-tools
## 第 13 题 建立可执行的本地质量门禁

**主题**：代码质量
**建议用时**：12‑15 分钟

复用第 10 题完成的 greetlab 包，在`q13` 中建立一个轻量本地质量检查。

**题目要求**

1. 复制`q10` 为`q13`；在`pyproject.toml` 中加入`ruff` 和`pytest` 的最小配置。
2. 补充一个正常姓名测试和一个空白姓名测试，每个测试包含有效断言。
3. 运行`ruff format`、`ruff check` 和`pytest`，修复全部问题，不得全局忽略规则。
4. 编写`check.sh`，依次执行`ruff format --check`、`ruff check` 和`pytest`；运行并保证返回 0。

## 第 14 题 让 Make 只重建真正受影响的产物

**主题**：元编程：构建系统
**建议用时**：12‑15 分钟

在`q14` 中按给定内容创建三个源文件，只需完成`Makefile`。

**给定内容**
`data.csv`

```
name,value
alpha,2
beta,3
gamma,5
```

`stats.py`

```
import csv
with open("data.csv") as f:
    total = sum(int(r["value"]) for r in csv.DictReader(f))
open("stats.txt", "w").write(str(total))
```

`build_report.py`

```
text = open("report.md").read()
total = open("stats.txt").read()
open("report.txt", "w").write(f"{text}\nTotal: {total}\n")
```

`report.md`

```
# Data Report
```

**题目要求**

1. 创建给定的`data.csv`、`stats.py`、`build_report.py` 和`report.md`。
2. 编写`Makefile`，包含`all`、`stats.txt`、`report.txt` 和`clean`；准确列出数据文件、脚本和中间产物依赖，并把`all`、`clean` 声明为`.PHONY`。
3. 验证首次`make` 生成两个产物；第二次无改动时不执行配方。
4. `touch data.csv` 后再次`make`，确认`stats.txt` 和`report.txt` 重新生成；`clean` 只删除生成物。

## 第 15 题 把本地 API 数据转换为可读报告

**主题**：大杂烩：API、jq、CLI 约定与 Markdown
**建议用时**：12‑15 分钟

在`q15` 中创建给定 JSON 和本地 HTTP 服务，再用`curl` 与`jq` 生成简短 Markdown 报告。

**给定 JSON（packages.json）**

```
[
{"name":"alpha","status":"active","downloads":120,"version":"1.2.0"},
{"name":"beta","status":"inactive","downloads":900,"version":"2.0.0"},
{"name":"gamma","status":"active","downloads":450,"version":"1.5.1"},
{"name":"delta","status":"active","downloads":450,"version":"0.9.0"},
{"name":"epsilon","status":"active","downloads":80,"version":"3.1.0"}
]
```

**题目要求**

1. 把给定 JSON 保存为`packages.json`，并在`q15` 目录运行 `python -m http.server 8000`。
2. 使用 `curl -fsS` 获取 `http://127.0.0.1:8000/packages.json`。
3. 使用`jq` 筛选`status` 为`active` 且`downloads` 不少于 100 的记录，并按`downloads` 降序、`name` 升序排列。
4. 编写`api_report.sh`，把结果生成`summary.md`，包含标题和`name/version/downloads` 三列表格。

## 第 16 题 修复并交付一个陌生的小型工具仓库

**主题**：课堂综合测试
**建议用时**：12‑15 分钟

复用第 13 题的项目，在`q16` 中完成一次 15 分钟综合检查。

**题目要求**

1. 复制`q13` 为`q16` 并初始化 / 继续使用 Git。
2. 把问候语实现临时改成始终返回字面量`Hello, name!`，运行`check.sh` 确认测试失败；随后定位并修复。
3. 编写最小`Makefile`，包含`check`、`build` 和`clean`；`check` 调用`check.sh`，`build` 生成 wheel。
4. 运行`make check` 和`make build`，计算 wheel 的 SHA‑256，并把最终改动提交为一个内容聚焦的 Git 提交。
