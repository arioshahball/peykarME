
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PEYKAR | Cyberpunk OS</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <style>
        :root {
            --neon-blue: #00f3ff;
            --neon-pink: #ff00ff;
            --neon-yellow: #f3ff00;
            --bg-dark: #05050a;
            --card-bg: #10101a;
        }

        body {
            background: var(--bg-dark);
            color: #e0e0e0;
            font-family: 'Tahoma', sans-serif;
            margin: 0;
            overflow-x: hidden;
        }

        /* Cyberpunk Background Effect */
        body::before {
            content: "";
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(rgba(0, 243, 255, 0.05) 1px, transparent 1px),
                        linear-gradient(90deg, rgba(0, 243, 255, 0.05) 1px, transparent 1px);
            background-size: 30px 30px;
            z-index: -1;
        }

        .section {
            display: none;
            padding: 20px;
            max-width: 500px;
            margin: 40px auto;
            background: var(--card-bg);
            border: 2px solid var(--neon-blue);
            box-shadow: 0 0 15px var(--neon-blue);
            border-radius: 5px;
        }

        .active { display: block; animation: flicker 0.3s ease-in; }

        @keyframes flicker {
            0% { opacity: 0; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        h1, h2 {
            color: var(--neon-pink);
            text-shadow: 0 0 10px var(--neon-pink);
            text-align: center;
            text-transform: uppercase;
            letter-spacing: 3px;
        }

        input, select, button {
            background: #000;
            border: 1px solid var(--neon-blue);
            color: var(--neon-blue);
            padding: 12px;
            margin: 10px 0;
            width: 100%;
            box-sizing: border-box;
            font-size: 14px;
        }

        input:focus { outline: none; border-color: var(--neon-pink); box-shadow: 0 0 10px var(--neon-pink); }

        button {
            cursor: pointer;
            font-weight: bold;
            text-transform: uppercase;
            transition: 0.3s;
        }

        button:hover {
            background: var(--neon-blue);
            color: #000;
            box-shadow: 0 0 20px var(--neon-blue);
        }

        .btn-pink { border-color: var(--neon-pink); color: var(--neon-pink); }
        .btn-pink:hover { background: var(--neon-pink); color: #000; }

        #map { height: 250px; border: 1px solid var(--neon-blue); margin: 15px 0; }
        
        .order-card {
            border: 1px solid var(--neon-yellow);
            padding: 10px;
            margin: 10px 0;
            background: rgba(243, 255, 0, 0.05);
        }

        .admin-item {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            border-bottom: 1px solid #333;
        }
    </style>
</head>
<body>

<!-- بخش ورود (Login) -->
<div id="auth-section" class="section active">
    <h1>PEYKAR_OS</h1>
    <p style="text-align:center; color:var(--neon-blue)">System Login Required</p>
    <input type="text" id="login-phone" placeholder="شماره موبایل">
    <input type="password" id="login-pass" placeholder="رمز عبور">
    <button onclick="handleLogin()">اجرای ورود (Login)</button>
    <button class="btn-pink" onclick="showSection('register-section')">ایجاد حساب جدید</button>
</div>

<!-- بخش ثبت نام (Register) -->
<div id="register-section" class="section">
    <h2>ثبت نام در شبکه</h2>
    <input type="text" id="reg-name" placeholder="نام کاربری">
    <input type="text" id="reg-phone" placeholder="شماره موبایل">
    <input type="password" id="reg-pass" placeholder="رمز عبور">
    <select id="reg-role">
        <option value="customer">مشتری (Customer)</option>
        <option value="piker">پیک (Piker)</option>
    </select>
    <button onclick="startOTP()">دریافت کد امنیتی</button>
    <input type="text" id="otp-input" placeholder="کد ۴ رقمی" style="display:none">
    <button id="verify-btn" onclick="verifyRegister()" style="display:none" class="btn-pink">تایید و ثبت نهایی</button>
</div>

<!-- پنل مشتری (Customer Panel) -->
<div id="customer-panel" class="section">
    <h2 id="cust-welcome">مشتری</h2>
    <div id="map"></div>
    <button onclick="createOrder()">ثبت سفارش جدید</button>
    <div id="customer-orders"></div>
    <button class="btn-pink" onclick="logout()">قطع اتصال (Logout)</button>
</div>

<!-- پنل پیک (Piker Panel) -->
<div id="piker-panel" class="section">
    <h2 id="piker-welcome">پیک</h2>
    <div id="piker-orders-list"></div>
    <button class="btn-pink" onclick="logout()">قطع اتصال (Logout)</button>
</div>

<!-- پنل ادمین/طلایی (Admin Panel) -->
<div id="admin-panel" class="section">
    <h2 style="color:var(--neon-yellow)">ADMIN_COMMAND_CENTER</h2>
    <div id="admin-stats"></div>
    <h3>لیست سیاه (Banned Users)</h3>
    <div id="blacklist-area"></div>
    <button class="btn-pink" onclick="logout()">خروج از سیستم مدیریت</button>
</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script>
    // --- دیتابیس و متغیرهای اصلی ---
    let users = JSON.parse(localStorage.getItem('peykar_users') || '[]');
    let orders = JSON.parse(localStorage.getItem('peykar_orders') || '[]');
    let banned = JSON.parse(localStorage.getItem('peykar_banned') || '[]');
    let currentUser = JSON.parse(localStorage.getItem('currentUser')) || null;
    let map;

    // --- سیستم مدیریت نمایش (SPA) ---
    function showSection(id) {
        document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
        const target = document.getElementById(id);
        if(target) target.classList.add('active');
    }

    // --- منطق احراز هویت ---
    function startOTP() {
        const phone = document.getElementById('reg-phone').value;
        const pass = document.getElementById('reg-pass').value;
        const name = document.getElementById('reg-name').value;

        if(!phone || !pass || !name) return alert("همه فیلدها پر شود!");
        if(users.find(u => u.phone === phone)) return alert("این شماره قبلاً ثبت شده!");

        window.tempOTP = Math.floor(1000 + Math.random() * 9000);
        alert("کد امنیتی شما در شبکه: " + window.tempOTP);
        
        document.getElementById('otp-input').style.display = 'block';
        document.getElementById('verify-btn').style.display = 'block';
    }

    function verifyRegister() {
        const code = document.getElementById('otp-input').value;
        if(code != window.tempOTP) return alert("کد اشتباه است!");

        const newUser = {
            name: document.getElementById('reg-name').value,
            phone: document.getElementById('reg-phone').value,
            pass: document.getElementById('reg-pass').value,
            role: document.getElementById('reg-role').value
        };

        users.push(newUser);
        localStorage.setItem('peykar_users', JSON.stringify(users));
        alert("ثبت نام با موفقیت انجام شد.");
        showSection('auth-section');
    }

    function handleLogin() {
        const phone = document.getElementById('login-phone').value;
        const pass = document.getElementById('login-pass').value;

        // چک کردن لیست سیاه
        if(banned.includes(phone)) {
            alert("هشدار: حساب شما مسدود (BANNED) شده است!");
            return;
        }

        // بررسی ادمین (حساب طلایی)
        if(phone === '09371130903') {
            currentUser = { name: 'Admin', phone: '09371130903', role: 'admin' };
            completeLogin();
            return;
        }

        // بررسی کاربران عادی
        const user = users.find(u => u.phone === phone && u.pass === pass);
        if(user) {
            currentUser = user;
            completeLogin();
        } else {
            alert("خطا در احراز هویت! شماره یا رمز اشتباه است.");
        }
    }

    function completeLogin() {
        localStorage.setItem('currentUser', JSON.stringify(currentUser));
        loadDashboard();
    }

    function loadDashboard() {
        if(!currentUser) return;

        if(currentUser.role === 'admin') {
            showSection('admin-panel');
            renderAdmin();
        } else if(currentUser.role === 'customer') {
            showSection('customer-panel');
            document.getElementById('cust-welcome').innerText = `خوش آمدید ${currentUser.name}`;
            initMap();
            renderCustomerOrders();
        } else if(currentUser.role === 'piker') {
            showSection('piker-panel');
            document.getElementById('piker-welcome').innerText = `پیک: ${currentUser.name}`;
            renderPikerOrders();
        }
    }

    // --- منطق مشتری (Customer) ---
    function initMap() {
        if(!map) {
            map = L.map('map').setView([35.6892, 51.3890], 13);
            L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);
        }
    }

    function createOrder() {
        const newOrder = {
            id: Date.now(),
            customerPhone: currentUser.phone,
            customerName: currentUser.name,
            status: 'pending', // pending, active, delivered
            lat: 35.6892,
            lng: 51.3890
        };
        orders.push(newOrder);
        localStorage.setItem('peykar_orders', JSON.stringify(orders));
        alert("سفارش با موفقیت در شبکه ثبت شد!");
        renderCustomerOrders();
    }

    function renderCustomerOrders() {
        const container = document.getElementById('customer-orders');
        const myOrders = orders.filter(o => o.customerPhone === currentUser.phone);
        container.innerHTML = "<h3>سفارشات من:</h3>";
        myOrders.forEach(o => {
            container.innerHTML += `<div class="order-card">ID: ${o.id} | وضعیت: ${o.status}</div>`;
        });
    }

    // --- منطق پیک (Piker) ---
    function renderPikerOrders() {
        const container = document.getElementById('piker-orders-list');
        const pendingOrders = orders.filter(o => o.status === 'pending');
        container.innerHTML = "<h3>سفارشات در دسترس:</h3>";
        if(pendingOrders.length === 0) container.innerHTML += "<p>سفارش جدیدی موجود نیست.</p>";
        
        pendingOrders.forEach(o => {
            container.innerHTML += `
                <div class="order-card">
                    مشتری: ${o.customerName}<br>
                    <button onclick="acceptOrder(${o.id})">پذیرش سفارش</button>
                </div>`;
        });
    }

    function acceptOrder(orderId) {
        const orderIndex = orders.findIndex(o => o.id === orderId);
        orders[orderIndex].status = 'active';
        orders[orderIndex].pikerPhone = currentUser.phone;
        localStorage.setItem('peykar_orders', JSON.stringify(orders));
        alert("سفارش پذیرفته شد!");
        renderPikerOrders();
    }

    // --- منطق ادمین (Admin/Golden Account) ---
    function renderAdmin() {
        const blacklistDiv = document.getElementById('blacklist-area');
        const statsDiv = document.getElementById('admin-stats');
        
        statsDiv.innerHTML = `کاربران: ${users.length} | سفارشات: ${orders.length}`;
        
        blacklistDiv.innerHTML = "";
        banned.forEach((phone, index) => {
            blacklistDiv.innerHTML += `
                <div class="admin-item">
                    <span>${phone}</span>
                    <button style="width:auto; padding:2px 10px" onclick="unban('${phone}')">بازگرداندن</button>
                </div>`;
        });
    }

    // (در دنیای واقعی اینجا تابع Ban هم می‌گذاریم، فعلاً فقط Unban)
    function unban(phone) {
        banned = banned.filter(p => p !== phone);
        localStorage.setItem('peykar_banned', JSON.stringify(banned));
        renderAdmin();
    }

    // --- خروج ---
    function logout() {
        localStorage.removeItem('currentUser');
        location.reload();
    }

    // لود اولیه
    if(currentUser) {
        loadDashboard();
    }
</script>

</body>
</html>
