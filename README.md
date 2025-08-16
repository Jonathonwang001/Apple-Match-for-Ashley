# Apple-Match-for-Ashley
Creating an interesting game only for my love, Ashley. Hope her happy everyday!
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>💕 Ashley的专属苹果消消乐</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            user-select: none;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        
        .hearts-background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
        
        .heart {
            position: absolute;
            font-size: 1.5rem;
            animation: floatHeart 8s linear infinite;
            opacity: 0.6;
        }
        
        @keyframes floatHeart {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 0.6;
            }
            90% {
                opacity: 0.6;
            }
            100% {
                transform: translateY(-50px) rotate(360deg);
                opacity: 0;
            }
        }
        
        .screen {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 1rem;
            position: relative;
            z-index: 10;
        }
        
        .main-menu {
            text-align: center;
            color: white;
        }
        
        .title {
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            animation: titleGlow 2s ease-in-out infinite alternate;
        }
        
        @keyframes titleGlow {
            from { text-shadow: 2px 2px 4px rgba(0,0,0,0.3), 0 0 20px rgba(255,182,193,0.4); }
            to { text-shadow: 2px 2px 4px rgba(0,0,0,0.3), 0 0 30px rgba(255,182,193,0.8); }
        }
        
        .subtitle {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            opacity: 0.9;
        }
        
        .menu-buttons {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            min-width: 200px;
        }
        
        .menu-btn {
            padding: 1rem 2rem;
            font-size: 1.1rem;
            border: none;
            border-radius: 25px;
            background: linear-gradient(135deg, #ff6b6b, #feca57);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
        
        .menu-btn:hover, .menu-btn:active {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.3);
        }
        
        .level-select {
            display: none;
            padding: 1rem;
            max-width: 1000px;
            width: 100%;
        }
        
        .level-header {
            text-align: center;
            color: white;
            margin-bottom: 2rem;
        }
        
        .level-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }
        
        .level-button {
            padding: 1.5rem;
            border: none;
            border-radius: 15px;
            background: linear-gradient(135deg, #74b9ff, #0984e3);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
        
        .level-button.special {
            background: linear-gradient(135deg, #fd79a8, #e84393);
            animation: specialPulse 2s ease-in-out infinite alternate;
        }
        
        .level-button.practice {
            background: linear-gradient(135deg, #55a3ff, #003d82);
            border: 2px solid #ffd700;
        }
        
        @keyframes specialPulse {
            from { box-shadow: 0 4px 15px rgba(0,0,0,0.2), 0 0 20px rgba(253,121,168,0.3); }
            to { box-shadow: 0 6px 25px rgba(0,0,0,0.3), 0 0 30px rgba(253,121,168,0.6); }
        }
        
        .level-button:hover, .level-button:active {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }
        
        .love-quote {
            font-style: italic;
            font-size: 0.9rem;
            margin-top: 0.5rem;
            opacity: 0.9;
        }
        
        .game-screen {
            display: none;
            padding: 1rem;
            max-width: 600px;
            width: 100%;
        }
        
        .game-header {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 0.5rem;
            margin-bottom: 1rem;
            color: white;
        }
        
        .stat-item {
            text-align: center;
            background: rgba(255,255,255,0.1);
            padding: 0.8rem 0.5rem;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }
        
        .stat-label {
            font-size: 0.8rem;
            opacity: 0.8;
        }
        
        .stat-value {
            font-size: 1.2rem;
            font-weight: bold;
            margin-top: 0.2rem;
        }
        
        .game-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 1rem;
        }
        
        .game-grid {
            display: grid;
            grid-template-columns: repeat(8, 1fr);
            gap: 2px;
            background: rgba(255,255,255,0.1);
            padding: 8px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
            width: 100%;
            max-width: 400px;
            aspect-ratio: 1;
            position: relative;
        }
        
        .grid-cell {
            background: #ffffff;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
            touch-action: manipulation;
        }
        
        .grid-cell:hover {
            background: #f0f8ff;
        }
        
        .grid-cell.selected {
            background: #ffd700 !important;
            box-shadow: 0 0 10px rgba(255,215,0,0.6);
            transform: scale(1.05);
        }
        
        .grid-cell.special-item {
            background: linear-gradient(45deg, #ffd700, #ff6b6b);
            animation: specialGlow 2s ease-in-out infinite alternate;
        }
        
        @keyframes specialGlow {
            from { box-shadow: 0 0 10px rgba(255,215,0,0.4); }
            to { box-shadow: 0 0 20px rgba(255,215,0,0.8), 0 0 30px rgba(255,107,107,0.4); }
        }
        
        .apple-icon {
            font-size: 1.8rem;
            transition: all 0.2s ease;
        }
        
        .power-ups {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 0.5rem;
            width: 100%;
            max-width: 400px;
        }
        
        .power-up {
            background: rgba(255,255,255,0.9);
            border-radius: 10px;
            padding: 0.8rem 0.5rem;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            touch-action: manipulation;
        }
        
        .power-up:hover, .power-up:active {
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
        
        .power-up.active {
            background: #4CAF50;
            color: white;
            box-shadow: 0 0 20px rgba(76,175,80,0.5);
        }
        
        .power-up .icon {
            font-size: 1.2rem;
            margin-bottom: 0.2rem;
        }
        
        .power-up .name {
            font-size: 0.8rem;
            font-weight: bold;
            margin-bottom: 0.2rem;
        }
        
        .power-up .count {
            background: #ff6b6b;
            color: white;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.7rem;
            font-weight: bold;
            position: absolute;
            top: -5px;
            right: -5px;
        }
        
        .controls {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 0.5rem;
            width: 100%;
            max-width: 400px;
            margin-top: 1rem;
        }
        
        .control-btn {
            padding: 0.8rem 1rem;
            border: none;
            border-radius: 20px;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.3s ease;
            touch-action: manipulation;
        }
        
        .control-btn.secondary {
            background: rgba(255,255,255,0.2);
            color: white;
            border: 1px solid rgba(255,255,255,0.3);
        }
        
        .control-btn:hover, .control-btn:active {
            transform: translateY(-1px);
            box-shadow: 0 3px 10px rgba(0,0,0,0.2);
        }
        
        .pause-menu {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }
        
        .pause-content {
            background: linear-gradient(135deg, #667eea, #764ba2);
            padding: 2rem;
            border-radius: 20px;
            text-align: center;
            color: white;
            max-width: 90vw;
        }
        
        .pause-buttons {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            margin-top: 1.5rem;
        }
        
        .combo-display {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(255,107,107,0.9);
            color: white;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-weight: bold;
            font-size: 1.1rem;
            z-index: 100;
            animation: comboPop 1s ease-out forwards;
            pointer-events: none;
        }
        
        @keyframes comboPop {
            0% { transform: translate(-50%, -50%) scale(0); }
            50% { transform: translate(-50%, -50%) scale(1.2); }
            100% { transform: translate(-50%, -50%) scale(1); opacity: 0; }
        }
        
        .achievement-popup {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%) translateY(-100%);
            background: linear-gradient(135deg, #4CAF50, #45a049);
            color: white;
            padding: 1rem 2rem;
            border-radius: 25px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            z-index: 999;
            text-align: center;
            transition: transform 0.5s ease;
            max-width: 90vw;
        }
        
        .achievement-popup.show {
            transform: translateX(-50%) translateY(0);
        }
        
        @media (max-width: 480px) {
            .title {
                font-size: 2rem;
            }
            
            .game-header {
                grid-template-columns: repeat(2, 1fr);
                grid-template-rows: repeat(2, 1fr);
            }
            
            .power-ups {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .controls {
                grid-template-columns: 1fr;
            }
            
            .apple-icon {
                font-size: 1.4rem;
            }
        }
        
        /* 游戏说明弹窗样式 */
        .game-guide {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }
        
        .guide-content {
            background: linear-gradient(135deg, #667eea, #764ba2);
            padding: 2rem;
            border-radius: 20px;
            color: white;
            max-width: 90vw;
            max-height: 80vh;
            overflow-y: auto;
        }
        
        .guide-section {
            margin-bottom: 1.5rem;
        }
        
        .guide-section h3 {
            margin-bottom: 0.8rem;
            color: #ffd700;
        }
        
        .guide-item {
            display: flex;
            align-items: center;
            margin-bottom: 0.8rem;
            padding: 0.5rem;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
        }
        
        .guide-icon {
            font-size: 1.5rem;
            margin-right: 1rem;
            min-width: 40px;
            text-align: center;
        }
        
        .guide-text {
            flex: 1;
        }
        
        .guide-title {
            font-weight: bold;
            margin-bottom: 0.2rem;
        }
        
        .guide-desc {
            font-size: 0.9rem;
            opacity: 0.9;
        }
    </style>
</head>
<body>
    <!-- 爱心背景 -->
    <div class="hearts-background" id="heartsBackground"></div>
    
    <!-- 主菜单 -->
    <div class="screen main-menu" id="mainMenu">
        <h1 class="title">🍎💕 Ashley的专属苹果消消乐</h1>
        <p class="subtitle">为最美丽的你量身定制 ✨</p>
        <div class="menu-buttons">
            <button class="menu-btn" onclick="showLevelSelect()">开始游戏 🎮</button>
            <button class="menu-btn" onclick="showAchievements()">成就系统 🏆</button>
            <button class="menu-btn" onclick="showLoveMessages()">专属情话 💕</button>
            <button class="menu-btn" onclick="showSettings()">游戏说明 ⚙️</button>
        </div>
    </div>
    
    <!-- 选关界面 -->
    <div class="screen level-select" id="levelSelect">
        <div class="level-header">
            <h2 style="margin-bottom: 0.5rem;">选择关卡</h2>
            <p>每一关都有专属的爱情话语 💖</p>
            <button class="menu-btn" onclick="backToMainMenu()" style="margin: 1rem auto; display: block; max-width: 200px;">返回主菜单 ⬅️</button>
        </div>
        <div class="level-grid" id="levelGrid"></div>
    </div>
    
    <!-- 游戏界面 -->
    <div class="screen game-screen" id="gameScreen">
        <!-- 游戏状态栏 -->
        <div class="game-header">
            <div class="stat-item">
                <div class="stat-label">关卡</div>
                <div class="stat-value" id="currentLevel">1</div>
            </div>
            <div class="stat-item">
                <div class="stat-label">得分</div>
                <div class="stat-value" id="score">0</div>
            </div>
            <div class="stat-item">
                <div class="stat-label">目标</div>
                <div class="stat-value" id="target">1000</div>
            </div>
            <div class="stat-item">
                <div class="stat-label">剩余步数</div>
                <div class="stat-value" id="moves">250</div>
            </div>
        </div>
        
        <div class="game-container">
            <!-- 游戏网格 -->
            <div class="game-grid" id="gameGrid"></div>
            
            <!-- 道具栏 -->
            <div class="power-ups" id="powerUps">
                <div class="power-up" data-power="bomb">
                    <div class="icon">💥</div>
                    <div class="name">炸弹</div>
                    <div class="count">10</div>
                </div>
                <div class="power-up" data-power="lightning">
                    <div class="icon">⚡</div>
                    <div class="name">闪电</div>
                    <div class="count">10</div>
                </div>
                <div class="power-up" data-power="rainbow">
                    <div class="icon">🌈</div>
                    <div class="name">彩虹</div>
                    <div class="count">8</div>
                </div>
                <div class="power-up" data-power="hammer">
                    <div class="icon">🔨</div>
                    <div class="name">锤子</div>
                    <div class="count">15</div>
                </div>
                <div class="power-up" data-power="shuffle">
                    <div class="icon">🔄</div>
                    <div class="name">洗牌</div>
                    <div class="count">8</div>
                </div>
                <div class="power-up" data-power="time">
                    <div class="icon">⏰</div>
                    <div class="name">时光</div>
                    <div class="count">8</div>
                </div>
            </div>
            
            <!-- 控制按钮 -->
            <div class="controls">
                <button class="control-btn secondary" onclick="showGameGuide()">游戏说明 📖</button>
                <button class="control-btn secondary" onclick="showHint()">提示 💡</button>
                <button class="control-btn secondary" onclick="pauseGame()">暂停 ⏸️</button>
                <button class="control-btn secondary" onclick="restartLevel()">重新开始 🔄</button>
                <button class="control-btn secondary" onclick="backToLevelSelect()">返回选关 ⬅️</button>
            </div>
        </div>
    </div>
    
    <!-- 暂停菜单 -->
    <div class="pause-menu" id="pauseMenu">
        <div class="pause-content">
            <h3>游戏暂停</h3>
            <div class="pause-buttons">
                <button class="menu-btn" onclick="resumeGame()">继续游戏 ▶️</button>
                <button class="menu-btn" onclick="restartLevel()">重新开始 🔄</button>
                <button class="menu-btn" onclick="backToLevelSelect()">返回选关 ⬅️</button>
                <button class="menu-btn" onclick="backToMainMenu()">主菜单 🏠</button>
            </div>
        </div>
    </div>
    
    <!-- 游戏说明弹窗 -->
    <div class="game-guide" id="gameGuide">
        <div class="guide-content">
            <h2 style="text-align: center; margin-bottom: 1.5rem; color: #ffd700;">🎮 游戏说明</h2>
            
            <div class="guide-section">
                <h3>🎯 游戏目标</h3>
                <p style="margin-bottom: 1rem;">交换相邻的苹果，消除3个或更多相同的苹果来获得分数，达到目标分数即可过关！</p>
            </div>
            
            <div class="guide-section">
                <h3>🔧 道具详解</h3>
                <div class="guide-item">
                    <div class="guide-icon">💥</div>
                    <div class="guide-text">
                        <div class="guide-title">炸弹</div>
                        <div class="guide-desc">消除以点击位置为中心的3×3范围内的所有苹果</div>
                    </div>
                </div>
                <div class="guide-item">
                    <div class="guide-icon">⚡</div>
                    <div class="guide-text">
                        <div class="guide-title">闪电</div>
                        <div class="guide-desc">同时消除点击位置的整行和整列苹果</div>
                    </div>
                </div>
                <div class="guide-item">
                    <div class="guide-icon">🌈</div>
                    <div class="guide-text">
                        <div class="guide-title">彩虹</div>
                        <div class="guide-desc">消除与点击苹果相同类型的所有苹果</div>
                    </div>
                </div>
                <div class="guide-item">
                    <div class="guide-icon">🔨</div>
                    <div class="guide-text">
                        <div class="guide-title">锤子</div>
                        <div class="guide-desc">消除单个指定位置的苹果</div>
                    </div>
                </div>
                <div class="guide-item">
                    <div class="guide-icon">🔄</div>
                    <div class="guide-text">
                        <div class="guide-title">洗牌</div>
                        <div class="guide-desc">重新打乱整个棋盘的苹果排列</div>
                    </div>
                </div>
                <div class="guide-item">
                    <div class="guide-icon">⏰</div>
                    <div class="guide-text">
                        <div class="guide-title">时光</div>
                        <div class="guide-desc">增加50步额外的移动步数</div>
                    </div>
                </div>
            </div>
            
            <div class="guide-section">
                <h3>🏆 连击技巧</h3>
                <p style="margin-bottom: 1rem;">连续消除会产生连击奖励！连击越高，分数加成越多。尝试寻找连锁反应的机会，创造更高连击！</p>
            </div>
            
            <div style="text-align: center; margin-top: 2rem;">
                <button class="menu-btn" onclick="closeGameGuide()">知道了 ✅</button>
            </div>
        </div>
    </div>
    
    <!-- 成就弹窗 -->
    <div class="achievement-popup" id="achievementPopup">
        <div id="achievementText"></div>
    </div>
    
    <!-- 特殊日期效果容器 -->
    <div id="specialDateEffect" style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 999;"></div>

<script>
// 继续第二部分...
// 游戏状态
const gameState = {
    grid: [],
    score: 0,
    target: 1000,
    moves: 250,
    currentLevel: 1,
    selectedCell: null,
    isGameActive: false,
    isPaused: false,
    combo: 0,
    maxCombo: 0,
    totalMatches: 0,
    soundEnabled: true,
    activePowerUp: null,
    powerUps: {
        bomb: 10,       // 炸弹增加到10个
        lightning: 10,  // 闪电增加到10个
        rainbow: 8,     // 彩虹增加到8个
        hammer: 15,     // 锤子增加到15个
        shuffle: 8,     // 洗牌增加到8个
        time: 8         // 时光增加到8个
    },
    // 统计数据
    achievements: new Set(),
    totalScore: 0,
    gamesPlayed: 0,
    perfectGames: 0
};

// 苹果类型配置
const APPLE_TYPES = [
    { emoji: '🍎', class: 'red-apple', type: 'red' },
    { emoji: '🍏', class: 'green-apple', type: 'green' },
    { emoji: '🍊', class: 'orange-apple', type: 'orange' },
    { emoji: '🍋', class: 'yellow-apple', type: 'yellow' },
    { emoji: '🍇', class: 'purple-apple', type: 'purple' },
    { emoji: '🍑', class: 'cherry-apple', type: 'cherry' }
];

// 关卡配置（增加初始步数10倍，提高连击概率）
const LEVELS = [
    {
        id: 1,
        target: 1000,
        moves: 300,    // 从30增加到300
        quote: "就像消除这些苹果一样，我想消除你所有的烦恼 💕",
        difficulty: 'easy',
        specialApples: 0.1,
        comboBoost: 1.5    // 增加连击概率
    },
    {
        id: 2,
        target: 1500,
        moves: 350,    // 从35增加到350
        quote: "每一次匹配，都像我们心灵的契合 ✨",
        difficulty: 'easy',
        specialApples: 0.15,
        comboBoost: 1.4
    },
    {
        id: 3,
        target: 2000,
        moves: 400,    // 从40增加到400
        quote: "红苹果是我的心，绿苹果是我们的希望 🍎💚",
        difficulty: 'normal',
        special: true,
        specialApples: 0.2,
        comboBoost: 1.6
    },
    {
        id: 4,
        target: 2500,
        moves: 450,    // 从45增加到450
        quote: "就算有再多挑战，我也要和你一起闯关 💪💕",
        difficulty: 'normal',
        specialApples: 0.15,
        comboBoost: 1.3
    },
    {
        id: 5,
        target: 3000,
        moves: 500,    // 从50增加到500
        quote: "五关了呢，就像我们认识的第五个月一样美好 🌸",
        difficulty: 'normal',
        specialApples: 0.2,
        comboBoost: 1.5
    },
    {
        id: 6,
        target: 3500,
        moves: 550,    // 从55增加到550
        quote: "六六大顺，希望我们的爱情也六六大顺 🍀",
        difficulty: 'hard',
        specialApples: 0.25,
        comboBoost: 1.7
    },
    {
        id: 7,
        target: 4000,
        moves: 600,    // 从60增加到600
        quote: "第七关，像七色彩虹一样绚烂的我们 🌈",
        difficulty: 'hard',
        special: true,
        specialApples: 0.3,
        comboBoost: 1.8
    },
    {
        id: 8,
        target: 4500,
        moves: 650,    // 从65增加到650
        quote: "八这个数字多吉利，像我们的爱情一样发发发 💰💕",
        difficulty: 'hard',
        specialApples: 0.25,
        comboBoost: 1.6
    },
    {
        id: 9,
        target: 5000,
        moves: 700,    // 从70增加到700
        quote: "九关了！长长久久，我们要一直在一起 💍",
        difficulty: 'expert',
        specialApples: 0.35,
        comboBoost: 2.0    // 最高连击加成
    },
    {
        id: 10,
        target: 5500,
        moves: 750,    // 从75增加到750
        quote: "十全十美的我们，十全十美的爱情 💯💕",
        difficulty: 'expert',
        special: true,
        specialApples: 0.4,
        comboBoost: 1.9
    },
    {
        id: 11,
        target: 6000,
        moves: 800,    // 从80增加到800
        quote: "11这个数字，像两个人紧紧相依 👫💕",
        difficulty: 'expert',
        specialApples: 0.3,
        comboBoost: 1.7
    },
    {
        id: 12,
        target: 6500,
        moves: 850,    // 从85增加到850
        quote: "最后一关了！就像我们要一起走到最后一样 🌅💕",
        difficulty: 'master',
        special: true,
        specialApples: 0.5,
        comboBoost: 2.2    // 最终关卡最高加成
    }
];

// 成就系统
const ACHIEVEMENTS = [
    {
        id: 'first_match',
        name: '初次邂逅',
        desc: '完成第一次苹果消除',
        icon: '🌟'
    },
    {
        id: 'combo_master',
        name: '连击达人',
        desc: '达成10连击',
        icon: '🔥'
    },
    {
        id: 'score_hunter',
        name: '分数猎手', 
        desc: '单局得分超过5000分',
        icon: '🎯'
    },
    {
        id: 'perfect_level',
        name: '完美通关',
        desc: '剩余步数超过100步完成关卡',
        icon: '👑'
    },
    {
        id: 'power_master',
        name: '道具大师',
        desc: '使用过所有类型的道具',
        icon: '⚡'
    },
    {
        id: 'love_master',
        name: 'Ashley专属',
        desc: '完成所有特殊关卡',
        icon: '💕'
    },
    {
        id: 'ashley_special',
        name: '真爱奇迹',
        desc: 'Ashley的专属成就',
        icon: '✨'
    }
];

// 游戏初始化
function initializeGame() {
    loadGameData();
    createHeartsBackground();
    createLevelButtons();
    setupEventListeners();
    checkSpecialDate();
}

// 创建爱心背景
function createHeartsBackground() {
    const container = document.getElementById('heartsBackground');
    
    for (let i = 0; i < 15; i++) {
        const heart = document.createElement('div');
        heart.className = 'heart';
        heart.innerHTML = ['💕', '💖', '💗', '💝', '💘'][Math.floor(Math.random() * 5)];
        heart.style.left = Math.random() * 100 + '%';
        heart.style.animationDelay = Math.random() * 8 + 's';
        heart.style.animationDuration = (Math.random() * 4 + 6) + 's';
        container.appendChild(heart);
    }
}

// 创建关卡按钮
function createLevelButtons() {
    const levelGrid = document.getElementById('levelGrid');
    
    // 练习模式按钮
    const practiceButton = document.createElement('button');
    practiceButton.className = 'level-button practice';
    practiceButton.innerHTML = `
        <h3>🎯 练习模式</h3>
        <p>无限步数，随意练习</p>
        <div class="love-quote">在这里尽情享受游戏的快乐吧 😊</div>
    `;
    practiceButton.onclick = () => startLevel(0);
    levelGrid.appendChild(practiceButton);
    
    // 正常关卡按钮
    LEVELS.forEach(level => {
        const button = document.createElement('button');
        button.className = `level-button ${level.special ? 'special' : ''}`;
        button.innerHTML = `
            <h3>${level.special ? '💖' : '🍎'} 第 ${level.id} 关</h3>
            <p>目标: ${level.target} 分 | 步数: ${level.moves}</p>
            <div class="love-quote">${level.quote}</div>
        `;
        button.onclick = () => startLevel(level.id);
        levelGrid.appendChild(button);
    });
}

// 检查特殊日期
function checkSpecialDate() {
    const today = new Date();
    const month = today.getMonth() + 1;
    const date = today.getDate();
    
    // Ashley的生日 3月25日
    if (month === 3 && date === 25) {
        createBirthdayEffect();
        setTimeout(() => {
            showMessage("🎂 生日快乐，我的宝贝Ashley！这是专属于你的特殊日子！💕");
        }, 2000);
    }
    
    // 情人节 2月14日
    if (month === 2 && date === 14) {
        createValentineEffect();
        setTimeout(() => {
            showMessage("💝 情人节快乐！愿我们的爱情甜甜蜜蜜！");
        }, 2000);
    }
}

// 开始关卡
function startLevel(levelId) {
    gameState.currentLevel = levelId;
    gameState.isGameActive = true;
    gameState.isPaused = false;
    gameState.combo = 0;
    gameState.selectedCell = null;
    gameState.activePowerUp = null;
    
    if (levelId === 0) {
        // 练习模式
        gameState.score = 0;
        gameState.target = Infinity;
        gameState.moves = Infinity;
        // 练习模式道具更多
        gameState.powerUps = {
            bomb: 20,
            lightning: 20, 
            rainbow: 15,
            hammer: 25,
            shuffle: 15,
            time: 15
        };
    } else {
        // 正常关卡
        const level = LEVELS.find(l => l.id === levelId);
        gameState.score = 0;
        gameState.target = level.target;
        gameState.moves = level.moves;
        
        // 根据关卡调整道具数量
        const baseMultiplier = Math.min(1 + (levelId * 0.1), 2.5); // 最高2.5倍
        gameState.powerUps = {
            bomb: Math.floor(10 * baseMultiplier),
            lightning: Math.floor(10 * baseMultiplier),
            rainbow: Math.floor(8 * baseMultiplier),
            hammer: Math.floor(15 * baseMultiplier),
            shuffle: Math.floor(8 * baseMultiplier),
            time: Math.floor(8 * baseMultiplier)
        };
    }
    
    initializeGrid();
    showGameScreen();
    updateUI();
    
    // 显示关卡开始消息
    if (levelId > 0) {
        const level = LEVELS.find(l => l.id === levelId);
        setTimeout(() => {
            showMessage(`💖 ${level.quote}`);
        }, 500);
    } else {
        setTimeout(() => {
            showMessage("🎯 练习模式开始！尽情享受游戏乐趣吧！");
        }, 500);
    }
}

// 初始化游戏网格
function initializeGrid() {
    gameState.grid = [];
    const gameGrid = document.getElementById('gameGrid');
    gameGrid.innerHTML = '';
    
    // 创建8x8网格
    for (let row = 0; row < 8; row++) {
        gameState.grid[row] = [];
        for (let col = 0; col < 8; col++) {
            gameState.grid[row][col] = createRandomApple();
            
            const cell = document.createElement('div');
            cell.className = 'grid-cell';
            cell.dataset.row = row;
            cell.dataset.col = col;
            
            updateCellDisplay(row, col);
            setupCellInteraction(cell, row, col);
            
            gameGrid.appendChild(cell);
        }
    }
    
    // 确保没有初始匹配，并增加连击概率
    removeInitialMatches();
    enhanceComboOpportunities();
}

// 增强连击机会（新增函数）
function enhanceComboOpportunities() {
    const currentLevel = LEVELS.find(l => l.id === gameState.currentLevel);
    if (!currentLevel) return;
    
    // 根据关卡的comboBoost值创建更多连击机会
    const comboBoost = currentLevel.comboBoost || 1.0;
    const enhancedCells = Math.floor(8 * comboBoost); // 增强的格子数量
    
    for (let i = 0; i < enhancedCells; i++) {
        const row = Math.floor(Math.random() * 8);
        const col = Math.floor(Math.random() * 8);
        
        // 在随机位置放置容易产生连击的苹果组合
        if (row < 6 && col < 6) {
            const appleType = APPLE_TYPES[Math.floor(Math.random() * APPLE_TYPES.length)];
            gameState.grid[row][col] = { ...appleType };
            gameState.grid[row + 1][col] = { ...appleType };
            
            // 35%概率创建更长的连击链
            if (Math.random() < 0.35) {
                gameState.grid[row][col + 1] = { ...appleType };
            }
            
            updateCellDisplay(row, col);
            updateCellDisplay(row + 1, col);
            if (gameState.grid[row][col + 1]?.type === appleType.type) {
                updateCellDisplay(row, col + 1);
            }
        }
    }
    
    // 添加一些特殊苹果来增加连击概率
    if (Math.random() < currentLevel.specialApples) {
        addRandomSpecialItems();
    }
}

// 创建随机苹果
function createRandomApple() {
    return { ...APPLE_TYPES[Math.floor(Math.random() * APPLE_TYPES.length)] };
}

// 移除初始匹配
function removeInitialMatches() {
    let hasMatches = true;
    let attempts = 0;
    const maxAttempts = 50;
    
    while (hasMatches && attempts < maxAttempts) {
        hasMatches = false;
        
        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                if (hasMatchAtPosition(row, col)) {
                    gameState.grid[row][col] = createRandomApple();
                    hasMatches = true;
                }
            }
        }
        attempts++;
    }
    
    // 更新所有单元格显示
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            updateCellDisplay(row, col);
        }
    }
}

// 检查指定位置是否有匹配
function hasMatchAtPosition(row, col) {
    const currentType = gameState.grid[row][col]?.type;
    if (!currentType) return false;
    
    // 检查水平匹配
    let horizontalCount = 1;
    // 向左检查
    for (let c = col - 1; c >= 0 && gameState.grid[row][c]?.type === currentType; c--) {
        horizontalCount++;
    }
    // 向右检查
    for (let c = col + 1; c < 8 && gameState.grid[row][c]?.type === currentType; c++) {
        horizontalCount++;
    }
    
    // 检查垂直匹配
    let verticalCount = 1;
    // 向上检查
    for (let r = row - 1; r >= 0 && gameState.grid[r][col]?.type === currentType; r--) {
        verticalCount++;
    }
    // 向下检查
    for (let r = row + 1; r < 8 && gameState.grid[r][col]?.type === currentType; r++) {
        verticalCount++;
    }
    
    return horizontalCount >= 3 || verticalCount >= 3;
}

// 更新单元格显示
function updateCellDisplay(row, col) {
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    const apple = gameState.grid[row][col];
    
    if (cell && apple) {
        cell.innerHTML = `<span class="apple-icon">${apple.emoji}</span>`;
        cell.className = `grid-cell ${apple.class || ''}`;
    }
}

// 游戏说明相关函数
function showGameGuide() {
    document.getElementById('gameGuide').style.display = 'flex';
}

function closeGameGuide() {
    document.getElementById('gameGuide').style.display = 'none';
}

// 音效播放
gameState.playSound = function(soundType) {
    if (!this.soundEnabled) return;
    
    // 这里可以添加实际的音效播放代码
    // 由于是演示版本，暂时用console.log代替
    // console.log(`Playing sound: ${soundType}`);
};
// 设置单元格交互
function setupCellInteraction(cell, row, col) {
    let startX, startY;
    
    // 触摸开始
    cell.addEventListener('touchstart', function(e) {
        e.preventDefault();
        const touch = e.touches[0];
        startX = touch.clientX;
        startY = touch.clientY;
        
        handleCellClick(row, col);
    }, { passive: false });
    
    // 触摸移动 - 实现拖拽交换
    cell.addEventListener('touchmove', function(e) {
        e.preventDefault();
        if (!startX || !startY) return;
        
        const touch = e.touches[0];
        const deltaX = touch.clientX - startX;
        const deltaY = touch.clientY - startY;
        const minSwipeDistance = 30;
        
        if (Math.abs(deltaX) > minSwipeDistance || Math.abs(deltaY) > minSwipeDistance) {
            let targetRow = row;
            let targetCol = col;
            
            if (Math.abs(deltaX) > Math.abs(deltaY)) {
                // 水平滑动
                targetCol = deltaX > 0 ? col + 1 : col - 1;
            } else {
                // 垂直滑动
                targetRow = deltaY > 0 ? row + 1 : row - 1;
            }
            
            if (targetRow >= 0 && targetRow < 8 && targetCol >= 0 && targetCol < 8) {
                attemptSwap(row, col, targetRow, targetCol);
            }
            
            startX = null;
            startY = null;
        }
    }, { passive: false });
    
    // 点击事件（作为备用）
    cell.addEventListener('click', function(e) {
        e.preventDefault();
        handleCellClick(row, col);
    });
}

// 处理单元格点击
function handleCellClick(row, col) {
    if (!gameState.isGameActive || gameState.isPaused) return;
    
    // 如果有激活的道具，使用道具
    if (gameState.activePowerUp) {
        usePowerUp(gameState.activePowerUp, row, col);
        return;
    }
    
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    
    if (gameState.selectedCell) {
        const [selectedRow, selectedCol] = gameState.selectedCell;
        
        if (selectedRow === row && selectedCol === col) {
            // 取消选择
            deselectCell();
            return;
        }
        
        // 尝试交换
        if (isAdjacent(selectedRow, selectedCol, row, col)) {
            attemptSwap(selectedRow, selectedCol, row, col);
        } else {
            // 选择新单元格
            deselectCell();
            selectCell(row, col);
        }
    } else {
        // 选择单元格
        selectCell(row, col);
    }
}

// 选择单元格
function selectCell(row, col) {
    gameState.selectedCell = [row, col];
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    if (cell) {
        cell.classList.add('selected');
    }
}

// 取消选择
function deselectCell() {
    if (gameState.selectedCell) {
        const [row, col] = gameState.selectedCell;
        const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
        if (cell) {
            cell.classList.remove('selected');
        }
        gameState.selectedCell = null;
    }
}

// 检查两个位置是否相邻
function isAdjacent(row1, col1, row2, col2) {
    const rowDiff = Math.abs(row1 - row2);
    const colDiff = Math.abs(col1 - col2);
    return (rowDiff === 1 && colDiff === 0) || (rowDiff === 0 && colDiff === 1);
}

// 尝试交换
function attemptSwap(row1, col1, row2, col2) {
    // 临时交换
    const temp = gameState.grid[row1][col1];
    gameState.grid[row1][col1] = gameState.grid[row2][col2];
    gameState.grid[row2][col2] = temp;
    
    // 检查是否产生匹配
    const matches = findMatches();
    
    if (matches.length > 0) {
        // 有效交换
        deselectCell();
        updateCellDisplay(row1, col1);
        updateCellDisplay(row2, col2);
        
        // 添加交换动画
        animateSwap(row1, col1, row2, col2);
        
        // 消耗步数（练习模式不消耗）
        if (gameState.currentLevel > 0) {
            gameState.moves--;
        }
        
        // 处理匹配
        setTimeout(() => {
            processMatches();
        }, 300);
        
        gameState.playSound('swap');
    } else {
        // 无效交换，恢复原状
        gameState.grid[row2][col2] = gameState.grid[row1][col1];
        gameState.grid[row1][col1] = temp;
        
        // 显示无效提示
        showInvalidSwapAnimation(row1, col1, row2, col2);
        deselectCell();
    }
    
    updateUI();
}

// 交换动画
function animateSwap(row1, col1, row2, col2) {
    const cell1 = document.querySelector(`[data-row="${row1}"][data-col="${col1}"]`);
    const cell2 = document.querySelector(`[data-row="${row2}"][data-col="${col2}"]`);
    
    if (cell1 && cell2) {
        cell1.style.transform = 'scale(1.1)';
        cell2.style.transform = 'scale(1.1)';
        
        setTimeout(() => {
            cell1.style.transform = '';
            cell2.style.transform = '';
        }, 200);
    }
}

// 无效交换动画
function showInvalidSwapAnimation(row1, col1, row2, col2) {
    const cell1 = document.querySelector(`[data-row="${row1}"][data-col="${col1}"]`);
    const cell2 = document.querySelector(`[data-row="${row2}"][data-col="${col2}"]`);
    
    if (cell1 && cell2) {
        cell1.style.animation = 'shake 0.5s ease-in-out';
        cell2.style.animation = 'shake 0.5s ease-in-out';
        
        setTimeout(() => {
            cell1.style.animation = '';
            cell2.style.animation = '';
        }, 500);
    }
    
    // 添加摇摆动画CSS（如果还没有的话）
    if (!document.querySelector('#shakeAnimation')) {
        const style = document.createElement('style');
        style.id = 'shakeAnimation';
        style.textContent = `
            @keyframes shake {
                0%, 100% { transform: translateX(0); }
                25% { transform: translateX(-5px); }
                75% { transform: translateX(5px); }
            }
        `;
        document.head.appendChild(style);
    }
}

// 寻找匹配
function findMatches() {
    const matches = new Set();
    
    // 检查水平匹配
    for (let row = 0; row < 8; row++) {
        let count = 1;
        let currentType = gameState.grid[row][0]?.type;
        
        for (let col = 1; col < 8; col++) {
            if (gameState.grid[row][col]?.type === currentType && currentType) {
                count++;
            } else {
                if (count >= 3) {
                    for (let i = col - count; i < col; i++) {
                        matches.add(`${row}-${i}`);
                    }
                }
                count = 1;
                currentType = gameState.grid[row][col]?.type;
            }
        }
        
        // 检查行末尾
        if (count >= 3) {
            for (let i = 8 - count; i < 8; i++) {
                matches.add(`${row}-${i}`);
            }
        }
    }
    
    // 检查垂直匹配
    for (let col = 0; col < 8; col++) {
        let count = 1;
        let currentType = gameState.grid[0][col]?.type;
        
        for (let row = 1; row < 8; row++) {
            if (gameState.grid[row][col]?.type === currentType && currentType) {
                count++;
            } else {
                if (count >= 3) {
                    for (let i = row - count; i < row; i++) {
                        matches.add(`${i}-${col}`);
                    }
                }
                count = 1;
                currentType = gameState.grid[row][col]?.type;
            }
        }
        
        // 检查列末尾
        if (count >= 3) {
            for (let i = 8 - count; i < 8; i++) {
                matches.add(`${i}-${col}`);
            }
        }
    }
    
    return Array.from(matches).map(pos => {
        const [row, col] = pos.split('-').map(Number);
        return { row, col };
    });
}

// 处理匹配（增强连击逻辑）
async function processMatches() {
    let totalMatches = 0;
    let comboCount = 0;
    const currentLevel = LEVELS.find(l => l.id === gameState.currentLevel);
    const comboBoost = currentLevel?.comboBoost || 1.0;
    
    while (true) {
        const matches = findMatches();
        if (matches.length === 0) break;
        
        comboCount++;
        totalMatches += matches.length;
        
        // 连击加分计算（增强版）
        const baseScore = matches.length * 100;
        const comboMultiplier = Math.min(1 + (comboCount - 1) * 0.5 * comboBoost, 5.0); // 最高5倍
        const finalScore = Math.floor(baseScore * comboMultiplier);
        
        gameState.score += finalScore;
        gameState.combo = comboCount;
        gameState.totalMatches += matches.length;
        
        // 更新最大连击记录
        if (comboCount > gameState.maxCombo) {
            gameState.maxCombo = comboCount;
        }
        
        // 显示连击效果
        if (comboCount > 1) {
            showComboEffect(comboCount, finalScore);
        }
        
        // 播放音效
        if (comboCount === 1) {
            gameState.playSound('match');
        } else {
            gameState.playSound('combo');
        }
        
        // 移除匹配的苹果（带动画）
        await removeMatchedApples(matches);
        
        // 添加特殊道具生成概率（连击时）
        if (comboCount >= 3 && Math.random() < 0.3 * comboBoost) {
            await addRandomSpecialItems();
        }
        
        // 下落
        await dropApples();
        
        // 填充新苹果
        await fillEmptySpaces();
        
        // 增加额外连击机会（基于comboBoost）
        if (comboCount >= 2 && Math.random() < 0.2 * comboBoost) {
            await createRandomMatches();
        }
        
        // 短暂延迟以显示动画
        await new Promise(resolve => setTimeout(resolve, 200));
    }
    
    // 连击结束，重置连击计数器
    gameState.combo = 0;
    
    updateUI();
    checkGameStatus();
    checkAchievements();
    
    // 检查是否还有可能的移动
    if (gameState.isGameActive && !gameState.isPaused) {
        const possibleMoves = findPossibleMoves();
        if (possibleMoves.length === 0) {
            setTimeout(() => {
                showMessage("没有可行的移动了！");
                // 自动洗牌或提示使用洗牌道具
                if (gameState.powerUps.shuffle > 0) {
                    setTimeout(() => {
                        showMessage("💡 试试使用洗牌道具！");
                    }, 2000);
                }
            }, 1000);
        }
    }
}

// 创建随机匹配机会（新增函数）
async function createRandomMatches() {
    const emptyPositions = [];
    
    // 找到可以增加匹配机会的位置
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            if (col < 6) { // 水平机会
                const type1 = gameState.grid[row][col]?.type;
                const type2 = gameState.grid[row][col + 2]?.type;
                if (type1 === type2 && type1) {
                    // 在中间放置相同类型的苹果
                    gameState.grid[row][col + 1] = { ...APPLE_TYPES.find(a => a.type === type1) };
                    updateCellDisplay(row, col + 1);
                    return;
                }
            }
            
            if (row < 6) { // 垂直机会
                const type1 = gameState.grid[row][col]?.type;
                const type2 = gameState.grid[row + 2][col]?.type;
                if (type1 === type2 && type1) {
                    // 在中间放置相同类型的苹果
                    gameState.grid[row + 1][col] = { ...APPLE_TYPES.find(a => a.type === type1) };
                    updateCellDisplay(row + 1, col);
                    return;
                }
            }
        }
    }
}

// 显示连击效果
function showComboEffect(combo, score) {
    const comboDiv = document.createElement('div');
    comboDiv.className = 'combo-display';
    
    let comboText = '';
    if (combo >= 10) {
        comboText = `🔥 AMAZING ${combo}连击! +${score} 🔥`;
    } else if (combo >= 7) {
        comboText = `⚡ SUPER ${combo}连击! +${score} ⚡`;
    } else if (combo >= 5) {
        comboText = `✨ GREAT ${combo}连击! +${score} ✨`;
    } else if (combo >= 3) {
        comboText = `💫 GOOD ${combo}连击! +${score} 💫`;
    } else {
        comboText = `🌟 ${combo}连击! +${score} 🌟`;
    }
    
    comboDiv.textContent = comboText;
    
    const gameGrid = document.getElementById('gameGrid');
    gameGrid.appendChild(comboDiv);
    
    setTimeout(() => {
        comboDiv.remove();
    }, 1000);
}

// 移除匹配的苹果
async function removeMatchedApples(matches) {
    // 添加消除动画
    matches.forEach(match => {
        const cell = document.querySelector(`[data-row="${match.row}"][data-col="${match.col}"]`);
        if (cell) {
            cell.style.animation = 'fadeOut 0.3s ease-out forwards';
        }
    });
    
    // 等待动画完成
    await new Promise(resolve => setTimeout(resolve, 300));
    
    // 移除苹果
    matches.forEach(match => {
        gameState.grid[match.row][match.col] = null;
        updateCellDisplay(match.row, match.col);
    });
    
    // 添加消除动画的CSS
    if (!document.querySelector('#fadeOutAnimation')) {
        const style = document.createElement('style');
        style.id = 'fadeOutAnimation';
        style.textContent = `
            @keyframes fadeOut {
                0% { transform: scale(1); opacity: 1; }
                100% { transform: scale(0.8); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
    }
}
// 道具相关功能
function setupPowerUpButtons() {
    document.querySelectorAll('.power-up').forEach(button => {
        button.addEventListener('click', function() {
            const powerType = this.dataset.power;
            selectPowerUp(powerType);
        });
    });
}

// 选择道具
function selectPowerUp(powerType) {
    if (!gameState.isGameActive || gameState.isPaused) return;
    
    if (gameState.powerUps[powerType] <= 0) {
        showMessage('❌ 道具数量不足！');
        return;
    }
    
    // 取消之前的道具选择
    document.querySelectorAll('.power-up').forEach(btn => {
        btn.classList.remove('active');
    });
    
    if (gameState.activePowerUp === powerType) {
        // 取消选择
        gameState.activePowerUp = null;
        showMessage('取消道具选择');
    } else {
        // 选择新道具
        gameState.activePowerUp = powerType;
        const button = document.querySelector(`[data-power="${powerType}"]`);
        if (button) {
            button.classList.add('active');
        }
        
        const powerNames = {
            bomb: '💥 炸弹',
            lightning: '⚡ 闪电', 
            rainbow: '🌈 彩虹',
            hammer: '🔨 锤子',
            shuffle: '🔄 洗牌',
            time: '⏰ 时光'
        };
        
        showMessage(`已选择道具：${powerNames[powerType]}`);
        
        // 洗牌和时光道具直接使用
        if (powerType === 'shuffle') {
            usePowerUp('shuffle', 0, 0);
        } else if (powerType === 'time') {
            usePowerUp('time', 0, 0);
        }
    }
}

// 使用道具
function usePowerUp(powerType, row, col) {
    if (gameState.powerUps[powerType] <= 0) {
        showMessage('❌ 道具数量不足！');
        return;
    }
    
    // 消耗道具
    gameState.powerUps[powerType]--;
    gameState.activePowerUp = null;
    
    // 取消所有道具的激活状态
    document.querySelectorAll('.power-up').forEach(btn => {
        btn.classList.remove('active');
    });
    
    switch (powerType) {
        case 'bomb':
            useBomb(row, col);
            break;
        case 'lightning':
            useLightning(row, col);
            break;
        case 'rainbow':
            useRainbow(row, col);
            break;
        case 'hammer':
            useHammer(row, col);
            break;
        case 'shuffle':
            useShuffle();
            break;
        case 'time':
            useTime();
            break;
    }
    
    updatePowerUpUI();
    gameState.playSound('powerUp');
    checkAchievements();
}

// 炸弹道具 - 消除3x3范围
function useBomb(centerRow, centerCol) {
    const affectedCells = [];
    
    for (let row = Math.max(0, centerRow - 1); row <= Math.min(7, centerRow + 1); row++) {
        for (let col = Math.max(0, centerCol - 1); col <= Math.min(7, centerCol + 1); col++) {
            if (gameState.grid[row][col]) {
                affectedCells.push({ row, col });
            }
        }
    }
    
    // 爆炸动画
    showExplosionEffect(centerRow, centerCol);
    
    setTimeout(() => {
        const score = affectedCells.length * 150; // 炸弹分数更高
        gameState.score += score;
        
        affectedCells.forEach(({row, col}) => {
            gameState.grid[row][col] = null;
            updateCellDisplay(row, col);
        });
        
        showMessage(`💥 炸弹爆炸！获得 ${score} 分！`);
        
        setTimeout(() => {
            processAfterPowerUp();
        }, 500);
    }, 600);
}

// 闪电道具 - 消除整行整列
function useLightning(row, col) {
    const affectedCells = [];
    
    // 收集整行
    for (let c = 0; c < 8; c++) {
        if (gameState.grid[row][c]) {
            affectedCells.push({ row, col: c });
        }
    }
    
    // 收集整列
    for (let r = 0; r < 8; r++) {
        if (gameState.grid[r][col] && !affectedCells.some(cell => cell.row === r && cell.col === col)) {
            affectedCells.push({ row: r, col });
        }
    }
    
    // 闪电动画
    showLightningEffect(row, col);
    
    setTimeout(() => {
        const score = affectedCells.length * 120;
        gameState.score += score;
        
        affectedCells.forEach(({row, col}) => {
            gameState.grid[row][col] = null;
            updateCellDisplay(row, col);
        });
        
        showMessage(`⚡ 闪电一击！获得 ${score} 分！`);
        
        setTimeout(() => {
            processAfterPowerUp();
        }, 500);
    }, 800);
}

// 彩虹道具 - 消除所有相同类型
function useRainbow(row, col) {
    const targetType = gameState.grid[row][col]?.type;
    if (!targetType) {
        showMessage('❌ 请选择有效的苹果！');
        gameState.powerUps.rainbow++; // 退还道具
        updatePowerUpUI();
        return;
    }
    
    const affectedCells = [];
    for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
            if (gameState.grid[r][c]?.type === targetType) {
                affectedCells.push({ row: r, col: c });
            }
        }
    }
    
    // 彩虹动画
    showRainbowEffect();
    
    setTimeout(() => {
        const score = affectedCells.length * 200; // 彩虹分数最高
        gameState.score += score;
        
        affectedCells.forEach(({row, col}) => {
            gameState.grid[row][col] = null;
            updateCellDisplay(row, col);
        });
        
        showMessage(`🌈 彩虹消除！获得 ${score} 分！`);
        
        setTimeout(() => {
            processAfterPowerUp();
        }, 500);
    }, 1000);
}

// 锤子道具 - 消除单个苹果
function useHammer(row, col) {
    if (!gameState.grid[row][col]) {
        showMessage('❌ 请选择有效的苹果！');
        gameState.powerUps.hammer++; // 退还道具
        updatePowerUpUI();
        return;
    }
    
    // 锤击动画
    showHammerEffect(row, col);
    
    setTimeout(() => {
        gameState.score += 100;
        gameState.grid[row][col] = null;
        updateCellDisplay(row, col);
        
        showMessage('🔨 精准打击！获得 100 分！');
        
        setTimeout(() => {
            processAfterPowerUp();
        }, 300);
    }, 400);
}

// 洗牌道具 - 重新排列
function useShuffle() {
    // 洗牌动画
    showShuffleEffect();
    
    setTimeout(() => {
        const allApples = [];
        
        // 收集所有苹果
        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                if (gameState.grid[row][col]) {
                    allApples.push(gameState.grid[row][col]);
                }
            }
        }
        
        // 洗牌
        for (let i = allApples.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [allApples[i], allApples[j]] = [allApples[j], allApples[i]];
        }
        
        // 重新放置
        let index = 0;
        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                if (index < allApples.length) {
                    gameState.grid[row][col] = allApples[index++];
                    updateCellDisplay(row, col);
                }
            }
        }
        
        // 确保洗牌后没有初始匹配
        removeInitialMatches();
        // 增加连击机会
        enhanceComboOpportunities();
        
        showMessage('🔄 棋盘洗牌完成！');
        
        setTimeout(() => {
            // 检查洗牌后是否产生了匹配
            const matches = findMatches();
            if (matches.length > 0) {
                processMatches();
            }
        }, 500);
    }, 1000);
}

// 时光道具 - 增加步数（修改为增加50步）
function useTime() {
    if (gameState.currentLevel === 0) {
        showMessage('⏰ 练习模式已经是无限步数了！');
        gameState.powerUps.time++; // 退还道具
        updatePowerUpUI();
        return;
    }
    
    const addedMoves = 50; // 从5步增加到50步
    gameState.moves += addedMoves;
    
    // 时光动画
    showTimeEffect();
    
    showMessage(`⏰ 时光倒流！增加 ${addedMoves} 步！`);
    updateUI();
}

// 道具使用后的处理
async function processAfterPowerUp() {
    await dropApples();
    await fillEmptySpaces();
    
    // 检查是否产生新的匹配
    const matches = findMatches();
    if (matches.length > 0) {
        setTimeout(() => {
            processMatches();
        }, 300);
    } else {
        updateUI();
    }
}

// 苹果下落
async function dropApples() {
    let needsDrop = true;
    
    while (needsDrop) {
        needsDrop = false;
        
        for (let col = 0; col < 8; col++) {
            for (let row = 7; row >= 0; row--) {
                if (!gameState.grid[row][col]) {
                    // 找到上面的苹果
                    for (let r = row - 1; r >= 0; r--) {
                        if (gameState.grid[r][col]) {
                            gameState.grid[row][col] = gameState.grid[r][col];
                            gameState.grid[r][col] = null;
                            needsDrop = true;
                            break;
                        }
                    }
                }
            }
        }
        
        // 更新显示
        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                updateCellDisplay(row, col);
            }
        }
        
        if (needsDrop) {
            await new Promise(resolve => setTimeout(resolve, 150));
        }
    }
}

// 填充空格
async function fillEmptySpaces() {
    for (let col = 0; col < 8; col++) {
        for (let row = 0; row < 8; row++) {
            if (!gameState.grid[row][col]) {
                gameState.grid[row][col] = createRandomApple();
                updateCellDisplay(row, col);
                
                // 添加下落动画
                const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
                if (cell) {
                    cell.style.animation = 'dropIn 0.3s ease-out';
                    setTimeout(() => {
                        cell.style.animation = '';
                    }, 300);
                }
                
                await new Promise(resolve => setTimeout(resolve, 50));
            }
        }
    }
    
    // 添加下落动画CSS
    if (!document.querySelector('#dropInAnimation')) {
        const style = document.createElement('style');
        style.id = 'dropInAnimation';
        style.textContent = `
            @keyframes dropIn {
                0% { transform: translateY(-20px); opacity: 0; }
                100% { transform: translateY(0); opacity: 1; }
            }
        `;
        document.head.appendChild(style);
    }
}

// 添加随机特殊道具（增强连击概率）
async function addRandomSpecialItems() {
    const specialCount = Math.floor(Math.random() * 3) + 1; // 1-3个特殊道具
    
    for (let i = 0; i < specialCount; i++) {
        const emptyPositions = [];
        
        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                if (gameState.grid[row][col]) {
                    emptyPositions.push({ row, col });
                }
            }
        }
        
        if (emptyPositions.length > 0) {
            const randomPos = emptyPositions[Math.floor(Math.random() * emptyPositions.length)];
            const cell = document.querySelector(`[data-row="${randomPos.row}"][data-col="${randomPos.col}"]`);
            
            if (cell) {
                cell.classList.add('special-item');
                
                // 特殊效果：这个位置的苹果更容易产生连击
                const currentApple = gameState.grid[randomPos.row][randomPos.col];
                currentApple.special = true;
                currentApple.comboBonus = 2.0; // 连击加成
            }
        }
    }
}

// 特效动画函数
function showExplosionEffect(centerRow, centerCol) {
    const cell = document.querySelector(`[data-row="${centerRow}"][data-col="${centerCol}"]`);
    if (!cell) return;
    
    const explosion = document.createElement('div');
    explosion.style.cssText = `
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 3rem;
        z-index: 100;
        animation: explode 0.6s ease-out forwards;
        pointer-events: none;
    `;
    explosion.textContent = '💥';
    
    cell.style.position = 'relative';
    cell.appendChild(explosion);
    
    // 添加爆炸动画CSS
    if (!document.querySelector('#explodeAnimation')) {
        const style = document.createElement('style');
        style.id = 'explodeAnimation';
        style.textContent = `
            @keyframes explode {
                0% { transform: translate(-50%, -50%) scale(0.5); opacity: 1; }
                50% { transform: translate(-50%, -50%) scale(2); opacity: 1; }
                100% { transform: translate(-50%, -50%) scale(3); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => {
        explosion.remove();
    }, 600);
}

function showLightningEffect(row, col) {
    const gameGrid = document.getElementById('gameGrid');
    
    // 创建闪电效果
    const lightning = document.createElement('div');
    lightning.style.cssText = `
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: linear-gradient(45deg, transparent 45%, #fff3cd 50%, transparent 55%);
        z-index: 99;
        animation: lightning 0.8s ease-out forwards;
        pointer-events: none;
    `;
    
    gameGrid.style.position = 'relative';
    gameGrid.appendChild(lightning);
    
    // 添加闪电动画CSS
    if (!document.querySelector('#lightningAnimation')) {
        const style = document.createElement('style');
        style.id = 'lightningAnimation';
        style.textContent = `
            @keyframes lightning {
                0%, 100% { opacity: 0; }
                10%, 20%, 30% { opacity: 1; }
                15%, 25% { opacity: 0.5; }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => {
        lightning.remove();
    }, 800);
}

function showRainbowEffect() {
    const gameGrid = document.getElementById('gameGrid');
    
    const rainbow = document.createElement('div');
    rainbow.style.cssText = `
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: linear-gradient(45deg, 
            #ff0000 0%, #ff8000 14%, #ffff00 28%, 
            #80ff00 42%, #00ff00 57%, #00ff80 71%, 
            #00ffff 85%, #0080ff 100%);
        opacity: 0.3;
        z-index: 99;
        animation: rainbow 1s ease-in-out forwards;
        pointer-events: none;
    `;
    
    gameGrid.appendChild(rainbow);
    
    // 添加彩虹动画CSS
    if (!document.querySelector('#rainbowAnimation')) {
        const style = document.createElement('style');
        style.id = 'rainbowAnimation';
        style.textContent = `
            @keyframes rainbow {
                0% { opacity: 0; transform: scale(0); }
                50% { opacity: 0.6; transform: scale(1.1); }
                100% { opacity: 0; transform: scale(1.2); }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => {
        rainbow.remove();
    }, 1000);
}

function showHammerEffect(row, col) {
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    if (!cell) return;
    
    const hammer = document.createElement('div');
    hammer.style.cssText = `
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 2rem;
        z-index: 100;
        animation: hammer 0.4s ease-out forwards;
        pointer-events: none;
    `;
    hammer.textContent = '🔨';
    
    cell.style.position = 'relative';
    cell.appendChild(hammer);
    
    // 添加锤击动画CSS
    if (!document.querySelector('#hammerAnimation')) {
        const style = document.createElement('style');
        style.id = 'hammerAnimation';
        style.textContent = `
            @keyframes hammer {
                0% { transform: translate(-50%, -100%) rotate(-45deg); }
                50% { transform: translate(-50%, -50%) rotate(0deg); }
                100% { transform: translate(-50%, -50%) rotate(0deg) scale(1.5); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => {
        hammer.remove();
    }, 400);
}

function showShuffleEffect() {
    const gameGrid = document.getElementById('gameGrid');
    
    gameGrid.style.animation = 'shuffle 1s ease-in-out';
    
    // 添加洗牌动画CSS
    if (!document.querySelector('#shuffleAnimation')) {
        const style = document.createElement('style');
        style.id = 'shuffleAnimation';
        style.textContent = `
            @keyframes shuffle {
                0%, 100% { transform: rotate(0deg); }
                25% { transform: rotate(2deg); }
                75% { transform: rotate(-2deg); }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => {
        gameGrid.style.animation = '';
    }, 1000);
}

function showTimeEffect() {
    const gameGrid = document.getElementById('gameGrid');
    
    const timeEffect = document.createElement('div');
    timeEffect.style.cssText = `
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 4rem;
        color: #ffd700;
        z-index: 100;
        animation: timeReverse 2s ease-out forwards;
        pointer-events: none;
        text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
    `;
    timeEffect.textContent = '⏰';
    
    gameGrid.style.position = 'relative';
    gameGrid.appendChild(timeEffect);
    
    // 添加时光动画CSS
    if (!document.querySelector('#timeAnimation')) {
        const style = document.createElement('style');
        style.id = 'timeAnimation';
        style.textContent = `
            @keyframes timeReverse {
                0% { transform: translate(-50%, -50%) scale(0) rotate(0deg); opacity: 1; }
                50% { transform: translate(-50%, -50%) scale(1.5) rotate(180deg); opacity: 1; }
                100% { transform: translate(-50%, -50%) scale(2) rotate(360deg); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => {
        timeEffect.remove();
    }, 2000);
}

// 更新道具UI
function updatePowerUpUI() {
    Object.keys(gameState.powerUps).forEach(powerType => {
        const button = document.querySelector(`[data-power="${powerType}"]`);
        if (button) {
            const countElement = button.querySelector('.count');
            if (countElement) {
                countElement.textContent = gameState.powerUps[powerType];
                
                // 道具不足时的视觉提示
                if (gameState.powerUps[powerType] <= 0) {
                    button.style.opacity = '0.5';
                    countElement.style.backgroundColor = '#999';
                } else {
                    button.style.opacity = '1';
                    countElement.style.backgroundColor = '#ff6b6b';
                }
            }
        }
    });
}

// 初始化道具系统
function initializePowerUps() {
    setupPowerUpButtons();
    updatePowerUpUI();
}
// 下一关
function nextLevel() {
    if (gameState.currentLevel < LEVELS.length) {
        startLevel(gameState.currentLevel + 1);
    } else {
        backToLevelSelect();
        showMessage('🎉 恭喜完成所有关卡！');
    }
}

// 检查游戏状态
function checkGameStatus() {
    if (gameState.currentLevel === 0) return; // 练习模式不检查状态
    
    // 检查是否达成目标
    if (gameState.score >= gameState.target) {
        gameState.isGameActive = false;
        gameState.gamesPlayed++;
        gameState.totalScore += gameState.score;
        
        // 检查完美通关
        if (gameState.moves >= 100) {
            gameState.perfectGames++;
        }
        
        showLevelCompleteDialog();
    } else if (gameState.moves <= 0) {
        // 步数用完
        gameState.isGameActive = false;
        showGameOverDialog();
    }
}

// 显示过关对话框
function showLevelCompleteDialog() {
    const level = LEVELS.find(l => l.id === gameState.currentLevel);
    let message = `🎉 第${gameState.currentLevel}关完成！\n\n`;
    message += `最终得分: ${gameState.score}\n`;
    message += `剩余步数: ${gameState.moves}\n`;
    
    if (gameState.moves >= 100) {
        message += `\n👑 完美通关奖励！`;
    }
    
    if (gameState.maxCombo >= 5) {
        message += `\n🔥 最高连击: ${gameState.maxCombo}`;
    }
    
    message += `\n\n💕 ${level?.quote || ''}`;
    
    setTimeout(() => {
        if (confirm(message + '\n\n继续下一关？')) {
            nextLevel();
        } else {
            backToLevelSelect();
        }
    }, 1000);
}

// 显示游戏结束对话框
function showGameOverDialog() {
    let message = `😔 游戏结束\n\n`;
    message += `当前得分: ${gameState.score}\n`;
    message += `目标分数: ${gameState.target}\n`;
    message += `差距: ${gameState.target - gameState.score}\n\n`;
    message += `不要气馁，再来一次吧！💪`;
    
    setTimeout(() => {
        if (confirm(message + '\n\n重新开始这一关？')) {
            restartLevel();
        } else {
            backToLevelSelect();
        }
    }, 1000);
}

// 成就系统
function checkAchievements() {
    const newAchievements = [];
    
    // 检查各种成就条件
    if (gameState.totalMatches >= 1 && !gameState.achievements.has('first_match')) {
        newAchievements.push('first_match');
    }
    
    if (gameState.maxCombo >= 10 && !gameState.achievements.has('combo_master')) {
        newAchievements.push('combo_master');
    }
    
    if (gameState.score >= 5000 && !gameState.achievements.has('score_hunter')) {
        newAchievements.push('score_hunter');
    }
    
    if (gameState.moves >= 100 && gameState.score >= gameState.target && !gameState.achievements.has('perfect_level')) {
        newAchievements.push('perfect_level');
    }
    
    // 检查是否使用过所有道具
    const usedAllPowerUps = Object.entries(gameState.powerUps).every(([key, count]) => {
        const initialCounts = {
            bomb: 10, lightning: 10, rainbow: 8, hammer: 15, shuffle: 8, time: 8
        };
        return count < initialCounts[key];
    });
    if (usedAllPowerUps && !gameState.achievements.has('power_master')) {
        newAchievements.push('power_master');
    }
    
    // 特殊成就 - Ashley专属
    const completedSpecialLevels = LEVELS.filter(l => l.special).every(level => 
        gameState.currentLevel >= level.id
    );
    if (completedSpecialLevels && !gameState.achievements.has('love_master')) {
        newAchievements.push('love_master');
    }
    
    // 显示新获得的成就
    newAchievements.forEach((achievementId, index) => {
        gameState.achievements.add(achievementId);
        const achievement = ACHIEVEMENTS.find(a => a.id === achievementId);
        if (achievement) {
            setTimeout(() => {
                showAchievement(achievement);
            }, index * 2000 + Math.random() * 1000);
        }
    });
    
    if (newAchievements.length > 0) {
        saveGameData();
    }
}

// 显示成就弹窗
function showAchievement(achievement) {
    const popup = document.getElementById('achievementPopup');
    const text = document.getElementById('achievementText');
    
    text.innerHTML = `
        <div style="font-size: 1.5rem; margin-bottom: 0.5rem;">${achievement.icon}</div>
        <div style="font-weight: bold; margin-bottom: 0.2rem;">${achievement.name}</div>
        <div style="font-size: 0.9rem;">${achievement.desc}</div>
    `;
    
    popup.classList.add('show');
    gameState.playSound('achievement');
    
    setTimeout(() => {
        popup.classList.remove('show');
    }, 3000);
}

// 显示成就页面
function showAchievements() {
    let html = `
        <div class="pause-content" style="max-height: 80vh; overflow-y: auto;">
            <h2 style="margin-bottom: 1.5rem; color: #ffd700;">🏆 成就系统</h2>
            <div style="text-align: left;">
    `;
    
    ACHIEVEMENTS.forEach(achievement => {
        const unlocked = gameState.achievements.has(achievement.id);
        html += `
            <div style="display: flex; align-items: center; padding: 1rem; margin-bottom: 0.8rem; 
                 background: ${unlocked ? 'rgba(76, 175, 80, 0.2)' : 'rgba(255,255,255,0.1)'}; 
                 border-radius: 10px; border-left: 4px solid ${unlocked ? '#4CAF50' : '#666'};">
                <div style="font-size: 2rem; margin-right: 1rem; filter: ${unlocked ? 'none' : 'grayscale(1)'};">
                    ${achievement.icon}
                </div>
                <div>
                    <div style="font-weight: bold; margin-bottom: 0.3rem; color: ${unlocked ? '#4CAF50' : '#999'};">
                        ${achievement.name} ${unlocked ? '✅' : '🔒'}
                    </div>
                    <div style="font-size: 0.9rem; opacity: 0.9;">${achievement.desc}</div>
                </div>
            </div>
        `;
    });
    
    html += `
            </div>
            <div style="margin-top: 2rem; padding: 1rem; background: rgba(255,255,255,0.1); border-radius: 10px;">
                <h3 style="margin-bottom: 0.8rem;">🎮 游戏统计</h3>
                <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 1rem; text-align: center;">
                    <div>
                        <div style="font-size: 1.5rem; font-weight: bold; color: #4CAF50;">${gameState.gamesPlayed}</div>
                        <div style="font-size: 0.8rem;">游戏场次</div>
                    </div>
                    <div>
                        <div style="font-size: 1.5rem; font-weight: bold; color: #2196F3;">${gameState.totalScore.toLocaleString()}</div>
                        <div style="font-size: 0.8rem;">累计得分</div>
                    </div>
                    <div>
                        <div style="font-size: 1.5rem; font-weight: bold; color: #FF9800;">${gameState.maxCombo}</div>
                        <div style="font-size: 0.8rem;">最高连击</div>
                    </div>
                    <div>
                        <div style="font-size: 1.5rem; font-weight: bold; color: #9C27B0;">${gameState.perfectGames}</div>
                        <div style="font-size: 0.8rem;">完美通关</div>
                    </div>
                </div>
            </div>
            <button class="menu-btn" onclick="closePauseMenu(); showScreen('mainMenu');" style="margin-top: 1.5rem;">
                返回主菜单 🏠
            </button>
        </div>
    `;
    
    document.getElementById('pauseMenu').innerHTML = html;
    document.getElementById('pauseMenu').style.display = 'flex';
}

// 显示专属情话页面
function showLoveMessages() {
    const loveMessages = [
        "亲爱的Ashley，你就像这游戏中的彩虹道具，能消除我心中所有的烦恼 🌈💕",
        "每一次苹果的匹配，都像我们心灵的契合，那么完美，那么甜蜜 🍎💖",
        "就像游戏中的连击一样，我对你的爱也是连绵不断，永不停歇 🔥💝",
        "你是我的限定版道具，独一无二，珍贵无比 ✨👑",
        "愿我们的爱情像这游戏一样，充满惊喜，充满快乐 🎮💕",
        "每当看到你的笑容，就像获得了无限的道具，什么困难都能克服 💪❤️",
        "你是我生命中最特别的苹果，甜蜜、珍贵、不可替代 🍎👸",
        "跟你在一起的每一天，都像通关一样充满成就感 🏆💕",
        "你就是我的专属成就，最珍贵的那一个 🌟💖",
        "我愿意为你消除所有的障碍，就像这游戏中的道具一样 🔨💝"
    ];
    
    let html = `
        <div class="pause-content" style="max-height: 80vh; overflow-y: auto;">
            <h2 style="margin-bottom: 1.5rem; color: #ffd700;">💕 专属情话</h2>
            <div style="text-align: left;">
    `;
    
    loveMessages.forEach((message, index) => {
        html += `
            <div style="padding: 1.5rem; margin-bottom: 1rem; background: linear-gradient(135deg, rgba(255,182,193,0.3), rgba(255,160,122,0.3)); 
                 border-radius: 15px; border-left: 4px solid #ff6b6b;">
                <div style="font-size: 0.9rem; margin-bottom: 0.5rem; color: #666;">情话 ${index + 1}</div>
                <div style="font-size: 1rem; line-height: 1.5; color: #333;">${message}</div>
            </div>
        `;
    });
    
    html += `
            </div>
            <div style="text-align: center; margin-top: 2rem; padding: 1.5rem; background: rgba(255,255,255,0.1); border-radius: 15px;">
                <div style="font-size: 1.2rem; margin-bottom: 0.5rem;">💖</div>
                <div style="font-style: italic; color: #ffd700;">
                    "这些都是为你专门写的小情话<br>
                    希望每一句都能温暖你的心 ☀️"
                </div>
            </div>
            <button class="menu-btn" onclick="closePauseMenu(); showScreen('mainMenu');" style="margin-top: 1.5rem;">
                返回主菜单 🏠
            </button>
        </div>
    `;
    
    document.getElementById('pauseMenu').innerHTML = html;
    document.getElementById('pauseMenu').style.display = 'flex';
}

// 显示设置页面
function showSettings() {
    let html = `
        <div class="pause-content">
            <h2 style="margin-bottom: 1.5rem; color: #ffd700;">⚙️ 游戏设置</h2>
            
            <div style="text-align: left; margin-bottom: 2rem;">
                <div style="display: flex; justify-content: space-between; align-items: center; 
                     padding: 1rem; margin-bottom: 1rem; background: rgba(255,255,255,0.1); border-radius: 10px;">
                    <span>🔊 音效</span>
                    <button onclick="toggleSound()" class="menu-btn" style="padding: 0.5rem 1rem; margin: 0;">
                        ${gameState.soundEnabled ? '开启 ✅' : '关闭 ❌'}
                    </button>
                </div>
                
                <div style="display: flex; justify-content: space-between; align-items: center; 
                     padding: 1rem; margin-bottom: 1rem; background: rgba(255,255,255,0.1); border-radius: 10px;">
                    <span>📊 清除数据</span>
                    <button onclick="clearGameData()" class="menu-btn" style="padding: 0.5rem 1rem; margin: 0; background: #ff6b6b;">
                        清除 🗑️
                    </button>
                </div>
            </div>
            
            <div style="margin-bottom: 2rem; padding: 1rem; background: rgba(255,255,255,0.1); border-radius: 10px;">
                <h3 style="margin-bottom: 1rem;">❤️ 关于游戏</h3>
                <p style="font-size: 0.9rem; line-height: 1.5; margin-bottom: 1rem;">
                    这是专门为Ashley定制的苹果消消乐游戏，每一个细节都充满了爱意。
                    希望你能在游戏中感受到满满的爱和快乐！
                </p>
                <div style="text-align: center; font-size: 0.8rem; color: #ffd700;">
                    💕 Version 2.0 - Enhanced Edition 💕
                </div>
            </div>
            
            <button class="menu-btn" onclick="closePauseMenu(); showScreen('mainMenu');">
                返回主菜单 🏠
            </button>
        </div>
    `;
    
    document.getElementById('pauseMenu').innerHTML = html;
    document.getElementById('pauseMenu').style.display = 'flex';
}

// 音效开关
function toggleSound() {
    gameState.soundEnabled = !gameState.soundEnabled;
    saveGameData();
    showSettings(); // 刷新设置页面
    
    showMessage(gameState.soundEnabled ? '🔊 音效已开启' : '🔇 音效已关闭');
}

// 清除游戏数据
function clearGameData() {
    if (confirm('⚠️ 确定要清除所有游戏数据吗？\n这将删除所有成就和统计数据！')) {
        localStorage.removeItem('ashleyAppleGameData');
        
        // 重置游戏状态
        gameState.achievements.clear();
        gameState.totalScore = 0;
        gameState.gamesPlayed = 0;
        gameState.perfectGames = 0;
        gameState.maxCombo = 0;
        
        showMessage('🗑️ 游戏数据已清除');
        showSettings(); // 刷新设置页面
    }
}

// 界面控制函数
function showScreen(screenName) {
    document.querySelectorAll('.screen').forEach(screen => {
        screen.style.display = 'none';
    });
    document.getElementById(screenName).style.display = 'flex';
}

function showGameScreen() {
    showScreen('gameScreen');
}

function showLevelSelect() {
    showScreen('levelSelect');
}

function backToMainMenu() {
    gameState.isGameActive = false;
    gameState.isPaused = false;
    closePauseMenu();
    showScreen('mainMenu');
}

function backToLevelSelect() {
    gameState.isGameActive = false;
    gameState.isPaused = false;
    closePauseMenu();
    showScreen('levelSelect');
}

// 游戏控制函数
function pauseGame() {
    if (!gameState.isGameActive) return;
    
    gameState.isPaused = true;
    showPauseMenu();
}

function resumeGame() {
    gameState.isPaused = false;
    closePauseMenu();
}

function showPauseMenu() {
    let html = `
        <div class="pause-content">
            <h3>⏸️ 游戏暂停</h3>
            <div class="pause-buttons">
                <button class="menu-btn" onclick="resumeGame()">继续游戏 ▶️</button>
                <button class="menu-btn" onclick="restartLevel()">重新开始 🔄</button>
                <button class="menu-btn" onclick="backToLevelSelect()">返回选关 ⬅️</button>
                <button class="menu-btn" onclick="backToMainMenu()">主菜单 🏠</button>
            </div>
        </div>
    `;
    
    document.getElementById('pauseMenu').innerHTML = html;
    document.getElementById('pauseMenu').style.display = 'flex';
}

function closePauseMenu() {
    document.getElementById('pauseMenu').style.display = 'none';
}

function restartLevel() {
    closePauseMenu();
    startLevel(gameState.currentLevel);
}

// 提示系统
function showHint() {
    if (!gameState.isGameActive || gameState.isPaused) return;
    
    const possibleMoves = findPossibleMoves();
    if (possibleMoves.length === 0) {
        showMessage('💡 没有可行的移动，试试使用道具吧！');
        return;
    }
    
    // 随机选择一个可能的移动并高亮显示
    const randomMove = possibleMoves[Math.floor(Math.random() * possibleMoves.length)];
    highlightHint(randomMove.from.row, randomMove.from.col, randomMove.to.row, randomMove.to.col);
    
    showMessage('💡 试试这里！');
}

function highlightHint(fromRow, fromCol, toRow, toCol) {
    const fromCell = document.querySelector(`[data-row="${fromRow}"][data-col="${fromCol}"]`);
    const toCell = document.querySelector(`[data-row="${toRow}"][data-col="${toCol}"]`);
    
    if (fromCell && toCell) {
        fromCell.style.animation = 'hint 2s ease-in-out';
        toCell.style.animation = 'hint 2s ease-in-out';
        
        setTimeout(() => {
            fromCell.style.animation = '';
            toCell.style.animation = '';
        }, 2000);
    }
    
    // 添加提示动画CSS
    if (!document.querySelector('#hintAnimation')) {
        const style = document.createElement('style');
        style.id = 'hintAnimation';
        style.textContent = `
            @keyframes hint {
                0%, 100% { box-shadow: 0 0 0 rgba(255, 215, 0, 0); }
                50% { box-shadow: 0 0 20px rgba(255, 215, 0, 0.8); }
            }
        `;
        document.head.appendChild(style);
    }
}

// 寻找可能的移动
function findPossibleMoves() {
    const possibleMoves = [];
    
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            // 检查右侧交换
            if (col < 7) {
                const temp = gameState.grid[row][col];
                gameState.grid[row][col] = gameState.grid[row][col + 1];
                gameState.grid[row][col + 1] = temp;
                
                if (hasMatchAtPosition(row, col) || hasMatchAtPosition(row, col + 1)) {
                    possibleMoves.push({
                        from: { row, col },
                        to: { row, col: col + 1 }
                    });
                }
                
                // 恢复
                gameState.grid[row][col + 1] = gameState.grid[row][col];
                gameState.grid[row][col] = temp;
            }
            
            // 检查下方交换
            if (row < 7) {
                const temp = gameState.grid[row][col];
                gameState.grid[row][col] = gameState.grid[row + 1][col];
                gameState.grid[row + 1][col] = temp;
                
                if (hasMatchAtPosition(row, col) || hasMatchAtPosition(row + 1, col)) {
                    possibleMoves.push({
                        from: { row, col },
                        to: { row: row + 1, col }
                    });
                }
                
                // 恢复
                gameState.grid[row + 1][col] = gameState.grid[row][col];
                gameState.grid[row][col] = temp;
            }
        }
    }
    
    return possibleMoves;
}

// UI更新
function updateUI() {
    document.getElementById('currentLevel').textContent = gameState.currentLevel || '练习';
    document.getElementById('score').textContent = gameState.score.toLocaleString();
    document.getElementById('target').textContent = gameState.target === Infinity ? '∞' : gameState.target.toLocaleString();
    document.getElementById('moves').textContent = gameState.moves === Infinity ? '∞' : gameState.moves;
    
    updatePowerUpUI();
}

// 消息显示
function showMessage(message, duration = 3000) {
    // 移除现有消息
    const existingMessage = document.querySelector('.game-message');
    if (existingMessage) {
        existingMessage.remove();
    }
    
    const messageDiv = document.createElement('div');
    messageDiv.className = 'game-message';
    messageDiv.style.cssText = `
        position: fixed;
        top: 20px;
        left: 50%;
        transform: translateX(-50%);
        background: rgba(0, 0, 0, 0.8);
        color: white;
        padding: 1rem 2rem;
        border-radius: 25px;
        z-index: 1000;
        text-align: center;
        font-weight: bold;
        animation: messageSlide 0.5s ease-out;
        max-width: 90vw;
        word-wrap: break-word;
    `;
    
    messageDiv.textContent = message;
    document.body.appendChild(messageDiv);
    
    // 添加消息动画CSS
    if (!document.querySelector('#messageAnimation')) {
        const style = document.createElement('style');
        style.id = 'messageAnimation';
        style.textContent = `
            @keyframes messageSlide {
                from { transform: translateX(-50%) translateY(-20px); opacity: 0; }
                to { transform: translateX(-50%) translateY(0); opacity: 1; }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => {
        if (messageDiv.parentNode) {
            messageDiv.remove();
        }
    }, duration);
}

// 特殊日期效果
function createBirthdayEffect() {
    const effect = document.getElementById('specialDateEffect');
    for (let i = 0; i < 50; i++) {
        const cake = document.createElement('div');
        cake.innerHTML = '🎂';
        cake.style.cssText = `
            position: absolute;
            font-size: 2rem;
            left: ${Math.random() * 100}%;
            animation: birthdayFloat ${Math.random() * 3 + 4}s linear infinite;
            animation-delay: ${Math.random() * 5}s;
        `;
        effect.appendChild(cake);
    }
    
    if (!document.querySelector('#birthdayAnimation')) {
        const style = document.createElement('style');
        style.id = 'birthdayAnimation';
        style.textContent = `
            @keyframes birthdayFloat {
                0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
                10% { opacity: 1; }
                90% { opacity: 1; }
                100% { transform: translateY(-100px) rotate(360deg); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
    }
}

function createValentineEffect() {
    const effect = document.getElementById('specialDateEffect');
    const hearts = ['💕', '💖', '💗', '💝', '💘'];
    
    for (let i = 0; i < 30; i++) {
        const heart = document.createElement('div');
        heart.innerHTML = hearts[Math.floor(Math.random() * hearts.length)];
        heart.style.cssText = `
            position: absolute;
            font-size: 2rem;
            left: ${Math.random() * 100}%;
            animation: valentineFloat ${Math.random() * 4 + 5}s ease-in-out infinite;
            animation-delay: ${Math.random() * 6}s;
        `;
        effect.appendChild(heart);
    }
    
    if (!document.querySelector('#valentineAnimation')) {
        const style = document.createElement('style');
        style.id = 'valentineAnimation';
        style.textContent = `
            @keyframes valentineFloat {
                0%, 100% { transform: translateY(100vh) scale(0); opacity: 0; }
                10%, 90% { opacity: 1; }
                50% { transform: translateY(50vh) scale(1); }
            }
        `;
        document.head.appendChild(style);
    }
}

// 数据存储
function saveGameData() {
    const data = {
        achievements: Array.from(gameState.achievements),
        totalScore: gameState.totalScore,
        gamesPlayed: gameState.gamesPlayed,
        perfectGames: gameState.perfectGames,
        maxCombo: gameState.maxCombo,
        soundEnabled: gameState.soundEnabled
    };
    
    try {
        localStorage.setItem('ashleyAppleGameData', JSON.stringify(data));
    } catch (e) {
        console.warn('无法保存游戏数据:', e);
    }
}

function loadGameData() {
    try {
        const data = localStorage.getItem('ashleyAppleGameData');
        if (data) {
            const parsed = JSON.parse(data);
            gameState.achievements = new Set(parsed.achievements || []);
            gameState.totalScore = parsed.totalScore || 0;
            gameState.gamesPlayed = parsed.gamesPlayed || 0;
            gameState.perfectGames = parsed.perfectGames || 0;
            gameState.maxCombo = parsed.maxCombo || 0;
            gameState.soundEnabled = parsed.soundEnabled !== false;
        }
    } catch (e) {
        console.warn('无法加载游戏数据:', e);
    }
}

// 事件监听器设置
function setupEventListeners() {
    // 防止页面滚动
    document.addEventListener('touchmove', function(e) {
        e.preventDefault();
    }, { passive: false });
    
    // 防止双击缩放
    let lastTouchEnd = 0;
    document.addEventListener('touchend', function(e) {
        const now = (new Date()).getTime();
        if (now - lastTouchEnd <= 300) {
            e.preventDefault();
        }
        lastTouchEnd = now;
    }, false);
    
    // 键盘支持（可选）
    document.addEventListener('keydown', function(e) {
        if (e.key === 'Escape' && gameState.isGameActive) {
            if (gameState.isPaused) {
                resumeGame();
            } else {
                pauseGame();
            }
        }
    });
    
    // 初始化道具按钮
    initializePowerUps();
}

// 页面加载完成后初始化游戏
document.addEventListener('DOMContentLoaded', function() {
    initializeGame();
});

// 页面离开时保存数据
window.addEventListener('beforeunload', function() {
    saveGameData();
});

// 定期保存数据
setInterval(() => {
    if (gameState.isGameActive) {
        saveGameData();
    }
}, 30000); // 每30秒保存一次

</script>
</body>
</html>
