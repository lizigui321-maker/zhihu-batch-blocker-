# ☢️ Zhihu Nuke Protocol | 一键拉黑知乎回答全部点赞者

> **“一次点击，物理超度。把赛博垃圾扫进历史的垃圾堆。”**

**Zhihu Nuke Protocol** 是一个带有硬核“黑客终端”视觉风格的浏览器书签脚本（Bookmarklet）。它可以帮助你一键批量拉黑知乎某个回答或专栏文章下的**所有点赞用户**，并支持自动**优先拉黑原作者**，彻底净化你的知乎时间线。

![Version](https://img.shields.io/badge/VER-3.1_Pro-00ff41?style=for-the-badge&logo=terminal)
![Build](https://img.shields.io/badge/BUILD-2026.06.09-00ff41?style=for-the-badge&logo=github)

---

## ✨ 核心功能 (Features)

* **💻 沉浸式赛博终端 UI：** 告别简陋的系统弹窗！脚本自带悬浮毛玻璃霓虹黑客面板，实时打印终端执行日志，配备 ASCII 字符进度条。
* **🎯 擒贼先擒王 (Author First)：** 自动抓取当前页面的作者信息。若非匿名用户，脚本将优先对其实施“核打击”（拉黑）。
* **⚙️ 全场景双模引擎：** 完美兼容知乎**「回答详情页」** (`/answer/...`) 与**「专栏文章页」** (`zhuanlan.../p/...`)，智能切换底层 API 协议。
* **🛡️ 防呆拦截机制：** 如果在错误的页面（如首页、问题列表）误触脚本，将自动拦截并在终端输出错误日志，避免无效请求。

---

## 🚀 安装与使用教程 (Usage)

无需安装任何浏览器插件（如 Tampermonkey），只需将其添加为浏览器书签即可。

### 步骤一：创建一键执行书签
1. 在浏览器的书签栏上点击**右键**，选择 **“添加网页” / “添加书签”**。
2. 将 **名称 (Name)** 修改为你能认出的名字，例如：`☢️ 净化协议`。
3. 将 **网址 (URL)** 栏清空，并**完整复制下方代码框中的所有内容**，粘贴进去并保存。

```javascript
javascript:(async()=>{const e=document.getElementById("zh-nuke-panel");e&&e.remove();const t=document.createElement("div");t.id="zh-nuke-panel",t.style.cssText="position:fixed;top:20px;right:20px;width:360px;background:rgba(5,5,5,0.95);color:#00ff41;padding:20px;border:1px solid #00ff41;border-radius:6px;z-index:2147483647;font-family:'Courier New',Courier,monospace;font-size:13px;box-shadow:0 0 15px rgba(0,255,65,0.4),inset 0 0 10px rgba(0,255,65,0.2);line-height:1.6;backdrop-filter:blur(5px);",t.innerHTML='<div style="text-align:center;margin-bottom:10px;"><strong style="font-size:16px;letter-spacing:2px;text-shadow:0 0 5px #00ff41;">> NUKE PROTOCOL <</strong></div><div style="display:flex;justify-content:space-between;font-size:11px;color:#0aa;margin-bottom:2px;font-weight:bold;"><span>[ AUTHOR: Gemini ]</span><span>[ PM: Rick ]</span></div><div style="display:flex;justify-content:space-between;font-size:11px;color:#0aa;margin-bottom:8px;font-weight:bold;"><span>[ VER: 3.1 Pro ]</span><span>[ BUILD: 2026.06.09 ]</span></div><div style="border-bottom:1px dashed #00ff41;margin-bottom:10px;"></div><div id="zh-nuke-content" style="white-space:pre-wrap;word-wrap:break-word">> SYSTEM BOOTING... <span id="zh-cursor">_</span></div>',document.documentElement.appendChild(t);const a=document.getElementById("zh-nuke-content"),n=document.createElement("style");n.innerHTML="@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}#zh-cursor{animation:blink 1s step-end infinite}",document.head.appendChild(n);const o=(e,t=!1)=>{a.innerHTML=e+(t?"":" <span id='zh-cursor'>_</span>")},r=e=>new Promise((t=>setTimeout(t,e))),s=(e,t)=>{if(0===t)return"[--------------------] 0%";const a=Math.min(1,e/t),n=Math.round(20*a),o="█".repeat(n)+"<span style='color:#004411'>░".repeat(20-n)+"</span>";return`[${o}] <span style="color:#fff;text-shadow:0 0 5px #fff">${Math.floor(100*a)}%</span>`},l=()=>{const e=document.createElement("button");e.innerText="[ DISCONNECT & EXIT ]",e.style.cssText="margin-top:15px;padding:8px 10px;background:transparent;color:#00ff41;border:1px solid #00ff41;border-radius:3px;font-family:'Courier New',monospace;font-weight:bold;cursor:pointer;width:100%;text-align:center;transition:all 0.3s;box-shadow:inset 0 0 5px rgba(0,255,65,0.3);",e.onmouseover=()=>{e.style.background="#00ff41",e.style.color="#000"},e.onmouseout=()=>{e.style.background="transparent",e.style.color="#00ff41"},e.onclick=()=>{t.remove(),n.remove()},t.appendChild(e)};const i=location.href;let c,d;const u=i.match(/question\/\d+\/answer\/(\d+)/),p=i.match(/zhihu\.com\/p\/(\d+)/);if(u)c="answers",d=u[1];else{if(!p)return o("> <span style='color:#f00;font-weight:bold'>[ ERROR: INVALID TARGET AREA ]</span>\n> 目标未锁定！拦截协议启动失败。\n> <span style='color:#ff0'>请先点击进入具体的【回答详情页】\n> 或【专栏文章页】后，再执行此协议。</span>\n> CURRENT STATUS: STANDBY...",!0),void l();c="articles",d=p[1]}let m=["|","/","-","\\"],h=0;try{let e=0;o("> <span style='color:#0aa'>LOCATING AUTHOR...</span>");let t=await fetch(`https://www.zhihu.com/api/v4/${c}/${d}?include=author`);if(t.ok){const a=await t.json(),n=a.author;n&&n.url_token&&"0"!==n.url_token?(o(`> TARGET (AUTHOR): <span style='color:#fff'>${n.name}</span>\n> ACTION: <span style='color:#f00;animation:blink .5s infinite'>[ NUKING ]</span>`),await fetch(`https://www.zhihu.com/api/v4/members/${n.url_token}/actions/block`,{method:"POST"}),e++,await r(1000)):(o("> AUTHOR IS ANONYMOUS. <span style='color:#ff0'>SKIPPING</span>..."),await r(1000))}let a=0,n=!1,i=0,u=0,f="upvoters";for(;!n;){let t=await fetch(`https://www.zhihu.com/api/v4/${c}/${d}/${f}?limit=10&offset=${a}`);if(!t.ok&&"upvoters"===f&&"articles"===c&&(f="likers",t=await fetch(`https://www.zhihu.com/api/v4/${c}/${d}/${f}?limit=10&offset=${a}`)),!t.ok){o("> <span style='color:#f00'>ERROR: CONNECTION REFUSED.</span>",!0);break}const b=await t.json(),k=Array.isArray(b.data)?b.data:[];0===a&&(i=b.paging&&"number"==typeof b.paging.totals?b.paging.totals:k.length);for(const t of k)u++,e++,h=(h+1)%4,o(`> TARGET: <span style='color:#fff'>${t.name}</span>\n> STATUS: <span style='color:#f00'>EXTERMINATING ${m[h]}</span>\n> PROGRESS: [${u}/${i}]\n> ${s(u,i)}`),await fetch(`https://www.zhihu.com/api/v4/members/${t.url_token}/actions/block`,{method:"POST"}),await r(1000);if(n=!!(b.paging&&b.paging.is_end),a+=10,n)o(`> <span style='color:#0f0'>MISSION ACCOMPLISHED.</span>\n> TOTAL NEUTRALIZED: <span style='color:#fff'>${e}</span>\n> AWAITING COMMAND...`,!0),l()} }catch(e){o(`> <span style='color:#f00'>FATAL ERROR:</span> ${e.message}`,!0),l()}})();
```
*(注意：请确保复制的内容以 `javascript:` 开头)*

### 步骤二：发动协议
1. 日常浏览知乎时，如果遇到想要清理的内容，请点击进入具体的 **回答详情页** (网址形如 `.../answer/...`) 或 **专栏文章页** (网址形如 `.../p/...`)。
2. 直接点击你刚才在书签栏保存的 `☢️ 净化协议` 书签。
3. 坐和放宽，欣赏黑客终端面板自动为你执行清理任务。任务完成后，点击 `[ DISCONNECT & EXIT ]` 即可关闭终端。

---

## ⚠️ 风险警告与免责声明

* **风控说明：** 脚本内置了 1 秒/人的操作间隔以模拟人类操作，但短时间内大量、频繁地调用拉黑接口，仍**可能触发知乎的反滥用风控机制**（表现为暂时无法拉黑、需要输入验证码或账号被临时限制）。请适度使用，切勿过载。
* **免责条款：** 本脚本仅作为 JavaScript 自动化技术的学习与交流示例。使用者需自行承担因使用本脚本可能带来的账号风险。

---

## 👨‍💻 Credits

* **Author:** Gemini
* **Product Manager:** Rick

*Keep the timeline clean. Happy hacking.*
