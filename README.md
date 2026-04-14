<svg width="800" height="220" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <style>
      @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&amp;display=swap');
      
      .title { font-family: 'Press Start 2P', monospace; font-size: 20px; fill: #7ec850; }
      .subtitle { font-family: 'Press Start 2P', monospace; font-size: 9px; fill: #f5e6c8; opacity: 0.8; }
      .tag { font-family: 'Press Start 2P', monospace; font-size: 7px; fill: #f0c040; }
      
      @keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-6px)} }
      @keyframes twinkle { 0%,100%{opacity:0.3} 50%{opacity:1} }
      @keyframes sway { 0%,100%{transform:rotate(-2deg)} 50%{transform:rotate(2deg)} }
      @keyframes walk { 
        0%,100%{transform:translateX(0)} 
        50%{transform:translateX(8px)} 
      }
      @keyframes blink {
        0%,90%,100%{opacity:1}
        95%{opacity:0}
      }

      .float { animation: float 3s ease-in-out infinite; }
      .float2 { animation: float 4s ease-in-out 1s infinite; }
      .float3 { animation: float 3.5s ease-in-out 0.5s infinite; }
      .twinkle1 { animation: twinkle 2s ease-in-out infinite; }
      .twinkle2 { animation: twinkle 3s ease-in-out 1s infinite; }
      .twinkle3 { animation: twinkle 2.5s ease-in-out 0.5s infinite; }
      .twinkle4 { animation: twinkle 1.8s ease-in-out 1.5s infinite; }
      .sway { animation: sway 4s ease-in-out infinite; transform-origin: bottom center; }
      .chicken { animation: walk 2s steps(2) infinite; }
      .cat-blink { animation: blink 4s ease infinite; }
    </style>
  </defs>

  <!-- Background -->
  <rect width="800" height="220" rx="8" fill="#1c1710"/>
  <rect x="2" y="2" width="796" height="216" rx="7" fill="none" stroke="#6b5530" stroke-width="3"/>
  <rect x="6" y="6" width="788" height="208" rx="5" fill="none" stroke="#3d3222" stroke-width="1"/>
  
  <!-- Stars -->
  <circle cx="50" cy="30" r="1.5" fill="#f5e6c8" class="twinkle1"/>
  <circle cx="150" cy="18" r="1" fill="#f5e6c8" class="twinkle2"/>
  <circle cx="280" cy="25" r="1.5" fill="#f5e6c8" class="twinkle3"/>
  <circle cx="400" cy="15" r="1" fill="#f5e6c8" class="twinkle4"/>
  <circle cx="520" cy="28" r="1.5" fill="#f5e6c8" class="twinkle1"/>
  <circle cx="620" cy="12" r="1" fill="#f5e6c8" class="twinkle2"/>
  <circle cx="700" cy="22" r="1.5" fill="#f5e6c8" class="twinkle3"/>
  <circle cx="750" cy="35" r="1" fill="#f5e6c8" class="twinkle4"/>
  <circle cx="100" cy="45" r="1" fill="#f5e6c8" class="twinkle3"/>
  <circle cx="350" cy="40" r="1" fill="#f5e6c8" class="twinkle1"/>
  <circle cx="580" cy="38" r="1" fill="#f5e6c8" class="twinkle2"/>
  <circle cx="450" cy="50" r="1" fill="#f5e6c8" class="twinkle4"/>

  <!-- Ground -->
  <rect x="6" y="185" width="788" height="29" rx="0" fill="#2e2518"/>
  <rect x="6" y="183" width="788" height="3" fill="#3d3222"/>
  
  <!-- Grass tufts -->
  <g class="sway">
    <rect x="30" y="178" width="2" height="7" fill="#5a9a32"/>
    <rect x="34" y="176" width="2" height="9" fill="#7ec850"/>
    <rect x="38" y="179" width="2" height="6" fill="#5a9a32"/>
  </g>
  <g class="sway" style="animation-delay: 0.5s">
    <rect x="180" y="178" width="2" height="7" fill="#5a9a32"/>
    <rect x="184" y="175" width="2" height="10" fill="#7ec850"/>
    <rect x="188" y="179" width="2" height="6" fill="#5a9a32"/>
  </g>
  <g class="sway" style="animation-delay: 1s">
    <rect x="600" y="177" width="2" height="8" fill="#5a9a32"/>
    <rect x="604" y="175" width="2" height="10" fill="#7ec850"/>
    <rect x="608" y="179" width="2" height="6" fill="#5a9a32"/>
  </g>
  <g class="sway" style="animation-delay: 1.5s">
    <rect x="740" y="178" width="2" height="7" fill="#7ec850"/>
    <rect x="744" y="176" width="2" height="9" fill="#5a9a32"/>
  </g>
  
  <!-- Flowers -->
  <g class="float2">
    <rect x="100" y="174" width="2" height="9" fill="#5a9a32"/>
    <rect x="99" y="172" width="4" height="3" fill="#f0c040"/>
    <rect x="100" y="171" width="2" height="1" fill="#ffdd66"/>
  </g>
  <g class="float3">
    <rect x="500" y="174" width="2" height="9" fill="#5a9a32"/>
    <rect x="499" y="172" width="4" height="3" fill="#e85070"/>
    <rect x="500" y="171" width="2" height="1" fill="#ff8090"/>
  </g>
  <g class="float">
    <rect x="680" y="175" width="2" height="8" fill="#5a9a32"/>
    <rect x="679" y="173" width="4" height="3" fill="#82c8ff"/>
    <rect x="680" y="172" width="2" height="1" fill="#aaddff"/>
  </g>

  <!-- Tree -->
  <rect x="710" y="130" width="8" height="53" fill="#6b5530"/>
  <rect x="694" y="105" width="40" height="30" rx="3" fill="#5a9a32"/>
  <rect x="700" y="95" width="28" height="18" rx="3" fill="#7ec850"/>
  <rect x="707" y="88" width="14" height="12" rx="3" fill="#5a9a32"/>
  
  <!-- House -->
  <rect x="56" y="140" width="50" height="43" fill="#8b6914"/>
  <rect x="50" y="133" width="62" height="10" fill="#6b5530"/>
  <polygon points="81,110 50,133 112,133" fill="#c89820"/>
  <rect x="68" y="155" width="12" height="28" fill="#5c4422"/>
  <rect x="73" y="165" width="2" height="4" rx="1" fill="#f0c040"/>
  <rect x="57" y="148" width="8" height="8" fill="#4a8cd8" opacity="0.6"/>
  <rect x="94" y="148" width="8" height="8" fill="#4a8cd8" opacity="0.6"/>
  
  <!-- Chicken -->
  <g class="chicken">
    <rect x="138" y="175" width="8" height="6" fill="#f5e6c8"/>
    <rect x="144" y="173" width="4" height="4" fill="#f5e6c8"/>
    <rect x="148" y="174" width="2" height="2" fill="#e8822a"/>
    <rect x="142" y="173" width="2" height="2" fill="#e85050"/>
    <rect x="140" y="181" width="2" height="2" fill="#e8822a"/>
    <rect x="144" y="181" width="2" height="2" fill="#e8822a"/>
  </g>
  
  <!-- Cat -->
  <g class="float" style="animation-delay: 2s">
    <rect x="650" y="173" width="10" height="8" fill="#e8822a"/>
    <rect x="648" y="170" width="4" height="4" fill="#e8822a"/>
    <rect x="656" y="170" width="4" height="4" fill="#e8822a"/>
    <rect x="650" y="174" width="2" height="2" fill="#1c1710" class="cat-blink"/>
    <rect x="656" y="174" width="2" height="2" fill="#1c1710" class="cat-blink"/>
    <rect x="660" y="175" width="8" height="2" fill="#e8822a"/>
    <rect x="650" y="181" width="2" height="2" fill="#e8822a"/>
    <rect x="658" y="181" width="2" height="2" fill="#e8822a"/>
  </g>

  <!-- Main text content -->
  <text x="240" y="85" class="title" class="float">
    Kari Atílio Moreira
  </text>
  
  <text x="260" y="110" class="subtitle">
    🌾 Fullstack Dev • ☁️ Cloud • 🔭 Stargazer
  </text>

  <text x="280" y="135" class="tag">
    criador do OpenXNAX 🛩️
  </text>

  <text x="270" y="158" class="tag" fill="#7ec850">
    📍 Brasil • 💻 atiliodev.com
  </text>

  <!-- Decorative icons floating -->
  <text x="220" y="80" font-size="16" class="float">⛏️</text>
  <text x="580" y="90" font-size="14" class="float2">⭐</text>
  <text x="210" y="155" font-size="12" class="float3">🌸</text>
  <text x="570" y="150" font-size="12" class="float">🦋</text>
</svg>
