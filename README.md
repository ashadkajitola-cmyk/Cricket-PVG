<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Schedule & Betting Platform Pro</title>
    <style>
        :root {
            --primary: #1e3c72;
            --secondary: #2a5298;
            --accent: #ff9800;
            --bg: #f4f7f6;
            --white: #ffffff;
            --text: #333333;
            --danger: #e74c3c;
            --success: #2ecc71;
            --border: #e0e0e0;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: var(--bg); color: var(--text); padding-bottom: 50px; }
        header { background: linear-gradient(135deg, var(--primary), var(--secondary)); color: var(--white); padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 4px 15px rgba(0,0,0,0.15); }
        header h1 { font-size: 1.3rem; font-weight: 700; letter-spacing: 0.5px; }
        .user-info { display: flex; gap: 12px; align-items: center; font-size: 0.9rem; }
        .wallet-badge { background: var(--accent); color: #000; padding: 6px 12px; border-radius: 20px; font-weight: bold; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .container { max-width: 900px; margin: 20px auto; padding: 0 15px; }
        .card { background: var(--white); border-radius: 10px; padding: 20px; margin-bottom: 20px; box-shadow: 0 4px 10px rgba(0,0,0,0.05); }
        .btn { background: var(--secondary); color: var(--white); border: none; padding: 10px 18px; border-radius: 6px; cursor: pointer; font-weight: bold; transition: 0.2s; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .btn:hover { opacity: 0.9; transform: translateY(-1px); }
        .btn-danger { background: var(--danger); }
        .btn-success { background: var(--success); }
        .btn-warning { background: var(--accent); color: #000; }
        input, select, textarea { width: 100%; padding: 12px; margin: 8px 0 15px 0; border: 1px solid var(--border); border-radius: 6px; font-size: 0.95rem; background: #fff; }
        label { font-weight: 600; font-size: 0.85rem; color: #555; }
        .tabs { display: flex; gap: 10px; margin-bottom: 20px; background: #e9ecef; padding: 5px; border-radius: 8px; }
        .tab-btn { flex: 1; padding: 12px; background: transparent; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; color: #555; transition: 0.2s; }
        .tab-btn.active { background: var(--white); color: var(--primary); box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        
        .match-card { border: 1px solid var(--border); border-radius: 8px; padding: 15px; margin-bottom: 15px; background: var(--white); box-shadow: 0 2px 5px rgba(0,0,0,0.02); }
        .series-title-bar { background: #e8f4fd; color: #1a5276; padding: 8px 12px; border-radius: 6px; font-weight: bold; font-size: 0.95rem; margin-bottom: 12px; display: flex; justify-content: space-between; align-items: center; }
        .match-row { display: flex; justify-content: space-between; align-items: center; margin: 10px 0; }
        .team-box { font-size: 1.1rem; font-weight: bold; display: flex; align-items: center; gap: 8px; }
        .vs-text { font-weight: bold; color: #888; font-size: 0.9rem; }
        .match-meta { font-size: 0.85rem; color: #666; margin-top: 8px; border-top: 1px dashed var(--border); padding-top: 8px; display: flex; justify-content: space-between; flex-wrap: wrap; gap: 5px; }
        
        .hidden { display: none !important; }
        .flex-row { display: flex; gap: 10px; }
        .flex-row > * { flex: 1; }
        .modal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); display: flex; justify-content: center; align-items: center; z-index: 1000; overflow-y: auto; padding: 20px; }
        .modal-content { background: var(--white); padding: 25px; border-radius: 10px; width: 100%; max-width: 550px; position: relative; max-height: 90vh; overflow-y: auto; }
        .close-modal { position: absolute; top: 12px; right: 18px; font-size: 1.4rem; cursor: pointer; color: #888; }
        .alert-box { padding: 12px; margin-bottom: 12px; border-radius: 6px; font-size: 0.9rem; }
        .alert-error { background: #fadbd8; color: #78281f; }
        .alert-success { background: #d4efdf; color: #145a32; }
    </style>
</head>
<body>

    <header>
        <h1>🏏 Cricket Schedule & Betting Pro</h1>
        <div class="user-info">
            <span id="displayNumber" style="font-weight: 650;">Login करें</span>
            <span class="wallet-badge">Wallet: ₹<span id="displayWallet">0</span></span>
            <button class="btn btn-danger" onclick="logout()" style="padding: 6px 12px; font-size: 0.8rem;">Logout</button>
        </div>
    </header>

    <div class="container">
        <!-- Login Section -->
        <div id="loginSection" class="card">
            <h2>Login / Register</h2>
            <p id="deviceLimitInfo" style="font-size:0.85rem; color:#666; margin-bottom:12px;"></p>
            <label>Mobile Number:</label>
            <input type="text" id="loginMobileInput" placeholder="Enter mobile number">
            <button class="btn" style="width:100%;" onclick="handleLogin()">Login to Dashboard</button>
        </div>

        <!-- Main Dashboard -->
        <div id="mainDashboard" class="hidden">
            
            <!-- Recharge / Transaction ID Card -->
            <div class="card" style="border-left: 5px solid var(--success);">
                <h3>💳 Wallet Recharge Request (Transaction ID)</h3>
                <p style="font-size: 0.85rem; color: #666; margin-bottom: 10px;">Payment SMS ki Full Transaction ID ya UTR number yahan dalein. Admin verify karne ke baad ₹210 approve karega.</p>
                <label>Full Transaction ID / UTR:</label>
                <input type="text" id="txFullInput" placeholder="Enter full transaction reference ID">
                <button class="btn btn-success" onclick="submitRechargeRequest()" style="width:100%;">Submit for Admin Verification</button>
            </div>

            <!-- Dashboard Access Button / Panel Trigger -->
            <div class="card" style="border-left: 5px solid var(--accent);">
                <h3>🚀 Apna Schedule Dashboard</h3>
                <p style="font-size: 0.85rem; color: #666; margin-bottom: 10px;">Apna khud ka schedule create karne ke liye panel open karein (Subscription zaroori hai).</p>
                <button class="btn btn-warning" style="width: 100%;" onclick="openCreatorDashboard()">📂 Open My Schedule Dashboard</button>
            </div>

            <!-- Active Subscription Status Box -->
            <div id="activeSubStatusBox" class="card hidden" style="border-left: 5px solid var(--primary); background: #f0f4f8;">
                <h3>✨ Active Subscription Status</h3>
                <div id="subStatusContent" style="margin-top: 10px; font-size: 0.95rem;"></div>
            </div>

            <!-- Code Verification Box -->
            <div class="card">
                <h3>🔍 6-Digit Code Verification</h3>
                <div class="flex-row">
                    <input type="text" id="verifyCodeInput" maxlength="6" placeholder="Enter 6-digit match code">
                    <button class="btn" onclick="verifyMatchCode()" style="margin-top:8px;">Check Code</button>
                </div>
                <div id="verifyResult" style="margin-top: 10px;"></div>
            </div>

            <!-- Tabs -->
            <div class="tabs">
                <button class="tab-btn active" onclick="switchTab('international')">🌍 International Schedule</button>
                <button class="tab-btn" onclick="switchTab('apna')">👤 Apna Schedule</button>
                <button class="tab-btn" onclick="switchTab('activeTickets')">🎟️ Active Tickets & Satta</button>
            </div>

            <!-- Tab Content -->
            <div id="internationalTabContent" class="tab-content">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
                    <h2>International Matches (Website Admin)</h2>
                    <button id="adminCreateMatchBtn" class="btn btn-success hidden" onclick="openInternationalMatchModal()">+ Create International Match</button>
                </div>
                <div id="internationalMatchesList" style="margin-top: 15px;"></div>
            </div>

            <div id="apnaTabContent" class="tab-content hidden">
                <h2>Apna Schedule (User Created)</h2>
                <div id="apnaMatchesList" style="margin-top: 15px;"></div>
            </div>

            <div id="activeTicketsTabContent" class="tab-content hidden">
                <h2>Active Tickets & Satta</h2>
                <div id="activeTicketsList" style="margin-top: 15px;"></div>
            </div>

        </div>
    </div>

    <!-- Creator Dashboard / Subscription Modal -->
    <div id="creatorModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeCreatorModal()">&times;</span>
            
            <div id="subscriptionRequiredView">
                <h3 style="margin-bottom: 10px; color: var(--danger);">📢 Subscription Required</h3>
                <p style="font-size:0.85rem; color:#666; margin-bottom:15px;">Apna schedule create karne ke liye pehle subscription plan kharidein:</p>
                <div id="subPlansList" style="display: flex; flex-direction: column; gap: 8px; margin-bottom: 15px;"></div>
                <button class="btn btn-success" style="width:100%;" onclick="buySelectedSubscription()">Subscription Buy Karein</button>
            </div>

            <div id="creatorActionView" class="hidden">
                <h3 style="margin-bottom: 15px;">👤 User Creator Panel</h3>
                <p style="font-size: 0.9rem; color: var(--success); margin-bottom: 15px; font-weight: bold;">✔ Aapke paas active subscription hai. Aap apna schedule create kar sakte hain!</p>
                <button class="btn" style="width:100%; margin-bottom: 10px;" onclick="openMatchModal()">+ Create Apna Match Schedule</button>
                
                <div id="mainAdminExtraControls" class="hidden" style="margin-top: 15px; border-top: 1px dashed var(--border); padding-top: 15px;">
                    <h4 style="margin-bottom: 10px; color: var(--primary);">👑 Master Admin Controls</h4>
                    <button class="btn btn-warning" style="width:100%; margin-bottom: 8px;" onclick="openRechargeRequestsModal()">📥 Verify Recharge Requests (<span id="pendingCountBadge">0</span>)</button>
                    <button class="btn btn-danger" style="width:100%;" onclick="openAdminEditModal()">⚙️ Website Edit Panel</button>
                </div>
            </div>

        </div>
    </div>

    <!-- Match Creation Modal (User) -->
    <div id="matchModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeMatchModal()">&times;</span>
            <h3 style="margin-bottom: 15px;">Create Apna Match Schedule</h3>
            
            <label>Series Name:</label>
            <input type="text" id="matchSeriesName" placeholder="e.g., Local League 2026">

            <div class="flex-row">
                <div><label>Team 1 Name:</label><input type="text" id="matchTeam1" placeholder="Team A"></div>
                <div><label>Team 2 Name:</label><input type="text" id="matchTeam2" placeholder="Team B"></div>
            </div>

            <div class="flex-row">
                <div><label>Team 1 Score:</label><input type="text" id="matchScore1" placeholder="180/4"></div>
                <div><label>Team 2 Score:</label><input type="text" id="matchScore2" placeholder="175/8"></div>
            </div>

            <label>Date & Time:</label>
            <input type="datetime-local" id="matchDateTime">

            <label>Venue:</label>
            <input type="text" id="matchVenue" placeholder="Ground Name">

            <div class="flex-row">
                <div><label>Ticket Price (₹):</label><input type="number" id="matchPrice" placeholder="100"></div>
                <div><label>Total Tickets Limit:</label><input type="number" id="matchLimit" placeholder="50"></div>
            </div>

            <label>6-Digit Security Code:</label>
            <input type="text" id="matchCode6" maxlength="6" placeholder="6 digit code">

            <label>Result / Winner Status:</label>
            <select id="matchResultStatus">
                <option value="Upcoming">Upcoming / Live</option>
                <option value="Team 1 Won">Team 1 Won (Double Payout)</option>
                <option value="Team 2 Won">Team 2 Won (Double Payout)</option>
                <option value="Draw / Abandoned">Draw / Refund</option>
            </select>

            <button class="btn" style="width:100%; margin-top:10px;" onclick="saveMatchSchedule(false)">Save & Publish Apna Schedule</button>
        </div>
    </div>

    <!-- International Match Creation Modal (Admin) -->
    <div id="internationalMatchModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeInternationalMatchModal()">&times;</span>
            <h3 style="margin-bottom: 15px;">🌍 Create International Match (Admin)</h3>
            
            <label>Series Name:</label>
            <input type="text" id="intSeriesName" placeholder="e.g., ICC World Cup 2026">

            <div class="flex-row">
                <div><label>Team 1 Name:</label><input type="text" id="intTeam1" placeholder="India"></div>
                <div><label>Team 2 Name:</label><input type="text" id="intTeam2" placeholder="Australia"></div>
            </div>

            <div class="flex-row">
                <div><label>Team 1 Score:</label><input type="text" id="intScore1" placeholder="250/5"></div>
                <div><label>Team 2 Score:</label><input type="text" id="intScore2" placeholder="240/10"></div>
            </div>

            <label>Date & Time:</label>
            <input type="datetime-local" id="intDateTime">

            <label>Venue:</label>
            <input type="text" id="intVenue" placeholder="Stadium Name">

            <div class="flex-row">
                <div><label>Ticket Price (₹):</label><input type="number" id="intPrice" placeholder="200"></div>
                <div><label>Total Tickets Limit:</label><input type="number" id="intLimit" placeholder="100"></div>
            </div>

            <label>6-Digit Security Code:</label>
            <input type="text" id="intCode6" maxlength="6" placeholder="6 digit code">

            <label>Result / Winner Status:</label>
            <select id="intResultStatus">
                <option value="Upcoming">Upcoming / Live</option>
                <option value="Team 1 Won">Team 1 Won (Double Payout)</option>
                <option value="Team 2 Won">Team 2 Won (Double Payout)</option>
                <option value="Draw / Abandoned">Draw / Refund</option>
            </select>

            <button class="btn" style="width:100%; margin-top:10px;" onclick="saveMatchSchedule(true)">Publish International Match</button>
        </div>
    </div>

    <!-- Admin Recharge Verification Modal -->
    <div id="rechargeModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeRechargeModal()">&times;</span>
            <h3 style="margin-bottom: 15px;">📥 Pending Recharge Requests</h3>
            <div id="pendingRechargesList" style="margin-top: 10px;"></div>
        </div>
    </div>

    <!-- Admin Edit Panel Modal (Full Customization) -->
    <div id="adminEditModal" class="modal hidden">
        <div class="modal-content">
            <span class="close-modal" onclick="closeAdminEditModal()">&times;</span>
            <h3 style="margin-bottom: 15px;">⚙️ Website Edit & Customization Panel</h3>
            
            <label>Website Admin Number:</label>
            <input type="text" id="editAdminNumber">

            <label>Max Numbers Allowed Per Device:</label>
            <input type="number" id="editMaxDevices">

            <h4 style="margin-top: 15px; margin-bottom: 8px; color: var(--primary);">Subscription Plan Names & Rates (₹) & Delete Option:</h4>
            <div id="adminPlansEditContainer"></div>

            <button class="btn btn-success" style="width:100%; margin-top:10px;" onclick="addNewPlanField()">+ Add New Subscription Plan</button>
            <button class="btn" style="width:100%; margin-top:15px;" onclick="saveAdminSettings()">Save All Website Settings</button>
        </div>
    </div>

    <script>
        const DEFAULT_ADMIN = "9569981484";
        
        let db = JSON.parse(localStorage.getItem('cricket_pro_db')) || {
            users: {},
            matches: [],
            tickets: [],
            rechargeRequests: [],
            usedTransactions: [],
            settings: {
                adminNumber: DEFAULT_ADMIN,
                maxDevices: 4,
                plans: [
                    { id: '4hour', name: '4 Hour Pass', price: 99, durationHours: 4 },
                    { id: '1day', name: '1 Day Pass', price: 108, durationHours: 24, matchesCount: 1 },
                    { id: '1match', name: '1 Match Pass', price: 200, matchesCount: 1 },
                    { id: 'halfMonth', name: 'Half Month Plan', price: 299, durationDays: 15 },
                    { id: 'month', name: 'Monthly Plan', price: 449, durationDays: 30 },
                    { id: 'year', name: 'Yearly Plan', price: 4000, durationDays: 365 }
                ]
            },
            deviceSessions: {}
        };

        if (!db.settings.plans) {
            db.settings.plans = [
                { id: '4hour', name: '4 Hour Pass', price: 99, durationHours: 4 },
                { id: '1day', name: '1 Day Pass', price: 108, durationHours: 24, matchesCount: 1 },
                { id: '1match', name: '1 Match Pass', price: 200, matchesCount: 1 },
                { id: 'halfMonth', name: 'Half Month Plan', price: 299, durationDays: 15 },
                { id: 'month', name: 'Monthly Plan', price: 449, durationDays: 30 },
                { id: 'year', name: 'Yearly Plan', price: 4000, durationDays: 365 }
            ];
        }

        let currentMobile = localStorage.getItem('cricket_pro_current_mobile') || null;
        let deviceId = localStorage.getItem('cricket_pro_device_id') || 'dev_' + Math.random().toString(36).substring(2,9);
        localStorage.setItem('cricket_pro_device_id', deviceId);

        function saveDB() {
            localStorage.setItem('cricket_pro_db', JSON.stringify(db));
        }

        window.onload = function() {
            // Ensure admin exists with 50000 starting balance if not initialized
            if (!db.users[db.settings.adminNumber]) {
                db.users[db.settings.adminNumber] = { wallet: 50000, subscription: null };
            }

            if (currentMobile && db.users[currentMobile]) {
                showDashboard();
            } else {
                currentMobile = null;
                showLogin();
            }
        };

        function showLogin() {
            document.getElementById('loginSection').classList.remove('hidden');
            document.getElementById('mainDashboard').classList.add('hidden');
            document.getElementById('deviceLimitInfo').innerText = `(Max ${db.settings.maxDevices} numbers allowed per device)`;
        }

        function showDashboard() {
            document.getElementById('loginSection').classList.add('hidden');
            document.getElementById('mainDashboard').classList.remove('hidden');
            
            if (currentMobile === db.settings.adminNumber) {
                document.getElementById('adminCreateMatchBtn').classList.remove('hidden');
            } else {
                document.getElementById('adminCreateMatchBtn').classList.add('hidden');
            }

            updateHeader();
            renderSubscriptionStatusBox();
            renderSubscriptionPlans();
            renderMatches();
            renderActiveTickets();
        }

        function handleLogin() {
            let mobile = document.getElementById('loginMobileInput').value.trim();
            if (!mobile || mobile.length < 10) {
                alert("Kripya sahi 10-digit mobile number enter karein!");
                return;
            }

            if (!db.deviceSessions[deviceId]) db.deviceSessions[deviceId] = [];
            let activeNumbers = db.deviceSessions[deviceId];
            
            if (!activeNumbers.includes(mobile)) {
                if (activeNumbers.length >= db.settings.maxDevices) {
                    alert(`Is device par maximum ${db.settings.maxDevices} numbers hi allow hain!`);
                    return;
                }
                activeNumbers.push(mobile);
            }

            if (!db.users[mobile]) {
                // If logging in as the active admin number for the first time, give 50000, otherwise standard 100
                let initialWallet = (mobile === db.settings.adminNumber) ? 50000 : 100;
                db.users[mobile] = { wallet: initialWallet, subscription: null };
            }

            currentMobile = mobile;
            localStorage.setItem('cricket_pro_current_mobile', currentMobile);
            saveDB();
            showDashboard();
        }

        function logout() {
            currentMobile = null;
            localStorage.removeItem('cricket_pro_current_mobile');
            showLogin();
        }

        function updateHeader() {
            document.getElementById('displayNumber').innerText = currentMobile;
            let user = db.users[currentMobile];
            document.getElementById('displayWallet').innerText = user ? user.wallet : 0;
            
            if (currentMobile === db.settings.adminNumber) {
                let pending = (db.rechargeRequests || []).filter(r => r.status === 'Pending').length;
                let badge = document.getElementById('pendingCountBadge');
                if (badge) badge.innerText = pending;
            }
        }

        function submitRechargeRequest() {
            let txInput = document.getElementById('txFullInput').value.trim();
            if (!txInput || txInput.length < 6) {
                alert("Kripya valid Transaction ID / UTR enter karein!");
                return;
            }

            if (!db.usedTransactions) db.usedTransactions = [];
            if (db.usedTransactions.includes(txInput)) {
                alert("Yeh Transaction ID pehle hi use ya verify ki ja chuki hai!");
                return;
            }

            if (!db.rechargeRequests) db.rechargeRequests = [];
            let existingPending = db.rechargeRequests.find(r => r.txId === txInput && r.status === 'Pending');
            if (existingPending) {
                alert("Is Transaction ID ki request pehle se hi Admin verification me pending hai!");
                return;
            }

            db.rechargeRequests.push({
                id: 'req_' + Date.now(),
                mobile: currentMobile,
                txId: txInput,
                status: 'Pending'
            });

            saveDB();
            document.getElementById('txFullInput').value = '';
            alert("Aapki recharge request Admin ke paas bhej di gayi hai! Verification ke baad ₹210 wallet me add ho jayenge.");
        }

        function openRechargeRequestsModal() {
            if (currentMobile !== db.settings.adminNumber) return;
            let listDiv = document.getElementById('pendingRechargesList');
            let pending = (db.rechargeRequests || []).filter(r => r.status === 'Pending');

            if (pending.length === 0) {
                listDiv.innerHTML = '<p>Koi pending recharge request nahi hai.</p>';
            } else {
                let html = '';
                pending.forEach(req => {
                    html += `
                        <div class="match-card" style="border-left: 5px solid var(--accent); padding:10px; margin-bottom:10px;">
                            <p><strong>Mobile:</strong> ${req.mobile}</p>
                            <p><strong>Tx ID / UTR:</strong> ${req.txId}</p>
                            <div style="margin-top:8px; display:flex; gap:10px;">
                                <button class="btn btn-success" style="padding:5px 10px; font-size:0.8rem;" onclick="approveRecharge('${req.id}')">Approve & Send ₹210</button>
                                <button class="btn btn-danger" style="padding:5px 10px; font-size:0.8rem;" onclick="rejectRecharge('${req.id}')">Decline / Reject</button>
                            </div>
                        </div>
                    `;
                });
                listDiv.innerHTML = html;
            }
            document.getElementById('rechargeModal').classList.remove('hidden');
        }

        function closeRechargeModal() { document.getElementById('rechargeModal').classList.add('hidden'); }

        function approveRecharge(reqId) {
            let req = db.rechargeRequests.find(r => r.id === reqId);
            if (!req) return;

            if (!db.usedTransactions) db.usedTransactions = [];
            db.usedTransactions.push(req.txId);
            req.status = 'Approved';

            if (!db.users[req.mobile]) db.users[req.mobile] = { wallet: 0, subscription: null };
            db.users[req.mobile].wallet += 210;

            saveDB();
            updateHeader();
            openRechargeRequestsModal();
            alert("Request approve ho gayi aur ₹210 user ke wallet me bhej diye gaye!");
        }

        function rejectRecharge(reqId) {
            db.rechargeRequests = db.rechargeRequests.filter(r => r.id !== reqId);
            saveDB();
            updateHeader();
            openRechargeRequestsModal();
            alert("Request reject kar di gayi.");
        }

        function checkUserHasActiveSub() {
            let isAdmin = (currentMobile === db.settings.adminNumber);
            if (isAdmin) return true;

            let user = db.users[currentMobile];
            if (user && user.subscription) {
                if (user.subscription.matchesLeft !== undefined) {
                    return user.subscription.matchesLeft > 0;
                } else {
                    return new Date().getTime() < user.subscription.expiresAt;
                }
            }
            return false;
        }

        function renderSubscriptionStatusBox() {
            let box = document.getElementById('activeSubStatusBox');
            let content = document.getElementById('subStatusContent');
            let user = db.users[currentMobile];
            let isAdmin = (currentMobile === db.settings.adminNumber);

            if (isAdmin) {
                box.classList.remove('hidden');
                content.innerHTML = `<strong>Role:</strong> Master Website Admin (Full Access)`;
                return;
            }

            if (user && user.subscription && checkUserHasActiveSub()) {
                box.classList.remove('hidden');
                let sub = user.subscription;
                let now = new Date().getTime();
                let timeLeftText = '';

                if (sub.matchesLeft !== undefined && sub.expiresAt > now + (30*24*3600*1000)) {
                    timeLeftText = `Matches Left: ${sub.matchesLeft}`;
                } else if (sub.matchesLeft !== undefined && sub.expiresAt && now < sub.expiresAt) {
                    let diffMs = sub.expiresAt - now;
                    let diffHrs = Math.floor(diffMs / (1000 * 60 * 60));
                    timeLeftText = `Matches Left: ${sub.matchesLeft} | Time: ${diffHrs}h`;
                } else if (sub.matchesLeft !== undefined) {
                    timeLeftText = `Matches Left: ${sub.matchesLeft}`;
                } else {
                    let diffMs = sub.expiresAt - now;
                    let diffHrs = Math.floor(diffMs / (1000 * 60 * 60));
                    let diffDays = Math.floor(diffHrs / 24);
                    timeLeftText = diffDays > 0 ? `Bache hue din: ${diffDays} Days (~${diffHrs} Hours)` : `Bacha hua samay: ${diffHrs} Hours`;
                }
                content.innerHTML = `<strong>Plan:</strong> ${sub.planName} <br><strong>Status:</strong> Active <br>⏱️ ${timeLeftText}`;
            } else {
                box.classList.add('hidden');
            }
        }

        function openCreatorDashboard() {
            let modal = document.getElementById('creatorModal');
            let reqView = document.getElementById('subscriptionRequiredView');
            let actView = document.getElementById('creatorActionView');
            let adminControls = document.getElementById('mainAdminExtraControls');

            if (checkUserHasActiveSub()) {
                reqView.classList.add('hidden');
                actView.classList.remove('hidden');
                if (currentMobile === db.settings.adminNumber) {
                    adminControls.classList.remove('hidden');
                } else {
                    adminControls.classList.add('hidden');
                }
            } else {
                reqView.classList.remove('hidden');
                actView.classList.add('hidden');
            }
            modal.classList.remove('hidden');
        }

        function closeCreatorModal() { document.getElementById('creatorModal').classList.add('hidden'); }

        function renderSubscriptionPlans() {
            let listHTML = '';
            if (db.settings.plans.length === 0) {
                listHTML = '<p style="color:red; font-size:0.85rem;">Koi subscription plan available nahi hai.</p>';
            } else {
                db.settings.plans.forEach((plan, index) => {
                    let checked = index === 0 ? 'checked' : '';
                    listHTML += `<label><input type="radio" name="subPlan" value="${plan.id}" ${checked}> ${plan.name} - ₹${plan.price}</label>`;
                });
            }
            document.getElementById('subPlansList').innerHTML = listHTML;
        }

        function buySelectedSubscription() {
            let selectedRadio = document.querySelector('input[name="subPlan"]:checked');
            if (!selectedRadio) {
                alert("Kripya pehle koi plan select karein!");
                return;
            }
            let selectedId = selectedRadio.value;
            let planObj = db.settings.plans.find(p => p.id === selectedId);
            if (!planObj) return;

            let user = db.users[currentMobile];
            if (user.wallet < planObj.price) {
                alert("Wallet me balance kam hai! Pehle Transaction ID se recharge request dalein.");
                return;
            }

            user.wallet -= planObj.price;
            let adminMob = db.settings.adminNumber;
            if (!db.users[adminMob]) db.users[adminMob] = { wallet: 50000, subscription: null };
            db.users[adminMob].wallet += planObj.price;

            let now = new Date().getTime();
            let expiresAt = now;
            let matchesLeft = undefined;

            if (planObj.durationHours) expiresAt = now + (planObj.durationHours * 3600 * 1000);
            if (planObj.durationDays) expiresAt = now + (planObj.durationDays * 24 * 3600 * 1000);
            if (planObj.matchesCount) {
                matchesLeft = planObj.matchesCount;
                if (!planObj.durationDays && !planObj.durationHours) expiresAt = now + (7 * 24 * 3600 * 1000);
            }

            user.subscription = { planId: planObj.id, planName: planObj.name, expiresAt: expiresAt, matchesLeft: matchesLeft };

            saveDB();
            updateHeader();
            renderSubscriptionStatusBox();
            closeCreatorModal();
            alert("Subscription successfully buy ho gaya!");
        }

        function openMatchModal() { closeCreatorModal(); document.getElementById('matchModal').classList.remove('hidden'); }
        function closeMatchModal() { document.getElementById('matchModal').classList.add('hidden'); }

        function openInternationalMatchModal() { document.getElementById('internationalMatchModal').classList.remove('hidden'); }
        function closeInternationalMatchModal() { document.getElementById('internationalMatchModal').classList.add('hidden'); }

        function openAdminEditModal() {
            if (currentMobile !== db.settings.adminNumber) return;
            document.getElementById('editAdminNumber').value = db.settings.adminNumber;
            document.getElementById('editMaxDevices').value = db.settings.maxDevices;
            renderAdminPlansEditForm();
            document.getElementById('adminEditModal').classList.remove('hidden');
        }
        function closeAdminEditModal() { document.getElementById('adminEditModal').classList.add('hidden'); }

        function renderAdminPlansEditForm() {
            let container = document.getElementById('adminPlansEditContainer');
            let html = '';
            if (db.settings.plans.length === 0) {
                html = '<p style="color:#666; font-size:0.85rem; margin-bottom:10px;">Koi plan nahi hai. Naya plan add karein.</p>';
            } else {
                db.settings.plans.forEach((plan, idx) => {
                    html += `
                        <div class="flex-row" style="align-items:center; margin-bottom:10px; background:#f9f9f9; padding:8px; border-radius:6px; border:1px solid var(--border);">
                            <div><label>Plan Name:</label><input type="text" id="planName_${idx}" value="${plan.name}"></div>
                            <div><label>Price (₹):</label><input type="number" id="planPrice_${idx}" value="${plan.price}"></div>
                            <div><button type="button" class="btn btn-danger" style="margin-top:22px; padding:10px; width:100%;" onclick="removePlan(${idx})">🗑️ Delete</button></div>
                        </div>
                    `;
                });
            }
            container.innerHTML = html;
        }

        function addNewPlanField() {
            let newId = 'plan_' + Date.now();
            db.settings.plans.push({ id: newId, name: 'New Plan', price: 150, durationDays: 30 });
            renderAdminPlansEditForm();
        }

        function removePlan(idx) {
            if (confirm("Kya aap waqai is subscription plan ko delete karna chahte hain?")) {
                db.settings.plans.splice(idx, 1);
                renderAdminPlansEditForm();
            }
        }

        function saveAdminSettings() {
            let newAdmin = document.getElementById('editAdminNumber').value.trim();
            if (!newAdmin || newAdmin.length < 10) {
                alert("Kripya valid admin mobile number enter karein!");
                return;
            }

            db.settings.adminNumber = newAdmin;
            db.settings.maxDevices = Number(document.getElementById('editMaxDevices').value);

            let updatedPlans = [];
            db.settings.plans.forEach((plan, idx) => {
                let nameInput = document.getElementById(`planName_${idx}`);
                let priceInput = document.getElementById(`planPrice_${idx}`);
                if (nameInput && priceInput) {
                    updatedPlans.push({
                        id: plan.id,
                        name: nameInput.value.trim(),
                        price: Number(priceInput.value),
                        durationDays: plan.durationDays || 30,
                        durationHours: plan.durationHours,
                        matchesCount: plan.matchesCount
                    });
                }
            });
            db.settings.plans = updatedPlans;

            // Ensure new admin profile exists with 50000 free balance if not already present
            if (!db.users[newAdmin]) {
                db.users[newAdmin] = { wallet: 50000, subscription: null };
            }

            saveDB();
            closeAdminEditModal();
            showDashboard();
            alert("Website settings aur plans successfully update ho gaye hain! Naya admin active ho gaya hai aur use 50000₹ free credit mil gaye hain.");
        }

        function saveMatchSchedule(isInternational) {
            let prefix = isInternational ? 'int' : 'match';
            let matchObj = {
                id: 'match_' + Date.now(),
                creator: currentMobile,
                isInternational: isInternational,
                seriesName: document.getElementById(`${prefix}SeriesName`).value.trim(),
                team1: document.getElementById(`${prefix}Team1`).value.trim(),
                team2: document.getElementById(`${prefix}Team2`).value.trim(),
                score1: document.getElementById(`${prefix}Score1`).value.trim(),
                score2: document.getElementById(`${prefix}Score2`).value.trim(),
                dateTime: document.getElementById(`${prefix}DateTime`).value,
                venue: document.getElementById(`${prefix}Venue`).value.trim(),
                price: Number(document.getElementById(`${prefix}Price`).value),
                limit: Number(document.getElementById(`${prefix}Limit`).value),
                soldCount: 0,
                code6: document.getElementById(`${prefix}Code6`).value.trim(),
                resultStatus: document.getElementById(`${prefix}ResultStatus`).value
            };

            if (!matchObj.seriesName || !matchObj.team1 || !matchObj.team2 || matchObj.code6.length !== 6) {
                alert("Sabhi zaroori fields bharein aur 6-digit code sahi dalein!");
                return;
            }

            db.matches.push(matchObj);
            saveDB();
            if (isInternational) closeInternationalMatchModal();
            else closeMatchModal();
            renderMatches();
            alert("Match successfully publish ho gaya!");
        }

        function verifyMatchCode() {
            let code = document.getElementById('verifyCodeInput').value.trim();
            let resDiv = document.getElementById('verifyResult');
            let match = db.matches.find(m => m.code6 === code);

            if (!match) {
                resDiv.innerHTML = `<div class="alert-box alert-error">Invalid Code! Koi match nahi mila.</div>`;
                return;
            }

            resDiv.innerHTML = `
                <div class="alert-box alert-success">
                    <strong>Series:</strong> ${match.seriesName}<br>
                    <strong>Match:</strong> ${match.team1} vs ${match.team2}<br>
                    <strong>Venue:</strong> ${match.venue}
                </div>
            `;
        }

        function renderMatches() {
            let intList = document.getElementById('internationalMatchesList');
            let apnaList = document.getElementById('apnaMatchesList');
            let intHTML = '', apnaHTML = '';

            db.matches.forEach(match => {
                let cardHTML = `
                    <div class="match-card">
                        <div class="series-title-bar">
                            <span>${match.seriesName}</span>
                            <span style="font-size:0.75rem; background:#fff; padding:2px 6px; border-radius:4px;">Code: ${match.code6}</span>
                        </div>
                        <div class="match-row">
                            <div class="team-box">🏏 ${match.team1} <span style="font-size:0.85rem; color:#666;">(${match.score1 || 'Yet to bat'})</span></div>
                            <div class="vs-text">vs</div>
                            <div class="team-box"><span style="font-size:0.85rem; color:#666;">(${match.score2 || 'Yet to bat'})</span> ${match.team2} 🏏</div>
                        </div>
                        <div class="match-meta">
                            <span>📍 ${match.venue}</span>
                            <span>📅 ${match.dateTime || 'TBD'}</span>
                            <span>💰 ₹${match.price} (Sold: ${match.soldCount}/${match.limit})</span>
                        </div>
                        <div style="margin-top: 10px; display:flex; justify-content:space-between; align-items:center;">
                            <span style="font-size:0.85rem; font-weight:bold; color:var(--success);">Status: ${match.resultStatus}</span>
                            <div style="display:flex; gap:8px;">
                                <button class="btn btn-success" style="padding:6px 12px; font-size:0.85rem;" onclick="buyTicket('${match.id}')">Buy Ticket</button>
                                ${(currentMobile === db.settings.adminNumber || currentMobile === match.creator) ? 
                                    `<button class="btn btn-danger" style="padding:6px 12px; font-size:0.85rem;" onclick="deleteMatch('${match.id}')">Delete</button>` : ''}
                            </div>
                        </div>
                    </div>
                `;

                if (match.isInternational) intHTML += cardHTML;
                else if (match.creator === currentMobile) apnaHTML += cardHTML;
            });

            intList.innerHTML = intHTML || '<p>Koi International match available nahi hai.</p>';
            apnaList.innerHTML = apnaHTML || '<p>Aapne apna koi schedule create nahi kiya hai.</p>';
        }

        function buyTicket(matchId) {
            let match = db.matches.find(m => m.id === matchId);
            if (match.soldCount >= match.limit) { alert("Tickets sold out!"); return; }

            let user = db.users[currentMobile];
            if (user.wallet < match.price) { alert("Balance kam hai! Pehle recharge request dalein."); return; }

            user.wallet -= match.price;
            let recipientMob = match.creator || db.settings.adminNumber;
            if (!db.users[recipientMob]) db.users[recipientMob] = { wallet: 50000, subscription: null };
            db.users[recipientMob].wallet += match.price;

            match.soldCount += 1;
            db.tickets.push({
                id: 'tkt_' + Date.now(),
                matchId: match.id,
                mobile: currentMobile,
                pricePaid: match.price,
                teamPicked: null,
                sattaAmount: 0,
                status: 'Active'
            });

            saveDB();
            updateHeader();
            renderMatches();
            renderActiveTickets();
            alert("Ticket successfully buy ho gayi!");
        }

        function renderActiveTickets() {
            let listDiv = document.getElementById('activeTicketsList');
            let userTickets = db.tickets.filter(t => t.mobile === currentMobile && t.status === 'Active');

            if (userTickets.length === 0) {
                listDiv.innerHTML = '<p>Koi active ticket nahi hai.</p>';
                return;
            }

            let html = '';
            userTickets.forEach(tkt => {
                let match = db.matches.find(m => m.id === tkt.matchId);
                if (!match) return;

                if (match.resultStatus === 'Team 1 Won' && tkt.teamPicked === match.team1) settleSatta(tkt, match, true);
                else if (match.resultStatus === 'Team 2 Won' && tkt.teamPicked === match.team2) settleSatta(tkt, match, true);
                else if (match.resultStatus === 'Team 1 Won' || match.resultStatus === 'Team 2 Won') settleSattA(tkt, match, false);

                html += `
                    <div class="match-card" style="border-left: 5px solid var(--success);">
                        <div class="series-title-bar"><span>Ticket ID: ${tkt.id}</span><span>${match.seriesName}</span></div>
                        <p><strong>${match.team1} vs ${match.team2}</strong></p>
                        <div style="margin-top:10px; background:#fcfcfc; padding:12px; border-radius:6px; border:1px solid var(--border);">
                            <h4 style="margin-bottom:8px;">🎲 Satta Zone</h4>
                            ${tkt.teamPicked ? 
                                `<p>Chuni gayi team: <b>${tkt.teamPicked}</b> | Lagaye gaye ₹: <b>${tkt.sattaAmount}</b></p>` :
                                `<label>Konsi team jeete gi?</label>
                                <select id="sattaTeam_${tkt.id}"><option value="${match.team1}">${match.team1}</option><option value="${match.team2}">${match.team2}</option></select>
                                <label>Bet Amount (₹):</label>
                                <input type="number" id="sattaAmt_${tkt.id}" placeholder="Amount">
                                <button class="btn btn-warning" style="width:100%;" onclick="placeSatta('${tkt.id}')">Confirm Satta</button>`
                            }
                        </div>
                    </div>
                `;
            });
            listDiv.innerHTML = html;
        }

        function placeSatta(tktId) {
            let tkt = db.tickets.find(t => t.id === tktId);
            let match = db.matches.find(m => m.id === tkt.matchId);
            let team = document.getElementById(`sattaTeam_${tktId}`).value;
            let amt = Number(document.getElementById(`sattaAmt_${tktId}`).value);

            let user = db.users[currentMobile];
            if (amt <= 0 || user.wallet < amt) { alert("Wallet balance kam hai!"); return; }

            user.wallet -= amt;
            let recipientMob = match.creator || db.settings.adminNumber;
            if (!db.users[recipientMob]) db.users[recipientMob] = { wallet: 50000, subscription: null };
            db.users[recipientMob].wallet += amt;

            tkt.teamPicked = team;
            tkt.sattaAmount = amt;
            saveDB();
            updateHeader();
            renderActiveTickets();
            alert("Satta successfully place ho gaya!");
        }

        function settleSatta(tkt, match, isWinner) {
            if (tkt.status !== 'Active') return;
            let user = db.users[tkt.mobile];
            let recipientMob = match.creator || db.settings.adminNumber;

            if (isWinner) {
                let doubleAmt = tkt.sattaAmount * 2;
                if (db.users[recipientMob]) db.users[recipientMob].wallet -= doubleAmt;
                user.wallet += doubleAmt;
            }
            tkt.status = 'Settled';
            saveDB();
        }

        function deleteMatch(matchId) {
            if (confirm("Delete karna chahte hain?")) {
                db.matches = db.matches.filter(m => m.id !== matchId);
                saveDB();
                renderMatches();
            }
        }

        function switchTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));

            if (tabName === 'international') {
                document.getElementById('internationalTabContent').classList.remove('hidden');
                event.target.classList.add('active');
            } else if (tabName === 'apna') {
                document.getElementById('apnaTabContent').classList.remove('hidden');
                event.target.classList.add('active');
            } else if (tabName === 'activeTickets') {
                document.getElementById('activeTicketsTabContent').classList.remove('hidden');
                event.target.classList.add('active');
            }
        }
    </script>
</body>
</html>
