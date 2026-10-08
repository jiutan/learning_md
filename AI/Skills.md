# AI Skills

### 使用：

```
请使用 <技能包名>，要求。
```



### 1. drawio-skill

- 作用：

  根据自然语言生成可编辑 `.drawio` 图，并支持自检、修改、导出 SVG/PDF/PPTX

- 下载安装：

  ```shell
  npx skills add Agents365-ai/drawio-skill \
    --global \
    --agent codex \
    --yes \
    --copy
  ```

- 使用：

  ```文本
  请使用 drawio-skill，把我的三自由度船载稳定平台数字孪生故障诊断技术路线生成可编辑 draw.io 图。
  ```

  

### 2. nature-skills

- 作用：

  论文阅读、学术润色、科研绘图、论文转 PPT、审稿意见回复等

- 部分技能：

  `nature-reader`：读取论文并整理结构化笔记

  `nature-figure`：生成投稿级科研图

  `nature-paper2ppt`：将论文整理成汇报 PPT

  `nature-polishing`：论文语言润色

  `nature-shared`：共享支持包

- 下载安装：

  ```shell
  npx skills add Yuan1z0825/nature-skills \
    --global \
    --agent codex \
    --skill nature-reader \
    --skill nature-figure \
    --skill nature-paper2ppt \
    --skill nature-polishing \
    --skill nature-shared \
    --yes \
    --copy
  ```

- 使用：

  ```文本
  请使用 nature-reader，分析这篇液压系统故障诊断论文，输出研究对象、故障参数、模型、残差、诊断方法、验证方式和对我课题的借鉴价值。
  ```

  