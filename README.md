# AI Word Book（双语台词词汇本 LaTeX 模板）

这是一个用 LaTeX（XeLaTeX）排版的「英文台词 + 中文翻译 + 词汇表」笔记模板，适合把影视剧/播客/采访等素材做成结构化词汇本。项目提供两套风格：

* **aiwordbook.sty（现代风格）**：卡片式句子块、时间戳、词汇范围标签、单词 chip、可选 IPA 音标、可选多主题配色。
* **classic.sty（经典风格）**：更朴素的版式，同样支持在单词与词性之间显示 IPA（DejaVu Sans）。

项目目录示例（你的仓库大致就是这样）：

```
Movies/
Severance/
SlowHorses/
TedLasso/
aiwordbook.sty
classic.sty
```

---

## 1. 编译方式

推荐使用 **XeLaTeX**（因为需要 CJK 与字体支持）。

* 本地：`xelatex yourfile.tex`
* Overleaf：选择 XeLaTeX 编译器

---

## 2. 快速开始（现代风格 aiwordbook）

### 2.1 最小示例

```tex
\documentclass[11pt,a4paper]{article}
\usepackage[Blue]{aiwordbook}   % 主题可选，默认 Blue

\title{Slow Horses}
\subtitle{S05E04: Missiles}

\date{}
\author{}

\begin{document}
\maketitle
\bigskip

\SentenceBlock[0:00:47]
{And if she has done anything, it was done under duress.}
{就算她做了什么，那也是被胁迫的。}{
  \Word{duress}{n.}{胁迫，强迫}[djʊəˈres]
}

\end{document}
```

---

## 3. 现代风格：核心命令说明（aiwordbook.sty）

### 3.1 `\SentenceBlock`（句子卡片）

```tex
\SentenceBlock[时间戳]{英文句子}{中文翻译}{
  % 可选：若干个 \Word...
}
```

* **可选参数 `[]`**：通常放时间戳，如 `0:01:14`。为空也可以（不显示右上角标签）。
* **第 2 个参数**：英文句子
* **第 3 个参数**：中文翻译（每行有轻微缩进，便于阅读）
* **第 4 个参数**：词汇列表（可为空）

> 右上角会显示时间戳；若本块包含多个单词条目，会显示类似 `#14-15` 的“词汇序号范围”（全局累计）。

---

### 3.2 `\Word`（词条）

```tex
\Word{word}{pos.}{中文释义}[IPA]
```

* 前三个参数必填：

  * `word`：单词
  * `pos.`：词性（例如 `n.` / `v.` / `adj.` / `adv.` 等）
  * `中文释义`：释义
* **可选第 4 参数**：IPA 音标（Unicode 字符），会使用 **DejaVu Sans** 字体渲染，并显示在 **单词与词性之间**：

  * 示例：`plague /pleɪɡ/ (n.) — 瘟疫，灾祸`

如果不写 `[IPA]`，则不显示音标。

---

### 3.3 `\subtitle`（副标题）

使用：`\subtitle`命令

```tex
\title{Slow Horses}
\subtitle{S05E04: Missiles}
```

然后 `\maketitle` 会自动排版为主标题 + 副标题。

---

### 3.4 `\AIDivider`（可选：分隔带）

用于章节/段落分隔：

```tex
\AIDivider{Part 1}
```

---

## 4. 多主题配色（aiwordbook）

默认主题为 **Blue**。你也可以在 `\usepackage[...]` 中切换：

```tex
\usepackage[Indigo]{aiwordbook}
```

可用主题（区分大小写）：

* `Blue`（默认）
* `Orange`
* `Cyan`
* `Indigo`
* `Amber`
* `Green`
* `BlueGrey`

---

## 5. 切换到 classic 风格（classic.sty）

如果你想使用更朴素的 “classic” 主题：

```tex
\documentclass[11pt,a4paper]{article}
\usepackage{classic}

\begin{document}
\maketitle

\SentenceBlock[0:00:47]{...}{...}{
  \Word{duress}{n.}{胁迫，强迫}[djʊəˈres]
}
\end{document}
```

> classic 风格保持原有排版风格，只在需要时支持 IPA（同样使用 DejaVu Sans）。其余使用方式与现代风格保持一致：依旧是 `\SentenceBlock` + `\Word`。

---

## 6. 推荐写作习惯

* 每个 `SentenceBlock` 对应一个台词句子（建议包含时间戳）
* 每个句子里仅挑最关键的词做 `\Word`，并保持释义简洁
* IPA 使用 Unicode（如 `ˈ`、`ɪ`、`ʊ` 等），不用额外转义

---

## 7. 常见问题

### Q1：如何不显示 IPA？

不写第四个参数即可：

```tex
\Word{undercover}{adv.}{秘密地，暗中地}
```

### Q2：如何换主题？

把 `\usepackage[主题]{aiwordbook}` 中的主题名替换即可，例如：

```tex
\usepackage[BlueGrey]{aiwordbook}
```

### Q3：如何改回 classic？

把 `\usepackage{aiwordbook}` 改为：

```tex
\usepackage{classic}
```

