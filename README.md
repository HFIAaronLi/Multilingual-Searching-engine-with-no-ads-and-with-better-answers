[README-2.md](https://github.com/user-attachments/files/34210506/README-2.md)
# Multilingual-Searching-engine-with-no-ads-and-with-better-answers
# Terminal Search / 终端搜索

A bilingual terminal search tool with unrestricted-language search by default, ad filtering, result previews, and on-demand paragraph summaries.

一个默认不限搜索语言的中英双语终端搜索工具，支持广告过滤、结果预览，以及按需提取网页段落摘要。

## Improvements / 改进内容

- **Unrestricted language by default / 默认不限语言：** `auto` no longer guesses Chinese or English and does not add a language or region condition to the query. `auto` 不再把查询自动归为中英文，也不会给查询附加语言或地区条件。
- **Optional language setting / 可主动设置语言：** use commands such as `:lang zh`, `:lang en`, `:lang ja`, or `:lang fr`. 可使用 `:lang zh`、`:lang en`、`:lang ja`、`:lang fr` 等命令主动指定搜索语言。
- **Ad and junk filtering / 广告及垃圾内容过滤：** enabled by default; known advertising hosts and explicit ad labels are removed. 默认开启，会过滤已知广告域名和明确的广告标识。
- **Paragraph previews / 段落预览：** results show the beginnings of P1, P2, and Last when those text units are available. 结果会尽量分别显示首段、次段和末段的开头。
- **On-demand page summaries / 按需网页摘要：** `:summary <number>` fetches a selected page and extracts its first, second, and last paragraphs. `:summary <编号>` 会读取指定网页并提取首段、次段和末段。
- **Always bilingual / 始终双语：** the interface displays English first, followed by Chinese; there is no interface-language selection step. 界面固定为英文在前、中文在后，不需要选择界面语言。
- **More built-in engines / 更多内置引擎：** Google, Bing, DuckDuckGo, Yahoo, Yahoo Japan, Baidu, Brave, Ecosia, Yandex, Mojeek, and Sogou are available. 内置 Google、Bing、DuckDuckGo、Yahoo、雅虎日本、百度、Brave、Ecosia、Yandex、Mojeek 和搜狗。
- **Yahoo Global stays global / 全球 Yahoo 不再换站：** the built-in `yahoo` uses only `search.yahoo.com`. It keeps session cookies and retries that same global endpoint once after a 5xx response; it never substitutes Yahoo Japan. `yahoojp` remains a separate, explicitly selected engine. 内置 `yahoo` 只访问 `search.yahoo.com`，保留会话 Cookie，并在收到 5xx 后重试同一个全球入口一次，绝不会擅自改用雅虎日本；`yahoojp` 仍是需要明确选择的独立引擎。
- **Compatible static-page parsing / 静态网页解析兼容：** Google has a basic-HTML retry, DuckDuckGo supports HTML GET/POST and Lite, and Baidu can retry its mobile result page. Google 增加基本 HTML 重试；DuckDuckGo 支持 HTML GET／POST 和 Lite；百度可自动重试移动版结果页。
- **Specific page diagnostics / 明确的页面诊断：** `:errors` distinguishes CAPTCHA/security checks, consent pages, explicit no-results pages, unrecognized layouts, HTTP errors, and connection failures, and includes the page title and final URL when available. `:errors` 会区分验证码／安全检查、同意页、明确无结果、布局无法识别、HTTP 错误和连接失败，并尽量显示网页标题与最终地址。
- **Optional real-browser fallback / 可选真实浏览器回退：** `:browser on` retries failed static engines in Chromium using the original search URL, executes JavaScript, and keeps a separate persistent browser profile. It never changes Yahoo Global to Yahoo Japan, does not repeat HTTP 429 requests, and never solves CAPTCHA automatically. 开启 `:browser on` 后，失败的静态引擎会在 Chromium 中按原搜索地址重试、执行 JavaScript，并使用独立的持久浏览器配置。不会把全球 Yahoo 换成雅虎日本，不会对 HTTP 429 重复请求，也不会自动破解验证码。
- **Custom engine domains / 自定义域名引擎：** enter a domain such as `yahoo.hk`, `yahoo.co.jp`, or `baidu.com` directly in `:pool`; no provider editing is needed. 可在 `:pool` 中直接输入 `yahoo.hk`、`yahoo.co.jp`、`baidu.com` 等域名，无需修改程序。
- **Real next-page fetching / 真正的下一页：** when cached results run out, the program requests the next result page from the selected engines and removes repeated URLs. 缓存结果用完后，程序会向所选引擎请求下一页，并移除重复网址。
- **Transparent relevance and counts / 透明的相关性与数量统计：** every result shows its score; `:score`, `:stats`, and `:errors` explain ranking, result counts, and engine failures. 每条结果都会显示分数；`:score`、`:stats` 和 `:errors` 分别解释排序、结果数量和引擎失败原因。
- **More reliable operation / 运行更稳妥：** adds HTTP error checks, safer result numbers, page-bound checks, and clearer error messages. 增加网络错误检查、编号与翻页边界检查，以及更清楚的提示。

## Requirements / 环境要求

- Python 3.9 or newer / Python 3.9 或更新版本。
- macOS or Windows / macOS 或 Windows。
- An internet connection / 可用的网络连接。

No separate compilation step is required. Run the file with Python 3.

不需要单独编译，直接使用 Python 3 运行即可。

## 1. Save the program / 保存程序

Save the supplied file as **`tsearch.py`** on your Desktop. Keep it as a UTF-8 Python file.

将提供的文件以 **`tsearch.py`** 为名保存到桌面，并保持 UTF-8 编码。

Do not rename it to `tsearch.py.txt`, and do not paste Markdown fences such as ```` ```python ```` into the file.

不要把它保存成 `tsearch.py.txt`，也不要把 ```` ```python ```` 等 Markdown 标记复制进文件。

## 2A. macOS installation and launch / macOS 安装与运行

Open **Terminal**. The following commands use a virtual environment, so they do not modify the system Python and do not require activating the environment.

打开“终端”。以下命令使用独立的虚拟环境，不修改系统 Python，也不需要执行环境激活命令。

### Check Python 3 / 检查 Python 3

```bash
python3 --version
```

If Terminal says `python3: command not found`, install Python 3 from <https://www.python.org/downloads/macos/>, then close and reopen Terminal.

如果提示 `python3: command not found`，请先从上述 Python 官网安装 Python 3，然后关闭并重新打开终端。

### Go to Desktop / 进入桌面目录

```bash
cd ~/Desktop
```

### Create an isolated environment / 创建独立环境

```bash
python3 -m venv .tsearch-venv
```

### Install dependencies / 安装依赖

```bash
.tsearch-venv/bin/python -m pip install requests beautifulsoup4 rich
```

PyYAML is no longer required.

新版不再需要 PyYAML。

### Launch / 启动

```bash
.tsearch-venv/bin/python tsearch.py
```

For later runs, only these two commands are needed:

以后再次运行时，只需执行：

```bash
cd ~/Desktop
.tsearch-venv/bin/python tsearch.py
```

## 2B. Windows installation and launch / Windows 安装与运行

Open **Windows Terminal** or **PowerShell**. These commands also use an isolated environment and do not require changing PowerShell's execution policy.

打开“Windows 终端”或 PowerShell。以下命令同样使用独立环境，不需要修改 PowerShell 执行策略。

### Check Python / 检查 Python

```powershell
py --version
```

If `py` is unavailable, try `python --version`; in the next command, replace `py` with `python`.

如果 `py` 不可用，请尝试 `python --version`，并在下一条创建环境的命令中用 `python` 替代 `py`。

### Go to Desktop / 进入桌面目录

```powershell
cd "$env:USERPROFILE\Desktop"
```

### Create an isolated environment / 创建独立环境

```powershell
py -m venv .tsearch-venv
```

### Install dependencies / 安装依赖

```powershell
.tsearch-venv\Scripts\python.exe -m pip install requests beautifulsoup4 rich
```

### Launch / 启动

```powershell
.tsearch-venv\Scripts\python.exe tsearch.py
```

For later runs, only these two commands are needed:

以后再次运行时，只需执行：

```powershell
cd "$env:USERPROFILE\Desktop"
.tsearch-venv\Scripts\python.exe tsearch.py
```

## 2C. Optional Chromium fallback / 可选 Chromium 浏览器回退

**The basic installation does not need Playwright or Chromium. Install this section only if you want failed static engines to be rendered in a real browser.**

**基本安装不需要 Playwright 或 Chromium。只有希望静态失败的引擎改用真实浏览器渲染时，才需要安装本节的组件。**

macOS:

```bash
.tsearch-venv/bin/python -m pip install playwright
.tsearch-venv/bin/python -m playwright install chromium
```

Windows PowerShell:

```powershell
.tsearch-venv\Scripts\python.exe -m pip install playwright
.tsearch-venv\Scripts\python.exe -m playwright install chromium
```

Then start the program normally and enable the feature once:

随后正常启动程序，并开启一次功能即可：

```text
:browser on
```

The setting is saved. Use `:browser off` to disable it. Chromium opens only after a static engine failure, not for engines that already returned results.

该设置会自动保存，输入 `:browser off` 可关闭。Chromium 只会在静态引擎失败后打开，不会重复抓取已经成功返回结果的引擎。

## 3. Basic use / 基本使用

When you see the following prompt, enter a query in any language:

看到以下提示后，可以用任意语言输入搜索内容：

```text
Search 搜索 >
```

Examples / 示例：

```text
Python decorators
巴黎 旅游
東京 ラーメン
inteligencia artificial
```

Enter only the topic you want to search. Do not paste the program's yellow engine-failure warning back into the search prompt as a query. Commands such as `:errors` are entered on their own line.

只需输入真正想搜索的主题，不要把程序黄色的引擎失败警告再粘贴为搜索内容。`:errors` 等命令应单独输入一行。

Type `:help` to see all commands, and `:exit` or `q` after a colon (`:q`) to quit.

输入 `:help` 查看全部命令；输入 `:exit` 或 `:q` 退出。

## 4. Commands / 命令

| Command / 命令 | Function / 功能 |
| --- | --- |
| `:new` | Start a new topic / 开始新话题 |
| `:next` or `n` / `:next` 或 `n` | Show cached results or fetch the next engine page / 展示缓存或抓取引擎下一页 |
| `:prev` or `p` / `:prev` 或 `p` | Previous page / 上一页 |
| `:open 1` | Open result 1 in the browser / 在浏览器中打开第 1 条结果 |
| `:summary 1` | Extract a paragraph summary from result 1 / 提取第 1 条结果网页的段落摘要 |
| `:score 1` | Show the relevance formula and matching tokens for result 1 / 查看第 1 条结果的相关性计算式和命中词元 |
| `:stats` | Show received, filtered, duplicate, and retained result counts / 查看抓取、过滤、重复和保留数量 |
| `:errors` | Show detailed engine connection or parsing errors / 查看引擎连接或解析错误详情 |
| `:pool` | Show available engines and the current pool / 查看可用引擎和当前搜索池 |
| `:pool bing,baidu` | Use Bing and Baidu / 使用 Bing 和百度 |
| `:pool google,yahoo.co.jp,baidu.com` | Mix built-in engines and custom domains / 混合使用内置引擎与自定义域名 |
| `:pool reset` | Restore the expanded default pool / 恢复扩展后的默认搜索池 |
| `:lang auto` | Remove the explicit language setting / 取消主动语言设置 |
| `:lang ja` | Request Japanese results / 请求日文搜索结果 |
| `:lang zh-CN` | Request Simplified Chinese results / 请求简体中文搜索结果 |
| `:filter on` | Enable ad and junk filtering / 开启广告及垃圾内容过滤 |
| `:filter off` | Disable filtering / 关闭过滤 |
| `:browser on` | Enable Chromium fallback after static engine failures / 静态引擎失败后启用 Chromium 回退 |
| `:browser off` | Disable browser fallback / 关闭浏览器回退 |
| `:exit` or `:q` | Quit / 退出 |

The search language, pool, custom engines, filtering setting, and browser-fallback setting are saved in `.tsearch.json` in your home directory.

搜索语言、搜索池、自定义引擎、过滤设置和浏览器回退设置会保存在用户主目录下的 `.tsearch.json` 中。

### Language behavior / 语言行为说明

`auto` means no additional language restriction. Other language codes are passed to engines that support language or regional preferences. Search engines can still occasionally return pages in other languages; Baidu does not provide a general language-control parameter in this tool.

`auto` 表示不附加语言限制。其他语言代码会传递给支持语言或地区设置的引擎。搜索引擎仍可能偶尔返回其他语言的网页；本工具中的百度搜索没有通用的语言控制参数。

This setting never changes the bilingual interface.

该设置不会改变中英双语界面。

### Filtering and summaries / 过滤与摘要说明

Filtering is enabled by default. If you are researching advertising itself and believe a useful result was removed, use `:filter off`.

广告过滤默认开启。如果你正在研究广告相关内容，并认为有用结果被误过滤，可使用 `:filter off`。

The search table builds its short preview from search-result text. Use `:summary <number>` to read the selected public page and show the beginnings of its first, second, and last available paragraphs. Sites that require login, block automated access, use only JavaScript-rendered text, or return non-HTML content may not be summarizable.

结果表格中的简短预览来自搜索结果文本。使用 `:summary <编号>` 可读取对应的公开网页，并显示首段、次段和末段的开头。需要登录、阻止自动访问、仅通过 JavaScript 生成正文，或返回非 HTML 内容的网站可能无法生成摘要。

### Real pagination and result counts / 真正的分页与结果数量

The first search reads the first result page from each selected engine. Each provider contributes up to 10 parsed results per fetch. The program then removes invalid entries, explicit ads or junk when filtering is enabled, and duplicate URLs. It does **not** remove results for having a low relevance score.

首次搜索会读取每个所选引擎的第一页。每个引擎每次最多提供 10 条可解析结果，随后程序会移除无效条目、过滤开启时的明确广告或垃圾内容，以及重复网址。**不会因为相关性分数低而删除结果。**

If more than 10 results are already loaded, `:next` first moves through that local cache. When the cache is exhausted, `:next` requests the next page from the engines. New URLs are appended; repeated URLs are not presented as a new page. If a fetch produces no new URLs, the program reports that there are no more new results.

如果已经加载超过 10 条结果，`:next` 会先浏览本地缓存。缓存用完后，`:next` 会向引擎请求下一页，并追加新网址；重复网址不会被伪装成新的一页。如果一次抓取没有产生新网址，程序会明确提示没有更多新结果。

Use `:stats` to see exactly why a batch has a particular size. For example, 10 received results minus 1 duplicate means 9 retained results. If an engine only returned 9 readable results, the statistics will show 9 received instead.

使用 `:stats` 可以准确查看某批结果数量的来源。例如，引擎返回 10 条、重复 1 条，最终就是 9 条。如果引擎本身只返回 9 条可解析结果，统计中会直接显示收到 9 条。

### Relevance score / 相关性分数

Every result row includes a `Score / 相关度` value. Use `:score <number>` to see the exact tokens, hit counts, and formula for that result.

每条结果都会显示 `Score / 相关度`。使用 `:score <编号>` 可以查看该结果的具体词元、命中数量和计算式。

```text
Score = (3 × number of query tokens matched in the title
         + number of query tokens matched in the snippet)
        / number of unique query tokens

分数 =（3 × 标题命中的查询词元数 + 摘要命中的查询词元数）
        ÷ 查询的不重复词元数
```

The theoretical range is **0–4**. It is a lightweight ranking index, not a probability, percentage, or neural semantic-similarity score. A score of zero does not delete a result.

理论范围是 **0–4**。它是轻量排序指数，不是概率、百分比，也不是神经网络语义相似度。即使分数为 0，结果也不会被删除。

Text is normalized and lowercased before matching. Latin and other word-based text uses Unicode word tokens. Chinese, Japanese, and Korean text additionally uses whole words, single characters, and adjacent two-character bigrams. Repeated occurrences of the same token count only once because matching uses sets.

匹配前会规范化文本并转为小写。拉丁字母等按词书写的文本使用 Unicode 词元；中日韩文本还会使用整词、单字和相邻二字词元。由于命中通过集合计算，同一个词元重复出现不会重复计分。

For example, with query `red apple`, title `red`, and snippet `apple`, there are two query tokens, one title hit, and one snippet hit: `(1 × 3 + 1 × 1) / 2 = 2.0`.

例如，查询为 `red apple`、标题为 `red`、摘要为 `apple` 时，共有两个查询词元，标题和摘要各命中一个，因此分数为 `(1 × 3 + 1 × 1) / 2 = 2.0`。

## 5. Search engines / 搜索引擎

### Start with no setup / 无需设置，直接使用

The default pool now searches Google, Bing, DuckDuckGo, Yahoo, Baidu, and Brave at the same time. You do not need to configure an engine before typing a query.

默认搜索池现在会同时使用 Google、Bing、DuckDuckGo、Yahoo、百度和 Brave。输入搜索内容前不需要配置引擎。

To see every available engine and your current pool:

查看全部引擎和当前搜索池：

```text
:pool
```

To restore the default pool at any time:

随时可用以下命令恢复默认搜索池：

```text
:pool reset
```

### Choose built-in engines / 选择内置引擎

Available names are:

可用名称如下：

```text
google, bing, duckduckgo, yahoo, yahoojp, baidu, brave,
ecosia, yandex, mojeek, sogou
```

Examples / 示例：

```text
:pool google
:pool google,bing,yahoo
:pool yahoojp
:pool bing,baidu,sogou
:pool google,ecosia,mojeek
```

Setting `:pool` replaces the current pool, so include every engine you want to use. If you normally use Google, Yahoo, Bing, DuckDuckGo, or Ecosia through Safari, choose the same engine name here; Safari itself is the browser rather than a separate search provider in this tool.

设置 `:pool` 会替换当前搜索池，因此需要列出所有想使用的引擎。如果你平时通过 Safari 使用 Google、Yahoo、Bing、DuckDuckGo 或 Ecosia，在这里选择对应名称即可；Safari 本身是浏览器，不是本工具中的独立搜索提供方。

### Add your own engine by domain / 通过域名添加自己的引擎

Type the domain directly after `:pool`. Do not edit the source code.

把域名直接写在 `:pool` 后面即可，不需要修改源代码。

```text
:pool yahoo.hk
:pool yahoo.co.jp
:pool google,yahoo.co.jp,baidu.com
:pool https://search.yahoo.co.jp
```

For Yahoo Japan alone, use `:pool yahoojp`. Its actual search endpoint is `search.yahoo.co.jp`. If you previously entered `yahoo.jp`, the program treats that as a Yahoo Japan alias, displays the corrected `yahoo.co.jp` name, and migrates the saved custom-engine entry.

仅使用雅虎日本时，可输入 `:pool yahoojp`。实际搜索地址为 `search.yahoo.co.jp`。如果此前输入过 `yahoo.jp`，程序会将其作为雅虎日本别名，显示更正后的 `yahoo.co.jp`，并迁移已保存的自定义引擎条目。

The built-in `:pool yahoo` is different: it requests only Yahoo Global at `search.yahoo.com`. A 5xx response causes one retry of that same address with the same query and page number. It never switches to Yahoo Japan. The Source column reads `yahoo.com`; if the global endpoint still fails, `:errors` reports that actual failure.

内置 `:pool yahoo` 的行为不同：它只请求全球入口 `search.yahoo.com`。收到 5xx 后，会使用相同查询和页码重试同一个地址，不会切换到雅虎日本。来源栏显示 `yahoo.com`；如果全球入口仍然失败，`:errors` 会报告这个真实失败。

Custom engines are saved automatically and appear under `Custom engines / 自定义引擎` the next time you run `:pool`.

自定义引擎会自动保存；下次输入 `:pool` 时，会显示在“Custom engines / 自定义引擎”一栏。

Enter a domain only, with an optional `http://` or `https://` prefix. The program recognizes several common search sites and otherwise tries a standard search address plus a general result parser. It follows redirects returned by the website. Apart from the explicitly documented `yahoo.jp` to `yahoo.co.jp` alias, it does not substitute a different regional engine on your behalf.

只需输入域名，也可以加上 `http://` 或 `https://` 前缀。程序会识别多个常见搜索网站；对于其他网站，会尝试常见的搜索地址和通用结果解析。网站自身返回跳转时，程序会跟随跳转。除了上面明确说明的 `yahoo.jp` 至 `yahoo.co.jp` 别名外，不会擅自替你换成其他地区的引擎。

A custom engine can still fail because of network access, regional availability, CAPTCHA checks, login requirements, or an unsupported page layout. This is reported as an engine failure; it does not stop the other engines.

自定义引擎仍可能因网络连接、地区可用性、验证码、登录要求或网页结构不受支持而失败。程序会显示该引擎失败，但不会影响其他引擎。

### SearXNG: optional; most people can skip it / SearXNG：可选项，大多数人可跳过

**You do not need SearXNG. If you do not already use it, ignore this subsection and no address configuration is needed.**

**你不需要安装或配置 SearXNG。如果你本来就没有使用它，直接跳过本小节即可，也不需要填写任何地址。**

Only if you already have a running SearXNG service, you can add it like any other engine:

只有已经运行 SearXNG 服务的人，才需要像下面这样把它加入搜索池：

```text
:pool searxng
:pool bing,searxng
```

If it does not connect, use `:pool reset` and continue with the normal engines.

如果无法连接，输入 `:pool reset`，继续使用普通搜索引擎即可。

### Network availability / 网络可用性

Any search engine may be unreachable on a particular network. A failed, timed-out, CAPTCHA-blocked, or unreadable engine is listed in a warning while the remaining engines can still return results.

任何搜索引擎都可能在特定网络下无法连接。失败、超时、被验证码拦截或无法解析的引擎会显示在警告中，其他引擎仍可正常返回结果。

Use `:errors` after a search to distinguish DNS failure, connection timeout, HTTP 429 rate limiting, other HTTP errors, CAPTCHA/security verification, consent pages, explicit no-results responses, and unrecognized result layouts. For a returned web page, the diagnostic includes its HTTP status, title, and final URL after redirects. A layout error is no longer described as proof that there are no more results.

搜索后使用 `:errors` 可以区分域名解析失败、连接超时、HTTP 429 限流、其他 HTTP 错误、验证码／安全验证、同意页、网站明确返回无结果，以及结果布局无法识别。对于已经返回的网页，诊断会显示 HTTP 状态、网页标题和跳转后的最终地址。布局无法识别不再被当作“没有更多结果”的确定证据。

### Why a browser can work when static parsing fails / 为什么浏览器能用而程序可能无法解析

The program requests a search endpoint and parses the returned HTML; it is not reading the page currently displayed by Safari, Chrome, or another browser. A browser may already have cookies, execute JavaScript, complete a consent flow or CAPTCHA, and receive a different HTML layout. An HTTP 200 response only means that a page arrived—it does not prove that the page contains search results.

程序会请求搜索入口并解析返回的 HTML，并不是读取 Safari、Chrome 等浏览器当前显示的画面。浏览器可能已有 Cookie、能够执行 JavaScript、已经完成同意流程或验证码，并收到不同的 HTML 布局。HTTP 200 只表示收到了网页，并不能证明网页中有搜索结果。

The revised program handles readable desktop, mobile, basic-HTML, and Lite layouts where possible and retries the documented alternate endpoints listed above. It does not bypass CAPTCHA or consent checks. When those are returned, `:errors` now says so explicitly instead of pretending that the engine had no results.

新版会尽量兼容可读的桌面版、移动版、基本 HTML 和 Lite 布局，并尝试上面列出的备用入口，但不会绕过验证码或同意确认。网站返回这些验证页时，`:errors` 会明确说明，不再假装引擎没有搜索结果。

### Real browser fallback / 真实浏览器回退

After installing the optional components in section 2C, enter `:browser on`. When a static engine fails, the program opens that engine's original search URL in Chromium and parses the rendered DOM after JavaScript runs. It uses one browser sequentially rather than launching one browser per failed engine. Results obtained this way have a Source value such as `browser:google`, `browser:ddg-html`, or `browser:yahoo.com`.

按照 2C 节安装可选组件后，输入 `:browser on`。静态引擎失败时，程序会在 Chromium 中打开该引擎的原搜索地址，并在 JavaScript 执行后解析渲染完成的 DOM。多个失败引擎会顺序使用同一个浏览器，不会每个引擎都启动一个浏览器。通过此方式取得的结果，来源会显示为 `browser:google`、`browser:ddg-html` 或 `browser:yahoo.com` 等。

The browser profile is stored separately in `.tsearch-browser-profile` in your home directory. It preserves cookies between runs but does not read, copy, or modify your Safari, Chrome, or Edge personal profile. If a CAPTCHA or consent page appears, complete it yourself in the opened Chromium window; the program waits up to 90 seconds. It does not automatically solve CAPTCHA.

浏览器配置独立保存在主目录的 `.tsearch-browser-profile` 中，可在多次运行间保留 Cookie，但不会读取、复制或修改你的 Safari、Chrome 或 Edge 个人配置。如果出现验证码或同意页，需要你在打开的 Chromium 窗口中亲自完成，程序最多等待 90 秒，不会自动破解验证码。

HTTP 429 responses are not retried through Chromium. Browser rendering also cannot guarantee access when the network is unreachable or the website continues to return HTTP 500. In those cases, `:errors` retains both the static and browser failure details. Use `:browser off` to return to static-only operation.

HTTP 429 不会通过 Chromium 再次请求。网络无法连接或网站持续返回 HTTP 500 时，浏览器渲染也不能保证成功；此时 `:errors` 会同时保留静态请求和浏览器回退的失败详情。输入 `:browser off` 可恢复仅静态请求模式。

## 6. Troubleshooting / 故障排查

### Yahoo shows HTTP 500 or INKApi Error / Yahoo 显示 500 或 INKApi Error

HTTP 500 means the global endpoint returned an error rather than a result page, so a static result parser cannot turn that response into search results. The built-in `yahoo` retries the same `search.yahoo.com` request once and retains session cookies. It does not conceal the error by switching to Yahoo Japan. With `:browser on`, it can then try the same global URL in Chromium; if that also fails, `:errors` reports both failures.

HTTP 500 表示全球入口返回的是错误而非结果页，静态解析器无法把这种响应变成搜索结果。内置 `yahoo` 会重试同一个 `search.yahoo.com` 请求一次并保留会话 Cookie，不会通过切换到雅虎日本来掩盖错误。开启 `:browser on` 后，还可以用 Chromium 尝试同一个全球地址；如果仍然失败，`:errors` 会同时报告两次失败。

### Baidu, Google, or DuckDuckGo returns a verification page / 百度、Google 或 DuckDuckGo 返回验证页

The built-in providers retry Baidu Mobile, Google basic HTML, or DuckDuckGo HTML/Lite as applicable. Being in Japan does not itself create or remove a Baidu verification requirement; the website decides that for each connection and session. If all static endpoints return verification or consent pages, enable the optional `:browser on` fallback and complete the challenge yourself in Chromium. Without browser fallback, the program reports the verification page rather than treating it as an empty result set.

内置引擎会按情况重试百度移动版、Google 基本 HTML 或 DuckDuckGo HTML／Lite。身在日本本身不会必然产生或解除百度的验证要求，网站会针对每次连接和会话自行判断。如果所有静态入口都返回验证或同意页，可开启可选的 `:browser on`，并在 Chromium 中亲自完成验证。未开启浏览器回退时，程序会如实报告验证页，而不是把它当成空结果。

### Brave HTTP 429 / Brave 返回 429

This is rate limiting, not a result-layout problem. Wait before using Brave again. The program deliberately does not retry a 429 response through Chromium, because sending the same request through another client immediately can worsen the limiting.

这是访问频率限制，不是结果布局问题。请等待一段时间再使用 Brave。程序故意不通过 Chromium 重试 429，因为立即换客户端重复请求可能加重限流。

### Why did the original fail in macOS Terminal? / 原版为什么在苹果终端中失败？

The pasted original source passes a Python 3 syntax check, so a definite cause cannot be identified without the actual Terminal error. The most common causes are using `python` instead of `python3`, missing packages, running from the wrong directory, a `.txt` suffix, or accidentally saving Markdown fences with the code.

你贴出的原版代码可以通过 Python 3 语法检查，因此没有实际报错信息时，无法断定唯一原因。常见原因包括：误用 `python` 而不是 `python3`、缺少依赖、运行目录不正确、文件带有 `.txt` 后缀，或把 Markdown 代码标记一起保存了进去。

The installation commands above avoid these issues by using an explicit Python 3 environment and its full interpreter path.

上述安装命令通过明确的 Python 3 环境和完整解释器路径来避开这些问题。

### `No module named requests`, `bs4`, or `rich` / 提示缺少模块

Install dependencies with the same interpreter that launches the program. The commands in sections 2A and 2B already do this.

请使用启动程序的同一个 Python 解释器安装依赖。2A 和 2B 中的命令已经按此方式处理。

### `externally-managed-environment` on macOS / macOS 提示环境受系统管理

Use the virtual-environment commands in section 2A instead of installing packages into Homebrew or system Python.

请使用 2A 中的虚拟环境命令，不要直接向 Homebrew 或系统 Python 安装软件包。

### `can't open file` or `No such file or directory` / 找不到文件

Check that Terminal is in the folder containing `tsearch.py`:

请确认终端当前目录中存在 `tsearch.py`：

- macOS: run `ls` / macOS：执行 `ls`。
- Windows: run `dir` / Windows：执行 `dir`。

Then use `cd` to enter the actual folder where the file is saved.

如果文件不在当前目录，请用 `cd` 进入实际保存位置。

### `Permission denied` on macOS / macOS 提示权限不足

Do not run `./tsearch.py`. Launch it through Python as shown:

不要直接执行 `./tsearch.py`，请按以下方式通过 Python 启动：

```bash
.tsearch-venv/bin/python tsearch.py
```

### A `SyntaxError` appears / 出现语法错误

Use the supplied `tsearch.py` directly, make sure the file contains Python code only, and launch it with Python 3 rather than Python 2.

请直接使用提供的 `tsearch.py`，确保文件中只有 Python 代码，并使用 Python 3 而不是 Python 2 启动。
