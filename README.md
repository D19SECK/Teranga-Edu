# Teranga-Edu
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="Content-Security-Policy" content="default-src 'self' 'unsafe-inline' https://fonts.googleapis.com https://fonts.gstatic.com; script-src 'self' 'unsafe-inline';">
<meta http-equiv="X-Content-Type-Options" content="nosniff">
<meta http-equiv="X-Frame-Options" content="DENY">
<meta http-equiv="Referrer-Policy" content="no-referrer">
<title>EduTrack — Système de Gestion des Étudiants</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
/* ══════════════════════════════════════
   DESIGN SYSTEM — INDUSTRIAL DARK
   ══════════════════════════════════════ */
:root {
  --bg:        #0a0a0f;
  --bg2:       #111118;
  --bg3:       #18181f;
  --border:    #2a2a35;
  --accent:    #00e5a0;
  --accent2:   #7b61ff;
  --danger:    #ff4d6d;
  --warn:      #ffb703;
  --text:      #e8e8f0;
  --text2:     #8888a0;
  --text3:     #4a4a60;
  --font-head: 'Syne', sans-serif;
  --font-mono: 'Space Mono', monospace;
  --radius:    6px;
  --shadow:    0 8px 32px rgba(0,0,0,.6);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-mono);
  font-size: 14px;
  min-height: 100vh;
  overflow-x: hidden;
}

/* ── GRID BACKGROUND ── */
body::before {
  content: '';
  position: fixed; inset: 0;
  background-image:
    linear-gradient(rgba(0,229,160,.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,229,160,.03) 1px, transparent 1px);
  background-size: 40px 40px;
  pointer-events: none;
  z-index: 0;
}

/* ── NOISE OVERLAY ── */
body::after {
  content: '';
  position: fixed; inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 0;
  opacity: .4;
}

/* ══════════════════════════════
   LAYOUT
   ══════════════════════════════ */
#app { position: relative; z-index: 1; display: flex; flex-direction: column; min-height: 100vh; }

/* ── TOP BAR ── */
header {
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 32px;
  height: 64px;
  background: rgba(10,10,15,.9);
  border-bottom: 1px solid var(--border);
  backdrop-filter: blur(12px);
  position: sticky; top: 0; z-index: 100;
}

.logo {
  font-family: var(--font-head);
  font-size: 22px;
  font-weight: 800;
  letter-spacing: -0.5px;
  color: var(--text);
}
.logo span { color: var(--accent); }

.header-badges { display: flex; gap: 8px; align-items: center; }

.badge {
  padding: 3px 10px;
  border-radius: 3px;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: .08em;
  text-transform: uppercase;
}
.badge-secure { background: rgba(0,229,160,.12); color: var(--accent); border: 1px solid rgba(0,229,160,.3); }
.badge-local  { background: rgba(123,97,255,.12); color: var(--accent2); border: 1px solid rgba(123,97,255,.3); }

/* ── MAIN CONTENT ── */
main { flex: 1; padding: 32px; max-width: 1400px; margin: 0 auto; width: 100%; }

/* ── STAT CARDS ── */
.stats-row {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  margin-bottom: 32px;
}

.stat-card {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 20px 24px;
  position: relative;
  overflow: hidden;
  transition: border-color .2s;
}
.stat-card:hover { border-color: var(--accent); }
.stat-card::before {
  content: '';
  position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, var(--accent), var(--accent2));
  opacity: 0; transition: opacity .2s;
}
.stat-card:hover::before { opacity: 1; }

.stat-label {
  font-size: 10px;
  letter-spacing: .1em;
  text-transform: uppercase;
  color: var(--text2);
  margin-bottom: 8px;
}
.stat-value {
  font-family: var(--font-head);
  font-size: 32px;
  font-weight: 800;
  color: var(--text);
  line-height: 1;
}
.stat-sub { font-size: 11px; color: var(--text3); margin-top: 6px; }
.stat-accent { color: var(--accent); }
.stat-danger  { color: var(--danger); }
.stat-warn    { color: var(--warn); }

/* ── TWO-COL LAYOUT ── */
.layout-grid {
  display: grid;
  grid-template-columns: 360px 1fr;
  gap: 24px;
}

/* ── PANEL ── */
.panel {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  overflow: hidden;
}

.panel-header {
  display: flex; align-items: center; justify-content: space-between;
  padding: 14px 20px;
  border-bottom: 1px solid var(--border);
  background: var(--bg3);
}

.panel-title {
  font-family: var(--font-head);
  font-size: 13px;
  font-weight: 700;
  letter-spacing: .06em;
  text-transform: uppercase;
  color: var(--text);
}

.panel-body { padding: 20px; }

/* ── FORM ── */
.form-group { margin-bottom: 16px; }

label {
  display: block;
  font-size: 10px;
  letter-spacing: .1em;
  text-transform: uppercase;
  color: var(--text2);
  margin-bottom: 6px;
}

input, select {
  width: 100%;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  color: var(--text);
  font-family: var(--font-mono);
  font-size: 13px;
  padding: 10px 12px;
  outline: none;
  transition: border-color .15s, box-shadow .15s;
}
input:focus, select:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(0,229,160,.1);
}
input.error { border-color: var(--danger); }
input.ok    { border-color: var(--accent); }

.field-error {
  font-size: 11px;
  color: var(--danger);
  margin-top: 4px;
  display: none;
}
.field-error.show { display: block; }

select option { background: var(--bg3); }

/* ── BUTTONS ── */
.btn {
  display: inline-flex; align-items: center; justify-content: center; gap: 6px;
  padding: 10px 18px;
  border-radius: var(--radius);
  font-family: var(--font-mono);
  font-size: 12px;
  font-weight: 700;
  letter-spacing: .06em;
  text-transform: uppercase;
  cursor: pointer;
  border: none;
  transition: all .15s;
  white-space: nowrap;
}
.btn:active { transform: scale(.97); }

.btn-primary {
  background: var(--accent);
  color: #000;
  width: 100%;
}
.btn-primary:hover { background: #00ffc0; box-shadow: 0 0 20px rgba(0,229,160,.3); }

.btn-ghost {
  background: transparent;
  color: var(--text2);
  border: 1px solid var(--border);
}
.btn-ghost:hover { border-color: var(--text2); color: var(--text); }

.btn-danger {
  background: transparent;
  color: var(--danger);
  border: 1px solid rgba(255,77,109,.3);
  padding: 6px 12px;
  font-size: 11px;
}
.btn-danger:hover { background: rgba(255,77,109,.1); }

.btn-edit {
  background: transparent;
  color: var(--accent2);
  border: 1px solid rgba(123,97,255,.3);
  padding: 6px 12px;
  font-size: 11px;
}
.btn-edit:hover { background: rgba(123,97,255,.1); }

.btn-row { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 8px; }

/* ── SEARCH BAR ── */
.search-bar {
  display: flex; gap: 8px;
  margin-bottom: 16px;
}
.search-bar input { flex: 1; }

/* ── TABLE ── */
.table-wrap { overflow-x: auto; }

table {
  width: 100%;
  border-collapse: collapse;
}

thead tr {
  background: var(--bg3);
  border-bottom: 1px solid var(--border);
}

th {
  padding: 10px 14px;
  text-align: left;
  font-size: 10px;
  letter-spacing: .12em;
  text-transform: uppercase;
  color: var(--text3);
  white-space: nowrap;
  cursor: pointer;
  user-select: none;
}
th:hover { color: var(--accent); }

td {
  padding: 12px 14px;
  border-bottom: 1px solid rgba(42,42,53,.6);
  font-size: 13px;
  vertical-align: middle;
}

tr:hover td { background: rgba(255,255,255,.02); }

.td-id   { color: var(--text3); font-size: 11px; }
.td-name { font-family: var(--font-head); font-weight: 600; }
.td-moy  { font-weight: 700; }

.chip {
  display: inline-block;
  padding: 2px 8px;
  border-radius: 3px;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: .06em;
  text-transform: uppercase;
}
.chip-ok  { background: rgba(0,229,160,.12); color: var(--accent); }
.chip-bad { background: rgba(255,77,109,.12); color: var(--danger); }

.empty-state {
  text-align: center;
  padding: 48px 20px;
  color: var(--text3);
  font-size: 13px;
}
.empty-state .icon { font-size: 32px; margin-bottom: 12px; }

/* ── MODAL ── */
.modal-overlay {
  position: fixed; inset: 0;
  background: rgba(0,0,0,.8);
  backdrop-filter: blur(4px);
  z-index: 200;
  display: flex; align-items: center; justify-content: center;
  opacity: 0; pointer-events: none;
  transition: opacity .2s;
}
.modal-overlay.open { opacity: 1; pointer-events: all; }

.modal {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 10px;
  width: 100%;
  max-width: 520px;
  max-height: 90vh;
  overflow-y: auto;
  transform: translateY(16px) scale(.97);
  transition: transform .2s;
  box-shadow: var(--shadow);
}
.modal-overlay.open .modal { transform: translateY(0) scale(1); }

.modal-header {
  display: flex; align-items: center; justify-content: space-between;
  padding: 20px 24px 0;
}
.modal-title {
  font-family: var(--font-head);
  font-size: 18px;
  font-weight: 800;
}
.modal-close {
  background: none; border: none; color: var(--text2);
  font-size: 20px; cursor: pointer; padding: 4px 8px;
}
.modal-close:hover { color: var(--text); }
.modal-body { padding: 20px 24px 24px; }

/* ── TOAST ── */
#toast {
  position: fixed; bottom: 32px; right: 32px;
  background: var(--bg3);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 14px 20px;
  font-size: 13px;
  z-index: 300;
  transform: translateY(20px);
  opacity: 0;
  transition: all .25s;
  max-width: 320px;
  box-shadow: var(--shadow);
}
#toast.show { transform: translateY(0); opacity: 1; }
#toast.success { border-color: var(--accent); color: var(--accent); }
#toast.error   { border-color: var(--danger); color: var(--danger); }
#toast.info    { border-color: var(--accent2); color: var(--accent2); }

/* ── SECURITY LOG ── */
.sec-log {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 12px;
  max-height: 160px;
  overflow-y: auto;
  font-size: 11px;
  color: var(--text3);
  font-family: var(--font-mono);
  margin-top: 16px;
}
.sec-entry { padding: 3px 0; border-bottom: 1px solid rgba(42,42,53,.4); }
.sec-entry:last-child { border: none; }
.sec-time  { color: var(--accent); margin-right: 8px; }
.sec-ok    { color: var(--accent); }
.sec-err   { color: var(--danger); }

/* ── TABS ── */
.tabs { display: flex; gap: 0; border-bottom: 1px solid var(--border); margin-bottom: 20px; }
.tab-btn {
  background: none; border: none; color: var(--text2);
  font-family: var(--font-mono);
  font-size: 11px; font-weight: 700;
  letter-spacing: .08em; text-transform: uppercase;
  padding: 10px 16px;
  cursor: pointer;
  border-bottom: 2px solid transparent;
  margin-bottom: -1px;
  transition: all .15s;
}
.tab-btn:hover { color: var(--text); }
.tab-btn.active { color: var(--accent); border-bottom-color: var(--accent); }
.tab-pane { display: none; }
.tab-pane.active { display: block; }

/* ── ANIMATIONS ── */
@keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }
.fade-in { animation: fadeIn .3s ease forwards; }

@keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: .5; } }
.pulse { animation: pulse 2s infinite; }

/* ── SCROLLBAR ── */
::-webkit-scrollbar { width: 6px; height: 6px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }
::-webkit-scrollbar-thumb:hover { background: var(--text3); }

/* ── RESPONSIVE ── */
@media (max-width: 1100px) {
  .layout-grid { grid-template-columns: 1fr; }
  .stats-row   { grid-template-columns: repeat(2, 1fr); }
}
@media (max-width: 600px) {
  main { padding: 16px; }
  .stats-row { grid-template-columns: 1fr 1fr; }
  header { padding: 0 16px; }
}
</style>
</head>
<body>
<div id="app">

<!-- ═══════════ HEADER ═══════════ -->
<header>
  <div class="logo">Edu<span>Track</span></div>
  <div class="header-badges">
    <span class="badge badge-secure">🔒 Données locales</span>
    <span class="badge badge-local pulse" id="status-badge">● En ligne</span>
  </div>
</header>

<!-- ═══════════ MAIN ═══════════ -->
<main>

  <!-- STATS ROW -->
  <div class="stats-row" id="stats-row">
    <div class="stat-card">
      <div class="stat-label">Total étudiants</div>
      <div class="stat-value stat-accent" id="s-total">0</div>
      <div class="stat-sub">enregistrés</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Admis</div>
      <div class="stat-value stat-accent" id="s-admis">0</div>
      <div class="stat-sub">moyenne ≥ 10/20</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Recalés</div>
      <div class="stat-value stat-danger" id="s-recales">0</div>
      <div class="stat-sub">moyenne < 10/20</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Moy. classe</div>
      <div class="stat-value" id="s-moy">—</div>
      <div class="stat-sub">/20</div>
    </div>
  </div>

  <!-- LAYOUT GRID -->
  <div class="layout-grid">

    <!-- ═══ LEFT : FORM PANEL ═══ -->
    <div>
      <div class="panel">
        <div class="panel-header">
          <span class="panel-title" id="form-panel-title">Ajouter un étudiant</span>
        </div>
        <div class="panel-body">
          <form id="student-form" novalidate autocomplete="off">
            <input type="hidden" id="edit-index" value="-1">

            <div class="form-group">
              <label for="f-id">Identifiant (ID) *</label>
              <input type="number" id="f-id" placeholder="Ex: 1001" min="1" required>
              <div class="field-error" id="err-id">ID invalide ou déjà utilisé.</div>
            </div>

            <div class="form-group">
              <label for="f-nom">Nom *</label>
              <input type="text" id="f-nom" placeholder="DIALLO" required maxlength="50">
              <div class="field-error" id="err-nom">Le nom ne peut pas être vide.</div>
            </div>

            <div class="form-group">
              <label for="f-prenom">Prénom *</label>
              <input type="text" id="f-prenom" placeholder="Mamadou" required maxlength="50">
              <div class="field-error" id="err-prenom">Le prénom ne peut pas être vide.</div>
            </div>

            <div class="form-group">
              <label for="f-ddn">Date de naissance *</label>
              <input type="text" id="f-ddn" placeholder="jj/mm/aaaa" maxlength="10" required>
              <div class="field-error" id="err-ddn">Format invalide. Ex: 25/03/2001</div>
            </div>

            <div class="form-group">
              <label for="f-lieu">Lieu de naissance *</label>
              <input type="text" id="f-lieu" placeholder="Dakar" required maxlength="50">
              <div class="field-error" id="err-lieu">Le lieu ne peut pas être vide.</div>
            </div>

            <div class="form-group">
              <label for="f-tel">Téléphone *</label>
              <input type="tel" id="f-tel" placeholder="77 000 00 00" maxlength="15" required>
              <div class="field-error" id="err-tel">Numéro invalide (7-15 chiffres).</div>
            </div>

            <div class="form-group">
              <label for="f-moy">Moyenne générale (0 – 20) *</label>
              <input type="number" id="f-moy" placeholder="14.5" min="0" max="20" step="0.01" required>
              <div class="field-error" id="err-moy">Entrez une valeur entre 0 et 20.</div>
            </div>

            <button type="submit" class="btn btn-primary" id="submit-btn">
              ＋ Ajouter l'étudiant
            </button>
            <div class="btn-row">
              <button type="button" class="btn btn-ghost" id="cancel-edit" style="display:none;flex:1">
                ✕ Annuler
              </button>
            </div>
          </form>
        </div>
      </div>

      <!-- SECURITY LOG -->
      <div class="panel" style="margin-top:16px">
        <div class="panel-header">
          <span class="panel-title">Journal de sécurité</span>
          <span class="badge badge-secure">Local</span>
        </div>
        <div class="panel-body" style="padding:12px">
          <div class="sec-log" id="sec-log">
            <div class="sec-entry"><span class="sec-time">--:--:--</span> Système initialisé</div>
          </div>
        </div>
      </div>
    </div>

    <!-- ═══ RIGHT : TABLE PANEL ═══ -->
    <div>
      <div class="panel">
        <div class="panel-header">
          <span class="panel-title">Liste des étudiants</span>
          <div style="display:flex;gap:8px">
            <button class="btn btn-ghost" id="btn-export" style="padding:6px 12px;font-size:11px">⬇ Export CSV</button>
            <button class="btn btn-ghost" id="btn-import-label" onclick="document.getElementById('csv-import').click()" style="padding:6px 12px;font-size:11px">⬆ Import CSV</button>
            <input type="file" id="csv-import" accept=".csv" style="display:none">
          </div>
        </div>
        <div class="panel-body">

          <!-- SEARCH + TABS -->
          <div class="tabs">
            <button class="tab-btn active" data-tab="tab-all">Tous</button>
            <button class="tab-btn" data-tab="tab-admis">Admis</button>
            <button class="tab-btn" data-tab="tab-recales">Recalés</button>
            <button class="tab-btn" data-tab="tab-stats">Statistiques</button>
          </div>

          <!-- TAB: ALL -->
          <div class="tab-pane active" id="tab-all">
            <div class="search-bar">
              <input type="search" id="search-input" placeholder="Rechercher par nom, prénom, ID…">
              <select id="sort-select" style="width:auto;min-width:160px">
                <option value="id">Trier par ID</option>
                <option value="nom">Trier par nom</option>
                <option value="moy-desc">Moy. ↓</option>
                <option value="moy-asc">Moy. ↑</option>
              </select>
            </div>
            <div class="table-wrap">
              <table id="students-table">
                <thead>
                  <tr>
                    <th>ID</th>
                    <th>Nom complet</th>
                    <th>Naissance</th>
                    <th>Lieu</th>
                    <th>Téléphone</th>
                    <th>Moy.</th>
                    <th>Statut</th>
                    <th>Actions</th>
                  </tr>
                </thead>
                <tbody id="table-body"></tbody>
              </table>
            </div>
          </div>

          <!-- TAB: ADMIS -->
          <div class="tab-pane" id="tab-admis">
            <div class="table-wrap">
              <table>
                <thead>
                  <tr>
                    <th>ID</th><th>Nom complet</th><th>Moy.</th><th>Actions</th>
                  </tr>
                </thead>
                <tbody id="table-admis"></tbody>
              </table>
            </div>
          </div>

          <!-- TAB: RECALES -->
          <div class="tab-pane" id="tab-recales">
            <div class="table-wrap">
              <table>
                <thead>
                  <tr>
                    <th>ID</th><th>Nom complet</th><th>Moy.</th><th>Actions</th>
                  </tr>
                </thead>
                <tbody id="table-recales"></tbody>
              </table>
            </div>
          </div>

          <!-- TAB: STATS -->
          <div class="tab-pane" id="tab-stats">
            <div id="stats-detail" style="padding:8px 0"></div>
          </div>

        </div>
      </div>
    </div>
  </div>
</main>

<!-- ═══════════ MODAL CONFIRM DELETE ═══════════ -->
<div class="modal-overlay" id="delete-modal">
  <div class="modal">
    <div class="modal-header">
      <span class="modal-title" style="color:var(--danger)">⚠ Supprimer</span>
      <button class="modal-close" id="delete-modal-close">✕</button>
    </div>
    <div class="modal-body">
      <p style="color:var(--text2);margin-bottom:20px">Voulez-vous vraiment supprimer <strong id="delete-name" style="color:var(--text)"></strong> ? Cette action est irréversible.</p>
      <div style="display:flex;gap:12px">
        <button class="btn btn-ghost" id="delete-cancel" style="flex:1">Annuler</button>
        <button class="btn btn-danger" id="delete-confirm" style="flex:1;padding:10px 18px">Supprimer</button>
      </div>
    </div>
  </div>
</div>

<!-- TOAST -->
<div id="toast"></div>

<!-- ═══════════ SCRIPT ═══════════ -->
<script>
/* ─────────────────────────────────────────
   SÉCURITÉ : sanitisation XSS
   ─────────────────────────────────────────*/
function sanitize(str) {
  if (typeof str !== 'string') return String(str);
  return str
    .replace(/&/g,'&amp;')
    .replace(/</g,'&lt;')
    .replace(/>/g,'&gt;')
    .replace(/"/g,'&quot;')
    .replace(/'/g,'&#039;')
    .trim();
}

function sanitizeNum(v) {
  const n = parseFloat(v);
  return isNaN(n) ? null : n;
}

/* ─────────────────────────────────────────
   DONNÉES (localStorage chiffré en base64)
   ─────────────────────────────────────────*/
const STORAGE_KEY = 'edutrack_v1';

function loadData() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return [];
    return JSON.parse(atob(raw));
  } catch(e) {
    secLog('Erreur chargement données', 'err');
    return [];
  }
}

function saveData(arr) {
  try {
    localStorage.setItem(STORAGE_KEY, btoa(JSON.stringify(arr)));
  } catch(e) {
    secLog('Erreur sauvegarde', 'err');
  }
}

let students = loadData();

/* ─────────────────────────────────────────
   JOURNAL DE SÉCURITÉ
   ─────────────────────────────────────────*/
function secLog(msg, type='ok') {
  const log = document.getElementById('sec-log');
  const now = new Date().toLocaleTimeString('fr-FR');
  const div = document.createElement('div');
  div.className = 'sec-entry';
  div.innerHTML = `<span class="sec-time">${now}</span><span class="sec-${type}">${sanitize(msg)}</span>`;
  log.insertBefore(div, log.firstChild);
  if (log.children.length > 50) log.removeChild(log.lastChild);
}

/* ─────────────────────────────────────────
   TOAST
   ─────────────────────────────────────────*/
let toastTimer;
function showToast(msg, type='success') {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = `show ${type}`;
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => { t.className = ''; }, 3000);
}

/* ─────────────────────────────────────────
   VALIDATION
   ─────────────────────────────────────────*/
function validateDate(d) {
  if (!/^\d{2}\/\d{2}\/\d{4}$/.test(d)) return false;
  const [dd,mm,yy] = d.split('/').map(Number);
  return dd>=1 && dd<=31 && mm>=1 && mm<=12 && yy>=1900 && yy<=2025;
}

function validatePhone(p) {
  const clean = p.replace(/\s/g,'');
  return /^[+\d]{7,15}$/.test(clean);
}

function setFieldState(id, ok, errId) {
  const el = document.getElementById(id);
  const err = document.getElementById(errId);
  el.classList.toggle('error', !ok);
  el.classList.toggle('ok', ok);
  if (err) err.classList.toggle('show', !ok);
}

/* ─────────────────────────────────────────
   STATS
   ─────────────────────────────────────────*/
function updateStats() {
  const total = students.length;
  const admis = students.filter(s => s.moyenne >= 10).length;
  const recales = total - admis;
  const moy = total ? (students.reduce((a,s)=>a+s.moyenne,0)/total).toFixed(2) : '—';

  document.getElementById('s-total').textContent   = total;
  document.getElementById('s-admis').textContent   = admis;
  document.getElementById('s-recales').textContent = recales;
  document.getElementById('s-moy').textContent     = moy;
}

function renderStatsDetail() {
  const el = document.getElementById('stats-detail');
  if (!students.length) {
    el.innerHTML = '<div class="empty-state"><div class="icon">📊</div>Aucune donnée disponible.</div>';
    return;
  }
  const sorted = [...students].sort((a,b)=>a.moyenne-b.moyenne);
  const n = sorted.length;
  const med = n%2===0 ? (sorted[n/2-1].moyenne+sorted[n/2].moyenne)/2 : sorted[Math.floor(n/2)].moyenne;
  const best = sorted[n-1];
  const worst = sorted[0];
  const t = [0,0,0,0];
  students.forEach(s => {
    if (s.moyenne<5) t[0]++;
    else if (s.moyenne<10) t[1]++;
    else if (s.moyenne<15) t[2]++;
    else t[3]++;
  });
  const admis = students.filter(s=>s.moyenne>=10).length;
  const moy = (students.reduce((a,s)=>a+s.moyenne,0)/n).toFixed(2);

  el.innerHTML = `
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:16px">
      <div class="stat-card"><div class="stat-label">Moyenne classe</div><div class="stat-value stat-accent">${moy}</div></div>
      <div class="stat-card"><div class="stat-label">Médiane</div><div class="stat-value" style="color:var(--accent2)">${med.toFixed(2)}</div></div>
      <div class="stat-card"><div class="stat-label">Meilleure note</div><div class="stat-value stat-accent">${best.moyenne.toFixed(2)}</div><div class="stat-sub">${sanitize(best.prenom)} ${sanitize(best.nom)}</div></div>
      <div class="stat-card"><div class="stat-label">Note la plus basse</div><div class="stat-value stat-danger">${worst.moyenne.toFixed(2)}</div><div class="stat-sub">${sanitize(worst.prenom)} ${sanitize(worst.nom)}</div></div>
    </div>
    <div class="panel-header" style="margin-bottom:12px;border-radius:4px"><span class="panel-title">Répartition par tranches</span></div>
    ${[['[ 0 – 5 [',t[0],'var(--danger)'],['[ 5 – 10 [',t[1],'var(--warn)'],['[ 10 – 15 [',t[2],'var(--accent2)'],['[ 15 – 20 ]',t[3],'var(--accent)']].map(([label,count,color])=>`
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:10px">
        <span style="width:90px;font-size:11px;color:var(--text2)">${label}</span>
        <div style="flex:1;background:var(--bg);border-radius:3px;height:8px;overflow:hidden">
          <div style="height:100%;width:${n?Math.round(count/n*100):0}%;background:${color};border-radius:3px;transition:width .5s"></div>
        </div>
        <span style="font-size:12px;font-weight:700;color:${color};width:24px;text-align:right">${count}</span>
      </div>
    `).join('')}
    <div style="margin-top:16px;padding:12px;background:var(--bg);border-radius:4px;display:flex;justify-content:space-between">
      <span style="color:var(--accent)">✔ Admis : <strong>${admis}</strong> (${n?Math.round(admis/n*100):0}%)</span>
      <span style="color:var(--danger)">✘ Recalés : <strong>${n-admis}</strong> (${n?Math.round((n-admis)/n*100):0}%)</span>
    </div>
  `;
}

/* ─────────────────────────────────────────
   RENDER TABLE
   ─────────────────────────────────────────*/
function getFiltered() {
  const q = document.getElementById('search-input').value.toLowerCase().trim();
  const sort = document.getElementById('sort-select').value;

  let list = [...students];

  if (q) {
    list = list.filter(s =>
      s.nom.toLowerCase().includes(q) ||
      s.prenom.toLowerCase().includes(q) ||
      String(s.id).includes(q) ||
      s.lieu_naissance.toLowerCase().includes(q)
    );
  }

  if (sort === 'nom')      list.sort((a,b)=>a.nom.localeCompare(b.nom));
  else if (sort === 'moy-desc') list.sort((a,b)=>b.moyenne-a.moyenne);
  else if (sort === 'moy-asc')  list.sort((a,b)=>a.moyenne-b.moyenne);
  else list.sort((a,b)=>a.id-b.id);

  return list;
}

function renderRow(s, idx, cols='full') {
  const admis = s.moyenne >= 10;
  const chipHtml = admis
    ? '<span class="chip chip-ok">Admis</span>'
    : '<span class="chip chip-bad">Recalé</span>';
  const moyColor = admis ? 'var(--accent)' : 'var(--danger)';

  if (cols === 'short') {
    return `<tr class="fade-in">
      <td class="td-id">#${sanitize(s.id)}</td>
      <td class="td-name">${sanitize(s.prenom)} ${sanitize(s.nom)}</td>
      <td class="td-moy" style="color:${moyColor}">${sanitize(s.moyenne.toFixed(2))}</td>
      <td>
        <div style="display:flex;gap:6px">
          <button class="btn btn-edit" onclick="editStudent(${idx})">✏</button>
          <button class="btn btn-danger" onclick="confirmDelete(${idx})">✕</button>
        </div>
      </td>
    </tr>`;
  }

  return `<tr class="fade-in">
    <td class="td-id">#${sanitize(s.id)}</td>
    <td class="td-name">${sanitize(s.prenom)} ${sanitize(s.nom)}</td>
    <td style="color:var(--text2);font-size:12px">${sanitize(s.date_naissance)}</td>
    <td style="color:var(--text2);font-size:12px">${sanitize(s.lieu_naissance)}</td>
    <td style="color:var(--text2);font-size:12px">${sanitize(s.telephone)}</td>
    <td class="td-moy" style="color:${moyColor};font-size:15px">${sanitize(s.moyenne.toFixed(2))}</td>
    <td>${chipHtml}</td>
    <td>
      <div style="display:flex;gap:6px">
        <button class="btn btn-edit" onclick="editStudent(${idx})">✏</button>
        <button class="btn btn-danger" onclick="confirmDelete(${idx})">✕</button>
      </div>
    </td>
  </tr>`;
}

function renderTables() {
  const list = getFiltered();
  const tbody = document.getElementById('table-body');

  if (!list.length) {
    tbody.innerHTML = `<tr><td colspan="8"><div class="empty-state"><div class="icon">🎓</div>Aucun étudiant trouvé.</div></td></tr>`;
  } else {
    tbody.innerHTML = list.map((s,i) => {
      const realIdx = students.indexOf(s);
      return renderRow(s, realIdx, 'full');
    }).join('');
  }

  // Admis tab
  const admisData = students.filter(s=>s.moyenne>=10).sort((a,b)=>b.moyenne-a.moyenne);
  const tAdmis = document.getElementById('table-admis');
  tAdmis.innerHTML = admisData.length
    ? admisData.map(s=>renderRow(s, students.indexOf(s), 'short')).join('')
    : `<tr><td colspan="4"><div class="empty-state">Aucun étudiant admis.</div></td></tr>`;

  // Recalés tab
  const recalesData = students.filter(s=>s.moyenne<10).sort((a,b)=>a.moyenne-b.moyenne);
  const tRec = document.getElementById('table-recales');
  tRec.innerHTML = recalesData.length
    ? recalesData.map(s=>renderRow(s, students.indexOf(s), 'short')).join('')
    : `<tr><td colspan="4"><div class="empty-state">Aucun étudiant recalé.</div></td></tr>`;

  updateStats();
  renderStatsDetail();
}

/* ─────────────────────────────────────────
   FORM : AJOUTER / MODIFIER
   ─────────────────────────────────────────*/
document.getElementById('student-form').addEventListener('submit', function(e) {
  e.preventDefault();

  const editIdx = parseInt(document.getElementById('edit-index').value);
  const isEdit  = editIdx >= 0;

  const id     = parseInt(document.getElementById('f-id').value);
  const nom    = sanitize(document.getElementById('f-nom').value);
  const prenom = sanitize(document.getElementById('f-prenom').value);
  const ddn    = sanitize(document.getElementById('f-ddn').value);
  const lieu   = sanitize(document.getElementById('f-lieu').value);
  const tel    = sanitize(document.getElementById('f-tel').value);
  const moy    = parseFloat(document.getElementById('f-moy').value);

  // Validation
  let valid = true;

  const idExists = students.some((s,i) => s.id === id && i !== editIdx);
  const idOk = id > 0 && !isNaN(id) && !idExists;
  setFieldState('f-id','f-id', 'err-id');
  if (!idOk) { setFieldState('f-id',false,'err-id'); valid=false; }
  else        { setFieldState('f-id',true, 'err-id'); }

  if (!nom)   { setFieldState('f-nom',false,'err-nom');    valid=false; }
  else         { setFieldState('f-nom',true, 'err-nom'); }
  if (!prenom) { setFieldState('f-prenom',false,'err-prenom'); valid=false; }
  else          { setFieldState('f-prenom',true, 'err-prenom'); }

  if (!validateDate(ddn)) { setFieldState('f-ddn',false,'err-ddn'); valid=false; }
  else                    { setFieldState('f-ddn',true, 'err-ddn'); }

  if (!lieu) { setFieldState('f-lieu',false,'err-lieu'); valid=false; }
  else        { setFieldState('f-lieu',true, 'err-lieu'); }

  if (!validatePhone(tel)) { setFieldState('f-tel',false,'err-tel'); valid=false; }
  else                     { setFieldState('f-tel',true, 'err-tel'); }

  if (isNaN(moy)||moy<0||moy>20) { setFieldState('f-moy',false,'err-moy'); valid=false; }
  else                            { setFieldState('f-moy',true, 'err-moy'); }

  if (!valid) {
    secLog(`Tentative ${isEdit?'modification':'ajout'} — validation échouée`, 'err');
    return;
  }

  const student = { id, nom, prenom, date_naissance: ddn, lieu_naissance: lieu, telephone: tel, moyenne: moy };

  if (isEdit) {
    students[editIdx] = student;
    secLog(`Étudiant #${id} modifié`, 'ok');
    showToast(`✔ ${prenom} ${nom} modifié avec succès`, 'success');
    cancelEdit();
  } else {
    students.push(student);
    secLog(`Étudiant #${id} ajouté`, 'ok');
    showToast(`✔ ${prenom} ${nom} ajouté avec succès`, 'success');
  }

  saveData(students);
  resetForm();
  renderTables();
});

function resetForm() {
  document.getElementById('student-form').reset();
  ['f-id','f-nom','f-prenom','f-ddn','f-lieu','f-tel','f-moy'].forEach(id => {
    const el = document.getElementById(id);
    el.classList.remove('error','ok');
  });
  document.querySelectorAll('.field-error').forEach(e=>e.classList.remove('show'));
}

/* ─────────────────────────────────────────
   EDIT
   ─────────────────────────────────────────*/
function editStudent(idx) {
  const s = students[idx];
  document.getElementById('edit-index').value = idx;
  document.getElementById('f-id').value     = s.id;
  document.getElementById('f-nom').value    = s.nom;
  document.getElementById('f-prenom').value = s.prenom;
  document.getElementById('f-ddn').value    = s.date_naissance;
  document.getElementById('f-lieu').value   = s.lieu_naissance;
  document.getElementById('f-tel').value    = s.telephone;
  document.getElementById('f-moy').value    = s.moyenne;

  document.getElementById('form-panel-title').textContent = 'Modifier l\'étudiant';
  document.getElementById('submit-btn').textContent = '✔ Enregistrer les modifications';
  document.getElementById('cancel-edit').style.display = 'flex';
  document.getElementById('f-id').scrollIntoView({ behavior: 'smooth', block: 'center' });
  secLog(`Édition étudiant #${s.id} démarrée`);
}

function cancelEdit() {
  document.getElementById('edit-index').value = -1;
  document.getElementById('form-panel-title').textContent = 'Ajouter un étudiant';
  document.getElementById('submit-btn').textContent = '＋ Ajouter l\'étudiant';
  document.getElementById('cancel-edit').style.display = 'none';
  resetForm();
}

document.getElementById('cancel-edit').addEventListener('click', cancelEdit);

/* ─────────────────────────────────────────
   DELETE
   ─────────────────────────────────────────*/
let deleteIdx = -1;

function confirmDelete(idx) {
  deleteIdx = idx;
  const s = students[idx];
  document.getElementById('delete-name').textContent = `${s.prenom} ${s.nom} (#${s.id})`;
  document.getElementById('delete-modal').classList.add('open');
}

document.getElementById('delete-confirm').addEventListener('click', () => {
  if (deleteIdx < 0) return;
  const s = students[deleteIdx];
  secLog(`Étudiant #${s.id} supprimé`, 'err');
  showToast(`✕ ${s.prenom} ${s.nom} supprimé`, 'error');
  students.splice(deleteIdx, 1);
  saveData(students);
  renderTables();
  deleteIdx = -1;
  document.getElementById('delete-modal').classList.remove('open');
});

['delete-cancel','delete-modal-close'].forEach(id => {
  document.getElementById(id).addEventListener('click', () => {
    document.getElementById('delete-modal').classList.remove('open');
    deleteIdx = -1;
  });
});

/* ─────────────────────────────────────────
   TABS
   ─────────────────────────────────────────*/
document.querySelectorAll('.tab-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
    document.querySelectorAll('.tab-pane').forEach(p=>p.classList.remove('active'));
    btn.classList.add('active');
    document.getElementById(btn.dataset.tab).classList.add('active');
    if (btn.dataset.tab === 'tab-stats') renderStatsDetail();
  });
});

/* ─────────────────────────────────────────
   SEARCH + SORT
   ─────────────────────────────────────────*/
document.getElementById('search-input').addEventListener('input', renderTables);
document.getElementById('sort-select').addEventListener('change', renderTables);

/* ─────────────────────────────────────────
   EXPORT CSV
   ─────────────────────────────────────────*/
document.getElementById('btn-export').addEventListener('click', () => {
  if (!students.length) { showToast('Aucun étudiant à exporter', 'info'); return; }
  const header = 'id;nom;prenom;date_naissance;lieu_naissance;telephone;moyenne\n';
  const rows = students.map(s =>
    `${s.id};${s.nom};${s.prenom};${s.date_naissance};${s.lieu_naissance};${s.telephone};${s.moyenne.toFixed(2)}`
  ).join('\n');
  const blob = new Blob([header + rows], { type: 'text/csv;charset=utf-8;' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = `etudiants_${new Date().toISOString().slice(0,10)}.csv`;
  a.click();
  secLog('Export CSV réalisé', 'ok');
  showToast('⬇ Export CSV téléchargé', 'success');
});

/* ─────────────────────────────────────────
   IMPORT CSV
   ─────────────────────────────────────────*/
document.getElementById('csv-import').addEventListener('change', function(e) {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = function(ev) {
    const lines = ev.target.result.trim().split('\n');
    let imported = 0, skipped = 0;
    lines.slice(1).forEach(line => {
      const parts = line.split(';');
      if (parts.length < 7) { skipped++; return; }
      const id = parseInt(parts[0]);
      const moy = parseFloat(parts[6]);
      if (isNaN(id) || isNaN(moy) || moy<0 || moy>20) { skipped++; return; }
      if (students.some(s=>s.id===id)) { skipped++; return; }
      students.push({
        id, nom: sanitize(parts[1]), prenom: sanitize(parts[2]),
        date_naissance: sanitize(parts[3]), lieu_naissance: sanitize(parts[4]),
        telephone: sanitize(parts[5]), moyenne: moy
      });
      imported++;
    });
    saveData(students);
    renderTables();
    secLog(`Import CSV : ${imported} ajoutés, ${skipped} ignorés`, imported?'ok':'err');
    showToast(`⬆ ${imported} étudiant(s) importé(s)`, 'success');
    e.target.value = '';
  };
  reader.readAsText(file);
});

/* ─────────────────────────────────────────
   DATE AUTOFORMAT jj/mm/aaaa
   ─────────────────────────────────────────*/
document.getElementById('f-ddn').addEventListener('input', function() {
  let v = this.value.replace(/\D/g,'');
  if (v.length>2) v = v.slice(0,2)+'/'+v.slice(2);
  if (v.length>5) v = v.slice(0,5)+'/'+v.slice(5,9);
  this.value = v;
});

/* ─────────────────────────────────────────
   INIT
   ─────────────────────────────────────────*/
secLog(`Chargement : ${students.length} étudiant(s)`, 'ok');
renderTables();
</script>
</body>
</html>
