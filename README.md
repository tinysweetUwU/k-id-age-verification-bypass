# k-ID Age Verification Bypass

[![Support](https://img.shields.io/discord/1557983883704795217?style=for-the-badge&logo=discord&logoColor=white&label=Support&color=5865F2)](https://discord.gg/wkwsthag5D)
[![Browser](https://img.shields.io/badge/Browser%20Console-000000?style=for-the-badge&logo=googlechrome&logoColor=white)](#usage)

I built a Discord bot that completes k-ID age verification for you. Join the support server, grab a key (buy one or win one in giveaways), generate your verification link, and let the bot handle the rest.

<a href="https://ko-fi.com/tinysweet"><img src="https://storage.ko-fi.com/cdn/kofi2.png?v=3" width="140" alt="Support me on Ko-fi"></a>

> **Contact** — My main Discord account, `tinysweet_dev`, was banned by Discord. Add my backup: **`tinysweet._.`**.
>
> **How to get a key**
> - **Buy** — join the support server and DM `tinysweet._.` to purchase
> - **Free** — join the server and participate in **giveaways**
>
> **Support server:** https://discord.gg/wkwsthag5D

---

## How it works

1. **Join the server** — https://discord.gg/wkwsthag5D
2. **Get a key** — buy via DM to `tinysweet._.` or win one in giveaways
3. **Redeem** — run `/redeem` with your key (binds to your Discord account)
4. **Generate a link** — follow [Usage](#usage) below on the account you want verified
5. **Verify** — run `/verify` with your link. The bot completes the check and replies **Verified — check the account.** If it fails, press **Try again**.

| Plan | Details |
| ---- | ------- |
| `trial` | Limited uses (e.g. 1 or 3 verifies) |
| `monthly` | 30 days |
| `lifetime` | Never expires |

> The bot currently supports **Credit Card** and **AgeKey** links. Other methods return *Unsupported method*.

---

<details>
<summary><b>English</b></summary>

### Requirements

- Discord web — [discord.com/app](https://discord.com/app) or [discord.com/channels/@me](https://discord.com/channels/@me)
- Chrome / Edge / Brave / any Chromium browser (Firefox works with minor UI differences)
- Console access (F12)

### Usage

1. Open Discord in your browser and log in to the account you want verified.
2. Press **F12** → open the **Console** tab.
3. Type `allow pasting` and press Enter (Chromium blocks paste by default).
4. Paste the **entire script** (collapsible at the bottom) and press Enter.
5. Click the floating blue icon → open the panel.
6. Select a verification method → click **Generate verification link**.
7. The link is auto-copied. If not, click **Copy**.
8. In the support server: `/redeem <key>` (once), then `/verify <link>`.
9. Wait for **Verified — check the account.**

### Verification methods

| Method ID | Title        | Vendor | Provider         |
| --------- | ------------ | ------ | ---------------- |
| 5         | Credit Card  | 1      | Provided by k-ID |
| 3         | Video Selfie | 1      | Provided by k-ID |
| 1         | ID Scan      | 1      | Provided by k-ID |
| 10        | AgeKey       | 1      | Provided by k-ID |

The list is fetched live from Discord. The table above is the fallback if module discovery fails.

### Technical notes

- `webpackChunkdiscord_app.push(...)` grabs the webpack module registry
- Module `482876` exports the method list (`J`)
- Module `295972` exports the link generator (`en`)
- `en(method, vendor)` returns an object with `verification_webview_url`
- UI is injected into a shadow DOM so Discord styles do not leak in
- The bot submits the link server-side and polls k-ID status

### Troubleshooting

| Problem | Fix |
| ------- | --- |
| Verification module unavailable | Reload the page and re-run the script. Discord rotated the module ID. |
| Request timed out after 20 seconds | Discord API slow or blocked. Check the Network tab. |
| Paste blocked in console | Type `allow pasting` first (step 3). |
| Icon does not appear | Script may have thrown. Check the console for errors. |
| Link opens but verification fails | Link is session-bound. Generate from the same account you want verified. |
| Bot says "No active key" | Run `/redeem` first, or ask `tinysweet._.` for a key. |
| Bot says "Link expired" | Generate a fresh link and `/verify` again. |

</details>

---

<details>
<summary><b>Tiếng Việt</b></summary>

### Yêu cầu

- Discord web — [discord.com/app](https://discord.com/app) hoặc [discord.com/channels/@me](https://discord.com/channels/@me)
- Chrome / Edge / Brave / trình duyệt Chromium (Firefox cũng được, UI hơi khác)
- Console (F12)

### Cách sử dụng

1. Mở Discord trên trình duyệt, đăng nhập tài khoản cần xác minh.
2. Nhấn **F12** → tab **Console**.
3. Gõ `allow pasting` rồi Enter (Chromium chặn paste mặc định).
4. Paste **toàn bộ script** (phần thu gọn cuối README) rồi Enter.
5. Click icon xanh nổi → mở panel.
6. Chọn phương thức → **Generate verification link**.
7. Link tự copy. Nếu không, nhấn **Copy**.
8. Trong server: `/redeem <key>` (1 lần), rồi `/verify <link>`.
9. Đợi bot báo **Verified — check tài khoản.**

### Phương thức xác minh

| Method ID | Tên          | Vendor | Nhà cung cấp     |
| --------- | ------------ | ------ | ---------------- |
| 5         | Credit Card  | 1      | Provided by k-ID |
| 3         | Video Selfie | 1      | Provided by k-ID |
| 1         | ID Scan      | 1      | Provided by k-ID |
| 10        | AgeKey       | 1      | Provided by k-ID |

Danh sách fetch trực tiếp từ Discord. Bảng trên là fallback nếu không lấy được module.

### Ghi chú kỹ thuật

- `webpackChunkdiscord_app.push(...)` lấy webpack module registry
- Module `482876` export danh sách method (`J`)
- Module `295972` export hàm tạo link (`en`)
- `en(method, vendor)` trả về object chứa `verification_webview_url`
- UI inject vào shadow DOM để không bị style Discord ảnh hưởng
- Bot submit link phía server và poll status của k-ID

### Xử lý sự cố

| Vấn đề | Cách khắc phục |
| ------ | -------------- |
| Verification module unavailable | Reload trang và chạy lại script. Discord đã đổi module ID. |
| Request timed out after 20 seconds | API Discord chậm hoặc bị chặn. Kiểm tra tab Network. |
| Console chặn paste | Gõ `allow pasting` trước (bước 3). |
| Icon không xuất hiện | Script có thể đã lỗi. Kiểm tra console. |
| Link mở được nhưng verify thất bại | Link gắn với session. Generate từ đúng tài khoản cần xác minh. |
| Bot báo "No active key" | Chạy `/redeem` trước, hoặc xin key từ `tinysweet._.`. |
| Bot báo "Link expired" | Tạo link mới và `/verify` lại. |

</details>

---

<details>
<summary><b>Full script</b> — click to expand, then copy all</summary>

```js
(() => {
    const existing = document.getElementById('age-verification-ui');
    if (existing) existing.remove();

    const w = webpackChunkdiscord_app.push([[Symbol()], {}, r => r]);
    webpackChunkdiscord_app.pop();

    const defaultMethods = [
        { method: 5,  vendor: 1, title: 'Credit Card',  by: 'Provided by k-ID' },
        { method: 3,  vendor: 1, title: 'Video Selfie', by: 'Provided by k-ID' },
        { method: 1,  vendor: 1, title: 'ID Scan',      by: 'Provided by k-ID' },
        { method: 10, vendor: 1, title: 'AgeKey',       by: 'Provided by k-ID' },
    ];
    let methodList = defaultMethods;
    let selectedMethod = methodList.find(x => x.method === 5 && x.vendor === 1) || methodList[0];

    try {
        const q = w(482876)?.J;
        if (typeof q === 'function') {
            Promise.resolve(q()).then(x => {
                if (Array.isArray(x) && x.length) {
                    methodList = x;
                    populateSelect();
                    setStatus('Ready');
                }
            }).catch(() => {});
        }
    } catch {}

    const host = document.createElement('div');
    host.id = 'age-verification-ui';
    host.style.cssText = 'position:fixed;inset:0;width:0;height:0;z-index:2147483647;pointer-events:none';
    document.documentElement.appendChild(host);
    const shadow = host.attachShadow({ mode: 'open' });

    const style = document.createElement('style');
    style.textContent = `
        * { box-sizing: border-box; }
        #icon {
            position: fixed; right: 18px; bottom: 18px;
            width: 56px; height: 56px; border-radius: 16px;
            overflow: hidden; background: #5865f2;
            box-shadow: 0 10px 35px rgba(0,0,0,.45);
            cursor: grab; pointer-events: auto;
            touch-action: none; user-select: none;
        }
        #icon.dragging { cursor: grabbing; transform: scale(.97); }
        #icon img { display: block; width: 100%; height: 100%; object-fit: cover; pointer-events: none; }
        #panel {
            position: fixed; right: 18px; bottom: 86px;
            width: 420px; max-width: calc(100vw - 24px);
            display: none; overflow: hidden; border-radius: 17px;
            background: #111214; color: #fff;
            border: 1px solid rgba(255,255,255,.08);
            box-shadow: 0 25px 80px rgba(0,0,0,.55);
            font-family: 'gg sans', 'Noto Sans', Whitney, 'Helvetica Neue', Helvetica, Roboto, Arial, sans-serif;
            pointer-events: auto;
        }
        #head {
            height: 52px; padding: 0 12px 0 16px;
            display: flex; align-items: center; justify-content: space-between;
            background: #18191c; cursor: grab;
            user-select: none; touch-action: none;
        }
        #head.dragging { cursor: grabbing; }
        #title { display: flex; align-items: center; gap: 9px; font-size: 14px; font-weight: 600; letter-spacing: .3px; }
        #dot { display: none; }
        #closeBtn {
            width: 32px; height: 32px; border: 0; border-radius: 8px;
            background: transparent; color: #b5bac1; cursor: pointer;
            display: flex; align-items: center; justify-content: center; transition: .15s;
        }
        #closeBtn:hover { background: #2b2d31; color: #fff; }
        #body { padding: 16px; }
        #methodLabel { display: flex; align-items: center; gap: 7px; margin-bottom: 7px; color: #b5bac1; font-size: 12px; }
        #methodSelect, #urlInput {
            width: 100%; border: 1px solid #3f4147; border-radius: 10px;
            outline: none; background: #1e1f22; color: #fff;
        }
        #methodSelect { height: 44px; padding: 0 11px; margin-bottom: 10px; font-size: 13px; }
        #urlInput { height: 44px; padding: 0 11px; margin-top: 10px; font-size: 12px; }
        .btn {
            height: 42px; border: 0; border-radius: 10px;
            display: flex; align-items: center; justify-content: center;
            gap: 8px; font-weight: 700; cursor: pointer; transition: .15s;
        }
        .btn svg { width: 15px; height: 15px; flex: 0 0 15px; }
        #methodLabel svg { flex: 0 0 14px; }
        #genBtn {
            width: 100%;
            background: linear-gradient(135deg, #e5a900, #ffd34d);
            color: #242424; letter-spacing: .3px;
        }
        #genBtn:hover:not(:disabled) { background: linear-gradient(135deg, #cc9700, #f0bd32); box-shadow: 0 4px 15px rgba(240,189,50,.35); }
        #genBtn:disabled { opacity: .55; cursor: default; box-shadow: none; }
        #genBtn.success { background: linear-gradient(135deg, #248a50, #57f287); color: #fff; }
        #genBtn.success:hover:not(:disabled) { background: linear-gradient(135deg, #1e7041, #3dcc70); box-shadow: 0 4px 15px rgba(87,242,135,.3); }
        #genBtn.error { background: linear-gradient(135deg, #c0392b, #e74c3c); color: #fff; }
        #genBtn.error:hover:not(:disabled) { background: linear-gradient(135deg, #a93226, #c0392b); box-shadow: 0 4px 15px rgba(231,76,60,.4); }
        #actions { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-top: 10px; }
        #copyBtn, #openBtn { background: #2b2d31; color: #dbdee1; }
        #copyBtn:hover, #openBtn:hover { background: #36393f; color: #fff; }
        #statusMsg { min-height: 18px; margin-top: 10px; color: #949ba4; font-size: 12px; line-height: 18px; word-break: break-word; }
        #statusMsg.ok  { color: #57f287; }
        #statusMsg.err { color: #ed4245; }
        @media (max-width: 520px) {
            #panel { left: 12px !important; right: 12px !important; width: auto; max-width: none; bottom: 82px; }
            #icon  { right: 14px; bottom: 14px; }
        }
    `;
    shadow.appendChild(style);

    const iconEl = document.createElement('div');
    iconEl.id = 'icon';
    iconEl.innerHTML = '<img alt="">';
    iconEl.querySelector('img').src = 'https://cdn.discordapp.com/icons/1557983883704795217/fe40ed3b5225f619bfed03c40d33d975.webp?size=80&quality=lossless';
    const panelEl = document.createElement('div');
    panelEl.id = 'panel';

    const headEl = document.createElement('div');
    headEl.id = 'head';
    headEl.innerHTML = `
        <div id="title"><span id="dot"></span><span>Age Verification</span></div>
        <button id="closeBtn" type="button">
            <svg viewBox="0 0 24 24" width="15" height="15" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round">
                <line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/>
            </svg>
        </button>`;

    const bodyEl = document.createElement('div');
    bodyEl.id = 'body';

    const methodLabel = document.createElement('div');
    methodLabel.id = 'methodLabel';
    methodLabel.innerHTML = `
        <svg viewBox="0 0 24 24" width="13" height="13" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="3"/><path d="M19.07 4.93a10 10 0 0 1 0 14.14M4.93 4.93a10 10 0 0 0 0 14.14"/>
        </svg>
        <span>Verification method</span>`;

    const methodSelect = document.createElement('select');
    methodSelect.id = 'methodSelect';

    const genBtn = document.createElement('button');
    genBtn.id = 'genBtn';
    genBtn.className = 'btn';
    genBtn.innerHTML = `
        <svg viewBox="0 0 24 24" width="15" height="15" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"/>
            <path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"/>
        </svg>
        <span>Generate verification link</span>`;

    const urlInput = document.createElement('input');
    urlInput.id = 'urlInput';
    urlInput.readOnly = true;
    urlInput.placeholder = 'Verification URL will appear here';

    const actionsEl = document.createElement('div');
    actionsEl.id = 'actions';

    const copyBtn = document.createElement('button');
    copyBtn.id = 'copyBtn';
    copyBtn.className = 'btn';
    copyBtn.innerHTML = `
        <svg viewBox="0 0 256 256" width="16" height="16" fill="currentColor">
            <path d="M216,32H88a8,8,0,0,0-8,8V80H40a8,8,0,0,0-8,8V216a8,8,0,0,0,8,8H168a8,8,0,0,0,8-8V176h40a8,8,0,0,0,8-8V40A8,8,0,0,0,216,32ZM160,208H48V96H160Zm48-48H176V88a8,8,0,0,0-8-8H96V48H208Z"/>
        </svg>
        <span>Copy link</span>`;

    const openBtn = document.createElement('button');
    openBtn.id = 'openBtn';
    openBtn.className = 'btn';
    openBtn.innerHTML = `
        <svg viewBox="0 0 256 256" width="16" height="16" fill="currentColor">
            <path d="M224,104a8,8,0,0,1-16,0V59.32l-82.34,82.34a8,8,0,0,1-11.32-11.32L196.68,48H152a8,8,0,0,1,0-16h64a8,8,0,0,1,8,8Zm-40,24a8,8,0,0,0-8,8v72H48V80h72a8,8,0,0,0,0-16H48A16,16,0,0,0,32,80V208a16,16,0,0,0,16,16H176a16,16,0,0,0,16-16V136A8,8,0,0,0,184,128Z"/>
        </svg>
        <span>Open</span>`;

    const statusMsg = document.createElement('div');
    statusMsg.id = 'statusMsg';

    actionsEl.append(copyBtn, openBtn);
    bodyEl.append(methodLabel, methodSelect, genBtn, urlInput, actionsEl, statusMsg);
    panelEl.append(headEl, bodyEl);
    shadow.append(iconEl, panelEl);

    function populateSelect() {
        methodSelect.innerHTML = '';
        for (const item of methodList) {
            const opt = document.createElement('option');
            opt.value = `${item.method}:${item.vendor}`;
            opt.textContent = item.by ? `${item.title} • ${item.by}` : item.title;
            methodSelect.appendChild(opt);
        }
        selectedMethod = methodList.find(x => x.method === selectedMethod.method && x.vendor === selectedMethod.vendor) || methodList[0];
        methodSelect.value = `${selectedMethod.method}:${selectedMethod.vendor}`;
    }

    function setStatus(text, type = '') {
        statusMsg.textContent = text;
        statusMsg.className = type;
    }

    function clamp(el) {
        const rect = el.getBoundingClientRect();
        el.style.left   = `${Math.max(8, Math.min(rect.left, innerWidth  - rect.width  - 8))}px`;
        el.style.top    = `${Math.max(8, Math.min(rect.top,  innerHeight - rect.height - 8))}px`;
        el.style.right  = 'auto';
        el.style.bottom = 'auto';
    }

    function makeDraggable(el, grip, isIcon) {
        let active = false, moved = false;
        let startX = 0, startY = 0, startLeft = 0, startTop = 0;

        grip.addEventListener('pointerdown', e => {
            if (e.button !== 0) return;
            if (e.target.closest?.('#closeBtn')) return;
            active = true; moved = false;
            const rect = el.getBoundingClientRect();
            startX = e.clientX; startY = e.clientY;
            startLeft = rect.left; startTop = rect.top;
            el.style.left = `${startLeft}px`; el.style.top = `${startTop}px`;
            el.style.right = 'auto'; el.style.bottom = 'auto';
            (isIcon ? iconEl : headEl).classList.add('dragging');
            grip.setPointerCapture?.(e.pointerId);
        });

        grip.addEventListener('pointermove', e => {
            if (!active) return;
            const dx = e.clientX - startX;
            const dy = e.clientY - startY;
            if (Math.abs(dx) > 5 || Math.abs(dy) > 5) moved = true;
            if (!moved) return;
            const rect = el.getBoundingClientRect();
            el.style.left = `${Math.max(8, Math.min(startLeft + dx, innerWidth  - rect.width  - 8))}px`;
            el.style.top  = `${Math.max(8, Math.min(startTop  + dy, innerHeight - rect.height - 8))}px`;
            e.preventDefault();
        });

        grip.addEventListener('pointerup', e => {
            if (!active) return;
            active = false;
            (isIcon ? iconEl : headEl).classList.remove('dragging');
            if (isIcon && moved) iconEl.dataset.dragged = '1';
            grip.releasePointerCapture?.(e.pointerId);
        });

        grip.addEventListener('pointercancel', () => {
            active = false; moved = false;
            iconEl.classList.remove('dragging');
            headEl.classList.remove('dragging');
        });
    }

    iconEl.onclick = () => {
        if (iconEl.dataset.dragged === '1') { iconEl.dataset.dragged = '0'; return; }
        const show = panelEl.style.display !== 'block';
        panelEl.style.display = show ? 'block' : 'none';
        if (show) clamp(panelEl);
    };

    const closeBtn = headEl.querySelector('#closeBtn');
    closeBtn.addEventListener('pointerdown', e => e.stopPropagation());
    closeBtn.addEventListener('click', e => { e.stopPropagation(); panelEl.style.display = 'none'; });

    methodSelect.onchange = () => {
        const [method, vendor] = methodSelect.value.split(':').map(Number);
        selectedMethod = { method, vendor };
        urlInput.value = '';
        setStatus('');
    };

    genBtn.onclick = async () => {
        genBtn.classList.remove('error', 'success');
        genBtn.disabled = true;
        genBtn.querySelector('span').textContent = 'Generating...';
        urlInput.value = '';
        setStatus('Contacting Discord...');
        try {
            const mod = w(295972);
            if (!mod?.en) throw new Error('Verification module unavailable');
            const res = await Promise.race([
                mod.en(selectedMethod.method, selectedMethod.vendor),
                new Promise((_, reject) => setTimeout(() => reject(new Error('Request timed out after 20 seconds')), 20000))
            ]);
            const link = res?.verification_webview_url;
            if (!link) throw new Error('Discord did not return a verification URL');
            genBtn.classList.remove('error');
            genBtn.classList.add('success');
            urlInput.value = link;
            try {
                await navigator.clipboard.writeText(link);
                setStatus('Generated and copied to clipboard', 'ok');
            } catch {
                setStatus('Verification link generated', 'ok');
            }
            console.log('[Age Verification]', res);
        } catch (e) {
            console.error('[Age Verification]', e);
            setStatus(e?.message || String(e), 'err');
            genBtn.classList.remove('success');
            genBtn.classList.add('error');
            genBtn.querySelector('span').textContent = 'Try again';
        } finally {
            genBtn.disabled = false;
            if (!genBtn.classList.contains('error')) {
                genBtn.querySelector('span').textContent = genBtn.classList.contains('success') ? 'Link generated' : 'Generate verification link';
            }
        }
    };

    copyBtn.onclick = async () => {
        if (!urlInput.value) { setStatus('No verification link', 'err'); return; }
        try {
            await navigator.clipboard.writeText(urlInput.value);
            setStatus('Copied to clipboard ✓', 'ok');
        } catch {
            urlInput.select();
            document.execCommand('copy');
            setStatus('Copied to clipboard ✓', 'ok');
        }
    };

    openBtn.onclick = () => {
        if (!urlInput.value) { setStatus('No verification link', 'err'); return; }
        window.open(urlInput.value, '_blank', 'noopener,noreferrer');
    };

    makeDraggable(iconEl,  iconEl, true);
    makeDraggable(panelEl, headEl, false);

    addEventListener('resize', () => {
        clamp(iconEl);
        if (panelEl.style.display === 'block') clamp(panelEl);
    });

    populateSelect();
    setStatus(methodList.length + ' verification methods available');
    console.log('%c[Age Verification] Ready', 'color:#5865f2;font-weight:bold');
})();
```

</details>
