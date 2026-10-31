<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>F.6 English Grammar Academy</title>
  <style>
    :root {
      --primary: #2563eb;
      --primary-dark: #1d4ed8;
      --secondary: #0ea5e9;
      --success: #16a34a;
      --danger: #dc2626;
      --bg: #f8fafc;
      --card-bg: #ffffff;
      --text: #1e293b;
      --text-muted: #64748b;
      --border: #cbd5e1;
      --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    }
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    }
    body {
      background-color: var(--bg);
      color: var(--text);
      line-height: 1.5;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }
    header {
      background: linear-gradient(135deg, #1e3a8a, #3b82f6);
      color: white;
      padding: 1rem 1.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: var(--shadow);
    }
    header h1 {
      font-size: 1.3rem;
      font-weight: 700;
    }
    .header-actions {
      display: flex;
      gap: 0.5rem;
      align-items: center;
    }
    button {
      cursor: pointer;
      border: none;
      border-radius: 8px;
      padding: 0.55rem 1.1rem;
      font-weight: 600;
      font-size: 0.9rem;
      transition: all 0.2s ease;
    }
    .btn-primary { background-color: var(--primary); color: white; }
    .btn-primary:hover { background-color: var(--primary-dark); }
    .btn-secondary { background-color: #e2e8f0; color: var(--text); }
    .btn-secondary:hover { background-color: #cbd5e1; }
    .btn-danger { background-color: var(--danger); color: white; }
    .btn-teacher { background-color: #475569; color: #f8fafc; font-size: 0.8rem; }
    main {
      flex: 1;
      max-width: 950px;
      width: 100%;
      margin: 1.5rem auto;
      padding: 0 1rem;
    }
    .view-panel { display: none; }
    .view-panel.active { display: block !important; }
    .card {
      background: var(--card-bg);
      border-radius: 12px;
      border: 1px solid var(--border);
      padding: 1.5rem;
      box-shadow: var(--shadow);
      margin-bottom: 1.5rem;
    }
    /* Avatar Grid Selection */
    .avatar-selection-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 0.75rem;
      margin: 0.75rem 0 1rem 0;
    }
    @media (max-width: 600px) {
      .avatar-selection-grid { grid-template-columns: repeat(2, 1fr); }
    }
    .avatar-card {
      background: #f8fafc;
      border: 2px solid #cbd5e1;
      border-radius: 10px;
      padding: 0.8rem 0.5rem;
      text-align: center;
      cursor: pointer;
      position: relative;
    }
    .avatar-card:hover {
      border-color: var(--secondary);
      background: #f0f9ff;
    }
    .avatar-card.active {
      border-color: var(--primary);
      background: #eff6ff;
      box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
    }
    .avatar-card.active::after {
      content: "✔";
      position: absolute;
      top: 5px;
      right: 5px;
      background: var(--primary);
      color: white;
      border-radius: 50%;
      width: 18px;
      height: 18px;
      font-size: 0.7rem;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
    }
    .avatar-card-icon { font-size: 2.3rem; display: block; margin-bottom: 0.2rem; }
    .avatar-card-name { font-size: 0.85rem; font-weight: 700; }

    /* Dashboard Avatar Showcase & Wearables */
    .avatar-showcase {
      display: flex;
      align-items: center;
      gap: 1.5rem;
      background: linear-gradient(135deg, #eff6ff, #dbeafe);
      border: 2px dashed #93c5fd;
      border-radius: 16px;
      padding: 1.25rem 1.5rem;
      margin-bottom: 1.5rem;
    }
    .avatar-frame {
      width: 90px;
      height: 90px;
      border-radius: 50%;
      background: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 3.2rem;
      box-shadow: 0 4px 10px rgba(0,0,0,0.12);
      position: relative;
      flex-shrink: 0;
      user-select: none;
    }
    .wearable-item {
      position: absolute;
      pointer-events: none;
      line-height: 1;
      filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.25));
      transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
    }
    .wearable-head {
      top: -16px;
      font-size: 2rem;
      left: 50%;
      transform: translateX(-50%);
      z-index: 5;
    }
    .wearable-eyes {
      top: 26px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 1.5rem;
      z-index: 6;
    }
    .wearable-neck {
      bottom: -6px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 1.8rem;
      z-index: 7;
    }
    .wearable-badge {
      top: 4px;
      left: -6px;
      font-size: 1.4rem;
      z-index: 8;
    }
    .avatar-gear-badge {
      position: absolute;
      bottom: -3px;
      right: -3px;
      background: #f59e0b;
      color: white;
      border-radius: 50%;
      width: 24px;
      height: 24px;
      font-size: 0.75rem;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      z-index: 9;
    }
    .accessory-chip {
      background: white;
      border: 1px solid #cbd5e1;
      border-radius: 20px;
      padding: 0.25rem 0.75rem;
      font-size: 0.8rem;
      font-weight: 600;
      display: inline-flex;
      align-items: center;
      gap: 0.35rem;
      margin-right: 0.4rem;
      margin-top: 0.4rem;
      box-shadow: 0 1px 2px rgba(0,0,0,0.05);
    }

    /* Topics Grid */
    .grid-2 {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1.25rem;
    }
    .topic-card {
      background: white;
      border-radius: 10px;
      border: 1px solid var(--border);
      padding: 1.25rem;
      box-shadow: var(--shadow);
    }
    .topic-card h3 {
      font-size: 1.1rem;
      margin-bottom: 0.5rem;
      color: var(--primary-dark);
    }
    .stage-buttons {
      display: flex;
      gap: 0.4rem;
      flex-wrap: wrap;
      margin-top: 0.5rem;
    }
    .btn-stage {
      flex: 1;
      min-width: 42px;
      padding: 0.5rem 0.2rem;
      font-size: 0.8rem;
      text-align: center;
      border-radius: 6px;
      background-color: #f1f5f9;
      color: var(--text-muted);
      border: 1px solid #cbd5e1;
    }
    .btn-stage.unlocked {
      background-color: #dbeafe;
      color: var(--primary-dark);
      border-color: #93c5fd;
      cursor: pointer;
      font-weight: 600;
    }
    .btn-stage.cleared {
      background-color: #dcfce7;
      color: #15803d;
      border-color: #86efac;
      cursor: pointer;
      font-weight: 700;
    }

    /* Quiz Area */
    .quiz-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1.25rem;
      border-bottom: 2px solid var(--border);
      padding-bottom: 0.75rem;
    }
    .q-box {
      font-size: 1.25rem;
      font-weight: 600;
      margin-bottom: 1.5rem;
      color: #0f172a;
      min-height: 40px;
    }
    .options-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 0.8rem;
      margin-bottom: 1.5rem;
    }
    @media (max-width: 600px) {
      .options-grid { grid-template-columns: 1fr; }
    }
    .opt-btn {
      padding: 0.9rem;
      text-align: left;
      font-size: 1.05rem;
      border-radius: 8px;
      background: #f8fafc;
      border: 2px solid #cbd5e1;
      color: var(--text);
    }
    .opt-btn:hover:not(:disabled) {
      border-color: var(--primary);
      background-color: #eff6ff;
    }
    .opt-btn.selected {
      border-color: var(--primary);
      background-color: #dbeafe;
      font-weight: 700;
    }
    .progress-bar-container {
      width: 100%;
      height: 8px;
      background-color: #e2e8f0;
      border-radius: 4px;
      overflow: hidden;
      margin-top: 1rem;
    }
    .progress-bar-fill {
      height: 100%;
      background-color: var(--primary);
      width: 0%;
      transition: width 0.2s ease;
    }

    /* Tables */
    .table-container {
      overflow-x: auto;
      margin: 1rem 0;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.9rem;
    }
    th, td {
      padding: 0.65rem 0.85rem;
      border: 1px solid var(--border);
      text-align: left;
    }
    th {
      background-color: #f1f5f9;
      font-weight: 600;
    }
    .badge-correct { color: var(--success); font-weight: 700; }
    .badge-wrong { color: var(--danger); font-weight: 700; }

    /* Modals */
    .modal-overlay {
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0, 0, 0, 0.5);
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }
    .modal-overlay.active { display: flex !important; }
    .modal-content {
      background: white;
      padding: 1.5rem;
      border-radius: 12px;
      max-width: 650px;
      width: 90%;
      max-height: 85vh;
      overflow-y: auto;
    }
  </style>
</head>
<body>
  <header>
    <h1>🎓 F.6 English Mastery</h1>
    <div class="header-actions">
      <button class="btn-secondary" onclick="showDashboard()">Dashboard</button>
      <button class="btn-secondary" onclick="showLeaderboard()">Leaderboard</button>
      <button class="btn-teacher" onclick="openTeacherModal()">🔒 Teacher Backdoor</button>
    </div>
  </header>

  <main>
    <!-- LOGIN VIEW -->
    <section id="login-view" class="view-panel active">
      <div class="card" style="max-width: 500px; margin: 2rem auto;">
        <h2 style="text-align: center; margin-bottom: 0.4rem;">Student Registration</h2>
        <p style="text-align: center; color: var(--text-muted); font-size: 0.9rem; margin-bottom: 1rem;">
          Enter your name and pick your companion avatar to get started.
        </p>
        <div style="margin-bottom: 1rem;">
          <label style="font-weight: 600; font-size: 0.9rem;">Your Name</label>
          <input type="text" id="student-name-input" placeholder="e.g. Alex Wong (6A)" value="Alex Wong" style="width: 100%; padding: 0.7rem; border: 1px solid #cbd5e1; border-radius: 8px; margin-top: 0.3rem; font-size: 1rem;">
        </div>
        <div>
          <label style="font-weight: 600; font-size: 0.9rem;">Choose Companion Avatar</label>
          <div class="avatar-selection-grid">
            <div class="avatar-card active" onclick="pickAvatar('🦁 Leo the Lion', '🦁', this)">
              <span class="avatar-card-icon">🦁</span>
              <div class="avatar-card-name">Leo</div>
            </div>
            <div class="avatar-card" onclick="pickAvatar('🦉 Athena Owl', '🦉', this)">
              <span class="avatar-card-icon">🦉</span>
              <div class="avatar-card-name">Athena</div>
            </div>
            <div class="avatar-card" onclick="pickAvatar('🐬 Echo Dolphin', '🐬', this)">
              <span class="avatar-card-icon">🐬</span>
              <div class="avatar-card-name">Echo</div>
            </div>
            <div class="avatar-card" onclick="pickAvatar('🦊 Felix Fox', '🦊', this)">
              <span class="avatar-card-icon">🦊</span>
              <div class="avatar-card-name">Felix</div>
            </div>
          </div>
        </div>
        <div style="background: #f1f5f9; padding: 0.6rem; border-radius: 8px; text-align: center; margin-bottom: 1.25rem; font-size: 0.9rem;" id="login-companion-preview">
          Selected: <strong>🦁 Leo the Lion</strong>
        </div>
        <button class="btn-primary" style="width: 100%; padding: 0.8rem; font-size: 1rem;" onclick="handleLogin()">Start Practising &rarr;</button>
      </div>
    </section>

    <!-- DASHBOARD VIEW -->
    <section id="dashboard-view" class="view-panel">
      <!-- Companion Showcase with Wearables -->
      <div class="avatar-showcase">
        <div class="avatar-frame">
          <span id="avatar-icon">🦁</span>
          <!-- Dynamic Wearables Overlay -->
          <span class="wearable-item wearable-head" id="wearable-head" style="display: none;"></span>
          <span class="wearable-item wearable-eyes" id="wearable-eyes" style="display: none;"></span>
          <span class="wearable-item wearable-neck" id="wearable-neck" style="display: none;"></span>
          <span class="wearable-item wearable-badge" id="wearable-badge" style="display: none;"></span>
          <span class="avatar-gear-badge" id="avatar-badge-count">0</span>
        </div>
        <div style="flex: 1;">
          <h3 id="avatar-name-display" style="font-size: 1.15rem; color: #1e3a8a;">Companion: Leo the Lion</h3>
          <p id="student-welcome-msg" style="color: var(--text-muted); font-size: 0.85rem;">Pass requirement: 16 / 20 to clear a stage and unlock avatar gear!</p>
          <div id="wardrobe-items" style="margin-top: 0.3rem;">
            <!-- Accessories unlocked rendered here -->
          </div>
        </div>
      </div>

      <div class="grid-2" id="topics-container">
        <!-- Topic cards inserted here -->
      </div>
    </section>

    <!-- QUIZ VIEW -->
    <section id="quiz-view" class="view-panel">
      <div class="card">
        <div class="quiz-header">
          <div>
            <h2 id="quiz-topic-title" style="font-size: 1.2rem;">Grammar Practice</h2>
            <span id="quiz-stage-subtitle" style="color: var(--text-muted); font-size: 0.9rem; font-weight: 600;">Stage 1 &bull; Question 1 of 20</span>
          </div>
          <div>
            <span style="font-weight: 700; color: var(--primary);" id="live-score-display">Score: 0 / 20</span>
          </div>
        </div>
        <div class="q-box" id="question-text">
          Question loading...
        </div>
        <div class="options-grid" id="options-container">
          <!-- Options -->
        </div>
        <div style="display: flex; justify-content: space-between; align-items: center; margin-top: 1rem;">
          <button class="btn-secondary" onclick="abortQuiz()">Back to Menu</button>
          <button class="btn-primary" id="btn-next-question" onclick="submitCurrentQuestion()" disabled>Next Question &rarr;</button>
        </div>
        <div class="progress-bar-container">
          <div class="progress-bar-fill" id="quiz-progress-fill"></div>
        </div>
      </div>
    </section>

    <!-- RESULT VIEW -->
    <section id="result-view" class="view-panel">
      <div class="card">
        <div style="text-align: center; margin-bottom: 1.5rem;" id="result-banner">
          <!-- Banner -->
        </div>
        <h3 style="margin-bottom: 0.5rem; font-size: 1.1rem;">Answers & Review</h3>
        <p style="font-size: 0.85rem; color: var(--text-muted); margin-bottom: 1rem;">
          Here are the answers for all 20 questions in this stage:
        </p>
        <div class="table-container">
          <table>
            <thead>
              <tr>
                <th style="width: 5%;">#</th>
                <th style="width: 45%;">Question Prompt</th>
                <th style="width: 20%;">Your Answer</th>
                <th style="width: 20%;">Correct Answer</th>
                <th style="width: 10%;">Result</th>
              </tr>
            </thead>
            <tbody id="review-table-body">
              <!-- Reviews -->
            </tbody>
          </table>
        </div>
        <div style="display: flex; justify-content: flex-end; gap: 0.75rem; margin-top: 1.25rem;" id="result-action-buttons">
          <!-- Buttons -->
        </div>
      </div>
    </section>

    <!-- LEADERBOARD VIEW -->
    <section id="leaderboard-view" class="view-panel">
      <div class="card">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem;">
          <h2>🏆 Academy Leaderboard</h2>
          <button class="btn-secondary" onclick="showDashboard()">Dashboard</button>
        </div>
        <p style="color: var(--text-muted); font-size: 0.85rem; margin-bottom: 1rem;">
          Rankings are based on stages cleared (16/20 or above) and total points.
        </p>
        <div class="table-container">
          <table>
            <thead>
              <tr>
                <th>Rank</th>
                <th>Student Name</th>
                <th>Companion</th>
                <th>Stages Cleared</th>
                <th>Total Score</th>
              </tr>
            </thead>
            <tbody id="leaderboard-tbody">
              <!-- Records -->
            </tbody>
          </table>
        </div>
      </div>
    </section>
  </main>

  <!-- TEACHER BACKDOOR MODAL (PIN HINT REMOVED) -->
  <div class="modal-overlay" id="teacher-modal">
    <div class="modal-content">
      <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem;">
        <h3>🔒 Teacher Administration Backdoor</h3>
        <button class="btn-secondary" style="padding: 0.2rem 0.6rem;" onclick="closeTeacherModal()">&times;</button>
      </div>
      <div id="teacher-auth-box">
        <p style="font-size: 0.9rem; color: var(--text-muted); margin-bottom: 0.6rem;">Enter Teacher Master PIN:</p>
        <div style="display: flex; gap: 0.5rem;">
          <input type="password" id="teacher-pin-input" placeholder="Enter PIN" style="flex: 1; padding: 0.55rem; border: 1px solid #cbd5e1; border-radius: 6px;">
          <button class="btn-primary" onclick="verifyTeacherPin()">Unlock</button>
        </div>
      </div>
      <div id="teacher-portal-body" style="display: none;">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem;">
          <h4>Student Progress Records</h4>
          <button class="btn-danger" onclick="clearLeaderboardData()">⚠️ Clear Leaderboard & Reset</button>
        </div>
        <div class="table-container">
          <table>
            <thead>
              <tr>
                <th>Student</th>
                <th>Stages Cleared</th>
                <th>Avg Score</th>
                <th>Accessories</th>
              </tr>
            </thead>
            <tbody id="teacher-student-progress-tbody">
              <!-- Student diagnostic data -->
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

  <script>
    /* Safe In-Memory Storage */
    let memoryStore = {};
    const safeStore = {
      get: function(k) {
        try { return localStorage.getItem(k) || memoryStore[k] || null; }
        catch(e) { return memoryStore[k] || null; }
      },
      set: function(k, v) {
        try { localStorage.setItem(k, v); } catch(e) {}
        memoryStore[k] = v;
      },
      del: function(k) {
        try { localStorage.removeItem(k); } catch(e) {}
        delete memoryStore[k];
      }
    };

    const PASSING_THRESHOLD = 16;
    const TEACHER_PIN = "F6ENG2026";
    const TOPICS = ["Prepositions", "Word Formation", "Tenses", "Articles", "Plurals"];

    let state = {
      currentUser: null,
      selectedAvatar: "🦁 Leo the Lion",
      avatarIcon: "🦁",
      currentTopic: null,
      currentStage: 1,
      currentQuestionIdx: 0,
      currentScore: 0,
      selectedOption: null,
      activeQuestionSet: [],
      stageAnswerLog: []
    };

    // Accessories awarded upon clearing Stage 1 to Stage 5 with wear slot mappings
    const stageAccessories = {
      1: { name: "Cadet Cap", icon: "🧢", slot: "head" },
      2: { name: "Study Glasses", icon: "👓", slot: "eyes" },
      3: { name: "Star Badge", icon: "⭐", slot: "badge" },
      4: { name: "Hero Cape", icon: "🧣", slot: "neck" },
      5: { name: "Champion Crown", icon: "👑", slot: "head" }
    };

    function pickAvatar(name, icon, el) {
      state.selectedAvatar = name;
      state.avatarIcon = icon;
      document.querySelectorAll(".avatar-card").forEach(c => c.classList.remove("active"));
      if (el) el.classList.add("active");
      const preview = document.getElementById("login-companion-preview");
      if (preview) preview.innerHTML = `Selected: <strong>${name}</strong>`;
    }

    const questionRepo = {};
    function buildEasyRepository() {
      const data = {
        "Prepositions": {
          1: [
            { q: "She is very good _____ English.", a: "at", d: ["in", "on", "for"] },
            { q: "I am interested _____ sports.", a: "in", d: ["at", "on", "to"] },
            { q: "Listen _____ your teacher.", a: "to", d: ["at", "for", "with"] },
            { q: "He arrived _____ school early today.", a: "at", d: ["in", "to", "on"] },
            { q: "The meeting will be held _____ Friday.", a: "on", d: ["in", "at", "by"] },
            { q: "Are you afraid _____ dogs?", a: "of", d: ["with", "to", "about"] },
            { q: "I completely agree _____ you.", a: "with", d: ["to", "at", "on"] },
            { q: "Please wait _____ me outside the gate.", a: "for", d: ["to", "with", "at"] },
            { q: "He was born _____ May.", a: "in", d: ["on", "at", "for"] },
            { q: "The book is _____ the desk.", a: "on", d: ["in", "at", "to"] },
            { q: "She smiled _____ him kindly.", a: "at", d: ["to", "on", "with"] },
            { q: "Thank you _____ your help.", a: "for", d: ["to", "of", "with"] },
            { q: "He is proud _____ his daughter.", a: "of", d: ["with", "at", "for"] },
            { q: "I am tired _____ doing homework.", a: "of", d: ["with", "from", "at"] },
            { q: "Pay attention _____ the whiteboard.", a: "to", d: ["at", "on", "in"] },
            { q: "He borrowed a pen _____ his classmate.", a: "from", d: ["to", "at", "with"] },
            { q: "Look _____ the blackboard, please.", a: "at", d: ["to", "on", "in"] },
            { q: "We walked _____ the park together.", a: "in", d: ["at", "on", "to"] },
            { q: "She apologized _____ being late.", a: "for", d: ["to", "about", "at"] },
            { q: "They arrived in Hong Kong _____ 8 o'clock.", a: "at", d: ["in", "on", "for"] }
          ],
          2: [
            { q: "He is responsible _____ cleaning the classroom.", a: "for", d: ["to", "with", "about"] },
            { q: "She complained _____ the cold weather.", a: "about", d: ["for", "with", "to"] },
            { q: "According _____ the news, it will rain tomorrow.", a: "to", d: ["with", "by", "at"] },
            { q: "He applied _____ a student helper job.", a: "for", d: ["to", "in", "with"] },
            { q: "Smoking is bad _____ your health.", a: "for", d: ["to", "at", "with"] },
            { q: "She prefers tea _____ coffee.", a: "to", d: ["than", "over", "against"] },
            { q: "Don't worry _____ the exam results.", a: "about", d: ["for", "to", "with"] },
            { q: "He is capable _____ getting an A grade.", a: "of", d: ["to", "for", "in"] },
            { q: "We rely _____ our parents for guidance.", a: "on", d: ["in", "at", "to"] },
            { q: "She 
