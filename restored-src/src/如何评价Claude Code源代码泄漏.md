# (1 封私信) 如何评价Claude Code源代码泄漏？ - 知乎

[

开源

](//www.zhihu.com/topic/19562746)

[

源码泄露

](//www.zhihu.com/topic/19627898)

[

vibe-coding

](//www.zhihu.com/topic/1885613669322319751)

[

claude-code

](//www.zhihu.com/topic/1946631524649800689)

# 如何评价Claude Code源代码泄漏？

关注者

**190**

被浏览

**147,197**

关注问题​写回答

​邀请回答

​好问题 1

​添加评论

​分享

​

[查看全部 40 个回答](/question/2022392127145911515)

[![冯若航](https://pic1.zhimg.com/v2-8ca9b6d12b3090efc67bcd27047fff6a_l.jpg?source=2c26e567)](//www.zhihu.com/people/vonng)

[冯若航](//www.zhihu.com/people/vonng)

[​![](https://pic1.zhimg.com/v2-4a07bc69c4bb04444721f35b32125c75_l.png?source=32738c0c)](https://www.zhihu.com/question/48509984)​![](https://pic1.zhimg.com/v2-4812630bc27d642f7cafcd6cdeca3d7a.jpg?source=88ceefae)

知势榜科技互联网领域影响力榜答主

​ 关注

324 人赞同了该回答

> SOTA Coding Agent —— Claude Code 源代码又泄漏了，在同一个阴沟里翻了两次船。代码全部白给，堪称行为艺术。

好消息！好消息！走过路过不要错过！Anthropic 最新旗舰编码智能体 Claude Code，源代码全部公开了！

[GitHub](https://zhida.zhihu.com/search?content_id=775515375&content_type=Answer&match_order=1&q=GitHub&zhida_source=entity) 仓库已有上千 Star，四千七百多个源文件，五十多万行代码，全部免费！不要 998，不要 98，点开就能看！ 地表最强 Agent 实现全部白给，全场 TypeScript 统统白给！Tools 实现白给！多 Agent 协调白给！System Prompt 白给！ 内部代号 KAIROS 都白给！挥泪大放送，走过路过千万不要错过！

---

## 这是一个愚人节笑话吗？

不是，今天是 3 月 31 号，明天才是愚人节。

实际上是 Anthropic 打包流水线翻车了，[Source Map](https://zhida.zhihu.com/search?content_id=775515375&content_type=Answer&match_order=1&q=Source+Map&zhida_source=entity) **又泄了！**

![](https://picx.zhimg.com/50/v2-cf1064017a3d3b87ef1781051b8bf894_720w.jpg?source=2c26e567)

不是 Anthropic 大发慈悲搞了个 Apache 2.0。而是有人发现：**[NPM](https://zhida.zhihu.com/search?content_id=775515375&content_type=Answer&match_order=1&q=NPM&zhida_source=entity) 发布包里的** **`cli.js.map`** **中完整保留了** **`sourcesContent`** **字段**。一行命令提取，全部源码还原。4756 个文件，整整齐齐。

![](https://pica.zhimg.com/50/v2-292c6a1ecef15d6d9f11ff9caccb62f7_720w.jpg?source=2c26e567)

这不是“开源”，这是 **开裆裤**。

---

## 为什么是“又泄了”？

没错。**一模一样的翻车方式，一年前就来过一次。**

2025 年 2 月 24 日，Claude Code 作为研究预览版首次发布。TypeScript 开发者们兴冲冲地打开 `node_modules`，翻到 `cli.mjs` 的最后一行，赫然发现了 `sourceMappingURL`——直指完整的 Source Map 文件。

有位叫 Dave Schumaker 的开发者完整记录了这段经历：他发现泄露后，想去 NPM 下载旧版本备份——发现 Anthropic 已经从 NPM Registry 上下架了所有旧版本。去翻本地 npm cache——也没找到。正要认命关电脑，发现 Sublime Text 还开着那个文件，按了一下 `⌘+Z`……撤销大法好，Source Map 又回来了。

Anthropic 当时的反应堪称迅速：推更新删除 Source Map，同时从 NPM Registry 下架所有包含 Source Map 的旧版本。亡羊补牢，雷厉风行。

![](https://picx.zhimg.com/50/v2-661af5094ceefb58b841268da7ac5481_720w.jpg?source=2c26e567)

  

然后一年后，**同一个坑，又跳了进去**。

版本号从 `0.2.x` 涨到了 `2.1.88`，功能翻了好几倍，但构建流水线的 Source Map 配置显然没有写进 CI/CD 的 checklist 里。有意思的是，截至发稿时 NPM 上显示的最新版本已经回退到了 `2.1.87`——看来 Anthropic 又开始了熟悉的“紧急撤包”流程。

这让我想起一句老话：**历史不会简单地重复，但它确实押韵。**

---

## 上次翻车引发了什么？

这是很多人不知道的：**2025 年初 Claude Code 的第一次源码泄露，实质性地催化了 AI Coding Agent 赛道的“寒武纪大爆发”。**

在此之前，大家对“怎么构建一个 Coding Agent”这件事其实相当模糊。你能看到 Aider、Continue、Cursor 各有各的路子，但谁也不确定 SOTA 的做法是什么。

然后 Claude Code 的源码摊在了所有人面前：

-   用 System Prompt + Tool Use 组织工作流
-   用子代理分工处理不同类型的任务
-   用权限沙箱控制文件系统和命令执行

这不是什么火箭科学。但它告诉了整个行业：**SOTA 就是这么做的。原来就这？**

于是大家纷纷跟进。那一波爆发，Claude Code 的泄露功不可没——虽然 Anthropic 肯定不想承认这一点。

---

## 这次又暴露了什么？

一年过去了，Claude Code 从一个简单的 CLI 工具进化成了一个复杂的 Agent 平台。这次 `v2.1.88` 的泄露，展示了大量一年前完全不存在的新模块：

**`coordinator/`** **—— 多 Agent 协调**

这是 Agent Teams 功能背后的核心实现。如何让多个 Agent 各自拥有独立上下文窗口、独立工具权限、并行工作又不互相打架？答案就在这个目录里。开源社区之前只能通过 System Prompt 猜测其工作方式，现在能看到完整的工程实现了。

**`assistant/`** **—— 内部代号 KAIROS**

这个代号此前从未公开出现过。它代表什么？是一种新的交互范式？一种高级助手模式？源码里应该有答案。

**`voice/`** **—— 语音交互**

Claude Code 的语音模式。这在公开文档和 Changelog 中有所提及，但实现细节一直是黑箱。

**`plugins/`** **+** **`skills/`** **—— 插件和技能系统**

这是 Claude Code 的可扩展性架构。技能系统允许按需加载领域知识——源码中能看到完整的加载、匹配和注入机制。

**`buddy/`** **—— AI 伴侣 UI**

这又是个什么东西？

![](https://pica.zhimg.com/50/v2-8e3384fe6be633c18f1af896eca22f1b_720w.jpg?source=2c26e567)

  

这几天所有搞 AI Agent 的应该都会来琢磨、研究这份泄露的代码。实际上我已经看到社区有人放出来一些研究结果了。 估计用不了几天，又会有一大堆编码助手冒出来了。

---

## Anthropic 最近的“泄露体质”

如果只是 Source Map 泄露，还可以说是个 “oops” 级别的工程事故。

但联系上下文看就有意思了：就在上周（3 月 26 日），Fortune 杂志报道 Anthropic 因为 CMS 配置错误，导致未发布的 **Claude Mythos** 模型信息（内部定位为 Opus 之上的新层级）和一场欧洲 CEO 闭门峰会的细节被安全研究者在公开数据湖中发现。

再往前推，今年 1 月 Check Point 披露了 Claude Code 的安全漏洞 CVE-2026-21852——恶意仓库可以通过 `.claude/settings.json` 中的 `ANTHROPIC_BASE_URL` 配置窃取用户的 API Key，用户只需要打开仓库就会中招。

Source Map 泄露 + CMS 数据湖泄露 + 安全漏洞……对于一家以 “AI Safety” 为核心招牌的公司来说，2026 年 Q1 的表现多少有些行为艺术的味道。

---

## 为什么会反复翻车？

答案很简单：**因为他们选择了 NPM。**

Claude Code 用 TypeScript 编写，通过 `npm install -g` 全局安装分发。这意味着：

1.  **NPM 包是透明的。** 任何人都可以解压 `.tgz` 检查内容，这是 JS 生态的基本特性。
2.  **Source Map 是 JS 生态的标准调试工具。** 构建流水线中只要有一个配置项没关对，它就会跟着包一起发出去。
3.  **即使是 minified 的 JS，也可以通过 LLM 辅助逆向还原。** 有人（Yuyz0112）专门做了一个项目，让 Claude 自己反编译自己的代码。

如果 Claude Code 像 Cursor 一样用 Electron 打包二进制分发，或者像 Devin 那样做纯 SaaS，Source Map 泄露这个问题根本不会存在。但 Anthropic 选择了 NPM——选择了 JS 生态的便利性，就要接受它的透明性。

而说到 NPM 生态的风险，Source Map 泄露其实只是最温和的那种。**就在今天（3 月 31 日），NPM 生态爆出了一起严重得多的事件：Axios 供应链投毒攻击。**

\*\*一个 `npm install`，两秒钟，木马就已经开始向攻击者的服务器回传数据了——`npm` 甚至还没解析完依赖树。 \*\* StepSecurity 的安全研究者称这是“有记录以来针对 Top-10 NPM 包最精密的供应链攻击之一”。Anthropic 的 Source Map 泄露简直是“小巫见大巫”。

老实说，前端圈 JS、TS 圈的这些花活，真是让人瞠目结舌。

---

## 所以影响是什么？

**对行业：又一次免费技术培训。**

一年前的泄露让大家知道了“Coding Agent 该怎么做”。这一次让大家知道了“SOTA Coding Agent 现在进化到了什么程度”。 多 Agent 编排、插件系统、语音交互、技能按需加载……这些都是 2025-2026 年 Agent 工程的前沿实践。开源社区会消化得很快。

**对 Anthropic：尴尬但不致命。**

Claude Code 的核心竞争力从来不是客户端代码 —— 而是底层的 Claude 模型能力。 Anthropic 在 [Harness 维度](https://zhida.zhihu.com/search?content_id=775515375&content_type=Answer&match_order=1&q=Harness+%E7%BB%B4%E5%BA%A6&zhida_source=entity)上和大家共产了一把，虽然尴尬，但不会伤筋动骨。

**对安全：可能反而是好事。**

更多人能审计 Claude Code 的权限模型、Hooks 机制、MCP 信任边界，意味着更多漏洞会被更快发现。Check Point 已经证明了这一点。

当然也少不了 Claude 的自我反思环节。我请 Claude Opus 自我点评了这场泄露事件，看上去它还透露出一股高兴的劲儿。

![](https://picx.zhimg.com/50/v2-ca3e51a6fa06bc4d9e5d7eb02c247bbf_720w.jpg?source=2c26e567)

---

## 愚人节前的滑稽戏

如果我告诉你 SOTA Agent “Claude Code 开源了”，你可能会觉得这是愚人节玩笑。

但事实是：Claude Code 的完整源码确实在 GitHub 上公开了。只不过不是 Anthropic 主动开源的，而是他们的构建流水线替他们做了这个决定。

**这大概是 2026 年最好的愚人节笑话：它是真的。**

历史告诉我们，一年前的那次泄露，Anthropic 紧急删除、清理、封堵。这次大概率也会重复同样的流程。所以如果你想看的话——趁现在赶紧去保存一份吧。

---

**参考链接：**

-   [ChinaSiro/claude-code-sourcemap](https://link.zhihu.com/?target=https%3A//github.com/ChinaSiro/claude-code-sourcemap) — 本次 `v2.1.88` 源码还原
-   [Digging into the Claude Code source](https://link.zhihu.com/?target=https%3A//daveschumaker.net/digging-into-the-claude-code-source-saved-by-sublime-text/) — 一年前第一次泄露的完整记录
-   [Hacker News: Claude Code source code leaked (2025)](https://link.zhihu.com/?target=https%3A//news.ycombinator.com/item%3Fid%3D43173324) — HN 上的历史讨论
-   [Hacker News: Claude Code source code leaked (2026)](https://link.zhihu.com/?target=https%3A//news.ycombinator.com/item%3Fid%3D47584540) — 这次的 HN 讨论
-   [Piebald-AI/claude-code-system-prompts](https://link.zhihu.com/?target=https%3A//github.com/Piebald-AI/claude-code-system-prompts) — 每个版本的 System Prompt 追踪
-   [Fortune: Anthropic Mythos Leak](https://link.zhihu.com/?target=https%3A//fortune.com/2026/03/26/anthropic-says-testing-mythos-powerful-new-ai-model-after-data-leak-reveals-its-existence-step-change-in-capabilities/) — Anthropic CMS 泄露事件
-   [Check Point: Claude Code RCE Vulnerabilities](https://link.zhihu.com/?target=https%3A//research.checkpoint.com/2026/rce-and-api-token-exfiltration-through-claude-code-project-files-cve-2025-59536/) — Claude Code 安全漏洞分析
-   [Socket: Axios Supply Chain Attack](https://link.zhihu.com/?target=https%3A//socket.dev/blog/axios-npm-package-compromised) — Axios 供应链投毒事件分析
-   [StepSecurity: Axios Compromised on npm](https://link.zhihu.com/?target=https%3A//www.stepsecurity.io/blog/axios-compromised-on-npm-malicious-versions-drop-remote-access-trojan) — Axios 攻击链技术细节

[发布于 2026-03-31 19:35](//www.zhihu.com/question/2022392127145911515/answer/2022396606889170293)・日本

### 继续追问

由知乎直答提供

[

泄漏事件对开发者社区有何影响？

](https://zhida.zhihu.com/search?content_id=775515375&content_type=ANSWER&is_preview=1&q=%E6%B3%84%E6%BC%8F%E4%BA%8B%E4%BB%B6%E5%AF%B9%E5%BC%80%E5%8F%91%E8%80%85%E7%A4%BE%E5%8C%BA%E6%9C%89%E4%BD%95%E5%BD%B1%E5%93%8D%EF%BC%9F&zhida_source=below_banner_question)[

为何 Source Map 会泄露源代码？

](https://zhida.zhihu.com/search?content_id=775515375&content_type=ANSWER&is_preview=1&q=%E4%B8%BA%E4%BD%95+Source+Map+%E4%BC%9A%E6%B3%84%E9%9C%B2%E6%BA%90%E4%BB%A3%E7%A0%81%EF%BC%9F&zhida_source=below_banner_question)[

Anthropic 为何没有修复之前的泄漏问题？

](https://zhida.zhihu.com/search?content_id=775515375&content_type=ANSWER&is_preview=1&q=Anthropic+%E4%B8%BA%E4%BD%95%E6%B2%A1%E6%9C%89%E4%BF%AE%E5%A4%8D%E4%B9%8B%E5%89%8D%E7%9A%84%E6%B3%84%E6%BC%8F%E9%97%AE%E9%A2%98%EF%BC%9F&zhida_source=below_banner_question)

赞同 324​​23 条评论​284 ​12

​分享

​

​

收起​

#### 更多回答

[![Asher](https://picx.zhimg.com/v2-bc2b2d9c1f82584dcf281fdcd908144d_l.jpg?source=1def8aca)](//www.zhihu.com/people/han-ming-45-96)

[Asher](//www.zhihu.com/people/han-ming-45-96)

[​![知乎知识会员](https://picx.zhimg.com/v2-57fe7feb4813331d5eca02ef731e12c9.jpg?source=88ceefae)](https://www.zhihu.com/kvip/purchase)

何不来996.ninja摸鱼？

​ 关注

他们发 npm 包的时候，.npmignore 里没过滤 source map，导致打包进去的 .map 文件直接暴露了完整的 TypeScript 源码映射。

有开发者在 node\_modules 里翻到之后，还原出了 1900 多个文件——终端 CLI 架构、40 多个工具、50 来个命令，一目了然。

GitHub 上已经有人把这份代码打包上传了，Bun 运行时的接入方式、Anthropic SDK 的调用逻辑、权限控制设计、自然语言转代码的执行流程，全部对外可见。更尴尬的是，老版本就出过同样的问题。

需要的老哥们赶紧去github fork一下：[链接](https://link.zhihu.com/?target=https%3A//github.com/instructkr/claude-code)

---

没超过2小时，代码就已经被替换了

![](https://pic1.zhimg.com/50/v2-ab8f5d92478df063c78d560c7a7cb7cc_720w.jpg?source=1def8aca)

不过fork过的仓库还是能下载的，不行的话直接用我下载的这个：[https://file.gongju.dev/share/40b366c6a7](https://link.zhihu.com/?target=https%3A//file.gongju.dev/share/40b366c6a7)

送礼物

还没有人送礼物，鼓励一下作者吧

[编辑于 2026-03-31 22:08](//www.zhihu.com/question/2022392127145911515/answer/2022398444245886693)

赞同 93​​7 条评论​80 ​1

​分享

​

​

[![平凡](https://picx.zhimg.com/v2-9f81432bb5f397e14ec2c65e949eb0d3_l.jpg?source=1def8aca)](//www.zhihu.com/people/jzwa)

[平凡](//www.zhihu.com/people/jzwa)

[​![](https://pic1.zhimg.com/v2-4a07bc69c4bb04444721f35b32125c75_l.png?source=32738c0c)](https://www.zhihu.com/question/510340037)

新知答主

短的结论：泄露的仅为客户端工具源码，用户对话、API 密钥、个人信息零泄露，也就是对于个人来说没有损害，对于Anthropic伤害巨大。

下面的来源全部来自于：[https://github.com/Kuberwastaken/claude-code](https://link.zhihu.com/?target=https%3A//github.com/Kuberwastaken/claude-code)

**Claude Code 完整源代码通过 npm Source Map 泄露事件深度解析**

作者：Kuber Mehta | 发布日期：2026年3月31日

2026年3月31日，研究员 Chaofan Shou 在 X（原 Twitter）上发现了一件 Anthropic 大概不希望外界看到的事：Claude Code——Anthropic 官方 AI 编程 CLI 工具——的完整源代码，就躺在 npm 注册表里，藏于一个随包发布的 sourcemap 文件中，等着任何人去取。

本仓库是泄露源代码的备份，本文将全面解析：泄露内容是什么、泄露如何发生，以及我们因此得知的、那些本不应公开的内部信息。

## 一、这场泄露是怎么发生的？

当你将一个 JavaScript/TypeScript 包发布到 npm 时，构建工具链通常会生成 source map 文件（.map 文件）。这些文件的作用是在生产环境崩溃时，让堆栈追踪能定位到原始源代码的具体行，而不是指向压缩后的天书代码。

问题的关键在于：source map 包含原始源代码。不是引用，不是摘要，而是完整的、逐字逐句的原始源代码，以字符串形式嵌入在一个 JSON 文件里。

.map 文件的结构大致如下：

```text
{   "version": 3,   "sources": ["../src/main.tsx", "../src/tools/BashTool.ts", "..."],   "sourcesContent": ["// 每个文件的完整原始源代码", "..."],   "mappings": "AAAA,SAAS,OAAO..." }
```

那个 sourcesContent 数组？里面是一切：每个文件、每条注释、每个内部常量、每条系统提示，全部躺平在一个 npm 愉快地对任何运行 npm pack 或浏览包内容的人开放的 JSON 文件里。

这种攻击向量并不新鲜，以前发生过，将来还会再发生。

错误几乎总是同一个：有人忘记在 .npmignore 里加上 \*.map，或者没有配置构建工具在生产构建时跳过 source map 生成。Claude Code 使用的是 Bun 构建器，默认会生成 source map，除非你明确关闭。

最讽刺的是：代码里有一套名为「卧底模式」的完整子系统，专门防止 Anthropic 内部信息泄露。他们造了个系统来防止 AI 在 git 提交里意外暴露内部代号……然后把完整源代码装进了一个 .map 文件——很可能就是 Claude 干的。

## 二、Claude 的内部架构

Claude Code 从外部看是个精致但相对简单的命令行工具。从内部看，它是一个 785KB 的 main.tsx 入口文件、一个自定义 React 终端渲染器、40+ 个工具、一套多智能体编排系统、一个后台记忆整合引擎「dream」……以及更多。

## 三、BUDDY——你终端里的电子宠物

Claude Code 内置了一套完整的「电子宠物」系统，代号 BUDDY，通过编译时特性标志 BUDDY 开关控制。

这套系统有确定性扭蛋机制、物种稀有度、闪光变体、程序化生成属性，以及由 Claude 在首次孵化时创作的「灵魂描述」。

### 扭蛋系统

宠物物种由 Mulberry32 伪随机数生成器决定，以 userId 哈希为种子（加盐值 'friend-2026-401'），保证同一用户永远获得同一只宠物。

// Mulberry32 PRNG - 确定性，每用户可复现 function mulberry32(seed: number): () => number { return function() { seed |= 0; seed = seed + 0x6D2B79F5 | 0; var t = Math.imul(seed ^ seed >>> 15, 1 | seed); t = t + Math.imul(t ^ t >>> 7, 61 | t) ^ t; return ((t ^ t >>> 14) >>> 0) / 4294967296; } }

### 18 种物种（代码中已混淆）

物种名称通过 String.fromCharCode() 数组隐藏，完整列表如下：

稀有度

物种

普通（60%）

Pebblecrab, Dustbunny, Mossfrog, Twigling, Dewdrop, Puddlefish

罕见（25%）

Cloudferret, Gustowl, Bramblebear, Thornfox

稀有（10%）

Crystaldrake, Deepstag, Lavapup

史诗（4%）

Stormwyrm, Voidcat, Aetherling

传说（1%）

Cosmoshale, Nebulynx

此外还有独立的 1% 闪光概率，与稀有度无关。也就是说，闪光传说级 Nebulynx 的概率仅为 0.01%。

### 属性与灵魂

每只宠物都有程序化生成的 5 项属性：DEBUGGING（调试）、PATIENCE（耐心）、CHAOS（混乱）、WISDOM（智慧）、SNARK（毒舌），各 0-100。精灵以 5 行 12 字符宽的 ASCII 动画渲染在输入框旁边。

### 上线计划

代码显示 2026 年 4 月 1-7 日为预告窗口，正式上线计划于 2026 年 5 月。

## 四、KAIROS——「永远在线的 Claude」

在 assistant/ 目录下，有一个名为 KAIROS 的完整模式——一个持久运行、不需要你主动输入的 Claude 助手。它会监视、记录，并主动对观察到的事物采取行动。通过 PROACTIVE / KAIROS 编译时特性标志控制，对外发布版本中完全不存在。

### 运行机制

KAIROS 维护仅追加的每日日志文件，按固定间隔接收 <tick> 提示，自主决定是否主动行动或保持安静。系统设有 15 秒阻塞预算，任何会阻塞用户超过 15 秒的主动操作都会被推迟。

### KAIROS 专属工具

工具

功能

SendUserFile

直接向用户推送文件（通知、摘要等）

PushNotification

向用户设备发送推送通知

SubscribePR

订阅并监控拉取请求动态

## 五、ULTRAPLAN——30 分钟远程规划会话

ULTRAPLAN 是一种模式：Claude Code 将复杂规划任务转交给运行 Opus 4.6 的远程云容器（CCR）会话，最多给它 30 分钟思考，让你在浏览器里审批结果。

基本流程：Claude Code 识别需要深度规划的任务 → 启动远程 CCR 会话 → 终端显示轮询状态（每 3 秒检查一次）→ 浏览器 UI 让你实时观看并审批 → 审批后，特殊哨兵值 \_\_ULTRAPLAN\_TELEPORT\_LOCAL\_\_ 将结果「传送」回本地终端。

## 六、「Dream」系统——Claude 真的在做梦

Claude Code 有一套名为 autoDream（services/autoDream/）的系统——一个以 forked 子智能体形式运行的后台记忆整合引擎。命名绝非偶然，这就是 Claude 在做梦。

### 三重触发门控

-   时间门：距上次梦境已过 24 小时
-   会话门：距上次梦境已有至少 5 个会话
-   锁门：获取整合锁（防止并发做梦）  
    三重条件全部满足才会触发。

### **四个阶段**

-   第一阶段（定向）：ls 记忆目录，读取 MEMORY.md，浏览现有主题文件
-   第二阶段（采集最新信号）：寻找值得持久化的新信息，优先级：每日日志 → 漂移记忆 → 转录搜索
-   第三阶段（整合）：撰写或更新记忆文件，将相对日期转换为绝对日期，删除被矛盾的事实
-   第四阶段（剪枝与索引）：保持 MEMORY.md 不超过 200 行约 25KB，移除过时指针，解决矛盾  
    提示词里写道：「你正在进行一场梦境——对记忆文件的反思性遍历。将你最近学到的内容整合为持久、有序的记忆，让未来的会话能快速定向。」  
    

## **七、卧底模式——「不要暴露你的身份」**

  
Anthropic 员工（以 USER\_TYPE === 'ant' 标识）会用 Claude Code 在公开/开源仓库工作。卧底模式（utils/undercover.ts）防止 AI 意外在提交和 PR 中泄露内部信息。

激活后，系统提示中会注入以下内容：

> \## UNDERCOVER MODE - CRITICAL  
> You are operating UNDERCOVER in a PUBLIC/OPEN-SOURCE repository. Your commit  
> messages, PR titles, and PR bodies MUST NOT contain ANY Anthropic-internal  
> information. Do not blow your cover.  
>   
> NEVER include in commit messages or PR descriptions:  
> \- Internal model codenames (animal names like Capybara, Tengu, etc.)  
> \- Unreleased model version numbers (e.g., opus-4-7, sonnet-4-8)  
> \- Internal repo or project names  
> \- Internal tooling, Slack channels, or short links (e.g., go/cc, #claude-code-…)  
> \- The phrase "Claude Code" or any mention that you are an AI  
> \- Co-Authored-By lines or any other attribution

  
这由此确认了：Anthropic 员工正在积极使用 Claude Code 向开源项目贡献代码，且 AI 被要求隐瞒自己是 AI 的事实。内部模型代号是动物名——Capybara、Tengu 等。「Tengu」在代码中出现了数百次作为特性标志和分析事件的前缀，这几乎可以确定是 Claude Code 的内部项目代号。

## **八、多智能体编排——「协调者模式」**

Claude Code 在 coordinator/ 目录下有完整的多智能体编排系统，通过 CLAUDE\_CODE\_COORDINATOR\_MODE=1 激活。启用后，Claude Code 从单一智能体转变为协调者，并行生成、指挥、管理多个工作智能体。

阶段

执行者

目的

研究

工作智能体（并行）

调查代码库，定位文件，理解问题

综合

协调者

阅读发现结果，理解问题，制定规格

实施

工作智能体

按规格进行针对性修改并提交

验证

工作智能体

测试修改是否有效

  
提示词明确教导并行性：「并行性是你的超级能力。工作智能体是异步的。尽可能并发启动独立工作智能体——不要串行处理可以同时进行的工作。」

## **九、快速模式内部叫「企鹅模式」**

他们真的这么叫。utils/fastMode.ts 中的 API 端点字面量是：

> const endpoint = \`${getOauthConfig().BASE\_API\_URL}/api/claude\_code\_penguin\_mode\`

配置键是 penguinModeOrgEnabled，熔断开关是 tengu\_penguins\_off，失败时的分析事件是 tengu\_org\_penguin\_mode\_fetch\_failed。企鹅到底。

## **十、系统提示架构**

系统提示不是大多数应用中的单一字符串，而是由模块化的缓存片段在运行时组合而成（constants/）。

架构使用 SYSTEM\_PROMPT\_DYNAMIC\_BOUNDARY 标记，将提示拆分为：静态部分（跨组织可缓存）和动态部分（用户/会话特定内容）。

有一个函数叫 DANGEROUS\_uncachedSystemPromptSection()，专门用于你明确想要破坏缓存的易失性部分。仅凭命名惯例就能看出：某人曾经以惨痛的方式学到了这个教训。

**网络安全风险指令**

constants/cyberRiskInstruction.ts 中有一条特别有意思的内容，其头部有醒目警告：

重要：未经安全团队审核，请勿修改此指令 此指令归属于安全保障团队（David Forsythe, Kyla Guru）

于是我们现在知道了在 Anthropic 内部谁负责安全边界决策，以及这是由特定团队的具名个人管辖的。

## **十一、完整工具注册表——40+ 个工具**

工具

功能

AgentTool

生成子智能体

BashTool / PowerShellTool

Shell 执行（可选沙箱）

FileReadTool / FileEditTool / FileWriteTool

文件操作

GlobTool / GrepTool

文件搜索

WebFetchTool / WebSearchTool / WebBrowserTool

网络访问

NotebookEditTool

Jupyter Notebook 编辑

SkillTool

调用用户自定义技能

REPLTool

交互式 VM Shell

LSPTool

语言服务器协议通信

AskUserQuestionTool

向用户提问

EnterPlanModeTool / ExitPlanModeV2Tool

计划模式控制

SendMessageTool / TeamCreateTool / TeamDeleteTool

智能体群组管理

TaskCreateTool / TaskGetTool / ...

后台任务管理

ScheduleCronTool

定时任务调度

ConfigTool

修改设置（仅内部）

TungstenTool

高级功能（仅内部）

SendUserFile / PushNotification / SubscribePR

KAIROS 专属工具

阅读全文​

赞同 38​​1 条评论​32 ​喜欢

​分享

​

[查看全部 40 个回答](/question/2022392127145911515)

大家都在搜

换一换

[伊朗局势518 万](/search?q=%E4%BC%8A%E6%9C%97%E5%B1%80%E5%8A%BF&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)热

[鞠婧祎被实名举报偷税漏税414 万](/search?q=%E9%9E%A0%E5%A9%A7%E7%A5%8E%E8%A2%AB%E5%AE%9E%E5%90%8D%E4%B8%BE%E6%8A%A5%E5%81%B7%E7%A8%8E%E6%BC%8F%E7%A8%8E&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)热

[李荣浩喊话单依纯称其强行侵权《李白》374 万](/search?q=%E6%9D%8E%E8%8D%A3%E6%B5%A9%E5%96%8A%E8%AF%9D%E5%8D%95%E4%BE%9D%E7%BA%AF%E7%A7%B0%E5%85%B6%E5%BC%BA%E8%A1%8C%E4%BE%B5%E6%9D%83%E3%80%8A%E6%9D%8E%E7%99%BD%E3%80%8B&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)热

[张雪机车 WSBK葡萄牙站夺冠310 万](/search?q=%E5%BC%A0%E9%9B%AA%E6%9C%BA%E8%BD%A6+WSBK%E8%91%A1%E8%90%84%E7%89%99%E7%AB%99%E5%A4%BA%E5%86%A0&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)热

[张雪峰追悼会举行民众排长队送别298 万](/search?q=%E5%BC%A0%E9%9B%AA%E5%B3%B0%E8%BF%BD%E6%82%BC%E4%BC%9A%E4%B8%BE%E8%A1%8C%E6%B0%91%E4%BC%97%E6%8E%92%E9%95%BF%E9%98%9F%E9%80%81%E5%88%AB&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)

[重庆一隧道爆炸致4死9伤280 万](/search?q=%E9%87%8D%E5%BA%86%E4%B8%80%E9%9A%A7%E9%81%93%E7%88%86%E7%82%B8%E8%87%B44%E6%AD%BB9%E4%BC%A4&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)

[Claude Code 源码泄露277 万](/search?q=Claude+Code+%E6%BA%90%E7%A0%81%E6%B3%84%E9%9C%B2&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)热

[瑞幸新品喝一半发现椰肉变紫255 万](/search?q=%E7%91%9E%E5%B9%B8%E6%96%B0%E5%93%81%E5%96%9D%E4%B8%80%E5%8D%8A%E5%8F%91%E7%8E%B0%E6%A4%B0%E8%82%89%E5%8F%98%E7%B4%AB&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)

[郑丽文率国民党访问大陆245 万](/search?q=%E9%83%91%E4%B8%BD%E6%96%87%E7%8E%87%E5%9B%BD%E6%B0%91%E5%85%9A%E8%AE%BF%E9%97%AE%E5%A4%A7%E9%99%86&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)

[兰州大学考研初试401分被刷241 万](/search?q=%E5%85%B0%E5%B7%9E%E5%A4%A7%E5%AD%A6%E8%80%83%E7%A0%94%E5%88%9D%E8%AF%95401%E5%88%86%E8%A2%AB%E5%88%B7&search_source=Trending&utm_content=search_hot&utm_medium=organic&utm_source=zhihu&type=content)
