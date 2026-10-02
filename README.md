# k-ID Age Verification Bypass

[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Support](https://img.shields.io/discord/1392413874204049518?style=for-the-badge&logo=discord&logoColor=white&label=Support&color=5865F2)](https://discord.gg/hqr6YW2MjJ)
[![Browser](https://img.shields.io/badge/Browser%20Console-000000?style=for-the-badge&logo=googlechrome&logoColor=white)](#usage)

Discord k-ID Age Verification Bypass — generate a verification link directly from the Discord client and send it to the verifier to complete age verification on your behalf.

<a href="https://ko-fi.com/tinysweet"><img src="https://storage.ko-fi.com/cdn/kofi2.png?v=3" width="140" alt="Support me on Ko-fi"></a>

> [!TIP]
> **Currently free** — Verification is free at the moment. Support the project via the donate button above if you find it useful.

---

<details>
<summary><b>🇬🇧 English</b></summary>

## What it does

This script hooks into Discord's internal webpack module registry from the browser console. It locates the k-ID age verification module, enumerates the available verification methods, and calls Discord's own API to generate a verification link — without going through the official UI flow.

You generate the link on your own Discord account, then send it to the verifier (`tinysweet_dev`) who completes the verification for you.

> [!TIP]
> **Currently free:** Verification is free right now. Feel free to donate if you appreciate the work.

## Requirements

- Discord web client open — [https://discord.com/app](https://discord.com/app) or [https://discord.com/channels/@me](https://discord.com/channels/@me)
- Desktop Chrome / Edge / Brave / any Chromium-based browser (Firefox works too, minor UI differences)
- Console access (F12)

## Usage

1. Open Discord in your browser and log in to the account you want verified.
2. Press **F12** to open DevTools → go to the **Console** tab.
3. **Allow pasting** — Chromium blocks pasting into the console by default. Type this and press Enter:

   ```
   allow pasting
   ```

   Once the warning disappears, paste is enabled for this tab.

4. Paste the **entire script** (see collapsible at the bottom of this README) into the console and press Enter.
5. A floating blue icon appears in the bottom-right corner of the page. Click it to open the panel.
6. Select a verification method from the dropdown.
7. Click **Generate verification link**.
8. The link is auto-copied to your clipboard. If not, click **Copy**.
9. **Send the generated link to `tinysweet_dev` via DM.**
10. The verifier (`tinysweet_dev`) opens the link and completes the verification for you.

---

## Verification methods

| Method ID | Title        | Vendor | Provider           |
|-----------|--------------|--------|--------------------|
| 5         | Credit Card  | 1      | Provided by k-ID   |
| 3         | Video Selfie | 1      | Provided by k-ID   |
| 1         | ID Scan      | 1      | Provided by k-ID   |
| 10        | AgeKey       | 1      | Provided by k-ID   |

The list is fetched live from Discord when the script loads. The table above is the fallback if module discovery fails.

## How it works

- `webpackChunkdiscord_app.push(...)` grabs a reference to the webpack module registry.
- Module `482876` exports the method list (`J`).
- Module `295972` exports the link generator (`en`).
- `en(method, vendor)` calls Discord's internal endpoint and resolves to an object containing `verification_webview_url`.
- The UI is injected into a shadow DOM host so Discord's styles don't bleed in.

## Troubleshooting

| Problem                              | Fix                                                                 |
|--------------------------------------|---------------------------------------------------------------------|
| "Verification module unavailable"    | Reload the page and re-run the script. Discord rotated the module ID. |
| "Request timed out after 20 seconds" | Discord API slow or blocked. Check the network tab.                 |
| Paste is blocked in console          | Type `allow pasting` first (see step 3).                            |
| Icon doesn't appear                  | The script may have thrown. Check the console for errors.           |
| Link opens but verification fails    | The link is session-bound. Generate and send from the same account you want verified. |

</details>

---

<details>
<summary><b>🇻🇳 Tiếng Việt</b></summary>

## Chức năng

Script này hook vào webpack module registry nội bộ của Discord client từ console trình duyệt. Nó tìm module xử lý age verification của k-ID, liệt kê các phương thức xác minh có sẵn, và gọi API nội bộ của Discord để tạo verification link — không cần đi qua UI chính thức.

Bạn tạo link trên chính tài khoản Discord của mình, sau đó gửi link đó cho người xác minh (`tinysweet_dev`) để họ hoàn tất xác minh hộ bạn.

> [!TIP]
> **Hiện đang miễn phí:** Dịch vụ xác minh đang free. Nếu thấy hữu ích thì donate ủng hộ nhé.

## Yêu cầu

- Discord web đang mở — [https://discord.com/app](https://discord.com/app) hoặc [https://discord.com/channels/@me](https://discord.com/channels/@me)
- Chrome / Edge / Brave / bất kỳ trình duyệt nhân Chromium nào (Firefox cũng chạy được, UI khác chút)
- Quyền truy cập Console (F12)

## Cách sử dụng

1. Mở Discord trên trình duyệt và đăng nhập vào tài khoản bạn muốn xác minh.
2. Nhấn **F12** để mở DevTools → chuyển sang tab **Console**.
3. **Allow pasting** — Chromium chặn paste vào console mặc định. Gõ dòng này rồi Enter:

   ```
   allow pasting
   ```

   Khi cảnh báo biến mất, paste đã được bật cho tab này.

4. Paste **toàn bộ script** (xem phần thu gọn ở cuối README) vào console và nhấn Enter.
5. Một icon xanh nổi xuất hiện ở góc phải dưới màn hình. Click vào để mở panel.
6. Chọn phương thức xác minh từ dropdown.
7. Nhấn **Generate verification link**.
8. Link sẽ tự động được copy vào clipboard. Nếu không, nhấn **Copy**.
9. **Gửi link vừa tạo cho `tinysweet_dev` qua DM.**
10. Người xác minh (`tinysweet_dev`) sẽ mở link và hoàn tất xác minh hộ bạn.

---

## Các phương thức xác minh

| Method ID | Tên          | Vendor | Nhà cung cấp       |
|-----------|--------------|--------|--------------------|
| 5         | Credit Card  | 1      | Provided by k-ID   |
| 3         | Video Selfie | 1      | Provided by k-ID   |
| 1         | ID Scan      | 1      | Provided by k-ID   |
| 10        | AgeKey       | 1      | Provided by k-ID   |

Danh sách được fetch trực tiếp từ Discord khi script load. Bảng trên là fallback nếu module discovery thất bại.

## Cách hoạt động

- `webpackChunkdiscord_app.push(...)` lấy reference tới webpack module registry.
- Module `482876` export danh sách method (`J`).
- Module `295972` export hàm tạo link (`en`).
- `en(method, vendor)` gọi endpoint nội bộ của Discord và trả về object chứa `verification_webview_url`.
- UI được inject vào shadow DOM host để style của Discord không ảnh hưởng.

## Xử lý sự cố

| Vấn đề                               | Cách khắc phục                                                      |
|--------------------------------------|---------------------------------------------------------------------|
| "Verification module unavailable"    | Reload trang và chạy lại script. Discord đã đổi module ID.          |
| "Request timed out after 20 seconds" | API Discord chậm hoặc bị chặn. Kiểm tra tab Network.                |
| Console chặn paste                   | Gõ `allow pasting` trước (xem bước 3).                              |
| Icon không xuất hiện                 | Script có thể đã throw. Kiểm tra console để xem lỗi.                |
| Link mở được nhưng verify thất bại   | Link gắn với session. Generate và gửi từ cùng tài khoản bạn muốn xác minh. |

</details>

---

<details>
<summary><b>Full script / Toàn bộ script</b> — click to expand, then copy all</summary>

```js
(() => {
    const old = document.getElementById('age-verification-ui');
    if (old) old.remove();
    const w = webpackChunkdiscord_app.push([[Symbol()], {}, r => r]);
    webpackChunkdiscord_app.pop();
    const fallback = [
        { method: 5, vendor: 1, title: 'Credit Card', by: 'Provided by k-ID' },
        { method: 3, vendor: 1, title: 'Video Selfie', by: 'Provided by k-ID' },
        { method: 1, vendor: 1, title: 'ID Scan', by: 'Provided by k-ID' },
        { method: 10, vendor: 1, title: 'AgeKey', by: 'Provided by k-ID' }
    ];
    let list = fallback;
    let sel = list.find(x => x.method === 5 && x.vendor === 1) || list[0];
    try {
        const fn = w(482876)?.J;
        if (typeof fn === 'function') {
            Promise.resolve(fn()).then(x => {
                if (Array.isArray(x) && x.length) {
                    list = x;
                    fill();
                    setStatus('Ready');
                }
            }).catch(() => {});
        }
    } catch {}
    const iconData = 'data:image/webp;base64,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';
    const host = document.createElement('div');
    host.id = 'age-verification-ui';
    host.style.cssText = 'position:fixed;inset:0;width:0;height:0;z-index:2147483647;pointer-events:none';
    document.documentElement.appendChild(host);
    const root = host.attachShadow({ mode: 'open' });
    const css = document.createElement('style');
    css.textContent = `
        *{box-sizing:border-box}
        #icon{position:fixed;right:18px;bottom:18px;width:56px;height:56px;border-radius:16px;overflow:hidden;background:#5865f2;box-shadow:0 10px 35px rgba(0,0,0,.45);cursor:grab;pointer-events:auto;touch-action:none;user-select:none;transition:.15s}
        #icon:hover{transform:translateY(-2px);box-shadow:0 14px 40px rgba(0,0,0,.55)}
        #icon.dragging{cursor:grabbing;transform:scale(.97)}
        #icon img{display:block;width:100%;height:100%;object-fit:cover;pointer-events:none}
        #panel{position:fixed;right:18px;bottom:86px;width:420px;max-width:calc(100vw - 24px);display:none;overflow:hidden;border-radius:17px;background:#111214;color:#fff;border:1px solid rgba(255,255,255,.08);box-shadow:0 25px 80px rgba(0,0,0,.55);font-family:Arial,Helvetica,sans-serif;pointer-events:auto}
        #head{height:52px;padding:0 12px 0 16px;display:flex;align-items:center;justify-content:space-between;background:#18191c;cursor:grab;user-select:none;touch-action:none}
        #head.dragging{cursor:grabbing}
        #title{display:flex;align-items:center;gap:9px;font-size:14px;font-weight:700}
        #dot{width:8px;height:8px;border-radius:50%;background:#57f287;box-shadow:0 0 10px rgba(87,242,135,.5)}
        #close{width:32px;height:32px;border:0;border-radius:8px;background:transparent;color:#b5bac1;cursor:pointer;display:flex;align-items:center;justify-content:center}
        #close:hover{background:#2b2d31;color:#fff}
        #body{padding:16px}
        #label{display:flex;align-items:center;gap:7px;margin-bottom:7px;color:#b5bac1;font-size:12px}
        #select,#url{width:100%;border:1px solid #3f4147;border-radius:10px;outline:none;background:#1e1f22;color:#fff}
        #select{height:44px;padding:0 11px;margin-bottom:10px;font-size:13px}
        #url{height:44px;padding:0 11px;margin-top:10px;font-size:12px}
        .btn{height:42px;border:0;border-radius:10px;display:flex;align-items:center;justify-content:center;gap:8px;font-weight:700;cursor:pointer}
        .btn svg{width:16px;height:16px;flex:0 0 16px}
        #gen{width:100%;background:#5865f2;color:#fff}
        #gen:hover{background:#4752c4}
        #gen:disabled{opacity:.65;cursor:default}
        #acts{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:10px}
        #copy,#open{background:#2b2d31;color:#fff}
        #copy:hover,#open:hover{background:#36393f}
        #msg{min-height:18px;margin-top:10px;color:#949ba4;font-size:12px;line-height:18px;word-break:break-word}
        #msg.ok{color:#57f287}
        #msg.err{color:#ed4245}
        @media(max-width:520px){#panel{left:12px!important;right:12px!important;width:auto;max-width:none;bottom:82px}#icon{right:14px;bottom:14px}}
    `;
    root.appendChild(css);
    const icon = document.createElement('div');
    icon.id = 'icon';
    icon.innerHTML = '<img alt="">';
    icon.querySelector('img').src = iconData;
    const panel = document.createElement('div');
    panel.id = 'panel';
    const head = document.createElement('div');
    head.id = 'head';
    head.innerHTML = `
        <div id="title"><span id="dot"></span><span>Age Verification</span></div>
        <button id="close" type="button">
            <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round">
                <path d="M6 6l12 12M18 6L6 18"/>
            </svg>
        </button>
    `;
    const body = document.createElement('div');
    body.id = 'body';
    const label = document.createElement('div');
    label.id = 'label';
    label.innerHTML = `
        <svg viewBox="0 0 24 24" width="15" height="15" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
            <rect x="4" y="3" width="16" height="18" rx="3"/>
            <path d="M8 8h8M8 12h8M8 16h5"/>
        </svg>
        <span>Verification method</span>
    `;
    const select = document.createElement('select');
    select.id = 'select';
    const gen = document.createElement('button');
    gen.id = 'gen';
    gen.className = 'btn';
    gen.innerHTML = `
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 3l1.7 5.3L19 10l-5.3 1.7L12 17l-1.7-5.3L5 10l5.3-1.7L12 3z"/>
            <path d="M19 15l.7 2.3L22 18l-2.3.7L19 15z"/>
        </svg>
        <span>Generate verification link</span>
    `;
    const url = document.createElement('input');
    url.id = 'url';
    url.readOnly = true;
    url.placeholder = 'Verification URL';
    const acts = document.createElement('div');
    acts.id = 'acts';
    const copy = document.createElement('button');
    copy.id = 'copy';
    copy.className = 'btn';
    copy.innerHTML = `
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round">
            <rect x="9" y="9" width="10" height="10" rx="2"/>
            <path d="M6 15H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v1"/>
        </svg>
        <span>Copy</span>
    `;
    const open = document.createElement('button');
    open.id = 'open';
    open.className = 'btn';
    open.innerHTML = `
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round">
            <path d="M14 4h6v6"/>
            <path d="M10 14L20 4"/>
            <path d="M20 13v5a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h5"/>
        </svg>
        <span>Open</span>
    `;
    const msg = document.createElement('div');
    msg.id = 'msg';
    acts.append(copy, open);
    body.append(label, select, gen, url, acts, msg);
    panel.append(head, body);
    root.append(icon, panel);
    fill();
    setStatus(list.length + ' verification methods available');
    function fill() {
        select.innerHTML = '';
        for (const m of list) {
            const o = document.createElement('option');
            o.value = `${m.method}:${m.vendor}`;
            o.textContent = m.by ? `${m.title} • ${m.by}` : m.title;
            select.appendChild(o);
        }
        sel = list.find(x => x.method === sel.method && x.vendor === sel.vendor) || list[0];
        select.value = `${sel.method}:${sel.vendor}`;
    }
    function setStatus(text, type = '') {
        msg.textContent = text;
        msg.className = type;
    }
    function clamp(el) {
        const r = el.getBoundingClientRect();
        el.style.left = `${Math.max(8, Math.min(r.left, innerWidth - r.width - 8))}px`;
        el.style.top = `${Math.max(8, Math.min(r.top, innerHeight - r.height - 8))}px`;
        el.style.right = 'auto';
        el.style.bottom = 'auto';
    }
    function drag(el, grip, isIcon) {
        let on = false, moved = false, sx = 0, sy = 0, sl = 0, st = 0;
        grip.addEventListener('pointerdown', e => {
            if (e.button !== 0) return;
            if (e.target.closest?.('#close')) return;
            on = true;
            moved = false;
            const r = el.getBoundingClientRect();
            sx = e.clientX;
            sy = e.clientY;
            sl = r.left;
            st = r.top;
            el.style.left = `${sl}px`;
            el.style.top = `${st}px`;
            el.style.right = 'auto';
            el.style.bottom = 'auto';
            (isIcon ? icon : head).classList.add('dragging');
            grip.setPointerCapture?.(e.pointerId);
        });
        grip.addEventListener('pointermove', e => {
            if (!on) return;
            const dx = e.clientX - sx;
            const dy = e.clientY - sy;
            if (Math.abs(dx) > 5 || Math.abs(dy) > 5) moved = true;
            if (!moved) return;
            const r = el.getBoundingClientRect();
            el.style.left = `${Math.max(8, Math.min(sl + dx, innerWidth - r.width - 8))}px`;
            el.style.top = `${Math.max(8, Math.min(st + dy, innerHeight - r.height - 8))}px`;
            e.preventDefault();
        });
        grip.addEventListener('pointerup', e => {
            if (!on) return;
            on = false;
            (isIcon ? icon : head).classList.remove('dragging');
            if (isIcon && moved) icon.dataset.dragged = '1';
            grip.releasePointerCapture?.(e.pointerId);
        });
        grip.addEventListener('pointercancel', () => {
            on = false;
            moved = false;
            icon.classList.remove('dragging');
            head.classList.remove('dragging');
        });
    }
    icon.onclick = () => {
        if (icon.dataset.dragged === '1') {
            icon.dataset.dragged = '0';
            return;
        }
        const show = panel.style.display !== 'block';
        panel.style.display = show ? 'block' : 'none';
        if (show) clamp(panel);
    };
    const close = head.querySelector('#close');

    close.addEventListener('pointerdown', e => {
        e.stopPropagation();
    });

    close.addEventListener('click', e => {
        e.stopPropagation();
        panel.style.display = 'none';
    });
    select.onchange = () => {
        const [method, vendor] = select.value.split(':').map(Number);
        sel = { method, vendor };
        url.value = '';
        setStatus('');
    };
    gen.onclick = async () => {
        gen.disabled = true;
        gen.querySelector('span').textContent = 'Generating...';
        url.value = '';
        setStatus('Contacting Discord...');
        try {
            const mod = w(295972);
            if (!mod?.en) throw new Error('Verification module unavailable');
            const res = await Promise.race([
                mod.en(sel.method, sel.vendor),
                new Promise((_, reject) =>
                    setTimeout(() => reject(new Error('Request timed out after 20 seconds')), 20000)
                )
            ]);
            const link = res?.verification_webview_url;
            if (!link) throw new Error('Discord did not return a verification URL');
            url.value = link;
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
        } finally {
            gen.disabled = false;
            gen.querySelector('span').textContent = 'Generate verification link';
        }
    };
    copy.onclick = async () => {
        if (!url.value) {
            setStatus('No verification link', 'err');
            return;
        }
        try {
            await navigator.clipboard.writeText(url.value);
            setStatus('Copied', 'ok');
        } catch {
            url.select();
            document.execCommand('copy');
            setStatus('Copied', 'ok');
        }
    };
    open.onclick = () => {
        if (!url.value) {
            setStatus('No verification link', 'err');
            return;
        }
        window.open(url.value, '_blank', 'noopener,noreferrer');
    };
    drag(icon, icon, true);
    drag(panel, head, false);
    addEventListener('resize', () => {
        clamp(icon);
        if (panel.style.display === 'block') clamp(panel);
    });
    console.log('%c[Age Verification] Ready', 'color:#5865f2;font-weight:bold');
})();
```

</details>
