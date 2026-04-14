import { useState, useEffect, useRef } from "react";

const PIXEL = "https://fonts.googleapis.com/css2?family=Press+Start+2P&family=VT323&display=swap";

const PALETTE = {
  bg: "#1c1710",
  panel: "#2e2518",
  panelLight: "#3d3222",
  border: "#6b5530",
  borderLight: "#8a7040",
  green: "#7ec850",
  greenDark: "#5a9a32",
  gold: "#f0c040",
  goldDark: "#c89820",
  brown: "#8b6914",
  orange: "#e8822a",
  red: "#e85050",
  blue: "#50a0e8",
  sky: "#4a8cd8",
  cream: "#f5e6c8",
  white: "#ede0d0",
  darkBg: "#151008",
  heart: "#e85070",
  wood: "#5c4422",
  woodLight: "#7a5c33",
  soil: "#3a2a14",
};

const SKILLS = {
  "⚔️ Frontend": [
    { name: "HTML", lvl: 10, icon: "🌐" },
    { name: "CSS", lvl: 9, icon: "🎨" },
    { name: "JavaScript", lvl: 10, icon: "⚡" },
    { name: "React", lvl: 9, icon: "⚛️" },
    { name: "Next.js", lvl: 8, icon: "▲" },
  ],
  "🛡️ Backend": [
    { name: "Node.js", lvl: 9, icon: "💚" },
    { name: "Spring Boot", lvl: 8, icon: "🍃" },
    { name: "NestJS", lvl: 7, icon: "🐱" },
    { name: "Java Swing", lvl: 7, icon: "☕" },
    { name: "JSP", lvl: 6, icon: "📜" },
    { name: "XML/XSL", lvl: 6, icon: "📋" },
  ],
  "🗃️ Banco de Dados": [
    { name: "MySQL", lvl: 9, icon: "🐬" },
    { name: "Oracle", lvl: 8, icon: "🔴" },
    { name: "MongoDB", lvl: 7, icon: "🍃" },
    { name: "PostgreSQL", lvl: 8, icon: "🐘" },
    { name: "SQLite", lvl: 7, icon: "🪶" },
    { name: "JDBC", lvl: 6, icon: "🔗" },
  ],
  "☁️ Cloud & DevOps": [
    { name: "AWS", lvl: 7, icon: "☁️" },
    { name: "Git", lvl: 9, icon: "🌿" },
    { name: "GitHub", lvl: 9, icon: "🐙" },
    { name: "Azure", lvl: 7, icon: "🔷" },
    { name: "Azure DevOps", lvl: 7, icon: "🚀" },
    { name: "GitHub Actions", lvl: 8, icon: "⚙️" },
    { name: "Jenkins", lvl: 6, icon: "🤖" },
    { name: "CI/CD", lvl: 8, icon: "♾️" },
  ],
};

const SEASONS = ["spring", "summer", "fall", "winter"];
const SEASON_THEMES = {
  spring: { accent: "#7ec850", sky1: "#1a2818", sky2: "#0f1a0c", particles: ["🌸", "🦋", "🌱", "🌼", "🐝"], label: "Primavera" },
  summer: { accent: "#f0c040", sky1: "#2a2210", sky2: "#1a1508", particles: ["☀️", "🌻", "🍉", "🐞", "✨"], label: "Verão" },
  fall: { accent: "#e8822a", sky1: "#2a1a10", sky2: "#1a0f08", particles: ["🍂", "🍁", "🎃", "🌰", "🍄"], label: "Outono" },
  winter: { accent: "#82c8ff", sky1: "#14202a", sky2: "#0a1018", particles: ["❄️", "⛄", "🌨️", "💎", "🧊"], label: "Inverno" },
};

function PixelBorder({ children, style, glow }) {
  return (
    <div style={{
      border: `3px solid ${PALETTE.border}`,
      borderRadius: "2px",
      boxShadow: `inset -2px -2px 0 ${PALETTE.panelLight}, inset 2px 2px 0 ${PALETTE.darkBg}, 4px 4px 0 rgba(0,0,0,0.5)${glow ? `, 0 0 20px ${glow}30` : ""}`,
      background: PALETTE.panel,
      ...style,
    }}>{children}</div>
  );
}

function SkillBar({ skill, delay, accent }) {
  const [width, setWidth] = useState(0);
  const [hovered, setHovered] = useState(false);
  useEffect(() => { const t = setTimeout(() => setWidth((skill.lvl / 10) * 100), delay); return () => clearTimeout(t); }, [skill.lvl, delay]);
  return (
    <div onMouseEnter={() => setHovered(true)} onMouseLeave={() => setHovered(false)}
      style={{ marginBottom: "8px", cursor: "pointer", transform: hovered ? "translateX(4px)" : "translateX(0)", transition: "transform 0.2s ease" }}>
      <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: "3px" }}>
        <span style={{ fontFamily: "'VT323', monospace", fontSize: "18px", color: PALETTE.cream, display: "flex", alignItems: "center", gap: "6px" }}>
          <span style={{ fontSize: "16px", animation: hovered ? "pixelBounce 0.3s steps(3) infinite" : "none" }}>{skill.icon}</span>
          {skill.name}
        </span>
        <span style={{ fontFamily: "'Press Start 2P'", fontSize: "8px", color: accent }}>Lv.{skill.lvl}</span>
      </div>
      <div style={{ height: "12px", background: PALETTE.darkBg, borderRadius: "1px", border: `2px solid ${PALETTE.border}`, overflow: "hidden", boxShadow: "inset 1px 1px 0 rgba(0,0,0,0.5)" }}>
        <div style={{
          height: "100%", width: `${width}%`, transition: "width 1s steps(10)",
          background: `repeating-linear-gradient(90deg, ${accent} 0px, ${accent} 6px, ${accent}cc 6px, ${accent}cc 8px)`,
          boxShadow: hovered ? `0 0 8px ${accent}80` : "none", position: "relative",
        }}>
          {hovered && <div style={{ position: "absolute", right: "2px", top: "-1px", fontSize: "10px", animation: "sparkle 0.4s steps(2) infinite" }}>✨</div>}
        </div>
      </div>
    </div>
  );
}

function Chicken() {
  const [pos, setPos] = useState({ x: 70, flip: false });
  const [pecking, setPecking] = useState(false);
  useEffect(() => {
    const i = setInterval(() => {
      setPos(prev => { const nx = Math.max(5, Math.min(90, prev.x + (Math.random() - 0.5) * 20)); return { x: nx, flip: nx < prev.x }; });
      if (Math.random() > 0.6) { setPecking(true); setTimeout(() => setPecking(false), 600); }
    }, 2500);
    return () => clearInterval(i);
  }, []);
  return (
    <div onClick={e => { e.stopPropagation(); setPecking(true); }} style={{
      position: "absolute", bottom: "8px", left: `${pos.x}%`, transition: "left 2s steps(8)",
      fontSize: "22px", transform: `scaleX(${pos.flip ? -1 : 1}) ${pecking ? "rotate(20deg)" : "rotate(0deg)"}`,
      transformOrigin: "bottom center", cursor: "pointer", filter: "drop-shadow(0 2px 4px rgba(0,0,0,0.5))", zIndex: 5,
    }}>🐔</div>
  );
}

function Cat() {
  const [sleeping, setSleeping] = useState(true);
  const [msg, setMsg] = useState("");
  const msgs = ["Miau! 🐾", "git push meow~", "npm run purr", "SELECT * FROM peixe", "docker run --cat", "Zzz...", "Commit fofo!"];
  return (
    <div style={{
      position: "absolute", bottom: "6px", right: "16px", cursor: "pointer", zIndex: 5, fontSize: "24px",
      animation: sleeping ? "none" : "pixelBounce 0.4s steps(3) 2",
    }} onClick={e => {
      e.stopPropagation(); setSleeping(false);
      setMsg(msgs[Math.floor(Math.random() * msgs.length)]);
      setTimeout(() => { setSleeping(true); setMsg(""); }, 2500);
    }}>
      {sleeping ? "😺" : "😻"}
      {msg && <div style={{
        position: "absolute", bottom: "32px", right: 0, background: PALETTE.panel,
        border: `2px solid ${PALETTE.border}`, padding: "4px 10px", fontFamily: "'VT323', monospace",
        fontSize: "14px", color: PALETTE.gold, whiteSpace: "nowrap",
        boxShadow: "3px 3px 0 rgba(0,0,0,0.5)", animation: "popUp 0.2s steps(3)",
      }}>{msg}</div>}
    </div>
  );
}

function Particle({ emoji, delay }) {
  const s = useRef({
    left: `${5 + Math.random() * 90}%`, dur: `${6 + Math.random() * 6}s`,
    size: `${12 + Math.random() * 10}px`, sway: `${-30 + Math.random() * 60}px`,
  }).current;
  return (
    <div style={{
      position: "absolute", top: "-20px", left: s.left, fontSize: s.size,
      animation: `particleFall ${s.dur} linear ${delay}s infinite`,
      pointerEvents: "none", opacity: 0.5, zIndex: 0, "--sway": s.sway,
    }}>{emoji}</div>
  );
}

function CurlyBoyAvatar({ accent }) {
  return (
    <svg width="80" height="80" viewBox="0 0 16 16" style={{
      imageRendering: "pixelated", border: `3px solid ${accent}`, borderRadius: "2px",
      background: PALETTE.darkBg,
      boxShadow: `0 0 15px ${accent}30, inset 0 0 10px rgba(0,0,0,0.5)`,
    }}>
      {/* curly hair top */}
      <rect x="4" y="0" width="1" height="1" fill="#2a1a08"/><rect x="5" y="0" width="1" height="1" fill="#3a2510"/>
      <rect x="6" y="0" width="1" height="1" fill="#2a1a08"/><rect x="7" y="0" width="1" height="1" fill="#3a2510"/>
      <rect x="8" y="0" width="1" height="1" fill="#2a1a08"/><rect x="9" y="0" width="1" height="1" fill="#3a2510"/>
      <rect x="10" y="0" width="1" height="1" fill="#2a1a08"/>
      {/* curly sides */}
      <rect x="3" y="1" width="1" height="2" fill="#2a1a08"/><rect x="11" y="1" width="1" height="2" fill="#2a1a08"/>
      <rect x="2" y="2" width="1" height="2" fill="#3a2510"/><rect x="12" y="2" width="1" height="2" fill="#3a2510"/>
      <rect x="2" y="4" width="1" height="1" fill="#2a1a08"/><rect x="12" y="4" width="1" height="1" fill="#2a1a08"/>
      <rect x="1" y="3" width="1" height="1" fill="#2a1a08"/><rect x="13" y="3" width="1" height="1" fill="#2a1a08"/>
      {/* hair mass */}
      <rect x="4" y="1" width="7" height="1" fill="#3a2510"/>
      <rect x="3" y="2" width="9" height="2" fill="#3a2510"/>
      {/* face */}
      <rect x="4" y="4" width="7" height="6" fill="#c8935a"/>
      <rect x="3" y="5" width="1" height="4" fill="#c8935a"/>
      <rect x="11" y="5" width="1" height="4" fill="#c8935a"/>
      {/* eyes */}
      <rect x="5" y="5" width="2" height="2" fill="#1a1008"/>
      <rect x="9" y="5" width="2" height="2" fill="#1a1008"/>
      <rect x="5" y="5" width="1" height="1" fill="#fff" opacity="0.35"/>
      <rect x="9" y="5" width="1" height="1" fill="#fff" opacity="0.35"/>
      {/* nose */}
      <rect x="7" y="7" width="1" height="1" fill="#b8834a"/>
      {/* smile */}
      <rect x="6" y="8" width="1" height="1" fill="#a07040"/>
      <rect x="7" y="9" width="1" height="1" fill="#a07040"/>
      <rect x="8" y="8" width="1" height="1" fill="#a07040"/>
      {/* cheeks */}
      <rect x="4" y="7" width="1" height="1" fill="#d8a070" opacity="0.6"/>
      <rect x="10" y="7" width="1" height="1" fill="#d8a070" opacity="0.6"/>
      {/* shirt */}
      <rect x="3" y="10" width="9" height="3" fill="#4a8850"/>
      <rect x="2" y="11" width="1" height="2" fill="#4a8850"/>
      <rect x="12" y="11" width="1" height="2" fill="#4a8850"/>
      <rect x="7" y="10" width="1" height="2" fill="#5aaa65"/>
      <rect x="6" y="10" width="3" height="1" fill="#5a9a60"/>
      {/* pants */}
      <rect x="4" y="13" width="3" height="2" fill="#3a6590"/>
      <rect x="8" y="13" width="3" height="2" fill="#3a6590"/>
      <rect x="7" y="13" width="1" height="2" fill="#2a5580"/>
      {/* shoes */}
      <rect x="4" y="15" width="3" height="1" fill="#6b5530"/>
      <rect x="8" y="15" width="3" height="1" fill="#6b5530"/>
    </svg>
  );
}

function AstropySection() {
  const [activeTab, setActiveTab] = useState("about");
  const [starMap, setStarMap] = useState([]);
  const [hoverStar, setHoverStar] = useState(null);

  useEffect(() => {
    setStarMap(Array.from({ length: 60 }, (_, i) => ({
      id: i, x: Math.random() * 100, y: Math.random() * 100,
      size: 1 + Math.random() * 3, brightness: 0.3 + Math.random() * 0.7,
      twinkleSpeed: 1 + Math.random() * 3,
      name: ["Sirius", "Vega", "Arcturus", "Polaris", "Betelgeuse", "Rigel", "Aldebaran", "Antares"][Math.floor(Math.random() * 8)],
    })));
  }, []);

  const modules = [
    { name: "Coordinates", desc: "SkyCoord, ICRS, Galactic frames", icon: "📍" },
    { name: "Tables", desc: "Leitura de tabelas FITS & VOTable", icon: "📊" },
    { name: "Units", desc: "Conversão de unidades astronômicas", icon: "📐" },
    { name: "Cosmology", desc: "Parâmetros cosmológicos & distâncias", icon: "🌌" },
    { name: "Time", desc: "Escalas de tempo astronômicas", icon: "⏰" },
    { name: "FITS I/O", desc: "Leitura e escrita de arquivos FITS", icon: "💾" },
  ];

  return (
    <PixelBorder glow="#4a8cd8" style={{ padding: "0", overflow: "hidden", marginBottom: "20px" }}>
      <div style={{
        position: "relative", height: "200px", overflow: "hidden",
        background: "linear-gradient(180deg, #020008 0%, #06041a 50%, #0e0a1e 100%)",
        borderBottom: `3px solid ${PALETTE.border}`,
      }}>
        {starMap.map(star => (
          <div key={star.id}
            onMouseEnter={() => setHoverStar(star)} onMouseLeave={() => setHoverStar(null)}
            style={{
              position: "absolute", left: `${star.x}%`, top: `${star.y}%`,
              width: `${star.size}px`, height: `${star.size}px`, borderRadius: "50%",
              background: `rgba(220,230,255,${star.brightness})`,
              boxShadow: `0 0 ${star.size * 2}px rgba(200,220,255,${star.brightness * 0.5})`,
              animation: `twinkle ${star.twinkleSpeed}s ease-in-out infinite`,
              cursor: "crosshair", transition: "transform 0.2s",
              transform: hoverStar?.id === star.id ? "scale(3)" : "scale(1)", zIndex: 2,
            }}
          />
        ))}
        {hoverStar && (
          <div style={{
            position: "absolute", left: `${Math.min(hoverStar.x, 75)}%`, top: `${Math.max(hoverStar.y - 8, 5)}%`,
            fontFamily: "'VT323', monospace", fontSize: "12px", color: "#aaccff",
            background: "rgba(0,0,10,0.85)", padding: "2px 8px", border: "1px solid #335",
            zIndex: 10, pointerEvents: "none",
          }}>★ {hoverStar.name} (mag {(hoverStar.brightness * 6).toFixed(1)})</div>
        )}
        <div style={{
          position: "absolute", bottom: "10px", left: "50%", transform: "translateX(-50%)",
          fontSize: "48px", filter: "drop-shadow(0 0 10px rgba(100,150,255,0.5))",
          animation: "floatTelescope 4s ease-in-out infinite", zIndex: 3,
        }}>🔭</div>
        <div style={{
          position: "absolute", bottom: "65px", left: "50%", transform: "translateX(-50%)",
          fontFamily: "'Press Start 2P'", fontSize: "14px", color: "#aaccff",
          textShadow: "0 0 10px rgba(100,150,255,0.8)", zIndex: 3, whiteSpace: "nowrap",
        }}>★ ASTROPY ★</div>
        <div style={{
          position: "absolute", bottom: "50px", left: "50%", transform: "translateX(-50%)",
          fontFamily: "'VT323', monospace", fontSize: "14px", color: "rgba(170,200,255,0.6)",
          zIndex: 3, whiteSpace: "nowrap",
        }}>Explorando o universo com Python</div>
        <div style={{
          position: "absolute", top: "20%", left: "-10%", width: "60px", height: "2px",
          background: "linear-gradient(90deg, transparent, #fff, transparent)",
          animation: "shootingStar 4s linear infinite", animationDelay: "2s",
          opacity: 0.7, transform: "rotate(-15deg)", zIndex: 1,
        }} />
      </div>

      <div style={{ display: "flex", borderBottom: `2px solid ${PALETTE.border}` }}>
        {["about", "modules", "code"].map(tab => (
          <button key={tab} onClick={e => { e.stopPropagation(); setActiveTab(tab); }} style={{
            flex: 1, padding: "10px", fontFamily: "'Press Start 2P'", fontSize: "8px",
            color: activeTab === tab ? PALETTE.gold : PALETTE.cream + "80",
            background: activeTab === tab ? PALETTE.panelLight : "transparent",
            border: "none", borderRight: `2px solid ${PALETTE.border}`,
            cursor: "pointer", textTransform: "uppercase", transition: "all 0.2s", letterSpacing: "1px",
          }}>
            {tab === "about" ? "📖 Sobre" : tab === "modules" ? "📦 Módulos" : "💻 Code"}
          </button>
        ))}
      </div>

      <div style={{ padding: "16px" }} onClick={e => e.stopPropagation()}>
        {activeTab === "about" && (
          <div style={{ fontFamily: "'VT323', monospace", fontSize: "18px", color: PALETTE.cream, lineHeight: 1.6 }}>
            <p style={{ marginBottom: "12px" }}>🌟 Astropy é a biblioteca central do ecossistema Python para astronomia.</p>
            <p style={{ marginBottom: "12px" }}>🔭 Uso Astropy para análise de dados astronômicos, manipulação de coordenadas celestes, e processamento de arquivos FITS.</p>
            <div style={{ display: "flex", gap: "12px", flexWrap: "wrap", marginTop: "16px" }}>
              {[{ label: "Observações", val: "150+", icon: "🌠" }, { label: "Datasets", val: "42", icon: "📡" }, { label: "Galáxias", val: "∞", icon: "🌌" }].map((s, i) => (
                <div key={i} style={{
                  flex: "1", minWidth: "80px", textAlign: "center", padding: "12px 8px",
                  background: "rgba(74,140,216,0.1)", border: `2px solid ${PALETTE.border}`, borderRadius: "2px",
                }}>
                  <div style={{ fontSize: "20px", marginBottom: "4px" }}>{s.icon}</div>
                  <div style={{ fontFamily: "'Press Start 2P'", fontSize: "12px", color: "#82c8ff" }}>{s.val}</div>
                  <div style={{ fontSize: "12px", color: PALETTE.cream + "80", marginTop: "2px" }}>{s.label}</div>
                </div>
              ))}
            </div>
          </div>
        )}
        {activeTab === "modules" && (
          <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: "10px" }}>
            {modules.map((c, i) => (
              <div key={i} style={{
                padding: "12px", background: "rgba(74,140,216,0.06)", border: `2px solid ${PALETTE.border}`,
                borderRadius: "2px", cursor: "pointer", transition: "all 0.2s",
              }}
                onMouseEnter={e => { e.currentTarget.style.background = "rgba(74,140,216,0.15)"; e.currentTarget.style.transform = "translateY(-2px)"; e.currentTarget.style.boxShadow = "0 4px 0 rgba(0,0,0,0.3)"; }}
                onMouseLeave={e => { e.currentTarget.style.background = "rgba(74,140,216,0.06)"; e.currentTarget.style.transform = "translateY(0)"; e.currentTarget.style.boxShadow = "none"; }}
              >
                <div style={{ fontSize: "20px", marginBottom: "4px" }}>{c.icon}</div>
                <div style={{ fontFamily: "'Press Start 2P'", fontSize: "8px", color: "#82c8ff", marginBottom: "6px" }}>{c.name}</div>
                <div style={{ fontFamily: "'VT323', monospace", fontSize: "14px", color: PALETTE.cream + "99" }}>{c.desc}</div>
              </div>
            ))}
          </div>
        )}
        {activeTab === "code" && (
          <div style={{
            fontFamily: "'VT323', monospace", fontSize: "16px", background: "#0a0808",
            border: `2px solid ${PALETTE.border}`, padding: "14px", borderRadius: "2px", lineHeight: 1.7, overflow: "auto",
          }}>
            <div><span style={{ color: "#e8822a" }}>from</span> <span style={{ color: "#82c8ff" }}>astropy</span> <span style={{ color: "#e8822a" }}>import</span> units <span style={{ color: "#e8822a" }}>as</span> u</div>
            <div><span style={{ color: "#e8822a" }}>from</span> <span style={{ color: "#82c8ff" }}>astropy.coordinates</span> <span style={{ color: "#e8822a" }}>import</span> SkyCoord</div>
            <div style={{ color: "#666", marginTop: "8px" }}># Coordenadas da Nebulosa de Órion</div>
            <div>coord = SkyCoord(<span style={{ color: "#f0c040" }}>'05h35m17.3s'</span>,</div>
            <div>&nbsp;&nbsp;&nbsp;&nbsp;<span style={{ color: "#f0c040" }}>'-05d23m28s'</span>, frame=<span style={{ color: "#f0c040" }}>'icrs'</span>)</div>
            <div style={{ marginTop: "8px" }}><span style={{ color: "#666" }}># Distância em parsecs</span></div>
            <div>dist = <span style={{ color: "#82c8ff" }}>412</span> * u.pc</div>
            <div>print(dist.to(u.lightyear)) <span style={{ color: "#666" }}># ~1344 ly ✨</span></div>
          </div>
        )}
      </div>
    </PixelBorder>
  );
}

export default function StardewProfile() {
  const [season, setSeason] = useState("spring");
  const [expandedCat, setExpandedCat] = useState(null);
  const [gold, setGold] = useState(13370);
  const [energy] = useState(270);
  const [clickEffects, setClickEffects] = useState([]);
  const theme = SEASON_THEMES[season];

  const addClickEffect = (e) => {
    const id = Date.now();
    const amt = Math.floor(Math.random() * 10) + 1;
    setClickEffects(prev => [...prev, { id, x: e.clientX, y: e.clientY, amt }]);
    setGold(g => g + amt);
    setTimeout(() => setClickEffects(prev => prev.filter(ef => ef.id !== id)), 800);
  };

  return (
    <>
      <link href={PIXEL} rel="stylesheet" />
      <style>{`
        @keyframes pixelBounce { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-6px)} }
        @keyframes sparkle { 0%,100%{opacity:1} 50%{opacity:0.3} }
        @keyframes popUp { from{transform:translateY(8px);opacity:0} to{transform:translateY(0);opacity:1} }
        @keyframes twinkle { 0%,100%{opacity:0.3} 50%{opacity:1} }
        @keyframes particleFall {
          0%{transform:translateY(-20px) translateX(0) rotate(0deg);opacity:0}
          10%{opacity:0.6} 90%{opacity:0.6}
          100%{transform:translateY(100vh) translateX(var(--sway)) rotate(360deg);opacity:0}
        }
        @keyframes floatTelescope { 0%,100%{transform:translateX(-50%) translateY(0) rotate(-5deg)} 50%{transform:translateX(-50%) translateY(-8px) rotate(5deg)} }
        @keyframes shootingStar {
          0%{transform:translateX(0) translateY(0) rotate(-15deg);opacity:0}
          5%{opacity:0.9} 15%{opacity:0}
          100%{transform:translateX(500px) translateY(200px) rotate(-15deg);opacity:0}
        }
        @keyframes slideIn { from{opacity:0;transform:translateY(12px)} to{opacity:1;transform:translateY(0)} }
        @keyframes idleBob { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-3px)} }
        * { box-sizing:border-box; margin:0; padding:0; }
        ::-webkit-scrollbar { width:8px }
        ::-webkit-scrollbar-track { background:${PALETTE.darkBg} }
        ::-webkit-scrollbar-thumb { background:${PALETTE.border}; border:2px solid ${PALETTE.darkBg} }
      `}</style>

      <div onClick={addClickEffect} style={{
        minHeight: "100vh",
        background: `linear-gradient(180deg, ${theme.sky1} 0%, ${theme.sky2} 100%)`,
        fontFamily: "'VT323', monospace", position: "relative", overflow: "hidden",
        transition: "background 1s ease",
        cursor: "url('data:image/svg+xml;utf8,<svg xmlns=%22http://www.w3.org/2000/svg%22 width=%2224%22 height=%2224%22><text y=%2218%22 font-size=%2218%22>⛏️</text></svg>') 12 12, auto",
      }}>
        {/* Day/night bar */}
        <div style={{
          position: "absolute", top: 0, left: 0, right: 0, height: "4px",
          background: `linear-gradient(90deg, ${theme.accent}80, ${theme.accent}, ${theme.accent}80)`,
          transition: "background 2s ease", zIndex: 10,
        }} />

        {clickEffects.map(ef => (
          <div key={ef.id} style={{
            position: "fixed", left: ef.x, top: ef.y, fontFamily: "'Press Start 2P'",
            fontSize: "10px", color: PALETTE.gold, animation: "popUp 0.6s ease forwards",
            pointerEvents: "none", zIndex: 999,
          }}>+{ef.amt}g</div>
        ))}

        {theme.particles.map((emoji, i) => (
          <Particle key={`${season}-${i}`} emoji={emoji} delay={i * 1.5} />
        ))}

        <div style={{ maxWidth: "700px", margin: "0 auto", padding: "30px 16px", position: "relative", zIndex: 1 }}>

          {/* Season selector */}
          <div style={{ display: "flex", justifyContent: "center", gap: "6px", marginBottom: "16px" }}>
            {SEASONS.map(s => (
              <button key={s} onClick={e => { e.stopPropagation(); setSeason(s); }} style={{
                fontFamily: "'Press Start 2P'", fontSize: "7px", padding: "6px 12px",
                background: season === s ? SEASON_THEMES[s].accent + "30" : "rgba(0,0,0,0.3)",
                color: season === s ? SEASON_THEMES[s].accent : PALETTE.cream + "60",
                border: `2px solid ${season === s ? SEASON_THEMES[s].accent : PALETTE.border}`,
                cursor: "pointer", transition: "all 0.2s", borderRadius: "2px",
                boxShadow: season === s ? `0 0 10px ${SEASON_THEMES[s].accent}30` : "none",
              }}>{SEASON_THEMES[s].label}</button>
            ))}
          </div>

          {/* Profile card */}
          <PixelBorder style={{ padding: "20px", marginBottom: "20px", position: "relative", overflow: "visible" }}>
            <Chicken />
            <Cat />
            <div style={{ textAlign: "center", paddingBottom: "16px" }}>
              <div style={{ margin: "0 auto 14px", width: "80px", animation: "idleBob 3s ease-in-out infinite" }}>
                <CurlyBoyAvatar accent={theme.accent} />
              </div>

              <h1 style={{
                fontFamily: "'Press Start 2P'", fontSize: "16px", color: theme.accent,
                textShadow: `0 0 10px ${theme.accent}50`, marginBottom: "8px",
              }}>karimoreira</h1>

              <div style={{
                fontFamily: "'VT323', monospace", fontSize: "18px", color: PALETTE.cream + "aa", marginBottom: "10px",
              }}>🌾 Fullstack Developer &nbsp;•&nbsp; ☁️ Cloud Explorer &nbsp;•&nbsp; 🔭 Stargazer</div>

              <a href="https://github.com/karimoreira/" target="_blank" rel="noopener noreferrer"
                onClick={e => e.stopPropagation()} style={{
                  fontFamily: "'Press Start 2P'", fontSize: "8px", color: PALETTE.green,
                  textDecoration: "none", display: "inline-flex", alignItems: "center", gap: "6px",
                  padding: "6px 14px", background: "rgba(126,200,80,0.1)",
                  border: `2px solid ${PALETTE.green}60`, borderRadius: "2px", transition: "all 0.2s", cursor: "pointer",
                }}
                onMouseEnter={e => { e.currentTarget.style.background = "rgba(126,200,80,0.2)"; e.currentTarget.style.transform = "translateY(-2px)"; }}
                onMouseLeave={e => { e.currentTarget.style.background = "rgba(126,200,80,0.1)"; e.currentTarget.style.transform = "translateY(0)"; }}
              >🐙 github.com/karimoreira</a>

              {/* HUD */}
              <div style={{
                display: "flex", justifyContent: "center", gap: "20px", flexWrap: "wrap",
                padding: "12px", marginTop: "16px", background: "rgba(0,0,0,0.3)",
                border: `2px solid ${PALETTE.border}`, borderRadius: "2px",
              }}>
                <div style={{ display: "flex", alignItems: "center", gap: "6px" }}>
                  <span>❤️</span>
                  <div style={{ width: "80px", height: "10px", background: PALETTE.darkBg, border: `1px solid ${PALETTE.border}` }}>
                    <div style={{ width: "85%", height: "100%", background: `linear-gradient(90deg, ${PALETTE.red}, ${PALETTE.heart})` }} />
                  </div>
                </div>
                <div style={{ display: "flex", alignItems: "center", gap: "6px" }}>
                  <span>⚡</span>
                  <div style={{ width: "80px", height: "10px", background: PALETTE.darkBg, border: `1px solid ${PALETTE.border}` }}>
                    <div style={{ width: "100%", height: "100%", background: `linear-gradient(90deg, ${PALETTE.green}, ${PALETTE.gold})` }} />
                  </div>
                  <span style={{ fontFamily: "'Press Start 2P'", fontSize: "7px", color: PALETTE.green }}>{energy}/270</span>
                </div>
                <div style={{ display: "flex", alignItems: "center", gap: "4px" }}>
                  <span>💰</span>
                  <span style={{ fontFamily: "'Press Start 2P'", fontSize: "9px", color: PALETTE.gold }}>{gold.toLocaleString()}g</span>
                </div>
              </div>
            </div>
          </PixelBorder>

          {/* Skills */}
          <PixelBorder style={{ padding: "0", marginBottom: "20px", overflow: "hidden" }}>
            <div style={{ padding: "12px 16px", borderBottom: `3px solid ${PALETTE.border}`, background: "rgba(0,0,0,0.2)" }}>
              <h2 style={{ fontFamily: "'Press Start 2P'", fontSize: "10px", color: theme.accent, display: "flex", alignItems: "center", gap: "8px" }}>
                📦 INVENTÁRIO DE SKILLS
              </h2>
            </div>
            {Object.entries(SKILLS).map(([cat, skills]) => (
              <div key={cat} style={{ borderBottom: `2px solid ${PALETTE.border}` }}>
                <button onClick={e => { e.stopPropagation(); setExpandedCat(expandedCat === cat ? null : cat); }}
                  style={{
                    width: "100%", padding: "12px 16px",
                    background: expandedCat === cat ? "rgba(255,255,255,0.03)" : "transparent",
                    border: "none", cursor: "pointer", display: "flex", justifyContent: "space-between",
                    alignItems: "center", fontFamily: "'Press Start 2P'", fontSize: "9px",
                    color: expandedCat === cat ? theme.accent : PALETTE.cream, transition: "all 0.2s",
                  }}>
                  <span>{cat}</span>
                  <span style={{
                    fontSize: "14px", fontFamily: "'VT323'",
                    transform: expandedCat === cat ? "rotate(90deg)" : "rotate(0deg)",
                    transition: "transform 0.3s", display: "inline-block",
                  }}>▶</span>
                </button>
                <div style={{
                  maxHeight: expandedCat === cat ? "500px" : "0", overflow: "hidden",
                  transition: "max-height 0.5s ease",
                  padding: expandedCat === cat ? "0 16px 16px" : "0 16px",
                }}>
                  {skills.map((skill, si) => (
                    <SkillBar key={skill.name} skill={skill} delay={100 + si * 80} accent={theme.accent} />
                  ))}
                </div>
              </div>
            ))}
          </PixelBorder>

          {/* Astropy */}
          <AstropySection />

          {/* Quest log */}
          <PixelBorder style={{ padding: "0", marginBottom: "20px", overflow: "hidden" }}>
            <div style={{ padding: "12px 16px", borderBottom: `3px solid ${PALETTE.border}`, background: "rgba(0,0,0,0.2)" }}>
              <h2 style={{ fontFamily: "'Press Start 2P'", fontSize: "10px", color: PALETTE.gold, display: "flex", alignItems: "center", gap: "8px" }}>
                📜 QUEST LOG
              </h2>
            </div>
            <div style={{ padding: "16px" }}>
              {[
                { q: "Construir apps com Spring Boot + React", xp: "500 XP", status: "🟢" },
                { q: "Dominar arquitetura Cloud AWS", xp: "750 XP", status: "🟡" },
                { q: "Explorar galáxias com Astropy", xp: "1000 XP", status: "🟡" },
                { q: "Automatizar tudo com CI/CD", xp: "300 XP", status: "🟢" },
                { q: "Contribuir para open source", xp: "∞ XP", status: "🔵" },
              ].map((quest, i) => (
                <div key={i} style={{
                  display: "flex", alignItems: "center", gap: "10px", padding: "10px 12px",
                  marginBottom: "6px", background: "rgba(255,255,255,0.02)",
                  border: `1px solid ${PALETTE.border}40`, borderRadius: "2px",
                  animation: `slideIn 0.4s ease ${i * 0.1}s both`, cursor: "pointer", transition: "all 0.2s",
                }}
                  onMouseEnter={e => { e.currentTarget.style.background = "rgba(255,255,255,0.05)"; e.currentTarget.style.transform = "translateX(4px)"; }}
                  onMouseLeave={e => { e.currentTarget.style.background = "rgba(255,255,255,0.02)"; e.currentTarget.style.transform = "translateX(0)"; }}
                >
                  <span>{quest.status}</span>
                  <span style={{ flex: 1, fontSize: "17px", color: PALETTE.cream }}>{quest.q}</span>
                  <span style={{ fontFamily: "'Press Start 2P'", fontSize: "7px", color: PALETTE.gold }}>{quest.xp}</span>
                </div>
              ))}
            </div>
          </PixelBorder>

          {/* Footer */}
          <div style={{
            textAlign: "center", padding: "20px", fontFamily: "'Press Start 2P'",
            fontSize: "7px", color: PALETTE.cream + "40", letterSpacing: "1px",
          }}>
            <div style={{ fontSize: "24px", marginBottom: "12px", letterSpacing: "6px" }}>🌾🏠🌳🐔🌻</div>
            feito com ☕ e 💛 • clique para ganhar gold!
            <div style={{ marginTop: "10px", display: "flex", justifyContent: "center", gap: "16px" }}>
              {[
                { icon: "🐙", url: "https://github.com/karimoreira/" },
                { icon: "💼", url: "#" },
                { icon: "📧", url: "#" },
              ].map((link, i) => (
                <a key={i} href={link.url} target="_blank" rel="noopener noreferrer"
                  onClick={e => e.stopPropagation()} style={{
                    cursor: "pointer", fontSize: "22px", transition: "transform 0.2s",
                    display: "inline-block", textDecoration: "none",
                  }}
                  onMouseEnter={e => e.currentTarget.style.transform = "scale(1.3) translateY(-4px)"}
                  onMouseLeave={e => e.currentTarget.style.transform = "scale(1)"}
                >{link.icon}</a>
              ))}
            </div>
          </div>
        </div>
      </div>
    </>
  );
}
