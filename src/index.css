import { useState, useMemo, useEffect } from "react";

const MEDICATIONS = [
  { id:1, name:"Paracetamol", category:"Analgésicos", dosePerKg:15, maxDose:1000, interval:"4-6h", syrup:{conc:160,unit:"mg/5ml"}, drops:{conc:100,unit:"mg/ml"}, minAge:0, notes:"Dosis máxima 75 mg/kg/día" },
  { id:2, name:"Ibuprofeno", category:"Analgésicos", dosePerKg:10, maxDose:400, interval:"6-8h", syrup:{conc:200,unit:"mg/5ml"}, drops:{conc:40,unit:"mg/ml"}, minAge:6, notes:"No usar < 6 meses" },
  { id:3, name:"Metamizol (Dipirona)", category:"Analgésicos", dosePerKg:10, maxDose:500, interval:"6-8h", syrup:{conc:500,unit:"mg/5ml"}, drops:{conc:500,unit:"mg/ml"}, minAge:3, notes:"No usar < 3 meses" },
  { id:4, name:"Amoxicilina", category:"Antibióticos", dosePerKg:25, maxDose:500, interval:"8h", syrup:{conc:250,unit:"mg/5ml"}, drops:{conc:100,unit:"mg/ml"}, minAge:0, notes:"" },
  { id:5, name:"Amoxicilina + Clavulanato", category:"Antibióticos", dosePerKg:25, maxDose:500, interval:"8h", syrup:{conc:250,unit:"mg/5ml"}, drops:{conc:100,unit:"mg/ml"}, minAge:0, notes:"Para infecciones resistentes" },
  { id:6, name:"Cefalexina", category:"Antibióticos", dosePerKg:25, maxDose:500, interval:"6-8h", syrup:{conc:250,unit:"mg/5ml"}, drops:null, minAge:0, notes:"" },
  { id:7, name:"Azitromicina", category:"Antibióticos", dosePerKg:10, maxDose:500, interval:"24h", syrup:{conc:200,unit:"mg/5ml"}, drops:null, minAge:2, notes:"Ciclo de 3-5 días" },
  { id:8, name:"Claritromicina", category:"Antibióticos", dosePerKg:7.5, maxDose:500, interval:"12h", syrup:{conc:125,unit:"mg/5ml"}, drops:null, minAge:6, notes:"" },
  { id:9, name:"Trimetoprim-Sulfametoxazol", category:"Antibióticos", dosePerKg:5, maxDose:160, interval:"12h", syrup:{conc:40,unit:"mg/5ml"}, drops:null, minAge:2, notes:"Dosis en TMP" },
  { id:10, name:"Metronidazol", category:"Antibióticos", dosePerKg:7.5, maxDose:500, interval:"8h", syrup:{conc:200,unit:"mg/5ml"}, drops:{conc:125,unit:"mg/5ml"}, minAge:0, notes:"" },
  { id:11, name:"Loratadina", category:"Antialérgicos", dosePerKg:0.2, maxDose:10, interval:"24h", syrup:{conc:5,unit:"mg/5ml"}, drops:{conc:1,unit:"mg/ml"}, minAge:24, notes:"Máx 10 mg/día" },
  { id:12, name:"Cetirizina", category:"Antialérgicos", dosePerKg:0.25, maxDose:10, interval:"24h", syrup:{conc:5,unit:"mg/5ml"}, drops:{conc:10,unit:"mg/ml"}, minAge:6, notes:"" },
  { id:13, name:"Fexofenadina", category:"Antialérgicos", dosePerKg:2, maxDose:60, interval:"12h", syrup:{conc:30,unit:"mg/5ml"}, drops:null, minAge:24, notes:"" },
  { id:14, name:"Clorfeniramina", category:"Antialérgicos", dosePerKg:0.1, maxDose:4, interval:"6-8h", syrup:{conc:2,unit:"mg/5ml"}, drops:{conc:0.4,unit:"mg/ml"}, minAge:2, notes:"Puede causar somnolencia" },
  { id:15, name:"Ambroxol", category:"Expectorantes", dosePerKg:1.5, maxDose:30, interval:"8-12h", syrup:{conc:15,unit:"mg/5ml"}, drops:{conc:7.5,unit:"mg/ml"}, minAge:0, notes:"" },
  { id:16, name:"Salbutamol", category:"Expectorantes", dosePerKg:0.1, maxDose:2, interval:"4-6h", syrup:{conc:2,unit:"mg/5ml"}, drops:null, minAge:0, notes:"" },
  { id:17, name:"Dextrometorfano", category:"Expectorantes", dosePerKg:0.5, maxDose:30, interval:"6-8h", syrup:{conc:15,unit:"mg/5ml"}, drops:null, minAge:24, notes:"No usar < 2 años" },
  { id:18, name:"Guaifenesina", category:"Expectorantes", dosePerKg:6, maxDose:200, interval:"4-6h", syrup:{conc:100,unit:"mg/5ml"}, drops:null, minAge:24, notes:"" },
  { id:19, name:"Butilhioscina", category:"Antiespasmódicos", dosePerKg:0.5, maxDose:10, interval:"8h", syrup:null, drops:{conc:10,unit:"mg/ml"}, minAge:0, notes:"" },
  { id:20, name:"Simeticona", category:"Antiespasmódicos", dosePerKg:null, maxDose:40, interval:"8h", syrup:null, drops:{conc:40,unit:"mg/0.6ml"}, minAge:0, notes:"0.3 ml < 2 años; 0.6 ml > 2 años" },
  { id:21, name:"Albendazol", category:"Antiparasitarios", dosePerKg:7.5, maxDose:400, interval:"24h", syrup:{conc:200,unit:"mg/5ml"}, drops:null, minAge:12, notes:"Dosis única o 3 días" },
  { id:22, name:"Mebendazol", category:"Antiparasitarios", dosePerKg:null, maxDose:100, interval:"12h", syrup:{conc:100,unit:"mg/5ml"}, drops:null, minAge:12, notes:"100 mg c/12h x 3 días independiente del peso" },
  { id:23, name:"Nitazoxanida", category:"Antiparasitarios", dosePerKg:7.5, maxDose:500, interval:"12h", syrup:{conc:100,unit:"mg/5ml"}, drops:null, minAge:12, notes:"" },
  { id:24, name:"Secnidazol", category:"Antiparasitarios", dosePerKg:30, maxDose:2000, interval:"dosis única", syrup:{conc:500,unit:"mg/5ml"}, drops:null, minAge:12, notes:"Dosis única" },
  { id:25, name:"Nistatina", category:"Antifúngicos", dosePerKg:null, maxDose:null, interval:"6h", syrup:{conc:100000,unit:"UI/ml"}, drops:{conc:100000,unit:"UI/ml"}, minAge:0, notes:"100,000 UI/dosis independiente del peso" },
  { id:26, name:"Fluconazol", category:"Antifúngicos", dosePerKg:6, maxDose:200, interval:"24h", syrup:{conc:50,unit:"mg/5ml"}, drops:null, minAge:0, notes:"" },
  { id:27, name:"Vitamina D3", category:"Vitaminas", dosePerKg:null, maxDose:400, interval:"24h", syrup:null, drops:{conc:400,unit:"UI/gota"}, minAge:0, notes:"400 UI/día lactantes; 600 UI/día niños" },
  { id:28, name:"Hierro (Sulfato Ferroso)", category:"Vitaminas", dosePerKg:3, maxDose:60, interval:"24h", syrup:{conc:25,unit:"mg/5ml"}, drops:{conc:25,unit:"mg/ml"}, minAge:0, notes:"Dar en ayunas con vitamina C" },
  { id:29, name:"Zinc", category:"Vitaminas", dosePerKg:1, maxDose:20, interval:"24h", syrup:{conc:10,unit:"mg/5ml"}, drops:{conc:10,unit:"mg/ml"}, minAge:0, notes:"" },
  { id:30, name:"Vitamina C", category:"Vitaminas", dosePerKg:5, maxDose:500, interval:"24h", syrup:{conc:100,unit:"mg/5ml"}, drops:null, minAge:0, notes:"" },
  { id:31, name:"Ondansetrón", category:"Antieméticos", dosePerKg:0.15, maxDose:8, interval:"8h", syrup:{conc:4,unit:"mg/5ml"}, drops:null, minAge:6, notes:"" },
  { id:32, name:"Domperidona", category:"Antieméticos", dosePerKg:0.25, maxDose:10, interval:"8h", syrup:{conc:5,unit:"mg/5ml"}, drops:{conc:5,unit:"mg/ml"}, minAge:0, notes:"Máx 0.75 mg/kg/día" },
  { id:33, name:"Prednisolona", category:"Corticoides", dosePerKg:1, maxDose:40, interval:"24h", syrup:{conc:15,unit:"mg/5ml"}, drops:null, minAge:0, notes:"" },
  { id:34, name:"Dexametasona", category:"Corticoides", dosePerKg:0.15, maxDose:8, interval:"6-12h", syrup:{conc:0.5,unit:"mg/5ml"}, drops:null, minAge:0, notes:"" },
  { id:35, name:"Fenobarbital", category:"Anticonvulsivantes", dosePerKg:3, maxDose:100, interval:"24h", syrup:{conc:15,unit:"mg/5ml"}, drops:{conc:40,unit:"mg/ml"}, minAge:0, notes:"Solo bajo supervisión médica estricta" },
  { id:36, name:"Ácido Valproico", category:"Anticonvulsivantes", dosePerKg:15, maxDose:500, interval:"8-12h", syrup:{conc:250,unit:"mg/5ml"}, drops:null, minAge:0, notes:"Solo bajo supervisión médica estricta" },
];

const CATEGORIES = [...new Set(MEDICATIONS.map(m => m.category))];
const CAT_COLORS = {
  "Analgésicos":"#ef4444","Antibióticos":"#3b82f6","Antialérgicos":"#8b5cf6",
  "Expectorantes":"#06b6d4","Antiespasmódicos":"#f59e0b","Antiparasitarios":"#10b981",
  "Antifúngicos":"#ec4899","Vitaminas":"#84cc16","Antieméticos":"#f97316",
  "Corticoides":"#6366f1","Anticonvulsivantes":"#dc2626"
};

// WHO simplified height→weight table (cm → kg, percentile 50)
const WHO_HW = [[60,5.9],[65,7.3],[70,8.6],[75,9.9],[80,11.1],[85,12.3],[90,13.4],[95,14.7],[100,16.0],[105,17.6],[110,19.2],[115,21.0],[120,22.9],[125,25.0],[130,27.3],[135,29.7],[140,32.5],[145,35.7],[150,39.5],[155,43.8],[160,48.2]];

function estimateWeight(hStr) {
  const h = parseFloat(hStr);
  if (isNaN(h)) return null;
  for (let i = 0; i < WHO_HW.length - 1; i++) {
    const [h1,w1] = WHO_HW[i], [h2,w2] = WHO_HW[i+1];
    if (h >= h1 && h <= h2) return +(w1 + (h-h1)/(h2-h1)*(w2-w1)).toFixed(1);
  }
  return h < 60 ? WHO_HW[0][1] : WHO_HW[WHO_HW.length-1][1];
}

function getDoseSchedule(interval) {
  const h = parseInt(interval.split("-")[0]);
  if (!h || h === 0) return ["Dosis única"];
  const n = Math.round(24/h), start = 7;
  return Array.from({length:n}, (_,i) => {
    const hr = (start + i*h) % 24;
    const period = hr < 12 ? "AM" : "PM";
    const hr12 = hr === 0 ? 12 : hr > 12 ? hr - 12 : hr;
    return `${hr12}:00 ${period}`;
  });
}

function calcOneMed(med, weightKg, ageMths, pres) {
  const warnings = [];
  if (ageMths < med.minAge) warnings.push(`⚠️ No recomendado < ${med.minAge} meses`);
  let dose;
  if (med.dosePerKg) {
    dose = +(med.dosePerKg * weightKg).toFixed(2);
    if (med.maxDose && dose > med.maxDose) { warnings.push(`⚠️ Ajustada al máximo (${med.maxDose} mg)`); dose = med.maxDose; }
  } else { dose = med.maxDose || 0; warnings.push("ℹ️ Dosis fija"); }
  let volume = null, drops = null;
  if (pres === "jarabe" && med.syrup) {
    volume = med.id===25 ? "1 ml" : +((dose/med.syrup.conc)*5).toFixed(2)+" ml";
  } else if (pres === "gotas" && med.drops) {
    if (med.id===27) { drops="1 gota"; }
    else { const ml=+(dose/med.drops.conc).toFixed(2); volume=ml+" ml"; drops=Math.round(ml*20)+" gotas"; }
  }
  if (med.notes) warnings.push("ℹ️ "+med.notes);
  return { med, dose, volume, drops, warnings, interval:med.interval };
}

export default function App() {
  const [tab, setTab] = useState("calc");
  const [dark, setDark] = useState(false);
  const [gender, setGender] = useState("niño");
  const [weightVal, setWeightVal] = useState("");
  const [weightUnit, setWeightUnit] = useState("kg");
  const [ageVal, setAgeVal] = useState("");
  const [ageUnit, setAgeUnit] = useState("meses");
  const [heightVal, setHeightVal] = useState("");
  const [showWHO, setShowWHO] = useState(false);
  const [pres, setPres] = useState("jarabe");
  const [selCat, setSelCat] = useState(null);
  const [calcSearch, setCalcSearch] = useState("");
  const [selMed1, setSelMed1] = useState(null);
  const [selMed2, setSelMed2] = useState(null);
  const [results, setResults] = useState([]);
  const [history, setHistory] = useState([]);
  const [listCat, setListCat] = useState("todas");
  const [listSearch, setListSearch] = useState("");
  const [showConv, setShowConv] = useState(true);
  const [copied, setCopied] = useState(false);
  const [timerSecs, setTimerSecs] = useState(0);
  const [timerActive, setTimerActive] = useState(false);
  const [timerLabel, setTimerLabel] = useState("");

  const T = {
    bg: dark?"#0f172a":"#f0f9ff", card:dark?"#1e293b":"#fff",
    border:dark?"#334155":"#e2e8f0", text:dark?"#f1f5f9":"#1e293b",
    sub:dark?"#94a3b8":"#64748b", inp:dark?"#0f172a":"#fff",
    inBorder:dark?"#475569":"#cbd5e1", muted:dark?"#334155":"#f8fafc",
    mutedTxt:dark?"#475569":"#94a3b8",
  };

  useEffect(()=>{
    if (!timerActive||timerSecs<=0){if(timerSecs<=0&&timerActive)setTimerActive(false);return;}
    const id=setInterval(()=>setTimerSecs(s=>s-1),1000);
    return ()=>clearInterval(id);
  },[timerActive,timerSecs]);

  const weightKg = useMemo(()=>{
    const v=parseFloat(weightVal); if(isNaN(v))return null;
    return weightUnit==="lbs"?+(v*0.453592).toFixed(2):v;
  },[weightVal,weightUnit]);

  const ageMths = useMemo(()=>{
    const v=parseFloat(ageVal); if(isNaN(v))return null;
    return ageUnit==="años"?Math.round(v*12):v;
  },[ageVal,ageUnit]);

  const whoEst = useMemo(()=>estimateWeight(heightVal),[heightVal]);

  const calcMeds = useMemo(()=>MEDICATIONS.filter(m=>
    (selCat?m.category===selCat:true)&&
    (pres==="jarabe"?m.syrup:m.drops)&&
    m.name.toLowerCase().includes(calcSearch.toLowerCase())
  ),[selCat,pres,calcSearch]);

  const listMeds = useMemo(()=>MEDICATIONS.filter(m=>
    (listCat==="todas"?true:m.category===listCat)&&
    m.name.toLowerCase().includes(listSearch.toLowerCase())
  ),[listCat,listSearch]);

  function calculate(){
    if(!weightKg||!ageMths||!selMed1)return;
    const r=[];
    const m1=MEDICATIONS.find(m=>m.id===selMed1);
    if(m1)r.push(calcOneMed(m1,weightKg,ageMths,pres));
    if(selMed2){const m2=MEDICATIONS.find(m=>m.id===selMed2);if(m2)r.push(calcOneMed(m2,weightKg,ageMths,pres));}
    setResults(r);
    setHistory(h=>[{id:Date.now(),time:new Date().toLocaleTimeString('es',{hour:'2-digit',minute:'2-digit'}),date:new Date().toLocaleDateString('es'),gender,weightKg,ageMths,pres,results:r},...h.slice(0,19)]);
  }

  function buildRecipe(){
    if(!results.length)return"";
    const lines=[`👶 ${gender==="niño"?"Niño":"Niña"} · ${weightKg} kg · ${ageMths<24?ageMths+" meses":+(ageMths/12).toFixed(1)+" años"}`,"─────────────────"];
    results.forEach(r=>{
      lines.push(`💊 ${r.med.name} (${pres==="jarabe"?"Jarabe":"Gotas"})`);
      lines.push(`   Dosis: ${r.dose} mg`);
      if(r.volume)lines.push(`   Volumen: ${r.volume}`);
      if(r.drops)lines.push(`   Gotas: ${r.drops}`);
      lines.push(`   Intervalo: c/${r.interval}`);
      lines.push(`   Horario: ${getDoseSchedule(r.interval).join(" · ")}`);
    });
    lines.push("─────────────────","⚕️ Dosis Pediátrica v2.0");
    return lines.join("\n");
  }

  async function copyRecipe(){
    try{await navigator.clipboard.writeText(buildRecipe());setCopied(true);setTimeout(()=>setCopied(false),2500);}catch{}
  }

  function startTimer(intStr){
    const h=parseInt(intStr.split("-")[0]);
    if(!h)return;
    setTimerSecs(h*3600);setTimerLabel(`Próxima dosis en ${h}h`);setTimerActive(true);
  }

  function fmt(s){const h=Math.floor(s/3600),m=Math.floor((s%3600)/60),sc=s%60;return`${String(h).padStart(2,'0')}:${String(m).padStart(2,'0')}:${String(sc).padStart(2,'0')}`;}

  const gEmoji=gender==="niño"?"👦":"👧";

  return(
    <div style={{fontFamily:"'Segoe UI',sans-serif",background:T.bg,minHeight:"100vh",maxWidth:480,margin:"0 auto",display:"flex",flexDirection:"column",transition:"background .3s"}}>

      {/* Header */}
      <div style={{background:"linear-gradient(135deg,#0ea5e9,#06b6d4)",padding:"14px 18px",color:"#fff",display:"flex",justifyContent:"space-between",alignItems:"center",boxShadow:"0 2px 8px rgba(0,0,0,0.15)"}}>
        <div><div style={{fontSize:19,fontWeight:700}}>💊 Dosis Pediátrica</div><div style={{fontSize:11,opacity:.85}}>Calculadora Médica Infantil</div></div>
        <button onClick={()=>setDark(!dark)} style={{background:"rgba(255,255,255,0.2)",border:"none",borderRadius:20,padding:"7px 13px",color:"#fff",cursor:"pointer",fontSize:16}}>{dark?"☀️":"🌙"}</button>
      </div>

      {/* Timer Bar */}
      {timerActive&&(
        <div style={{background:dark?"#1e3a5f":"#dbeafe",padding:"8px 16px",display:"flex",justifyContent:"space-between",alignItems:"center",borderBottom:`1px solid ${dark?"#334155":"#bfdbfe"}`}}>
          <span style={{fontSize:12,fontWeight:600,color:dark?"#93c5fd":"#1d4ed8"}}>⏰ {timerLabel}</span>
          <span style={{fontSize:17,fontWeight:800,color:dark?"#60a5fa":"#2563eb",fontFamily:"monospace"}}>{fmt(timerSecs)}</span>
          <button onClick={()=>setTimerActive(false)} style={{background:"none",border:"none",color:T.sub,cursor:"pointer",fontSize:14}}>✕</button>
        </div>
      )}

      {/* Tabs */}
      <div style={{display:"flex",background:T.card,borderBottom:`2px solid ${dark?"#334155":"#e0f2fe"}`}}>
        {[["calc","🧮","Calcular"],["history","📋","Historial"],["meds","💊","Medicam."],["config","⚙️","Config"]].map(([k,ico,l])=>(
          <button key={k} onClick={()=>setTab(k)} style={{flex:1,padding:"10px 0",border:"none",background:"none",fontWeight:tab===k?700:500,color:tab===k?"#0ea5e9":T.sub,borderBottom:tab===k?"3px solid #0ea5e9":"3px solid transparent",cursor:"pointer",fontSize:11}}>
            <div style={{fontSize:15}}>{ico}</div><div>{l}</div>
          </button>
        ))}
      </div>

      <div style={{flex:1,overflowY:"auto",padding:"13px"}}>

        {/* ====== CALCULADORA ====== */}
        {tab==="calc"&&(
          <div style={{display:"flex",flexDirection:"column",gap:11}}>

            {/* Género */}
            <div style={{background:T.card,borderRadius:12,padding:13,boxShadow:"0 1px 4px rgba(0,0,0,0.08)"}}>
              <div style={{fontSize:12,fontWeight:600,color:T.sub,marginBottom:7}}>👶 Paciente</div>
              <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:8}}>
                {["niño","niña"].map(g=>(
                  <button key={g} onClick={()=>setGender(g)} style={{padding:"10px",borderRadius:10,border:`2px solid ${gender===g?(g==="niño"?"#3b82f6":"#ec4899"):T.border}`,background:gender===g?(g==="niño"?"#eff6ff":"#fdf2f8"):T.muted,cursor:"pointer",fontWeight:gender===g?700:500,color:gender===g?(g==="niño"?"#3b82f6":"#ec4899"):T.sub,fontSize:15}}>
                    {g==="niño"?"👦 Niño":"👧 Niña"}
                  </button>
                ))}
              </div>
            </div>

            {/* Datos */}
            <div style={{background:T.card,borderRadius:12,padding:13,boxShadow:"0 1px 4px rgba(0,0,0,0.08)"}}>
              <div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:9}}>
                <div style={{fontSize:12,fontWeight:600,color:T.sub}}>📏 Datos del Paciente</div>
                <button onClick={()=>setShowWHO(!showWHO)} style={{fontSize:10,color:"#0ea5e9",background:"#e0f2fe",border:"none",borderRadius:20,padding:"3px 9px",cursor:"pointer",fontWeight:600}}>📐 Estimar por talla</button>
              </div>
              {showWHO&&(
                <div style={{marginBottom:10,padding:10,background:dark?"#0f172a":"#f0f9ff",borderRadius:10,border:`1px solid ${dark?"#334155":"#bae6fd"}`}}>
                  <div style={{fontSize:11,color:T.sub,marginBottom:5}}>Talla en cm → peso estimado (OMS p50)</div>
                  <div style={{display:"flex",gap:7,alignItems:"center"}}>
                    <input value={heightVal} onChange={e=>setHeightVal(e.target.value)} placeholder="ej: 90" type="number" style={{flex:1,padding:"7px",border:`1px solid ${T.inBorder}`,borderRadius:8,fontSize:14,background:T.inp,color:T.text,outline:"none"}}/>
                    {whoEst&&<button onClick={()=>{setWeightVal(String(whoEst));setWeightUnit("kg");}} style={{padding:"7px 11px",background:"#0ea5e9",color:"#fff",border:"none",borderRadius:8,cursor:"pointer",fontSize:11,fontWeight:700,whiteSpace:"nowrap"}}>Usar {whoEst} kg</button>}
                  </div>
                  {whoEst&&<div style={{fontSize:10,color:"#0ea5e9",marginTop:3}}>≈ {whoEst} kg</div>}
                </div>
              )}
              <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:9}}>
                <div>
                  <label style={{fontSize:11,color:T.sub,display:"block",marginBottom:3}}>⚖️ Peso</label>
                  <div style={{display:"flex",gap:3}}>
                    <input value={weightVal} onChange={e=>setWeightVal(e.target.value)} placeholder="0.0" type="number" step="0.1" min="0" style={{flex:1,padding:"8px",border:`1px solid ${T.inBorder}`,borderRadius:8,fontSize:14,outline:"none",background:T.inp,color:T.text,width:"100%"}}/>
                    <select value={weightUnit} onChange={e=>setWeightUnit(e.target.value)} style={{padding:"8px 3px",border:`1px solid ${T.inBorder}`,borderRadius:8,fontSize:12,background:T.inp,color:T.text,cursor:"pointer"}}>
                      <option>kg</option><option>lbs</option>
                    </select>
                  </div>
                  {showConv&&weightKg&&weightUnit==="lbs"&&<div style={{fontSize:10,color:"#0ea5e9",marginTop:2}}>≈ {weightKg} kg</div>}
                </div>
                <div>
                  <label style={{fontSize:11,color:T.sub,display:"block",marginBottom:3}}>📅 Edad</label>
                  <div style={{display:"flex",gap:3}}>
                    <input value={ageVal} onChange={e=>setAgeVal(e.target.value)} placeholder="0" type="number" min="0" style={{flex:1,padding:"8px",border:`1px solid ${T.inBorder}`,borderRadius:8,fontSize:14,outline:"none",background:T.inp,color:T.text,width:"100%"}}/>
                    <select value={ageUnit} onChange={e=>setAgeUnit(e.target.value)} style={{padding:"8px 3px",border:`1px solid ${T.inBorder}`,borderRadius:8,fontSize:12,background:T.inp,color:T.text,cursor:"pointer"}}>
                      <option>meses</option><option>años</option>
                    </select>
                  </div>
                  {showConv&&ageMths&&ageUnit==="años"&&<div style={{fontSize:10,color:"#0ea5e9",marginTop:2}}>≈ {ageMths} meses</div>}
                </div>
              </div>
            </div>

            {/* Presentación */}
            <div style={{background:T.card,borderRadius:12,padding:13,boxShadow:"0 1px 4px rgba(0,0,0,0.08)"}}>
              <div style={{fontSize:12,fontWeight:600,color:T.sub,marginBottom:7}}>💉 Presentación</div>
              <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:8}}>
                {[["jarabe","🍶 Jarabe"],["gotas","💧 Gotas"]].map(([k,l])=>(
                  <button key={k} onClick={()=>{setPres(k);setSelMed1(null);setSelMed2(null);setResults([]);}} style={{padding:"10px",borderRadius:10,border:`2px solid ${pres===k?"#0ea5e9":T.border}`,background:pres===k?"#e0f2fe":T.muted,cursor:"pointer",fontWeight:pres===k?700:500,color:pres===k?"#0ea5e9":T.sub,fontSize:14}}>{l}</button>
                ))}
              </div>
            </div>

            {/* Selección medicamentos */}
            <div style={{background:T.card,borderRadius:12,padding:13,boxShadow:"0 1px 4px rgba(0,0,0,0.08)"}}>
              <div style={{fontSize:12,fontWeight:600,color:T.sub,marginBottom:7}}>🔍 Seleccionar Medicamentos</div>
              <input value={calcSearch} onChange={e=>setCalcSearch(e.target.value)} placeholder="Buscar por nombre..." style={{width:"100%",padding:"8px 11px",border:`1px solid ${T.inBorder}`,borderRadius:8,fontSize:13,background:T.inp,color:T.text,outline:"none",boxSizing:"border-box",marginBottom:7}}/>
              <div style={{display:"flex",flexWrap:"wrap",gap:5,marginBottom:9}}>
                <button onClick={()=>setSelCat(null)} style={{padding:"4px 9px",borderRadius:20,border:`2px solid ${!selCat?"#0ea5e9":T.border}`,background:!selCat?"#e0f2fe":T.muted,cursor:"pointer",fontSize:10,fontWeight:!selCat?700:500,color:!selCat?"#0ea5e9":T.sub}}>Todas</button>
                {CATEGORIES.map(c=>(
                  <button key={c} onClick={()=>setSelCat(c)} style={{padding:"4px 9px",borderRadius:20,border:`2px solid ${selCat===c?CAT_COLORS[c]:T.border}`,background:selCat===c?CAT_COLORS[c]+"22":T.muted,cursor:"pointer",fontSize:10,fontWeight:selCat===c?700:500,color:selCat===c?CAT_COLORS[c]:T.sub}}>{c}</button>
                ))}
              </div>

              <div style={{fontSize:11,fontWeight:700,color:"#0ea5e9",marginBottom:4}}>Medicamento 1 {selMed1?"✅":""}</div>
              <div style={{maxHeight:150,overflowY:"auto",display:"flex",flexDirection:"column",gap:4,marginBottom:9}}>
                {calcMeds.map(m=>(
                  <button key={m.id} onClick={()=>{setSelMed1(m.id===selMed1?null:m.id);setResults([]);}} style={{padding:"8px 11px",borderRadius:8,border:`2px solid ${selMed1===m.id?CAT_COLORS[m.category]||"#0ea5e9":T.border}`,background:selMed1===m.id?(CAT_COLORS[m.category]||"#0ea5e9")+"18":T.muted,cursor:"pointer",textAlign:"left",display:"flex",justifyContent:"space-between",alignItems:"center"}}>
                    <span style={{fontWeight:selMed1===m.id?700:500,fontSize:12,color:selMed1===m.id?CAT_COLORS[m.category]||"#0ea5e9":T.text}}>{m.name}</span>
                    <span style={{fontSize:9,color:T.sub,padding:"2px 6px",borderRadius:20,background:T.muted}}>{m.category}</span>
                  </button>
                ))}
              </div>

              <div style={{fontSize:11,fontWeight:700,color:"#10b981",marginBottom:4}}>Medicamento 2 — opcional {selMed2?"✅":""}</div>
              <div style={{maxHeight:130,overflowY:"auto",display:"flex",flexDirection:"column",gap:4}}>
                <button onClick={()=>{setSelMed2(null);setResults([]);}} style={{padding:"7px 11px",borderRadius:8,border:`2px solid ${!selMed2?"#10b981":T.border}`,background:!selMed2?"#d1fae5":T.muted,cursor:"pointer",textAlign:"left",fontSize:11,color:!selMed2?"#065f46":T.sub,fontWeight:!selMed2?700:400}}>— Ninguno</button>
                {calcMeds.filter(m=>m.id!==selMed1).map(m=>(
                  <button key={m.id} onClick={()=>{setSelMed2(m.id===selMed2?null:m.id);setResults([]);}} style={{padding:"8px 11px",borderRadius:8,border:`2px solid ${selMed2===m.id?CAT_COLORS[m.category]||"#10b981":T.border}`,background:selMed2===m.id?(CAT_COLORS[m.category]||"#10b981")+"18":T.muted,cursor:"pointer",textAlign:"left",display:"flex",justifyContent:"space-between",alignItems:"center"}}>
                    <span style={{fontWeight:selMed2===m.id?700:500,fontSize:12,color:selMed2===m.id?CAT_COLORS[m.category]||"#10b981":T.text}}>{m.name}</span>
                    <span style={{fontSize:9,color:T.sub,padding:"2px 6px",borderRadius:20}}>{m.category}</span>
                  </button>
                ))}
              </div>
            </div>

            {/* Botón calcular */}
            <button onClick={calculate} disabled={!weightKg||!ageMths||!selMed1} style={{padding:"14px",borderRadius:12,border:"none",background:(!weightKg||!ageMths||!selMed1)?"#cbd5e1":"linear-gradient(135deg,#0ea5e9,#06b6d4)",color:"#fff",fontWeight:700,fontSize:16,cursor:(!weightKg||!ageMths||!selMed1)?"not-allowed":"pointer",boxShadow:(!weightKg||!ageMths||!selMed1)?"none":"0 4px 12px rgba(14,165,233,0.4)"}}>
              🧮 Calcular Dosis
            </button>

            {/* Resultados */}
            {results.map((res,idx)=>(
              <div key={idx} style={{background:T.card,borderRadius:12,padding:15,boxShadow:"0 2px 10px rgba(0,0,0,0.1)",border:`2px solid ${idx===0?"#0ea5e9":"#10b981"}`}}>
                <div style={{display:"flex",alignItems:"center",gap:10,marginBottom:11}}>
                  <div style={{fontSize:30}}>{gEmoji}</div>
                  <div style={{flex:1}}>
                    <div style={{fontWeight:700,fontSize:15,color:idx===0?"#0ea5e9":"#10b981"}}>{res.med.name}</div>
                    <div style={{fontSize:11,color:T.sub}}>{pres==="jarabe"?"🍶 Jarabe":"💧 Gotas"} · c/{res.interval}</div>
                  </div>
                  {idx===0&&<button onClick={()=>startTimer(res.interval)} style={{background:"#fef3c7",border:"1px solid #fbbf24",borderRadius:8,padding:"6px 9px",cursor:"pointer",fontSize:10,color:"#92400e",fontWeight:700}}>⏰ Recordar</button>}
                </div>
                <div style={{background:dark?"#0f172a":"#f0f9ff",borderRadius:10,padding:11,marginBottom:9}}>
                  <div style={{color:T.sub,fontSize:11,marginBottom:3}}>Dosis calculada:</div>
                  <div style={{fontSize:25,fontWeight:800,color:"#0369a1"}}>{res.dose} mg</div>
                  {res.volume&&<div style={{fontSize:17,fontWeight:700,color:"#0ea5e9",marginTop:2}}>📏 {res.volume}</div>}
                  {res.drops&&<div style={{fontSize:15,fontWeight:600,color:"#06b6d4",marginTop:2}}>💧 {res.drops}</div>}
                </div>
                <div style={{marginBottom:9}}>
                  <div style={{fontSize:11,color:T.sub,marginBottom:5}}>📅 Horario sugerido:</div>
                  <div style={{display:"flex",flexWrap:"wrap",gap:5}}>
                    {getDoseSchedule(res.interval).map((t,i)=>(
                      <div key={i} style={{background:"#0ea5e9",color:"#fff",borderRadius:7,padding:"4px 9px",fontSize:11,fontWeight:700}}>{t}</div>
                    ))}
                  </div>
                </div>
                {res.warnings.map((w,i)=>(
                  <div key={i} style={{marginTop:5,padding:"6px 9px",borderRadius:7,background:w.startsWith("⚠️")?(dark?"#451a03":"#fff7ed"):(dark?"#0c1e3c":"#f0f9ff"),border:`1px solid ${w.startsWith("⚠️")?"#fbbf24":"#7dd3fc"}`,fontSize:11,color:w.startsWith("⚠️")?"#92400e":"#0369a1"}}>{w}</div>
                ))}
              </div>
            ))}

            {results.length>0&&(
              <>
                <button onClick={copyRecipe} style={{padding:"12px",borderRadius:12,border:`2px solid ${copied?"#10b981":"#0ea5e9"}`,background:copied?(dark?"#064e3b":"#d1fae5"):(dark?"#0c2340":"#e0f2fe"),color:copied?"#065f46":"#0369a1",fontWeight:700,fontSize:14,cursor:"pointer"}}>
                  {copied?"✅ ¡Receta copiada!":"📋 Copiar Receta (WhatsApp / Imprimir)"}
                </button>
                <div style={{padding:"9px 11px",borderRadius:9,background:dark?"#1f0a0a":"#fef2f2",border:"1px solid #fca5a5",fontSize:11,color:"#991b1b"}}>
                  ⚕️ Herramienta orientativa. Confirme con el médico tratante antes de administrar.
                </div>
              </>
            )}
          </div>
        )}

        {/* ====== HISTORIAL ====== */}
        {tab==="history"&&(
          <div style={{display:"flex",flexDirection:"column",gap:10}}>
            <div style={{fontSize:13,fontWeight:600,color:T.sub}}>📋 Historial de sesión</div>
            {history.length===0&&(
              <div style={{background:T.card,borderRadius:12,padding:24,textAlign:"center",color:T.mutedTxt,fontSize:14}}>No hay cálculos aún.<br/>Usa la calculadora para ver el historial.</div>
            )}
            {history.map(h=>(
              <div key={h.id} style={{background:T.card,borderRadius:12,padding:13,boxShadow:"0 1px 4px rgba(0,0,0,0.08)",borderLeft:"4px solid #0ea5e9"}}>
                <div style={{display:"flex",justifyContent:"space-between",marginBottom:5}}>
                  <span style={{fontWeight:700,color:T.text}}>{h.gender==="niño"?"👦":"👧"} {h.weightKg} kg · {h.ageMths<24?h.ageMths+"m":+(h.ageMths/12).toFixed(1)+"a"}</span>
                  <span style={{fontSize:10,color:T.sub}}>{h.date} {h.time}</span>
                </div>
                <div style={{fontSize:11,color:T.sub,marginBottom:5}}>{h.pres==="jarabe"?"🍶 Jarabe":"💧 Gotas"}</div>
                {h.results.map((r,i)=>(
                  <div key={i} style={{background:dark?"#0f172a":"#f8fafc",borderRadius:7,padding:"7px 9px",marginBottom:3}}>
                    <div style={{fontWeight:600,fontSize:12,color:"#0ea5e9"}}>{r.med.name}</div>
                    <div style={{fontSize:11,color:T.sub}}>{r.dose} mg {r.volume?"· "+r.volume:""} {r.drops?"· "+r.drops:""} · c/{r.interval}</div>
                  </div>
                ))}
              </div>
            ))}
            {history.length>0&&(
              <button onClick={()=>setHistory([])} style={{padding:"10px",borderRadius:10,border:`1px solid ${T.border}`,background:T.card,color:"#ef4444",cursor:"pointer",fontSize:13,fontWeight:600}}>🗑️ Limpiar historial</button>
            )}
          </div>
        )}

        {/* ====== MEDICAMENTOS ====== */}
        {tab==="meds"&&(
          <div style={{display:"flex",flexDirection:"column",gap:9}}>
            <input value={listSearch} onChange={e=>setListSearch(e.target.value)} placeholder="🔍 Buscar medicamento..." style={{padding:"9px 13px",border:`1px solid ${T.inBorder}`,borderRadius:10,fontSize:13,outline:"none",background:T.inp,color:T.text}}/>
            <div style={{display:"flex",flexWrap:"wrap",gap:5}}>
              <button onClick={()=>setListCat("todas")} style={{padding:"4px 10px",borderRadius:20,border:`2px solid ${listCat==="todas"?"#0ea5e9":T.border}`,background:listCat==="todas"?"#e0f2fe":T.card,cursor:"pointer",fontSize:10,fontWeight:listCat==="todas"?700:500,color:listCat==="todas"?"#0ea5e9":T.sub}}>Todas</button>
              {CATEGORIES.map(c=>(
                <button key={c} onClick={()=>setListCat(c)} style={{padding:"4px 10px",borderRadius:20,border:`2px solid ${listCat===c?CAT_COLORS[c]:T.border}`,background:listCat===c?CAT_COLORS[c]+"22":T.card,cursor:"pointer",fontSize:10,fontWeight:listCat===c?700:500,color:listCat===c?CAT_COLORS[c]:T.sub}}>{c}</button>
              ))}
            </div>
            <div style={{fontSize:11,color:T.mutedTxt}}>{listMeds.length} medicamento(s)</div>
            {listMeds.map(m=>(
              <div key={m.id} style={{background:T.card,borderRadius:11,padding:13,boxShadow:"0 1px 4px rgba(0,0,0,0.07)",borderLeft:`4px solid ${CAT_COLORS[m.category]||"#0ea5e9"}`}}>
                <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start"}}>
                  <div style={{fontWeight:700,fontSize:13,color:T.text}}>{m.name}</div>
                  <span style={{fontSize:10,background:CAT_COLORS[m.category]+"22",color:CAT_COLORS[m.category],padding:"2px 7px",borderRadius:20,fontWeight:600}}>{m.category}</span>
                </div>
                <div style={{marginTop:5,fontSize:11,color:T.sub,display:"flex",flexWrap:"wrap",gap:7}}>
                  {m.dosePerKg&&<span>💊 {m.dosePerKg} mg/kg</span>}
                  {m.maxDose&&<span>🔺 Máx {m.maxDose} mg</span>}
                  <span>⏰ c/{m.interval}</span>
                  {m.syrup&&<span>🍶 {m.syrup.conc} {m.syrup.unit}</span>}
                  {m.drops&&<span>💧 {m.drops.conc} {m.drops.unit}</span>}
                  {m.minAge>0&&<span style={{color:"#f59e0b"}}>⚠️ +{m.minAge}m</span>}
                </div>
                {m.notes&&<div style={{marginTop:5,fontSize:10,color:"#6366f1",background:dark?"#1e1b4b":"#eef2ff",padding:"3px 7px",borderRadius:5}}>{m.notes}</div>}
              </div>
            ))}
          </div>
        )}

        {/* ====== CONFIG ====== */}
        {tab==="config"&&(
          <div style={{display:"flex",flexDirection:"column",gap:11}}>
            <div style={{background:T.card,borderRadius:12,padding:15,boxShadow:"0 1px 4px rgba(0,0,0,0.08)"}}>
              <div style={{fontWeight:700,color:T.text,marginBottom:11}}>⚙️ Preferencias</div>
              {[["Unidad de peso",["kg","lbs"],weightUnit,setWeightUnit],["Unidad de edad",["meses","años"],ageUnit,setAgeUnit]].map(([lbl,opts,val,set])=>(
                <div key={lbl} style={{marginBottom:11}}>
                  <div style={{fontSize:12,color:T.sub,marginBottom:5}}>{lbl}</div>
                  <div style={{display:"flex",gap:7}}>
                    {opts.map(u=>(
                      <button key={u} onClick={()=>set(u)} style={{flex:1,padding:"9px",borderRadius:9,border:`2px solid ${val===u?"#0ea5e9":T.border}`,background:val===u?"#e0f2fe":T.muted,cursor:"pointer",fontWeight:val===u?700:500,color:val===u?"#0ea5e9":T.sub,fontSize:13}}>{u}</button>
                    ))}
                  </div>
                </div>
              ))}
              {[["Mostrar conversiones","kg↔lbs, meses↔años",showConv,setShowConv],["🌙 Modo oscuro","Para guardias nocturnas",dark,setDark]].map(([lbl,desc,val,set])=>(
                <div key={lbl} style={{display:"flex",justifyContent:"space-between",alignItems:"center",padding:"9px 0",borderTop:`1px solid ${T.border}`}}>
                  <div><div style={{fontSize:12,fontWeight:600,color:T.text}}>{lbl}</div><div style={{fontSize:10,color:T.sub}}>{desc}</div></div>
                  <button onClick={()=>set(!val)} style={{width:42,height:23,borderRadius:12,border:"none",background:val?"#0ea5e9":"#cbd5e1",cursor:"pointer",position:"relative",flexShrink:0}}>
                    <div style={{width:17,height:17,background:"#fff",borderRadius:9,position:"absolute",top:3,left:val?22:3,transition:"left .2s"}}/>
                  </button>
                </div>
              ))}
            </div>

            <div style={{background:T.card,borderRadius:12,padding:15,boxShadow:"0 1px 4px rgba(0,0,0,0.08)"}}>
              <div style={{fontWeight:700,color:T.text,marginBottom:9}}>📊 Base de Datos</div>
              <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:9}}>
                {[["💊",MEDICATIONS.length,"Medicamentos"],["📂",CATEGORIES.length,"Categorías"],["🍶",MEDICATIONS.filter(m=>m.syrup).length,"Con jarabe"],["💧",MEDICATIONS.filter(m=>m.drops).length,"Con gotas"]].map(([ico,v,l])=>(
                  <div key={l} style={{background:dark?"#0f172a":"#f0f9ff",borderRadius:9,padding:"11px",textAlign:"center"}}>
                    <div style={{fontSize:18}}>{ico}</div>
                    <div style={{fontSize:21,fontWeight:800,color:"#0ea5e9"}}>{v}</div>
                    <div style={{fontSize:10,color:T.sub}}>{l}</div>
                  </div>
                ))}
              </div>
            </div>

            <div style={{background:dark?"#1f0a0a":"#fef2f2",borderRadius:12,padding:14,border:"1px solid #fca5a5"}}>
              <div style={{fontWeight:700,color:"#991b1b",marginBottom:6}}>⚕️ Aviso Médico</div>
              <div style={{fontSize:11,color:"#7f1d1d",lineHeight:1.6}}>Herramienta de apoyo para profesionales de salud. Las dosis son orientativas basadas en guías farmacológicas estándar. Confirme siempre con el médico tratante y las indicaciones del fabricante.</div>
            </div>
            <div style={{textAlign:"center",fontSize:10,color:T.mutedTxt}}>💊 Dosis Pediátrica v2.0</div>
          </div>
        )}
      </div>
    </div>
  );
}