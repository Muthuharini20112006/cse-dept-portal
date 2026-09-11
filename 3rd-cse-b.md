<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>CSE Department — LeetCode Tracker</title>
<style>
  :root{
    --bg: #0b0d12;
    --panel: #12151c;
    --panel-2: #171b24;
    --line: #232833;
    --ink: #e8ebf2;
    --ink-dim: #8a92a6;
    --accent: #5b8cff;
    --easy: #33d17a;
    --medium: #ffb020;
    --hard: #ff5470;
    --purple: #8b5cf6;
    --orange: #f0883e;
  }
  *{ box-sizing:border-box; }
  html,body{ margin:0; padding:0; }
  body{
    background: radial-gradient(1200px 600px at 10% -10%, #161b26 0%, var(--bg) 55%) fixed;
    color: var(--ink);
    font-family: 'Segoe UI', Inter, ui-sans-serif, system-ui, -apple-system, sans-serif;
    padding: 32px 20px 80px;
  }

  .wrap{ max-width: 1200px; margin: 0 auto; }

  .page-title{
    display:flex; align-items:center; gap:12px; justify-content:center;
    font-size:26px; font-weight:800; margin-bottom:26px;
  }

  header.top{
    display:flex; flex-direction:column; align-items:center; gap:14px;
    margin-bottom: 24px; text-align:center;
  }
  .title-block h1{
    font-size: 24px; margin:0; letter-spacing:-0.02em;
    display:flex; align-items:center; gap:10px;
  }
  .badges{ display:flex; gap:8px; flex-wrap:wrap; justify-content:center; }
  .badge{
    background: var(--panel-2); border:1px solid var(--line);
    padding:6px 12px; border-radius:8px; font-size:12px; color:var(--ink-dim);
    display:flex; gap:6px; align-items:center; font-weight:600; letter-spacing:.03em;
  }
  .badge b, .badge .pill{ color:#0b0d12; font-weight:800; padding:1px 8px; border-radius:6px; }
  .badge .pill.total{ background:var(--easy); }
  .badge .pill.batch{ background:var(--orange); color:#1a1200; }
  .badge .pill.section{ background:var(--purple); color:#fff; }
  .badge .pill.tracking{ background:var(--easy); }

  .quote{
    color:var(--ink-dim); font-style:italic; font-size:14px; text-align:center;
    border-left:3px solid var(--accent); padding:6px 16px; margin: 4px auto 24px; max-width:640px;
  }

  .summary{
    display:grid; grid-template-columns: repeat(4, 1fr); gap:12px;
    margin-bottom: 26px;
  }
  .stat-card{
    background: var(--panel); border:1px solid var(--line); border-radius:12px;
    padding:16px 18px;
  }
  .stat-card .num{ font-size:26px; font-weight:800; }
  .stat-card .lbl{ color:var(--ink-dim); font-size:12px; margin-top:4px; text-transform:uppercase; letter-spacing:.06em; }

  .board{
    background: var(--panel); border:1px solid var(--line); border-radius:14px; overflow:hidden;
  }
  .board-head{
    padding:18px 20px; border-bottom:1px solid var(--line);
    display:flex; align-items:center; gap:10px;
  }
  .board-head h2{ margin:0; font-size:18px; }

  table{ width:100%; border-collapse: collapse; }
  thead th{
    text-align:left; font-size:11px; text-transform:uppercase; letter-spacing:.06em;
    color:var(--ink-dim); padding:12px 16px; border-bottom:1px solid var(--line);
    background: var(--panel-2); position: sticky; top:0;
  }
  tbody td{
    padding:16px; border-bottom:1px solid var(--line); vertical-align:middle; font-size:14px;
  }
  tbody tr:hover{ background: rgba(255,255,255,0.02); }
  tbody tr:last-child td{ border-bottom:none; }

  .rank-cell{ color:var(--ink-dim); font-variant-numeric: tabular-nums; width:38px; }
  .regno{ color:var(--ink-dim); font-variant-numeric: tabular-nums; font-size:13px; white-space:nowrap; }
  .student{ font-weight:700; white-space:nowrap; letter-spacing:.01em; }

  .icon-link{
    display:inline-flex; align-items:center; justify-content:center;
    width:32px; height:32px; text-decoration:none;
  }
  .icon-link.disabled{ opacity:.2; pointer-events:none; }
  .icon-github{ color: var(--purple); }
  .icon-repo{ color: var(--orange); }
  .icon-leetcode{ color: var(--accent); }

  .stats-card{
    display:flex; align-items:center; gap:16px;
    background: var(--panel-2); border:1px solid var(--line); border-radius:10px;
    padding:14px 18px; min-width: 340px;
  }
  .stats-card.empty{ color:var(--ink-dim); font-style:italic; font-size:13px; min-width:auto; }
  .stats-card.loading{ color:var(--ink-dim); font-size:13px; min-width:auto; }
  .stats-card.error{ color:var(--hard); font-size:13px; min-width:auto; }

  .lc-id{
    display:flex; flex-direction:column; gap:2px; min-width:120px;
  }
  .lc-id .uname{ font-weight:700; font-size:14px; }
  .lc-id .rank{ color:var(--ink-dim); font-size:12px; }

  .ring-wrap{ position:relative; width:64px; height:64px; flex:none; }
  .ring-wrap svg{ transform: rotate(-90deg); }
  .ring-total{
    position:absolute; inset:0; display:flex; align-items:center; justify-content:center;
    font-size:17px; font-weight:800;
  }

  .bars{ display:flex; flex-direction:column; gap:6px; flex:1; }
  .bar-row{ display:flex; align-items:center; gap:8px; font-size:12px; }
  .bar-row .lbl{ width:58px; font-weight:700; }
  .bar-row .lbl.easy{ color:var(--easy); }
  .bar-row .lbl.medium{ color:var(--medium); }
  .bar-row .lbl.hard{ color:var(--hard); }
  .bar-row .track{ flex:1; height:5px; border-radius:4px; background:#20242f; overflow:hidden; }
  .bar-row .fill{ height:100%; border-radius:4px; }
  .bar-row .val{ width:72px; text-align:right; color:var(--ink-dim); font-variant-numeric: tabular-nums; }

  footer{
    text-align:center; color:var(--ink-dim); font-size:12px; margin-top:30px;
  }

  @media (max-width: 760px){
    .summary{ grid-template-columns: repeat(2,1fr); }
    table, thead, tbody, th, td, tr{ display:block; }
    thead{ display:none; }
    tbody tr{ padding:14px 16px; border-bottom:1px solid var(--line); }
    tbody td{ border:none; padding:4px 0; display:flex; justify-content:space-between; align-items:center; gap:10px; }
    tbody td::before{ content: attr(data-label); color:var(--ink-dim); font-size:11px; text-transform:uppercase; letter-spacing:.05em; }
    .stats-card{ min-width:0; width:100%; }
  }
</style>
</head>
<body>
<div class="wrap">

  <div class="page-title">💻 CSE Department — LeetCode Tracker</div>

  <header class="top">
    <div class="title-block"><h1>🎓 Batch 2024 – 2028 | Section B</h1></div>
    <div class="badges">
      <span class="badge">TOTAL STUDENTS <span class="pill total" id="hdrTotal">65</span></span>
      <span class="badge">BATCH <span class="pill batch">2024-2028</span></span>
      <span class="badge">SECTION <span class="pill section">B</span></span>
      <span class="badge">TRACKING <span class="pill tracking">ACTIVE</span></span>
    </div>
  </header>

  <div class="quote">🚀 Tracking daily LeetCode progress of CSE 2024–2028 Section B — one problem at a time.</div>

  <div class="summary">
    <div class="stat-card"><div class="num" id="sumSolved">–</div><div class="lbl">Total problems solved</div></div>
    <div class="stat-card"><div class="num" id="sumAvg">–</div><div class="lbl">Avg. solved / student</div></div>
    <div class="stat-card"><div class="num" id="sumTop">–</div><div class="lbl">Top performer</div></div>
    <div class="stat-card"><div class="num" id="sumPending">–</div><div class="lbl">Yet to submit profile</div></div>
  </div>

  <div class="board">
    <div class="board-head">
      <h2>📊 Student Progress Board</h2>
    </div>
    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>Reg No</th>
          <th>Student</th>
          <th>GitHub</th>
          <th>Tracker Repo</th>
          <th>LeetCode</th>
          <th>Live Stats</th>
        </tr>
      </thead>
      <tbody id="rows"></tbody>
    </table>
  </div>

  <footer>Live stats fetched client-side from public LeetCode stat APIs · refresh the page to re-pull latest numbers</footer>
</div>

<script>
const students = [
{r:"710724104064",n:"KAMALESH S",gh:"Kamalesh-S-coder",repo:"https://github.com/Kamalesh-S-coder/Leetcode-Kamalesh-S",lc:"Kamalesh_S_"},
{r:"710724104065",n:"KAMALITHA K",gh:null,repo:null,lc:null},
{r:"710724104066",n:"KANIKA C",gh:null,repo:null,lc:null},
{r:"710724104067",n:"KANISH M",gh:null,repo:null,lc:null},
{r:"710724104068",n:"KARUPPUSAMY A",gh:"A-Karuppusamy06",repo:"https://github.com/A-Karuppusamy06/leetcode-karuppusamy",lc:"karuppusamy-A"},
{r:"710724104069",n:"KATHIR PRASANTH M S",gh:"kathirprasanth725",repo:"https://github.com/kathirprasanth725/Leetcode-Kathir-Prasanth-M-S",lc:"kathirprasanthms"},
{r:"710724104070",n:"KAVINAYA S K",gh:"Kavinaya0120",repo:"https://github.com/Kavinaya0120/Leetcode-Kavinaya",lc:"Kavinaya_Sasikumar"},
{r:"710724104071",n:"KAVINKUMAR M",gh:null,repo:null,lc:null},
{r:"710724104072",n:"KISHORE S",gh:"kishoresaravanan511",repo:"https://github.com/kishoresaravanan511/Leetcode-kishore",lc:"KishoreS_511"},
{r:"710724104073",n:"KRISHNA PRASANTH V",gh:"krishnaprasanthv2006",repo:"https://github.com/krishnaprasanthv2006/LeetCode-Krishna_Prasanth",lc:"krishnaprasanth_v"},
{r:"710724104074",n:"KRISHNAKUMAR M G",gh:"KRISHNAKUMAR-74",repo:"https://github.com/KRISHNAKUMAR-74/LEETCODE-TRACKER---KRISHNAKUMAR",lc:"ir8tIFf7xf"},
{r:"710724104075",n:"LAKSHANA K",gh:null,repo:null,lc:null},
{r:"710724104076",n:"LINGESH B",gh:"Lingeshbs-2007",repo:"https://github.com/Lingeshbs-2007/Leetcode",lc:"J00i7ZP2T8"},
{r:"710724104077",n:"LOGESH K",gh:null,repo:null,lc:null},
{r:"710724104078",n:"LOKNATH T R",gh:null,repo:null,lc:null},
{r:"710724104079",n:"MADAN R K",gh:"rkmadan1311",repo:"https://github.com/rkmadan1311/leetcode-madan-rk",lc:"MadanRK"},
{r:"710724104080",n:"MADHAV KUMAR V M",gh:"madhav-7623",repo:"https://github.com/madhav-7623/Letcode-Tracker-Madhav",lc:"Madhav_76"},
{r:"710724104081",n:"MAHALAKSHMI M",gh:"mahalakshmi-17-2006",repo:"https://github.com/mahalakshmi-17-2006/Leetcode-Maha",lc:"Mahalakshmi-17-01"},
{r:"710724104082",n:"MANJUDHARANI R",gh:"manjudharani1107",repo:"https://github.com/manjudharani1107/Leetcode-Tracker",lc:"Manjudharani"},
{r:"710724104083",n:"MANJUPRIYA K",gh:"Kmanjupriya",repo:"https://github.com/Kmanjupriya/Leetcode-manjupriya",lc:"manju_2006"},
{r:"710724104084",n:"MANOJ R",gh:null,repo:null,lc:null},
{r:"710724104085",n:"MARUTHUPANDI M",gh:"Maruthupandi-M",repo:"https://github.com/Maruthupandi-M/Leetcode-Maruthupandi-M",lc:"MARUTHUPANDI_M"},
{r:"710724104086",n:"MIDUN D",gh:"Midun-28",repo:null,lc:"Midun3399"},
{r:"710724104087",n:"MITHRABALA R S",gh:"mithrabalaRS",repo:"https://github.com/mithrabalaRS/Leetcode-Mithrabala",lc:"__Mithrabala"},
{r:"710724104088",n:"MRITTIKA U P",gh:null,repo:null,lc:null},
{r:"710724104089",n:"MUDIREDDY REVANTH REDDY",gh:"mudireddyrevanthreddy63-arch",repo:"https://github.com/mudireddyrevanthreddy63-arch/Leetcode-Tracker-Revanth-",lc:"MUDIREDDY_REVANTH_REDDY"},
{r:"710724104090",n:"MUHAMMED YASIN M",gh:"YasinM007875",repo:"https://github.com/YasinM007875/Leetcode-Yasin",lc:"Muhammed_YasinM"},
{r:"710724104091",n:"MUTHU KUMAR M",gh:"MuthuKumar257",repo:"https://github.com/MuthuKumar257/Leetcode",lc:"MUTHUKUMAR25"},
{r:"710724104093",n:"MUTHUHARINI M",gh:"Muthuharini20112006",repo:"https://github.com/Muthuharini20112006/Leetcode-tracker",lc:"Harinimariappan20"},
{r:"710724104094",n:"NAGU GANESH VR",gh:null,repo:null,lc:null},
{r:"710724104095",n:"NALINAKSHA N A",gh:null,repo:null,lc:null},
{r:"710724104096",n:"NAMRITHA G",gh:null,repo:null,lc:null},
{r:"710724104097",n:"NANDHANA S",gh:null,repo:null,lc:null},
{r:"710724104098",n:"NANDHINI S",gh:"Nandhini-115",repo:"https://github.com/Nandhini-115/Leetcode--Nandhini",lc:"NandhiniSel_16"},
{r:"710724104099",n:"NARESH K",gh:null,repo:null,lc:null},
{r:"710724104100",n:"NAVANEETHAN K",gh:"Navaneethan36",repo:"https://github.com/Navaneethan36/leetcode-Navaneethan",lc:"NavaneethanKS"},
{r:"710724104101",n:"NAVEEN T",gh:null,repo:null,lc:null},
{r:"710724104102",n:"NAVEENA A",gh:null,repo:null,lc:null},
{r:"710724104103",n:"NIDHISRI M",gh:"nidhisri06",repo:"https://github.com/nidhisri06/leetcode-Nidhisri",lc:"nidhisri_murugaraj"},
{r:"710724104104",n:"NITARSHA R",gh:"Nitarsha",repo:"https://github.com/Nitarsha/leetcode-Nitarsha",lc:"Nisha_rajkumar"},
{r:"710724104105",n:"NITHIN D T",gh:"NITHIN-DT",repo:"https://github.com/NITHIN-DT/leetcode-NithinDT",lc:"NithinDT105"},
{r:"710724104106",n:"NITHIN L",gh:"nithin2006-L",repo:"https://github.com/nithin2006-L/leetcode-Nithin_L",lc:"NITHIN_L_2006_"},
{r:"710724104107",n:"NITHYA SHREE P",gh:null,repo:null,lc:null},
{r:"710724104108",n:"NIYAS AHAMED M",gh:"niyascr72109",repo:"https://github.com/niyascr72109/leetcode-solutions",lc:"niyasahamed2109"},
{r:"710724104109",n:"OSWIN VIBIN ORLANDO",gh:"oswinvibin07",repo:"https://github.com/oswinvibin07/Leetcode-Vibin",lc:"Vibin0204"},
{r:"710724104110",n:"PALLAVI S",gh:"pallavi22092006",repo:"https://github.com/pallavi22092006/Leetcode-Pallavi",lc:"Pallavigowda22"},
{r:"710724104111",n:"PANDILAKSHMI P",gh:"pandilakshmi20062510-dotcom",repo:"https://github.com/pandilakshmi20062510-dotcom/leetcode-Pandilakshmi",lc:"Pandilakshmi_23"},
{r:"710724104112",n:"PARAMESHWARI S",gh:null,repo:null,lc:null},
{r:"710724104113",n:"POONGUZHALI R",gh:"Poonguzhali0403",repo:"https://github.com/Poonguzhali0403/Leetcode-Poonguzhali",lc:"poonguzhali_R"},
{r:"710724104115",n:"PRANOV P M",gh:"pranov05",repo:null,lc:"nice_ance"},
{r:"710724104116",n:"PRAVEEN A",gh:"praveensan2006-spec",repo:"https://github.com/praveensan2006-spec/prav.git",lc:"praveen_A7"},
{r:"710724104117",n:"PRAVEEN R",gh:"PraveenR1510",repo:"https://github.com/PraveenR1510/Leetcode-PraveenR",lc:"Praveen_R1510"},
{r:"710724104118",n:"PRIYANGA V",gh:"priyangavijayakumar0",repo:"https://github.com/priyangavijayakumar0/Leetcode-Priyanga-V",lc:"priyangavijayakumar_0"},
{r:"710724104119",n:"PRIYANKA G",gh:null,repo:null,lc:null},
{r:"710724104120",n:"R LAKSHYA LAVANYA",gh:"Lavanya11-blip",repo:"https://github.com/Lavanya11-blip/Leetcode-Lakshya",lc:"Lakshya-120"},
{r:"710724104121",n:"RAGAVI R",gh:"ragavii45",repo:"https://github.com/ragavii45/Leetcode-RagaviR",lc:"__ragavi"},
{r:"710724104122",n:"RAHMATH H",gh:"rahmathh14",repo:"https://github.com/rahmathh14/Leetcode-RahmathH",lc:"RahmathH"},
{r:"710724104123",n:"RAJALINGAM P",gh:"Rajalingam0512",repo:null,lc:"Rajalingam_P"},
{r:"710724104124",n:"RAJESKUMAR L",gh:null,repo:null,lc:null},
{r:"710724104125",n:"RANJANI S",gh:"ranjani0802007",repo:"https://github.com/ranjani0802007/Leetcode-Ranjani",lc:"Ranjanisathishkumar"},
{r:"710724104305",n:"GOWTHAM K",gh:"Gowtham313968",repo:"https://github.com/Gowtham313968/Leetcode-Gowtham-k",lc:"eDsoOqHSKP"},
{r:"710724104306",n:"A S KAVIN RAJ",gh:"kavinraj6380",repo:"https://github.com/kavinraj6380/Leet-Code-Kavin-Raj",lc:null},
{r:"710724104307",n:"MADHAN G",gh:"madhanmadhan8015-debug",repo:"https://github.com/madhanmadhan8015-debug/Leetcode-Madhan",lc:"25csl07"},
{r:"710724104308",n:"NAREN KARTHIK M S",gh:"Narenkarthikselvam-Git",repo:"https://github.com/Narenkarthikselvam-Git/Leetcode-Naren",lc:"Naren_Karthik_"},
{r:"710724104309",n:"NAVENDHIRAN M",gh:"navendhiranmoorthi1181-gif",repo:"https://github.com/navendhiranmoorthi1181-gif/LeetCode-Navendhiran",lc:"NM7845qZgc"},
];

const ghIcon = `<svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.48 2 2 6.58 2 12.25c0 4.53 2.87 8.37 6.84 9.73.5.1.68-.22.68-.49 0-.24-.01-1.04-.01-1.9-2.78.62-3.37-1.19-3.37-1.19-.45-1.17-1.11-1.48-1.11-1.48-.9-.63.07-.62.07-.62 1 .07 1.53 1.05 1.53 1.05.89 1.56 2.34 1.11 2.91.85.09-.66.35-1.11.63-1.37-2.22-.26-4.56-1.14-4.56-5.06 0-1.12.39-2.03 1.03-2.75-.1-.26-.45-1.31.1-2.72 0 0 .84-.27 2.75 1.05a9.29 9.29 0 015 0c1.91-1.32 2.75-1.05 2.75-1.05.55 1.41.2 2.46.1 2.72.64.72 1.03 1.63 1.03 2.75 0 3.93-2.34 4.8-4.57 5.05.36.32.68.94.68 1.9 0 1.37-.01 2.48-.01 2.82 0 .27.18.6.69.49A10.02 10.02 0 0022 12.25C22 6.58 17.52 2 12 2z"/></svg>`;
const repoIcon = `<svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M4 4.5A2.5 2.5 0 016.5 2h12a1 1 0 011 1v17.5a1 1 0 01-1 1H7a2.5 2.5 0 01-2.5-2.5V4.5zm2.5-.5a.5.5 0 00-.5.5V16a2.49 2.49 0 011-.21V4h9.5V4H6.5zM7.5 17.5A1.5 1.5 0 006 19a1.5 1.5 0 001.5 1.5H18v-3H7.5z"/></svg>`;
const lcIcon = `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"/><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"/></svg>`;
const leetLogo = `<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M13.48 22.34c-1.86 0-3.61-.72-4.94-2.03l-4.34-4.24c-2.73-2.67-2.73-7.02 0-9.69l4.34-4.24a6.93 6.93 0 015.94-1.93c1.97.31 3.68 1.48 4.7 3.22a1 1 0 11-1.73 1.01c-.76-1.3-2.02-2.16-3.46-2.38a4.93 4.93 0 00-4.24 1.38L5.41 7.68a4.95 4.95 0 000 6.93l4.34 4.24a4.93 4.93 0 004.24 1.38c1.44-.22 2.7-1.08 3.46-2.38a1 1 0 111.73 1.01c-1.02 1.74-2.73 2.91-4.7 3.22-.34.05-.67.08-1 .08z"/></svg>`;

const rowsEl = document.getElementById("rows");
let submittedCount = 0;

students.forEach((s, i) => {
  if (s.lc) submittedCount++;
  const tr = document.createElement("tr");
  tr.innerHTML = `
    <td class="rank-cell" data-label="#">${String(i+1).padStart(2,"0")}</td>
    <td class="regno" data-label="Reg No">${s.r}</td>
    <td class="student" data-label="Student">${s.n}</td>
    <td data-label="GitHub">
      ${s.gh ? `<a class="icon-link icon-github" href="https://github.com/${s.gh}" target="_blank" rel="noopener">${ghIcon}</a>` : `<span class="icon-link icon-github disabled">${ghIcon}</span>`}
    </td>
    <td data-label="Tracker Repo">
      ${s.repo ? `<a class="icon-link icon-repo" href="${s.repo}" target="_blank" rel="noopener">${repoIcon}</a>` : `<span class="icon-link icon-repo disabled">${repoIcon}</span>`}
    </td>
    <td data-label="LeetCode">
      ${s.lc ? `<a class="icon-link icon-leetcode" href="https://leetcode.com/u/${s.lc}/" target="_blank" rel="noopener">${lcIcon}</a>` : `<span class="icon-link icon-leetcode disabled">${lcIcon}</span>`}
    </td>
    <td data-label="Live Stats">
      <div class="stats-card ${s.lc ? "loading" : "empty"}" id="stats-${i}">
        ${s.lc ? "Loading…" : "Not submitted"}
      </div>
    </td>
  `;
  rowsEl.appendChild(tr);
});

document.getElementById("hdrTotal").textContent = students.length;
document.getElementById("sumPending").textContent = (students.length - submittedCount);

const API_BASE = "https://leetcode-stats-api.herokuapp.com/";

function ring(pct, total){
  const r = 27, c = 2*Math.PI*r;
  const off = c - (Math.min(pct,100)/100)*c;
  return `
    <div class="ring-wrap">
      <svg width="64" height="64" viewBox="0 0 64 64">
        <circle cx="32" cy="32" r="${r}" fill="none" stroke="#20242f" stroke-width="5"/>
        <circle cx="32" cy="32" r="${r}" fill="none" stroke="var(--medium)" stroke-width="5"
          stroke-dasharray="${c}" stroke-dashoffset="${off}" stroke-linecap="round"/>
      </svg>
      <div class="ring-total">${total}</div>
    </div>`;
}

function barRow(label, cls, val, max, color){
  const pct = max ? Math.min(100, (val/max)*100) : 0;
  return `
    <div class="bar-row">
      <div class="lbl ${cls}">${label}</div>
      <div class="track"><div class="fill" style="width:${pct}%; background:${color}"></div></div>
      <div class="val">${val} / ${max}</div>
    </div>`;
}

async function loadStats(i, username){
  const el = document.getElementById(`stats-${i}`);
  try{
    const res = await fetch(API_BASE + encodeURIComponent(username));
    if(!res.ok) throw new Error("bad response");
    const d = await res.json();
    if(d.status !== "success") throw new Error("api error");

    el.classList.remove("loading");
    el.innerHTML = `
      ${leetLogo}
      <div class="lc-id">
        <span class="uname">${username}</span>
        <span class="rank">#${d.ranking ? d.ranking.toLocaleString() : "—"}</span>
      </div>
      ${ring(d.totalQuestions ? (d.totalSolved/d.totalQuestions*100) : 0, d.totalSolved)}
      <div class="bars">
        ${barRow("Easy", "easy", d.easySolved, d.totalEasy, "var(--easy)")}
        ${barRow("Medium", "medium", d.mediumSolved, d.totalMedium, "var(--medium)")}
        ${barRow("Hard", "hard", d.hardSolved, d.totalHard, "var(--hard)")}
      </div>
    `;
    return d.totalSolved || 0;
  }catch(err){
    el.classList.remove("loading");
    el.classList.add("error");
    el.textContent = "Unable to load stats";
    return null;
  }
}

async function runQueue(items, worker, concurrency = 4){
  let idx = 0;
  const results = [];
  async function next(){
    while(idx < items.length){
      const cur = idx++;
      results[cur] = await worker(items[cur], cur);
    }
  }
  await Promise.all(Array.from({length: concurrency}, next));
  return results;
}

(async () => {
  const targets = students
    .map((s, i) => ({...s, i}))
    .filter(s => s.lc);

  const solvedResults = await runQueue(targets, (t) => loadStats(t.i, t.lc));

  const valid = solvedResults.filter(v => typeof v === "number");
  const totalSolved = valid.reduce((a,b) => a+b, 0);
  document.getElementById("sumSolved").textContent = totalSolved.toLocaleString();
  document.getElementById("sumAvg").textContent = valid.length ? Math.round(totalSolved/valid.length) : "–";

  if(valid.length){
    let topIdx = -1, topVal = -1;
    targets.forEach((t, k) => {
      if(typeof solvedResults[k] === "number" && solvedResults[k] > topVal){
        topVal = solvedResults[k]; topIdx = t.i;
      }
    });
    document.getElementById("sumTop").textContent = topIdx >= 0 ? students[topIdx].n.split(" ")[0] : "–";
  }
})();
</script>
</body>
</html>
