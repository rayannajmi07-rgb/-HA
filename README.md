<!DOCTYPE html>
<html lang="ar">
<meta name="google-site-verification" content="0lNE4Y3s0Esnu5MFa1ZSX96KxYrjPXrFITMwT1fx_sU" />
 <head>
<meta charset="UTF-8">
<title>المستشار الجامعي الذكي</title>

<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">

<style>
:root{
  --black:#0f0f0f;
  --dark:#1a1a1a;
  --gray:#2a2a2a;
  --border:#3a3a3a;
  --green:#2ecc71;
  --text:#f5f5f5;
  --muted:#bdbdbd;
}

body{
  margin:0;
  font-family:'Cairo',sans-serif;
  background:var(--black);
  color:var(--text);
  direction:rtl;
}

/* ====== Header وزارة التعليم ====== */
.moe-header{
  display:flex;
  justify-content:center;
  align-items:center;
  gap:15px;
  padding:25px 0 10px;
}

.moe-header img{
  height:65px;
}

.moe-text{
  text-align:right;
}

.moe-text span{
  font-size:14px;
  color:var(--muted);
}

.moe-text strong{
  font-size:18px;
  color:var(--green);
  font-weight:700;
}

/* ====== Container ====== */
.container{
  max-width:850px;
  margin:30px auto 50px;
  background:var(--dark);
  padding:35px;
  border-radius:18px;
  border:1px solid var(--border);
}

h1{
  text-align:center;
  color:var(--green);
  margin-bottom:30px;
}

.card{
  background:var(--gray);
  padding:25px;
  border-radius:14px;
  border:1px solid var(--border);
}

label{
  display:block;
  margin-top:18px;
  color:var(--muted);
  font-weight:600;
}

input,select{
  width:100%;
  padding:12px;
  margin-top:8px;
  background:#111;
  border:1px solid var(--border);
  border-radius:10px;
  color:var(--text);
  font-size:15px;
}

input:focus,select:focus{
  outline:none;
  border-color:var(--green);
}

button{
  width:100%;
  margin-top:25px;
  padding:14px;
  border:none;
  border-radius:12px;
  background:var(--green);
  color:#000;
  font-size:17px;
  font-weight:700;
  cursor:pointer;
}

button:hover{
  opacity:0.9;
}

.result{
  margin-top:30px;
  padding:25px;
  background:#111;
  border-radius:14px;
  border:1px solid var(--border);
  line-height:1.8;
}

.result b{
  color:var(--green);
}

.footer-note{
  margin-top:15px;
  font-size:13px;
  color:var(--muted);
  text-align:center;
}
</style>
</head>

<body>

<!-- ====== شعار وزارة التعليم (محلي) ====== -->
<div class="moe-header">
  <img src="logo.png" alt="وزارة التعليم">
  <div class="moe-text">
    <span>المملكة العربية السعودية</span><br>
    <strong>وزارة التعليم</strong>
  </div>
</div>

<div class="container">
<h1>🎓 المستشار الجامعي الذكي</h1>

<div class="card">
<label>🏛️ الجامعة</label>
<select id="university">
  <option value="kingabd">جامعة الملك عبدالعزيز</option>
  <option value="kingkhalid">جامعة الملك خالد</option>
  <option value="imamu">جامعة الإمام محمد بن سعود</option>
  <option value="taibah">جامعة طيبة</option>
  <option value="kfupm">جامعة الملك فهد للبترول والمعادن</option>
</select>

<label>📚 معدل الثانوية</label>
<input id="gpa" type="number" min="0" max="100" placeholder="95">

<label>🧠 القدرات</label>
<input id="qudrat" type="number" min="0" max="100" placeholder="85">

<label>✏️ التحصيلي</label>
<input id="tahsili" type="number" min="0" max="100" placeholder="90">

<label>📑 STEP (اختياري)</label>
<input id="step" type="number" min="0" max="100">

<button id="calculateBtn">تحليل فرص القبول</button>
</div>

<div class="result" id="result"></div>

<div class="footer-note">
⚠️ النتائج تقديرية وقد تختلف حسب سياسة القبول لكل جامعة وسنة.
</div>
</div>

<script>
document.getElementById("calculateBtn").onclick = function(){
  let g = Number(gpa.value),
      q = Number(qudrat.value),
      t = Number(tahsili.value),
      s = Number(step.value)||0,
      u = university.value;

  if(!g || !q || !t){
    alert("الرجاء إدخال جميع الدرجات الأساسية");
    return;
  }

  let wG,wQ,wT,wS;
  switch(u){
    case "kingabd": wG=.3;wQ=.3;wT=.3;wS=.1;break;
    case "kingkhalid": wG=.3;wQ=.3;wT=.35;wS=.05;break;
    case "imamu": wG=.5;wQ=.4;wT=.1;wS=0;break;
    case "taibah": wG=.4;wQ=.3;wT=.3;wS=0;break;
    case "kfupm": wG=.1;wQ=.5;wT=.4;wS=0;break;
  }

  let total = (g*wG)+(q*wQ)+(t*wT)+(s*wS);
  let name = university.selectedOptions[0].text;

  result.innerHTML = `
  <b>الجامعة:</b> ${name}<br>
  <b>النسبة الموزونة:</b> ${total.toFixed(2)}%<br><br>
  <b>التقييم:</b> ${total>=85?"فرص قبول قوية":"تحتاج تحسين"}<br>
  <b>التوصية:</b> ${total>=85?"التقديم على تخصصات علمية":"رفع القدرات والتحصيلي"}
  `;
}
</script>

</body>
</html>
