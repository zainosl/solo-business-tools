# 乔不不斯的一人公司工具 · 待办与 CRM

适合自己找客户、做交付、管进度的独立经营者。比如，一位客户今天来询价，你可以在 CRM 记录需求，把“今天发报价”放入待办的今日聚焦。成交后，继续在 CRM 跟踪收材料、交付和售后。两套工具可单独使用，记录由你分别维护。

| 想解决的问题 | 打开什么 | 你可以做什么 |
| --- | --- | --- |
| 事情多，今天先做哪三件？ | 待办工作台 | 用四象限区分轻重缓急，把例行工作放进“持续性待办”，按主题筛选，点 ☆ 加入今日聚焦，完成后可查历史。 |
| 客户谈到哪一步，成交后还欠什么？ | 客户管理 CRM | 用销售和交付两块看板分别推进客户，记录来源、产品、联系方式和历次跟进；切换表格可集中查找。销售选“已成交”或“老客待激活”后，客户进入交付看板。 |

## 第一次打开

1. [下载工具 ZIP](https://github.com/zainosl/solo-business-tools/archive/refs/heads/main.zip)，解压整个文件夹。
2. 双击 `index.html`，选择「待办工作台」或「客户管理 CRM」。页面首次打开是空白工作区。保留旁边的 `assets` 文件夹。
3. 想先看效果？在空白待办页点「数据管理 → 从备份恢复」，选择 [todo.example.json](examples/todo.example.json)。CRM 点「导入」，选择 [crm.example.json](examples/crm.example.json)。你会看到两条待办、两位虚构客户，其中一位已进入交付看板。

日常使用不需要账号、API Key 或服务器。数据保存在当前浏览器，浏览器清理、隐私模式、移动文件位置或换电脑都可能让你看到新的空白工作区。固定使用同一浏览器和位置，定期分别「下载备份」和「导出」。自己的备份可放在仓库忽略的 `private/` 目录。

若浏览器限制双击文件的本地存储，安装了 Python 3 的用户可以在解压目录运行下面的命令，再打开 [本机工作台](http://127.0.0.1:8765)。Windows 可用 `py -3` 替换 `python3`。以后使用同一地址和端口。

```sh
python3 -m http.server 8765 --bind 127.0.0.1
```

## 用 DeepSeek 或豆包把笔记变成自己的看板

适合已有会议纪要、零散任务、客户表格，希望先把内容整理出来的人。打开 [DeepSeek](https://chat.deepseek.com/) 或 [豆包](https://www.doubao.com/chat/)，新建对话，按需复制下面一段。用代号替换真实客户姓名、联系方式和合同信息。这里使用你自己的 AI 对话账号，工具本身不会调用模型。

**我要整理待办**（把最后一行换成你的记录）

```text
把我的记录整理为可以导入待办工作台的 JSON。只输出合法 JSON，不包代码块。
格式为 {"version":1,"tasks":[{"title":"具体行动","category":"业务主题","quadrant":"important_urgent","focused":true,"note":""}]}。
每条任务写一个能执行的动作。quadrant 只能用 ongoing（持续性）、important_urgent（重要且紧急）、important_not_urgent（重要不紧急）、urgent_not_important（紧急不重要）、not_important_not_urgent（均否）。证据不足先用 important_not_urgent，并在 note 标注待确认。只有我明确说今天最重要的事项才填 focused:true，最多三条。不要补造截止日期、客户或承诺。
我的记录：今天最要紧的是给客户甲发报价。每周五整理新增线索。
```

**我要整理客户**（每位客户一条，原文没有提到的字段留空）

```text
整理下面的脱敏跟进笔记，只输出一个合法 JSON 数组，不包代码块。
每条格式为 {"name":"客户代号","source":"","contact":"","product":"无","salesStatus":"intent","deliveryStatus":"to_serve","notes":"","logs":[]}。
salesStatus 可用 intent（有意向）、deposit（已付定金）、won（已成交）、reactivation（老客待激活）、abandoned（已放弃）、lost（已流失）。仅询价用 intent，不确定记在 notes；只有原文明确成交才用 won。未开始交付用 to_serve，正在收材料用 material_collecting，材料已交用 material_received。product 不清楚填“无”。带明确日期的跟进写成 {"t":"YYYY-MM-DD","text":"事实"} 加到 logs；缺日期只写 notes。
我的笔记：客户甲是朋友介绍的，询问工作坊报价。客户乙已成交，正在收集项目材料。
```

把 AI 回复保存为 UTF-8 纯文本，文件名分别用 `my-todo.json` 或 `my-crm.json`。按「第一次打开」里的对应入口导入，核对条数、今日聚焦和成交状态。**导入会替换该工具现有的全部记录。** 已经在用的用户先导出备份；如果只加一两条，直接在页面新增最简便。

## 用 WorkBuddy 改成自己的工具

如果你还想把“能力判断 / 首单冲刺”改成自己的服务名称，或把交付列改成你常用的步骤，用能操作本地文件的 WorkBuddy 更方便。复制一份解压目录，让 WorkBuddy 只打开这份副本，再粘贴下面这段。首次使用可参阅 [WorkBuddy 官方快速开始](https://www.codebuddy.ai/docs/zh/workbuddy/Quickstart)。

```text
请阅读这个文件夹的 README.md、todo.html、crm.html 和 examples/。帮我做一套适合自己的待办和客户管理工具。
先问我三个问题：我卖哪两种产品或服务？从首次接触到交付结束通常经过哪些阶段？每周要重复推进哪些事？
我回答后，在这份副本里把页面名称、产品选项、按钮文案和阶段显示名称改成我的表述。保留已有字段名和阶段 ID，让旧备份仍可导入。若需要增删阶段，先告诉我旧记录如何迁移。
按我的回答在 private/ 下分别生成 my-todo.json、my-crm.json；未知字段留空，不虚构客户。完成后告诉我打开哪个文件，先用虚构数据检查新增、导入、导出与刷新，再让我导入自己的数据。
```

只有 DeepSeek 或豆包聊天窗口，也能定制界面。把副本中 `crm.html` 的相关片段粘贴给 AI，说明“将 01 能力判断改成我的服务名，同时覆盖筛选按钮、编辑表单、卡片和转产品提示，保留 01 这个内部值。列出要查找的原文和替换文本”。在文本编辑器里逐项替换，保存后刷新副本即可。

## 更新与维护

- 普通用户更新前，先在两套工具分别导出 JSON。下载新版后用虚构样例试开，再恢复自己的备份。做过定制的用户可 Fork 仓库，在自己的分支保留修改。
- 主要文件为 `todo.html`（待办、聚焦与历史）、`crm.html`（销售、交付与客户记录）、`assets/`（样式和主题）、`examples/`（可直接导入的虚构数据）。
- 反馈问题请到 [Issues](https://github.com/zainosl/solo-business-tools/issues)，写明浏览器、操作步骤、预期和实际结果，复现数据请用虚构样例。欢迎通过 Pull Request 提交修改。
- 每次推送或提交 Pull Request，GitHub Actions 会在 Chrome 中使用虚构样例检查导入、刷新、导出与恢复。用例在 `tests/smoke.cjs`。
- 修改存储字段或导入逻辑后，请用两个示例分别导入、编辑、导出、刷新并重新导入，确认原记录可恢复，CRM 成交客户仍可见于交付看板。

采用 [MIT 许可证](LICENSE)。
