donationalerts_full/
├── backend/
│   ├── main.py
│   └── Dockerfile
├── frontend/
│   ├── src/
│   └── Dockerfile
└── docker-compose.yml
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Donatello Ultra | Криптодонаты + Виджеты + NFT</title>
    <style>
        :root {
            --primary: #6c5ce7;
            --primary-dark: #5649c0;
            --secondary: #00cec9;
            --dark: #2d3436;
            --light: #f5f6fa;
            --success: #00b894;
            --warning: #fdcb6e;
            --error: #d63031;
            --nft: #ff7675;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
        }
        
        body {
            background-color: var(--dark);
            color: var(--light);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            background-image: 
                radial-gradient(circle at 25% 25%, rgba(108, 92, 231, 0.15) 0%, transparent 50%),
                radial-gradient(circle at 75% 75%, rgba(0, 206, 201, 0.15) 0%, transparent 50%);
        }
        
        /* Header */
        header {
            padding: 1.5rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-size: 1.5rem;
            font-weight: 700;
            color: white;
            text-decoration: none;
        }
        
        .logo-icon {
            width: 32px;
            height: 32px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
        }
        
        nav {
            display: flex;
            gap: 1.5rem;
        }
        
        nav a {
            color: rgba(255, 255, 255, 0.7);
            text-decoration: none;
            transition: color 0.2s;
            font-weight: 500;
        }
        
        nav a:hover {
            color: white;
        }
        
        .theme-toggle {
            background: none;
            border: none;
            color: rgba(255, 255, 255, 0.7);
            cursor: pointer;
            font-size: 1.2rem;
        }
        
        /* Main Content */
        main {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 2rem;
        }
        
        h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            background: linear-gradient(to right, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            line-height: 1.2;
            text-align: center;
        }
        
        .subtitle {
            font-size: 1.2rem;
            color: rgba(255, 255, 255, 0.7);
            max-width: 600px;
            margin-bottom: 2.5rem;
            line-height: 1.6;
            text-align: center;
        }
        
        /* Tabs */
        .tabs-container {
            width: 100%;
            max-width: 1200px;
            margin-bottom: 2rem;
        }
        
        .tabs {
            display: flex;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            padding: 4px;
            margin-bottom: 1.5rem;
        }
        
        .tab {
            flex: 1;
            padding: 0.75rem;
            text-align: center;
            cursor: pointer;
            border-radius: 8px;
            font-weight: 500;
            transition: all 0.2s;
        }
        
        .tab.active {
            background: var(--primary);
            color: white;
        }
        
        /* Donate Section */
        .donate-container {
            width: 100%;
            max-width: 500px;
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 16px;
            padding: 2rem;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            margin-bottom: 2rem;
        }
        
        .donate-container:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.3);
        }
        
        .crypto-selector {
            margin-bottom: 1.5rem;
        }
        
        select {
            width: 100%;
            padding: 1rem;
            border-radius: 12px;
            border: none;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 1rem;
            cursor: pointer;
            appearance: none;
            background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='white'%3e%3cpath d='M7 10l5 5 5-5z'/%3e%3c/svg%3e");
            background-repeat: no-repeat;
            background-position: right 1rem center;
            background-size: 1rem;
        }
        
        select:focus {
            outline: none;
            box-shadow: 0 0 0 2px var(--primary);
        }
        
        .amount-input {
            margin-bottom: 1.5rem;
        }
        
        .amount-input label {
            display: block;
            text-align: left;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        
        .input-group {
            display: flex;
            border-radius: 12px;
            overflow: hidden;
            background: rgba(255, 255, 255, 0.1);
        }
        
        .input-group input {
            flex: 1;
            padding: 1rem;
            border: none;
            background: transparent;
            color: white;
            font-size: 1rem;
        }
        
        .input-group input:focus {
            outline: none;
        }
        
        .input-group select {
            width: auto;
            border-left: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 0;
            background-position: right 0.5rem center;
        }
        
        .qr-container {
            margin: 1.5rem 0;
            padding: 1rem;
            background: white;
            border-radius: 12px;
            display: inline-block;
        }
        
        .qr-code {
            width: 180px;
            height: 180px;
        }
        
        .address-container {
            margin-bottom: 1.5rem;
        }
        
        .address {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: rgba(255, 255, 255, 0.1);
            padding: 1rem;
            border-radius: 12px;
            font-family: monospace;
            font-size: 0.9rem;
            word-break: break-all;
        }
        
        .copy-btn {
            background: none;
            border: none;
            color: var(--secondary);
            cursor: pointer;
            margin-left: 0.5rem;
            transition: color 0.2s;
        }
        
        .copy-btn:hover {
            color: white;
        }
        
        .btn {
            width: 100%;
            padding: 1rem;
            border-radius: 12px;
            border: none;
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(108, 92, 231, 0.4);
        }
        
        .btn-secondary {
            background: rgba(255, 255, 255, 0.1);
            margin-top: 1rem;
        }
        
        .btn-secondary:hover {
            background: rgba(255, 255, 255, 0.2);
            box-shadow: none;
        }
        
        .network-info {
            margin-top: 1rem;
            font-size: 0.8rem;
            color: rgba(255, 255, 255, 0.5);
        }
        
        /* Widget Section */
        .widget-container {
            width: 100%;
            max-width: 800px;
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 16px;
            padding: 2rem;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.1);
            margin-bottom: 2rem;
            display: none;
        }
        
        .widget-preview {
            display: flex;
            gap: 2rem;
            margin-top: 1.5rem;
        }
        
        .widget-code {
            flex: 1;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 8px;
            padding: 1rem;
            font-family: monospace;
            overflow-x: auto;
        }
        
        .widget-example {
            flex: 1;
            background: white;
            border-radius: 8px;
            padding: 1rem;
            color: black;
            min-height: 150px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .widget-example .donation {
            margin: 0.5rem 0;
            padding: 0.5rem 1rem;
            background: rgba(108, 92, 231, 0.1);
            border-radius: 4px;
            width: 100%;
            animation: fadeIn 0.5s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* NFT Section */
        .nft-container {
            width: 100%;
            max-width: 800px;
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 16px;
            padding: 2rem;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.1);
            margin-bottom: 2rem;
            display: none;
        }
        
        .nft-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 1.5rem;
            margin-top: 1.5rem;
        }
        
        .nft-card {
            background: rgba(255, 118, 117, 0.1);
            border-radius: 12px;
            padding: 1rem;
            text-align: center;
            border: 1px solid rgba(255, 118, 117, 0.3);
            transition: transform 0.3s;
        }
        
        .nft-card:hover {
            transform: translateY(-5px);
        }
        
        .nft-image {
            width: 100%;
            aspect-ratio: 1;
            background: linear-gradient(45deg, var(--nft), #fdcb6e);
            border-radius: 8px;
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 2rem;
        }
        
        .nft-name {
            font-weight: 600;
            margin-bottom: 0.25rem;
        }
        
        .nft-price {
            font-size: 0.8rem;
            color: var(--warning);
        }
        
        /* Features */
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            margin-top: 3rem;
            width: 100%;
            max-width: 1200px;
        }
        
        .feature-card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 16px;
            padding: 1.5rem;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: transform 0.3s;
        }
        
        .feature-card:hover {
            transform: translateY(-5px);
        }
        
        .feature-icon {
            font-size: 2rem;
            margin-bottom: 1rem;
            color: var(--secondary);
        }
        
        .feature-title {
            font-size: 1.2rem;
            margin-bottom: 0.5rem;
            font-weight: 600;
        }
        
        .feature-desc {
            color: rgba(255, 255, 255, 0.7);
            font-size: 0.9rem;
            line-height: 1.6;
        }
        
        /* Footer */
        footer {
            padding: 2rem;
            text-align: center;
            color: rgba(255, 255, 255, 0.5);
            font-size: 0.9rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        /* Toast */
        .toast {
            position: fixed;
            bottom: 2rem;
            left: 50%;
            transform: translateX(-50%);
            background: var(--success);
            color: white;
            padding: 0.75rem 1.5rem;
            border-radius: 8px;
            font-weight: 500;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
            opacity: 0;
            transition: opacity 0.3s;
            z-index: 1000;
        }
        
        .toast.show {
            opacity: 1;
        }
        
        /* Light Theme */
        body.light {
            background-color: var(--light);
            color: var(--dark);
            background-image: 
                radial-gradient(circle at 25% 25%, rgba(108, 92, 231, 0.05) 0%, transparent 50%),
                radial-gradient(circle at 75% 75%, rgba(0, 206, 201, 0.05) 0%, transparent 50%);
        }
        
        body.light .donate-container,
        body.light .widget-container,
        body.light .nft-container,
        body.light .feature-card {
            background: rgba(255, 255, 255, 0.8);
            border: 1px solid rgba(0, 0, 0, 0.1);
        }
        
        body.light nav a,
        body.light .subtitle,
        body.light .feature-desc,
        body.light .network-info,
        body.light footer {
            color: rgba(0, 0, 0, 0.7);
        }
        
        body.light .address,
        body.light select,
        body.light .input-group,
        body.light .input-group input,
        body.light .tab:not(.active),
        body.light .widget-code {
            background: rgba(0, 0, 0, 0.05);
            color: var(--dark);
        }
        
        body.light .tab.active {
            color: white;
        }
        
        body.light .btn-secondary {
            background: rgba(0, 0, 0, 0.05);
            color: var(--dark);
        }
        
        body.light .btn-secondary:hover {
            background: rgba(0, 0, 0, 0.1);
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            h1 {
                font-size: 2rem;
            }
            
            .subtitle {
                font-size: 1rem;
            }
            
            .donate-container,
            .widget-container,
            .nft-container {
                padding: 1.5rem;
            }
            
            .widget-preview {
                flex-direction: column;
            }
            
            .features {
                grid-template-columns: 1fr;
            }
            
            nav {
                display: none;
            }
        }
    </style>
</head>
<body>
    <header>
        <a href="#" class="logo">
            <div class="logo-icon">DU</div>
            Donatello Ultra
        </a>
        <nav>
            <a href="#" class="nav-link" data-tab="donate">Донат</a>
            <a href="#" class="nav-link" data-tab="widget">Виджет</a>
            <a href="#" class="nav-link" data-tab="nft">NFT Бонусы</a>
        </nav>
        <button class="theme-toggle" id="themeToggle">🌓</button>
    </header>
    
    <main>
        <h1>Продвинутая система криптодонатов</h1>
        <p class="subtitle">Поддержите проект и получайте эксклюзивные NFT бонусы. Интегрируйте виджеты для стримов и сайтов.</p>
        
        <div class="tabs-container">
            <div class="tabs">
                <div class="tab active" data-tab="donate">Донат</div>
                <div class="tab" data-tab="widget">Виджет для стримов</div>
                <div class="tab" data-tab="nft">NFT Бонусы</div>
            </div>
        </div>
        
        <!-- Donate Section -->
        <div class="donate-container" id="donateSection">
            <div class="crypto-selector">
                <select id="cryptoSelect">
                    <option value="usdt-trc20">USDT (TRC20)</option>
                    <option value="usdt-erc20">USDT (ERC20)</option>
                    <option value="btc">Bitcoin (BTC)</option>
                    <option value="eth">Ethereum (ETH)</option>
                    <option value="ton">Toncoin (TON)</option>
                    <option value="sol">Solana (SOL)</option>
                </select>
            </div>
            
            <div class="amount-input">
                <label for="amount">Сумма доната</label>
                <div class="input-group">
                    <input type="number" id="amount" placeholder="10">
                    <select id="currency">
                        <option value="USD">USD</option>
                        <option value="EUR">EUR</option>
                        <option value="RUB">RUB</option>
                        <option value="BTC">BTC</option>
                        <option value="ETH">ETH</option>
                    </select>
                </div>
            </div>
            
            <button class="btn" id="generateBtn">Сгенерировать QR-код</button>
            
            <div id="qrSection" style="display: none;">
                <div class="qr-container">
                    <img src="https://api.qrserver.com/v1/create-qr-code/?size=180x180&data=donatello-ultra" class="qr-code" id="qrCode" alt="QR Code">
                </div>
                
                <div class="address-container">
                    <p style="margin-bottom: 0.5rem;">Адрес кошелька:</p>
                    <div class="address">
                        <span id="walletAddress">TK1234567890abcdefghijk</span>
                        <button class="copy-btn" id="copyBtn">Копировать</button>
                    </div>
                </div>
                
                <p class="network-info">Сеть: <span id="networkInfo">TRC20</span></p>
                
                <button class="btn btn-secondary" id="saveQrBtn">Сохранить QR-код</button>
            </div>
        </div>
        
        <!-- Widget Section -->
        <div class="widget-container" id="widgetSection">
            <h2 style="margin-bottom: 1rem;">Виджет для стримов</h2>
            <p style="margin-bottom: 1.5rem; color: rgba(255, 255, 255, 0.7);">Интегрируйте донаты прямо в ваш стрим. Последние донаты будут отображаться в реальном времени.</p>
            
            <div class="widget-preview">
                <div class="widget-code">
                    <pre>&lt;script src="https://donatello.ultra/widget.js"&gt;&lt;/script&gt;
&lt;div class="donatello-widget" 
  data-channel="YOUR_CHANNEL_ID"
  data-theme="dark"
  data-animation="fade"&gt;
&lt;/div&gt;</pre>
                </div>
                <div class="widget-example" id="widgetExample">
                    <h3>Последние донаты</h3>
                    <div class="donation">Аноним: 10 USDT</div>
                    <div class="donation">Иван: 0.005 BTC</div>
                    <div class="donation">Мария: 50 TON</div>
                </div>
            </div>
            
            <button class="btn" style="margin-top: 1.5rem;" id="copyWidgetBtn">Копировать код виджета</button>
        </div>
        
        <!-- NFT Section -->
        <div class="nft-container" id="nftSection">
            <h2 style="margin-bottom: 1rem;">NFT Бонусы за донаты</h2>
            <p style="margin-bottom: 1.5rem; color: rgba(255, 255, 255, 0.7);">Получайте эксклюзивные NFT за ваши донаты. Коллекционируйте и продавайте их на маркетплейсах.</p>
            
            <div class="nft-grid">
                <div class="nft-card">
                    <div class="nft-image">🎨</div>
                    <div class="nft-name">Supporter</div>
                    <div class="nft-price">От 10 USDT</div>
                </div>
                <div class="nft-card">
                    <div class="nft-image">🏆</div>
                    <div class="nft-name">Champion</div>
                    <div class="nft-price">От 50 USDT</div>
                </div>
                <div class="nft-card">
                    <div class="nft-image">👑</div>
                    <div class="nft-name">VIP</div>
                    <div class="nft-price">От 100 USDT</div>
                </div>
                <div class="nft-card">
                    <div class="nft-image">💎</div>
                    <div class="nft-name">Diamond</div>
                    <div class="nft-price">От 500 USDT</div>
                </div>
            </div>
            
            <button class="btn" style="margin-top: 1.5rem;" id="connectWalletBtn">Подключить кошелёк</button>
        </div>
        
        <!-- Features -->
        <div class="features">
            <div class="feature-card">
                <div class="feature-icon">⚡</div>
                <h3 class="feature-title">Реальные платежи</h3>
                <p class="feature-desc">Интеграция с блокчейнами Tron, Ethereum, Binance Smart Chain и другими</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">📺</div>
                <h3 class="feature-title">Виджеты для стримов</h3>
                <p class="feature-desc">Поддержка Twitch, YouTube и других платформ</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">🖼️</div>
                <h3 class="feature-title">Эксклюзивные NFT</h3>
                <p class="feature-desc">Уникальные цифровые активы за ваши донаты</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">🔌</div>
                <h3 class="feature-title">API для разработчиков</h3>
                <p class="feature-desc">Легкая интеграция с вашими проектами</p>
            </div>
        </div>
    </main>
    
    <footer>
        <p>© 2023 Donatello Ultra. Все права защищены.</p>
    </footer>
    
    <div class="toast" id="toast">Адрес скопирован!</div>
    
    <script>
        // Theme Toggle
        const themeToggle = document.getElementById('themeToggle');
        const body = document.body;
        
        themeToggle.addEventListener('click', () => {
            body.classList.toggle('light');
            localStorage.setItem('theme', body.classList.contains('light') ? 'light' : 'dark');
        });
        
        if (localStorage.getItem('theme') === 'light') {
            body.classList.add('light');
        }
        
        // Tab Switching
        const tabs = document.querySelectorAll('.tab');
        const navLinks = document.querySelectorAll('.nav-link');
        const sections = {
            donate: document.getElementById('donateSection'),
            widget: document.getElementById('widgetSection'),
            nft: document.getElementById('nftSection')
        };
        
        function switchTab(tabName) {
            // Hide all sections
            Object.values(sections).forEach(section => {
                section.style.display = 'none';
            });
            
            // Show selected section
            sections[tabName].style.display = 'block';
            
            // Update tab states
            tabs.forEach(tab => {
                tab.classList.toggle('active', tab.dataset.tab === tabName);
            });
            
            navLinks.forEach(link => {
                link.classList.toggle('active', link.dataset.tab === tabName);
            });
        }
        
        tabs.forEach(tab => {
            tab.addEventListener('click', () => {
                switchTab(tab.dataset.tab);
            });
        });
        
        navLinks.forEach(link => {
            link.addEventListener('click', (e) => {
                e.preventDefault();
                switchTab(link.dataset.tab);
            });
        });
        
        // Initialize first tab
        switchTab('donate');
        
        // Donate Section Functionality
        const generateBtn = document.getElementById('generateBtn');
        const qrSection = document.getElementById('qrSection');
        const qrCode = document.getElementById('qrCode');
        const walletAddress = document.getElementById('walletAddress');
        const networkInfo = document.getElementById('networkInfo');
        const cryptoSelect = document.getElementById('cryptoSelect');
        const copyBtn = document.getElementById('copyBtn');
        const toast = document.getElementById('toast');
        const saveQrBtn = document.getElementById('saveQrBtn');
        
        generateBtn.addEventListener('click', () => {
            const crypto = cryptoSelect.value;
            let address = '';
            let network = '';
            
            switch(crypto) {
                case 'usdt-trc20':
                    address = 'TJx...3a4b';
                    network = 'TRC20';
                    break;
                case 'usdt-erc20':
                    address = '0x9a...7f8e';
                    network = 'ERC20';
                    break;
                case 'btc':
                    address = 'bc1q...zxyw';
                    network = 'Bitcoin';
                    break;
                case 'eth':
                    address = '0x4d...9e0f';
                    network = 'Ethereum';
                    break;
                case 'ton':
                    address = 'EQD...v2k';
                    network = 'TON';
                    break;
                case 'sol':
                    address = '7xZ...mNq';
                    network = 'Solana';
                    break;
            }
            
            walletAddress.textContent = address;
            networkInfo.textContent = network;
            
            const amount = document.getElementById('amount').value || '0';
            const currency = document.getElementById('currency').value;
            
            // Generate QR code with payment data
            const qrData = `crypto:${address}?amount=${amount}&currency=${currency}&network=${network}`;
            qrCode.src = `https://api.qrserver.com/v1/create-qr-code/?size=180x180&data=${encodeURIComponent(qrData)}`;
            
            qrSection.style.display = 'block';
        });
        
        copyBtn.addEventListener('click', () => {
            navigator.clipboard.writeText(walletAddress.textContent)
                .then(() => {
                    toast.textContent = 'Адрес скопирован!';
                    toast.classList.add('show');
                    setTimeout(() => toast.classList.remove('show'), 3000);
                });
        });
        
        saveQrBtn.addEventListener('click', () => {
            const link = document.createElement('a');
            link.href = qrCode.src;
            link.download = 'donatello-qr.png';
            link.click();
        });
        
        cryptoSelect.addEventListener('change', () => {
            const currencySelect = document.getElementById('currency');
            const crypto = cryptoSelect.value;
            
            if (crypto === 'btc') {
                currencySelect.value = 'BTC';
            } else if (crypto === 'eth') {
                currencySelect.value = 'ETH';
            } else {
                currencySelect.value = 'USD';
            }
        });
        
        // Widget Section Functionality
        const copyWidgetBtn = document.getElementById('copyWidgetBtn');
        
        copyWidgetBtn.addEventListener('click', () => {
            const widgetCode = document.querySelector('.widget-code pre').textContent;
            navigator.clipboard.writeText(widgetCode)
                .then(() => {
                    toast.textContent = 'Код виджета скопирован!';
                    toast.classList.add('show');
                    setTimeout(() => toast.classList.remove('show'), 3000);
                });
        });
        
        // Simulate new donations in widget example
        const widgetExample = document.getElementById('widgetExample');
        const donations = [
            { name: 'Алексей', amount: '0.1 ETH', comment: 'Отличный контент!' },
            { name: 'Катя', amount: '25 USDT', comment: '❤️' },
            { name: 'Максим', amount: '100 TON', comment: 'Продолжайте в том же духе' },
            { name: 'Олег', amount: '0.005 BTC', comment: '' }
        ];
        
        setInterval(() => {
            const randomDonation = donations[Math.floor(Math.random() * donations.length)];
            const donationElement = document.createElement('div');
            donationElement.className = 'donation';
            donationElement.textContent = `${randomDonation.name}: ${randomDonation.amount}`;
            if (randomDonation.comment) {
                donationElement.textContent += ` (${randomDonation.comment})`;
            }
            
            widgetExample.insertBefore(donationElement, widgetExample.firstChild.nextSibling);
            
            if (widgetExample.children.length > 5) {
                widgetExample.removeChild(widgetExample.lastChild);
            }
        }, 8000);
        
        // NFT Section Functionality
        const connectWalletBtn = document.getElementById('connectWalletBtn');
        
        connectWalletBtn.addEventListener('click', () => {
            toast.textContent = 'Функция подключения кошелька в разработке';
            toast.classList.add('show');
            setTimeout(() => toast.classList.remove('show'), 3000);
        });
    </script>
</body>
</html>
