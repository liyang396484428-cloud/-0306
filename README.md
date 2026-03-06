<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Aice 冰柜巡检系统</title>
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
        }
        
        :root {
            --aice-red: #e31e24;
            --aice-red-light: #ff6b6b;
            --aice-red-dark: #c41a1f;
        }
        
        .login-container {
            max-width: 400px;
            width: 90%;
            margin: 0 auto;
            background: white;
            border-radius: 30px;
            padding: 40px 30px;
            box-shadow: 0 20px 60px rgba(227, 30, 36, 0.15);
            border: 1px solid rgba(227, 30, 36, 0.1);
        }
        
        .logo {
            text-align: center;
            margin-bottom: 30px;
        }

        .logo h1 {
            color: var(--aice-red);
            font-size: 72px;
            font-weight: bold;
            font-style: italic;
            letter-spacing: 2px;
            text-shadow: 3px 3px 0 rgba(227, 30, 36, 0.1);
            margin-bottom: 5px;
            line-height: 1;
        }

        .brand-line {
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--aice-red), transparent);
            width: 80px;
            margin: 15px auto;
        }

        .tagline {
            margin: 20px 0 30px;
            font-size: 20px;
            letter-spacing: 2px;
            color: #333;
            font-weight: 500;
        }

        .tagline span {
            color: var(--aice-red);
            font-weight: bold;
            font-style: italic;
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        .input-group label {
            display: block;
            color: #333;
            font-size: 14px;
            margin-bottom: 5px;
            font-weight: 500;
        }
        
        .input-group input {
            width: 100%;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 12px;
            font-size: 16px;
            transition: 0.3s;
        }
        
        .input-group input:focus {
            outline: none;
            border-color: var(--aice-red);
            box-shadow: 0 0 0 3px rgba(227, 30, 36, 0.1);
        }
        
        .remember {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .remember input {
            margin-right: 8px;
            accent-color: var(--aice-red);
        }
        
        .login-btn {
            width: 100%;
            padding: 15px;
            background: var(--aice-red);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        .login-btn:hover {
            background: var(--aice-red-dark);
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(227, 30, 36, 0.3);
        }
        
        .main-container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            min-height: 100vh;
            position: relative;
            box-shadow: 0 0 30px rgba(0,0,0,0.05);
        }
        
        .header {
            background: var(--aice-red);
            padding: 15px 20px;
            color: white;
            position: relative;
            overflow: hidden;
        }
        
        .header::after {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200px;
            height: 200px;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
        }
        
        .header::before {
            content: '';
            position: absolute;
            bottom: -50%;
            left: -50%;
            width: 200px;
            height: 200px;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
        }
        
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
        }
        
        .lang-switch {
            display: flex;
            gap: 10px;
            background: rgba(255,255,255,0.2);
            padding: 4px;
            border-radius: 30px;
            backdrop-filter: blur(5px);
        }
        
        .lang-btn {
            padding: 4px 16px;
            border-radius: 30px;
            font-size: 13px;
            cursor: pointer;
            transition: 0.3s;
            font-weight: 500;
            color: white;
        }
        
        .lang-btn.active {
            background: white;
            color: var(--aice-red);
            font-weight: bold;
        }
        
        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
            position: relative;
            z-index: 1;
        }
        
        .user-name {
            font-size: 16px;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 5px;
            background: rgba(255,255,255,0.2);
            padding: 5px 12px;
            border-radius: 30px;
        }
        
        .user-name::before {
            content: '👤';
            font-size: 14px;
            opacity: 0.9;
        }
        
        .logout-btn {
            background: rgba(255,255,255,0.2);
            padding: 5px 12px;
            border-radius: 30px;
            font-size: 13px;
            cursor: pointer;
            backdrop-filter: blur(5px);
            transition: 0.3s;
        }
        
        .logout-btn:hover {
            background: rgba(255,255,255,0.3);
        }
        
        .date {
            font-size: 14px;
            opacity: 0.9;
            margin-top: 5px;
            position: relative;
            z-index: 1;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .date::before {
            content: '📅';
            font-size: 14px;
        }
        
        .brand-footer {
            text-align: center;
            padding: 15px;
            font-size: 12px;
            color: #999;
            border-top: 1px solid #eee;
            background: white;
        }
        
        .brand-footer span {
            color: var(--aice-red);
            font-weight: bold;
        }
        
        .stats-card {
            background: white;
            margin: 15px;
            padding: 20px;
            border-radius: 16px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.03);
            border: 1px solid #f0f0f0;
        }
        
        .stats-title {
            font-size: 18px;
            font-weight: bold;
            color: #333;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .stats-title::before {
            content: '📊';
            font-size: 20px;
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
            margin-top: 5px;
        }
        
        .region-list {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        .region-item {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 12px;
        }
        
        .region-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .region-name {
            font-weight: bold;
            font-size: 16px;
            color: #333;
        }
        
        .region-stats {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .region-count {
            font-size: 14px;
            color: #666;
        }
        
        .region-percent {
            font-weight: bold;
            padding: 4px 8px;
            border-radius: 20px;
            font-size: 13px;
        }
        
        .region-percent.high {
            background: #e8f5e9;
            color: #00a65a;
        }
        
        .region-percent.medium {
            background: #fff3e0;
            color: #ff9800;
        }
        
        .region-percent.low {
            background: #ffebee;
            color: #ff4444;
        }
        
        .progress-bar {
            height: 8px;
            background: #e0e0e0;
            border-radius: 4px;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            background: var(--aice-red);
            border-radius: 4px;
            transition: width 0.3s;
        }
        
        .freezer-id {
            font-weight: bold;
            font-size: 16px;
            color: var(--aice-red);
            background: rgba(227, 30, 36, 0.05);
            padding: 4px 10px;
            border-radius: 20px;
        }
        
        .task-list {
            padding: 0 15px;
        }
        
        .task-item {
            background: white;
            border: 1px solid #f0f0f0;
            border-radius: 16px;
            padding: 15px;
            margin-bottom: 12px;
            transition: 0.3s;
        }
        
        .task-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .shop-name {
            font-weight: bold;
            font-size: 16px;
        }
        
        .shop-details {
            color: #666;
            font-size: 14px;
            margin: 5px 0;
        }
        
        .task-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 10px;
        }
        
        .time {
            color: #999;
            font-size: 13px;
        }
        
        .photo-btn {
            background: var(--aice-red);
            color: white;
            border: none;
            padding: 8px 20px;
            border-radius: 30px;
            font-size: 14px;
            cursor: pointer;
            transition: 0.3s;
            font-weight: 500;
        }
        
        .photo-btn:hover {
            background: var(--aice-red-dark);
            transform: scale(1.02);
        }
        
        .photo-btn.completed {
            background: #00a65a;
        }
        
        .photo-btn:disabled {
            background: #ccc;
            cursor: not-allowed;
        }
        
        .photo-preview {
            width: 100%;
            height: 200px;
            background: #f5f5f5;
            border-radius: 10px;
            margin: 10px 0;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #999;
            overflow: hidden;
        }
        
        .photo-preview img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .camera-btn {
            background: #333;
            color: white;
            border: none;
            padding: 12px;
            border-radius: 10px;
            width: 100%;
            font-size: 16px;
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
            border: 1px solid rgba(227, 30, 36, 0.2);
        }
        
        .remark-title {
            font-weight: bold;
            color: var(--aice-red);
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .remark-title::before {
            content: '📝';
        }
        
        .remark-select {
            width: 100%;
            padding: 12px;
            border: 1px solid #ffcdd2;
            border-radius: 12px;
            font-size: 14px;
            margin-bottom: 10px;
            background: white;
            color: #333;
        }
        
        .remark-input {
            width: 100%;
            padding: 12px;
            border: 1px solid #ffcdd2;
            border-radius: 12px;
            font-size: 14px;
            margin-top: 10px;
        }
        
        .remark-input:focus {
            outline: none;
            border-color: var(--aice-red);
            box-shadow: 0 0 0 3px rgba(227, 30, 36, 0.1);
        }
        
        .remark-badge {
            background: #fff3e0;
            color: #e65100;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            display: inline-block;
            margin: 5px 0;
            border: 1px solid #ffe0b2;
        }
        
        .remark-detail {
            background: #f5f5f5;
            padding: 10px;
            border-radius: 12px;
            font-size: 13px;
            color: #666;
            margin-top: 5px;
            border-left: 3px solid var(--aice-red);
        }
        
        .sync-card {
            background: white;
            margin: 15px;
            padding: 20px;
            border-radius: 12px;
            border: 1px solid var(--aice-red);
        }
        
        .sync-textarea {
            width: 100%;
            height: 100px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 10px;
            margin: 10px 0;
            font-size: 14px;
        }
        
        .sync-btn {
            background: var(--aice-red);
            color: white;
            border: none;
            padding: 12px;
            border-radius: 10px;
            width: 100%;
            font-size: 16px;
            cursor: pointer;
        }
        
        .region-tasks {
            background: white;
            margin: 15px;
            padding: 20px;
            border-radius: 12px;
        }
        
        .region-title {
            font-weight: bold;
            margin: 15px 0 10px;
            color: var(--aice-red);
        }
        
        .freezer-tag {
            display: inline-block;
            background: #f0f0f0;
            padding: 5px 12px;
            border-radius: 20px;
            margin: 0 5px 5px 0;
            font-size: 13px;
        }
        
        .nav-bar {
            display: flex;
            background: white;
            border-top: 1px solid #eee;
            border-bottom: 1px solid #eee;
            position: sticky;
            top: 0;
            width: 100%;
            max-width: 500px;
            z-index: 100;
            padding: 5px 0;
            box-shadow: 0 2px 10px rgba(0,0,0,0.03);
        }
        
        .nav-item {
            flex: 1;
            text-align: center;
            padding: 12px;
            color: #666;
            cursor: pointer;
            font-size: 14px;
            transition: 0.3s;
            position: relative;
            font-weight: 500;
        }
        
        .nav-item.active {
            color: var(--aice-red);
            font-weight: bold;
        }
        
        .nav-item.active::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 30px;
            height: 3px;
            background: var(--aice-red);
            border-radius: 3px;
        }
        
        .search-box {
            margin: 15px;
            padding: 10px;
            background: white;
            border-radius: 10px;
            border: 1px solid #ddd;
            display: flex;
            gap: 10px;
        }
        
        .search-box input {
            flex: 1;
            padding: 10px;
            border: none;
            font-size: 16px;
        }
        
        .search-box input:focus {
            outline: none;
        }
        
        .stat-row {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px dashed #eee;
        }
        
        .stat-label {
            color: #666;
        }
        
        .stat-value {
            font-weight: bold;
            color: #333;
        }
        
        .stat-value.warning {
            color: #ff4444;
        }
        
        .stat-value.success {
            color: #00a65a;
        }
        
        .history-item {
            padding: 10px;
            border-bottom: 1px solid #eee;
        }
        
        .history-time {
            color: #999;
            font-size: 12px;
        }
        
        .badge {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 12px;
            background: #00a65a;
            color: white;
        }
        
        .badge.warning {
            background: #ffaa00;
        }
        
        .badge.danger {
            background: #ff4444;
        }
        
        #photoModal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.9);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow-y: auto;
            padding: 20px;
        }
        
        #photoModal > div {
            background: white;
            width: 100%;
            max-width: 450px;
            padding: 25px;
            border-radius: 30px;
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
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .modal-title::before {
            content: '📸';
            font-size: 24px;
        }
        
        .hidden {
            display: none !important;
        }
    </style>
</head>
<body>
    <div id="app">
        <!-- 登录页 -->
        <div id="loginPage" class="login-container">
            <div class="logo">
                <h1>Aice</h1>
                <div class="brand-line"></div>
                <div class="tagline">
                    HAVE AN <span>AICE</span> DAY
                </div>
            </div>
            
            <div class="input-group">
                <label id="usernameLabel">编号</label>
                <input type="text" id="username" placeholder="001-005" value="001">
            </div>
            
            <div class="input-group">
                <label id="passwordLabel">密码</label>
                <input type="password" id="password" placeholder="123456" value="123456">
            </div>
            
            <div class="remember">
                <input type="checkbox" id="remember" checked>
                <label for="remember" id="rememberLabel">记住登录状态</label>
            </div>
            
            <button class="login-btn" onclick="handleLogin()" id="loginBtn">登录</button>
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

        <!-- 拍照模态框 -->
        <div id="photoModal" class="hidden">
            <div>
                <div class="modal-title" id="photoModalTitle">拍照上传 - <span id="modalFreezerId"></span></div>
                
                <div style="margin-bottom: 20px;">
                    <div style="font-weight: bold; color: #333; margin-bottom: 10px; display: flex; align-items: center; gap: 5px;">
                        <span style="background: var(--aice-red); color: white; width: 24px; height: 24px; border-radius: 50%; display: inline-flex; align-items: center; justify-content: center; font-size: 14px;">1</span>
                        <span id="step1Title">拍照</span>
                    </div>
                    <div id="camera-preview" class="photo-preview">
                        相机预览区域
                    </div>
                    <input type="file" id="camera-input" accept="image/*" capture="environment" style="display: none;">
                    <button class="camera-btn" onclick="openCamera()" id="openCameraBtn">打开相机</button>
                </div>
                
                <div class="remark-section">
                    <div class="remark-title" id="step2Title">
                        <span style="background: var(--aice-red); color: white; width: 24px; height: 24px; border-radius: 50%; display: inline-flex; align-items: center; justify-content: center; font-size: 14px; margin-right: 8px;">2</span>
                        备注
                    </div>
                    <select class="remark-select" id="remarkType">
                        <option value="normal">冰柜正常</option>
                        <option value="unused">冰柜未使用</option>
                        <option value="dirty_inside">冰柜内部脏了，需清洁</option>
                        <option value="other_ad">冰柜外部有其他广告</option>
                        <option value="temperature">冰柜温度异常</option>
                        <option value="damaged">冰柜有损坏</option>
                        <option value="other">其他问题</option>
                    </select>
                    
                    <input type="text" class="remark-input" id="remarkDetail" placeholder="详细说明（选填，最多100字）" maxlength="100" value="">
                    <div style="text-align: right; font-size: 12px; color: #999; margin-top: 5px;">
                        <span id="charCount">0</span>/100
                    </div>
                </div>
                
                <button class="upload-btn" onclick="uploadPhoto()" id="uploadBtn">确认上传</button>
                <button style="background: #999; color: white; border: none; padding: 12px; border-radius: 12px; width: 100%; margin-top: 10px; cursor: pointer;" onclick="closePhotoModal()" id="cancelBtn">取消</button>
            </div>
        </div>
    </div>

    <script>
        // ========== Google Sheets 数据链接 ==========
        const CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vRw6l0RVWFFp1KX7cJbWn9lZDHBNNWBV9Im8QEXxjRBoTKTEe5eFIMxtP8Bb8Y3WmOXEu2RIU6kAEVt/pub?output=csv';

        // ========== 全局变量 ==========
        let freezers = [];
        let currentUser = null;
        let currentFreezer = null;
        let currentLang = localStorage.getItem('language') || 'zh';
        
        // 拍照记录
        let photos = JSON.parse(localStorage.getItem('photos')) || [];

        // 今日任务（从WhatsApp同步）
        let todayTasks = {
            A: [],
            B: [],
            C: []
        };

        // ========== 账号数据（编号登录）==========
        const users = {
            '001': { password: '123456', role: 'sales', region: 'A', name: '业务员001', nameEn: 'Sales 001' },
            '002': { password: '123456', role: 'sales', region: 'B', name: '业务员002', nameEn: 'Sales 002' },
            '003': { password: '123456', role: 'sales', region: 'C', name: '业务员003', nameEn: 'Sales 003' },
            '004': { password: '123456', role: 'office', name: '办公室', nameEn: 'Office' },
            '005': { password: '123456', role: 'boss', name: '老板', nameEn: 'Boss' }
        };

        // ========== 多语言文案 ==========
        const translations = {
            zh: {
                usernameLabel: '编号',
                passwordLabel: '密码',
                rememberLabel: '记住登录状态',
                loginBtn: '登录',
                logoutBtn: '退出',
                step1Title: '拍照',
                step2Title: '备注',
                openCameraBtn: '打开相机',
                uploadBtn: '确认上传',
                cancelBtn: '取消',
                cameraPreview: '相机预览区域',
                
                remarkNormal: '冰柜正常',
                remarkUnused: '冰柜未使用',
                remarkDirtyInside: '冰柜内部脏了，需清洁',
                remarkOtherAd: '冰柜外部有其他广告',
                remarkTemperature: '冰柜温度异常',
                remarkDamaged: '冰柜有损坏',
                remarkOther: '其他问题',
                remarkDetailPlaceholder: '详细说明（选填，最多100字）',
                
                todayTasks: '今日任务',
                myRecords: '我的记录',
                progress: '进度',
                waiting: '待拍照',
                completed: '已完成',
                photo: '拍照',
                
                syncTasks: '同步任务',
                freezerSearch: '冰柜查询',
                regionStats: '区域统计',
                alerts: '预警',
                
                overview: '总览',
                regions: '区域详情',
                salesmen: '业务员',
                
                totalFreezers: '总冰柜',
                todayPhotos: '今日拍照',
                weekPhotos: '本周拍照',
                monthPhotos: '本月拍照',
                overdue: '超期未拍',
                warning: '即将超期',
                
                search: '搜索',
                sync: '解析并同步'
            },
            en: {
                usernameLabel: 'ID',
                passwordLabel: 'Password',
                rememberLabel: 'Remember me',
                loginBtn: 'Login',
                logoutBtn: 'Logout',
                step1Title: 'Take Photo',
                step2Title: 'Remark',
                openCameraBtn: 'Open Camera',
                uploadBtn: 'Upload',
                cancelBtn: 'Cancel',
                cameraPreview: 'Camera Preview',
                
                remarkNormal: 'Freezer normal',
                remarkUnused: 'Freezer not in use',
                remarkDirtyInside: 'Inside dirty, needs cleaning',
                remarkOtherAd: 'Other ads on freezer',
                remarkTemperature: 'Temperature abnormal',
                remarkDamaged: 'Freezer damaged',
                remarkOther: 'Other issues',
                remarkDetailPlaceholder: 'Details (optional, max 100 chars)',
                
                todayTasks: "Today's Tasks",
                myRecords: 'My Records',
                progress: 'Progress',
                waiting: 'Pending',
                completed: 'Completed',
                photo: 'Photo',
                
                syncTasks: 'Sync Tasks',
                freezerSearch: 'Freezer Search',
                regionStats: 'Region Stats',
                alerts: 'Alerts',
                
                overview: 'Overview',
                regions: 'Regions',
                salesmen: 'Salesmen',
                
                totalFreezers: 'Total Freezers',
                todayPhotos: "Today's Photos",
                weekPhotos: 'This Week',
                monthPhotos: 'This Month',
                overdue: 'Overdue',
                warning: 'Warning',
                
                search: 'Search',
                sync: 'Sync'
            }
        };

        // ========== 工具函数 ==========
        function getRegion(salesPerson) {
            const map = {
                '1': 'A',
                '2': 'B', 
                '3': 'C'
            };
            return map[salesPerson?.trim()] || 'A';
        }

        // ========== 从 Google Sheets 加载数据 ==========
        async function loadFreezersFromSheet() {
            try {
                const response = await fetch(CSV_URL);
                const csv = await response.text();
                
                const lines = csv.split('\n');
                // 数据从第3行开始（索引2），跳过表头和空行
                const dataLines = lines.slice(2).filter(line => line.trim() && line.includes('FZ-'));
                
                freezers = dataLines.map(line => {
                    const values = line.split(',');
                    return {
                        id: values[0]?.trim(),
                        region: getRegion(values[1]),
                        shop: values[2]?.trim(),
                        owner: values[3]?.trim(),
                        phone: values[4]?.trim(),
                        status: values[5]?.trim() || '已投放'
                    };
                }).filter(f => f.id);
                
                console.log(`✅ 已加载 ${freezers.length} 台冰柜`);
                return freezers;
            } catch (error) {
                console.error('❌ 加载失败，使用默认数据', error);
                return getDefaultFreezers();
            }
        }

        // 默认数据（备用）
        function getDefaultFreezers() {
            return [
                { id: 'FZ-001', region: 'A', shop: 'Karachi Store', owner: 'Ali', phone: '0300-1234567', status: '已投放' },
                { id: 'FZ-002', region: 'A', shop: 'Ali Mart', owner: 'Ahmed', phone: '0300-7654321', status: '已投放' },
                { id: 'FZ-003', region: 'A', shop: 'Fresh Shop', owner: 'Kamran', phone: '0300-9876543', status: '已投放' }
            ];
        }

        // ========== 登录函数 ==========
        window.handleLogin = function() {
            console.log('登录函数被调用');
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const remember = document.getElementById('remember').checked;
            
            if (users[username] && users[username].password === password) {
                currentUser = {
                    username: username,
                    role: users[username].role,
                    region: users[username].region,
                    name: users[username].name,
                    nameEn: users[username].nameEn
                };
                
                if (remember) {
                    localStorage.setItem('aice_user', JSON.stringify(currentUser));
                }
                
                // 显示主页面
                document.getElementById('loginPage').classList.add('hidden');
                document.getElementById('mainPage').classList.remove('hidden');
                
                // 更新显示
                document.getElementById('displayName').textContent = currentLang === 'zh' ? currentUser.name : currentUser.nameEn;
                document.getElementById('currentDate').textContent = new Date().toLocaleDateString(currentLang === 'zh' ? 'zh-CN' : 'en-US', { 
                    year: 'numeric', 
                    month: 'long', 
                    day: 'numeric' 
                });
                
                // 根据角色显示不同视图
                if (currentUser.role === 'sales') {
                    showSalesView();
                } else if (currentUser.role === 'office') {
                    showOfficeView();
                } else if (currentUser.role === 'boss') {
                    showBossView();
                }
                
                console.log('登录成功', currentUser);
            } else {
                alert('编号或密码错误，请使用 001-005 / 123456');
            }
        };

        // 字符计数
        document.addEventListener('input', function(e) {
            if (e.target.id === 'remarkDetail') {
                const count = e.target.value.length;
                document.getElementById('charCount').textContent = count;
            }
        });

        // ========== 语言切换 ==========
        window.switchLanguage = function(lang) {
            currentLang = lang;
            localStorage.setItem('language', lang);
            
            document.getElementById('langZhBtn').classList.toggle('active', lang === 'zh');
            document.getElementById('langEnBtn').classList.toggle('active', lang === 'en');
            
            updateUILanguage();
            
            if (currentUser) {
                if (currentUser.role === 'sales') showSalesView();
                else if (currentUser.role === 'office') showOfficeView();
                else if (currentUser.role === 'boss') showBossView();
            }
        };

        function updateUILanguage() {
            const t = translations[currentLang];
            
            const elements = {
                'usernameLabel': 'usernameLabel',
                'passwordLabel': 'passwordLabel',
                'rememberLabel': 'rememberLabel',
                'loginBtn': 'loginBtn',
                'logoutBtn': 'logoutBtn',
                'step1Title': 'step1Title',
                'step2Title': 'step2Title',
                'openCameraBtn': 'openCameraBtn',
                'uploadBtn': 'uploadBtn',
                'cancelBtn': 'cancelBtn'
            };
            
            for (let [id, key] of Object.entries(elements)) {
                const el = document.getElementById(id);
                if (el) el.textContent = t[key];
            }
            
            const cameraPreview = document.getElementById('camera-preview');
            if (cameraPreview && !cameraPreview.querySelector('img')) {
                cameraPreview.textContent = t.cameraPreview;
            }
            
            const remarkSelect = document.getElementById('remarkType');
            if (remarkSelect) {
                remarkSelect.options[0].text = t.remarkNormal;
                remarkSelect.options[1].text = t.remarkUnused;
                remarkSelect.options[2].text = t.remarkDirtyInside;
                remarkSelect.options[3].text = t.remarkOtherAd;
                remarkSelect.options[4].text = t.remarkTemperature;
                remarkSelect.options[5].text = t.remarkDamaged;
                remarkSelect.options[6].text = t.remarkOther;
            }
            
            const remarkDetail = document.getElementById('remarkDetail');
            if (remarkDetail) remarkDetail.placeholder = t.remarkDetailPlaceholder;
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

        // ========== 初始化 ==========
        window.onload = async function() {
            switchLanguage(currentLang);
            
            // 加载冰柜数据
            await loadFreezersFromSheet();
            
            const savedUser = localStorage.getItem('aice_user');
            if (savedUser) {
                currentUser = JSON.parse(savedUser);
                // 显示主页面
                document.getElementById('loginPage').classList.add('hidden');
                document.getElementById('mainPage').classList.remove('hidden');
                
                document.getElementById('displayName').textContent = currentLang === 'zh' ? currentUser.name : currentUser.nameEn;
                document.getElementById('currentDate').textContent = new Date().toLocaleDateString(currentLang === 'zh' ? 'zh-CN' : 'en-US', { 
                    year: 'numeric', 
                    month: 'long', 
                    day: 'numeric' 
                });
                
                if (currentUser.role === 'sales') {
                    showSalesView();
                } else if (currentUser.role === 'office') {
                    showOfficeView();
                } else if (currentUser.role === 'boss') {
                    showBossView();
                }
            }
        };

        window.logout = function() {
            localStorage.removeItem('aice_user');
            currentUser = null;
            document.getElementById('loginPage').classList.remove('hidden');
            document.getElementById('mainPage').classList.add('hidden');
        };

        // ========== 业务员视图 ==========
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
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            event.target.classList.add('active');
            
            if (tab === 'tasks') showSalesTasks();
            else if (tab === 'history') showSalesHistory();
            else if (tab === 'stats') showSalesStats();
        };

        function showSalesTasks() {
            const t = translations[currentLang];
            const region = currentUser.region;
            const taskIds = todayTasks[region] || [];
            const tasks = taskIds.map(id => freezers.find(f => f.id === id)).filter(f => f);
            
            let html = `
                <div class="stats-card">
                    <div class="stats-title">📋 ${t.todayTasks}</div>
                    <div class="stats-grid">
                        <div class="stat-item">
                            <div class="stat-value">${tasks.length}</div>
                            <div class="stat-label">${t.totalFreezers}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value">${tasks.filter(t => hasPhotoToday(t.id)).length}</div>
                            <div class="stat-label">${t.completed}</div>
                        </div>
                    </div>
                    <div class="progress-bar">
                        <div class="progress-fill" style="width: ${(tasks.filter(t => hasPhotoToday(t.id)).length / tasks.length * 100) || 0}%"></div>
                    </div>
                </div>
                <div class="task-list">
            `;
            
            tasks.forEach(task => {
                const photo = photos.find(p => p.freezerId === task.id && isToday(new Date(p.time)));
                html += `
                    <div class="task-item">
                        <div class="task-header">
                            <span class="freezer-id">${task.id}</span>
                            <span class="shop-name">${task.shop}</span>
                        </div>
                        <div class="shop-details">
                          店主：${task.owner} | ${task.phone}
                        </div>
                        ${photo && photo.remark ? `
                            <div class="remark-badge">${photo.remark.text}</div>
                            ${photo.remark.detail ? `<div class="remark-detail">${photo.remark.detail}</div>` : ''}
                        ` : ''}
                        <div class="task-footer">
                            <span class="time">${photo ? '✅ ' + t.completed + ' ' + formatTime(photo.time) : '⏳ ' + t.waiting}</span>
                            <button class="photo-btn ${photo ? 'completed' : ''}" onclick="openPhotoModal('${task.id}')" ${photo ? 'disabled' : ''}>
                                ${photo ? t.completed : t.photo}
                            </button>
                        </div>
                    </div>
                `;
            });
            
            html += '</div>';
            document.getElementById('content').innerHTML = html;
        }

        function showSalesHistory() {
            const t = translations[currentLang];
            const myPhotos = photos.filter(p => p.sales === currentUser.username);
            let html = '<div class="task-list">';
            
            const grouped = {};
            myPhotos.forEach(photo => {
                if (!grouped[photo.freezerId]) grouped[photo.freezerId] = [];
                grouped[photo.freezerId].push(photo);
            });
            
            for (let freezerId in grouped) {
                const freezer = freezers.find(f => f.id === freezerId);
                const photoList = grouped[freezerId].sort((a, b) => new Date(b.time) - new Date(a.time));
                html += `
                    <div class="task-item">
                        <div class="task-header">
                            <span class="freezer-id">${freezerId}</span>
                            <span class="shop-name">${freezer ? freezer.shop : ''}</span>
                        </div>
                        <div style="margin-top: 10px;">
                            <span class="badge">${photoList.length} ${t.totalFreezers}</span>
                            <span class="badge warning">${getDaysAgo(photoList[0].time)}${currentLang === 'zh' ? '天前' : 'd'}</span>
                        </div>
                        <div style="margin-top: 10px; max-height: 150px; overflow-y: auto;">
                            ${photoList.slice(0, 3).map(p => `
                                <div class="history-item">
                                    <div class="history-time">${formatDateTime(p.time)}</div>
                                    ${p.remark ? `
                                        <div class="remark-badge">${p.remark.text}</div>
                                    ` : ''}
                                </div>
                            `).join('')}
                            ${photoList.length > 3 ? `<div style="color:#999;">+${photoList.length-3}</div>` : ''}
                        </div>
                    </div>
                `;
            }
            
            html += '</div>';
            document.getElementById('content').innerHTML = html;
        }

        function showSalesStats() {
            const t = translations[currentLang];
            const region = currentUser.region;
            const regionFreezers = freezers.filter(f => f.region === region);
            const myPhotos = photos.filter(p => p.sales === currentUser.username);
            
            const thisWeek = myPhotos.filter(p => isThisWeek(new Date(p.time))).length;
            const thisMonth = myPhotos.filter(p => isThisMonth(new Date(p.time))).length;
            const today = myPhotos.filter(p => isToday(new Date(p.time))).length;
            
            const lastPhotos = {};
            regionFreezers.forEach(f => {
                const photo = photos.filter(p => p.freezerId === f.id).sort((a, b) => new Date(b.time) - new Date(a.time))[0];
                if (photo) {
                    lastPhotos[f.id] = getDaysAgo(photo.time);
                }
            });
            
            const overdue = Object.entries(lastPhotos).filter(([id, days]) => days > 7).length;
            
            let html = `
                <div class="stats-card">
                    <div class="stats-title">📊 ${t.myRecords}</div>
                    <div class="stats-grid">
                        <div class="stat-item">
                            <div class="stat-value">${today}</div>
                            <div class="stat-label">${t.todayPhotos}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value">${thisWeek}</div>
                            <div class="stat-label">${t.weekPhotos}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value">${thisMonth}</div>
                            <div class="stat-label">${t.monthPhotos}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value ${overdue > 0 ? 'warning' : ''}">${overdue}</div>
                            <div class="stat-label">${t.overdue}</div>
                        </div>
                    </div>
                </div>
            `;
            
            document.getElementById('content').innerHTML = html;
        }

        // ========== 办公室视图 ==========
        window.showOfficeView = function() {
            const t = translations[currentLang];
            document.getElementById('navBar').innerHTML = `
                <div class="nav-item active" onclick="switchOfficeTab('sync')">${t.syncTasks}</div>
                <div class="nav-item" onclick="switchOfficeTab('freezers')">${t.freezerSearch}</div>
                <div class="nav-item" onclick="switchOfficeTab('stats')">${t.regionStats}</div>
                <div class="nav-item" onclick="switchOfficeTab('alerts')">${t.alerts}</div>
            `;
            showSyncView();
        };

        window.switchOfficeTab = function(tab) {
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            event.target.classList.add('active');
            
            if (tab === 'sync') showSyncView();
            else if (tab === 'freezers') showFreezerSearch();
            else if (tab === 'stats') showRegionStats();
            else if (tab === 'alerts') showAlerts();
        };

        function showSyncView() {
            const t = translations[currentLang];
            let html = `
                <div class="sync-card">
                    <div class="stats-title">📱 ${t.syncTasks}</div>
                    <div style="color: #666; font-size: 14px; margin-bottom: 10px;">
                        ${currentLang === 'zh' ? '复制微信群消息粘贴：' : 'Copy WhatsApp message:'}
                    </div>
                    <textarea class="sync-textarea" id="syncText" placeholder="区域A：FZ-A00006, FZ-A00019..."></textarea>
                    <button class="sync-btn" onclick="syncTasks()">${t.sync}</button>
                </div>
                <div class="region-tasks">
                    <div class="stats-title">📋 ${t.todayTasks}</div>
            `;
            
            for (let region in todayTasks) {
                html += `<div class="region-title">${currentLang === 'zh' ? '区域' : 'Region'}${region} (${todayTasks[region].length})</div>`;
                todayTasks[region].forEach(id => {
                    html += `<span class="freezer-tag">${id}</span>`;
                });
            }
            html += '</div>';
            
            document.getElementById('content').innerHTML = html;
        }

        window.showFreezerSearch = function() {
            const t = translations[currentLang];
            let html = `
                <div class="search-box">
                    <input type="text" id="searchFreezer" placeholder="FZ-A00006" onkeyup="searchFreezer(event)">
                    <button class="photo-btn" onclick="searchFreezer()">${t.search}</button>
                </div>
                <div id="searchResult"></div>
            `;
            document.getElementById('content').innerHTML = html;
        };

        window.searchFreezer = function(e) {
            if (e && e.key && e.key !== 'Enter') return;
            
            const searchId = document.getElementById('searchFreezer').value.toUpperCase();
            const freezer = freezers.find(f => f.id === searchId);
            
            if (!freezer) {
                document.getElementById('searchResult').innerHTML = `
                    <div class="stats-card">
                        <div style="color:#ff4444; text-align:center;">❌ ${searchId} ${currentLang === 'zh' ? '未找到' : 'not found'}</div>
                    </div>
                `;
                return;
            }
            
            const freezerPhotos = photos.filter(p => p.freezerId === freezer.id).sort((a, b) => new Date(b.time) - new Date(a.time));
            const lastPhoto = freezerPhotos[0];
            
            document.getElementById('searchResult').innerHTML = `
                <div class="stats-card">
                    <div class="stats-title">${freezer.id} - ${freezer.shop}</div>
                    <div class="stat-row">
                        <span>${currentLang === 'zh' ? '区域' : 'Region'}</span>
                        <span class="stat-value">${freezer.region}</span>
                    </div>
                    <div class="stat-row">
                        <span>${currentLang === 'zh' ? '店主' : 'Owner'}</span>
                        <span class="stat-value">${freezer.owner}</span>
                    </div>
                    <div class="stat-row">
                        <span>${currentLang === 'zh' ? '电话' : 'Phone'}</span>
                        <span class="stat-value">${freezer.phone}</span>
                    </div>
                    <div class="stat-row">
                        <span>${currentLang === 'zh' ? '累计拍照' : 'Total'}</span>
                        <span class="stat-value">${freezerPhotos.length}</span>
                    </div>
                    ${lastPhoto ? `
                        <div class="stat-row">
                            <span>${currentLang === 'zh' ? '最后拍照' : 'Last'}</span>
                            <span class="stat-value">${formatDateTime(lastPhoto.time)}</span>
                        </div>
                    ` : ''}
                </div>
            `;
        };

        function showRegionStats() {
            const t = translations[currentLang];
            const regions = ['A', 'B', 'C'];
            
            let html = '<div class="stats-card"><div class="stats-title">📍 ' + t.regionStats + '</div><div class="region-list">';
            
            regions.forEach(region => {
                const regionFreezers = freezers.filter(f => f.region === region);
                const todayCount = photos.filter(p => regionFreezers.some(f => f.id === p.freezerId) && isToday(new Date(p.time))).length;
                const percent = Math.round(todayCount / regionFreezers.length * 100) || 0;
                
                let percentClass = 'low';
                if (percent >= 80) percentClass = 'high';
                else if (percent >= 50) percentClass = 'medium';
                
                html += `
                    <div class="region-item">
                        <div class="region-header">
                            <span class="region-name">${currentLang === 'zh' ? '区域' : 'Region'}${region}</span>
                            <div class="region-stats">
                                <span class="region-count">${todayCount}/${regionFreezers.length}</span>
                                <span class="region-percent ${percentClass}">${percent}%</span>
                            </div>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${percent}%"></div>
                        </div>
                    </div>
                `;
            });
            
            html += '</div></div>';
            document.getElementById('content').innerHTML = html;
        }

        function showAlerts() {
            const t = translations[currentLang];
            const alerts = [];
            freezers.forEach(freezer => {
                const lastPhoto = photos.filter(p => p.freezerId === freezer.id).sort((a, b) => new Date(b.time) - new Date(a.time))[0];
                const daysAgo = lastPhoto ? getDaysAgo(lastPhoto.time) : 999;
                
                if (daysAgo > 7 || !lastPhoto) {
                    alerts.push({
                        freezer: freezer,
                        daysAgo: daysAgo,
                        lastPhoto: lastPhoto
                    });
                }
            });
            
            alerts.sort((a, b) => b.daysAgo - a.daysAgo);
            
            let html = `
                <div class="stats-card">
                    <div class="stats-title">⚠️ ${t.alerts} (${alerts.length})</div>
            `;
            
            if (alerts.length === 0) {
                html += '<div style="text-align:center; padding:30px; color:#00a65a;">✅ ' + (currentLang === 'zh' ? '一切正常' : 'All good') + '</div>';
            } else {
                html += '<div class="task-list">';
                alerts.slice(0, 5).forEach(alert => {
                    const days = alert.daysAgo === 999 ? (currentLang === 'zh' ? '新冰柜' : 'New') : alert.daysAgo + (currentLang === 'zh' ? '天' : 'd');
                    html += `
                        <div class="task-item" style="border-left: 4px solid #ff4444;">
                            <div class="task-header">
                                <span class="freezer-id">${alert.freezer.id}</span>
                                <span class="shop-name">${alert.freezer.shop}</span>
                            </div>
                            <div style="color:#ff4444; font-size:13px;">⚠️ ${days} ${currentLang === 'zh' ? '未拍照' : 'no photo'}</div>
                        </div>
                    `;
                });
                html += '</div>';
                if (alerts.length > 5) {
                    html += `<div style="text-align:center; padding:10px; color:#999;">+${alerts.length-5} ${currentLang === 'zh' ? '更多' : 'more'}</div>`;
                }
            }
            
            html += '</div>';
            document.getElementById('content').innerHTML = html;
        }

        // ========== 老板视图 ==========
        window.showBossView = function() {
            const t = translations[currentLang];
            document.getElementById('navBar').innerHTML = `
                <div class="nav-item active" onclick="switchBossTab('overview')">${t.overview}</div>
                <div class="nav-item" onclick="switchBossTab('regions')">${t.regions}</div>
                <div class="nav-item" onclick="switchBossTab('sales')">${t.salesmen}</div>
                <div class="nav-item" onclick="switchBossTab('alerts')">${t.alerts}</div>
            `;
            showBossOverview();
        };

        window.switchBossTab = function(tab) {
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            event.target.classList.add('active');
            
            if (tab === 'overview') showBossOverview();
            else if (tab === 'regions') showRegionStats();
            else if (tab === 'sales') showBossSales();
            else if (tab === 'alerts') showAlerts();
        };

        function showBossOverview() {
            const t = translations[currentLang];
            
            const totalFreezers = freezers.length;
            const todayPhotos = photos.filter(p => isToday(new Date(p.time))).length;
            const weekPhotos = photos.filter(p => isThisWeek(new Date(p.time))).length;
            const monthPhotos = photos.filter(p => isThisMonth(new Date(p.time))).length;
            
            let html = `
                <div class="stats-card">
                    <div class="stats-title">📊 ${t.overview}</div>
                    <div class="stats-grid">
                        <div class="stat-item">
                            <div class="stat-value">${totalFreezers}</div>
                            <div class="stat-label">${t.totalFreezers}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value">${todayPhotos}</div>
                            <div class="stat-label">${t.todayPhotos}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value">${weekPhotos}</div>
                            <div class="stat-label">${t.weekPhotos}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value">${monthPhotos}</div>
                            <div class="stat-label">${t.monthPhotos}</div>
                        </div>
                    </div>
                </div>
            `;
            
            document.getElementById('content').innerHTML = html;
        }

        function showBossSales() {
            const t = translations[currentLang];
            const salesmen = [
                { username: '001', name: '业务员001', region: 'A' },
                { username: '002', name: '业务员002', region: 'B' },
                { username: '003', name: '业务员003', region: 'C' }
            ];
            
            let html = '<div class="stats-card"><div class="stats-title">👥 ' + t.salesmen + '</div><div class="region-list">';
            
            salesmen.forEach(s => {
                const salesPhotos = photos.filter(p => p.sales === s.username);
                const today = salesPhotos.filter(p => isToday(new Date(p.time))).length;
                const week = salesPhotos.filter(p => isThisWeek(new Date(p.time))).length;
                const month = salesPhotos.filter(p => isThisMonth(new Date(p.time))).length;
                
                html += `
                    <div class="region-item">
                        <div class="region-header">
                            <span class="region-name">${s.name}</span>
                            <span class="region-count">${t.weekPhotos} ${week}</span>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin: 5px 0; font-size:13px;">
                            <span>${t.todayPhotos}: ${today}</span>
                            <span>${t.monthPhotos}: ${month}</span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${Math.min(100, week/25*100)}%"></div>
                        </div>
                    </div>
                `;
            });
            
            html += '</div></div>';
            document.getElementById('content').innerHTML = html;
        }

        // ========== 拍照相关 ==========
        window.openPhotoModal = function(freezerId) {
            currentFreezer = freezerId;
            document.getElementById('modalFreezerId').textContent = freezerId;
            document.getElementById('photoModal').classList.remove('hidden');
            
            document.getElementById('remarkType').value = 'normal';
            document.getElementById('remarkDetail').value = '';
            document.getElementById('charCount').textContent = '0';
            
            document.getElementById('camera-preview').innerHTML = translations[currentLang].cameraPreview;
        };

        window.closePhotoModal = function() {
            document.getElementById('photoModal').classList.add('hidden');
            currentFreezer = null;
        };

        window.openCamera = function() {
            document.getElementById('camera-input').click();
        };

        document.getElementById('camera-input').addEventListener('change', function(e) {
            if (e.target.files.length > 0) {
                const file = e.target.files[0];
                const reader = new FileReader();
                reader.onload = function(e) {
                    document.getElementById('camera-preview').innerHTML = `<img src="${e.target.result}" style="width:100%;height:100%;object-fit:cover;">`;
                };
                reader.readAsDataURL(file);
            }
        });

        window.uploadPhoto = function() {
            if (!currentFreezer) return;
            
            const remarkType = document.getElementById('remarkType').value;
            const remarkDetail = document.getElementById('remarkDetail').value;
            
            const photo = {
                freezerId: currentFreezer,
                time: new Date().toISOString(),
                sales: currentUser.username,
                photo: '📸',
                remark: {
                    type: remarkType,
                    text: getRemarkText(remarkType, currentLang),
                    detail: remarkDetail
                }
            };
            
            photos.push(photo);
            localStorage.setItem('photos', JSON.stringify(photos));
            
            closePhotoModal();
            if (currentUser.role === 'sales') {
                showSalesTasks();
            }
        };

        // ========== 工具函数 ==========
        function hasPhotoToday(freezerId) {
            return photos.some(p => p.freezerId === freezerId && isToday(new Date(p.time)));
        }

        function isToday(date) {
            const today = new Date();
            return date.getDate() === today.getDate() &&
                   date.getMonth() === today.getMonth() &&
                   date.getFullYear() === today.getFullYear();
        }

        function isThisWeek(date) {
            const today = new Date();
            const weekAgo = new Date(today);
            weekAgo.setDate(weekAgo.getDate() - 7);
            return date >= weekAgo && date <= today;
        }

        function isThisMonth(date) {
            const today = new Date();
            return date.getMonth() === today.getMonth() &&
                   date.getFullYear() === today.getFullYear();
        }

        function getDaysAgo(dateStr) {
            const date = new Date(dateStr);
            const today = new Date();
            const diffTime = today - date;
            const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
            return diffDays;
        }

        function formatTime(dateStr) {
            const date = new Date(dateStr);
            return `${date.getHours().toString().padStart(2, '0')}:${date.getMinutes().toString().padStart(2, '0')}`;
        }

        function formatDateTime(dateStr) {
            const date = new Date(dateStr);
            return `${date.getFullYear()}-${(date.getMonth()+1).toString().padStart(2, '0')}-${date.getDate().toString().padStart(2, '0')}`;
        }

        // ========== 同步任务（修复正则表达式）==========
        window.syncTasks = function() {
            const text = document.getElementById('syncText').value;
            // 修复了正则表达式，移除了无效的字符类
            const regex = /区域([ABC])[：:]\s*([FZ-A\d,\s]+)/g;
            let match;
            
            while ((match = regex.exec(text)) !== null) {
                const region = match[1];
                const ids = match[2].split(/[,，\s]+/).filter(id => id.startsWith('FZ-'));
                if (ids.length > 0) {
                    todayTasks[region] = ids;
                }
            }
            
            alert(translations[currentLang].sync + ' ' + (currentLang === 'zh' ? '完成' : 'completed'));
            showSyncView();
        };
    </script>
</body>
</html>
