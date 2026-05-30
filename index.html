<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Requested Books</title>
    <style>
        /* --- CSS VARIABLES & THEMES --- */
        :root {
            --bg-color: #17212b;
            --card-bg: #242f3d;
            --text-main: #ffffff;
            --text-muted: #8b9bb4;
            --accent: #5288c1;
            --accent-hover: #4170a3;
            --danger: #e53935;
            --danger-hover: #b71c1c;
            --success: #4caf50;
            --success-hover: #388e3c;
            --neon-orange: #ff9800;
            --modal-bg: rgba(0, 0, 0, 0.6);
            --border-radius: 12px;
            --input-border: #3b4b5e;
        }

        [data-theme="light"] {
            --bg-color: #f5f5f5;
            --card-bg: #ffffff;
            --text-main: #222222;
            --text-muted: #707579;
            --accent: #3390ec;
            --accent-hover: #2670b8;
            --danger: #d32f2f;
            --danger-hover: #b71c1c;
            --success: #2e7d32;
            --success-hover: #1b5e20;
            --neon-orange: #f57c00;
            --modal-bg: rgba(0, 0, 0, 0.4);
            --border-radius: 12px;
            --input-border: #cccccc;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
        body { background-color: var(--bg-color); color: var(--text-main); transition: background-color 0.3s ease, color 0.3s ease; padding-bottom: 110px; }

        #floating-ad { position: fixed; left: 50%; transform: translateX(-50%); bottom: 0; z-index: 999999999; width: auto; height: auto; display: flex; justify-content: center; align-items: center; pointer-events: auto; }

        header { background-color: var(--card-bg); padding: 15px 20px; display: grid; grid-template-columns: 1fr auto 1fr; align-items: center; box-shadow: 0 2px 10px rgba(0,0,0,0.1); position: sticky; top: 0; z-index: 100; }
        .back-btn { justify-self: start; text-decoration: none; font-weight: bold; color: var(--text-main); font-size: 1rem; }
        h1 { font-size: 1.4rem; font-weight: 600; justify-self: center; text-align: center; }
        .settings-btn { justify-self: end; background: none; border: none; font-size: 1.5rem; cursor: pointer; color: var(--text-main); }

        .container { max-width: 800px; margin: 20px auto; padding: 0 15px; padding-bottom: 40px; }
        .card { background-color: var(--card-bg); border-radius: var(--border-radius); padding: 20px; margin-bottom: 15px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); display: flex; flex-direction: column; gap: 15px; }
        
        .book-header { display: flex; align-items: center; gap: 15px; }
        .neon-book { font-size: 2.2rem; color: var(--neon-orange); text-shadow: 0 0 5px var(--neon-orange), 0 0 15px var(--neon-orange); flex-shrink: 0; }
        .book-info { display: flex; flex-direction: column; gap: 4px; flex-grow: 1; word-break: break-word; }
        .book-info h3 { font-size: 1.25rem; margin: 0; color: var(--text-main); }
        .book-info p { color: var(--text-muted); font-size: 0.9rem; margin: 0; }

        .btn { padding: 12px 20px; border: none; border-radius: 8px; font-size: 1rem; font-weight: 600; cursor: pointer; text-align: center; text-decoration: none; color: #fff; background-color: var(--accent); transition: 0.2s; display: inline-flex; justify-content: center; align-items: center; width: 100%; }
        .btn-danger { background-color: var(--danger); }
        .btn-success { background-color: var(--success); }
        .btn-outline { background-color: transparent; border: 1px solid var(--accent); color: var(--accent); }
        .btn-exit { border-color: var(--danger); color: var(--danger); }

        .input-group { display: flex; flex-direction: column; gap: 6px; width: 100%; }
        .input-group label { font-size: 0.9rem; color: var(--text-muted); }
        input[type="text"], input[type="url"], input[type="datetime-local"] { width: 100%; padding: 12px; border-radius: 8px; border: 1px solid var(--input-border); background-color: var(--bg-color); color: var(--text-main); outline: none; font-size: 1rem; }

        #admin-panel { display: none; border: 2px solid var(--accent); margin-bottom: 30px; }
        .admin-controls { display: flex; gap: 10px; margin-top: 5px; }
        .admin-badge { background-color: var(--accent); color: white; padding: 4px 8px; border-radius: 4px; font-size: 0.75rem; font-weight: bold; margin-bottom: 10px; text-transform: uppercase; display: inline-block; }

        .modal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: var(--modal-bg); display: none; justify-content: center; align-items: center; z-index: 1000; }
        .modal { background-color: var(--card-bg); padding: 25px; border-radius: var(--border-radius); width: 90%; max-width: 400px; display: flex; flex-direction: column; gap: 20px; }
        .modal-header { display: flex; justify-content: space-between; align-items: center; font-size: 1.2rem; font-weight: bold; }
        .close-btn { background: none; border: none; color: var(--text-main); font-size: 1.5rem; cursor: pointer; }
        .theme-toggle { display: flex; justify-content: space-between; align-items: center; }
        .empty-state { text-align: center; color: var(--text-muted); margin-top: 50px; }
    </style>
</head>
<body>

    <header>
        <a href="https://google-books.github.io/MainPage/" class="back-btn">Back</a>
        <h1>Requested Books</h1>
        <button class="settings-btn" onclick="window.openSettings()">⚙️</button>
    </header>

    <div class="container">
        <div id="admin-panel" class="card">
            <div><span class="admin-badge">Admin: Master Template Setup</span></div>
            <div class="input-group">
                <label>Book Name</label>
                <input type="text" id="master-name" placeholder="e.g., The Great Gatsby">
            </div>
            <div class="input-group">
                <label>Publish Date & Time</label>
                <input type="datetime-local" id="master-datetime">
            </div>
            <div class="input-group">
                <label>Download Link</label>
                <input type="url" id="master-link" placeholder="https://...">
            </div>
            <button class="btn btn-success" onclick="window.cloneTemplate()">➕ Clone & Publish Template</button>
            <button class="btn btn-outline btn-exit" onclick="window.exitAdmin()">🚪 Exit Admin Mode</button>
        </div>

        <div id="user-view"></div>
    </div>

    <div class="modal-overlay" id="settings-modal">
        <div class="modal">
            <div class="modal-header">
                <span>Settings</span>
                <button class="close-btn" onclick="window.closeSettings()">×</button>
            </div>
            <div class="theme-toggle">
                <span>App Theme</span>
                <button class="btn btn-outline" id="theme-btn" onclick="window.toggleTheme()">Day Mode</button>
            </div>
            <hr style="border: 0; border-top: 1px solid var(--input-border); margin: 5px 0;">
            <div class="input-group">
                <label>Quick Download Code</label>
                <div style="display: flex; gap: 10px;">
                    <input type="text" id="quick-code-input" placeholder="Enter code...">
                    <button class="btn" style="width: auto;" onclick="window.checkQuickCode()">Submit</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // --- DATA ---
        let templates = JSON.parse(localStorage.getItem('requested_books_v2')) || [];
        let isAdmin = false;
        let editingId = null;

        // --- GLOBAL FUNCTIONS ATTACHED TO WINDOW ---
        window.openSettings = function() { document.getElementById('settings-modal').style.display = 'flex'; };
        window.closeSettings = function() { document.getElementById('settings-modal').style.display = 'none'; };

        window.toggleTheme = function() {
            const isDark = document.documentElement.getAttribute('data-theme') === 'dark';
            const newTheme = isDark ? 'light' : 'dark';
            document.documentElement.setAttribute('data-theme', newTheme);
            localStorage.setItem('theme', newTheme);
            updateThemeBtn(newTheme);
        };

        function updateThemeBtn(theme) {
            const btn = document.getElementById('theme-btn');
            btn.textContent = theme === 'dark' ? 'Day Mode' : 'Night Mode';
        }

        window.checkQuickCode = function() {
            const inputField = document.getElementById('quick-code-input');
            if (inputField.value.trim() === '0785993080') {
                isAdmin = true;
                document.getElementById('admin-panel').style.display = 'flex';
                window.closeSettings();
                inputField.value = '';
                renderTemplates();
            } else {
                alert("Invalid Code");
                inputField.value = '';
            }
        };

        window.exitAdmin = function() {
            isAdmin = false;
            editingId = null;
            document.getElementById('admin-panel').style.display = 'none';
            renderTemplates();
        };

        window.cloneTemplate = function() {
            const name = document.getElementById('master-name').value.trim();
            const date = document.getElementById('master-datetime').value;
            const link = document.getElementById('master-link').value.trim();
            if (!name || !link) return alert('Fill fields');
            templates.unshift({ id: Date.now(), name, datetime: date, link });
            saveData();
            renderTemplates();
        };

        window.deleteTemplate = function(id) {
            if (confirm("Delete?")) {
                templates = templates.filter(t => t.id !== id);
                saveData();
                renderTemplates();
            }
        };

        window.startEdit = function(id) { editingId = id; renderTemplates(); };
        window.cancelEdit = function() { editingId = null; renderTemplates(); };

        window.saveEdit = function(id) {
            const name = document.getElementById(`edit-name-${id}`).value.trim();
            const date = document.getElementById(`edit-datetime-${id}`).value;
            const link = document.getElementById(`edit-link-${id}`).value.trim();
            const idx = templates.findIndex(t => t.id === id);
            if (idx > -1) { templates[idx] = { id, name, datetime: date, link }; saveData(); }
            editingId = null;
            renderTemplates();
        };

        function saveData() { localStorage.setItem('requested_books_v2', JSON.stringify(templates)); }

        function renderTemplates() {
            const container = document.getElementById('user-view');
            container.innerHTML = '';
            if (templates.length === 0) {
                container.innerHTML = '<div class="empty-state">No requested books available.</div>';
                return;
            }
            templates.forEach((t) => {
                const card = document.createElement('div');
                card.className = 'card';
                if (editingId === t.id && isAdmin) {
                    card.innerHTML = `<input type="text" id="edit-name-${t.id}" value="${t.name}"><input type="datetime-local" id="edit-datetime-${t.id}" value="${t.datetime}"><input type="url" id="edit-link-${t.id}" value="${t.link}"><div class="admin-controls"><button class="btn btn-success" onclick="window.saveEdit(${t.id})">Save</button><button class="btn btn-outline" onclick="window.cancelEdit()">Cancel</button></div>`;
                } else {
                    card.innerHTML = `<div class="book-header"><div class="neon-book">📘</div><div class="book-info"><h3>${t.name}</h3><p>${t.datetime}</p></div></div><a href="${t.link}" class="btn">📥 Download</a>` + (isAdmin ? `<div class="admin-controls"><button class="btn btn-outline" onclick="window.startEdit(${t.id})">Edit</button><button class="btn btn-danger" onclick="window.deleteTemplate(${t.id})">Delete</button></div>` : '');
                }
                container.appendChild(card);
            });
        }

        // Init
        document.addEventListener('DOMContentLoaded', () => {
            const savedTheme = localStorage.getItem('theme') || 'dark';
            document.documentElement.setAttribute('data-theme', savedTheme);
            updateThemeBtn(savedTheme);
            renderTemplates();
        });
    </script>

    <script type='text/javascript' src='//speedingdeadlyplays.com/YOUR_SOCIAL_BAR_CODE/invoke.js'></script>
    <div id="floating-ad"></div>

    <script>
        (function(){
            function loadAd() {
                const adContainer = document.getElementById("floating-ad");
                adContainer.innerHTML = '';
                let key = "", width = 0, height = 0;
                const w = window.innerWidth;
                if (w <= 360) { key = '3b8048b78e2b0fb0b882483f96fca8a2'; width = 320; height = 50; } 
                else if (w <= 768) { key = '27bf67bdd07dd3734a6fdff8c7879c99'; width = 468; height = 60; } 
                else { key = '30c18b6ace1c2676949453fd6ac33776'; width = 728; height = 90; }
                window.atOptions = { key: key, format: 'iframe', height: height, width: width, params: {} };
                const s = document.createElement("script");
                s.src = "https://speedingdeadlyplays.com/" + key + "/invoke.js";
                s.async = true;
                adContainer.appendChild(s);
            }
            loadAd();
            setInterval(loadAd, 13000);
        })();
    </script>
</body>
</html>
