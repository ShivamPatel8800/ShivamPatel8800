<!DOCTYPE html>
<html>
<head>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@700;900&display=swap');

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: #080808;
    color: #ccc;
    font-family: 'Share Tech Mono', monospace;
    font-size: 13px;
    line-height: 1.6;
    overflow-x: hidden;
  }

  /* Scanline overlay */
  body::before {
    content: '';
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.08) 2px, rgba(0,0,0,0.08) 4px);
    pointer-events: none;
    z-index: 100;
  }

  .container { max-width: 860px; margin: 0 auto; padding: 0 20px 40px; }

  /* HEADER */
  .header {
    text-align: center;
    padding: 32px 0 24px;
    border-bottom: 1px solid #2a0000;
    position: relative;
  }

  .header::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, #ff0000, transparent);
    animation: scanH 3s linear infinite;
  }

  @keyframes scanH { 0%,100%{opacity:0.3} 50%{opacity:1} }

  .name {
    font-family: 'Orbitron', monospace;
    font-size: 42px;
    font-weight: 900;
    color: #ff0000;
    letter-spacing: 8px;
    text-transform: uppercase;
    animation: glitch 4s infinite;
    position: relative;
  }

  @keyframes glitch {
    0%,90%,100% { text-shadow: none; transform: none; }
    91% { text-shadow: -2px 0 #ff0000, 2px 0 #ff4444; transform: skewX(-1deg); }
    92% { text-shadow: 2px 0 #ff0000, -2px 0 #aa0000; transform: skewX(1deg); }
    93% { text-shadow: none; transform: none; }
    94% { text-shadow: -1px 0 #ff2200; transform: translateX(1px); }
    95% { text-shadow: none; transform: none; }
  }

  .subtitle {
    color: #ff4444;
    font-size: 12px;
    letter-spacing: 4px;
    margin-top: 6px;
    opacity: 0.8;
  }

  /* TYPING EFFECT */
  .terminal-line {
    display: inline-block;
    overflow: hidden;
    white-space: nowrap;
    border-right: 2px solid #ff0000;
    animation: typing 3s steps(40) 0.5s both, blink 0.7s step-end infinite;
    color: #ff4444;
    font-size: 13px;
    margin-top: 12px;
  }

  @keyframes typing { from{width:0} to{width:100%} }
  @keyframes blink { 0%,100%{border-color:#ff0000} 50%{border-color:transparent} }

  /* BADGES ROW */
  .badges { display: flex; gap: 8px; justify-content: center; flex-wrap: wrap; margin-top: 16px; }

  .badge {
    background: #1a0000;
    border: 1px solid #ff0000;
    color: #ff4444;
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    padding: 4px 12px;
    letter-spacing: 2px;
    cursor: pointer;
    transition: all 0.2s;
    text-decoration: none;
  }

  .badge:hover { background: #ff0000; color: #000; box-shadow: 0 0 10px #ff000066; }

  /* SECTION */
  .section { margin: 28px 0; }

  .section-header {
    color: #ff0000;
    font-size: 14px;
    letter-spacing: 2px;
    border-left: 3px solid #ff0000;
    padding-left: 12px;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .section-header::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, #2a0000, transparent);
  }

  /* PROFILE CARD */
  .profile-card {
    background: #0d0000;
    border: 1px solid #2a0000;
    border-left: 3px solid #ff0000;
    padding: 16px 20px;
    position: relative;
    overflow: hidden;
  }

  .profile-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(90deg, #ff0000, transparent);
  }

  .profile-row { display: flex; gap: 6px; margin-bottom: 4px; }
  .profile-key { color: #ff4444; min-width: 100px; }
  .profile-val { color: #ccc; }

  /* SKILL TABLE */
  .skill-table { width: 100%; border-collapse: collapse; }

  .skill-table th {
    color: #ff0000;
    font-size: 10px;
    letter-spacing: 2px;
    padding: 6px 10px;
    text-align: left;
    border-bottom: 1px solid #2a0000;
    background: #0d0000;
  }

  .skill-table td {
    padding: 8px 10px;
    border-bottom: 1px solid #150000;
    vertical-align: middle;
    font-size: 12px;
  }

  .skill-table tr:hover td { background: #120000; }

  .threat-badge {
    font-size: 9px;
    padding: 2px 8px;
    letter-spacing: 1px;
    border: 1px solid;
    display: inline-block;
  }

  .threat-critical { color: #ff0000; border-color: #ff0000; background: #1a0000; }
  .threat-high { color: #ff6600; border-color: #ff6600; background: #1a0800; }
  .threat-medium { color: #ffaa00; border-color: #ffaa00; background: #1a1000; }
  .threat-standard { color: #00aa00; border-color: #00aa00; background: #001a00; }

  .vector-name { color: #ff4444; font-weight: bold; }
  .tools-list { color: #888; font-size: 11px; }

  /* PROJECT CARDS */
  .projects-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

  .project-card {
    background: #0d0000;
    border: 1px solid #2a0000;
    padding: 14px;
    position: relative;
    transition: border-color 0.2s;
    cursor: pointer;
  }

  .project-card:hover { border-color: #ff0000; box-shadow: 0 0 15px #ff000022; }

  .project-card::before {
    content: attr(data-status);
    position: absolute;
    top: 8px; right: 10px;
    font-size: 9px;
    color: #ff0000;
    letter-spacing: 1px;
  }

  .project-title { color: #ff4444; font-size: 13px; margin-bottom: 8px; }

  .project-meta {
    font-size: 10px;
    color: #555;
    border-left: 2px solid #2a0000;
    padding-left: 8px;
    margin-bottom: 8px;
    line-height: 1.8;
  }

  .project-desc { color: #888; font-size: 11px; line-height: 1.5; }

  /* STATS ROW */
  .stats-row { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; }

  .stat-card {
    background: #0d0000;
    border: 1px solid #2a0000;
    padding: 12px;
    text-align: center;
    transition: border-color 0.2s;
    animation: pulse 3s ease-in-out infinite;
  }

  @keyframes pulse { 0%,100%{border-color:#1a0000} 50%{border-color:#440000} }

  .stat-card:nth-child(2) { animation-delay: 0.5s; }
  .stat-card:nth-child(3) { animation-delay: 1s; }
  .stat-card:nth-child(4) { animation-delay: 1.5s; }

  .stat-num { font-family: 'Orbitron', monospace; font-size: 24px; color: #ff0000; font-weight: 700; }
  .stat-label { color: #555; font-size: 10px; letter-spacing: 1px; margin-top: 4px; }

  /* ATTACK MATRIX */
  .matrix { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 1px; background: #2a0000; border: 1px solid #2a0000; }

  .matrix-col { background: #080808; padding: 12px; }
  .matrix-col-header { color: #ff0000; font-size: 10px; letter-spacing: 2px; margin-bottom: 8px; padding-bottom: 6px; border-bottom: 1px solid #2a0000; }
  .matrix-item { color: #777; font-size: 11px; padding: 3px 0; border-bottom: 1px solid #110000; }
  .matrix-item:last-child { border: none; }
  .matrix-item::before { content: '▸ '; color: #440000; }

  /* FOOTER */
  .footer {
    text-align: center;
    padding: 24px 0;
    border-top: 1px solid #1a0000;
    color: #333;
    font-size: 11px;
    letter-spacing: 1px;
  }

  .footer span { color: #ff0000; }

  /* CURSOR BLINK */
  .cursor::after { content: '█'; animation: blink 0.8s step-end infinite; color: #ff0000; }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  /* CORNER DECORATION */
  .corner-box {
    position: relative;
  }
  .corner-box::before, .corner-box::after {
    content: '';
    position: absolute;
    width: 8px;
    height: 8px;
    border-color: #ff0000;
    border-style: solid;
  }
  .corner-box::before { top: 0; left: 0; border-width: 1px 0 0 1px; }
  .corner-box::after { bottom: 0; right: 0; border-width: 0 1px 1px 0; }

  /* SCROLLING TICKER */
  .ticker-wrap {
    overflow: hidden;
    background: #0d0000;
    border-top: 1px solid #2a0000;
    border-bottom: 1px solid #2a0000;
    padding: 6px 0;
    margin: 20px 0;
  }

  .ticker {
    display: inline-block;
    white-space: nowrap;
    animation: ticker 25s linear infinite;
    color: #ff4444;
    font-size: 11px;
    letter-spacing: 2px;
  }

  @keyframes ticker { 0%{transform:translateX(100vw)} 100%{transform:translateX(-100%)} }

  .sep { color: #440000; margin: 0 20px; }
</style>
</head>
<body>
<div class="container">

  <!-- HEADER -->
  <div class="header">
    <div class="name">SHIVAM PATEL</div>
    <div class="subtitle">RED TEAM · THREAT RESEARCH · ADVERSARIAL AI · DIGITAL FORENSICS</div>
    <div class="terminal-line">> Cybersecurity Researcher &amp; Penetration Tester | New Delhi, India</div>
    <div class="badges" style="margin-top:16px">
      <a class="badge" href="#">⬡ LINKEDIN</a>
      <a class="badge" href="#">⬡ GITHUB</a>
      <a class="badge" href="#">⬡ EMAIL</a>
      <a class="badge" href="#">⬡ RECON HITS: 1337</a>
    </div>
  </div>

  <!-- TICKER -->
  <div class="ticker-wrap">
    <span class="ticker">
      [INIT] Establishing covert channel...
      <span class="sep">///</span>
      [SCAN] Target enumeration complete
      <span class="sep">///</span>
      [EXPLOIT] CVE-2024-XXXX — Privilege escalation successful
      <span class="sep">///</span>
      [POST-EX] Maintaining persistence...
      <span class="sep">///</span>
      [REPORT] Ethically disclosing all findings 🔐
      <span class="sep">///</span>
      [STATUS] M.Sc. Cyber Security @ NFSU — ACTIVE
      <span class="sep">///</span>
      [MISSION] Break things ethically to build them safer
      <span class="sep">///</span>
    </span>
  </div>

  <!-- WHOAMI -->
  <div class="section">
    <div class="section-header">&gt; whoami</div>
    <div class="profile-card corner-box">
      <div class="profile-row"><span class="profile-key">HANDLE</span><span class="profile-val">ShivamPatel8800</span></div>
      <div class="profile-row"><span class="profile-key">ROLE</span><span class="profile-val">Red Teamer &amp; Cybersecurity Researcher</span></div>
      <div class="profile-row"><span class="profile-key">LOCATION</span><span class="profile-val">New Delhi, India 🇮🇳</span></div>
      <div class="profile-row"><span class="profile-key">STATUS</span><span class="profile-val" style="color:#ff0000">M.Sc. Cyber Security @ NFSU [ACTIVE]</span></div>
      <div class="profile-row"><span class="profile-key">CLEARANCE</span><span class="profile-val">PENTESTER · FORENSICS · AI-RED-TEAM</span></div>
      <div class="profile-row"><span class="profile-key">MOTIVE</span><span class="profile-val">Hack ethically. Break to build better.</span></div>
      <div style="margin-top:10px; color:#333; font-size:11px" class="cursor">&gt; </div>
    </div>
  </div>

  <!-- STATS -->
  <div class="section">
    <div class="section-header">&gt; ./stats --quick</div>
    <div class="stats-row">
      <div class="stat-card"><div class="stat-num">5+</div><div class="stat-label">PUBLICATIONS</div></div>
      <div class="stat-card"><div class="stat-num">4</div><div class="stat-label">ACTIVE PROJECTS</div></div>
      <div class="stat-card"><div class="stat-num">3</div><div class="stat-label">INTERNSHIPS</div></div>
      <div class="stat-card"><div class="stat-num">8.18</div><div class="stat-label">CGPA (M.Sc.)</div></div>
    </div>
  </div>

  <!-- SKILLS -->
  <div class="section">
    <div class="section-header">&gt; nmap --scan-capabilities -sV</div>
    <table class="skill-table">
      <thead>
        <tr>
          <th>ATTACK VECTOR</th>
          <th>TOOLS & TECHNIQUES</th>
          <th>THREAT LVL</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><span class="vector-name">🔴 Penetration Testing</span></td>
          <td><span class="tools-list">Metasploit · Burp Suite · Nmap · SQLMap · BeEF</span></td>
          <td><span class="threat-badge threat-critical">CRITICAL</span></td>
        </tr>
        <tr>
          <td><span class="vector-name">🔴 Network Exploitation</span></td>
          <td><span class="tools-list">Wireshark · Aircrack-NG · IDS/IPS · MITRE ATT&CK</span></td>
          <td><span class="threat-badge threat-critical">CRITICAL</span></td>
        </tr>
        <tr>
          <td><span class="vector-name">🟠 AI / LLM Red Teaming</span></td>
          <td><span class="tools-list">Prompt Injection · Jailbreaks · RAG Poisoning · Adversarial ML</span></td>
          <td><span class="threat-badge threat-high">HIGH</span></td>
        </tr>
        <tr>
          <td><span class="vector-name">🟠 Blockchain Security</span></td>
          <td><span class="tools-list">Mythril · Remix IDE · Smart Contract Auditing · zkSNARKs</span></td>
          <td><span class="threat-badge threat-high">HIGH</span></td>
        </tr>
        <tr>
          <td><span class="vector-name">🟡 Digital Forensics</span></td>
          <td><span class="tools-list">Autopsy · FTK Imager · Volatility · YARA · Cellebrite · AXIOM</span></td>
          <td><span class="threat-badge threat-medium">MEDIUM</span></td>
        </tr>
        <tr>
          <td><span class="vector-name">🟡 Vuln Assessment</span></td>
          <td><span class="tools-list">Nessus · OpenVAS · LinPEAS · WinPEAS</span></td>
          <td><span class="threat-badge threat-medium">MEDIUM</span></td>
        </tr>
        <tr>
          <td><span class="vector-name">🟢 SIEM & Monitoring</span></td>
          <td><span class="tools-list">Wazuh · Log-360 · Log Parsing · SOC Operations</span></td>
          <td><span class="threat-badge threat-standard">STANDARD</span></td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- PROJECTS -->
  <div class="section">
    <div class="section-header">&gt; ls /ops/active-exploits</div>
    <div class="projects-grid">
      <div class="project-card" data-status="● DEPLOYED">
        <div class="project-title">⛓ Confidential Invoice Financing</div>
        <div class="project-meta">
          VECTOR: Zero-Knowledge Cryptography<br>
          STACK: zk-SNARKs · Circom · Hyperledger Fabric
        </div>
        <div class="project-desc">ZK proof protocol verifying credit limits without leaking invoice data on-chain.</div>
      </div>
      <div class="project-card" data-status="● LIVE">
        <div class="project-title">🌿 Eco Blockchain Consensus</div>
        <div class="project-meta">
          VECTOR: Consensus Mechanism Research<br>
          STACK: Ethereum · Solidity · DeFi
        </div>
        <div class="project-desc">Proof-of-Environmentalism — eco-activities trigger verifiable on-chain reward distribution.</div>
      </div>
      <div class="project-card" data-status="● ACTIVE">
        <div class="project-title">🔐 Linux Endpoint Hardening</div>
        <div class="project-meta">
          VECTOR: Endpoint Compromise / Lateral Movement<br>
          STACK: Python · Bash · SHA-256 Integrity
        </div>
        <div class="project-desc">CLI framework: file integrity monitoring, anomaly detection, auto-threat remediation.</div>
      </div>
      <div class="project-card" data-status="● ACTIVE">
        <div class="project-title">🔍 PII Detection Pipeline</div>
        <div class="project-meta">
          VECTOR: Data Exfiltration / DLP Bypass<br>
          STACK: RabbitMQ · SpaCy · Presidio · Docker
        </div>
        <div class="project-desc">Zero-latency DLP via TCP proxy + async queue. Hybrid NLP + regex in fail-secure design.</div>
      </div>
    </div>
  </div>

  <!-- ATTACK MATRIX -->
  <div class="section">
    <div class="section-header">&gt; enum --attack-vectors</div>
    <div class="matrix">
      <div class="matrix-col">
        <div class="matrix-col-header">🔴 OFFENSIVE</div>
        <div class="matrix-item">Web App Pentesting</div>
        <div class="matrix-item">Network Exploitation</div>
        <div class="matrix-item">Bug Bounty Hunting</div>
        <div class="matrix-item">API Security Testing</div>
        <div class="matrix-item">Red Teaming</div>
        <div class="matrix-item">Social Engineering</div>
      </div>
      <div class="matrix-col">
        <div class="matrix-col-header">🔵 DEFENSIVE</div>
        <div class="matrix-item">Digital Forensics</div>
        <div class="matrix-item">Incident Response</div>
        <div class="matrix-item">SIEM & Log Analysis</div>
        <div class="matrix-item">Malware Analysis</div>
        <div class="matrix-item">Cloud Hardening</div>
        <div class="matrix-item">Threat Intelligence</div>
      </div>
      <div class="matrix-col">
        <div class="matrix-col-header">🟡 RESEARCH</div>
        <div class="matrix-item">AI / LLM Security</div>
        <div class="matrix-item">Smart Contract Audit</div>
        <div class="matrix-item">Zero Knowledge Proofs</div>
        <div class="matrix-item">Blockchain Security</div>
        <div class="matrix-item">AI Red Teaming</div>
        <div class="matrix-item">Adversarial ML</div>
      </div>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="footer">
    <div style="font-family:'Orbitron',monospace; font-size:10px; letter-spacing:4px; color:#440000; margin-bottom:8px">BREAKING THINGS ETHICALLY TO BUILD THEM SAFER</div>
    <div>Drop a <span>⭐</span> if my work adds value — it's the highest privilege you can escalate to.</div>
    <div style="margin-top:12px; color:#222">uid=1337(shivam) gid=1337(security) <span style="color:#330000">// All activities ethical & authorized</span></div>
  </div>

</div>

<script>
  // Glitch effect on stat numbers
  document.querySelectorAll('.stat-num').forEach(el => {
    const orig = el.textContent;
    setInterval(() => {
      if (Math.random() > 0.97) {
        el.textContent = Math.random().toString(36).substring(2,6).toUpperCase();
        setTimeout(() => el.textContent = orig, 80);
      }
    }, 500);
  });

  // Random flicker on matrix items
  document.querySelectorAll('.matrix-item').forEach(el => {
    setInterval(() => {
      if (Math.random() > 0.995) {
        el.style.color = '#ff4444';
        setTimeout(() => el.style.color = '', 100);
      }
    }, 300);
  });
</script>
</body>
</html>
