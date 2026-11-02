# Site navigation kit (side rail, phone menus, logo link home)

Owned by the Home page chat. Tool chats: copy these pieces into your tool as written, then follow the steps.
Look and behaviour are explained in the Design Brief ("Navigation on tool pages"). Kit version 1, 2 Nov 2026.

## What the tool page ends up with
- Laptops and desktops (900px and wider): a slim dark side rail down the left. Top to bottom: C-stone mark (links home), Home, Tools (pop-out), Vault (pop-out), Learn, then Join and Night/Day at the bottom. The page's own Night/Day button hides, because the rail has one.
- Phones and tablets (under 900px): no rail. Amber "Tools" and "Vault" drop-down buttons sit in the tool's top row, next to its Night/Day button.
- Logo: the C-stone mark sits in front of "crnrstone-co" in the tool's brand line, and the brand line links to the Home page.
- All links go to the live website (https://crnrstone-co.com/...), so they work the same in the Claude working copy and on the website.

## Steps
1. Paste the CSS at the end of the tool's `<style>`.
2. Paste the rail as the first thing inside the page content (before the tool's `.wrap`). It is fixed to the left, so its place in the file doesn't matter much.
3. In the tool's top row, wrap the phone menus and the tool's existing Night/Day button together: `<div class="navr">` phone menus, then the Night/Day button `</div>`.
4. Replace the tool's brand line with the logo link.
5. Mark this page's section in the rail: on Tools pages (Calculator, Plan Triangle, Trig Solver) replace `TOOLS_ON` with `on`. On other pages delete `TOOLS_ON` and add `on` to that section's item instead (Vault pages: the Vault summary; 3D model: Learn).
6. Paste the script at the end of the tool's `<script>`. It needs the page's existing Night/Day button to have `id="theme"` and its icon `id="theme-ic"` (all our tools already do).
7. Check: no sideways scrolling at 360px, 390px and 1280px; Night/Day from the rail and the page stay in step; menus close on an outside tap and on Escape.

## CSS
```css
/* Top menus: Tools and The Vault drop down from the nav */
.dd{position:relative}
.dd>summary{list-style:none;display:inline-flex;align-items:center;gap:6px;height:40px;padding:0 14px;border-radius:6px;font:600 16px Barlow,sans-serif;cursor:pointer;user-select:none;border:1.5px solid transparent}
.dd>summary::-webkit-details-marker{display:none}
.dd>summary::after{content:"";width:7px;height:7px;border-right:2px solid currentColor;border-bottom:2px solid currentColor;transform:translateY(-2px) rotate(45deg);transition:transform .2s}
.dd[open]>summary::after{transform:translateY(1px) rotate(-135deg)}
.dd>summary{background:var(--accent);color:var(--accent-ink)}
.dd>summary:focus-visible{outline:3px solid var(--accent);outline-offset:3px}
.menu{position:absolute;right:0;top:calc(100% + 8px);z-index:20;width:min(300px,calc(100vw - 32px));background:var(--surface);color:var(--ink);border:1px solid var(--line);border-top:4px solid var(--accent);border-radius:8px;padding:8px;box-shadow:0 12px 32px rgba(10,18,32,.28);display:flex;flex-direction:column;gap:2px}
.menu .mh{font:700 12px Barlow,sans-serif;letter-spacing:.12em;text-transform:uppercase;color:var(--mute);padding:8px 10px 4px}
.menu a,.menu .soon{display:flex;flex-direction:column;gap:1px;padding:8px 10px;border-radius:6px;text-decoration:none}
.menu a:hover,.menu a:focus-visible{background:var(--bg);outline:none}
.menu b{font:600 16px Barlow,sans-serif}
.menu small{font-size:13px;color:var(--mute);line-height:1.35}
.menu .soon{opacity:.75}
.menu .soon b::after{content:"Coming soon";margin-left:8px;font:600 11px Barlow,sans-serif;letter-spacing:.06em;text-transform:uppercase;border:1.5px solid var(--line);color:var(--mute);border-radius:99px;padding:1px 7px;vertical-align:2px}
@media (max-width:720px){.dd{position:static}.dd>summary{height:36px;padding:0 9px;font-size:15px;gap:5px}.menu{left:0;right:0;width:auto}}
@media (max-width:420px){.dd>summary::after{display:none}.dd>summary{padding:0 10px}}
/* Phone menus sit beside the page's Night/Day button */
.navr{display:flex;align-items:center;gap:8px}
.menu a{color:var(--ink)}
@media (max-width:440px){.dd.vault .the{display:none}}
/* Logo link home */
.brand{color:inherit;text-decoration:none;white-space:nowrap}
.brand .mark{display:inline-block;width:28px;height:28px;vertical-align:-5px;margin-right:9px}
.brand .word{color:inherit}
.brand .dash{color:var(--logo-accent,var(--accent));margin:0 .15em}
@media (max-width:420px){.brand{font-size:19px}.brand .mark{width:22px;height:22px;vertical-align:-4px;margin-right:7px}}
@media (max-width:374px){.brand .word{display:none}}
/* Side rail (laptops and desktops, 900px and wider): slim dark strip down the left with pop-out panels.
   Phones and tablets use the Tools and Vault drop-downs instead. */
.rail{display:none}
@media (min-width:900px){
  body{padding-left:88px}
  .rail{display:flex;flex-direction:column;align-items:stretch;gap:4px;position:fixed;z-index:30;top:0;bottom:0;left:0;width:88px;
    padding:14px 8px calc(14px + env(safe-area-inset-bottom,0px));background:#0E1A2E;border-right:1px solid rgba(234,240,248,.08)}
  .rail .mark{display:block;text-align:center;line-height:44px;height:44px;white-space:nowrap;margin-bottom:10px;font:700 18px "Barlow Condensed",sans-serif;color:#EAF0F8;text-decoration:none;letter-spacing:.02em}
  .rail .mark .rmark{width:34px;height:34px;vertical-align:middle;color:#EAF0F8}
  .ri{display:flex;flex-direction:column;align-items:center;gap:4px;width:100%;padding:10px 4px;border-radius:8px;border:0;background:none;color:#B8C4D6;font:600 12px Barlow,sans-serif;text-decoration:none;cursor:pointer;list-style:none;text-align:center}
  .ri::-webkit-details-marker{display:none}
  .ri svg{width:22px;height:22px;flex:none}
  .ri:hover{color:#EAF0F8;background:rgba(234,240,248,.07)}
  .ri.on{background:var(--accent);color:var(--accent-ink)}
  .rp[open]>.ri{background:rgba(234,240,248,.14);color:#EAF0F8}
  .ri:focus-visible{outline:3px solid var(--accent);outline-offset:2px}
  .rp{position:relative}
  .rp>.menu{position:absolute;left:calc(100% + 14px);top:0;right:auto;width:300px}
  .rail .spacer{flex:1}
  .rail .rule{height:1px;background:rgba(234,240,248,.12);margin:6px 8px}
  /* the rail replaces the top-bar menus on bigger screens */
  /* the rail replaces the phone menus and the page's own Night/Day button */
  .dd,.tgl{display:none}
}
```

## Rail
```html
<aside class="rail" aria-label="Site menu">
  <a class="mark" href="https://crnrstone-co.com/" aria-label="crnrstone-co home"><svg class="rmark" viewBox="0 0 100 100" aria-hidden="true"><polygon points="8,8 92,8 92,34 34,34 34,60 8,60" fill="currentColor"/><rect x="40" y="66" width="52" height="26" fill="currentColor"/><rect x="8" y="66" width="26" height="26" fill="#E3A857"/></svg></a>
  <a class="ri" href="https://crnrstone-co.com/"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M3 11l9-7 9 7"/><path d="M5 10v10h14V10"/><path d="M10 20v-6h4v6"/></svg>Home</a>
  <details class="rp"><summary class="ri TOOLS_ON"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="4" y="3" width="16" height="18" rx="2"/><path d="M8 7h8M8 12h2M14 12h2M8 16h2M14 16h2"/></svg>Tools</summary><div class="menu"><a href="https://crnrstone-co.com/calculations/calculator/"><b>Calculator</b><small>Basic and scientific, with GST keys and a history log</small></a><a href="https://crnrstone-co.com/calculations/plan-triangle/"><b>Plan triangle</b><small>Rafter and hip or valley lengths and angles</small></a><a href="https://crnrstone-co.com/calculations/trig-solver/"><b>Trig solver</b><small>Any right-angle triangle from two values</small></a><a href="https://crnrstone-co.com/learn/floor-model/"><b>3D floor model</b><small>See how slab and timber floors go together</small></a><div class="soon"><b>Job calculators and quotes</b><small>Materials for a job, straight into a quote</small></div></div></details>
  <details class="rp"><summary class="ri"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 3l8 3v6c0 4.5-3.4 8-8 9-4.6-1-8-4.5-8-9V6z"/><path d="M9 12l2 2 4-4"/></svg>Vault</summary><div class="menu"><div class="mh">Safety and documents</div><div class="soon"><b>JSA Builder</b><small>Job safety analysis with a risk matrix and crew sign-on</small></div><div class="soon"><b>SWMS Builder</b><small>Safe work method statements for high risk work</small></div><div class="soon"><b>SDS register</b><small>Safety data sheets, PPE at a glance and review dates</small></div><div class="soon"><b>Installation guides</b><small>Manufacturers’ guides and specs on your phone</small></div><div class="soon"><b>Tool registry</b><small>Tools and equipment, who has them, test and tag dates</small></div></div></details>
  <a class="ri" href="https://crnrstone-co.com/learn/floor-model/"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 3l9 5-9 5-9-5z"/><path d="M3 8v8l9 5 9-5V8"/><path d="M12 13v8"/></svg>Learn</a>
  <div class="spacer"></div>
  <a class="ri" href="https://crnrstone-co.com/#updates"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M6 8a6 6 0 1 1 12 0c0 7 3 8 3 8H3s3-1 3-8"/><path d="M10 20a2 2 0 0 0 4 0"/></svg>Join</a>
  <div class="rule"></div>
  <button class="ri" type="button" id="rail-theme" aria-label="Switch to night mode"><svg id="rail-theme-ic" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M21 12.8A9 9 0 1 1 11.2 3a7 7 0 0 0 9.8 9.8z"/></svg><span id="rail-theme-t">Night</span></button>
</aside>
```

## Phone menus (in the tool's top row)
```html
<details class="dd tools"><summary>Tools</summary><div class="menu"><a href="https://crnrstone-co.com/calculations/calculator/"><b>Calculator</b><small>Basic and scientific, with GST keys and a history log</small></a><a href="https://crnrstone-co.com/calculations/plan-triangle/"><b>Plan triangle</b><small>Rafter and hip or valley lengths and angles</small></a><a href="https://crnrstone-co.com/calculations/trig-solver/"><b>Trig solver</b><small>Any right-angle triangle from two values</small></a><a href="https://crnrstone-co.com/learn/floor-model/"><b>3D floor model</b><small>See how slab and timber floors go together</small></a><div class="soon"><b>Job calculators and quotes</b><small>Materials for a job, straight into a quote</small></div></div></details><details class="dd vault"><summary><span class="the">The</span>Vault</summary><div class="menu"><div class="mh">Safety and documents</div><div class="soon"><b>JSA Builder</b><small>Job safety analysis with a risk matrix and crew sign-on</small></div><div class="soon"><b>SWMS Builder</b><small>Safe work method statements for high risk work</small></div><div class="soon"><b>SDS register</b><small>Safety data sheets, PPE at a glance and review dates</small></div><div class="soon"><b>Installation guides</b><small>Manufacturers’ guides and specs on your phone</small></div><div class="soon"><b>Tool registry</b><small>Tools and equipment, who has them, test and tag dates</small></div></div></details>
```

## Logo link (replaces the tool's brand line)
```html
<a class="brand" href="https://crnrstone-co.com/" aria-label="crnrstone-co home"><svg class="mark" viewBox="0 0 100 100" aria-hidden="true"><polygon points="8,8 92,8 92,34 34,34 34,60 8,60" fill="currentColor"/><rect x="40" y="66" width="52" height="26" fill="currentColor"/><rect x="8" y="66" width="26" height="26" fill="#E3A857"/></svg><span class="word">crnrstone<span class="dash">-</span>co</span></a>
```

## Script
```js
/* Top menus: one open at a time; close on outside tap or Escape */
(function () {
  var dds = document.querySelectorAll('details.dd, details.rp');
  dds.forEach(function (d) {
    d.addEventListener('toggle', function () { if (d.open) dds.forEach(function (o) { if (o !== d) o.open = false; }); });
  });
  document.addEventListener('click', function (e) { dds.forEach(function (d) { if (d.open && !d.contains(e.target)) d.open = false; }); });
  document.addEventListener('keydown', function (e) { if (e.key === 'Escape') dds.forEach(function (d) { if (d.open) { d.open = false; d.querySelector('summary').focus(); } }); });
})();
/* Side rail Night/Day button works the same as the top-bar one */
(function () {
  var rb = document.getElementById('rail-theme'), main = document.getElementById('theme');
  if (!rb || !main) return;
  function sync() {
    var dark = main.getAttribute('aria-label') === 'Switch to day mode';
    document.getElementById('rail-theme-t').textContent = dark ? 'Day' : 'Night';
    rb.setAttribute('aria-label', main.getAttribute('aria-label'));
    document.getElementById('rail-theme-ic').innerHTML = document.getElementById('theme-ic').innerHTML;
  }
  rb.addEventListener('click', function () { main.click(); sync(); });
  main.addEventListener('click', function () { setTimeout(sync, 0); });
  sync();
})();
```

## When copying a tool to the website
Nothing to change: the links already point at https://crnrstone-co.com/.
