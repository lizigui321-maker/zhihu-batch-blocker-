# ☢️ Zhihu Nuke Protocol (知乎核平协议)

![Version](https://img.shields.io/badge/Version-v2.0-00ff41.svg?style=flat-square)
![Author](https://img.shields.io/badge/Author-Gemini3.1pro-blue.svg?style=flat-square)
![PM](https://img.shields.io/badge/PM-Rick-orange.svg?style=flat-square)

这是一个用于知乎 (Zhihu) 的前端自动化书签脚本 (Bookmarklet)。
通过注入一个极具赛博朋克风格的控制面板，实现**一键全自动拉黑**特定知乎【专栏文章】或【回答】的作者以及全部点赞者。

对付引战、低质量内容或特定群体，只需一键，即可彻底清理你的信息流。

---

## ✨ 核心特性 (Features)

* **🎯 跨域双杀**：完美兼容 `www.zhihu.com` (回答详情页) 与 `zhuanlan.zhihu.com` (专栏文章页)，自动识别当前环境并调用对应 API。
* **💀 斩草除根**：不仅拉黑所有点赞者 (Upvoters/Likers)，还会优先锁定并拉黑该文章/回答的**作者**。
* **💻 赛博朋克 UI**：注入悬浮控制台，实时显示执行进度、当前拉黑目标 (Target) 与统计数据，自带极客终端特效。
* **🛡️ 真实战果校验**：精准捕获 API 返回状态 (`res.ok`)，拒绝 UI 假嗨，只统计真正拉黑成功的账号数量。
* **⚙️ 纯净轻量**：纯原生 JavaScript 编写，无需安装浏览器插件，添加为浏览器书签即可使用。

---

## 🚀 安装与使用教程 (How to Use)

### 第一步：添加书签 (Bookmarklet)
1. 在你的浏览器（Chrome/Edge/Safari等）书签栏上**右键**，选择 **“添加网页”** 或 **“添加书签”**。
2. 名称可以随便填，例如：`☢️ 知乎核平`。
3. 在 **“网址” (URL)** 一栏中，清除原有的链接，将下方的**全部核心代码**复制并粘贴进去。
4. 点击保存。

### 第二步：锁定目标并执行 (Execution)
1. 在浏览器中打开知乎，进入你想清理的**具体回答页面**（URL 包含 `/answer/`）或**专栏文章页面**（URL 包含 `zhuanlan.zhihu.com/p/`）。
2. 点击你刚才保存在书签栏的 `☢️ 知乎核平` 书签。
3. 页面右上角将弹出 `> NUKE PROTOCOL <` 控制台，自动开始执行拉黑程序。
4. 喝杯咖啡，等待进度条拉满，点击 `[ DISCONNECT & EXIT ]` 关闭面板。

---

## 📜 核心代码 (The Code)

> **⚠️ 注意**：请复制以下整段代码（包括开头的 `javascript:`）。

```javascript
javascript:(async()=>{const e=document.getElementById("zh-nuke-panel");e&&e.remove();const t=document.createElement("div");t.id="zh-nuke-panel",t.style.cssText="position:fixed;top:20px;right:20px;width:360px;background:rgba(5,5,5,0.95);color:#00ff41;padding:20px;border:1px solid #00ff41;border-radius:6px;z-index:2147483647;font-family:'Courier New',Courier,monospace;font-size:13px;box-shadow:0 0 15px rgba(0,255,65,0.4),inset 0 0 10px rgba(0,255,65,0.2);line-height:1.6;backdrop-filter:blur(5px);",t.innerHTML='<div style="text-align:center;margin-bottom:10px;"><strong style="font-size:16px;letter-spacing:2px;text-shadow:0 0 5px #00ff41;">> NUKE PROTOCOL <</strong></div><div style="display:flex;justify-content:space-between;font-size:11px;color:#0aa;margin-bottom:2px;font-weight:bold;"><span>[ AUTHOR: Gemini3.1pro ]</span><span>[ PM: Rick ]</span></div><div style="display:flex;justify-content:space-between;font-size:11px;color:#0aa;margin-bottom:8px;font-weight:bold;"><span>[ VER: v2.0 ]</span><span>[ BUILD: 2026.06.09 ]</span></div><div style="border-bottom:1px dashed #00ff41;margin-bottom:10px;"></div><div id="zh-nuke-content" style="white-space:pre-wrap;word-wrap:break-word">> SYSTEM BOOTING... <span id="zh-cursor">_</span></div>',document.documentElement.appendChild(t);const a=document.getElementById("zh-nuke-content"),n=document.createElement("style");n.innerHTML="@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}#zh-cursor{animation:blink 1s step-end infinite}",document.head.appendChild(n);const o=(e,t=!1)=>{a.innerHTML=e+(t?"":" <span id='zh-cursor'>_</span>")},r=e=>new Promise((t=>setTimeout(t,e))),s=(e,t)=>{if(0===t)return"[--------------------] 0%";const a=Math.min(1,e/t),n=Math.round(20*a),o="█".repeat(n)+"<span style='color:#004411'>░".repeat(20-n)+"</span>";return`[${o}] <span style="color:#fff;text-shadow:0 0 5px #fff">${Math.floor(100*a)}%</span>`},l=()=>{const e=document.createElement("button");e.innerText="[ DISCONNECT & EXIT ]",e.style.cssText="margin-top:15px;padding:8px 10px;background:transparent;color:#00ff41;border:1px solid #00ff41;border-radius:3px;font-family:'Courier New',monospace;font-weight:bold;cursor:pointer;width:100%;text-align:center;transition:all 0.3s;box-shadow:inset 0 0 5px rgba(0,255,65,0.3);",e.onmouseover=()=>{e.style.background="#00ff41",e.style.color="#000"},e.onmouseout=()=>{e.style.background="transparent",e.style.color="#00ff41"},e.onclick=()=>{t.remove(),n.remove()},t.appendChild(e)};const i=location.href;let c,d;const u=i.match(/question\/\d+\/answer\/(\d+)/),p=i.match(/zhihu\.com\/p\/(\d+)/);if(u)c="answers",d=u[1];else{if(!p)return o("> <span style='color:#f00;font-weight:bold'>[ ERROR: INVALID TARGET AREA ]</span>\n> 目标未锁定！拦截协议启动失败。\n> <span style='color:#ff0'>请先点击进入具体的【回答详情页】\n> 或【专栏文章页】后，再执行此协议。</span>\n> CURRENT STATUS: STANDBY...",!0),void l();c="articles",d=p[1]}let m=["|","/","-","\\"],h=0;try{let e=0;o("> <span style='color:#0aa'>LOCATING AUTHOR...</span>");let t="articles"===c?`https://zhuanlan.zhihu.com/api/articles/${d}`:`https://www.zhihu.com/api/v4/answers/${d}?include=author`,i=await fetch(t,{credentials:"include"});if(i.ok){const t=await i.json(),n=t.author;n&&n.url_token&&"0"!==n.url_token?(o(`> TARGET (AUTHOR): <span style='color:#fff'>${n.name}</span>\n> ACTION: <span style='color:#f00;animation:blink .5s infinite'>[ NUKING ]</span>`),await fetch(`https://www.zhihu.com/api/v4/members/${n.url_token}/actions/block`,{method:"POST",credentials:"include"}).then((t=>{t.ok&&e++})),await r(1000)):(o("> AUTHOR IS ANONYMOUS. <span style='color:#ff0'>SKIPPING</span>..."),await r(1000))}else{o("> <span style='color:#ff0'>WARNING: FAILED TO FETCH AUTHOR.</span> SKIPPING...");await r(1000)}let u=0,f=!1,b=0,k=0,w="articles"===c?"likers":"upvoters";for(;!f;){let t=await fetch(`https://www.zhihu.com/api/v4/${c}/${d}/${w}?limit=10&offset=${u}`,{credentials:"include"});if(!t.ok){o("> <span style='color:#f00'>ERROR: CONNECTION REFUSED.</span>",!0);break}const i=await t.json(),p=Array.isArray(i.data)?i.data:[];0===u&&(b=i.paging&&"number"==typeof i.paging.totals?i.paging.totals:p.length);for(const t of p)k++,h=(h+1)%4,o(`> TARGET: <span style='color:#fff'>${t.name}</span>\n> STATUS: <span style='color:#f00'>EXTERMINATING ${m[h]}</span>\n> PROGRESS: [${k}/${b}]\n> ${s(k,b)}`),await fetch(`https://www.zhihu.com/api/v4/members/${t.url_token}/actions/block`,{method:"POST",credentials:"include"}).then((t=>{t.ok&&e++})),await r(1000);if(f=!!(i.paging&&i.paging.is_end),u+=10,f)o(`> <span style='color:#0f0'>MISSION ACCOMPLISHED.</span>\n> TOTAL NEUTRALIZED: <span style='color:#fff'>${e}</span>\n> AWAITING COMMAND...`,!0),l()}}catch(err){o(`> <span style='color:#f00'>FATAL ERROR:</span> ${err.message}`,!0),l()}})();
