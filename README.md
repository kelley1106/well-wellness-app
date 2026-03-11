import { useState, useEffect } from "react";

const LOGO_B64 = "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";

const ADMIN_PASSWORD = "well2024";

const DEFAULT_SUPPLEMENTS = [
  { id: 1, name: "Magnesium Glycinate", emoji: "🌙", tagline: "Sleep · Stress · Muscle", description: "Our #1 bestseller. Highly absorbable form supports deep sleep, muscle relaxation, and stress reduction.", badge: "Best Seller", badgeColor: "#7dd3c8", visible: true },
  { id: 2, name: "Vitamin D3 + K2", emoji: "☀️", tagline: "Immunity · Bones · Mood", description: "The essential pairing. D3 supports immunity and mood; K2 directs calcium to bones, not arteries.", badge: "Top Rated", badgeColor: "#e8c97a", visible: true },
  { id: 3, name: "Omega-3 Fish Oil", emoji: "🐟", tagline: "Heart · Brain · Inflammation", description: "Ultra-pure, third-party tested. Supports cardiovascular health, brain function, and whole-body inflammation.", badge: "Staff Pick", badgeColor: "#a78bfa", visible: true },
  { id: 4, name: "Ashwagandha KSM-66", emoji: "🌿", tagline: "Stress · Cortisol · Energy", description: "Clinically studied root extract that lowers cortisol, improves energy, and supports adrenal health.", badge: "Trending", badgeColor: "#f97316", visible: true },
  { id: 5, name: "Probiotic 50B CFU", emoji: "🦠", tagline: "Gut · Immunity · Mood", description: "25 diverse strains for a thriving microbiome. Supports digestion, immune function, and the gut-brain axis.", badge: "Popular", badgeColor: "#7dd3c8", visible: true },
  { id: 6, name: "B-Complex + Methylfolate", emoji: "⚡", tagline: "Energy · Nerves · Methylation", description: "Active, methylated B vitamins for sustained energy, nervous system health, and optimal cellular function.", badge: "Essential", badgeColor: "#e8c97a", visible: true },
  { id: 7, name: "Zinc + Copper Balance", emoji: "🛡️", tagline: "Immunity · Skin · Hormones", description: "Immune defense and hormonal balance in one. Includes copper to prevent depletion from zinc supplementation.", badge: "Popular", badgeColor: "#a78bfa", visible: true },
  { id: 8, name: "Collagen Peptides", emoji: "✨", tagline: "Skin · Joints · Hair", description: "Hydrolyzed types I & III for radiant skin, flexible joints, and stronger hair and nails.", badge: "Fan Fave", badgeColor: "#f97316", visible: true },
  { id: 9, name: "Creatine Monohydrate", emoji: "💪", tagline: "Strength · Power · Brain", description: "The most researched performance supplement. Builds strength, supports muscle recovery, and boosts cognitive energy.", badge: "Trending", badgeColor: "#7dd3c8", visible: true },
  { id: 10, name: "Alpha Lipoic Acid (ALA)", emoji: "🔋", tagline: "Antioxidant · Blood Sugar · Nerves", description: "Powerful universal antioxidant that supports insulin sensitivity, nerve health, and cellular energy production.", badge: "Clinical", badgeColor: "#e8c97a", visible: true },
  { id: 11, name: "Ascorbic Acid PureWay-C®", emoji: "🍊", tagline: "Immunity · Collagen · Antioxidant", description: "Advanced vitamin C with PureWay-C® technology for superior absorption and longer retention than standard ascorbic acid.", badge: "Premium", badgeColor: "#f97316", visible: true },
  { id: 12, name: "Niacinamide (Vitamin B3)", emoji: "🧬", tagline: "NAD+ · Skin · DNA Repair", description: "Boosts NAD+ levels for cellular energy, DNA repair, and longevity support. Also promotes clearer, healthier skin.", badge: "Anti-Aging", badgeColor: "#a78bfa", visible: true },
  { id: 13, name: "Women's Multivitamin", emoji: "🌸", tagline: "Hormones · Iron · Vitality", description: "Comprehensive formula with methylfolate, iron, and botanicals tailored to women's hormonal and nutritional needs.", badge: "For Her", badgeColor: "#f9a8d4", visible: true },
  { id: 14, name: "Men's Multivitamin", emoji: "🔵", tagline: "Energy · Prostate · Vitality", description: "Optimized blend with zinc, selenium, lycopene, and B vitamins designed for men's energy, heart, and prostate health.", badge: "For Him", badgeColor: "#60a5fa", visible: true },
  { id: 15, name: "CoQ10 (Ubiquinol)", emoji: "❤️", tagline: "Heart · Energy · Statin Support", description: "Active ubiquinol form for maximum absorption. Essential for heart health, cellular energy, and especially important for statin users.", badge: "Heart Health", badgeColor: "#f87171", visible: true }
];

const DEFAULT_AI_PROMPT = `You are a knowledgeable wellness advisor for "well | wellness from within," a premium supplement brand. Based on the following health intake, provide personalized supplement AND dietary recommendations.

Patient Profile:
- Age: {age}, Sex: {sex}
- Health Conditions: {conditions}
- Current Medications: {medications}
- Known Allergies/Sensitivities: {allergies}
- Health Goals: {goals}
- Current Diet: {diet}
- Smoking: {smoking}, Alcohol: {alcohol}
- Exercise: {exercise}, Stress Level: {stress}

Please provide:
1. A brief personalized wellness summary (2-3 sentences)
2. 4-6 specific supplement recommendations, each with name, why it's right for THIS person, dosage/timing, and any interaction cautions
3. Diet modifications tailored to their specific conditions and goals — include:
   - 3-5 foods/food groups to EMPHASIZE (with brief reason why for their conditions)
   - 3-5 foods/food groups to LIMIT OR AVOID (with brief reason why for their conditions)
   - 1-2 meal timing or eating pattern tips
4. 2-3 lifestyle tips tailored to their profile
5. A brief provider disclaimer

Format your response in clean JSON ONLY (no markdown, no backticks):
{
  "summary": "...",
  "supplements": [{ "name": "...", "reason": "...", "dosage": "...", "caution": "..." }],
  "diet": {
    "emphasize": [{ "food": "...", "reason": "..." }],
    "limit": [{ "food": "...", "reason": "..." }],
    "patterns": ["...", "..."]
  },
  "lifestyle_tips": ["...", "...", "..."],
  "disclaimer": "..."
}

Be specific, evidence-based, and compassionate. Flag serious interactions.`;

const healthConditions = [
  "Diabetes / Prediabetes","High Blood Pressure","High Cholesterol","Heart Disease","Thyroid Disorder",
  "Autoimmune Condition","Osteoporosis / Bone Loss","Anemia","Kidney Disease","Liver Disease",
  "GERD / Acid Reflux","IBS / Digestive Issues","Anxiety / Depression","Chronic Fatigue",
  "Arthritis / Joint Pain","Migraines / Headaches","Hormonal Imbalance","PCOS",
  "Menopause / Perimenopause","Cancer (current or history)"
];
const healthGoals = [
  "More energy & less fatigue","Better sleep","Reduce stress & anxiety","Improve gut & digestion",
  "Strengthen immune system","Support heart health","Improve brain & focus","Hormone balance",
  "Weight management","Stronger bones & joints","Healthier skin, hair & nails","Athletic performance & recovery"
];
const dietOptions = ["Omnivore (eat everything)","Vegetarian","Vegan","Keto / Low-carb","Gluten-free","Dairy-free"];
const BADGE_COLORS = ["#7dd3c8","#e8c97a","#a78bfa","#f97316","#f9a8d4","#60a5fa","#f87171","#86efac"];

// ─── SHARED STYLES ────────────────────────────────────────────────────────────
const T = "#7dd3c8";
const sharedStyles = {
  input: { width:"100%", padding:"11px 14px", background:"rgba(255,255,255,0.06)", border:"1px solid rgba(255,255,255,0.12)", borderRadius:8, color:"#fff", fontSize:14, fontFamily:"'Helvetica Neue',sans-serif", outline:"none", boxSizing:"border-box", marginBottom:12 },
  textarea: { width:"100%", padding:"11px 14px", background:"rgba(255,255,255,0.06)", border:"1px solid rgba(255,255,255,0.12)", borderRadius:8, color:"#fff", fontSize:13, fontFamily:"'Helvetica Neue',sans-serif", outline:"none", resize:"vertical", minHeight:80, boxSizing:"border-box", marginBottom:12 },
  btn: { background:T, color:"#0a0a0a", border:"none", borderRadius:8, padding:"12px 28px", fontSize:14, fontFamily:"'Helvetica Neue',sans-serif", fontWeight:"600", cursor:"pointer", letterSpacing:0.4 },
  btnSm: { background:T, color:"#0a0a0a", border:"none", borderRadius:6, padding:"7px 16px", fontSize:12, fontFamily:"'Helvetica Neue',sans-serif", fontWeight:"600", cursor:"pointer" },
  btnDanger: { background:"rgba(248,113,113,0.15)", color:"#f87171", border:"1px solid rgba(248,113,113,0.3)", borderRadius:6, padding:"7px 14px", fontSize:12, fontFamily:"'Helvetica Neue',sans-serif", cursor:"pointer" },
  btnGhost: { background:"transparent", color:"#888", border:"1px solid rgba(255,255,255,0.12)", borderRadius:8, padding:"11px 22px", fontSize:13, fontFamily:"'Helvetica Neue',sans-serif", cursor:"pointer" },
  label: { fontSize:12, fontFamily:"'Helvetica Neue',sans-serif", color:"#888", marginBottom:4, display:"block", letterSpacing:0.5, textTransform:"uppercase" },
  card: { background:"rgba(255,255,255,0.03)", border:"1px solid rgba(255,255,255,0.08)", borderRadius:12, padding:"18px 20px", marginBottom:12 },
  sectionTitle: { fontSize:10, letterSpacing:3, textTransform:"uppercase", color:T, fontFamily:"'Helvetica Neue',sans-serif", marginBottom:14 },
  divider: { height:1, background:"rgba(255,255,255,0.06)", margin:"24px 0" },
};

// ─── ADMIN DASHBOARD ──────────────────────────────────────────────────────────
function AdminDashboard({ onExit }) {
  const [tab, setTab] = useState("supplements");
  const [supplements, setSupplements] = useState([]);
  const [aiPrompt, setAiPrompt] = useState(DEFAULT_AI_PROMPT);
  const [responses, setResponses] = useState([]);
  const [editingId, setEditingId] = useState(null);
  const [editForm, setEditForm] = useState({});
  const [addingNew, setAddingNew] = useState(false);
  const [newSupp, setNewSupp] = useState({ name:"", emoji:"💊", tagline:"", description:"", badge:"New", badgeColor:"#7dd3c8", visible:true });
  const [saving, setSaving] = useState(false);
  const [saveMsg, setSaveMsg] = useState("");
  const [expandedResponse, setExpandedResponse] = useState(null);

  useEffect(() => {
    loadData();
  }, []);

  const loadData = async () => {
    try {
      const s = await window.storage.get("admin-supplements");
      setSupplements(s ? JSON.parse(s.value) : DEFAULT_SUPPLEMENTS);
    } catch { setSupplements(DEFAULT_SUPPLEMENTS); }
    try {
      const p = await window.storage.get("admin-ai-prompt");
      if (p) setAiPrompt(p.value);
    } catch {}
    try {
      const r = await window.storage.get("patient-responses");
      if (r) setResponses(JSON.parse(r.value));
    } catch { setResponses([]); }
  };

  const showSaved = (msg = "Saved!") => {
    setSaveMsg(msg);
    setTimeout(() => setSaveMsg(""), 2500);
  };

  const saveSupplements = async (updated) => {
    setSaving(true);
    try {
      await window.storage.set("admin-supplements", JSON.stringify(updated));
      setSupplements(updated);
      showSaved("Supplements saved ✓");
    } catch { showSaved("Save failed — try again"); }
    setSaving(false);
  };

  const savePrompt = async () => {
    setSaving(true);
    try {
      await window.storage.set("admin-ai-prompt", aiPrompt);
      showSaved("AI prompt saved ✓");
    } catch { showSaved("Save failed"); }
    setSaving(false);
  };

  const startEdit = (s) => { setEditingId(s.id); setEditForm({...s}); };
  const cancelEdit = () => { setEditingId(null); setEditForm({}); };

  const saveEdit = () => {
    const updated = supplements.map(s => s.id === editingId ? { ...editForm } : s);
    saveSupplements(updated);
    setEditingId(null);
  };

  const toggleVisible = (id) => {
    const updated = supplements.map(s => s.id === id ? { ...s, visible: !s.visible } : s);
    saveSupplements(updated);
  };

  const deleteSupp = (id) => {
    if (!window.confirm("Delete this supplement?")) return;
    saveSupplements(supplements.filter(s => s.id !== id));
  };

  const addSupp = () => {
    const updated = [...supplements, { ...newSupp, id: Date.now() }];
    saveSupplements(updated);
    setAddingNew(false);
    setNewSupp({ name:"", emoji:"💊", tagline:"", description:"", badge:"New", badgeColor:"#7dd3c8", visible:true });
  };

  const clearResponses = async () => {
    if (!window.confirm("Delete all patient responses? This cannot be undone.")) return;
    await window.storage.set("patient-responses", JSON.stringify([]));
    setResponses([]);
  };

  const tabs = [
    { id:"supplements", label:"💊 Supplements", count: supplements.length },
    { id:"prompt", label:"🤖 AI Prompt" },
    { id:"responses", label:"📋 Patient Responses", count: responses.length },
  ];

  return (
    <div style={{ minHeight:"100vh", background:"#0a0a0a", color:"#e8e8e8", fontFamily:"'Georgia',serif" }}>
      {/* Top Bar */}
      <div style={{ background:"rgba(255,255,255,0.03)", borderBottom:"1px solid rgba(125,211,200,0.2)", padding:"14px 24px", display:"flex", justifyContent:"space-between", alignItems:"center" }}>
        <div style={{ display:"flex", alignItems:"center", gap:16 }}>
          <span style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, fontFamily:"'Helvetica Neue',sans-serif" }}>well · Admin</span>
          {saveMsg && <span style={{ fontSize:12, color:"#86efac", fontFamily:"'Helvetica Neue',sans-serif" }}>{saveMsg}</span>}
        </div>
        <button style={{...sharedStyles.btnGhost, padding:"8px 18px", fontSize:12}} onClick={onExit}>← Back to App</button>
      </div>

      <div style={{ maxWidth:860, margin:"0 auto", padding:"24px 20px" }}>
        {/* Tabs */}
        <div style={{ display:"flex", gap:8, marginBottom:28, flexWrap:"wrap" }}>
          {tabs.map(t => (
            <button key={t.id} onClick={() => setTab(t.id)} style={{
              padding:"10px 20px", borderRadius:8, fontSize:13,
              fontFamily:"'Helvetica Neue',sans-serif", cursor:"pointer", border:"none",
              background: tab===t.id ? T : "rgba(255,255,255,0.06)",
              color: tab===t.id ? "#0a0a0a" : "#aaa",
              fontWeight: tab===t.id ? "600" : "400"
            }}>
              {t.label}{t.count !== undefined ? ` (${t.count})` : ""}
            </button>
          ))}
        </div>

        {/* ── SUPPLEMENTS TAB ── */}
        {tab === "supplements" && (
          <div>
            <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", marginBottom:20 }}>
              <div>
                <div style={sharedStyles.sectionTitle}>Supplement Catalog</div>
                <p style={{ fontSize:13, color:"#666", fontFamily:"'Helvetica Neue',sans-serif", margin:0 }}>
                  {supplements.filter(s=>s.visible).length} visible · {supplements.filter(s=>!s.visible).length} hidden
                </p>
              </div>
              <button style={sharedStyles.btnSm} onClick={() => setAddingNew(true)}>+ Add New</button>
            </div>

            {/* Add New Form */}
            {addingNew && (
              <div style={{ ...sharedStyles.card, border:"1px solid rgba(125,211,200,0.3)", marginBottom:20 }}>
                <div style={{...sharedStyles.sectionTitle, color:"#86efac"}}>New Supplement</div>
                <div style={{ display:"grid", gridTemplateColumns:"80px 1fr 1fr", gap:10, marginBottom:10 }}>
                  <div><label style={sharedStyles.label}>Emoji</label><input style={sharedStyles.input} value={newSupp.emoji} onChange={e=>setNewSupp({...newSupp,emoji:e.target.value})} /></div>
                  <div><label style={sharedStyles.label}>Name</label><input style={sharedStyles.input} placeholder="e.g. Berberine" value={newSupp.name} onChange={e=>setNewSupp({...newSupp,name:e.target.value})} /></div>
                  <div><label style={sharedStyles.label}>Tagline</label><input style={sharedStyles.input} placeholder="e.g. Blood Sugar · Weight" value={newSupp.tagline} onChange={e=>setNewSupp({...newSupp,tagline:e.target.value})} /></div>
                </div>
                <div style={{ marginBottom:10 }}>
                  <label style={sharedStyles.label}>Description</label>
                  <textarea style={sharedStyles.textarea} placeholder="What does it do? Who is it for?" value={newSupp.description} onChange={e=>setNewSupp({...newSupp,description:e.target.value})} />
                </div>
                <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:10, marginBottom:16 }}>
                  <div><label style={sharedStyles.label}>Badge Label</label><input style={sharedStyles.input} placeholder="e.g. New, Clinical, Popular" value={newSupp.badge} onChange={e=>setNewSupp({...newSupp,badge:e.target.value})} /></div>
                  <div>
                    <label style={sharedStyles.label}>Badge Color</label>
                    <div style={{ display:"flex", gap:8, flexWrap:"wrap", paddingTop:4 }}>
                      {BADGE_COLORS.map(c => (
                        <div key={c} onClick={() => setNewSupp({...newSupp,badgeColor:c})} style={{ width:24, height:24, borderRadius:"50%", background:c, cursor:"pointer", border: newSupp.badgeColor===c ? "2px solid #fff" : "2px solid transparent" }} />
                      ))}
                    </div>
                  </div>
                </div>
                <div style={{ display:"flex", gap:10 }}>
                  <button style={sharedStyles.btnSm} onClick={addSupp} disabled={!newSupp.name}>Add Supplement</button>
                  <button style={sharedStyles.btnGhost} onClick={() => setAddingNew(false)}>Cancel</button>
                </div>
              </div>
            )}

            {/* Supplement List */}
            {supplements.map(s => (
              <div key={s.id} style={{ ...sharedStyles.card, opacity: s.visible ? 1 : 0.45 }}>
                {editingId === s.id ? (
                  // Edit Mode
                  <div>
                    <div style={{ display:"grid", gridTemplateColumns:"70px 1fr 1fr", gap:10, marginBottom:10 }}>
                      <div><label style={sharedStyles.label}>Emoji</label><input style={sharedStyles.input} value={editForm.emoji} onChange={e=>setEditForm({...editForm,emoji:e.target.value})} /></div>
                      <div><label style={sharedStyles.label}>Name</label><input style={sharedStyles.input} value={editForm.name} onChange={e=>setEditForm({...editForm,name:e.target.value})} /></div>
                      <div><label style={sharedStyles.label}>Tagline</label><input style={sharedStyles.input} value={editForm.tagline} onChange={e=>setEditForm({...editForm,tagline:e.target.value})} /></div>
                    </div>
                    <div style={{ marginBottom:10 }}>
                      <label style={sharedStyles.label}>Description</label>
                      <textarea style={sharedStyles.textarea} value={editForm.description} onChange={e=>setEditForm({...editForm,description:e.target.value})} />
                    </div>
                    <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:10, marginBottom:14 }}>
                      <div><label style={sharedStyles.label}>Badge Label</label><input style={sharedStyles.input} value={editForm.badge} onChange={e=>setEditForm({...editForm,badge:e.target.value})} /></div>
                      <div>
                        <label style={sharedStyles.label}>Badge Color</label>
                        <div style={{ display:"flex", gap:8, flexWrap:"wrap", paddingTop:6 }}>
                          {BADGE_COLORS.map(c => (
                            <div key={c} onClick={() => setEditForm({...editForm,badgeColor:c})} style={{ width:22, height:22, borderRadius:"50%", background:c, cursor:"pointer", border: editForm.badgeColor===c ? "2px solid #fff" : "2px solid transparent" }} />
                          ))}
                        </div>
                      </div>
                    </div>
                    <div style={{ display:"flex", gap:10 }}>
                      <button style={sharedStyles.btnSm} onClick={saveEdit}>Save Changes</button>
                      <button style={sharedStyles.btnGhost} onClick={cancelEdit}>Cancel</button>
                    </div>
                  </div>
                ) : (
                  // View Mode
                  <div style={{ display:"flex", gap:14, alignItems:"flex-start" }}>
                    <span style={{ fontSize:26, flexShrink:0 }}>{s.emoji}</span>
                    <div style={{ flex:1, minWidth:0 }}>
                      <div style={{ display:"flex", alignItems:"center", gap:8, marginBottom:3, flexWrap:"wrap" }}>
                        <span style={{ fontSize:14, color:"#ddd" }}>{s.name}</span>
                        <span style={{ fontSize:9, padding:"2px 8px", borderRadius:8, background:s.badgeColor+"22", color:s.badgeColor, fontFamily:"'Helvetica Neue',sans-serif", letterSpacing:1, textTransform:"uppercase" }}>{s.badge}</span>
                        {!s.visible && <span style={{ fontSize:9, padding:"2px 8px", borderRadius:8, background:"rgba(255,255,255,0.08)", color:"#666", fontFamily:"'Helvetica Neue',sans-serif" }}>HIDDEN</span>}
                      </div>
                      <div style={{ fontSize:11, color:T, fontFamily:"'Helvetica Neue',sans-serif", letterSpacing:1, marginBottom:4 }}>{s.tagline}</div>
                      <div style={{ fontSize:12, color:"#666", fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.5 }}>{s.description}</div>
                    </div>
                    <div style={{ display:"flex", gap:8, flexShrink:0, flexWrap:"wrap", justifyContent:"flex-end" }}>
                      <button style={sharedStyles.btnSm} onClick={() => startEdit(s)}>Edit</button>
                      <button style={{ ...sharedStyles.btnGhost, padding:"7px 14px", fontSize:12 }} onClick={() => toggleVisible(s.id)}>
                        {s.visible ? "Hide" : "Show"}
                      </button>
                      <button style={sharedStyles.btnDanger} onClick={() => deleteSupp(s.id)}>Delete</button>
                    </div>
                  </div>
                )}
              </div>
            ))}
          </div>
        )}

        {/* ── AI PROMPT TAB ── */}
        {tab === "prompt" && (
          <div>
            <div style={sharedStyles.sectionTitle}>AI Recommendation Prompt</div>
            <p style={{ fontSize:13, color:"#666", fontFamily:"'Helvetica Neue',sans-serif", marginBottom:20, lineHeight:1.7 }}>
              This is the instruction set sent to the AI for every patient. The placeholders in curly braces (like <span style={{color:T}}>{"{age}"}</span>, <span style={{color:T}}>{"{conditions}"}</span>) are automatically filled in with the patient's answers. Edit the tone, add requirements, or adjust what sections the AI returns.
            </p>

            <div style={{ background:"rgba(125,211,200,0.05)", border:"1px solid rgba(125,211,200,0.15)", borderRadius:10, padding:"14px 16px", marginBottom:16, fontSize:12, fontFamily:"'Helvetica Neue',sans-serif", color:"#888", lineHeight:1.8 }}>
              <strong style={{color:T}}>Available placeholders:</strong>{" "}
              {["{age}","{sex}","{conditions}","{medications}","{allergies}","{goals}","{diet}","{smoking}","{alcohol}","{exercise}","{stress}"].map(p => (
                <span key={p} style={{color:T, marginRight:8}}>{p}</span>
              ))}
            </div>

            <textarea
              style={{ ...sharedStyles.textarea, minHeight:440, fontSize:13, lineHeight:1.7, fontFamily:"monospace" }}
              value={aiPrompt}
              onChange={e => setAiPrompt(e.target.value)}
            />
            <div style={{ display:"flex", gap:12, alignItems:"center" }}>
              <button style={sharedStyles.btn} onClick={savePrompt} disabled={saving}>
                {saving ? "Saving..." : "Save Prompt"}
              </button>
              <button style={sharedStyles.btnGhost} onClick={() => { setAiPrompt(DEFAULT_AI_PROMPT); }}>Reset to Default</button>
            </div>
          </div>
        )}

        {/* ── PATIENT RESPONSES TAB ── */}
        {tab === "responses" && (
          <div>
            <div style={{ display:"flex", justifyContent:"space-between", alignItems:"flex-start", marginBottom:20 }}>
              <div>
                <div style={sharedStyles.sectionTitle}>Patient Quiz Responses</div>
                <p style={{ fontSize:13, color:"#666", fontFamily:"'Helvetica Neue',sans-serif", margin:0 }}>
                  {responses.length} total submissions
                </p>
              </div>
              {responses.length > 0 && (
                <button style={sharedStyles.btnDanger} onClick={clearResponses}>Clear All</button>
              )}
            </div>

            {responses.length === 0 ? (
              <div style={{ textAlign:"center", padding:"48px 0", color:"#444", fontFamily:"'Helvetica Neue',sans-serif", fontSize:14 }}>
                No patient responses yet. They'll appear here after patients complete the quiz.
              </div>
            ) : (
              [...responses].reverse().map((r, i) => (
                <div key={i} style={sharedStyles.card}>
                  <div style={{ display:"flex", justifyContent:"space-between", alignItems:"flex-start", cursor:"pointer" }} onClick={() => setExpandedResponse(expandedResponse===i ? null : i)}>
                    <div>
                      <div style={{ fontSize:14, color:"#ddd", marginBottom:4 }}>
                        {r.sex || "—"}, age {r.age || "—"}
                        {r.conditions?.length > 0 && <span style={{ color:"#666", fontSize:12 }}> · {r.conditions.slice(0,2).join(", ")}{r.conditions.length>2 ? ` +${r.conditions.length-2}` : ""}</span>}
                      </div>
                      <div style={{ fontSize:11, color:"#555", fontFamily:"'Helvetica Neue',sans-serif" }}>
                        {new Date(r.timestamp).toLocaleString()}
                      </div>
                    </div>
                    <span style={{ color:T, fontSize:16, transform: expandedResponse===i ? "rotate(180deg)" : "none", transition:"0.2s" }}>▾</span>
                  </div>

                  {expandedResponse === i && (
                    <div style={{ marginTop:16, borderTop:"1px solid rgba(255,255,255,0.06)", paddingTop:16 }}>
                      {[
                        ["Age", r.age], ["Sex", r.sex], ["Diet", r.diet?.join(", ")],
                        ["Conditions", r.conditions?.join(", ")],
                        ["Medications", r.medications],
                        ["Allergies", r.allergies],
                        ["Goals", r.goals?.join(", ")],
                        ["Exercise", r.exercise], ["Stress", r.stress],
                        ["Alcohol", r.alcohol], ["Smoking", r.smoking],
                        ["Extra concerns", r.extraConcerns],
                        ["Current supplements", r.currentSupps],
                      ].filter(([,v]) => v).map(([label, val]) => (
                        <div key={label} style={{ display:"flex", gap:12, marginBottom:8, fontFamily:"'Helvetica Neue',sans-serif" }}>
                          <span style={{ fontSize:11, color:"#555", minWidth:130, flexShrink:0, textTransform:"uppercase", letterSpacing:0.5, paddingTop:1 }}>{label}</span>
                          <span style={{ fontSize:13, color:"#bbb", lineHeight:1.5 }}>{val}</span>
                        </div>
                      ))}
                    </div>
                  )}
                </div>
              ))
            )}
          </div>
        )}
      </div>
    </div>
  );
}

// ─── PATIENT APP ──────────────────────────────────────────────────────────────
export default function WellApp() {
  const [mode, setMode] = useState("patient"); // "patient" | "adminLogin" | "admin"
  const [adminPw, setAdminPw] = useState("");
  const [adminError, setAdminError] = useState("");
  const [step, setStep] = useState(0);
  const [form, setForm] = useState({ age:"", sex:"", conditions:[], medications:"", allergies:"", concerns:[], goals:[], diet:[], smoking:"", alcohol:"", exercise:"", stress:"", extraConcerns:"", currentSupps:"" });
  const [loading, setLoading] = useState(false);
  const [result, setResult] = useState(null);
  const [animIn, setAnimIn] = useState(true);
  const [supplements, setSupplements] = useState(DEFAULT_SUPPLEMENTS);
  const [aiPrompt, setAiPrompt] = useState(DEFAULT_AI_PROMPT);

  useEffect(() => {
    loadConfig();
  }, []);

  const loadConfig = async () => {
    try {
      const s = await window.storage.get("admin-supplements");
      if (s) setSupplements(JSON.parse(s.value));
    } catch {}
    try {
      const p = await window.storage.get("admin-ai-prompt");
      if (p) setAiPrompt(p.value);
    } catch {}
  };

  const saveResponse = async (f) => {
    try {
      const existing = await window.storage.get("patient-responses");
      const arr = existing ? JSON.parse(existing.value) : [];
      arr.push({ ...f, timestamp: Date.now() });
      await window.storage.set("patient-responses", JSON.stringify(arr));
    } catch {}
  };

  const goTo = (next) => {
    setAnimIn(false);
    setTimeout(() => { setStep(next); setAnimIn(true); }, 260);
  };

  const toggle = (field, val) => {
    setForm(f => ({ ...f, [field]: f[field].includes(val) ? f[field].filter(x => x !== val) : [...f[field], val] }));
  };

  const handleSubmit = async () => {
    goTo(6);
    setLoading(true);
    saveResponse(form);
    const filled = aiPrompt
      .replace("{age}", form.age || "Not specified")
      .replace("{sex}", form.sex || "Not specified")
      .replace("{conditions}", form.conditions.join(", ") || "None reported")
      .replace("{medications}", form.medications || "None")
      .replace("{allergies}", form.allergies || "None")
      .replace("{goals}", form.goals.join(", ") || "General wellness")
      .replace("{diet}", form.diet.join(", ") || "Not specified")
      .replace("{smoking}", form.smoking || "Not specified")
      .replace("{alcohol}", form.alcohol || "Not specified")
      .replace("{exercise}", form.exercise || "Not specified")
      .replace("{stress}", form.stress || "Not specified");

    try {
      const response = await fetch("https://api.anthropic.com/v1/messages", {
        method:"POST",
        headers:{"Content-Type":"application/json"},
        body:JSON.stringify({ model:"claude-sonnet-4-20250514", max_tokens:1500, messages:[{ role:"user", content:filled }] })
      });
      const data = await response.json();
      const text = data.content.map(i => i.text||"").join("");
      const clean = text.replace(/```json|```/g,"").trim();
      setResult(JSON.parse(clean));
    } catch { setResult({ error:"Something went wrong. Please try again." }); }
    setLoading(false);
  };

  const loginAdmin = () => {
    if (adminPw === ADMIN_PASSWORD) { setMode("admin"); setAdminError(""); }
    else { setAdminError("Incorrect password"); }
  };

  if (mode === "admin") return <AdminDashboard onExit={() => { setMode("patient"); loadConfig(); }} />;

  if (mode === "adminLogin") return (
    <div style={{ minHeight:"100vh", background:"#0a0a0a", display:"flex", alignItems:"center", justifyContent:"center", padding:24 }}>
      <div style={{ width:"100%", maxWidth:380, background:"rgba(255,255,255,0.04)", border:"1px solid rgba(125,211,200,0.2)", borderRadius:16, padding:"36px 32px" }}>
        <div style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, fontFamily:"'Helvetica Neue',sans-serif", marginBottom:8 }}>Admin Access</div>
        <div style={{ fontSize:22, color:"#fff", marginBottom:6 }}>Staff Login</div>
        <p style={{ fontSize:13, color:"#666", fontFamily:"'Helvetica Neue',sans-serif", marginBottom:24, lineHeight:1.6 }}>Enter your admin password to manage supplements, settings, and view patient responses.</p>
        <label style={sharedStyles.label}>Password</label>
        <input type="password" style={{ ...sharedStyles.input, marginBottom:8 }} value={adminPw} onChange={e => setAdminPw(e.target.value)} onKeyDown={e => e.key==="Enter" && loginAdmin()} placeholder="Enter admin password" />
        {adminError && <div style={{ color:"#f87171", fontSize:12, fontFamily:"'Helvetica Neue',sans-serif", marginBottom:12 }}>{adminError}</div>}
        <div style={{ display:"flex", gap:10, marginTop:8 }}>
          <button style={sharedStyles.btn} onClick={loginAdmin}>Login →</button>
          <button style={sharedStyles.btnGhost} onClick={() => { setMode("patient"); setAdminPw(""); setAdminError(""); }}>Cancel</button>
        </div>
      </div>
    </div>
  );

  // ── PATIENT UI ────────────────────────────────────────────────────────────
  const visibleSupps = supplements.filter(s => s.visible);

  const chip = (active) => ({
    display:"inline-block", padding:"8px 14px", borderRadius:20, fontSize:13,
    fontFamily:"'Helvetica Neue',sans-serif", cursor:"pointer", margin:"4px",
    transition:"all 0.18s",
    background: active ? T : "rgba(255,255,255,0.06)",
    color: active ? "#0a0a0a" : "#ccc",
    border: active ? `1px solid ${T}` : "1px solid rgba(255,255,255,0.1)",
    fontWeight: active ? "600" : "400"
  });

  const card = {
    width:"100%", maxWidth:680, background:"rgba(255,255,255,0.04)",
    border:"1px solid rgba(125,211,200,0.18)", borderRadius:20,
    padding:"32px 36px", marginTop:16,
    transition:"opacity 0.26s, transform 0.26s",
    opacity: animIn ? 1 : 0,
    transform: animIn ? "translateY(0)" : "translateY(10px)"
  };

  const progressSteps = ["Profile","History","Meds","Goals","Lifestyle","Results"];

  const SupplGrid = ({ size = "full" }) => (
    <div style={{ display:"grid", gridTemplateColumns: size==="sm" ? "1fr 1fr" : "1fr 1fr", gap:10 }}>
      {visibleSupps.map(s => (
        <div key={s.id} style={{ background:"rgba(255,255,255,0.03)", border:"1px solid rgba(255,255,255,0.08)", borderRadius:12, padding:"14px" }}>
          <div style={{ display:"flex", justifyContent:"space-between", alignItems:"flex-start", marginBottom:8 }}>
            <span style={{ fontSize:20 }}>{s.emoji}</span>
            <span style={{ fontSize:9, padding:"2px 8px", borderRadius:8, background:s.badgeColor+"22", color:s.badgeColor, fontFamily:"'Helvetica Neue',sans-serif", letterSpacing:1, textTransform:"uppercase" }}>{s.badge}</span>
          </div>
          <div style={{ fontSize:13, color:"#ddd", marginBottom:2 }}>{s.name}</div>
          <div style={{ fontSize:10, color:T, fontFamily:"'Helvetica Neue',sans-serif", letterSpacing:1, marginBottom:5 }}>{s.tagline}</div>
          <div style={{ fontSize:11, color:"#666", fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.5 }}>{s.description}</div>
        </div>
      ))}
    </div>
  );

  return (
    <div style={{ minHeight:"100vh", background:"linear-gradient(135deg,#0a0a0a 0%,#111 50%,#0d1a17 100%)", fontFamily:"'Georgia',serif", color:"#e8e8e8", display:"flex", flexDirection:"column", alignItems:"center", padding:"0 16px 40px" }}>
      {/* Header */}
      <div style={{ width:"100%", maxWidth:680, paddingTop:28, paddingBottom:4, display:"flex", flexDirection:"column", alignItems:"center" }}>
        <img src={`data:image/png;base64,${LOGO_B64}`} alt="well" style={{ width:170, marginBottom:4, filter:"brightness(1.1)" }} />
      </div>

      {/* Progress */}
      {step > 0 && step < 6 && (
        <div style={{ width:"100%", maxWidth:680, marginTop:16, display:"flex", gap:5 }}>
          {progressSteps.map((_, i) => (
            <div key={i} style={{ height:3, flex:1, borderRadius:2, background: step>i ? T : (step===i ? "rgba(125,211,200,0.4)" : "rgba(255,255,255,0.08)") }} />
          ))}
        </div>
      )}

      <div style={card}>

        {/* WELCOME */}
        {step === 0 && (
          <div>
            <div style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, marginBottom:8, fontFamily:"'Helvetica Neue',sans-serif" }}>Personalized Wellness</div>
            <h2 style={{ fontSize:24, fontWeight:"normal", color:"#fff", marginBottom:6, lineHeight:1.3 }}>Your supplement journey<br />starts here.</h2>
            <p style={{ fontSize:14, color:"#9a9a9a", marginBottom:28, fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.6 }}>
              Answer a few questions about your health history, medications, and goals. Our AI advisor creates a personalized supplement protocol just for you.
            </p>
            <button style={sharedStyles.btn} onClick={() => goTo(1)}>Begin Your Assessment →</button>

            <div style={sharedStyles.divider} />
            <div style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, marginBottom:18, fontFamily:"'Helvetica Neue',sans-serif" }}>Our Supplement Catalog</div>
            <SupplGrid />
            <div style={{ marginTop:20, textAlign:"center" }}>
              <button style={sharedStyles.btn} onClick={() => goTo(1)}>Get My Personalized Protocol →</button>
            </div>
          </div>
        )}

        {/* DEMOGRAPHICS */}
        {step === 1 && (
          <div>
            <div style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, marginBottom:8, fontFamily:"'Helvetica Neue',sans-serif" }}>Step 1 of 5 · Profile</div>
            <h2 style={{ fontSize:24, fontWeight:"normal", color:"#fff", marginBottom:6 }}>Tell us about yourself</h2>
            <p style={{ fontSize:14, color:"#9a9a9a", marginBottom:24, fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.6 }}>Basic information helps us tailor recommendations to your age and biology.</p>
            <label style={sharedStyles.label}>Age</label>
            <input style={sharedStyles.input} type="number" placeholder="e.g. 42" value={form.age} onChange={e => setForm({...form,age:e.target.value})} />
            <label style={sharedStyles.label}>Biological Sex</label>
            <div style={{ marginBottom:18 }}>{["Female","Male","Prefer not to say"].map(s => <span key={s} style={chip(form.sex===s)} onClick={() => setForm({...form,sex:s})}>{s}</span>)}</div>
            <label style={sharedStyles.label}>Dietary Pattern</label>
            <div style={{ marginBottom:24 }}>{dietOptions.map(d => <span key={d} style={chip(form.diet.includes(d))} onClick={() => toggle("diet",d)}>{d}</span>)}</div>
            <div style={{ display:"flex", justifyContent:"space-between" }}>
              <button style={sharedStyles.btnGhost} onClick={() => goTo(0)}>← Back</button>
              <button style={sharedStyles.btn} onClick={() => goTo(2)}>Continue →</button>
            </div>
          </div>
        )}

        {/* HEALTH HISTORY */}
        {step === 2 && (
          <div>
            <div style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, marginBottom:8, fontFamily:"'Helvetica Neue',sans-serif" }}>Step 2 of 5 · Health History</div>
            <h2 style={{ fontSize:24, fontWeight:"normal", color:"#fff", marginBottom:6 }}>Any existing health conditions?</h2>
            <p style={{ fontSize:14, color:"#9a9a9a", marginBottom:24, fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.6 }}>Select all that apply. This helps us avoid contraindications and target your needs.</p>
            <div style={{ marginBottom:20 }}>{healthConditions.map(c => <span key={c} style={chip(form.conditions.includes(c))} onClick={() => toggle("conditions",c)}>{c}</span>)}</div>
            <label style={sharedStyles.label}>Known allergies or sensitivities</label>
            <textarea style={sharedStyles.textarea} placeholder="e.g. shellfish, soy, fish oil..." value={form.allergies} onChange={e => setForm({...form,allergies:e.target.value})} />
            <div style={{ display:"flex", justifyContent:"space-between" }}>
              <button style={sharedStyles.btnGhost} onClick={() => goTo(1)}>← Back</button>
              <button style={sharedStyles.btn} onClick={() => goTo(3)}>Continue →</button>
            </div>
          </div>
        )}

        {/* MEDICATIONS */}
        {step === 3 && (
          <div>
            <div style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, marginBottom:8, fontFamily:"'Helvetica Neue',sans-serif" }}>Step 3 of 5 · Medications</div>
            <h2 style={{ fontSize:24, fontWeight:"normal", color:"#fff", marginBottom:6 }}>Current medications & supplements</h2>
            <p style={{ fontSize:14, color:"#9a9a9a", marginBottom:24, fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.6 }}>This is the most important section — some supplements interact with medications. Be as specific as possible.</p>
            <label style={sharedStyles.label}>Prescription Medications</label>
            <textarea style={sharedStyles.textarea} placeholder="e.g. Metformin 500mg, Lisinopril 10mg, Warfarin 5mg..." value={form.medications} onChange={e => setForm({...form,medications:e.target.value})} />
            <label style={sharedStyles.label}>Supplements Currently Taking</label>
            <textarea style={{ ...sharedStyles.textarea, minHeight:70 }} placeholder="e.g. Vitamin D3 2000IU, Fish Oil 1g..." value={form.currentSupps} onChange={e => setForm({...form,currentSupps:e.target.value})} />
            <div style={{ display:"flex", justifyContent:"space-between" }}>
              <button style={sharedStyles.btnGhost} onClick={() => goTo(2)}>← Back</button>
              <button style={sharedStyles.btn} onClick={() => goTo(4)}>Continue →</button>
            </div>
          </div>
        )}

        {/* GOALS */}
        {step === 4 && (
          <div>
            <div style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, marginBottom:8, fontFamily:"'Helvetica Neue',sans-serif" }}>Step 4 of 5 · Goals</div>
            <h2 style={{ fontSize:24, fontWeight:"normal", color:"#fff", marginBottom:6 }}>What are you hoping to improve?</h2>
            <p style={{ fontSize:14, color:"#9a9a9a", marginBottom:24, fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.6 }}>Select everything that resonates. More detail = better recommendations.</p>
            <div style={{ marginBottom:20 }}>{healthGoals.map(g => <span key={g} style={chip(form.goals.includes(g))} onClick={() => toggle("goals",g)}>{g}</span>)}</div>
            <label style={sharedStyles.label}>Anything else? (symptoms, recent labs, specific concerns)</label>
            <textarea style={sharedStyles.textarea} placeholder="e.g. My ferritin has been low, doctor mentioned Vitamin D deficiency..." value={form.extraConcerns} onChange={e => setForm({...form,extraConcerns:e.target.value})} />
            <div style={{ display:"flex", justifyContent:"space-between" }}>
              <button style={sharedStyles.btnGhost} onClick={() => goTo(3)}>← Back</button>
              <button style={sharedStyles.btn} onClick={() => goTo(5)}>Continue →</button>
            </div>
          </div>
        )}

        {/* LIFESTYLE */}
        {step === 5 && (
          <div>
            <div style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, marginBottom:8, fontFamily:"'Helvetica Neue',sans-serif" }}>Step 5 of 5 · Lifestyle</div>
            <h2 style={{ fontSize:24, fontWeight:"normal", color:"#fff", marginBottom:6 }}>A little about your daily life</h2>
            <p style={{ fontSize:14, color:"#9a9a9a", marginBottom:24, fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.6 }}>Lifestyle factors directly influence which supplements your body needs most.</p>
            <label style={sharedStyles.label}>Exercise Frequency</label>
            <div style={{ marginBottom:18 }}>{["Sedentary","Light (1-2x/week)","Moderate (3-4x/week)","Active (5+/week)","Athlete"].map(e => <span key={e} style={chip(form.exercise===e)} onClick={() => setForm({...form,exercise:e})}>{e}</span>)}</div>
            <label style={sharedStyles.label}>Stress Level</label>
            <div style={{ marginBottom:18 }}>{["Low","Moderate","High","Very high"].map(s => <span key={s} style={chip(form.stress===s)} onClick={() => setForm({...form,stress:s})}>{s}</span>)}</div>
            <label style={sharedStyles.label}>Alcohol Consumption</label>
            <div style={{ marginBottom:18 }}>{["None","Occasional","Moderate (weekly)","Regular"].map(a => <span key={a} style={chip(form.alcohol===a)} onClick={() => setForm({...form,alcohol:a})}>{a}</span>)}</div>
            <label style={sharedStyles.label}>Smoking / Tobacco</label>
            <div style={{ marginBottom:28 }}>{["Non-smoker","Former smoker","Current smoker"].map(s => <span key={s} style={chip(form.smoking===s)} onClick={() => setForm({...form,smoking:s})}>{s}</span>)}</div>
            <div style={{ display:"flex", justifyContent:"space-between" }}>
              <button style={sharedStyles.btnGhost} onClick={() => goTo(4)}>← Back</button>
              <button style={{ ...sharedStyles.btn, padding:"14px 36px" }} onClick={handleSubmit}>Get My Recommendations ✦</button>
            </div>
          </div>
        )}

        {/* RESULTS */}
        {step === 6 && (
          <div>
            {loading ? (
              <div style={{ textAlign:"center", padding:"44px 0" }}>
                <div style={{ fontSize:26, marginBottom:14 }}>✦</div>
                <div style={{ fontSize:15, color:T, fontFamily:"'Helvetica Neue',sans-serif", marginBottom:6 }}>Analyzing your profile...</div>
                <div style={{ fontSize:12, color:"#555", fontFamily:"'Helvetica Neue',sans-serif" }}>Reviewing health history, medications & goals</div>
              </div>
            ) : result?.error ? (
              <div>
                <p style={{ color:"#f87171" }}>{result.error}</p>
                <button style={sharedStyles.btn} onClick={() => goTo(5)}>← Try Again</button>
              </div>
            ) : result ? (
              <div>
                <div style={{ fontSize:11, letterSpacing:3, textTransform:"uppercase", color:T, marginBottom:8, fontFamily:"'Helvetica Neue',sans-serif" }}>Your Personalized Protocol</div>
                <h2 style={{ fontSize:24, fontWeight:"normal", color:"#fff", marginBottom:6 }}>Wellness recommendations<br />crafted for you</h2>

                {/* Summary */}
                <div style={{ background:"rgba(125,211,200,0.07)", border:"1px solid rgba(125,211,200,0.2)", borderRadius:12, padding:"15px 18px", marginBottom:24, fontSize:14, fontFamily:"'Helvetica Neue',sans-serif", color:"#ccc", lineHeight:1.7 }}>
                  {result.summary}
                </div>

                {/* Supplements */}
                <div style={{ fontSize:11, letterSpacing:2, textTransform:"uppercase", color:T, marginBottom:14, fontFamily:"'Helvetica Neue',sans-serif" }}>Recommended Supplements</div>
                {result.supplements?.map((s,i) => (
                  <div key={i} style={{ background:"rgba(125,211,200,0.05)", border:"1px solid rgba(125,211,200,0.18)", borderRadius:12, padding:"18px 20px", marginBottom:12 }}>
                    <div style={{ fontSize:16, color:T, marginBottom:5 }}>{s.name}</div>
                    <div style={{ fontSize:13, color:"#aaa", lineHeight:1.6, marginBottom:6, fontFamily:"'Helvetica Neue',sans-serif" }}><strong style={{color:"#ddd"}}>Why for you: </strong>{s.reason}</div>
                    <div style={{ fontSize:12, fontFamily:"'Helvetica Neue',sans-serif", color:"#888", marginBottom: s.caution ? 6 : 0 }}>
                      <span style={{ display:"inline-block", fontSize:10, padding:"2px 10px", borderRadius:8, background:T+"22", color:T, marginRight:6 }}>Dosage</span>{s.dosage}
                    </div>
                    {s.caution && <div style={{ fontSize:12, fontFamily:"'Helvetica Neue',sans-serif", color:"#e8c97a" }}><span style={{ display:"inline-block", fontSize:10, padding:"2px 10px", borderRadius:8, background:"#e8c97a22", color:"#e8c97a", marginRight:6 }}>Note</span>{s.caution}</div>}
                  </div>
                ))}

                {/* Diet */}
                {result.diet && (
                  <>
                    <div style={sharedStyles.divider} />
                    <div style={{ fontSize:11, letterSpacing:2, textTransform:"uppercase", color:"#86efac", marginBottom:6, fontFamily:"'Helvetica Neue',sans-serif" }}>Diet Modifications</div>
                    <p style={{ fontSize:12, color:"#555", fontFamily:"'Helvetica Neue',sans-serif", marginBottom:16, lineHeight:1.6 }}>Targeted nutrition changes to amplify your supplement protocol.</p>

                    {result.diet.emphasize?.length > 0 && (
                      <div style={{ background:"rgba(134,239,172,0.05)", border:"1px solid rgba(134,239,172,0.16)", borderRadius:12, padding:"18px 20px", marginBottom:12 }}>
                        <div style={{ fontSize:11, color:"#86efac", letterSpacing:1.5, textTransform:"uppercase", fontFamily:"'Helvetica Neue',sans-serif", marginBottom:12 }}>✅ Emphasize</div>
                        {result.diet.emphasize.map((item,i) => (
                          <div key={i} style={{ display:"flex", gap:10, marginBottom: i<result.diet.emphasize.length-1 ? 10 : 0, paddingBottom: i<result.diet.emphasize.length-1 ? 10 : 0, borderBottom: i<result.diet.emphasize.length-1 ? "1px solid rgba(255,255,255,0.04)" : "none" }}>
                            <span style={{ color:"#86efac", flexShrink:0 }}>+</span>
                            <div><div style={{ fontSize:13, color:"#ddd", fontFamily:"'Helvetica Neue',sans-serif", marginBottom:2 }}>{item.food}</div><div style={{ fontSize:11, color:"#666", fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.5 }}>{item.reason}</div></div>
                          </div>
                        ))}
                      </div>
                    )}

                    {result.diet.limit?.length > 0 && (
                      <div style={{ background:"rgba(251,191,36,0.05)", border:"1px solid rgba(251,191,36,0.14)", borderRadius:12, padding:"18px 20px", marginBottom:12 }}>
                        <div style={{ fontSize:11, color:"#fbbf24", letterSpacing:1.5, textTransform:"uppercase", fontFamily:"'Helvetica Neue',sans-serif", marginBottom:12 }}>⚠️ Limit or Avoid</div>
                        {result.diet.limit.map((item,i) => (
                          <div key={i} style={{ display:"flex", gap:10, marginBottom: i<result.diet.limit.length-1 ? 10 : 0, paddingBottom: i<result.diet.limit.length-1 ? 10 : 0, borderBottom: i<result.diet.limit.length-1 ? "1px solid rgba(255,255,255,0.04)" : "none" }}>
                            <span style={{ color:"#fbbf24", flexShrink:0 }}>–</span>
                            <div><div style={{ fontSize:13, color:"#ddd", fontFamily:"'Helvetica Neue',sans-serif", marginBottom:2 }}>{item.food}</div><div style={{ fontSize:11, color:"#666", fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.5 }}>{item.reason}</div></div>
                          </div>
                        ))}
                      </div>
                    )}

                    {result.diet.patterns?.length > 0 && (
                      <div style={{ background:"rgba(125,211,200,0.04)", border:"1px solid rgba(125,211,200,0.13)", borderRadius:12, padding:"18px 20px", marginBottom:12 }}>
                        <div style={{ fontSize:11, color:T, letterSpacing:1.5, textTransform:"uppercase", fontFamily:"'Helvetica Neue',sans-serif", marginBottom:12 }}>🕐 Eating Patterns</div>
                        {result.diet.patterns.map((p,i) => (
                          <div key={i} style={{ display:"flex", gap:10, marginBottom: i<result.diet.patterns.length-1 ? 8 : 0, fontSize:13, color:"#bbb", fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.6 }}>
                            <span style={{ color:T, flexShrink:0 }}>◆</span><span>{p}</span>
                          </div>
                        ))}
                      </div>
                    )}
                  </>
                )}

                {/* Lifestyle */}
                {result.lifestyle_tips?.length > 0 && (
                  <>
                    <div style={sharedStyles.divider} />
                    <div style={{ fontSize:11, letterSpacing:2, textTransform:"uppercase", color:T, marginBottom:14, fontFamily:"'Helvetica Neue',sans-serif" }}>Lifestyle Tips</div>
                    {result.lifestyle_tips.map((tip,i) => (
                      <div key={i} style={{ display:"flex", gap:10, marginBottom:12, fontSize:13, color:"#bbb", fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.6 }}>
                        <span style={{ color:T, flexShrink:0 }}>✦</span><span>{tip}</span>
                      </div>
                    ))}
                  </>
                )}

                <div style={sharedStyles.divider} />
                <div style={{ fontSize:11, color:"#555", fontFamily:"'Helvetica Neue',sans-serif", lineHeight:1.7, fontStyle:"italic" }}>{result.disclaimer}</div>

                <div style={{ marginTop:24, display:"flex", gap:10, flexWrap:"wrap" }}>
                  <button style={sharedStyles.btn} onClick={() => window.open("https://wellwellness.com","_blank")}>Shop Supplements →</button>
                  <button style={sharedStyles.btnGhost} onClick={() => { setResult(null); setStep(0); setForm({ age:"",sex:"",conditions:[],medications:"",allergies:"",concerns:[],goals:[],diet:[],smoking:"",alcohol:"",exercise:"",stress:"",extraConcerns:"",currentSupps:"" }); }}>Start Over</button>
                </div>

                <div style={sharedStyles.divider} />
                <div style={{ fontSize:11, letterSpacing:2, textTransform:"uppercase", color:T, marginBottom:14, fontFamily:"'Helvetica Neue',sans-serif" }}>Browse Our Catalog</div>
                <SupplGrid size="sm" />
              </div>
            ) : null}
          </div>
        )}
      </div>

      {/* Footer */}
      <div style={{ marginTop:20, fontSize:11, fontFamily:"'Helvetica Neue',sans-serif", color:"#333", textAlign:"center", maxWidth:480, lineHeight:1.7 }}>
        well | wellness from within · Educational purposes only · Not medical advice · Consult your provider before starting any supplement regimen
      </div>

      {/* Admin link */}
      <button onClick={() => setMode("adminLogin")} style={{ marginTop:16, background:"none", border:"none", color:"#2a2a2a", fontSize:10, fontFamily:"'Helvetica Neue',sans-serif", cursor:"pointer", letterSpacing:1 }}>
        staff login
      </button>
    </div>
  );
}
