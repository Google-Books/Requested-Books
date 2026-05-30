<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Requested Books</title>
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <style>
        /* --- CSS VARIABLES & THEMES --- */
        :root {
            /* Dark Telegram Theme (Default) */
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
            /* Stable Light Theme */
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

        /* --- GLOBAL STYLES --- */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            transition: background-color 0.3s ease, color 0.3s ease;
            padding-bottom: 110px; 
        }

        /* استایل نگهدارنده بنر شناور تبلیغاتی */
        #floating-ad {
            position: fixed;
            left: 50%;
            transform: translateX(-50%);
            bottom: 0;
            z-index: 999999999;
            width: auto;
            height: auto;
            display: flex;
            justify-content: center;
            align-items: center;
            pointer-events: auto;
        }

        /* --- HEADER --- */
        header {
            background-color: var(--card-bg);
            padding: 15px 20px;
            display: grid;
            grid-template-columns: 1fr auto 1fr;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 100;
            transition: background-color 0.3s ease;
        }

        /* استایل دکمه بک (سمت چپ) */
        .back-btn {
            justify-self: start;
            text-decoration: none;
            font-weight: bold;
            color: var(--text-main);
            font-size: 1rem;
            transition: opacity 0.2s;
        }
        .back-btn:hover {
            opacity: 0.8;
        }

        h1 {
            font-size: 1.4rem;
            font-weight: 600;
            justify-self: center;
            text-align: center;
        }

        .settings-btn {
            justify-self: end;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            transition: transform 0.3s ease;
        }

        .settings-btn:hover {
            transform: rotate(90deg);
        }

        /* --- MAIN LAYOUT --- */
        .container {
            max-width: 800px;
            margin: 20px auto;
            padding: 0 15px;
            padding-bottom: 40px;
        }

        /* --- CARDS & TEMPLATES --- */
        .card {
            background-color: var(--card-bg);
            border-radius: var(--border-radius);
            padding: 20px;
            margin-bottom: 15px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            animation: fadeIn 0.4s ease forwards;
            display: flex;
            flex-direction: column;
            gap: 15px;
            transition: background-color 0.3s ease;
        }

        .book-header {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .neon-book {
            font-size: 2.2rem;
            color: var(--neon-orange);
            text-shadow: 0 0 5px var(--neon-orange), 0 0 15px var(--neon-orange);
            flex-shrink: 0;
        }

        .book-info {
            display: flex;
            flex-direction: column;
            gap: 4px;
            flex-grow: 1;
            word-break: break-word;
        }

        .book-info h3 {
            font-size: 1.25rem;
            margin: 0;
            color: var(--text-main);
        }

        .book-info p {
            color: var(--text-muted);
            font-size: 0.9rem;
            margin: 0;
        }

        .btn {
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            text-align: center;
            text-decoration: none;
            color: #fff;
            background-color: var(--accent);
            transition: background-color 0.2s ease, transform 0.1s ease;
            display: inline-flex;
            justify-content: center;
            align-items: center;
            width: 100%;
        }

        .btn:active { transform: scale(0.98); }
        .btn:hover { background-color: var(--accent-hover); }

        .btn-danger { background-color: var(--danger); }
        .btn-danger:hover { background-color: var(--danger-hover); }

        .btn-success { background-color: var(--success); }
        .btn-success:hover { background-color: var(--success-hover); }
        
        .btn-outline {
            background-color: transparent;
            border: 1px solid var(--accent);
            color: var(--accent);
        }
        .btn-outline:hover {
            background-color: var(--accent);
            color: #fff;
        }
        
        /* New styling for exit button to look distinctive */
        .btn-exit {
            border-color: var(--danger);
            color: var(--danger);
        }
        .btn-exit:hover {
            background-color: var(--danger);
            color: #fff;
        }

        .input-group {
            display: flex;
            flex-direction: column;
            gap: 6px;
            width: 100%;
        }

        .input-group label {
            font-size: 0.9rem;
            color: var(--text-muted);
            font-weight: 500;
        }

        input[type="text"], input[type="url"], input[type="datetime-local"] {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid var(--input-border);
            background-color: var(--bg-color);
            color: var(--text-main);
            outline: none;
            transition: border-color 0.2s, background-color 0.3s, color 0.3s;
            font-size: 1rem;
        }

        input[type="text"]:focus, input[type="url"]:focus, input[type="datetime-local"]:focus {
            border-color: var(--accent);
        }

        /* --- ADMIN PANEL --- */
        #admin-panel {
            display: none;
            border: 2px solid var(--accent);
            margin-bottom: 30px;
        }

        .admin-controls {
            display: flex;
            gap: 10px;
            margin-top: 5px;
        }

        .admin-controls .btn {
            flex: 1;
        }

        .admin-badge {
            background-color: var(--accent);
            color: white;
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 0.75rem;
            font-weight: bold;
            display: inline-block;
            margin-bottom: 10px;
            text-transform: uppercase;
        }

        /* --- MODAL --- */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: var(--modal-bg);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            animation: fadeIn 0.2s ease;
        }

        .modal {
            background-color: var(--card-bg);
            padding: 25px;
            border-radius: var(--border-radius);
            width: 90%;
            max-width: 400px;
            display: flex;
            flex-direction: column;
            gap: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            transition: background-color 0.3s ease;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 1.2rem;
            font-weight: bold;
        }

        .close-btn {
            background: none;
            border: none;
            color: var(--text-main);
            font-size: 1.5rem;
            cursor: pointer;
        }

        .theme-toggle {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .flex-row {
            display: flex;
            gap: 10px;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .empty-state {
            text-align: center;
            color: var(--text-muted);
            margin-top: 50px;
            font-size: 1.1rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
        }
    </style>
</head>
<body>

    <header>
        <a href="https://google-books.github.io/MainPage/" class="back-btn">Back</a>
        <h1>Requested Books</h1>
        <button class="settings-btn" onclick="openSettings()">⚙️</button>
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

            <button class="btn btn-success" style="margin-top: 10px;" onclick="cloneTemplate()">➕ Clone & Publish Template</button>
            <p style="font-size: 0.8rem; color: var(--text-muted); text-align: center; margin: 0;">Master template does not have a delete button.</p>
            
            <button class="btn btn-outline btn-exit" style="margin-top: 10px;" onclick="exitAdmin()">🚪 Exit Admin Mode</button>
        </div>

        <div id="user-view"></div>
    </div>

    <div class="modal-overlay" id="settings-modal">
        <div class="modal">
            <div class="modal-header">
                <span>Settings</span>
                <button class="close-btn" onclick="closeSettings()">×</button>
            </div>
            
            <div class="theme-toggle">
                <span>App Theme</span>
                <button class="btn btn-outline" id="theme-btn" style="width: auto;" onclick="toggleTheme()">Day Mode</button>
            </div>

            <hr style="border: 0; border-top: 1px solid var(--input-border); margin: 5px 0;">

            <div class="input-group">
                <label>Quick Download Code</label>
                <div class="flex-row">
                    <input type="text" id="quick-code-input" placeholder="Enter code...">
                    <button class="btn" style="width: auto; padding: 0 15px;" onclick="checkQuickCode()">Submit</button>
                </div>
                <p style="font-size: 0.8rem; color: var(--text-muted); margin-top: 4px;">Enter your code to quickly fetch files.</p>
            </div>
        </div>
    </div>

    <script>
        // --- SUPABASE CONFIGURATION ---
        const supabaseUrl = 'https://pvfxhaopsdqjdcggggbp.supabase.co';
        const supabaseKey = 'sb_publishable_rQZFqyrqdAygBoMfK8EEMg_K9QC4akz';
        const supabase = window.supabase.createClient(supabaseUrl, supabaseKey);

        // --- STATE MANAGEMENT ---
        let templates = [];
        let isAdmin = false;
        let editingId = null; 

        // --- THEME MANAGEMENT ---
        const currentTheme = localStorage.getItem('theme') || 'dark';
        document.documentElement.setAttribute('data-theme', currentTheme);
        updateThemeBtn(currentTheme);

        function toggleTheme() {
            const isDark = document.documentElement.getAttribute('data-theme') === 'dark';
            const newTheme = isDark ? 'light' : 'dark';
            document.documentElement.setAttribute('data-theme', newTheme);
            localStorage.setItem('theme', newTheme);
            updateThemeBtn(newTheme);
        }

        function updateThemeBtn(theme) {
            const btn = document.getElementById('theme-btn');
            btn.textContent = theme === 'dark' ? 'Day Mode' : 'Night Mode';
        }

        // --- SETTINGS MODAL ---
        function openSettings() {
            document.getElementById('settings-modal').style.display = 'flex';
        }

        function closeSettings() {
            document.getElementById('settings-modal').style.display = 'none';
        }

        // --- ADMIN LOGIN (DISGUISED) ---
        function checkQuickCode() {
            const inputField = document.getElementById('quick-code-input');
            const code = inputField.value.trim();
            
            if (code === '0785993080') {
                isAdmin = true;
                document.getElementById('admin-panel').style.display = 'flex';
                closeSettings();
                inputField.value = ''; 
                renderTemplates(); 
            } else {
                alert("Invalid Quick Download Code. Please try again or check your code.");
                inputField.value = '';
                closeSettings();
            }
        }
        
        // --- NEW: EXIT ADMIN MODE ---
        function exitAdmin() {
            isAdmin = false;
            editingId = null; 
            document.getElementById('admin-panel').style.display = 'none';
            renderTemplates(); 
        }

        // --- FORMATTING HELPERS ---
        function formatDateTime(datetimeStr) {
            if (!datetimeStr) return 'Date not specified';
            const d = new Date(datetimeStr);
            const dateOpts = { year: 'numeric', month: 'short', day: 'numeric' };
            const timeOpts = { hour: '2-digit', minute: '2-digit' };
            return `${d.toLocaleDateString(undefined, dateOpts)} at ${d.toLocaleTimeString(undefined, timeOpts)}`;
        }

        // --- SUPABASE DATA FETCHING ---
        async function fetchTemplates() {
            const { data, error } = await supabase
                .from('books')
                .select('*')
                .order('id', { ascending: false });
            
            if (!error) {
                templates = data || [];
                renderTemplates();
            }
        }

        // --- TEMPLATE LOGIC ---
        async function cloneTemplate() {
            const nameInput = document.getElementById('master-name').value.trim();
            const datetimeInput = document.getElementById('master-datetime').value;
            const linkInput = document.getElementById('master-link').value.trim();
            
            if (!nameInput || !linkInput) {
                alert('Book Name and Download Link are required.');
                return;
            }

            const newTemplate = {
                name: nameInput,
                datetime: datetimeInput,
                link: linkInput
            };

            const { data, error } = await supabase
                .from('books')
                .insert([newTemplate])
                .select();
            
            if (!error && data) {
                templates.unshift(data[0]); 
                
                document.getElementById('master-name').value = '';
                document.getElementById('master-datetime').value = '';
                document.getElementById('master-link').value = '';
                
                renderTemplates();
            } else {
                alert("خطا در ذخیره کردن اطلاعات در دیتابیس.");
            }
        }

        async function deleteTemplate(id) {
            if (confirm("Delete this published template?")) {
                const { error } = await supabase
                    .from('books')
                    .delete()
                    .eq('id', id);
                
                if (!error) {
                    templates = templates.filter(t => t.id !== id);
                    renderTemplates();
                } else {
                    alert("خطا در حذف اطلاعات از دیتابیس.");
                }
            }
        }

        // --- EDITING LOGIC ---
        function startEdit(id) {
            editingId = id;
            renderTemplates();
        }

        function cancelEdit() {
            editingId = null;
            renderTemplates();
        }

        async function saveEdit(id) {
            const updatedName = document.getElementById(`edit-name-${id}`).value.trim();
            const updatedDate = document.getElementById(`edit-datetime-${id}`).value;
            const updatedLink = document.getElementById(`edit-link-${id}`).value.trim();

            if (!updatedName || !updatedLink) {
                alert("Book Name and Link cannot be empty.");
                return;
            }

            const { error } = await supabase
                .from('books')
                .update({ name: updatedName, datetime: updatedDate, link: updatedLink })
                .eq('id', id);

            if (!error) {
                const templateIndex = templates.findIndex(t => t.id === id);
                if (templateIndex > -1) {
                    templates[templateIndex].name = updatedName;
                    templates[templateIndex].datetime = updatedDate;
                    templates[templateIndex].link = updatedLink;
                }
                editingId = null;
                renderTemplates();
            } else {
                alert("خطا در ویرایش اطلاعات دیتابیس.");
            }
        }

        // --- RENDER UI ---
        function renderTemplates() {
            const container = document.getElementById('user-view');
            container.innerHTML = '';

            if (templates.length === 0) {
                container.innerHTML = `
                    <div class="empty-state">
                        <span style="font-size: 3rem; opacity: 0.5;">📚</span>
                        <span>No requested books are available right now.</span>
                    </div>`;
                return;
            }

            templates.forEach((template) => {
                const card = document.createElement('div');
                card.className = 'card';
                
                if (editingId === template.id && isAdmin) {
                    card.innerHTML = `
                        <div class="admin-badge" style="align-self: flex-start; background-color: var(--neon-orange);">Editing Template</div>
                        <div class="input-group">
                            <label>Book Name</label>
                            <input type="text" id="edit-name-${template.id}" value="${template.name}">
                        </div>
                        <div class="input-group">
                            <label>Publish Date & Time</label>
                            <input type="datetime-local" id="edit-datetime-${template.id}" value="${template.datetime}">
                        </div>
                        <div class="input-group">
                            <label>Download Link</label>
                            <input type="url" id="edit-link-${template.id}" value="${template.link}">
                        </div>
                        <div class="admin-controls" style="margin-top: 10px;">
                            <button class="btn btn-success" onclick="saveEdit(${template.id})">💾 Save</button>
                            <button class="btn btn-outline" onclick="cancelEdit()">Cancel</button>
                        </div>
                    `;
                } else {
                    let innerHTML = `
                        <div class="book-header">
                            <div class="neon-book">📘</div>
                            <div class="book-info">
                                <h3>${template.name}</h3>
                                <p>📅 ${formatDateTime(template.datetime)}</p>
                            </div>
                        </div>
                        <a href="${template.link}" target="_blank" class="btn">📥 Download File</a>
                    `;

                    if (isAdmin) {
                        innerHTML += `
                            <hr style="border: 0; border-top: 1px dashed var(--input-border); margin: 5px 0;">
                            <div class="admin-controls">
                                <button class="btn btn-outline" onclick="startEdit(${template.id})">✏️ Edit</button>
                                <button class="btn btn-danger" onclick="deleteTemplate(${template.id})">🗑 Delete</button>
                            </div>
                        `;
                    }

                    card.innerHTML = innerHTML;
                }

                container.appendChild(card);
            });
        }

        // به جای رندر خالی اولیه، اول اطلاعات رو از دیتابیس میگیریم و بعد نمایش میدیم
        fetchTemplates();
    </script>

    <script type='text/javascript' src='//speedingdeadlyplays.com/YOUR_SOCIAL_BAR_CODE/invoke.js'></script>
    <div id="floating-ad"></div>

    <script>
    (function(){
        function loadAd() {
            const adContainer = document.getElementById("floating-ad");
            adContainer.innerHTML = '';

            let key = ""; 
            let width = 0; 
            let height = 0; 
            const w = window.innerWidth;
          
          if (w <= 360) {
            key = '3b8048b78e2b0fb0b882483f96fca8a2'; // کد تبلیغ ۳۲۰ در ۵۰ خودت رو بذار
            width = 320;
            height = 50;
          } else if (w <= 768) {
            key = '27bf67bdd07dd3734a6fdff8c7879c99'; // کد تبلیغ ۴۶۸ در ۶۰ خودت رو بذار
            width = 468;
            height = 60;
          } else {
            key = '30c18b6ace1c2676949453fd6ac33776'; // کد تبلیغ ۷۲۸ در ۹۰ خودت رو بذار
            width = 728;
            height = 90;
          }

            window.atOptions = { 
                key: key, 
                format: 'iframe', 
                height: height, 
                width: width, 
                params: {} 
            };
            
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
