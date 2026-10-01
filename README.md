<!doctype html><html><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#faf9f5;color:#141413}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>SME Roster Planner</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Schibsted+Grotesk:wght@500;700;800&family=Instrument+Sans:wght@400;500;600&family=JetBrains+Mono:wght@400;600&display=swap">
<style>
/* Layout: an operations console. Status strip on top, tabbed work area below; wide grids scroll inside their own frames. */
:root {
  --bg: #F2F5F5; --surface: #FFFFFF; --surface-2: #E8EEEF; --line: #D2DCDE;
  --ink: #12232A; --muted: #586A70; --accent: #0D6C79; --accent-ink: #FFFFFF; --accent-soft: #D5ECEF;
  --gap: #B8322A; --gap-bg: #F8DAD6; --below: #A9520D; --below-bg: #FBE3CB;
  --thin: #7D6200; --thin-bg: #F8EDC2; --ok: #2B7148; --ok-bg: #DCEFE2;
  --s0: #FBE6C2; --s1: #CDEBEE; --s2: #DADBF6; --s3: #F1D9E9; --sx: #E4E4E4;
  --off: #EDF1F2; --off-ink: #7A8B90; --leave: #F5D7E5; --leave-ink: #87204F;
  --display: "Schibsted Grotesk", "Helvetica Neue", Arial, sans-serif;
  --body: "Instrument Sans", "Segoe UI", system-ui, sans-serif;
  --mono: "JetBrains Mono", ui-monospace, "SF Mono", Menlo, monospace;
  --r: 10px;
}
@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) {
  --bg: #0E191D; --surface: #15232A; --surface-2: #1C2D34; --line: #2A3D45;
  --ink: #E2ECEE; --muted: #93A7AD; --accent: #4CBFCD; --accent-ink: #062428; --accent-soft: #163B42;
  --gap: #FF8D80; --gap-bg: #4B1F1B; --below: #F2A35E; --below-bg: #432E18;
  --thin: #E6C75A; --thin-bg: #3A3214; --ok: #7AD29D; --ok-bg: #173826;
  --s0: #4A3A1C; --s1: #15404A; --s2: #2A2C58; --s3: #4A2641; --sx: #333;
  --off: #18272D; --off-ink: #7F949A; --leave: #4A2135; --leave-ink: #F5A8CA;
  color-scheme: dark; } }
:root[data-theme="dark"] {
  --bg: #0E191D; --surface: #15232A; --surface-2: #1C2D34; --line: #2A3D45;
  --ink: #E2ECEE; --muted: #93A7AD; --accent: #4CBFCD; --accent-ink: #062428; --accent-soft: #163B42;
  --gap: #FF8D80; --gap-bg: #4B1F1B; --below: #F2A35E; --below-bg: #432E18;
  --thin: #E6C75A; --thin-bg: #3A3214; --ok: #7AD29D; --ok-bg: #173826;
  --s0: #4A3A1C; --s1: #15404A; --s2: #2A2C58; --s3: #4A2641; --sx: #333;
  --off: #18272D; --off-ink: #7F949A; --leave: #4A2135; --leave-ink: #F5A8CA;
  color-scheme: dark; }

* { box-sizing: border-box; }
body { background: var(--bg); color: var(--ink); font-family: var(--body); font-size: 14px; line-height: 1.5; }
.shell { max-width: 1280px; margin: 0 auto; padding-inline: 20px; padding-block: 18px 60px; display: flex; flex-direction: column; gap: 16px; }
h1, h2, h3 { font-family: var(--display); text-wrap: balance; margin: 0; letter-spacing: -0.01em; }
h1 { font-size: 22px; font-weight: 800; }
h2 { font-size: 17px; font-weight: 700; }
h3 { font-size: 14px; font-weight: 700; }
p { margin: 0; }
.hint { color: var(--muted); font-size: 13px; max-width: 75ch; }
.mono, .tnum { font-family: var(--mono); font-variant-numeric: tabular-nums; }
button, select, input { font: inherit; color: inherit; }
:focus-visible { outline: 2px solid var(--accent); outline-offset: 2px; }

.top { display: flex; align-items: center; justify-content: space-between; gap: 12px; flex-wrap: wrap; }
.brand { display: flex; align-items: center; gap: 12px; }
.brand p { color: var(--muted); font-size: 13px; }
.mark { width: 38px; height: 38px; border-radius: 9px; background: var(--ink); display: grid; place-items: center; flex: none; }
.savestate { font-size: 12px; color: var(--muted); display: flex; align-items: center; gap: 6px; }
.savestate::before { content: ""; width: 8px; height: 8px; border-radius: 50%; background: var(--muted); }
.savestate.ok::before { background: var(--ok); }
.savestate.warn::before { background: var(--below); }

.summary { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 8px; }
.stat { background: var(--surface); border: 1px solid var(--line); border-radius: var(--r); padding: 10px 12px; display: flex; flex-direction: column; gap: 2px; min-width: 0; }
.stat b { font-family: var(--mono); font-size: 20px; font-weight: 600; }
.stat span { font-size: 12px; color: var(--muted); }
.stat.gap b { color: var(--gap); } .stat.below b { color: var(--below); } .stat.thin b { color: var(--thin); } .stat.ok b { color: var(--ok); }

.tabs { display: flex; gap: 4px; border-bottom: 1px solid var(--line); overflow-x: auto; }
.tabs button { background: none; border: 0; padding: 10px 14px; cursor: pointer; color: var(--muted); font-weight: 600; border-bottom: 2px solid transparent; white-space: nowrap; }
.tabs button[aria-selected="true"] { color: var(--ink); border-bottom-color: var(--accent); }

.panel { display: flex; flex-direction: column; gap: 16px; }
.card { background: var(--surface); border: 1px solid var(--line); border-radius: var(--r); padding: 16px; display: flex; flex-direction: column; gap: 12px; min-width: 0; }
.card-h { display: flex; align-items: center; justify-content: space-between; gap: 10px; flex-wrap: wrap; }
.row { display: flex; gap: 8px; flex-wrap: wrap; align-items: center; }
.btn { background: var(--surface); border: 1px solid var(--line); border-radius: 8px; padding: 7px 12px; cursor: pointer; font-weight: 600; font-size: 13px; }
.btn:hover { border-color: var(--accent); }
.btn.primary { background: var(--accent); color: var(--accent-ink); border-color: var(--accent); }
.btn.danger { color: var(--gap); }
.btn.small { padding: 4px 9px; font-size: 12px; }
.weeks { display: flex; gap: 6px; flex-wrap: wrap; }
.weeks button { border: 1px solid var(--line); background: var(--surface); border-radius: 999px; padding: 5px 12px; cursor: pointer; font-size: 12px; font-weight: 600; }
.weeks button[aria-pressed="true"] { background: var(--ink); color: var(--bg); border-color: var(--ink); }
.toggle { display: inline-flex; align-items: center; gap: 8px; font-weight: 600; font-size: 13px; cursor: pointer; }
.toggle input { width: 16px; height: 16px; accent-color: var(--gap); }

.scroll { overflow-x: auto; border: 1px solid var(--line); border-radius: 8px; }
table { border-collapse: separate; border-spacing: 0; width: 100%; font-size: 13px; }
th, td { padding: 6px 8px; border-bottom: 1px solid var(--line); text-align: left; vertical-align: middle; }
thead th { background: var(--surface-2); font-size: 12px; font-weight: 600; color: var(--muted); position: sticky; top: 0; white-space: nowrap; }
tbody tr:last-child td { border-bottom: 0; }

/* roster grid */
.grid th.day { text-align: center; min-width: 78px; }
.grid th.day span { display: block; font-size: 11px; text-transform: uppercase; letter-spacing: .06em; }
.grid th.day b { color: var(--ink); font-family: var(--mono); font-weight: 600; }
.grid th.day.wkend { background: color-mix(in srgb, var(--surface-2) 70%, var(--accent-soft)); }
.grid .who { position: sticky; left: 0; background: var(--surface); z-index: 1; min-width: 130px; border-right: 1px solid var(--line); }
.grid thead .who { background: var(--surface-2); z-index: 2; }
.grid .who b { display: block; font-weight: 600; }
.grid .who small { color: var(--muted); font-family: var(--mono); font-size: 11px; }
.grid td.c { text-align: center; padding: 3px; border-left: 1px solid var(--surface); }
.cell { border-radius: 6px; padding: 6px 4px; min-height: 40px; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 2px; font-family: var(--mono); font-size: 12px; width: 100%; border: 0; color: var(--ink); }
.cell b { font-weight: 600; }
button.cell { cursor: pointer; }
button.cell:hover { outline: 2px solid var(--gap); outline-offset: -2px; }
.s0 { background: var(--s0); } .s1 { background: var(--s1); } .s2 { background: var(--s2); } .s3 { background: var(--s3); } .sx { background: var(--sx); }
.cell.off { background: var(--off); color: var(--off-ink); font-size: 11px; letter-spacing: .06em; }
.cell.al { background: var(--leave); color: var(--leave-ink); font-weight: 600; font-size: 11px; letter-spacing: .06em; }
.cell.mc { background: repeating-linear-gradient(135deg, var(--gap-bg) 0 6px, var(--surface) 6px 10px); color: var(--gap); }
.cell.mc b { text-decoration: line-through; opacity: .6; }
.cell.tr { background-image: repeating-linear-gradient(45deg, transparent 0 5px, color-mix(in srgb, var(--ink) 8%, transparent) 5px 7px); }
.tag { font-style: normal; font-family: var(--body); font-size: 10px; font-weight: 600; border-radius: 4px; padding: 0 4px; background: var(--surface); color: var(--accent); line-height: 1.5; }
.tag.tr { color: var(--below); }
.tag.mc { color: var(--gap); }
.dot { width: 6px; height: 6px; border-radius: 50%; background: var(--accent); display: inline-block; }
.prevcol { font-family: var(--mono); font-size: 11px; color: var(--muted); white-space: nowrap; border-right: 1px dashed var(--line); }
tfoot td { background: var(--surface-2); font-size: 12px; text-align: center; font-family: var(--mono); }
tfoot td.who { text-align: left; font-family: var(--body); color: var(--muted); background: var(--surface-2); }
.legend { display: flex; flex-wrap: wrap; gap: 6px 14px; font-size: 12px; color: var(--muted); align-items: center; }
.legend i { display: inline-block; width: 14px; height: 14px; border-radius: 4px; vertical-align: -2px; margin-right: 5px; }

/* tiers */
.t-gap { background: var(--gap-bg); color: var(--gap); font-weight: 600; }
.t-below { background: var(--below-bg); color: var(--below); font-weight: 600; }
.t-thin { background: var(--thin-bg); color: var(--thin); }
.t-ok { background: var(--ok-bg); color: var(--ok); }
.pill { display: inline-block; padding: 1px 8px; border-radius: 999px; font-size: 11px; font-weight: 600; white-space: nowrap; }

.heat td, .heat th { text-align: center; padding: 4px 6px; }
.heat td.h { font-family: var(--mono); color: var(--muted); font-size: 11px; text-align: right; background: var(--surface); position: sticky; left: 0; white-space: nowrap; }
.heat td.v { font-family: var(--mono); font-size: 12px; min-width: 56px; border-left: 2px solid var(--surface); }

.team input[type="text"] { width: 100%; min-width: 120px; }
.team select, .team input, .form select, .form input { background: var(--surface); border: 1px solid var(--line); border-radius: 6px; padding: 5px 7px; }
.team td { white-space: nowrap; }
.namecell { display: flex; gap: 6px; align-items: center; }
.namecell .rm { color: var(--gap); }
.form { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 12px 16px; }
.field { display: flex; flex-direction: column; gap: 4px; min-width: 0; }
.field label, .field .lbl { font-size: 12px; font-weight: 600; color: var(--muted); }
.field small { color: var(--muted); font-size: 12px; }
.chk { display: flex; gap: 8px; align-items: flex-start; font-size: 13px; }
.presets { display: flex; flex-wrap: wrap; gap: 6px; }
.shiftset { display: flex; gap: 8px; flex-wrap: wrap; }
.note { border-radius: 8px; padding: 10px 12px; font-size: 13px; }
.note.warn { background: var(--below-bg); color: var(--ink); }
.note.bad { background: var(--gap-bg); color: var(--ink); }
.note.good { background: var(--ok-bg); color: var(--ink); }
.note.info { background: var(--accent-soft); color: var(--ink); }
ul.log { list-style: none; margin: 0; padding: 0; display: flex; flex-direction: column; }
ul.log li { padding: 8px 0; border-bottom: 1px solid var(--line); display: flex; gap: 10px; align-items: baseline; }
ul.log li:last-child { border-bottom: 0; }
ul.log li .pill { flex: none; }
ul.log small { color: var(--muted); display: block; }
.sugg { display: flex; flex-direction: column; gap: 8px; }
.sugg li { display: flex; justify-content: space-between; gap: 10px; align-items: baseline; }
.two { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 1fr); gap: 16px; }
@media (max-width: 860px) { .two { grid-template-columns: minmax(0, 1fr); } }
.empty { text-align: left; padding: 28px; display: flex; flex-direction: column; gap: 14px; max-width: 560px; }
.err { color: var(--gap); font-size: 13px; min-height: 1em; }
#toast { position: fixed; left: 50%; transform: translateX(-50%); bottom: calc(16px + env(safe-area-inset-bottom, 0px)); background: var(--ink); color: var(--bg); padding: 8px 14px; border-radius: 8px; font-size: 13px; opacity: 0; pointer-events: none; transition: opacity .2s; z-index: 10; }
#toast.on { opacity: 1; }
@media (prefers-reduced-motion: reduce) { #toast { transition: none; } }
@media (max-width: 520px) { .shell { padding-inline: 16px; } h1 { font-size: 19px; } }
</style>

<div class="shell">
  <header class="top">
    <div class="brand">
      <div class="mark" aria-hidden="true">
        <svg width="22" height="22" viewBox="0 0 22 22"><circle cx="11" cy="11" r="9" fill="none" stroke="var(--bg)" stroke-width="2"/><path d="M11 11 L11 4" stroke="var(--bg)" stroke-width="2" stroke-linecap="round"/><path d="M11 11 L16 14" stroke="var(--accent)" stroke-width="2" stroke-linecap="round"/></svg>
      </div>
      <div><h1>SME Roster Planner</h1><p>24/7 coverage · Sat–Fri schedule weeks · Mon–Sun payroll · 2 off-days</p></div>
    </div>
    <div id="saveState" class="savestate">Loading team…</div>
  </header>
  <section id="summary" class="summary" aria-label="Plan health"></section>
  <nav class="tabs" role="tablist" id="tabs"></nav>
  <section id="panel" class="panel"><div class="card empty"><h2>Loading your team</h2><p class="hint">Your saved roster appears here in a moment.</p></div></section>
</div>
<div id="toast" role="status" aria-live="polite"></div>

<script>
(() => {
'use strict';
const DOW = ['Sat','Sun','Mon','Tue','Wed','Thu','Fri'];
const MON = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
const PAIRS = ['Mon & Tue','Tue & Wed','Wed & Thu','Thu & Fri','Fri & Sat','Sat & Sun','Sun & Mon'];
// Day offsets inside a Mon–Sun payroll week (Mon = 0). Sun & Mon takes that week's Sunday and Monday,
// which in practice runs Sunday into the next Monday, and still gives exactly 2 off per payroll week.
const PAIR_DAYS = [[0, 1], [1, 2], [2, 3], [3, 4], [4, 5], [5, 6], [0, 6]];
const PRESETS = [
  { name: 'Allowance handover', starts: [0, 8, 16] },
  { name: 'Late day', starts: [7, 16, 23] },
  { name: 'Early start', starts: [5, 13, 21] },
  { name: '04:00 balanced', starts: [4, 12, 20] },
  { name: 'Four shifts', starts: [2, 8, 14, 20] },
];
const TABS = [['roster','Roster'],['risk','Coverage & MC risk'],['team','Team & leave'],['rules','Rules'],['checks','Checks & log']];
const DOC_PATH = 'plans/main', LS_KEY = 'sme-roster-planner.v1', UI_KEY = 'sme-roster-planner.ui', CLIENT = Math.random().toString(36).slice(2);

const $ = (s) => document.querySelector(s);
const esc = (s) => String(s ?? '').replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const pad = (n) => String(n).padStart(2, '0');
const m24 = (h) => ((h % 24) + 24) % 24;
const hh = (h) => pad(m24(h)) + ':00';
const span = (s, L) => `${hh(s)}–${hh(s + L)}`;
// Night shift allowance applies to shifts starting 16:00–04:00. A 15:00 start just misses it, so avoid it.
const allowance = (h) => { h = m24(h); return h >= 16 || h <= 4; };
const startPenalty = (base, use) => (m24(use) === 15 ? 10 : 0) + (allowance(base) && !allowance(use) ? 10 : 0);
const spanShort = (s, L) => `${pad(m24(s))}–${pad(m24(s + L))}`;
const T0 = (s) => Date.parse(s + 'T00:00:00Z');
const addDays = (s, n) => new Date(T0(s) + n * 864e5).toISOString().slice(0, 10);
const dayDiff = (a, b) => Math.round((T0(b) - T0(a)) / 864e5);
const jsDow = (s) => new Date(T0(s)).getUTCDay();
const snapSat = (s) => addDays(s, -((jsDow(s) + 1) % 7));
const uid = () => 's' + Math.random().toString(36).slice(2, 9);
const isISO = (s) => typeof s === 'string' && /^\d{4}-\d{2}-\d{2}$/.test(s) && !isNaN(T0(s));
function todayISO() { const d = new Date(); return `${d.getFullYear()}-${pad(d.getMonth() + 1)}-${pad(d.getDate())}`; }
function nextSat() { const t = todayISO(); return addDays(t, (6 - jsDow(t) + 7) % 7); }
function fmtD(s) { const d = new Date(T0(s)); return `${['Sun','Mon','Tue','Wed','Thu','Fri','Sat'][d.getUTCDay()]} ${d.getUTCDate()} ${MON[d.getUTCMonth()]}`; }
function fmtS(s) { const d = new Date(T0(s)); return `${d.getUTCDate()} ${MON[d.getUTCMonth()]}`; }
function clampInt(v, a, b, dflt) { const n = parseInt(v, 10); return Number.isFinite(n) ? Math.min(b, Math.max(a, n)) : dflt; }
const clone = (o) => JSON.parse(JSON.stringify(o));

/* ---------- plan shape ---------- */
function defaultSettings() {
  return { start: nextSat(), weeks: 4, starts: [0, 8, 16], shiftLen: 9, minStaff: 2, rotateEvery: 2, rotateOffs: false, maxSlide: 2, restMin: 12, maxRun: 7, weekendExtra: 1 };
}
function makeTeam(n, nS) {
  return Array.from({ length: n }, (_, i) => ({ id: uid(), name: `SME ${i + 1}`, base: i % nS, offPref: -1, prevStart: null, prevOff: [], leaves: [] }));
}
function normalize(p) {
  const s = Object.assign(defaultSettings(), p?.settings || {});
  s.start = isISO(s.start) ? snapSat(s.start) : nextSat();
  s.weeks = clampInt(s.weeks, 1, 8, 4);
  let st = (Array.isArray(s.starts) ? s.starts : []).map(x => clampInt(x, 0, 23, 0));
  st = [...new Set(st)].sort((a, b) => a - b).slice(0, 4);
  s.starts = st.length >= 2 ? st : [0, 8, 16];
  s.shiftLen = [8, 9, 10, 12].includes(+s.shiftLen) ? +s.shiftLen : 9;
  s.minStaff = clampInt(s.minStaff, 1, 5, 2);
  s.rotateEvery = [0, 1, 2, 4].includes(+s.rotateEvery) ? +s.rotateEvery : 2;
  s.rotateOffs = false;
  s.maxSlide = clampInt(s.maxSlide, 0, 4, 2);
  s.restMin = clampInt(s.restMin, 8, 16, 12);
  s.maxRun = clampInt(s.maxRun, 5, 12, 7);
  s.weekendExtra = clampInt(s.weekendExtra, 0, 1, 1);
  const staff = (Array.isArray(p?.staff) ? p.staff : []).slice(0, 60).map((x, i) => ({
    id: typeof x?.id === 'string' && x.id ? x.id : uid(),
    name: String(x?.name ?? `SME ${i + 1}`).slice(0, 60),
    base: clampInt(x?.base, 0, s.starts.length - 1, 0),
    offPref: clampInt(x?.offPref, -1, 6, -1),
    prevStart: x?.prevStart == null || x?.prevStart === '' ? null : clampInt(x.prevStart, 0, 23, null),
    prevOff: (Array.isArray(x?.prevOff) ? x.prevOff : []).map(v => clampInt(v, 0, 6, -1)).filter((v, j, a) => v >= 0 && a.indexOf(v) === j).slice(0, 2),
    leaves: (Array.isArray(x?.leaves) ? x.leaves : []).filter(l => l && isISO(l.from) && isISO(l.to)).map(l => ({
      id: l.id || uid(), from: l.from <= l.to ? l.from : l.to, to: l.from <= l.to ? l.to : l.from, note: String(l.note || '').slice(0, 80) })),
  }));
  return { settings: s, staff };
}

/* ---------- scheduling engine ---------- */
function computeSchedule(plan) {
  const S = plan.settings, starts = S.starts, nS = starts.length, L = S.shiftLen, MIN = S.minStaff;
  const W = S.weeks, D = W * 7, ND = D + 2, H = ND * 24;
  const tStart = performance.now(), inBudget = () => performance.now() - tStart < 1500;
  const nomIdx = (p, d) => { const k = Math.floor(d / 7); const r = S.rotateEvery > 0 ? Math.floor(k / S.rotateEvery) : 0; return (p.base + r) % nS; };
  const nominal = (p, d) => starts[nomIdx(p, d)];
  const dateOf = (d) => addDays(S.start, d);

  const P = plan.staff.map((s, i) => {
    const leave = new Uint8Array(ND);
    for (const r of s.leaves) {
      const a = dayDiff(S.start, r.from), b = dayDiff(S.start, r.to);
      for (let d = Math.max(0, a); d <= Math.min(ND - 1, b); d++) leave[d] = 1;
    }
    return { i, id: s.id, name: s.name.trim() || `SME ${i + 1}`, base: Math.min(s.base, nS - 1), fixed: s.offPref, prevStart: s.prevStart, prevOff: s.prevOff, leave };
  });

  // Starting point for recommended off-days: spread evenly inside each base-shift group.
  const groups = {};
  P.forEach(p => { if (p.fixed < 0) (groups[p.base] ??= []).push(p); });
  Object.values(groups).forEach(g => g.forEach((p, j) => { p.baseOff = Math.floor(j * 7 / g.length) % 6; }));
  P.forEach(p => { if (p.fixed >= 0) p.baseOff = p.fixed; });
  let typical = null;
  const WX = S.weekendExtra;
  // Recommended fixed off-days: start from an even spread, then improve each SME's pair in turn
  // against everyone else's (including pairs fixed by hand) on a typical Mon–Sun week, until nothing improves.
  {
    const wk = new Float64Array(168);
    const place = (p, a, sg) => { const s0 = starts[p.base]; for (let d = 0; d < 7; d++) { if (PAIR_DAYS[a].includes(d)) continue; for (let k = 0; k < L; k++) wk[(d * 24 + s0 + k) % 168] += sg; } };
    const wcost = () => { let x = 0; for (let t = 0; t < 168; t++) { const v = wk[t]; if (v <= 0) x += 40; if (v < MIN) x += (MIN - v) * 8; if (t >= 120) x -= WX * 0.6 * v; x += 1 / (v + 1); } return x; };
    P.forEach(p => place(p, p.baseOff, 1));
    const autos = P.filter(p => p.fixed < 0);
    for (let pass = 0; pass < 20; pass++) {
      let moved = false;
      for (const p of autos) {
        place(p, p.baseOff, -1);
        let best = p.baseOff, bc = (place(p, p.baseOff, 1), wcost()); place(p, p.baseOff, -1);
        for (let a = 0; a < PAIR_DAYS.length; a++) {
          if (a === p.baseOff) continue;
          place(p, a, 1); const c = wcost(); place(p, a, -1);
          if (c < bc - 1e-9) { bc = c; best = a; }
        }
        if (best !== p.baseOff) moved = true;
        p.baseOff = best; place(p, best, 1);
      }
      if (!moved) break;
    }
    let wd = 0, we = 0;
    for (let t = 0; t < 168; t++) { if (t >= 120) we += wk[t]; else wd += wk[t]; }
    typical = { weekday: wd / 120, weekend: we / 48 };
  }
  const offsetFor = (p) => p.fixed >= 0 ? p.fixed : p.baseOff;
  const recommended = Object.fromEntries(P.map(p => [p.id, p.baseOff]));

  // Payroll weeks (Mon–Sun). Week 0 = Sat/Sun of schedule week 1, which closes last payroll week.
  const weeks = [{ n: 0, days: [0, 1] }];
  for (let w = 1; w <= W; w++) { const m = 2 + 7 * (w - 1); weeks.push({ n: w, days: [m, m + 1, m + 2, m + 3, m + 4, m + 5, m + 6] }); }

  P.forEach(p => {
    p.hasPrevOff = p.prevOff.length > 0;
    p.prevStartEff = p.prevStart ?? nominal(p, 0);
    if (p.hasPrevOff) p.prevOffDays = p.prevOff.map(dw => dw - 7);
    else { const a0 = offsetFor(p, 0); p.prevOffDays = PAIR_DAYS[a0].map(x => x - 5).filter(d => d < 0); }
    p.prevWorked = (d) => !p.prevOffDays.includes(d);
    p.lastEnd = -1e9;
    for (let d = -1; d >= -7; d--) if (p.prevWorked(d)) { p.lastEnd = d * 24 + p.prevStartEff + L; break; }
    p.prevRun = 0;
    for (let d = -1; d >= -7 && p.prevWorked(d); d--) p.prevRun++;
  });

  function bestPair(p, wk, td) {
    const avail = wk.filter(d => !p.leave[d]);
    const need = Math.min(2, avail.length);
    if (need === 0) return [];
    if (need === 1) return [avail[0]];
    let best = null, bs = -1e9;
    for (let x = 0; x < avail.length; x++) for (let y = x + 1; y < avail.length; y++) {
      const a = avail[x], b = avail[y];
      let sc = 0;
      if (b === a + 1) sc += 3;
      if (p.leave[a - 1] || p.leave[a + 1]) sc += 1.5;
      if (p.leave[b - 1] || p.leave[b + 1]) sc += 1.5;
      if (td.includes(a)) sc += 1;
      if (td.includes(b)) sc += 1;
      if (sc > bs) { bs = sc; best = [a, b]; }
    }
    return best;
  }

  const off = P.map(() => new Uint8Array(ND)), patt = P.map(() => new Uint8Array(ND)), init = P.map(() => new Uint8Array(ND));
  P.forEach(p => {
    const i = p.i;
    let w0 = [];
    const avail0 = [0, 1].filter(d => !p.leave[d]);
    if (p.hasPrevOff) {
      const c = p.prevOff.filter(dw => dw >= 2).length;
      p.p0prev = c;
      p.p0avail = avail0.length;
      const need = Math.min(Math.max(0, 2 - c), avail0.length);
      if (need >= 2) w0 = [0, 1];
      else if (need === 1) {
        const pref = p.prevOff.includes(6) ? 0 : (PAIR_DAYS[offsetFor(p, 1)].includes(0) ? 1 : 0);
        w0 = [avail0.includes(pref) ? pref : avail0[0]];
      }
    } else {
      const a0 = offsetFor(p, 0);
      w0 = PAIR_DAYS[a0].map(x => x - 5).filter(d => d >= 0);
      p.p0prev = null;
    }
    w0.forEach(d => { patt[i][d] = 1; if (!p.leave[d]) off[i][d] = 1; });
    for (let w = 1; w <= W; w++) {
      const wk = weeks[w].days, a = offsetFor(p, w), td = PAIR_DAYS[a].map(x => wk[x]);
      td.forEach(d => { patt[i][d] = 1; });
      const pick = td.some(d => p.leave[d]) ? bestPair(p, wk, td) : td;
      pick.forEach(d => { off[i][d] = 1; });
    }
    init[i].set(off[i]);
  });

  const slide = P.map(() => new Int8Array(ND));
  // Daily start times. A shift change (rotation or transition) only happens once the rest rule allows it;
  // until then the SME stays on their previous start time.
  function tl(p, offA = off[p.i], slA = slide[p.i]) {
    const st = new Int8Array(ND), start = new Int32Array(ND), tr = new Uint8Array(ND);
    let cur = p.prevStartEff, last = p.lastEnd;
    for (let d = 0; d < ND; d++) {
      if (p.leave[d]) { st[d] = 2; continue; }
      if (offA[d]) { st[d] = 1; continue; }
      const nom = nominal(p, d);
      let use;
      if (cur === nom || d * 24 + nom - last >= S.restMin) { cur = nom; use = nom + slA[d]; }
      else { use = cur; tr[d] = 1; }
      start[d] = d * 24 + use;
      last = start[d] + L;
    }
    return { st, start, tr };
  }

  const count = new Int16Array(H);
  P.forEach(p => { if (p.prevWorked(-1)) { const s = -24 + p.prevStartEff; for (let t = Math.max(0, s); t < Math.min(H, s + L); t++) count[t]++; } });
  function addTL(T, sg, c = count) {
    for (let d = 0; d < ND; d++) if (T.st[d] === 0) { const s = T.start[d]; for (let t = Math.max(0, s), e = Math.min(H, s + L); t < e; t++) c[t] += sg; }
  }
  const cov = (a, b, c = count) => { let x = 0; for (let t = a; t < b; t++) { const v = c[t]; if (v <= 0) x += 40; if (v < MIN) x += (MIN - v) * 8; else if (v === MIN) x += 0.1; } return x; };
  function restBad(p, T) {
    let last = p.lastEnd, b = 0;
    for (let d = 0; d < ND; d++) if (T.st[d] === 0) { if (T.start[d] - last < S.restMin) b++; last = T.start[d] + L; }
    return b;
  }
  function pcost(p, T) {
    const i = p.i;
    let c = 0, run = p.prevRun;
    for (let d = 0; d < ND; d++) {
      if (T.st[d] === 0) { run++; if (run > S.maxRun) c += 12; if (T.tr[d]) c += 0.3; if (init[i][d]) c += 0.6; }
      else { run = 0; if (T.st[d] === 1 && !init[i][d]) c += 0.6; }
    }
    for (let w = 1; w <= W; w++) {
      const o = weeks[w].days.filter(d => T.st[d] === 1);
      if (o.length === 2 && o[1] !== o[0] + 1 && o[1] - o[0] !== 6 && !(p.leave[o[0] - 1] || p.leave[o[0] + 1] || p.leave[o[1] - 1] || p.leave[o[1] + 1])) c += 1.5;
    }
    return c + restBad(p, T) * 50;
  }
  function changedRange(A, B) {
    let lo = -1, hi = -1;
    for (let d = 0; d < ND; d++) if (A.st[d] !== B.st[d] || (A.st[d] === 0 && A.start[d] !== B.start[d])) { if (lo < 0) lo = d; hi = d; }
    return lo < 0 ? null : [Math.max(0, lo * 24 - 24), Math.min(H, hi * 24 + 48 + L)];
  }
  const TL = P.map(p => tl(p));
  TL.forEach(T => addTL(T, 1));
  const PC = P.map(p => pcost(p, TL[p.i]));
  function tryChange(p, T2) {
    const T = TL[p.i], r = changedRange(T, T2);
    if (!r) return null;
    const before = cov(r[0], r[1]);
    addTL(T, -1); addTL(T2, 1);
    const after = cov(r[0], r[1]);
    addTL(T2, -1); addTL(T, 1);
    return after - before + pcost(p, T2) - PC[p.i];
  }
  function commit(p, T2) { addTL(TL[p.i], -1); addTL(T2, 1); TL[p.i] = T2; PC[p.i] = pcost(p, T2); }

  // Pass 1: only in payroll weeks where someone is on leave, move off-days inside that week
  // (keeps exactly 2) to lift short hours. Every other week keeps everyone's fixed off-days.
  const leaveWeek = weeks.map(wk => P.some(p => wk.days.some(d => p.leave[d])));
  for (let pass = 0; pass < 25 && inBudget(); pass++) {
    let any = false;
    for (const p of P) {
      if (p.fixed >= 0) continue;
      const i = p.i;
      for (const wk of weeks) {
        if (!leaveWeek[wk.n]) continue;
        const offs = wk.days.filter(d => off[i][d] && !p.leave[d]);
        const works = wk.days.filter(d => !off[i][d] && !p.leave[d]);
        let best = null;
        for (const o of offs) for (const w of works) {
          off[i][o] = 0; off[i][w] = 1;
          const T2 = tl(p);
          off[i][w] = 0; off[i][o] = 1;
          const delta = tryChange(p, T2);
          if (delta != null && delta < -1e-6 && (!best || delta < best.delta)) best = { o, w, T2, delta };
        }
        if (best) { off[i][best.o] = 0; off[i][best.w] = 1; commit(p, best.T2); any = true; }
      }
    }
    if (!any) break;
  }

  // Pass 2: slide start times up to ±maxSlide hours from the SME's own shift to close what is left.
  if (S.maxSlide > 0) for (let it = 0; it < 300 && inBudget(); it++) {
    const days = new Set();
    for (let t = 0; t < H; t++) if (count[t] < MIN) { const d = Math.floor(t / 24); days.add(d); days.add(d - 1); }
    if (!days.size) break;
    let best = null;
    for (const d of days) {
      if (d < 0 || d >= ND) continue;
      for (const p of P) {
        const i = p.i, T = TL[i];
        if (T.st[d] !== 0 || T.tr[d]) continue;
        const cur = slide[i][d];
        for (let o = -S.maxSlide; o <= S.maxSlide; o++) {
          if (o === cur) continue;
          slide[i][d] = o; const T2 = tl(p); slide[i][d] = cur;
          const dl = tryChange(p, T2);
          if (dl == null) continue;
          const nom = nominal(p, d);
          const delta = dl + 0.25 * (Math.abs(o) - Math.abs(cur)) + startPenalty(nom, nom + o) - startPenalty(nom, nom + cur);
          if (delta < -1e-6 && (!best || delta < best.delta)) best = { i, d, o, T2, delta };
        }
      }
    }
    if (!best) break;
    slide[best.i][best.d] = best.o;
    commit(P[best.i], best.T2);
  }

  /* ---- explanations ---- */
  const listDays = (ds) => ds.length ? ds.map(d => fmtD(dateOf(d))).join(' & ') : 'none';
  const logs = [];
  P.forEach(p => {
    const i = p.i, T = TL[i];
    const trDays = [];
    for (let d = 0; d < D; d++) if (T.st[d] === 0 && T.tr[d]) trDays.push(d);
    if (trDays.length) {
      const old = T.start[trDays[0]] - trDays[0] * 24, nw = nominal(p, trDays[trDays.length - 1]);
      logs.push({ kind: 'transition', i, d: trDays[0], text: `${p.name} stays on ${span(old, L)} on ${listDays(trDays)}`,
        reason: `Moving straight to ${span(nw, L)} would leave less than ${S.restMin} h rest, so the switch happens after a day off.` });
    }
    weeks.forEach(wk => {
      const pat = wk.days.filter(d => patt[i][d]), fin = wk.days.filter(d => T.st[d] === 1);
      if (pat.join() === fin.join()) return;
      if (!pat.some(d => d < D) && !fin.some(d => d < D)) return;
      const ownClash = pat.some(d => p.leave[d]);
      const removed = pat.filter(d => !fin.includes(d));
      const others = [...new Set(P.filter(q => q !== p && removed.concat(fin).some(d => q.leave[d])).map(q => q.name))];
      const reason = ownClash ? 'Their usual off-days fell on annual leave, so that week they were placed around it.'
        : others.length ? `Keeps coverage while ${others.slice(0, 3).join(', ')}${others.length > 3 ? ' and others' : ''} ${others.length > 1 ? 'are' : 'is'} on leave.`
        : 'Moved to keep every hour at target staffing.';
      logs.push({ kind: 'off', i, d: (fin[0] ?? pat[0]), text: `${p.name}: off ${listDays(pat)} → ${listDays(fin)}`, reason });
    });
    for (let d = 0; d < D; d++) {
      const o = slide[i][d];
      if (!o || T.st[d] !== 0 || T.tr[d]) continue;
      const nom = nominal(p, d);
      const covers = o > 0 ? `${hh(nom + L)}–${hh(nom + L + o)}` : `${hh(nom + o)}–${hh(nom)}`;
      logs.push({ kind: 'slide', i, d, text: `${p.name} · ${fmtD(dateOf(d))}: ${span(nom + o, L)} instead of ${span(nom, L)} (${o > 0 ? '+' : ''}${o} h)`, reason: `Covers ${covers}, which would otherwise be short.` });
    }
  });
  logs.sort((a, b) => a.d - b.d);

  const payroll = P.map(p => {
    const T = TL[p.i];
    return weeks.map(wk => {
      let offs = wk.days.filter(d => T.st[d] === 1).length;
      const lv = wk.days.filter(d => p.leave[d]).length;
      let req = null, checked = true;
      if (wk.n === 0) {
        if (!p.hasPrevOff) checked = false;
        else { offs += p.p0prev; req = Math.max(p.p0prev, Math.min(2, p.p0prev + p.p0avail)); req = Math.min(req, 2); }
      } else req = Math.min(2, 7 - lv);
      return { offs, req, checked, ok: !checked || offs === req, projected: wk.days.some(d => d >= D), leave: lv };
    });
  });

  const fair = P.map(p => {
    const T = TL[p.i];
    let work = 0, night = 0, wkndOff = 0, al = 0, sl = 0, run = p.prevRun, maxRun = 0, tr = 0;
    for (let d = 0; d < D; d++) {
      if (T.st[d] === 0) {
        work++; if (allowance(T.start[d])) night++;
        if (slide[p.i][d] && !T.tr[d]) sl++;
        if (T.tr[d]) tr++;
        run++; maxRun = Math.max(maxRun, run);
      } else { run = 0; if (T.st[d] === 1 && d % 7 < 2) wkndOff++; if (T.st[d] === 2) al++; }
    }
    return { work, night, wkndOff, al, sl, maxRun, tr, rest: restBad(p, T) };
  });

  const hrs = new Array(24).fill(0);
  starts.forEach(s => { for (let k = 0; k < L; k++) hrs[(s + k) % 24]++; });
  const uncoveredTemplate = hrs.map((v, h) => v ? -1 : h).filter(h => h >= 0);

  return { recommended, typical, S, P, TL, count, H, D, ND, L, MIN, W, starts, nominal, nomIdx, off, slide, patt, weeks, tl, restBad, addTL, cov, logs, payroll, fair, uncoveredTemplate, dateOf };
}

/* ---------- who can step in ---------- */
function canCover(R, i, d) {
  const T = R.TL[i], p = R.P[i];
  if (T.st[d] !== 1) return null;
  const s = d * 24 + R.nominal(p, d);
  let prevEnd = p.lastEnd;
  for (let x = d - 1; x >= 0; x--) if (T.st[x] === 0) { prevEnd = T.start[x] + R.L; break; }
  let nextStart = 1e9;
  for (let x = d + 1; x < R.ND; x++) if (T.st[x] === 0) { nextStart = T.start[x]; break; }
  if (s - prevEnd < R.S.restMin || nextStart - (s + R.L) < R.S.restMin) return null;
  return s;
}

function analyzeMC(R, keys) {
  const { P, TL, L, H, MIN, S } = R;
  const mc = [];
  for (const k of keys) {
    const [id, ds] = k.split('|'); const i = P.findIndex(p => p.id === id), d = +ds;
    if (i >= 0 && d >= 0 && d < R.D && TL[i].st[d] === 0) mc.push({ i, d });
  }
  if (!mc.length) return null;
  const isMC = (i, d) => mc.some(m => m.i === i && m.d === d);
  const c = Int16Array.from(R.count);
  for (const m of mc) { const s = TL[m.i].start[m.d]; for (let t = Math.max(0, s); t < Math.min(H, s + L); t++) c[t]--; }
  const short = (a, b) => { let x = 0; for (let t = a; t < b; t++) { if (c[t] < MIN) x += MIN - c[t]; if (c[t] <= 0) x += 2; } return x; };
  const addSkip = (i, T, sg) => { for (let d = 0; d < R.ND; d++) if (T.st[d] === 0 && !isMC(i, d)) { const s = T.start[d]; for (let t = Math.max(0, s), e = Math.min(H, s + L); t < e; t++) c[t] += sg; } };
  const impacts = mc.map(m => {
    const s = TL[m.i].start[m.d]; let shortH = 0, zero = 0, low = 99; const hours = [];
    for (let t = Math.max(0, s); t < Math.min(H, s + L); t++) { low = Math.min(low, c[t]); if (c[t] < MIN) { shortH++; hours.push(t); } if (c[t] <= 0) zero++; }
    return { ...m, s, shortH, zero, low, blocks: toBlocks(hours) };
  });
  const sugg = [];
  const evalSwap = (i, T2) => {
    const T = TL[i]; let lo = -1, hi = -1;
    for (let d = 0; d < R.ND; d++) if (T.st[d] !== T2.st[d] || T.start[d] !== T2.start[d]) { if (lo < 0) lo = d; hi = d; }
    if (lo < 0) return 0;
    const a = Math.max(0, lo * 24 - 24), b = Math.min(H, hi * 24 + 48 + L);
    const before = short(a, b); addSkip(i, T, -1); addSkip(i, T2, 1); const after = short(a, b); addSkip(i, T2, -1); addSkip(i, T, 1);
    return before - after;
  };
  const dset = new Set(); mc.forEach(m => { dset.add(m.d - 1); dset.add(m.d); dset.add(m.d + 1); });
  for (const d of dset) {
    if (d < 0 || d >= R.ND) continue;
    P.forEach((p, i) => {
      const T = TL[i];
      if (T.st[d] !== 0 || T.tr[d] || isMC(i, d)) return;
      let best = null;
      for (let o = -S.maxSlide; o <= S.maxSlide; o++) {
        if (o === R.slide[i][d]) continue;
        const sl = Int8Array.from(R.slide[i]); sl[d] = o;
        const T2 = R.tl(p, R.off[i], sl);
        if (R.restBad(p, T2) > R.restBad(p, T)) continue;
        const g = evalSwap(i, T2), nom = R.nominal(p, d), pen = startPenalty(nom, nom + o) > 0;
        const score = g - (pen ? 1.5 : 0);
        if (g > 0 && (!best || score > best.score || (score === best.score && Math.abs(o) < Math.abs(best.o)))) best = { gain: g, score, o, T2, pen };
      }
      if (best) sugg.push({ type: 'slide', i, d, gain: best.gain, from: T.start[d], to: best.T2.start[d], pen: best.pen });
    });
  }
  const mcDays = [...new Set(mc.map(m => m.d))];
  for (const d of mcDays) {
    P.forEach((p, i) => {
      if (canCover(R, i, d) == null) return;
      const wk = R.weeks.find(w => w.days.includes(d));
      let best = null;
      for (const w of wk.days) {
        if (w === d || w >= R.ND || TL[i].st[w] !== 0 || isMC(i, w)) continue;
        const of = Uint8Array.from(R.off[i]); of[d] = 0; of[w] = 1;
        const T2 = R.tl(p, of, R.slide[i]);
        if (R.restBad(p, T2) > 0) continue;
        const g = evalSwap(i, T2);
        if (g > 0 && (!best || g > best.gain)) best = { gain: g, w, T2 };
      }
      const of = Uint8Array.from(R.off[i]); of[d] = 0;
      const T3 = R.tl(p, of, R.slide[i]);
      const gOT = R.restBad(p, T3) > 0 ? 0 : evalSwap(i, T3);
      if (best) sugg.push({ type: 'swap', i, d, w: best.w, gain: best.gain, start: best.T2.start[d] });
      else if (gOT > 0) sugg.push({ type: 'ot', i, d, gain: gOT, start: T3.start[d] });
    });
  }
  sugg.sort((a, b) => (b.gain - (b.pen ? 1.5 : 0)) - (a.gain - (a.pen ? 1.5 : 0)) || (a.type === 'slide' ? -1 : 1));
  const totalShort = short(0, R.D * 24);
  return { mc, count: c, impacts, sugg: sugg.slice(0, 8), totalShort };
}

function toBlocks(hours) {
  const out = [];
  for (const t of hours) { const last = out[out.length - 1]; if (last && last[1] === t) last[1] = t + 1; else out.push([t, t + 1]); }
  return out;
}
const tier = (v, MIN) => v <= 0 ? 'gap' : v < MIN ? 'below' : v === MIN ? 'thin' : 'ok';

function riskRows(R, w, c) {
  const rows = [];
  for (let d = w * 7; d < w * 7 + 7; d++) {
    let h = 0;
    while (h < 24) {
      const t = d * 24 + h;
      if (c[t] <= R.MIN) {
        let e = h, mn = c[t];
        while (e + 1 < 24 && c[d * 24 + e + 1] <= R.MIN) { e++; mn = Math.min(mn, c[d * 24 + e]); }
        const a = d * 24 + h, b = d * 24 + e + 1;
        const duty = [], backups = [];
        R.P.forEach((p, i) => {
          const T = R.TL[i];
          for (const x of [d - 1, d]) if (x >= 0 && T.st[x] === 0 && !state.mc.has(p.id + '|' + x)) { const s = T.start[x]; if (s < b && s + R.L > a) { duty.push(p.name); break; } }
          const s = canCover(R, i, d);
          if (s != null) { const ov = Math.min(b, s + R.L) - Math.max(a, s); if (ov > 0) backups.push({ name: p.name, ov, s }); }
        });
        backups.sort((x, y) => y.ov - x.ov);
        rows.push({ d, h1: h, h2: e + 1, min: mn, sev: tier(mn, R.MIN), duty: [...new Set(duty)], backups: backups.slice(0, 3) });
        h = e + 1;
      } else h++;
    }
  }
  const rank = { gap: 0, below: 1, thin: 2 };
  rows.sort((x, y) => rank[x.sev] - rank[y.sev] || x.d - y.d || x.h1 - y.h1);
  return rows;
}

/* ---------- state ---------- */
let plan = null;
const state = { R: null, M: null, mc: new Set(), storage: 'loading', readOnly: false, confirmRm: null, leaveErr: '', dl: null };
const ui = { tab: 'roster', week: 0, mcMode: false };
try { Object.assign(ui, JSON.parse(localStorage.getItem(UI_KEY) || '{}')); ui.mcMode = false; } catch {}
const saveUI = () => { try { localStorage.setItem(UI_KEY, JSON.stringify({ tab: ui.tab, week: ui.week })); } catch {} };

function recompute() {
  state.R = plan && plan.staff.length ? computeSchedule(plan) : null;
  if (state.R) ui.week = Math.min(ui.week, state.R.W - 1);
  state.M = state.R && state.mc.size ? analyzeMC(state.R, [...state.mc]) : null;
}

/* ---------- persistence ---------- */
let db = null, docRef = null, saveTimer = null, saving = false, dirty = false;
function setStatus(kind) {
  const el = $('#saveState');
  const map = {
    saved: ['Saved · shared with anyone you give access', 'ok'], pending: ['Saving…', ''], local: ['Saved in this browser only', 'warn'],
    readonly: ['View only · changes are not saved', 'warn'], error: ['Could not save · check your connection', 'warn'], loading: ['Loading team…', ''],
  };
  const [t, c] = map[kind] || map.loading;
  el.textContent = t; el.className = 'savestate ' + c;
}
function lsGet() { try { return JSON.parse(localStorage.getItem(LS_KEY) || 'null'); } catch { return null; } }
function lsSet(v) { try { localStorage.setItem(LS_KEY, JSON.stringify(v)); return true; } catch { return false; } }
function scheduleSave() {
  if (state.readOnly) return;
  dirty = true; setStatus('pending');
  clearTimeout(saveTimer); saveTimer = setTimeout(flush, 700);
}
async function flush() {
  if (saving) { clearTimeout(saveTimer); saveTimer = setTimeout(flush, 400); return; }
  saving = true; dirty = false;
  try {
    if (state.storage === 'db') { await docRef.set({ plan: clone(plan), clientId: CLIENT, savedAt: new Date().toISOString() }); setStatus('saved'); }
    else { setStatus(lsSet(plan) ? 'local' : 'error'); }
  } catch (e) {
    if (e?.code === 'invalid_argument') { state.readOnly = true; setStatus('readonly'); }
    else if (e?.code === 'unavailable') { dirty = true; setTimeout(flush, 800 + Math.random() * 800); }
    else setStatus('error');
  } finally { saving = false; }
}
async function initStore() {
  if (window.claude?.use) { try { db = await window.claude.use('db'); } catch { db = null; } }
  if (db) {
    state.storage = 'db';
    docRef = db.doc(DOC_PATH);
    docRef.onSnapshot(snap => {
      if (!snap.exists) { if (!plan) renderEmpty(); setStatus('saved'); return; }
      const data = snap.data();
      if (plan && (data.clientId === CLIENT || dirty || saving)) return;
      plan = normalize(clone(data.plan || {}));
      setStatus('saved'); recompute(); renderAll();
    }, () => { setStatus('error'); });
  } else {
    state.storage = 'local';
    const raw = lsGet();
    if (raw) { plan = normalize(raw); recompute(); renderAll(); } else renderEmpty();
    setStatus('local');
  }
}

/* ---------- rendering ---------- */
function toast(msg) { const t = $('#toast'); t.textContent = msg; t.classList.add('on'); clearTimeout(toast.h); toast.h = setTimeout(() => t.classList.remove('on'), 2200); }

function renderEmpty() {
  $('#summary').innerHTML = ''; $('#tabs').innerHTML = '';
  $('#panel').innerHTML = `<div class="card empty">
    <h2>Set up your SME team</h2>
    <p class="hint">Start with your headcount. You can rename SMEs, add more, and enter last week's shifts and annual leave next.</p>
    <div class="form">
      <div class="field"><label for="e-n">Number of SMEs</label><input id="e-n" type="number" min="1" max="60" value="10"></div>
      <div class="field"><label for="e-start">First Saturday of the plan</label><input id="e-start" type="date" value="${nextSat()}"></div>
    </div>
    <div class="row"><button class="btn primary" data-act="create">Create roster</button></div>
  </div>`;
}

function renderAll() {
  renderSummary();
  $('#tabs').innerHTML = TABS.map(([k, l]) => `<button role="tab" data-tab="${k}" aria-selected="${ui.tab === k}">${l}</button>`).join('');
  renderPanel();
}

function renderSummary() {
  const R = state.R;
  if (!R) { $('#summary').innerHTML = ''; return; }
  const c = R.count, Dh = R.D * 24;
  let zero = 0, below = 0, thin = 0;
  for (let t = 0; t < Dh; t++) { const v = c[t]; if (v <= 0) zero++; if (v < R.MIN) below++; else if (v === R.MIN) thin++; }
  const flat = R.payroll.flat().filter(x => x.checked), pass = flat.filter(x => x.ok).length;
  const rest = R.fair.reduce((n, f) => n + f.rest, 0);
  const adj = R.logs.filter(l => l.kind !== 'transition').length;
  const stats = [
    [zero, 'hours with no SME on duty', zero ? 'gap' : 'ok'],
    [below, `hours below ${R.MIN} on duty`, below ? 'below' : 'ok'],
    [thin, 'thin hours · one MC makes them short', thin ? 'thin' : 'ok'],
    [`${pass}/${flat.length}`, 'payroll weeks with exactly 2 off', pass === flat.length ? 'ok' : 'gap'],
    [rest, `shift changes under ${R.S.restMin} h rest`, rest ? 'gap' : 'ok'],
    [adj, 'automatic adjustments', ''],
  ];
  $('#summary').innerHTML = stats.map(([v, l, t]) => `<div class="stat ${t}"><b>${esc(v)}</b><span>${esc(l)}</span></div>`).join('');
}

function renderPanel() {
  const active = document.activeElement?.id;
  const el = $('#panel');
  if (!plan) { renderEmpty(); return; }
  const f = { roster: panelRoster, risk: panelRisk, team: panelTeam, rules: panelRules, checks: panelChecks }[ui.tab] || panelRoster;
  el.innerHTML = f();
  if (active) document.getElementById(active)?.focus();
}

function weekPicker() {
  const R = state.R; if (!R) return '';
  return `<div class="weeks" role="group" aria-label="Schedule week">${Array.from({ length: R.W }, (_, w) => {
    const a = R.dateOf(w * 7), b = R.dateOf(w * 7 + 6);
    return `<button data-week="${w}" aria-pressed="${ui.week === w}">Week ${w + 1} · ${fmtS(a)}–${fmtS(b)}</button>`;
  }).join('')}</div>`;
}
function noTeam() { return `<div class="card empty"><h2>No SMEs yet</h2><p class="hint">Add SMEs in Team & leave to build a roster.</p><div class="row"><button class="btn primary" data-act="gotoTeam">Open Team & leave</button></div></div>`; }

function shiftLegend(R) {
  return R.starts.map((s, k) => `<span><i class="s${k}"></i>${span(s, R.L)}</span>`).join('') +
    `<span><i style="background:var(--off)"></i>Off</span><span><i style="background:var(--leave)"></i>Annual leave</span>` +
    `<span><span class="dot"></span> off-day moved for a leave week</span><span><em class="tag">+2h</em> start time slid</span><span><em class="tag tr">prev</em> transition (still on last shift)</span>`;
}

function panelRoster() {
  const R = state.R; if (!R) return noTeam();
  const w = ui.week, L = R.L, c = state.M ? state.M.count : R.count;
  const days = Array.from({ length: 7 }, (_, k) => w * 7 + k);
  const head = `<tr><th class="who">SME</th>${w === 0 ? '<th>Last week</th>' : ''}${days.map(d => `<th class="day${d % 7 < 2 ? ' wkend' : ''}"><span>${DOW[d % 7]}</span><b>${fmtS(R.dateOf(d))}</b></th>`).join('')}</tr>`;
  const body = R.P.map((p, i) => {
    const T = R.TL[i];
    const baseNow = R.nominal(p, w * 7);
    const prev = w === 0 ? `<td class="prevcol">${p.prevStart != null ? spanShort(p.prevStart, L) : '—'}<br>${p.prevOff.length ? 'off ' + p.prevOff.map(x => DOW[x]).join(', ') : 'offs not set'}</td>` : '';
    const cells = days.map(d => {
      const st = T.st[d], key = p.id + '|' + d;
      if (st === 2) return `<td class="c"><div class="cell al">AL</div></td>`;
      if (st === 1) return `<td class="c"><div class="cell off">OFF${R.patt[i][d] ? '' : ' <span class="dot" title="Moved from usual off-days to cover leave"></span>'}</div></td>`;
      const s = T.start[d] - d * 24;
      const idx = T.tr[d] ? R.starts.indexOf(m24(s)) : R.nomIdx(p, d);
      const sl = !T.tr[d] && R.slide[i][d];
      const mc = state.mc.has(key);
      const inner = `<b>${spanShort(s, L)}</b>${sl ? `<em class="tag">${sl > 0 ? '+' : ''}${sl}h</em>` : ''}${T.tr[d] ? '<em class="tag tr">prev</em>' : ''}${mc ? '<em class="tag mc">MC/EL</em>' : ''}`;
      const cls = `cell ${idx >= 0 ? 's' + idx : 'sx'}${T.tr[d] ? ' tr' : ''}${mc ? ' mc' : ''}`;
      if (ui.mcMode) return `<td class="c"><button class="${cls}" data-mc="${esc(key)}" aria-pressed="${mc}" aria-label="${esc(p.name)} ${fmtD(R.dateOf(d))}: ${mc ? 'remove absence' : 'mark MC or EL'}">${inner}</button></td>`;
      return `<td class="c"><div class="${cls}">${inner}</div></td>`;
    }).join('');
    return `<tr><td class="who"><b>${esc(p.name)}</b><small>${span(baseNow, L)}</small></td>${prev}${cells}</tr>`;
  }).join('');
  const foot = (label, fn) => `<tr><td class="who">${label}</td>${w === 0 ? '<td></td>' : ''}${days.map(fn).join('')}</tr>`;
  const lowRow = foot('Lowest on duty', d => { let mn = 99; for (let h = 0; h < 24; h++) mn = Math.min(mn, c[d * 24 + h]); return `<td class="t-${tier(mn, R.MIN)}">${mn}</td>`; });
  const shortRow = foot('Short hours', d => { let n = 0; for (let h = 0; h < 24; h++) if (c[d * 24 + h] < R.MIN) n++; return `<td class="${n ? 't-below' : 't-ok'}">${n}</td>`; });

  return `<div class="card">
    <div class="card-h"><h2>Week ${w + 1} roster</h2>
      <div class="row">
        <label class="toggle"><input type="checkbox" id="mcMode" ${ui.mcMode ? 'checked' : ''}> Simulate MC / EL</label>
        <button class="btn" data-act="csv">Export CSV</button>
        <button class="btn" data-act="copy">Copy table</button>
      </div>
    </div>
    ${weekPicker()}
    ${ui.mcMode ? `<p class="note info">Click any working shift to mark it as an MC or emergency leave. The roster itself does not change; the impact and the best cover options appear below the grid.</p>` : ''}
    <div class="scroll"><table class="grid"><thead>${head}</thead><tbody>${body}</tbody><tfoot>${lowRow}${shortRow}</tfoot></table></div>
    <div class="legend">${shiftLegend(R)}</div>
  </div>
  ${mcPanel()}`;
}

function mcPanel() {
  const R = state.R, M = state.M;
  if (!M) return ui.mcMode ? `<div class="card"><h3>What-if: no absences marked yet</h3><p class="hint">Mark one or more shifts above to see which hours go short and who can cover.</p></div>` : '';
  const imp = M.impacts.map(m => {
    const p = R.P[m.i];
    const where = m.blocks.length ? m.blocks.map(([a, b]) => `${fmtD(R.dateOf(Math.floor(a / 24)))} ${hh(a)}–${hh(b)}`).join(', ') : 'no hours go short';
    const sev = m.zero ? 'gap' : m.shortH ? 'below' : 'ok';
    return `<li><span class="pill t-${sev}">${m.zero ? 'No cover' : m.shortH ? 'Short' : 'Absorbed'}</span><div><b>${esc(p.name)}</b> off sick ${fmtD(R.dateOf(m.d))} (${span(m.s - m.d * 24, R.L)})<small>${m.shortH ? `${m.shortH} h drop below ${R.MIN} on duty, lowest ${Math.max(0, m.low)}: ${where}` : 'The rest of the team still meets the target.'}</small></div></li>`;
  }).join('');
  const sg = M.sugg.length ? M.sugg.map(s => {
    const p = R.P[s.i], dd = fmtD(R.dateOf(s.d));
    let txt;
    if (s.type === 'slide') { const o = s.to - s.from; txt = `<b>${esc(p.name)}</b> starts ${hh(s.to)} instead of ${hh(s.from)} on ${dd} (${o > 0 ? '+' : ''}${o} h, within the ±${R.S.maxSlide} h rule)${s.pen ? ' · <span style="color:var(--below)">misses the night allowance</span>' : ''}`; }
    else if (s.type === 'swap') txt = `<b>${esc(p.name)}</b> works ${dd} (${span(s.start - s.d * 24, R.L)}) and takes ${fmtD(R.dateOf(s.w))} off instead · payroll stays at 2 off`;
    else txt = `<b>${esc(p.name)}</b> works an extra ${span(s.start - s.d * 24, R.L)} on ${dd} as overtime · they would then have only 1 off-day that payroll week`;
    return `<li><span>${txt}</span><span class="pill t-ok">recovers ${s.gain} staff-h</span></li>`;
  }).join('') : '<li><span class="hint">No single move from the current roster recovers coverage. Consider overtime extensions on the neighbouring shifts.</span></li>';
  return `<div class="two">
    <div class="card"><div class="card-h"><h3>Impact of marked absences</h3><button class="btn small" data-act="clearMC">Clear all</button></div><ul class="log">${imp}</ul></div>
    <div class="card"><h3>Best cover options</h3><p class="hint">Ranked by how many short staff-hours each single move recovers. Every option keeps ${R.S.restMin} h rest between shifts.</p><ul class="log sugg">${sg}</ul></div>
  </div>`;
}

function panelRisk() {
  const R = state.R; if (!R) return noTeam();
  const w = ui.week, c = state.M ? state.M.count : R.count;
  const days = Array.from({ length: 7 }, (_, k) => w * 7 + k);
  const namesAt = (t) => R.P.filter((p, i) => { const T = R.TL[i]; const d = Math.floor(t / 24); return [d - 1, d].some(x => x >= 0 && T.st[x] === 0 && !state.mc.has(p.id + '|' + x) && T.start[x] <= t && t < T.start[x] + R.L); }).map(p => p.name);
  const rows = Array.from({ length: 24 }, (_, h) => `<tr><td class="h">${hh(h)}</td>${days.map(d => { const t = d * 24 + h, v = c[t]; return `<td class="v t-${tier(v, R.MIN)}" title="${esc(namesAt(t).join(', ') || 'Nobody')}">${v}</td>`; }).join('')}</tr>`).join('');
  const risks = riskRows(R, w, c);
  const sevLbl = { gap: 'No cover', below: 'Short', thin: 'Thin' };
  const rr = risks.length ? risks.map(r => `<tr>
      <td><span class="pill t-${r.sev}">${sevLbl[r.sev]}</span></td>
      <td>${fmtD(R.dateOf(r.d))}</td><td class="tnum">${hh(r.h1)}–${hh(r.h2)}</td>
      <td class="tnum">${Math.max(0, r.min)}${r.sev === 'thin' ? ` → ${r.min - 1} if one MC` : ''}</td>
      <td style="white-space:normal">${esc(r.duty.join(', ') || 'Nobody')}</td>
      <td style="white-space:normal">${r.backups.length ? r.backups.map(b => `${esc(b.name)} <span class="hint">(${span(b.s - r.d * 24, R.L)}, swap an off-day)</span>`).join('<br>') : '<span class="hint">No rested SME off that day</span>'}</td>
    </tr>`).join('') : `<tr><td colspan="6" class="hint">Every hour this week has more than ${R.MIN} SMEs on duty, so one MC never makes it short.</td></tr>`;
  const counts = { gap: 0, below: 0, thin: 0 }; risks.forEach(r => counts[r.sev]++);
  return `<div class="card">
    <div class="card-h"><h2>Hourly coverage · week ${w + 1}</h2>${state.M ? `<span class="pill t-gap">Showing what-if with ${state.M.mc.length} absence${state.M.mc.length > 1 ? 's' : ''}</span>` : ''}</div>
    ${weekPicker()}
    <p class="hint">Each cell is the number of SMEs on duty in that hour, including night shifts that started the day before. Hover a cell to see who is on.</p>
    <div class="legend"><span><i class="t-gap"></i>0 · no cover</span><span><i class="t-below"></i>below ${R.MIN}</span><span><i class="t-thin"></i>exactly ${R.MIN} · one MC makes it short</span><span><i class="t-ok"></i>buffer for an MC</span></div>
    <div class="scroll"><table class="heat"><thead><tr><th></th>${days.map(d => `<th>${DOW[d % 7]}<br><span class="mono">${fmtS(R.dateOf(d))}</span></th>`).join('')}</tr></thead><tbody>${rows}</tbody></table></div>
  </div>
  <div class="card">
    <div class="card-h"><h2>MC / EL risk register</h2><div class="row"><span class="pill t-gap">${counts.gap} no cover</span><span class="pill t-below">${counts.below} short</span><span class="pill t-thin">${counts.thin} thin</span></div></div>
    <p class="hint">Windows where one unexpected absence leaves the team below target. First-call backups are SMEs who are off that day, rested at least ${R.S.restMin} h either side, and whose own shift covers the window.</p>
    <div class="scroll"><table><thead><tr><th>Risk</th><th>Day</th><th>Window</th><th>On duty</th><th>Who is on</th><th>First-call backup</th></tr></thead><tbody>${rr}</tbody></table></div>
  </div>`;
}

function shiftOptions(R, sel) { return R.starts.map((s, k) => `<option value="${k}" ${k === sel ? 'selected' : ''}>${span(s, R.L)}</option>`).join(''); }
function panelTeam() {
  const S = plan.settings, L = S.shiftLen;
  const Rlike = { starts: S.starts, L };
  const typNote = () => {
    const t = state.R?.typical; if (!t) return '';
    const more = t.weekend > t.weekday + 0.05;
    return `<p class="note ${more || !S.weekendExtra ? 'info' : 'warn'}">With these off-days, a typical week has on average <b class="tnum">${t.weekday.toFixed(1)}</b> SMEs on duty per hour on weekdays and <b class="tnum">${t.weekend.toFixed(1)}</b> on Saturday and Sunday.${!more && S.weekendExtra ? ' Fixed off-day picks are keeping weekends from getting more SMEs; switch some back to Recommended to rebalance.' : ''}</p>`;
  };
  const autoLabel = (s) => {
    const rec = state.R?.recommended?.[s.id];
    return rec == null ? 'Recommended' : `Recommended · ${PAIRS[rec]}`;
  };
  const rows = plan.staff.map((s, i) => {
    const conf = state.confirmRm === s.id;
    const lvDays = s.leaves.reduce((n, l) => n + dayDiff(l.from, l.to) + 1, 0);
    const pOff = (k) => `<select id="po${k}-${s.id}" data-f="prevOff${k}" data-id="${s.id}" aria-label="Last week off-day ${k + 1} for ${esc(s.name)}"><option value="">—</option>${DOW.map((d, j) => `<option value="${j}" ${s.prevOff[k] === j ? 'selected' : ''}>${d}</option>`).join('')}</select>`;
    return `<tr>
      <td><div class="namecell">
        <input type="text" id="n-${s.id}" data-f="name" data-id="${s.id}" value="${esc(s.name)}" aria-label="Name">
        ${conf ? `<button class="btn small danger" data-act="rmYes" data-id="${s.id}">Confirm remove</button><button class="btn small" data-act="rmNo">Keep</button>` : `<button class="btn small rm" data-act="rm" data-id="${s.id}" aria-label="Remove ${esc(s.name)}" title="Remove ${esc(s.name)}">Remove</button>`}
      </div></td>
      <td><select id="b-${s.id}" data-f="base" data-id="${s.id}" aria-label="Base shift for ${esc(s.name)}">${shiftOptions(Rlike, s.base)}</select></td>
      <td><select id="o-${s.id}" data-f="offPref" data-id="${s.id}" aria-label="Off-days for ${esc(s.name)}"><option value="-1">${autoLabel(s)}</option>${PAIRS.map((p, j) => `<option value="${j}" ${s.offPref === j ? 'selected' : ''}>Fixed ${p}</option>`).join('')}</select></td>
      <td><select id="ps-${s.id}" data-f="prevStart" data-id="${s.id}" aria-label="Last week's shift for ${esc(s.name)}"><option value="">Same as base</option>${Array.from({ length: 24 }, (_, h) => `<option value="${h}" ${s.prevStart === h ? 'selected' : ''}>${span(h, L)}</option>`).join('')}</select></td>
      <td>${pOff(0)} ${pOff(1)}</td>
      <td class="tnum">${lvDays ? `${lvDays} day${lvDays > 1 ? 's' : ''}` : '<span class="hint">none</span>'}</td>
    </tr>`;
  }).join('');
  const all = plan.staff.flatMap(s => s.leaves.map(l => ({ s, l }))).sort((a, b) => a.l.from.localeCompare(b.l.from));
  const end = addDays(S.start, S.weeks * 7 - 1);
  const lvRows = all.length ? all.map(({ s, l }) => {
    const n = dayDiff(l.from, l.to) + 1, inWin = l.to >= S.start && l.from <= end;
    return `<tr><td>${esc(s.name)}</td><td>${fmtD(l.from)}${l.to !== l.from ? ' – ' + fmtD(l.to) : ''}</td><td class="tnum">${n}</td><td>${esc(l.note) || '<span class="hint">—</span>'}</td><td>${inWin ? '<span class="pill t-ok">In this plan</span>' : '<span class="pill" style="background:var(--surface-2)">Later or earlier</span>'}</td><td><button class="btn small" data-act="rmLeave" data-id="${s.id}" data-lid="${l.id}">Remove</button></td></tr>`;
  }).join('') : `<tr><td colspan="6" class="hint">No annual leave planned yet.</td></tr>`;
  return `<div class="card">
    <div class="card-h"><h2>Team · ${plan.staff.length} SME${plan.staff.length === 1 ? '' : 's'}</h2>
      <div class="row"><button class="btn primary" data-act="add">Add SME</button><button class="btn" data-act="balance">Balance base shifts</button><button class="btn" data-act="recAll">Reset all off-days to recommended</button></div></div>
    <p class="hint">Base shift is where each SME starts the plan; rotation moves whole groups together. Off-days are fixed every week. Recommended pairs are worked out together for the best coverage; when you fix a pair for one SME, the recommendations for the rest adjust around it. "Last week" drives the transition week: the planner tops up Saturday and Sunday so last week's Mon–Sun payroll still ends with exactly 2 off-days, and keeps people on their old shift until ${S.restMin} h rest allows the change.</p>
    ${typNote()}
    <div class="scroll"><table class="team"><thead><tr><th>Name</th><th>Base shift</th><th>Off-days</th><th>Last week's shift</th><th>Last week's off-days (Sat–Fri)</th><th>Leave</th></tr></thead><tbody>${rows}</tbody></table></div>
  </div>
  <div class="card">
    <h2>Annual leave</h2>
    <p class="hint">Add leave as far ahead as you like. Leave days never count as off-days. The planner rearranges that SME's off-days around the leave, moves teammates' off-days within the same payroll week, then slides start times by up to ±${S.maxSlide} h to keep every hour covered.</p>
    <div class="form">
      <div class="field"><label for="lv-who">SME</label><select id="lv-who">${plan.staff.map(s => `<option value="${s.id}">${esc(s.name)}</option>`).join('')}</select></div>
      <div class="field"><label for="lv-from">From</label><input id="lv-from" type="date" value="${S.start}"></div>
      <div class="field"><label for="lv-to">To</label><input id="lv-to" type="date" value="${S.start}"></div>
      <div class="field"><label for="lv-note">Note (optional)</label><input id="lv-note" type="text" maxlength="80" placeholder="e.g. family trip"></div>
    </div>
    <div class="row"><button class="btn primary" data-act="addLeave">Add leave</button><span class="err" id="lv-err">${esc(state.leaveErr)}</span></div>
    <div class="scroll"><table><thead><tr><th>SME</th><th>Dates</th><th>Days</th><th>Note</th><th>Status</th><th></th></tr></thead><tbody>${lvRows}</tbody></table></div>
  </div>`;
}

function panelRules() {
  const S = plan.settings, n = plan.staff.length, nS = S.starts.length;
  const opt = (vals, sel) => vals.map(([v, l]) => `<option value="${v}" ${String(v) === String(sel) ? 'selected' : ''}>${l}</option>`).join('');
  const hrs = new Array(24).fill(0); S.starts.forEach(s => { for (let k = 0; k < S.shiftLen; k++) hrs[(s + k) % 24]++; });
  const unc = hrs.map((v, h) => v ? -1 : h).filter(h => h >= 0);
  const perDay = n * 5 / 7, perShift = perDay / nS;
  const at15 = S.starts.includes(15);
  const allowNote = at15 ? `<p class="note warn">A 15:00 start misses the night shift allowance by one hour. 16:00 is recommended (allowance applies to starts from 16:00 to 04:00).</p>`
    : `<p class="note info">Night shift allowance applies to starts from 16:00 to 04:00. Shifts here that qualify: ${S.starts.filter(allowance).map(h => hh(h)).join(', ') || 'none'}. The planner avoids sliding a start to 15:00 or out of the allowance window.</p>`;
  const tmplNote = unc.length ? `<p class="note bad">These shift times leave ${toBlocks(unc).map(([a, b]) => `${hh(a)}–${hh(b)}`).join(', ')} with nobody scheduled. Change a start time or pick a preset.</p>`
    : `<p class="note good">These shifts cover all 24 hours${hrs.some(v => v > 1) ? `, with handover overlap at ${toBlocks(hrs.map((v, h) => v > 1 ? h : -1).filter(h => h >= 0)).map(([a, b]) => `${hh(a)}–${hh(b)}`).join(', ')}` : ''}.</p>`;
  const capNote = perShift < S.minStaff ? `<p class="note bad">With ${n} SMEs and 2 off-days each, about ${perDay.toFixed(1)} are on duty per day (${perShift.toFixed(1)} per shift). That is below your target of ${S.minStaff} per hour, so some hours will be short. Add SMEs, lower the target, or use fewer shifts.</p>`
    : perShift < S.minStaff + 1 ? `<p class="note warn">With ${n} SMEs, about ${perDay.toFixed(1)} are on duty per day (${perShift.toFixed(1)} per shift). The target of ${S.minStaff} is reachable, but most hours have no spare person for an MC.</p>`
    : `<p class="note good">With ${n} SMEs, about ${perDay.toFixed(1)} are on duty per day (${perShift.toFixed(1)} per shift), leaving room for one MC in most hours.</p>`;
  return `<div class="card">
    <h2>Plan window</h2>
    <div class="form">
      <div class="field"><label for="r-start">First Saturday</label><input type="date" id="r-start" value="${S.start}"><small>Other dates snap back to the Saturday of that week.</small></div>
      <div class="field"><label for="r-weeks">Weeks to plan</label><select id="r-weeks">${opt(Array.from({ length: 8 }, (_, k) => [k + 1, `${k + 1} week${k ? 's' : ''}`]), S.weeks)}</select></div>
      <div class="field"><label for="r-min">Target SMEs on duty every hour</label><select id="r-min">${opt([1, 2, 3, 4, 5].map(v => [v, v]), S.minStaff)}</select></div>
      <div class="field"><label for="r-wx">Weekend staffing</label><select id="r-wx">${opt([[0, 'Same as weekdays'], [1, 'More SMEs on Sat & Sun']], S.weekendExtra)}</select><small>Recommended off-days move to weekdays as far as possible without any weekday hour dropping below the target.</small></div>
    </div>
  </div>
  <div class="card">
    <h2>Shift times</h2>
    <div class="presets">${PRESETS.map((p, k) => `<button class="btn small" data-act="preset" data-k="${k}">${p.name} · ${p.starts.map(s => pad(s)).join('/')}</button>`).join('')}</div>
    <div class="form">
      <div class="field"><label for="r-n">Number of shifts</label><select id="r-n">${opt([[2, '2 shifts'], [3, '3 shifts'], [4, '4 shifts']], nS)}</select></div>
      <div class="field"><label for="r-len">Shift length</label><select id="r-len">${opt([8, 9, 10, 12].map(v => [v, `${v} hours`]), S.shiftLen)}</select></div>
      <div class="field"><span class="lbl">Start times</span><div class="shiftset">${S.starts.map((s, k) => `<select id="r-s${k}" data-k="${k}" aria-label="Start time of shift ${k + 1}">${Array.from({ length: 24 }, (_, h) => `<option value="${h}" ${h === s ? 'selected' : ''}>${hh(h)}</option>`).join('')}</select>`).join('')}</div></div>
    </div>
    ${tmplNote}${allowNote}${capNote}
  </div>
  <div class="card">
    <h2>Rotation, rest and adjustments</h2>
    <div class="form">
      <div class="field"><label for="r-rot">Rotate shifts</label><select id="r-rot">${opt([[0, 'Never'], [1, 'Every week'], [2, 'Every 2 weeks'], [4, 'Every 4 weeks']], S.rotateEvery)}</select><small>Groups move forward together (morning → afternoon → night).</small></div>
      <div class="field"><label for="r-slide">Allowed start-time slide</label><select id="r-slide">${opt([[0, 'No slides'], [1, '±1 hour'], [2, '±2 hours'], [3, '±3 hours'], [4, '±4 hours']], S.maxSlide)}</select><small>Always measured from the SME's own shift. Smaller slides are always tried first.</small></div>
      <div class="field"><label for="r-rest">Minimum rest between shifts</label><select id="r-rest">${opt([8, 10, 11, 12, 14, 16].map(v => [v, `${v} hours`]), S.restMin)}</select></div>
      <div class="field"><label for="r-run">Longest working streak</label><select id="r-run">${opt([5, 6, 7, 8, 9, 10].map(v => [v, `${v} days`]), S.maxRun)}</select></div>
    </div>
  </div>
  <div class="card">
    <h2>How the planner decides</h2>
    <ol class="hint" style="margin:0;padding-left:20px;display:flex;flex-direction:column;gap:6px">
      <li>Each SME gets a fixed pair of off-days that stays the same every week. The recommended pairs are chosen together to give the most coverage across every hour of the week. When you fix a pair for an SME, everyone still on Recommended is re-optimised around it. Recommendations push off-days towards weekdays so Saturday and Sunday have more SMEs on duty (set under Weekend staffing). Sun & Mon is available as a pair and still gives exactly 2 off-days in every Mon–Sun payroll week.</li>
      <li>Every Mon–Sun payroll week gets exactly 2 off-days per SME. Leave days never count as off.</li>
      <li>Week 1 tops up Saturday and Sunday so last week's payroll also ends with 2 off. Shift changes wait until ${S.restMin} h rest is possible.</li>
      <li>Only in a week where someone is on annual leave, and only if an hour would be short, a teammate's off-day may move to another day in the same payroll week. Every other week keeps everyone's fixed off-days.</li>
      <li>Any hours still short get closed by sliding start times up to ±${S.maxSlide} h from each SME's own shift, as long as rest stays at ${S.restMin} h or more. Slides avoid a 15:00 start and never take a night shift out of the 16:00–04:00 allowance window unless that is the only way to close a gap.</li>
      <li>The MC/EL tools then show which hours have no spare SME, and who could step in.</li>
    </ol>
  </div>`;
}

function panelChecks() {
  const R = state.R; if (!R) return noTeam();
  const wkLbl = (wk) => wk.n === 0 ? `Mon ${fmtS(addDays(R.S.start, -5))} – Sun ${fmtS(R.dateOf(1))}` : `${fmtS(R.dateOf(wk.days[0]))} – ${fmtS(R.dateOf(wk.days[6]))}`;
  const pHead = `<tr><th class="who">SME</th>${R.weeks.map(wk => `<th>${wk.n === 0 ? 'Transition · ' : ''}${wkLbl(wk)}${wk.days.some(d => d >= R.D) ? ' *' : ''}</th>`).join('')}</tr>`;
  const pBody = R.P.map((p, i) => `<tr><td class="who"><b>${esc(p.name)}</b></td>${R.payroll[i].map(x => !x.checked ? '<td class="hint">no last-week data</td>' : `<td class="${x.ok ? 't-ok' : 't-gap'} tnum">${x.offs} off ${x.ok ? '✓' : `· needs ${x.req}`}${x.leave ? ` <span class="hint">+${x.leave} AL</span>` : ''}</td>`).join('')}</tr>`).join('');
  const fHead = `<tr><th class="who">SME</th><th>Shifts worked</th><th>Night-allowance shifts</th><th>Weekend days off</th><th>AL days</th><th>Slid starts</th><th>Transition days</th><th>Longest streak</th><th>Rest issues</th></tr>`;
  const fBody = R.P.map((p, i) => { const f = R.fair[i]; return `<tr><td class="who"><b>${esc(p.name)}</b></td><td class="tnum">${f.work}</td><td class="tnum">${f.night}</td><td class="tnum">${f.wkndOff}</td><td class="tnum">${f.al}</td><td class="tnum">${f.sl}</td><td class="tnum">${f.tr}</td><td class="tnum ${f.maxRun > R.S.maxRun ? 't-below' : ''}">${f.maxRun} days</td><td class="tnum ${f.rest ? 't-gap' : ''}">${f.rest}</td></tr>`; }).join('');
  const kinds = { off: ['Off-day moved', 't-thin'], slide: ['Start slid', 't-ok'], transition: ['Transition', 't-below'] };
  const logs = R.logs.length ? R.logs.map(l => `<li><span class="pill ${kinds[l.kind][1]}">${kinds[l.kind][0]}</span><div>${esc(l.text)}<small>${esc(l.reason)}</small></div></li>`).join('') : '<li class="hint">No adjustments were needed. Everyone keeps their fixed off-days.</li>';
  return `<div class="card">
    <h2>Mon–Sun payroll check</h2>
    <p class="hint">Each payroll week must have exactly 2 off-days per SME (fewer only when annual leave fills the week). The transition column adds last week's Mon–Fri off-days to this Saturday and Sunday. * The last week ends after the plan, so its weekend is projected.</p>
    <div class="scroll"><table class="grid"><thead>${pHead}</thead><tbody>${pBody}</tbody></table></div>
  </div>
  <div class="card">
    <h2>Fairness across the plan</h2>
    <div class="scroll"><table class="grid"><thead>${fHead}</thead><tbody>${fBody}</tbody></table></div>
  </div>
  <div class="card">
    <h2>What the planner changed and why</h2>
    <ul class="log">${logs}</ul>
  </div>`;
}

/* ---------- export ---------- */
function rosterTable() {
  const R = state.R, rows = [];
  rows.push(['SME', ...Array.from({ length: R.D }, (_, d) => fmtD(R.dateOf(d)))]);
  R.P.forEach((p, i) => {
    const T = R.TL[i];
    rows.push([p.name, ...Array.from({ length: R.D }, (_, d) => T.st[d] === 2 ? 'AL' : T.st[d] === 1 ? 'OFF' : span(T.start[d] - d * 24, R.L) + (T.tr[d] ? ' (prev shift)' : R.slide[i][d] ? ` (${R.slide[i][d] > 0 ? '+' : ''}${R.slide[i][d]}h)` : ''))]);
  });
  rows.push([]);
  rows.push(['Lowest on duty', ...Array.from({ length: R.D }, (_, d) => { let m = 99; for (let h = 0; h < 24; h++) m = Math.min(m, R.count[d * 24 + h]); return m; })]);
  rows.push(['Short hours', ...Array.from({ length: R.D }, (_, d) => { let n = 0; for (let h = 0; h < 24; h++) if (R.count[d * 24 + h] < R.MIN) n++; return n; })]);
  return rows;
}
async function exportCSV() {
  if (!state.R) return;
  const csv = '﻿' + rosterTable().map(r => r.map(x => `"${String(x).replace(/"/g, '""')}"`).join(',')).join('\r\n');
  if (state.dl === null && window.claude?.use) { try { state.dl = await window.claude.use('downloads'); } catch { state.dl = false; } }
  if (state.dl) {
    try { await state.dl.save({ filename: `sme-roster-${plan.settings.start}.csv`, data: csv }); toast('CSV saved'); return; }
    catch (e) { if (e?.code === 'declined') return; if (e?.code === 'rate_limited') { toast('A save prompt is already open'); return; } }
  }
  copyTable();
}
async function copyTable() {
  if (!state.R) return;
  const tsv = rosterTable().map(r => r.join('\t')).join('\n');
  try { await navigator.clipboard.writeText(tsv); toast('Copied · paste into Excel or Sheets'); }
  catch { toast('Copy is blocked here. Use Export CSV instead.'); }
}

/* ---------- events ---------- */
function changed(full = true) {
  recompute(); renderSummary();
  if (full) renderPanel();
  scheduleSave();
}
let typeTimer = null;
const findStaff = (id) => plan.staff.find(s => s.id === id);

document.addEventListener('click', (e) => {
  const tab = e.target.closest('[data-tab]');
  if (tab) { ui.tab = tab.dataset.tab; saveUI(); renderAll(); return; }
  const wk = e.target.closest('[data-week]');
  if (wk) { ui.week = +wk.dataset.week; saveUI(); renderPanel(); return; }
  const mcb = e.target.closest('[data-mc]');
  if (mcb) {
    const k = mcb.dataset.mc; state.mc.has(k) ? state.mc.delete(k) : state.mc.add(k);
    state.M = state.mc.size ? analyzeMC(state.R, [...state.mc]) : null;
    renderPanel(); return;
  }
  const a = e.target.closest('[data-act]');
  if (!a) return;
  const act = a.dataset.act;
  if (act === 'create') {
    const n = clampInt($('#e-n').value, 1, 60, 10);
    const st = $('#e-start').value;
    const s = defaultSettings(); if (isISO(st)) s.start = snapSat(st);
    plan = normalize({ settings: s, staff: makeTeam(n, s.starts.length) });
    ui.tab = 'roster'; recompute(); renderAll(); scheduleSave(); return;
  }
  if (act === 'gotoTeam') { ui.tab = 'team'; renderAll(); return; }
  if (act === 'csv') { exportCSV(); return; }
  if (act === 'copy') { copyTable(); return; }
  if (act === 'clearMC') { state.mc.clear(); state.M = null; renderPanel(); return; }
  if (act === 'add') {
    const nS = plan.settings.starts.length, cnt = new Array(nS).fill(0); plan.staff.forEach(s => cnt[s.base]++);
    const base = cnt.indexOf(Math.min(...cnt));
    plan.staff.push({ id: uid(), name: `SME ${plan.staff.length + 1}`, base, offPref: -1, prevStart: null, prevOff: [], leaves: [] });
    changed(); toast('SME added'); return;
  }
  if (act === 'balance') {
    const nS = plan.settings.starts.length, cnt = new Array(nS).fill(0);
    plan.staff.forEach(s => {
      const prefer = s.prevStart != null ? plan.settings.starts.map((x, k) => [k, Math.min(Math.abs(x - s.prevStart), 24 - Math.abs(x - s.prevStart))]).sort((p, q) => p[1] - q[1]).map(x => x[0]) : [...Array(nS).keys()];
      const mn = Math.min(...cnt); const k = prefer.find(k => cnt[k] === mn); s.base = k; cnt[k]++;
    });
    changed(); toast('Base shifts balanced'); return;
  }
  if (act === 'recAll') { plan.staff.forEach(s => { s.offPref = -1; }); changed(); toast('All off-days set to recommended'); return; }
  if (act === 'rm') { state.confirmRm = a.dataset.id; renderPanel(); return; }
  if (act === 'rmNo') { state.confirmRm = null; renderPanel(); return; }
  if (act === 'rmYes') { plan.staff = plan.staff.filter(s => s.id !== a.dataset.id); state.confirmRm = null; state.mc.clear(); changed(); toast('SME removed'); return; }
  if (act === 'addLeave') {
    const s = findStaff($('#lv-who').value), f = $('#lv-from').value, t = $('#lv-to').value;
    if (!s) return;
    if (!isISO(f) || !isISO(t)) { state.leaveErr = 'Pick both dates.'; renderPanel(); return; }
    if (t < f) { state.leaveErr = 'The end date is before the start date.'; renderPanel(); return; }
    if (s.leaves.some(l => !(t < l.from || f > l.to))) { state.leaveErr = `${s.name} already has leave on some of those days.`; renderPanel(); return; }
    s.leaves.push({ id: uid(), from: f, to: t, note: $('#lv-note').value.trim().slice(0, 80) });
    state.leaveErr = ''; changed(); toast(`Leave added for ${s.name}`); return;
  }
  if (act === 'rmLeave') { const s = findStaff(a.dataset.id); if (s) { s.leaves = s.leaves.filter(l => l.id !== a.dataset.lid); changed(); toast('Leave removed'); } return; }
  if (act === 'preset') {
    const p = PRESETS[+a.dataset.k]; const S = plan.settings;
    S.starts = [...p.starts];
    plan.staff.forEach((s, i) => { if (s.base >= S.starts.length) s.base = i % S.starts.length; });
    changed(); toast(`${p.name} shifts applied`); return;
  }
});

document.addEventListener('input', (e) => {
  const el = e.target;
  if (el.dataset?.f === 'name') {
    const s = findStaff(el.dataset.id); if (!s) return;
    s.name = el.value.slice(0, 60);
    clearTimeout(typeTimer); typeTimer = setTimeout(() => changed(false), 350);
  }
});

document.addEventListener('change', (e) => {
  const el = e.target, id = el.id;
  if (id === 'mcMode') { ui.mcMode = el.checked; renderPanel(); return; }
  if (el.dataset?.f && el.dataset.f !== 'name') {
    const s = findStaff(el.dataset.id); if (!s) return;
    const f = el.dataset.f, v = el.value;
    if (f === 'base') s.base = +v;
    else if (f === 'offPref') s.offPref = +v;
    else if (f === 'prevStart') s.prevStart = v === '' ? null : +v;
    else if (f === 'prevOff0' || f === 'prevOff1') {
      const k = f === 'prevOff0' ? 0 : 1; const arr = [s.prevOff[0] ?? null, s.prevOff[1] ?? null]; arr[k] = v === '' ? null : +v;
      s.prevOff = arr.filter((x, j, a) => x != null && a.indexOf(x) === j);
    }
    changed(); return;
  }
  if (el.dataset?.f === 'name') { changed(); return; }
  if (!plan || !id || !id.startsWith('r-')) return;
  const S = plan.settings;
  if (id === 'r-start') { if (isISO(el.value)) { const sat = snapSat(el.value); if (sat !== el.value) toast(`Snapped to Saturday ${fmtS(sat)}`); S.start = sat; } }
  else if (id === 'r-weeks') S.weeks = +el.value;
  else if (id === 'r-min') S.minStaff = +el.value;
  else if (id === 'r-len') S.shiftLen = +el.value;
  else if (id === 'r-rot') S.rotateEvery = +el.value;
  else if (id === 'r-slide') S.maxSlide = +el.value;
  else if (id === 'r-rest') S.restMin = +el.value;
  else if (id === 'r-run') S.maxRun = +el.value;
  else if (id === 'r-wx') S.weekendExtra = +el.value;
  else if (id === 'r-n') {
    const n = +el.value, cur = S.starts;
    if (n !== cur.length) {
      const p = PRESETS.find(x => x.starts.length === n);
      S.starts = p ? [...p.starts] : n === 2 ? [8, 15] : cur;
      plan.staff.forEach((s, i) => { s.base = i % S.starts.length; });
    }
  } else if (id.startsWith('r-s')) {
    const k = +el.dataset.k, v = +el.value;
    if (S.starts.includes(v) && S.starts[k] !== v) { toast('Two shifts cannot start at the same hour'); renderPanel(); return; }
    const old = [...S.starts]; old[k] = v;
    const order = old.map((x, j) => [x, j]).sort((a, b) => a[0] - b[0]);
    const remap = {}; order.forEach(([, j], nk) => { remap[j] = nk; });
    S.starts = order.map(x => x[0]);
    plan.staff.forEach(s => { s.base = remap[s.base] ?? 0; });
  }
  plan = normalize(plan);
  changed();
});

initStore();
})();
</script>

</body></html>
