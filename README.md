<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Aice 冰柜巡检系统</title>
    <!-- Google API 库 -->
    <script src="https://apis.google.com/js/api.js"></script>
    <!-- Google Identity Services 登录库 -->
    <script src="https://accounts.google.com/gsi/client" async defer></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }
        
        body {
            background: #f5f5f5;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 16px;
        }
        
        :root {
            --aice-red: #e31e24;
            --aice-red-light: #ff6b6b;
            --aice-red-dark: #c41a1f;
            --aice-red-bg: rgba(227, 30, 36, 0.1);
            --bg: #f8f9fa;
            --card: #ffffff;
            --text: #1e293b;
            --text-light: #64748b;
            --border: #e2e8f0;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --shadow: 0 4px 12px rgba(0,0,0,0.05);
            --shadow-lg: 0 10px 25px rgba(0,0,0,0.1);
        }
        
        .login-container {
            max-width: 400px;
            width: 100%;
            margin: 0 auto;
            background: white;
            border-radius: 32px;
            padding: 32px 24px;
            box-shadow: 0 20px 60px rgba(227,30,36,0.15);
            border: 1px solid rgba(227,30,36,0.1);
            text-align: center;
        }
        
        .logo {
            text-align: center;
            margin-bottom: 32px;
        }

        .logo h1 {
            color: var(--aice-red);
            font-size: 64px;
            font-weight: bold;
            font-style: italic;
            margin-bottom: 5px;
        }

        .brand-line {
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--aice-red), transparent);
            width: 80px;
            margin: 16px auto;
        }

        .tagline {
            font-size: 20px;
            font-weight: 500;
            color: #333;
            white-space: nowrap;
            margin: 20px 0 28px;
        }

        .tagline span {
            color: var(--aice-red);
            font-weight: bold;
            font-style: italic;
        }
        
        .g_id_signin {
            margin: 0 auto;
            display: flex;
            justify-content: center;
        }
        
        .main-container {
            max-width: 500px;
            width: 100%;
            margin: 0 auto;
            background: white;
            min-height: 100vh;
            position: relative;
            box-shadow: var(--shadow);
        }
        
        .header {
            background: var(--aice-red);
            padding: 16px 20px;
            color: white;
            position: sticky;
            top: 0;
            z-index: 10;
        }
        
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 8px;
        }
        
        .lang-switch {
            display: flex;
            gap: 4px;
            background: rgba(255,255,255,0.2);
            padding: 4px;
            border-radius: 40px;
        }
        
        .lang-btn {
            padding: 6px 16px;
            border-radius: 40px;
            font-size: 13px;
            cursor: pointer;
            color: white;
        }
        
        .lang-btn.active {
            background: white;
            color: var(--aice-red);
            font-weight: 600;
        }
        
        .user-info {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .user-name {
            font-size: 15px;
            font-weight: 500;
            background: rgba(255,255,255,0.2);
            padding: 6px 14px;
            border-radius: 40px;
        }
        
        .logout-btn {
            background: rgba(255,255,255,0.2);
            padding: 6px 14px;
            border-radius: 40px;
            font-size: 13px;
            cursor: pointer;
        }
        
        .date {
            font-size: 13px;
            opacity: 0.9;
            margin-top: 5px;
        }
        
        .brand-footer {
            text-align: center;
            padding: 16px;
            font-size: 12px;
            color: #999;
            border-top: 1px solid #eee;
            background: white;
            position: fixed;
            bottom: 0;
            width: 100%;
            max-width: 500px;
        }
        
        .brand-footer span {
            color: var(--aice-red);
            font-weight: 600;
        }
        
        .stats-card {
            background: white;
            margin: 15px;
            padding: 20px;
            border-radius: 24px;
            box-shadow: var(--shadow);
            border: 1px solid #f0f0f0;
        }
        
        .stats-title {
            font-size: 18px;
            font-weight: bold;
            color: #333;
            margin-bottom: 15px;
            border-left: 4px solid var(--aice-red);
            padding-left: 10px;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .stat-item {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 12px;
            text-align: center;
        }
        
        .stat-value {
            font-size: 32px;
            font-weight: bold;
            color: var(--aice-red);
            line-height: 1.2;
        }
        
        .stat-label {
            font-size: 13px;
            color: #666;
            margin-top: 4px;
        }
        
        .progress-bar {
            height: 8px;
            background: #e0e0e0;
            border-radius: 4px;
            overflow: hidden;
            margin: 8px 0;
        }
        
        .progress-fill {
            height: 100%;
            background: var(--aice-red);
            border-radius: 4px;
        }
        
        .freezer-id {
            font-weight: 600;
            color: var(--aice-red);
            background: rgba(227,30,36,0.05);
            padding: 4px 12px;
            border-radius: 30px;
        }
        
        .task-list {
            padding: 0 15px;
        }
        
        .task-item {
            background: white;
            border: 1px solid #f0f0f0;
            border-radius: 20px;
            padding: 15px;
            margin-bottom: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.02);
        }
        
        .task-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .shop-name {
            font-weight: 600;
            font-size: 15px;
        }
        
        .shop-details {
            color: #666;
            font-size: 13px;
            margin: 5px 0;
        }
        
        .task-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 10px;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .time {
            color: #999;
            font-size: 12px;
        }
        
        .photo-btn {
            background: var(--aice-red);
            color: white;
            border: none;
            padding: 8px 20px;
            border-radius: 30px;
            font-size: 13px;
            font-weight: 500;
            cursor: pointer;
        }
        
        .photo-btn.completed {
            background: #00a65a;
        }
        
        .photo-btn:disabled {
            background: #ccc;
            cursor: not-allowed;
        }
        
        .photo-preview-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin: 10px 0;
            max-height: 300px;
            overflow-y: auto;
            padding: 5px;
        }
        
        .photo-preview-item {
            position: relative;
            aspect-ratio: 1;
            border-radius: 8px;
            overflow: hidden;
            border: 2px solid #ddd;
        }
        
        .photo-preview-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .photo-preview-item .remove-btn {
            position: absolute;
            top: 2px;
            right: 2px;
            width: 20px;
            height: 20px;
            background: rgba(227,30,36,0.8);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            cursor: pointer;
        }
        
        .camera-btn {
            background: #333;
            color: white;
            border: none;
            padding: 12px;
            border-radius: 10px;
            width: 100%;
            font-size: 15px;
            cursor: pointer;
            margin: 10px 0;
        }
        
        .upload-btn {
            background: var(--aice-red);
            color: white;
            border: none;
            padding: 12px;
            border-radius: 10px;
            width: 100%;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }
        
        .remark-section {
            background: #fef5f5;
            border-radius: 16px;
            padding: 15px;
            margin: 15px 0;
            border: 1px solid rgba(227,30,36,0.2);
        }
        
        .remark-title {
            font-weight: bold;
            color: var(--aice-red);
            margin-bottom: 10px;
        }
        
        .remark-select {
            width: 100%;
            padding: 12px;
            border: 1px solid #ffcdd2;
            border-radius: 12px;
            font-size: 14px;
            margin-bottom: 10px;
        }
        
        .remark-input {
            width: 100%;
            padding: 12px;
            border: 1px solid #ffcdd2;
            border-radius: 12px;
            font-size: 14px;
            margin-top: 10px;
            font-family: inherit;
            line-height: 1.5;
            resize: vertical;
            min-height: 200px;
        }
        
        .sync-card {
            background: white;
            margin: 15px;
            padding: 20px;
            border-radius: 16px;
            border: 1px solid var(--aice-red);
            box-shadow: var(--shadow);
        }
        
        .sync-textarea {
            width: 100%;
            height: 100px;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 12px;
            margin: 10px 0;
            font-size: 14px;
        }
        
        .sync-btn {
            background: var(--aice-red);
            color: white;
            border: none;
            padding: 12px;
            border-radius: 30px;
            width: 100%;
            font-size: 16px;
            cursor: pointer;
        }
        
        .region-tasks {
            background: white;
            margin: 15px;
            padding: 20px;
            border-radius: 16px;
            border: 1px solid #f0f0f0;
        }
        
        .region-title {
            font-weight: bold;
            margin: 15px 0 10px;
            color: var(--aice-red);
        }
        
        .freezer-tag {
            display: inline-block;
            background: #f0f0f0;
            padding: 4px 12px;
            border-radius: 30px;
            margin: 0 5px 5px 0;
            font-size: 12px;
        }
        
        .nav-bar {
            display: flex;
            background: white;
            border-bottom: 1px solid #eee;
            position: sticky;
            top: 76px;
            z-index: 9;
            padding: 4px;
            overflow-x: auto;
            white-space: nowrap;
            gap: 2px;
        }
        
        .nav-item {
            flex: 1;
            text-align: center;
            padding: 12px 8px;
            color: #666;
            cursor: pointer;
            font-size: 14px;
            border-radius: 30px;
            min-width: fit-content;
            transition: all 0.2s;
        }
        
        .nav-item.active {
            color: var(--aice-red);
            background: rgba(227,30,36,0.05);
            font-weight: 600;
        }
        
        .content {
            padding: 16px;
            padding-bottom: 80px;
        }
        
        .hidden {
            display: none !important;
        }
        
        .call-btn {
            background: #10b981;
            color: white;
            border: none;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 12px;
            cursor: pointer;
        }
        
        .copy-btn {
            background: #3b82f6;
            color: white;
            border: none;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 12px;
            cursor: pointer;
        }
        
        .photo-thumb {
            width: 100%;
            max-height: 150px;
            object-fit: cover;
            border-radius: 12px;
            margin-top: 10px;
            cursor: pointer;
        }
        
        .fullscreen-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: black;
            z-index: 2000;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        
        .fullscreen-modal img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
        }
        
        #photoModal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            backdrop-filter: blur(4px);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 16px;
        }
        
        #photoModal > div {
            background: white;
            width: 100%;
            max-width: 450px;
            border-radius: 32px;
            padding: 24px;
            max-height: 90vh;
            overflow-y: auto;
            border: 2px solid var(--aice-red);
        }
        
        .modal-title {
            font-size: 22px;
            font-weight: bold;
            color: var(--aice-red);
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--aice-red);
        }
        
        .status-card {
            background: white;
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 16px;
            box-shadow: var(--shadow);
        }
        
        .status-header {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 16px;
        }
        
        .status-header-line {
            width: 4px;
            height: 24px;
            background: var(--aice-red);
            border-radius: 4px;
        }
        
        .total-card {
            background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
            border-radius: 20px;
            padding: 16px;
            margin-bottom: 20px;
        }
        
        .status-item {
            background: white;
            border-radius: 16px;
            padding: 16px;
            margin-bottom: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.02);
            border: 1px solid #f0f0f0;
        }
        
        .status-item-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .status-item-left {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .status-item-right {
            text-align: right;
        }
        
        .status-count {
            font-size: 18px;
            font-weight: 700;
        }
        
        .status-percent {
            font-size: 14px;
            color: #64748b;
            margin-left: 8px;
        }
        
        .progress-container {
            position: relative;
            height: 24px;
            background: #f1f5f9;
            border-radius: 12px;
            overflow: hidden;
        }
        
        .progress-fill-custom {
            height: 100%;
            border-radius: 12px;
            transition: width 0.3s ease;
        }
        
        .progress-text {
            position: absolute;
            top: 0;
            right: 8px;
            line-height: 24px;
            font-size: 12px;
            font-weight: 600;
            color: white;
            text-shadow: 0 1px 2px rgba(0,0,0,0.1);
        }
        
        .warning-card {
            background: linear-gradient(135deg, #fff1f0 0%, #fee2e2 100%);
            border-radius: 20px;
            padding: 20px;
        }
        
        .warning-header {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 16px;
        }
        
        .warning-item {
            display: flex;
            align-items: center;
            gap: 12px;
            background: rgba(255,255,255,0.5);
            padding: 10px;
            border-radius: 12px;
            margin-bottom: 8px;
        }
        
        .warning-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
        }
        
        .warning-text {
            flex: 1;
        }
        
        .warning-count {
            font-weight: 600;
        }
        
        @media (max-width: 380px) {
            .logo h1 { font-size: 52px; }
            .tagline { font-size: 18px; }
            .top-bar { flex-direction: column; align-items: flex-start; }
            .user-info { width: 100%; justify-content: space-between; }
            .stats-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
    <div id="app">
        <!-- 登录页 - 只有Google登录 -->
        <div id="loginPage" class="login-container">
            <div class="logo">
                <h1>Aice</h1>
                <div class="brand-line"></div>
                <div class="tagline">
                    HAVE AN <span>AICE</span> DAY
                </div>
            </div>
            
            <!-- Google登录按钮 -->
            <div id="g_id_onload"
                 data-client_id="373043108695-v2tnu077g4ptf6fvc9iu4kqb0cvvptpc.apps.googleusercontent.com"
                 data-context="signin"
                 data-ux_mode="popup"
                 data-callback="handleGoogleSignIn"
                 data-auto_prompt="false">
            </div>
            <div class="g_id_signin"
                 data-type="standard"
                 data-shape="rectangular"
                 data-theme="outline"
                 data-text="signin_with"
                 data-size="large"
                 data-logo_alignment="left">
            </div>
        </div>

        <!-- 主页面 -->
        <div id="mainPage" class="main-container hidden">
            <div class="header">
                <div class="top-bar">
                    <div class="lang-switch">
                        <span class="lang-btn active" onclick="switchLanguage('zh')" id="langZhBtn">中文</span>
                        <span class="lang-btn" onclick="switchLanguage('en')" id="langEnBtn">English</span>
                    </div>
                    <div class="user-info">
                        <span class="user-name" id="displayName"></span>
                        <span class="logout-btn" onclick="logout()" id="logoutBtn">退出</span>
                    </div>
                </div>
                <div class="date" id="currentDate"></div>
            </div>

            <div class="nav-bar" id="navBar"></div>
            <div class="content" id="content"></div>
            
            <div class="brand-footer">
                <span>Aice</span> • Karachi
            </div>
        </div>

        <!-- 拍照模态框（多张上传 + 10行备注） -->
        <div id="photoModal" class="hidden">
            <div>
                <div class="modal-title">照片上传 - <span id="modalFreezerId"></span></div>
                
                <!-- 第一步：选择照片 -->
                <div style="margin-bottom: 20px;">
                    <div style="font-weight: 600; margin-bottom: 10px;">
                        <span style="background: var(--aice-red); color: white; width: 26px; height: 26px; border-radius: 50%; display: inline-flex; align-items: center; justify-content: center; margin-right: 8px;">1</span>
                        <span id="step1Title">选择照片</span>
                    </div>
                    <div id="photo-preview-area" class="photo-preview-grid">
                        <div style="text-align:center; color:#999; padding:20px;">点击上方按钮选择照片</div>
                    </div>
                    <input type="file" id="photo-input" accept="image/*" multiple style="display: none;">
                    <button class="camera-btn" onclick="document.getElementById('photo-input').click()">选择照片（最多5张）</button>
                    <div style="font-size: 12px; color: #666; margin-top: 5px; text-align: right;">
                        <span id="photo-count-label">已选</span> <span id="photo-count">0</span>/5 <span id="photo-unit">张</span>
                    </div>
                </div>
                
                <!-- 第二步：备注（10行输入框） -->
                <div class="remark-section">
                    <div style="font-weight: 600; margin-bottom: 12px;">
                        <span style="background: var(--aice-red); color: white; width: 26px; height: 26px; border-radius: 50%; display: inline-flex; align-items: center; justify-content: center; margin-right: 8px;">2</span>
                        <span id="step2Title">备注</span>
                    </div>
                    
                    <select class="remark-select" id="remarkType">
                        <option value="normal">冰柜正常</option>
                        <option value="unused">冰柜未使用</option>
                        <option value="dirty_inside">冰柜内部脏了</option>
                        <option value="other_ad">外部有其他广告</option>
                        <option value="temperature">温度异常</option>
                        <option value="damaged">冰柜损坏</option>
                        <option value="other">其他问题</option>
                    </select>
                    
                    <textarea class="remark-input" id="remarkDetail" placeholder="详细说明（选填，最多200字）" maxlength="200" rows="10"></textarea>
                    <div style="text-align: right; font-size: 12px; margin-top: 6px;">
                        <span id="charCount">0</span>/200
                    </div>
                </div>
                
                <button class="upload-btn" onclick="uploadPhotos()" id="uploadBtn">确认上传</button>
                <button style="background: #999; color: white; border: none; padding: 12px; border-radius: 12px; width: 100%; margin-top: 10px;" onclick="closePhotoModal()" id="cancelBtn">取消</button>
            </div>
        </div>

        <!-- 图片全屏查看 -->
        <div id="fullscreenModal" class="fullscreen-modal hidden" onclick="closeFullscreen()">
            <img id="fullscreenImage" src="">
        </div>
    </div>

    <script>
        // ===== 配置 =====
        const CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vRw6l0RVWFFp1KX7cJbWn9lZDHBNNWBV9Im8QEXxjRBoTKTEe5eFIMxtP8Bb8Y3WmOXEu2RIU6kAEVt/pub?output=csv';
        const CLIENT_ID = '373043108695-v2tnu077g4ptf6fvc9iu4kqb0cvvptpc.apps.googleusercontent.com';
        const FOLDER_ID = '1svV1JTxJya7QJ0JVLgMC68BWsh58e6kJ';

        // ===== 全局变量 =====
        let freezers = [];
        let currentUser = null;
        let currentFreezer = null;
        let currentLang = localStorage.getItem('language') || 'zh';
        let photos = JSON.parse(localStorage.getItem('photos')) || [];
        let todayTasks = { '1': [], '2': [], '3': [] };
        let selectedPhotos = [];
        let googleAuth = null;

        // ===== 状态映射 =====
        const themeRed = '#e31e24';
        const themeRedLight = '#ff6b6b';
        const themeRedDark = '#c41a1f';

        const statusMap = {
            'active': { text: '✅ 已投放', color: themeRed },
            'repair': { text: '🔧 维修中', color: themeRedLight },
            'stock': { text: '📦 仓库', color: themeRedDark },
            'scrap': { text: '❌ 报废', color: '#6b7280' },
            'withdrawn': { text: '⬅️ 已撤回', color: themeRed },
            'office': { text: '🏢 直管', color: themeRedLight }
        };

        const sheetStatusMap = {
            '已投放': 'active',
            '维修中': 'repair',
            '仓库': 'stock',
            '报废': 'scrap',
            '已撤回': 'withdrawn',
            '直管': 'office'
        };

        // ===== 翻译 =====
        const translations = {
            zh: {
                usernameLabel: '编号', passwordLabel: '密码', rememberLabel: '记住登录状态',
                loginBtn: '登录', logoutBtn: '退出',
                step1Title: '选择照片', step2Title: '备注', openCameraBtn: '选择照片',
                uploadBtn: '确认上传', cancelBtn: '取消', cameraPreview: '点击上方按钮选择照片',
                photoModalTitle: '照片上传',
                photoCountLabel: '已选', photoUnit: '张',
                remarkNormal: '冰柜正常', remarkUnused: '冰柜未使用',
                remarkDirtyInside: '冰柜内部脏了', remarkOtherAd: '外部有其他广告',
                remarkTemperature: '温度异常', remarkDamaged: '冰柜损坏',
                remarkOther: '其他问题', remarkDetailPlaceholder: '详细说明（选填，最多200字）',
                todayTasks: '今日任务', myRecords: '我的记录', progress: '进度',
                waiting: '待拍照', completed: '已完成', photo: '上传',
                totalFreezers: '总冰柜', todayPhotos: '今日拍照',
                weekPhotos: '本周拍照', monthPhotos: '本月拍照',
                overdue: '超期未拍', warning: '即将超期',
                syncTasks: '同步任务', statusMgmt: '状态管理',
                regionStats: '区域统计', alerts: '预警',
                search: '搜索', sync: '解析并同步',
                overview: '总览', regions: '区域详情', salesmen: '业务员',
                totalFreezersLabel: '总冰柜',
                active: '已投放', repair: '维修中', stock: '仓库存放',
                scrap: '报废', withdrawn: '已撤回', officeManaged: '办公室直管',
                attentionNeeded: '需关注', allNormal: '一切正常',
                problemFreezers: '问题冰柜', allGood: '所有冰柜正常',
                todayRanking: '今日排行', thisWeekTotal: '本周总计',
                thisMonthTotal: '本月总计',
                owner: '店主', mainPhone: '主号', altPhone: '备用', copy: '复制',
                region: '区域', unit: '台',
                dateFormat: '{year}年{month}月{day}日'
            },
            en: {
                usernameLabel: 'ID', passwordLabel: 'Password', rememberLabel: 'Remember me',
                loginBtn: 'LOGIN', logoutBtn: 'Logout',
                step1Title: 'Select Photos', step2Title: 'Remark', openCameraBtn: 'Select Photos',
                uploadBtn: 'Upload', cancelBtn: 'Cancel', cameraPreview: 'Click to select photos',
                photoModalTitle: 'Photo Upload',
                photoCountLabel: 'Selected', photoUnit: '',
                remarkNormal: '✅ Freezer Normal', remarkUnused: '⭕ Not in Use',
                remarkDirtyInside: '🧹 Inside Dirty', remarkOtherAd: '📢 Other Ads',
                remarkTemperature: '🌡️ Temperature Abnormal', remarkDamaged: '🔧 Freezer Damaged',
                remarkOther: '❓ Other Issues', remarkDetailPlaceholder: 'Details (optional, max 200 chars)',
                todayTasks: "Today's Tasks", myRecords: 'My Records', progress: 'Progress',
                waiting: 'Pending', completed: 'Completed', photo: 'Upload',
                totalFreezers: 'Total', todayPhotos: 'Today',
                weekPhotos: 'Week', monthPhotos: 'Month',
                overdue: 'Overdue', warning: 'Warning',
                syncTasks: 'Sync Tasks', statusMgmt: 'Status Management',
                regionStats: 'Region Stats', alerts: 'Alerts',
                search: 'Search', sync: 'Sync',
                overview: 'Overview', regions: 'Regions', salesmen: 'Salesmen',
                totalFreezersLabel: 'Total Freezers',
                active: 'Active', repair: 'In Repair', stock: 'In Stock',
                scrap: 'Scrapped', withdrawn: 'Withdrawn', officeManaged: 'Office Managed',
                attentionNeeded: 'Attention Needed', allNormal: 'All Normal',
                problemFreezers: 'Problem Freezers', allGood: 'All Normal',
                todayRanking: "Today's Ranking", thisWeekTotal: 'This Week Total',
                thisMonthTotal: 'This Month Total',
                owner: 'Owner', mainPhone: 'Main', altPhone: 'Alt', copy: 'Copy',
                region: 'Region', unit: '',
                dateFormat: '{year}-{month}-{day}'
            }
        };

        // ===== Google登录回调 =====
        window.handleGoogleSignIn = function(response) {
            const payload = JSON.parse(atob(response.credential.split('.')[1]));
            const email = payload.email;
            
            // 根据邮箱判断角色
            let role, region, name, nameEn;
            
            switch(email) {
                case 'Yashgill1478@gmail.com':
                    role = 'sales';
                    region = '1';
                    name = '业务员001';
                    nameEn = 'Salesman 001';
                    break;
                case 'kashifkhi021@gmail.com':
                    role = 'sales';
                    region = '2';
                    name = '业务员002';
                    nameEn = 'Salesman 002';
                    break;
                case 'Farazjan482@gmail.com':
                    role = 'sales';
                    region = '3';
                    name = '业务员003';
                    nameEn = 'Salesman 003';
                    break;
                case 'pakaicemap@gmail.com':
                    role = 'office';
                    name = '办公室';
                    nameEn = 'Office';
                    break;
                case 'liyang396484428@gmail.com':
                    role = 'director';
                    name = '执行官';
                    nameEn = 'Director';
                    break;
                default:
                    alert('此邮箱未授权，请联系管理员');
                    return;
            }
            
            // 保存用户信息
            currentUser = {
                email: email,
                role: role,
                region: region,
                name: name,
                nameEn: nameEn
            };
            
            localStorage.setItem('aice_user', JSON.stringify(currentUser));
            
            // 显示主页面
            document.getElementById('loginPage').classList.add('hidden');
            document.getElementById('mainPage').classList.remove('hidden');
            document.getElementById('displayName').textContent = currentLang === 'zh' ? name : nameEn;
            
            const d = new Date();
            document.getElementById('currentDate').textContent = formatDate(d);
            
            if (role === 'sales') showSalesView();
            else if (role === 'office') showOfficeView();
            else if (role === 'director') showDirectorView();
            
            alert(currentLang === 'zh' ? `欢迎 ${name}` : `Welcome ${nameEn}`);
        };

        // ===== Google Drive上传相关 =====
        async function initGoogleAuth() {
            return new Promise((resolve, reject) => {
                google.accounts.oauth2.initTokenClient({
                    client_id: CLIENT_ID,
                    scope: 'https://www.googleapis.com/auth/drive.file',
                    callback: (response) => {
                        if (response.access_token) {
                            googleAuth = response;
                            resolve(response);
                        } else {
                            reject(response);
                        }
                    },
                });
            });
        }

        async function getAccessToken() {
            if (googleAuth && googleAuth.access_token) {
                const expiresAt = googleAuth.expires_at || 0;
                if (Date.now() < expiresAt) {
                    return googleAuth.access_token;
                }
            }
            
            const tokenClient = google.accounts.oauth2.initTokenClient({
                client_id: CLIENT_ID,
                scope: 'https://www.googleapis.com/auth/drive.file',
                callback: (response) => {
                    if (response.access_token) {
                        response.expires_at = Date.now() + response.expires_in * 1000;
                        googleAuth = response;
                    }
                },
            });
            
            tokenClient.requestAccessToken();
            
            for (let i = 0; i < 10; i++) {
                await new Promise(r => setTimeout(r, 500));
                if (googleAuth && googleAuth.access_token) {
                    return googleAuth.access_token;
                }
            }
            throw new Error('获取访问令牌超时');
        }

        async function uploadToDrive(imageData, fileName) {
            try {
                const accessToken = await getAccessToken();
                
                const byteCharacters = atob(imageData.split(',')[1]);
                const byteNumbers = new Array(byteCharacters.length);
                for (let i = 0; i < byteCharacters.length; i++) {
                    byteNumbers[i] = byteCharacters.charCodeAt(i);
                }
                const byteArray = new Uint8Array(byteNumbers);
                const blob = new Blob([byteArray], { type: 'image/jpeg' });
                
                const metadata = {
                    name: fileName,
                    parents: [FOLDER_ID]
                };
                
                const formData = new FormData();
                formData.append('metadata', new Blob([JSON.stringify(metadata)], { type: 'application/json' }));
                formData.append('file', blob);
                
                const response = await fetch('https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart', {
                    method: 'POST',
                    headers: new Headers({
                        'Authorization': 'Bearer ' + accessToken
                    }),
                    body: formData
                });
                
                const result = await response.json();
                console.log('上传成功:', result);
                return result.id;
                
            } catch (error) {
                console.error('上传失败:', error);
                throw error;
            }
        }

        // ===== 工具函数 =====
        function getRegion(salesPerson) {
            const num = parseInt(salesPerson);
            if (num === 1) return '1';
            if (num === 2) return '2';
            if (num === 3) return '3';
            if (num === 4) return 'OFFICE';
            return null;
        }

        function getStatusBadge(status) {
            return statusMap[status] || statusMap.active;
        }

        function getRemarkText(type, lang) {
            const t = translations[lang];
            const map = {
                'normal': t.remarkNormal,
                'unused': t.remarkUnused,
                'dirty_inside': t.remarkDirtyInside,
                'other_ad': t.remarkOtherAd,
                'temperature': t.remarkTemperature,
                'damaged': t.remarkDamaged,
                'other': t.remarkOther
            };
            return map[type] || t.remarkNormal;
        }

        // ===== 复制电话 =====
        window.copyPhone = function(phone) {
            navigator.clipboard.writeText(phone).then(() => {
                alert('📋 电话已复制');
            }).catch(() => {
                const textarea = document.createElement('textarea');
                textarea.value = phone;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
                alert('📋 电话已复制');
            });
        };

        // ===== 格式化日期 =====
        function formatDate(date) {
            const d = new Date(date);
            const year = d.getFullYear();
            const month = d.getMonth() + 1;
            const day = d.getDate();
            return translations[currentLang].dateFormat
                .replace('{year}', year)
                .replace('{month}', month)
                .replace('{day}', day);
        }

        // ===== 从 CSV 加载数据 =====
        async function loadFreezersFromCSV() {
            try {
                const response = await fetch(CSV_URL);
                const csvText = await response.text();
                
                const lines = csvText.split('\n');
                if (lines.length < 2) {
                    console.error('CSV 数据为空');
                    return;
                }
                
                const idIndex = 0;
                const areaIndex = 2;
                const shopIndex = 3;
                const ownerIndex = 4;
                const phoneIndex = 5;
                const stateIndex = 6;
                
                const rows = lines.slice(1).filter(line => line.trim());
                
                freezers = rows.map(line => {
                    const values = line.split(',').map(v => v.replace(/^"|"$/g, '').trim());
                    const state = values[stateIndex] || '';
                    
                    return {
                        id: values[idIndex] || '',
                        region: values[areaIndex] || '',
                        shop: values[shopIndex] || '',
                        owner: values[ownerIndex] || '',
                        phone: values[phoneIndex] || '无电话',
                        status: sheetStatusMap[state] || 'active'
                    };
                }).filter(f => f.id && f.region);
                
                console.log(`✅ 从 CSV 加载 ${freezers.length} 台冰柜`);
                
            } catch (error) {
                console.error('❌ CSV 加载失败', error);
                alert('无法连接 Google Sheets，请检查网络后刷新页面');
                freezers = [
                    { id: 'FZ-A00006', region: '1', shop: 'V.S.P STORE', owner: 'Yasmeen', phone: '0315-7022729', status: 'active' },
                    { id: 'FZ-A00009', region: '1', shop: 'AL-SADDAT', owner: 'AHMED', phone: '0321-2899218', status: 'active' },
                    { id: 'FZ-A00002', region: '2', shop: 'UHUD MART', owner: 'Muhammad', phone: '0303-4742525', status: 'active' }
                ];
            }
        }

        // ===== 同步任务 =====
        window.syncTasks = function() {
            const text = document.getElementById('syncText').value;
            const lines = text.split('\n');
            
            lines.forEach(line => {
                const match = line.match(/区域([123])：\s*(.+)/);
                if (match) {
                    const region = match[1];
                    const ids = match[2].split(/[,，\s]+/).filter(id => id.startsWith('FZ-'));
                    if (ids.length) todayTasks[region] = ids;
                }
            });
            
            alert(`同步成功！共 ${Object.values(todayTasks).flat().length} 个任务`);
            showSyncView();
        };

        // ===== 语言 =====
        function updateUILanguage() {
            const t = translations[currentLang];
            
            const elements = [
                'step1Title', 'step2Title', 'openCameraBtn',
                'uploadBtn', 'cancelBtn', 'photoModalTitle',
                'photo-count-label', 'photo-unit', 'logoutBtn'
            ];
            
            elements.forEach(id => {
                const el = document.getElementById(id);
                if (el) el.textContent = t[id] || '';
            });
            
            const select = document.getElementById('remarkType');
            if (select) {
                select.options[0].text = t.remarkNormal;
                select.options[1].text = t.remarkUnused;
                select.options[2].text = t.remarkDirtyInside;
                select.options[3].text = t.remarkOtherAd;
                select.options[4].text = t.remarkTemperature;
                select.options[5].text = t.remarkDamaged;
                select.options[6].text = t.remarkOther;
            }
            
            const detail = document.getElementById('remarkDetail');
            if (detail) detail.placeholder = t.remarkDetailPlaceholder;
            
            if (currentUser) {
                const d = new Date();
                document.getElementById('currentDate').textContent = formatDate(d);
            }
        }

        window.switchLanguage = function(lang) {
            currentLang = lang;
            localStorage.setItem('language', lang);
            
            document.getElementById('langZhBtn').classList.toggle('active', lang === 'zh');
            document.getElementById('langEnBtn').classList.toggle('active', lang === 'en');
            
            updateUILanguage();
            
            if (currentUser) {
                document.getElementById('displayName').textContent = lang === 'zh' ? currentUser.name : currentUser.nameEn;
                if (currentUser.role === 'sales') showSalesView();
                else if (currentUser.role === 'office') showOfficeView();
                else if (currentUser.role === 'director') showDirectorView();
            }
        };

        window.logout = function() {
            localStorage.removeItem('aice_user');
            currentUser = null;
            document.getElementById('loginPage').classList.remove('hidden');
            document.getElementById('mainPage').classList.add('hidden');
        };

        // ===== 照片选择相关 =====
        document.getElementById('photo-input').addEventListener('change', function(e) {
            const files = Array.from(e.target.files);
            const remaining = 5 - selectedPhotos.length;
            
            if (files.length > remaining) {
                alert(`最多只能选 ${remaining} 张`);
                return;
            }
            
            files.forEach(file => {
                const reader = new FileReader();
                reader.onload = function(e) {
                    selectedPhotos.push({
                        file: file,
                        data: e.target.result,
                        name: file.name
                    });
                    updatePhotoPreview();
                };
                reader.readAsDataURL(file);
            });
        });

        function updatePhotoPreview() {
            const container = document.getElementById('photo-preview-area');
            const t = translations[currentLang];
            document.getElementById('photo-count').textContent = selectedPhotos.length;
            
            if (selectedPhotos.length === 0) {
                container.innerHTML = `<div style="text-align:center; color:#999; padding:20px;">${t.cameraPreview}</div>`;
                return;
            }
            
            let html = '';
            selectedPhotos.forEach((photo, index) => {
                html += `
                    <div class="photo-preview-item">
                        <img src="${photo.data}">
                        <div class="remove-btn" onclick="removePhoto(${index})">×</div>
                    </div>
                `;
            });
            container.innerHTML = html;
        }

        window.removePhoto = function(index) {
            selectedPhotos.splice(index, 1);
            updatePhotoPreview();
            document.getElementById('photo-input').value = '';
        };

        function generateFileName(freezerId, salesmanId, index) {
            const now = new Date();
            const dateStr = now.toISOString().slice(0,10).replace(/-/g,'');
            const timeStr = now.toTimeString().slice(0,8).replace(/:/g,'');
            return `${freezerId}_${dateStr}_${timeStr}_${salesmanId}_${index}.jpg`;
        }

        // ===== 上传照片 =====
        window.uploadPhotos = async function() {
            if (selectedPhotos.length === 0) {
                alert(translations[currentLang].cameraPreview);
                return;
            }
            
            if (!currentUser || !currentUser.email) {
                alert('请先用 Google 账号登录才能上传照片');
                return;
            }
            
            const remarkType = document.getElementById('remarkType').value;
            const remarkDetail = document.getElementById('remarkDetail').value;
            
            const uploadBtn = document.getElementById('uploadBtn');
            const originalText = uploadBtn.textContent;
            uploadBtn.textContent = `${translations[currentLang].uploadBtn} 0/${selectedPhotos.length}`;
            uploadBtn.disabled = true;
            
            let successCount = 0;
            
            try {
                await initGoogleAuth();
                
                for (let i = 0; i < selectedPhotos.length; i++) {
                    const photo = selectedPhotos[i];
                    const fileName = generateFileName(currentFreezer, currentUser.email.split('@')[0], i+1);
                    
                    try {
                        await uploadToDrive(photo.data, fileName);
                        
                        const photoRecord = {
                            freezerId: currentFreezer,
                            time: new Date().toISOString(),
                            sales: currentUser.email,
                            photo: photo.data,
                            driveFileName: fileName,
                            remark: {
                                type: remarkType,
                                text: getRemarkText(remarkType, currentLang),
                                detail: remarkDetail
                            }
                        };
                        photos.push(photoRecord);
                        
                        successCount++;
                        uploadBtn.textContent = `${translations[currentLang].uploadBtn} ${successCount}/${selectedPhotos.length}`;
                    } catch (error) {
                        console.error('上传失败', error);
                    }
                }
                
                localStorage.setItem('photos', JSON.stringify(photos));
                alert(`${translations[currentLang].uploadBtn} ${successCount}/${selectedPhotos.length}`);
                
            } catch (error) {
                alert('Google授权失败，请重试');
                console.error(error);
            }
            
            selectedPhotos = [];
            updatePhotoPreview();
            uploadBtn.textContent = originalText;
            uploadBtn.disabled = false;
            closePhotoModal();
            if (currentUser.role === 'sales') showSalesTasks();
        };

        // ===== 拍照相关 =====
        window.openPhotoModal = function(id) {
            currentFreezer = id;
            document.getElementById('modalFreezerId').textContent = id;
            document.getElementById('photoModal').classList.remove('hidden');
            document.getElementById('remarkDetail').value = '';
            document.getElementById('charCount').textContent = '0';
            
            selectedPhotos = [];
            updatePhotoPreview();
        };

        window.closePhotoModal = function() {
            document.getElementById('photoModal').classList.add('hidden');
            currentFreezer = null;
            selectedPhotos = [];
        };

        window.viewFullscreen = function(src) {
            document.getElementById('fullscreenImage').src = src;
            document.getElementById('fullscreenModal').classList.remove('hidden');
        };

        window.closeFullscreen = function() {
            document.getElementById('fullscreenModal').classList.add('hidden');
        };

        document.getElementById('remarkDetail').addEventListener('input', e => {
            document.getElementById('charCount').textContent = e.target.value.length;
        });

        // ===== 业务员视图 =====
        window.showSalesView = function() {
            const t = translations[currentLang];
            document.getElementById('navBar').innerHTML = `
                <div class="nav-item active" onclick="switchSalesTab('tasks')">${t.todayTasks}</div>
                <div class="nav-item" onclick="switchSalesTab('history')">${t.myRecords}</div>
                <div class="nav-item" onclick="switchSalesTab('stats')">${t.progress}</div>
            `;
            showSalesTasks();
        };

        window.switchSalesTab = function(tab) {
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            event.target.classList.add('active');
            if (tab === 'tasks') showSalesTasks();
            else if (tab === 'history') showSalesHistory();
            else showSalesStats();
        };

        function showSalesTasks() {
            const t = translations[currentLang];
            const region = currentUser.region;
            const taskIds = todayTasks[region] || [];
            
            const tasks = taskIds
                .map(id => freezers.find(f => f.id === id))
                .filter(f => f && f.status === 'active');
            
            let html = `
                <div class="stats-card">
                    <div class="stats-title">📋 ${t.todayTasks}</div>
                    <div class="stats-grid">
                        <div class="stat-item"><div class="stat-value">${tasks.length}</div><div class="stat-label">${t.totalFreezers}</div></div>
                        <div class="stat-item"><div class="stat-value">${tasks.filter(t => hasPhotoToday(t.id)).length}</div><div class="stat-label">${t.completed}</div></div>
                    </div>
                    <div class="progress-bar"><div class="progress-fill" style="width: ${tasks.length ? (tasks.filter(t => hasPhotoToday(t.id)).length / tasks.length * 100) : 0}%"></div></div>
                </div>
                <div class="task-list">
            `;
            
            tasks.forEach(task => {
                const photo = photos.find(p => p.freezerId === task.id && isToday(p.time));
                const phones = task.phone.split('/').map(p => p.trim());
                const mainPhone = phones[0];
                const hasSecond = phones.length > 1;
                
                html += `
                    <div class="task-item">
                        <div class="task-header">
                            <span class="freezer-id">${task.id}</span>
                            <span class="shop-name">${task.shop}</span>
                        </div>
                        <div class="shop-details">
                            <div style="margin-bottom:4px;">${t.owner}：${task.owner}</div>
                            <div style="display:flex; align-items:center; gap:8px; flex-wrap:wrap;">
                                <span style="color:var(--text);">📞 ${task.phone}</span>
                                <div style="display:flex; gap:4px;">
                                    <a href="tel:${mainPhone}" style="text-decoration:none;">
                                        <button class="call-btn">📞 ${t.mainPhone}</button>
                                    </a>
                                    ${hasSecond ? 
                                        `<a href="tel:${phones[1]}" style="text-decoration:none;">
                                            <button class="call-btn">📞 ${t.altPhone}</button>
                                        </a>` 
                                        : ''}
                                    <button class="copy-btn" onclick="copyPhone('${task.phone}')">📋 ${t.copy}</button>
                                </div>
                            </div>
                        </div>
                        ${photo && photo.remark ? `<div style="font-size:12px; color:var(--text-light); margin:8px 0;">📝 ${photo.remark.text}</div>` : ''}
                        <div class="task-footer">
                            <span class="time">${photo ? '✅' : '⏳'}</span>
                            <button class="photo-btn ${photo ? 'completed' : ''}" onclick="openPhotoModal('${task.id}')" ${photo ? 'disabled' : ''}>
                                ${photo ? t.completed : t.photo}
                            </button>
                        </div>
                    </div>
                `;
            });
            
            document.getElementById('content').innerHTML = html + '</div>';
        }

        function showSalesHistory() {
            const t = translations[currentLang];
            const myPhotos = photos.filter(p => p.sales === currentUser.email);
            if (!myPhotos.length) {
                document.getElementById('content').innerHTML = `<div class="stats-card">${currentLang === 'zh' ? '暂无记录' : 'No records'}</div>`;
                return;
            }
            
            let html = '<div class="task-list">';
            myPhotos.sort((a, b) => new Date(b.time) - new Date(a.time)).forEach(p => {
                const f = freezers.find(f => f.id === p.freezerId);
                html += `
                    <div class="task-item">
                        <div class="task-header">
                            <span class="freezer-id">${p.freezerId}</span>
                            <span class="shop-name">${f ? f.shop : ''}</span>
                        </div>
                        <div class="time">${formatDate(p.time)}</div>
                        ${p.photo ? `<img src="${p.photo}" class="photo-thumb" onclick="viewFullscreen('${p.photo}')">` : ''}
                        ${p.remark ? `<div style="margin-top:8px;">📝 ${p.remark.text} ${p.remark.detail ? '- ' + p.remark.detail : ''}</div>` : ''}
                    </div>
                `;
            });
            document.getElementById('content').innerHTML = html + '</div>';
        }

        function showSalesStats() {
            const t = translations[currentLang];
            const myPhotos = photos.filter(p => p.sales === currentUser.email);
            const today = myPhotos.filter(p => isToday(p.time)).length;
            const week = myPhotos.filter(p => isThisWeek(p.time)).length;
            const month = myPhotos.filter(p => isThisMonth(p.time)).length;
            
            document.getElementById('content').innerHTML = `
                <div class="stats-card">
                    <div class="stats-title">📊 ${t.myRecords}</div>
                    <div class="stats-grid">
                        <div class="stat-item"><div class="stat-value">${today}</div><div class="stat-label">${t.todayPhotos}</div></div>
                        <div class="stat-item"><div class="stat-value">${week}</div><div class="stat-label">${t.weekPhotos}</div></div>
                        <div class="stat-item"><div class="stat-value">${month}</div><div class="stat-label">${t.monthPhotos}</div></div>
                    </div>
                </div>
            `;
        }

        // ===== 办公室视图 =====
        window.showOfficeView = function() {
            const t = translations[currentLang];
            document.getElementById('navBar').innerHTML = `
                <div class="nav-item active" onclick="switchOfficeTab('sync')">${t.syncTasks}</div>
                <div class="nav-item" onclick="switchOfficeTab('status')">${t.statusMgmt}</div>
                <div class="nav-item" onclick="switchOfficeTab('stats')">${t.regionStats}</div>
                <div class="nav-item" onclick="switchOfficeTab('alerts')">${t.alerts}</div>
            `;
            showSyncView();
        };

        window.switchOfficeTab = function(tab) {
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            event.target.classList.add('active');
            if (tab === 'sync') showSyncView();
            else if (tab === 'status') showStatusManagement();
            else if (tab === 'stats') showRegionStats();
            else showAlerts();
        };

        function showSyncView() {
            const t = translations[currentLang];
            let html = `
                <div class="sync-card">
                    <div class="stats-title">📱 ${t.syncTasks}</div>
                    <div style="background:#f5f5f5; padding:12px; border-radius:12px; margin-bottom:12px; font-size:13px;">
                        区域1：FZ-A00006, FZ-A00009<br>
                        区域2：FZ-A00101, FZ-A00102<br>
                        区域3：FZ-A00201, FZ-A00202
                    </div>
                    <textarea class="sync-textarea" id="syncText" placeholder="${t.syncTasks}：FZ-A00006, FZ-A00009"></textarea>
                    <button class="sync-btn" onclick="syncTasks()">${t.sync}</button>
                </div>
            `;
            
            html += '<div class="region-tasks"><div class="stats-title">' + t.todayTasks + '</div>';
            for (let r in todayTasks) {
                if (todayTasks[r].length) {
                    html += `<div class="region-title">${t.region}${r}</div>`;
                    todayTasks[r].forEach(id => html += `<span class="freezer-tag">${id}</span>`);
                }
            }
            document.getElementById('content').innerHTML = html + '</div>';
        }

        // ===== 状态管理 =====
        function showStatusManagement() {
            const t = translations[currentLang];
            const total = freezers.length;
            
            const statusCounts = {
                active: freezers.filter(f => f.status === 'active').length,
                repair: freezers.filter(f => f.status === 'repair').length,
                stock: freezers.filter(f => f.status === 'stock').length,
                scrap: freezers.filter(f => f.status === 'scrap').length,
                withdrawn: freezers.filter(f => f.status === 'withdrawn').length,
                office: freezers.filter(f => f.status === 'office').length
            };
            
            const statusConfig = [
                { key: 'active', icon: '✅', name: t.active, color: themeRed, gradient: `linear-gradient(135deg, ${themeRed} 0%, ${themeRedLight} 100%)` },
                { key: 'repair', icon: '🔧', name: t.repair, color: themeRedLight, gradient: `linear-gradient(135deg, ${themeRedLight} 0%, #ff8a8a 100%)` },
                { key: 'stock', icon: '📦', name: t.stock, color: themeRedDark, gradient: `linear-gradient(135deg, ${themeRedDark} 0%, ${themeRed} 100%)` },
                { key: 'scrap', icon: '❌', name: t.scrap, color: '#6b7280', gradient: 'linear-gradient(135deg, #6b7280 0%, #9ca3af 100%)' },
                { key: 'withdrawn', icon: '⬅️', name: t.withdrawn, color: themeRed, gradient: `linear-gradient(135deg, ${themeRed} 0%, ${themeRedLight} 100%)` },
                { key: 'office', icon: '🏢', name: t.officeManaged, color: themeRedLight, gradient: `linear-gradient(135deg, ${themeRedLight} 0%, ${themeRed} 100%)` }
            ];
            
            let html = `
                <div class="status-card">
                    <div class="status-header">
                        <div class="status-header-line"></div>
                        <h2 style="font-size: 20px; font-weight: 600; color: #1e293b;">📋 ${t.statusMgmt}</h2>
                    </div>
                    
                    <div class="total-card">
                        <div style="display: flex; justify-content: space-between; align-items: center;">
                            <span style="font-size: 16px; color: #64748b;">${t.totalFreezersLabel}</span>
                            <span style="font-size: 32px; font-weight: 700; color: ${themeRed};">${total}<span style="font-size: 16px; color: #64748b; margin-left: 4px;">${t.unit}</span></span>
                        </div>
                    </div>
                    
                    <div style="display: flex; flex-direction: column; gap: 12px; margin-bottom: 24px;">
                        ${statusConfig.map(s => {
                            const count = statusCounts[s.key];
                            if (count === 0) return '';
                            
                            const percent = Math.round(count / total * 100);
                            
                            return `
                                <div class="status-item">
                                    <div class="status-item-header">
                                        <div class="status-item-left">
                                            <span style="font-size: 20px;">${s.icon}</span>
                                            <span style="font-weight: 600; color: #1e293b;">${s.name}</span>
                                        </div>
                                        <div class="status-item-right">
                                            <span class="status-count" style="color: ${s.color};">${count}</span>
                                            <span class="status-percent">${percent}%</span>
                                        </div>
                                    </div>
                                    <div class="progress-container">
                                        <div class="progress-fill-custom" style="width: ${percent}%; background: ${s.gradient};"></div>
                                        <div class="progress-text">${percent}%</div>
                                    </div>
                                </div>
                            `;
                        }).join('')}
                    </div>
                    
                    <div class="warning-card">
                        <div class="warning-header">
                            <span style="font-size: 20px;">⚠️</span>
                            <span style="font-weight: 600; color: #991b1b;">${t.attentionNeeded}</span>
                        </div>
                        <div>
                            ${statusCounts.repair > 0 ? `
                                <div class="warning-item">
                                    <div class="warning-dot" style="background: ${themeRedLight};"></div>
                                    <span class="warning-text">🔧 ${t.repair}</span>
                                    <span class="warning-count" style="color: ${themeRedLight};">${statusCounts.repair}${t.unit}</span>
                                </div>
                            ` : ''}
                            ${statusCounts.stock > 0 ? `
                                <div class="warning-item">
                                    <div class="warning-dot" style="background: ${themeRedDark};"></div>
                                    <span class="warning-text">📦 ${t.stock}</span>
                                    <span class="warning-count" style="color: ${themeRedDark};">${statusCounts.stock}${t.unit}</span>
                                </div>
                            ` : ''}
                            ${statusCounts.scrap > 0 ? `
                                <div class="warning-item">
                                    <div class="warning-dot" style="background: #6b7280;"></div>
                                    <span class="warning-text">❌ ${t.scrap}</span>
                                    <span class="warning-count" style="color: #6b7280;">${statusCounts.scrap}${t.unit}</span>
                                </div>
                            ` : ''}
                            ${statusCounts.withdrawn > 0 ? `
                                <div class="warning-item">
                                    <div class="warning-dot" style="background: ${themeRed};"></div>
                                    <span class="warning-text">⬅️ ${t.withdrawn}</span>
                                    <span class="warning-count" style="color: ${themeRed};">${statusCounts.withdrawn}${t.unit}</span>
                                </div>
                            ` : ''}
                            ${statusCounts.office > 0 ? `
                                <div class="warning-item">
                                    <div class="warning-dot" style="background: ${themeRedLight};"></div>
                                    <span class="warning-text">🏢 ${t.officeManaged}</span>
                                    <span class="warning-count" style="color: ${themeRedLight};">${statusCounts.office}${t.unit}</span>
                                </div>
                            ` : ''}
                            ${statusCounts.repair + statusCounts.stock + statusCounts.scrap + statusCounts.withdrawn + statusCounts.office === 0 ? 
                                `<div style="text-align: center; padding: 20px; color: #059669;">✅ ${t.allNormal}</div>` 
                                : ''}
                        </div>
                    </div>
                </div>
            `;
            
            document.getElementById('content').innerHTML = html;
        }

        function showRegionStats() {
            const t = translations[currentLang];
            const regions = ['1', '2', '3'];
            let html = '<div class="stats-card"><div class="stats-title">📍 ' + t.regionStats + '</div>';
            regions.forEach(r => {
                const regionFreezers = freezers.filter(f => f.region === r && f.status === 'active');
                const todayCount = photos.filter(p => regionFreezers.some(f => f.id === p.freezerId) && isToday(p.time)).length;
                const percent = Math.round(todayCount / regionFreezers.length * 100) || 0;
                html += `
                    <div style="margin:15px 0;">
                        <div style="display:flex; justify-content:space-between;">${t.region}${r} <span>${todayCount}/${regionFreezers.length}</span></div>
                        <div class="progress-bar"><div class="progress-fill" style="width:${percent}%"></div></div>
                    </div>
                `;
            });
            document.getElementById('content').innerHTML = html + '</div>';
        }

        // ===== 预警系统（双色预警）=====
        function showAlerts() {
            const t = translations[currentLang];
            
            const yellowAlerts = freezers.filter(f => f.status === 'active').filter(f => {
                const last = photos.filter(p => p.freezerId === f.id)
                    .sort((a,b) => new Date(b.time) - new Date(a.time))[0];
                if (!last) return false;
                const daysAgo = (new Date() - new Date(last.time)) / (24*60*60*1000);
                return daysAgo >= 7 && daysAgo < 14;
            });
            
            const redAlerts = freezers.filter(f => f.status === 'active').filter(f => {
                const last = photos.filter(p => p.freezerId === f.id)
                    .sort((a,b) => new Date(b.time) - new Date(a.time))[0];
                if (!last) return false;
                const daysAgo = (new Date() - new Date(last.time)) / (24*60*60*1000);
                return daysAgo >= 14;
            });
            
            const neverPhoto = freezers.filter(f => f.status === 'active').filter(f => {
                const last = photos.filter(p => p.freezerId === f.id)[0];
                return !last;
            });
            
            let html = `<div class="stats-card"><div class="stats-title">⚠️ ${t.alerts}</div>`;
            
            if (yellowAlerts.length === 0 && redAlerts.length === 0 && neverPhoto.length === 0) {
                html += `<div style="text-align:center; padding:20px; color:#059669;">✅ ${t.allNormal}</div>`;
            } else {
                if (redAlerts.length > 0) {
                    html += `<div style="margin:15px 0 10px;"><span style="color:#ef4444; font-weight:bold;">🔴 红色预警 (${redAlerts.length})</span></div>`;
                    redAlerts.slice(0,5).forEach(f => {
                        const last = photos.filter(p => p.freezerId === f.id)[0];
                        const days = Math.floor((new Date() - new Date(last.time)) / (24*60*60*1000));
                        html += `<div style="padding:8px 0; border-bottom:1px solid #fee2e2; color:#ef4444; display:flex; justify-content:space-between;">
                            <span>${f.id} - ${f.shop}</span>
                            <span style="font-weight:bold;">${days}天</span>
                        </div>`;
                    });
                }
                
                if (yellowAlerts.length > 0) {
                    html += `<div style="margin:15px 0 10px;"><span style="color:#eab308; font-weight:bold;">🟡 黄色预警 (${yellowAlerts.length})</span></div>`;
                    yellowAlerts.slice(0,5).forEach(f => {
                        const last = photos.filter(p => p.freezerId === f.id)[0];
                        const days = Math.floor((new Date() - new Date(last.time)) / (24*60*60*1000));
                        html += `<div style="padding:8px 0; border-bottom:1px solid #fef9c3; color:#854d0e; display:flex; justify-content:space-between;">
                            <span>${f.id} - ${f.shop}</span>
                            <span style="font-weight:bold;">${days}天</span>
                        </div>`;
                    });
                }
                
                if (neverPhoto.length > 0) {
                    html += `<div style="margin:15px 0 10px;"><span style="color:#6b7280; font-weight:bold;">⚪ 从未拍照 (${neverPhoto.length})</span></div>`;
                    neverPhoto.slice(0,5).forEach(f => {
                        html += `<div style="padding:8px 0; border-bottom:1px solid #e5e7eb; color:#6b7280; display:flex; justify-content:space-between;">
                            <span>${f.id} - ${f.shop}</span>
                            <span style="font-weight:bold;">新冰柜</span>
                        </div>`;
                    });
                }
                
                if (yellowAlerts.length > 5 || redAlerts.length > 5 || neverPhoto.length > 5) {
                    html += `<div style="text-align:center; margin-top:10px; color:#999;">......</div>`;
                }
            }
            
            html += '</div>';
            document.getElementById('content').innerHTML = html;
        }

        // ===== 执行官视图 =====
        window.showDirectorView = function() {
            const t = translations[currentLang];
            document.getElementById('navBar').innerHTML = `
                <div class="nav-item active" onclick="switchDirectorTab('overview')">${t.overview}</div>
                <div class="nav-item" onclick="switchDirectorTab('status')">${t.statusMgmt}</div>
                <div class="nav-item" onclick="switchDirectorTab('regions')">${t.regions}</div>
                <div class="nav-item" onclick="switchDirectorTab('sales')">${t.salesmen}</div>
                <div class="nav-item" onclick="switchDirectorTab('alerts')">${t.alerts}</div>
            `;
            showDirectorOverview();
        };

        window.switchDirectorTab = function(tab) {
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            event.target.classList.add('active');
            if (tab === 'overview') showDirectorOverview();
            else if (tab === 'status') showStatusManagement();
            else if (tab === 'regions') showRegionStats();
            else if (tab === 'sales') showDirectorSales();
            else showAlerts();
        };

        function showDirectorOverview() {
            const t = translations[currentLang];
            const total = freezers.filter(f => f.status === 'active').length;
            const today = photos.filter(p => isToday(p.time)).length;
            const week = photos.filter(p => isThisWeek(p.time)).length;
            const month = photos.filter(p => isThisMonth(p.time)).length;
            
            const problems = photos.filter(p => {
                if (!p.remark) return false;
                const text = p.remark.text || '';
                return !text.includes('正常') && !text.includes('Normal');
            }).length;
            
            let html = `
                <div class="stats-card">
                    <div class="stats-title">📊 ${t.overview}</div>
                    <div class="stats-grid">
                        <div class="stat-item"><div class="stat-value">${total}</div><div class="stat-label">${t.totalFreezers}</div></div>
                        <div class="stat-item"><div class="stat-value">${today}</div><div class="stat-label">${t.todayPhotos}</div></div>
                        <div class="stat-item"><div class="stat-value">${week}</div><div class="stat-label">${t.weekPhotos}</div></div>
                        <div class="stat-item"><div class="stat-value">${month}</div><div class="stat-label">${t.monthPhotos}</div></div>
                    </div>
                    <div style="margin-top:16px; padding:12px; background:${problems > 0 ? '#fee2e2' : '#f0fdf4'}; border-radius:12px;">
                        ${problems > 0 ? `⚠️ ${t.problemFreezers}：${problems}${t.unit}` : `✅ ${t.allGood}`}
                    </div>
                </div>
            `;
            
            document.getElementById('content').innerHTML = html;
        }

        function showDirectorSales() {
            const t = translations[currentLang];
            const sales = [
                { name: currentLang === 'zh' ? '业务员001' : 'Salesman 001', email: 'Yashgill1478@gmail.com' },
                { name: currentLang === 'zh' ? '业务员002' : 'Salesman 002', email: 'kashifkhi021@gmail.com' },
                { name: currentLang === 'zh' ? '业务员003' : 'Salesman 003', email: 'Farazjan482@gmail.com' }
            ];
            
            let html = '<div class="stats-card"><div class="stats-title">👥 ' + t.salesmen + '</div>';
            
            const todayRank = sales.map(s => ({
                name: s.name,
                count: photos.filter(p => p.sales === s.email && isToday(p.time)).length
            })).sort((a,b) => b.count - a.count);
            
            html += '<div style="margin-bottom:16px;"><div style="font-weight:600;">' + t.todayRanking + '</div>';
            todayRank.forEach((s, i) => {
                const medal = i === 0 ? '🥇' : i === 1 ? '🥈' : i === 2 ? '🥉' : '👤';
                html += `<div style="display:flex; justify-content:space-between; padding:8px 0;">${medal} ${s.name} <span style="font-weight:600;">${s.count}${t.unit}</span></div>`;
            });
            html += '</div>';
            
            html += '<div><div style="font-weight:600;">' + t.thisWeekTotal + '</div>';
            sales.forEach(s => {
                const week = photos.filter(p => p.sales === s.email && isThisWeek(p.time)).length;
                const month = photos.filter(p => p.sales === s.email && isThisMonth(p.time)).length;
                html += `<div style="display:flex; justify-content:space-between; padding:6px 0;">${s.name} <span>${t.weekPhotos} ${week} / ${t.monthPhotos} ${month}</span></div>`;
            });
            html += '</div></div>';
            
            document.getElementById('content').innerHTML = html;
        }

        // ===== 工具函数 =====
        function hasPhotoToday(id) {
            return photos.some(p => p.freezerId === id && isToday(p.time));
        }

        function isToday(date) {
            const d = new Date(date);
            const t = new Date();
            return d.getDate() === t.getDate() && d.getMonth() === t.getMonth() && d.getFullYear() === t.getFullYear();
        }

        function isThisWeek(date) {
            const d = new Date(date);
            const t = new Date();
            const w = new Date(t); w.setDate(t.getDate() - 7);
            return d >= w;
        }

        function isThisMonth(date) {
            const d = new Date(date);
            const t = new Date();
            return d.getMonth() === t.getMonth() && d.getFullYear() === t.getFullYear();
        }

        // ===== 初始化 =====
        window.onload = async function() {
            await loadFreezersFromCSV();
            updateUILanguage();
            
            const saved = localStorage.getItem('aice_user');
            if (saved) {
                try {
                    currentUser = JSON.parse(saved);
                    document.getElementById('loginPage').classList.add('hidden');
                    document.getElementById('mainPage').classList.remove('hidden');
                    document.getElementById('displayName').textContent = currentLang === 'zh' ? currentUser.name : currentUser.nameEn;
                    
                    const d = new Date();
                    document.getElementById('currentDate').textContent = formatDate(d);
                    
                    if (currentUser.role === 'sales') showSalesView();
                    else if (currentUser.role === 'office') showOfficeView();
                    else if (currentUser.role === 'director') showDirectorView();
                } catch (e) {
                    localStorage.removeItem('aice_user');
                }
            }
        };
    </script>
</body>
</html>
