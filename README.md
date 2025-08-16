# Apple-Match-for-Ashley
Creating an interesting game only for my love, Ashley. Hope her happy everyday!
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Ashley's Apple Match - 专属苹果消消乐</title>
    <style>
        /* 基础重置和移动端优化 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            -webkit-touch-callout: none;
            -webkit-user-select: none;
            user-select: none;
        }

        html, body {
            height: 100%;
            overflow: hidden;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            position: fixed;
            width: 100%;
            height: 100vh;
            height: 100dvh; /* 新的动态视口单位 */
        }

        /* 屏幕容器 - 响应式设计 */
        .screen {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            padding: env(safe-area-inset-top) env(safe-area-inset-right) env(safe-area-inset-bottom) env(safe-area-inset-left);
            height: 100vh;
            height: 100dvh;
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
        }

        /* 主菜单样式 */
        #mainMenu {
            justify-content: center;
            text-align: center;
        }

        .logo {
            font-size: clamp(2rem, 8vw, 4rem);
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .subtitle {
            font-size: clamp(1rem, 4vw, 1.5rem);
            margin-bottom: 2rem;
            opacity: 0.9;
        }

        /* 响应式按钮 */
        .menu-btn {
            background: linear-gradient(135deg, #ff6b6b, #ffa500);
            border: none;
            border-radius: 25px;
            color: white;
            cursor: pointer;
            font-size: clamp(1rem, 4vw, 1.2rem);
            font-weight: bold;
            margin: 0.5rem;
            padding: clamp(0.8rem, 3vw, 1.2rem) clamp(1.5rem, 6vw, 2.5rem);
            text-align: center;
            text-decoration: none;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            min-height: 44px; /* iOS触控最小高度 */
            min-width: 120px;
        }

        .menu-btn:active {
            transform: scale(0.95);
            box-shadow: 0 2px 8px rgba(0,0,0,0.3);
        }

        /* 关卡选择界面 */
        #levelSelect {
            padding: 1rem;
        }

        .level-header {
            text-align: center;
            margin-bottom: 1.5rem;
        }

        .level-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1rem;
            max-width: 1200px;
            margin: 0 auto;
        }

        .level-button {
            background: rgba(255,255,255,0.15);
            border: 2px solid rgba(255,255,255,0.3);
            border-radius: 15px;
            color: white;
            cursor: pointer;
            padding: 1.5rem;
            text-align: center;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
            min-height: 120px;
        }

        .level-button:active {
            transform: scale(0.98);
            background: rgba(255,255,255,0.25);
        }

        .level-button.special {
            background: linear-gradient(135deg, rgba(255,182,193,0.3), rgba(255,160,122,0.3));
            border-color: #ffd700;
            box-shadow: 0 0 20px rgba(255,215,0,0.3);
        }

        .love-quote {
            font-size: 0.9rem;
            font-style: italic;
            margin-top: 0.5rem;
            opacity: 0.9;
        }

        /* 游戏界面 */
        #gameScreen {
            padding: 0.5rem;
        }

        .game-header {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 0.5rem;
            margin-bottom: 1rem;
            padding: 0 0.5rem;
        }

        .stat-item {
            background: rgba(255,255,255,0.2);
            border-radius: 10px;
            padding: 0.5rem;
            text-align: center;
            font-size: 0.8rem;
            backdrop-filter: blur(5px);
        }

        .stat-value {
            font-weight: bold;
            font-size: 1.1em;
        }

        /* 游戏网格 - 关键修复 */
        .game-container {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            max-width: 100vw;
            overflow: hidden;
        }

        .game-grid {
            display: grid;
            grid-template-columns: repeat(8, 1fr);
            gap: 2px;
            background: rgba(0,0,0,0.2);
            padding: 4px;
            border-radius: 15px;
            margin-bottom: 1rem;
            /* 响应式网格大小 */
            width: min(90vw, 400px);
            height: min(90vw, 400px);
            max-width: 400px;
            max-height: 400px;
        }

        .grid-cell {
            background: rgba(255,255,255,0.9);
            border-radius: 8px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s ease;
            position: relative;
            aspect-ratio: 1; /* 保持正方形 */
            min-height: 40px;
        }

        .grid-cell:active {
            transform: scale(0.95);
        }

        .grid-cell.selected {
            background: #ffd700 !important;
            box-shadow: 0 0 15px rgba(255,215,0,0.8);
        }

        .apple-icon {
            font-size: clamp(1.2rem, 4vw, 2rem);
            transition: transform 0.2s ease;
        }

        .grid-cell:active .apple-icon {
            transform: scale(1.1);
        }

        /* 道具栏 - 优化布局 */
        .power-ups {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 0.5rem;
            margin-bottom: 1rem;
            width: 100%;
            max-width: 400px;
        }

        .power-up {
            background: rgba(255,255,255,0.2);
            border: 2px solid transparent;
            border-radius: 15px;
            color: white;
            cursor: pointer;
            padding: 0.8rem 0.5rem;
            text-align: center;
            transition: all 0.3s ease;
            font-size: 0.8rem;
            backdrop-filter: blur(5px);
            position: relative;
            min-height: 60px;
        }

        .power-up:active {
            transform: scale(0.95);
            background: rgba(255,255,255,0.3);
        }

        .power-up.active {
            border-color: #ffd700;
            background: rgba(255,215,0,0.3);
            box-shadow: 0 0 15px rgba(255,215,0,0.5);
        }

        .power-up .count {
            position: absolute;
            top: -5px;
            right: -5px;
            background: #ff6b6b;
            border-radius: 50%;
            color: white;
            font-size: 0.7rem;
            font-weight: bold;
            height: 20px;
            line-height: 20px;
            min-width: 20px;
            text-align: center;
        }

        /* 控制按钮 */
        .game-controls {
            display: flex;
            justify-content: center;
            gap: 0.8rem;
            flex-wrap: wrap;
            margin-top: auto;
            padding: 1rem 0;
        }

        .control-btn {
            background: rgba(255,255,255,0.2);
            border: none;
            border-radius: 20px;
            color: white;
            cursor: pointer;
            font-size: 0.9rem;
            padding: 0.6rem 1.2rem;
            transition: all 0.3s ease;
            backdrop-filter: blur(5px);
            min-height: 40px;
        }

        .control-btn:active {
            transform: scale(0.95);
            background: rgba(255,255,255,0.3);
        }

        /* 弹窗样式 */
        .popup, .pause-menu, .achievement-popup {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            backdrop-filter: blur(5px);
        }

        .popup-content, .pause-content {
            background: linear-gradient(135deg, #667eea, #764ba2);
            border-radius: 20px;
            padding: 2rem;
            text-align: center;
            max-width: 90vw;
            max-height: 90vh;
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
            box-shadow: 0 20px 60px rgba(0,0,0,0.4);
        }

        .achievement-popup {
            align-items: flex-start;
            padding-top: 60px;
        }

        .achievement-popup.show {
            display: flex;
        }

        .achievement-content {
            background: linear-gradient(135deg, #4CAF50, #45a049);
            border-radius: 15px;
            padding: 1.5rem;
            text-align: center;
            transform: translateY(-20px);
            animation: achievementSlide 0.5s ease-out forwards;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        @keyframes achievementSlide {
            to { transform: translateY(0); }
        }

        /* 背景效果 */
        .hearts-background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
            overflow: hidden;
        }

        .heart {
            position: absolute;
            font-size: 1.5rem;
            opacity: 0.3;
            animation: heartFloat 8s linear infinite;
            pointer-events: none;
        }

        @keyframes heartFloat {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
            10% { opacity: 0.3; }
            90% { opacity: 0.3; }
            100% { transform: translateY(-50px) rotate(360deg); opacity: 0; }
        }

        /* 媒体查询 - 不同设备优化 */
        @media (max-width: 480px) {
            .game-grid {
                width: 95vw;
                height: 95vw;
                max-width: 350px;
                max-height: 350px;
            }
            
            .level-grid {
                grid-template-columns: 1fr;
                gap: 0.8rem;
            }
            
            .power-ups {
                grid-template-columns: repeat(6, 1fr);
                gap: 0.3rem;
            }
            
            .power-up {
                font-size: 0.7rem;
                padding: 0.5rem 0.3rem;
            }
        }

        @media (orientation: landscape) and (max-height: 600px) {
            .game-grid {
                width: min(60vh, 350px);
                height: min(60vh, 350px);
            }
            
            .screen {
                padding: 0.5rem;
            }
        }

        /* iOS安全区域适配 */
        @supports (padding: max(0px)) {
            .screen {
                padding-left: max(env(safe-area-inset-left), 1rem);
                padding-right: max(env(safe-area-inset-right), 1rem);
                padding-top: max(env(safe-area-inset-top), 1rem);
                padding-bottom: max(env(safe-area-inset-bottom), 1rem);
            }
        }
    </style>
</head>
<body>
    <!-- 背景爱心效果 -->
    <div id="heartsBackground" class="hearts-background"></div>
    
    <!-- 特殊日期效果 -->
    <div id="specialDateEffect" class="hearts-background"></div>

    <!-- 主菜单 -->
    <div id="mainMenu" class="screen" style="display: flex;">
        <div class="logo">🍎💕 Ashley's Apple Match 💕🍎</div>
        <div class="subtitle">专属于你的苹果消消乐</div>
        
        <button class="menu-btn" onclick="showScreen('levelSelect')">开始游戏 🎮</button>
        <button class="menu-btn" onclick="showAchievements()">成就系统 🏆</button>
        <button class="menu-btn" onclick="showLoveMessages()">专属情话 💕</button>
        <button class="menu-btn" onclick="showGameGuide()">游戏说明 📖</button>
        <button class="menu-btn" onclick="showSettings()">设置 ⚙️</button>
    </div>

    <!-- 关卡选择 -->
    <div id="levelSelect" class="screen">
        <div class="level-header">
            <h2 style="margin-bottom: 0.5rem;">🍎 选择关卡 🍎</h2>
            <p>为我的宝贝Ashley量身定制</p>
            <button class="control-btn" onclick="showScreen('mainMenu')" style="margin-top: 1rem;">
                返回主菜单 🏠
            </button>
        </div>
        <div id="levelGrid" class="level-grid"></div>
    </div>

    <!-- 游戏界面 -->
    <div id="gameScreen" class="screen">
        <!-- 游戏头部信息 -->
        <div class="game-header">
            <div class="stat-item">
                <div class="stat-value" id="currentLevel">1</div>
                <div>关卡</div>
            </div>
            <div class="stat-item">
                <div class="stat-value" id="score">0</div>
                <div>得分</div>
            </div>
            <div class="stat-item">
                <div class="stat-value" id="target">1000</div>
                <div>目标</div>
            </div>
            <div class="stat-item">
                <div class="stat-value" id="moves">30</div>
                <div>步数</div>
            </div>
        </div>

        <!-- 游戏容器 -->
        <div class="game-container">
            <!-- 游戏网格 -->
            <div id="gameGrid" class="game-grid"></div>

            <!-- 道具栏 -->
            <div class="power-ups">
                <div class="power-up" data-power="bomb">
                    💥<br>炸弹
                    <span class="count">5</span>
                </div>
                <div class="power-up" data-power="lightning">
                    ⚡<br>闪电
                    <span class="count">5</span>
                </div>
                <div class="power-up" data-power="rainbow">
                    🌈<br>彩虹
                    <span class="count">3</span>
                </div>
                <div class="power-up" data-power="hammer">
                    🔨<br>锤子
                    <span class="count">8</span>
                </div>
                <div class="power-up" data-power="shuffle">
                    🔄<br>洗牌
                    <span class="count">3</span>
                </div>
                <div class="power-up" data-power="time">
                    ⏰<br>时光
                    <span class="count">3</span>
                </div>
            </div>
        </div>

        <!-- 游戏控制 -->
        <div class="game-controls">
            <button class="control-btn" onclick="pauseGame()">暂停 ⏸️</button>
            <button class="control-btn" onclick="showHint()">提示 💡</button>
            <button class="control-btn" onclick="restartLevel()">重来 🔄</button>
        </div>
    </div>

    <!-- 暂停菜单 -->
    <div id="pauseMenu" class="pause-menu"></div>

    <!-- 成就弹窗 -->
    <div id="achievementPopup" class="achievement-popup">
        <div class="achievement-content">
            <div id="achievementText"></div>
        </div>
    </div>

    <!-- 游戏说明弹窗 -->
    <div id="gameGuide" class="popup">
        <div class="popup-content">
            <h2 style="margin-bottom: 1.5rem; color: #ffd700;">📖 游戏说明</h2>
            
            <div style="text-align: left; margin-bottom: 2rem;">
                <h3 style="color: #ffd700; margin-bottom: 1rem;">🎯 基本玩法</h3>
                <p style="margin-bottom: 1rem;">• 交换相邻的苹果，形成3个或更多相同的苹果连线</p>
                <p style="margin-bottom: 1rem;">• 可以水平或垂直连线，达成目标分数即可过关</p>
                <p style="margin-bottom: 1rem;">• 连击越多，分数加成越高！</p>
                
                <h3 style="color: #ffd700; margin: 1.5rem 0 1rem;">🔧 道具说明</h3>
                <div style="display: grid; gap: 0.8rem;">
                    <div>💥 <strong>炸弹</strong> - 消除3×3范围内所有苹果</div>
                    <div>⚡ <strong>闪电</strong> - 消除整行整列苹果</div>
                    <div>🌈 <strong>彩虹</strong> - 消除所有相同类型的苹果</div>
                    <div>🔨 <strong>锤子</strong> - 消除单个苹果</div>
                    <div>🔄 <strong>洗牌</strong> - 重新排列棋盘</div>
                    <div>⏰ <strong>时光</strong> - 增加20步数</div>
                </div>
                
                <h3 style="color: #ffd700; margin: 1.5rem 0 1rem;">💡 游戏技巧</h3>
                <p style="margin-bottom: 0.5rem;">• 优先寻找能形成连击的位置</p>
                <p style="margin-bottom: 0.5rem;">• 合理使用道具，特别是在困难时刻</p>
                <p style="margin-bottom: 0.5rem;">• 观察整个棋盘，寻找最佳移动策略</p>
                <p>• 练习模式可以无限练习，熟悉游戏机制</p>
            </div>
            
            <button class="menu-btn" onclick="closeGameGuide()">开始游戏 💕</button>
        </div>
    </div>

<script>
// 游戏状态 - 调整难度平衡
const gameState = {
    grid: [],
    score: 0,
    target: 1000,
    moves: 30,
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
        bomb: 5,       // 炸弹数量调回合理值
        lightning: 5,  // 闪电数量调回合理值
        rainbow: 3,    // 彩虹保持稀缺
        hammer: 8,     // 锤子适中
        shuffle: 3,    // 洗牌保持稀缺
        time: 3        // 时光保持稀缺
    },
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

// 关卡配置 - 调整为更合理的难度曲线
const LEVELS = [
    {
        id: 1,
        target: 1000,
        moves: 50,    // 适当增加但不过分
        quote: "就像消除这些苹果一样，我想消除你所有的烦恼 💕",
        difficulty: 'easy',
        specialApples: 0.05,    // 降低特殊苹果概率
        comboBoost: 1.1         // 降低连击加成
    },
    {
        id: 2,
        target: 1500,
        moves: 55,
        quote: "每一次匹配，都像我们心灵的契合 ✨",
        difficulty: 'easy',
        specialApples: 0.05,
        comboBoost: 1.1
    },
    {
        id: 3,
        target: 2000,
        moves: 60,
        quote: "红苹果是我的心，绿苹果是我们的希望 🍎💚",
        difficulty: 'normal',
        special: true,
        specialApples: 0.08,
        comboBoost: 1.2
    },
    {
        id: 4,
        target: 2500,
        moves: 65,
        quote: "就算有再多挑战，我也要和你一起闯关 💪💕",
        difficulty: 'normal',
        specialApples: 0.06,
        comboBoost: 1.15
    },
    {
        id: 5,
        target: 3000,
        moves: 70,
        quote: "五关了呢，就像我们认识的第五个月一样美好 🌸",
        difficulty: 'normal',
        specialApples: 0.08,
        comboBoost: 1.2
    },
    {
        id: 6,
        target: 3500,
        moves: 75,
        quote: "六六大顺，希望我们的爱情也六六大顺 🍀",
        difficulty: 'hard',
        specialApples: 0.1,
        comboBoost: 1.25
    },
    {
        id: 7,
        target: 4000,
        moves: 80,
        quote: "第七关，像七色彩虹一样绚烂的我们 🌈",
        difficulty: 'hard',
        special: true,
        specialApples: 0.12,
        comboBoost: 1.3
    },
    {
        id: 8,
        target: 4500,
        moves: 85,
        quote: "八这个数字多吉利，像我们的爱情一样发发发 💰💕",
        difficulty: 'hard',
        specialApples: 0.1,
        comboBoost: 1.25
    },
    {
        id: 9,
        target: 5000,
        moves: 90,
        quote: "九关了！长长久久，我们要一直在一起 💍",
        difficulty: 'expert',
        specialApples: 0.15,
        comboBoost: 1.4
    },
    {
        id: 10,
        target: 5500,
        moves: 95,
        quote: "十全十美的我们，十全十美的爱情 💯💕",
        difficulty: 'expert',
        special: true,
        specialApples: 0.18,
        comboBoost: 1.45
    },
    {
        id: 11,
        target: 6000,
        moves: 100,
        quote: "11这个数字，像两个人紧紧相依 👫💕",
        difficulty: 'expert',
        specialApples: 0.12,
        comboBoost: 1.35
    },
    {
        id: 12,
        target: 6500,
        moves: 110,
        quote: "最后一关了！就像我们要一起走到最后一样 🌅💕",
        difficulty: 'master',
        special: true,
        specialApples: 0.2,
        comboBoost: 1.5
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
        desc: '剩余步数超过30步完成关卡',
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
    
    for (let i = 0; i < 12; i++) {  // 减少爱心数量避免性能问题
        const heart = document.createElement('div');
        heart.className = 'heart';
        heart.innerHTML = ['💕', '💖', '💗', '💝', '💘'][Math.floor(Math.random() * 5)];
        heart.style.left = Math.random() * 100 + '%';
        heart.style.animationDelay = Math.random() * 8 + 's';
        heart.style.animationDuration = (Math.random() * 4 + 6) + 's';
        container.appendChild(heart);
    }
}

// 创建关卡按钮 (继续)
function createLevelButtons() {
    const levelGrid = document.getElementById('levelGrid');
    
    // 练习模式按钮
    const practiceButton = document.createElement('button');
    practiceButton.className = 'level-button practice';
    practiceButton.innerHTML = `
        <h3>🎯 练习模式</h3>
        <p>无限步数，随意练习</p>
        <div class="love-quote">在这里尽情享受游戏的乐趣吧~ 💕</div>
    `;
    practiceButton.onclick = () => startLevel(0);
    levelGrid.appendChild(practiceButton);

    // 创建正式关卡按钮
    LEVELS.forEach(level => {
        const button = document.createElement('button');
        button.className = level.special ? 'level-button special' : 'level-button';
        button.innerHTML = `
            <h3>${level.special ? '💖' : '🍎'} 第${level.id}关</h3>
            <p>目标: ${level.target.toLocaleString()} 分</p>
            <p>步数: ${level.moves} 步</p>
            <div class="love-quote">${level.quote}</div>
        `;
        button.onclick = () => startLevel(level.id);
        levelGrid.appendChild(button);
    });
}

// 开始游戏关卡
function startLevel(levelId) {
    gameState.currentLevel = levelId;
    
    if (levelId === 0) {
        // 练习模式
        gameState.target = Infinity;
        gameState.moves = Infinity;
    } else {
        // 正式关卡
        const level = LEVELS.find(l => l.id === levelId);
        if (level) {
            gameState.target = level.target;
            gameState.moves = level.moves;
        }
    }
    
    // 重置游戏状态
    gameState.score = 0;
    gameState.combo = 0;
    gameState.selectedCell = null;
    gameState.isGameActive = true;
    gameState.isPaused = false;
    gameState.activePowerUp = null;
    
    // 初始化网格
    initializeGrid();
    showGameScreen();
    updateUI();
    
    // 显示关卡开始消息
    if (levelId === 0) {
        showMessage('🎯 练习模式开始！尽情享受吧~');
    } else {
        const level = LEVELS.find(l => l.id === levelId);
        showMessage(`🍎 第${levelId}关开始！\n${level?.quote || ''}`);
    }
}

// 初始化游戏网格
function initializeGrid() {
    gameState.grid = [];
    
    for (let row = 0; row < 8; row++) {
        gameState.grid[row] = [];
        for (let col = 0; col < 8; col++) {
            gameState.grid[row][col] = createRandomApple();
        }
    }
    
    // 移除初始匹配
    removeInitialMatches();
    renderGrid();
}

// 创建随机苹果
function createRandomApple() {
    const randomType = APPLE_TYPES[Math.floor(Math.random() * APPLE_TYPES.length)];
    return {
        emoji: randomType.emoji,
        type: randomType.type,
        class: randomType.class
    };
}

// 移除初始匹配
function removeInitialMatches() {
    let hasMatches = true;
    let attempts = 0;
    
    while (hasMatches && attempts < 50) {
        hasMatches = false;
        attempts++;
        
        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                if (hasMatchAtPosition(row, col)) {
                    gameState.grid[row][col] = createRandomApple();
                    hasMatches = true;
                }
            }
        }
    }
}

// 检查位置是否有匹配
function hasMatchAtPosition(row, col) {
    const currentApple = gameState.grid[row][col];
    if (!currentApple) return false;
    
    // 检查水平匹配
    let horizontalCount = 1;
    
    // 向左检查
    for (let c = col - 1; c >= 0 && gameState.grid[row][c]?.type === currentApple.type; c--) {
        horizontalCount++;
    }
    
    // 向右检查
    for (let c = col + 1; c < 8 && gameState.grid[row][c]?.type === currentApple.type; c++) {
        horizontalCount++;
    }
    
    if (horizontalCount >= 3) return true;
    
    // 检查垂直匹配
    let verticalCount = 1;
    
    // 向上检查
    for (let r = row - 1; r >= 0 && gameState.grid[r][col]?.type === currentApple.type; r--) {
        verticalCount++;
    }
    
    // 向下检查
    for (let r = row + 1; r < 8 && gameState.grid[r][col]?.type === currentApple.type; r++) {
        verticalCount++;
    }
    
    return verticalCount >= 3;
}

// 渲染游戏网格
function renderGrid() {
    const gameGrid = document.getElementById('gameGrid');
    gameGrid.innerHTML = '';
    
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            const cell = document.createElement('div');
            cell.className = 'grid-cell';
            cell.dataset.row = row;
            cell.dataset.col = col;
            cell.addEventListener('click', () => handleCellClick(row, col));
            
            updateCellDisplay(row, col, cell);
            gameGrid.appendChild(cell);
        }
    }
}

// 更新单元格显示
function updateCellDisplay(row, col, cell = null) {
    if (!cell) {
        cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    }
    
    if (!cell) return;
    
    const apple = gameState.grid[row][col];
    if (apple) {
        cell.innerHTML = `<span class="apple-icon">${apple.emoji}</span>`;
        cell.style.background = 'rgba(255,255,255,0.9)';
    } else {
        cell.innerHTML = '';
        cell.style.background = 'rgba(255,255,255,0.3)';
    }
}

// 处理单元格点击
function handleCellClick(row, col) {
    if (!gameState.isGameActive || gameState.isPaused) return;
    
    // 如果选择了道具，使用道具
    if (gameState.activePowerUp) {
        usePowerUp(gameState.activePowerUp, row, col);
        return;
    }
    
    const clickedCell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    
    if (!gameState.selectedCell) {
        // 第一次选择
        if (!gameState.grid[row][col]) return; // 空格子不能选择
        
        gameState.selectedCell = { row, col };
        clickedCell.classList.add('selected');
        playSound('select');
    } else {
        const { row: selectedRow, col: selectedCol } = gameState.selectedCell;
        const selectedCell = document.querySelector(`[data-row="${selectedRow}"][data-col="${selectedCol}"]`);
        
        if (row === selectedRow && col === selectedCol) {
            // 取消选择
            gameState.selectedCell = null;
            selectedCell.classList.remove('selected');
            return;
        }
        
        // 检查是否相邻
        const isAdjacent = (Math.abs(row - selectedRow) === 1 && col === selectedCol) ||
                          (Math.abs(col - selectedCol) === 1 && row === selectedRow);
        
        if (isAdjacent) {
            // 尝试交换
            attemptSwap(selectedRow, selectedCol, row, col);
        }
        
        // 清除选择状态
        gameState.selectedCell = null;
        selectedCell.classList.remove('selected');
    }
}

// 尝试交换苹果
function attemptSwap(row1, col1, row2, col2) {
    // 交换苹果
    const temp = gameState.grid[row1][col1];
    gameState.grid[row1][col1] = gameState.grid[row2][col2];
    gameState.grid[row2][col2] = temp;
    
    // 检查是否形成匹配
    const hasMatch = hasMatchAtPosition(row1, col1) || hasMatchAtPosition(row2, col2);
    
    if (hasMatch) {
        // 有效移动
        gameState.moves--;
        updateCellDisplay(row1, col1);
        updateCellDisplay(row2, col2);
        playSound('swap');
        
        setTimeout(() => {
            processMatches();
        }, 200);
    } else {
        // 无效移动，交换回去
        gameState.grid[row2][col2] = gameState.grid[row1][col1];
        gameState.grid[row1][col1] = temp;
        
        playSound('invalid');
        showMessage('❌ 这样移动不能形成匹配！');
    }
    
    updateUI();
}

// 寻找所有匹配
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
                if (count >= 3 && currentType) {
                    for (let c = col - count; c < col; c++) {
                        matches.add(`${row}-${c}`);
                    }
                }
                count = 1;
                currentType = gameState.grid[row][col]?.type;
            }
        }
        
        if (count >= 3 && currentType) {
            for (let c = 8 - count; c < 8; c++) {
                matches.add(`${row}-${c}`);
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
                if (count >= 3 && currentType) {
                    for (let r = row - count; r < row; r++) {
                        matches.add(`${r}-${col}`);
                    }
                }
                count = 1;
                currentType = gameState.grid[row][col]?.type;
            }
        }
        
        if (count >= 3 && currentType) {
            for (let r = 8 - count; r < 8; r++) {
                matches.add(`${r}-${col}`);
            }
        }
    }
    
    return Array.from(matches).map(pos => {
        const [row, col] = pos.split('-').map(Number);
        return { row, col };
    });
}

// 处理匹配
function processMatches() {
    const matches = findMatches();
    
    if (matches.length === 0) {
        gameState.combo = 0;
        checkGameStatus();
        return;
    }
    
    // 增加连击
    gameState.combo++;
    gameState.maxCombo = Math.max(gameState.maxCombo, gameState.combo);
    gameState.totalMatches++;
    
    // 计算分数
    const baseScore = matches.length * 100;
    const comboBonus = gameState.combo > 1 ? (gameState.combo - 1) * 0.5 : 0;
    const currentLevel = LEVELS.find(l => l.id === gameState.currentLevel);
    const levelBonus = currentLevel?.comboBoost || 1;
    
    const totalScore = Math.floor(baseScore * (1 + comboBonus) * levelBonus);
    gameState.score += totalScore;
    
    // 显示匹配动画和分数
    matches.forEach(({row, col}) => {
        const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
        if (cell) {
            cell.style.animation = 'matchPulse 0.6s ease-out';
        }
        gameState.grid[row][col] = null;
    });
    
    // 显示连击和分数消息
    let message = `消除${matches.length}个苹果！+${totalScore}分`;
    if (gameState.combo > 1) {
        message += ` 🔥 ${gameState.combo}连击!`;
    }
    showMessage(message);
    
    playSound('match');
    
    // 添加匹配动画CSS
    if (!document.querySelector('#matchAnimation')) {
        const style = document.createElement('style');
        style.id = 'matchAnimation';
        style.textContent = `
            @keyframes matchPulse {
                0% { transform: scale(1); background: rgba(255,255,255,0.9); }
                50% { transform: scale(1.1); background: rgba(255,215,0,0.8); }
                100% { transform: scale(0); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => {
        matches.forEach(({row, col}) => {
            updateCellDisplay(row, col);
        });
        
        setTimeout(() => {
            fillGrid();
        }, 200);
    }, 600);
}

// 填充网格
async function fillGrid() {
    let needsFill = true;
    
    while (needsFill) {
        needsFill = false;
        
        // 苹果下落
        for (let col = 0; col < 8; col++) {
            for (let row = 7; row >= 0; row--) {
                if (!gameState.grid[row][col]) {
                    for (let r = row - 1; r >= 0; r--) {
                        if (gameState.grid[r][col]) {
                            gameState.grid[row][col] = gameState.grid[r][col];
                            gameState.grid[r][col] = null;
                            needsFill = true;
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
        
        if (needsFill) {
            await new Promise(resolve => setTimeout(resolve, 100));
        }
    }
    
    // 填充空位
    for (let col = 0; col < 8; col++) {
        for (let row = 0; row < 8; row++) {
            if (!gameState.grid[row][col]) {
                gameState.grid[row][col] = createRandomApple();
                updateCellDisplay(row, col);
                
                const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
                if (cell) {
                    cell.style.animation = 'dropIn 0.3s ease-out';
                    setTimeout(() => cell.style.animation = '', 300);
                }
            }
        }
    }
    
    // 添加下落动画
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
    
    setTimeout(() => {
        const newMatches = findMatches();
        if (newMatches.length > 0) {
            setTimeout(() => processMatches(), 300);
        } else {
            gameState.combo = 0;
            checkGameStatus();
        }
    }, 400);
}

// 音效播放
function playSound(type) {
    if (!gameState.soundEnabled) return;
    
    // 使用Web Audio API创建简单音效
    try {
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        const oscillator = audioContext.createOscillator();
        const gainNode = audioContext.createGain();
        
        oscillator.connect(gainNode);
        gainNode.connect(audioContext.destination);
        
        let frequency, duration;
        
        switch (type) {
            case 'select': frequency = 800; duration = 0.1; break;
            case 'swap': frequency = 600; duration = 0.2; break;
            case 'match': frequency = 1000; duration = 0.3; break;
            case 'combo': frequency = 1200; duration = 0.4; break;
            case 'powerUp': frequency = 1500; duration = 0.5; break;
            case 'achievement': frequency = 2000; duration = 0.8; break;
            case 'invalid': frequency = 300; duration = 0.2; break;
            default: frequency = 600; duration = 0.2;
        }
        
        oscillator.frequency.value = frequency;
        oscillator.type = 'sine';
        
        gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + duration);
        
        oscillator.start(audioContext.currentTime);
        oscillator.stop(audioContext.currentTime + duration);
    } catch (e) {
        // 静默处理音频错误
    }
}

// 为gameState添加playSound方法
gameState.playSound = playSound;

// 道具系统
function setupPowerUpButtons() {
    document.querySelectorAll('.power-up').forEach(button => {
        button.addEventListener('click', function() {
            const powerType = this.dataset.power;
            selectPowerUp(powerType);
        });
    });
}

function selectPowerUp(powerType) {
    if (!gameState.isGameActive || gameState.isPaused) return;
    
    if (gameState.powerUps[powerType] <= 0) {
        showMessage('❌ 道具数量不足！');
        return;
    }
    
    document.querySelectorAll('.power-up').forEach(btn => {
        btn.classList.remove('active');
    });
    
    if (gameState.activePowerUp === powerType) {
        gameState.activePowerUp = null;
        showMessage('取消道具选择');
    } else {
        gameState.activePowerUp = powerType;
        const button = document.querySelector(`[data-power="${powerType}"]`);
        if (button) button.classList.add('active');
        
        const powerNames = {
            bomb: '💥 炸弹',
            lightning: '⚡ 闪电',
            rainbow: '🌈 彩虹',
            hammer: '🔨 锤子',
            shuffle: '🔄 洗牌',
            time: '⏰ 时光'
        };
        
        showMessage(`已选择道具：${powerNames[powerType]}`);
        
        if (powerType === 'shuffle' || powerType === 'time') {
            usePowerUp(powerType, 0, 0);
        }
    }
}

function usePowerUp(powerType, row, col) {
    if (gameState.powerUps[powerType] <= 0) {
        showMessage('❌ 道具数量不足！');
        return;
    }
    
    gameState.powerUps[powerType]--;
    gameState.activePowerUp = null;
    
    document.querySelectorAll('.power-up').forEach(btn => {
        btn.classList.remove('active');
    });
    
    switch (powerType) {
        case 'bomb': useBomb(row, col); break;
        case 'lightning': useLightning(row, col); break;
        case 'rainbow': useRainbow(row, col); break;
        case 'hammer': useHammer(row, col); break;
        case 'shuffle': useShuffle(); break;
        case 'time': useTime(); break;
    }
    
    updatePowerUpUI();
    playSound('powerUp');
    checkAchievements();
}

function useBomb(centerRow, centerCol) {
    const affectedCells = [];
    
    for (let row = Math.max(0, centerRow - 1); row <= Math.min(7, centerRow + 1); row++) {
        for (let col = Math.max(0, centerCol - 1); col <= Math.min(7, centerCol + 1); col++) {
            if (gameState.grid[row][col]) {
                affectedCells.push({ row, col });
            }
        }
    }
    
    showExplosionEffect(centerRow, centerCol);
    
    setTimeout(() => {
        const score = affectedCells.length * 150;
        gameState.score += score;
        
        affectedCells.forEach(({row, col}) => {
            gameState.grid[row][col] = null;
            updateCellDisplay(row, col);
        });
        
        showMessage(`💥 炸弹爆炸！获得 ${score} 分！`);
        
        setTimeout(() => fillGrid(), 500);
    }, 600);
}

function useLightning(row, col) {
    const affectedCells = [];
    
    for (let c = 0; c < 8; c++) {
        if (gameState.grid[row][c]) {
            affectedCells.push({ row, col: c });
        }
    }
    
    for (let r = 0; r < 8; r++) {
        if (gameState.grid[r][col] && !affectedCells.some(cell => cell.row === r && cell.col === col)) {
            affectedCells.push({ row: r, col });
        }
    }
    
    showLightningEffect(row, col);
    
    setTimeout(() => {
        const score = affectedCells.length * 120;
        gameState.score += score;
        
        affectedCells.forEach(({row, col}) => {
            gameState.grid[row][col] = null;
            updateCellDisplay(row, col);
        });
        
        showMessage(`⚡ 闪电一击！获得 ${score} 分！`);
        
        setTimeout(() => fillGrid(), 500);
    }, 800);
}

function useTime() {
    if (gameState.currentLevel === 0) {
        showMessage('⏰ 练习模式已经是无限步数了！');
        gameState.powerUps.time++;
        updatePowerUpUI();
        return;
    }
    
    const addedMoves = 20; // 增加20步
    gameState.moves += addedMoves;
    
    showTimeEffect();
    showMessage(`⏰ 时光倒流！增加 ${addedMoves} 步！`);
    updateUI();
}

// 特效函数
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
    
    setTimeout(() => explosion.remove(), 600);
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
    
    setTimeout(() => timeEffect.remove(), 2000);
}

// 游戏说明
function showGameGuide() {
    document.getElementById('gameGuide').style.display = 'flex';
}

function closeGameGuide() {
    document.getElementById('gameGuide').style.display = 'none';
    showScreen('levelSelect');
}

// 界面控制
function showScreen(screenName) {
    document.querySelectorAll('.screen').forEach(screen => {
        screen.style.display = 'none';
    });
    document.getElementById(screenName).style.display = 'flex';
}

function showGameScreen() {
    showScreen('gameScreen');
}

function updateUI() {
    document.getElementById('currentLevel').textContent = gameState.currentLevel || '练习';
    document.getElementById('score').textContent = gameState.score.toLocaleString();
    document.getElementById('target').textContent = gameState.target === Infinity ? '∞' : gameState.target.toLocaleString();
    document.getElementById('moves').textContent = gameState.moves === Infinity ? '∞' : gameState.moves;
    
    updatePowerUpUI();
}

function updatePowerUpUI() {
    Object.keys(gameState.powerUps).forEach(powerType => {
        const button = document.querySelector(`[data-power="${powerType}"]`);
        if (button) {
            const countElement = button.querySelector('.count');
            if (countElement) {
                countElement.textContent = gameState.powerUps[powerType];
                
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

function showMessage(message, duration = 3000) {
    const existingMessage = document.querySelector('.game-message');
    if (existingMessage) existingMessage.remove();
    
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
        font-size: 0.9rem;
    `;
    
    messageDiv.textContent = message;
    document.body.appendChild(messageDiv);
    
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
        if (messageDiv.parentNode) messageDiv.remove();
    }, duration);
}

// 游戏状态检查
function checkGameStatus() {
    if (gameState.currentLevel === 0) return;
    
    if (gameState.score >= gameState.target) {
        gameState.isGameActive = false;
        gameState.gamesPlayed++;
        gameState.totalScore += gameState.score;
// 检查关卡胜利
        if (gameState.moves >= 30) {
            gameState.perfectGames++;
            showMessage('👑 完美通关！剩余步数超过30步！');
            checkAchievements();
        }
        
        setTimeout(() => {
            showLevelComplete();
        }, 1000);
        
    } else if (gameState.moves <= 0 && gameState.score < gameState.target) {
        gameState.isGameActive = false;
        setTimeout(() => {
            showGameOver();
        }, 500);
    }
    
    checkAchievements();
}

// 显示关卡完成
function showLevelComplete() {
    const level = LEVELS.find(l => l.id === gameState.currentLevel);
    
    const popup = document.createElement('div');
    popup.className = 'popup';
    popup.style.display = 'flex';
    
    popup.innerHTML = `
        <div class="popup-content">
            <h2 style="color: #4CAF50; margin-bottom: 1rem;">🎉 关卡完成！</h2>
            <div style="margin-bottom: 1.5rem;">
                <div style="font-size: 1.2rem; margin-bottom: 0.5rem;">第${gameState.currentLevel}关</div>
                <div style="font-size: 1.5rem; color: #ffd700; font-weight: bold;">${gameState.score.toLocaleString()} 分</div>
                <div style="margin-top: 0.8rem; font-style: italic; opacity: 0.9;">
                    ${level?.quote || '恭喜完成关卡！'}
                </div>
            </div>
            
            <div style="display: flex; gap: 0.8rem; flex-wrap: wrap; justify-content: center;">
                <button class="menu-btn" onclick="this.closest('.popup').remove(); showScreen('levelSelect');">
                    选择关卡 📝
                </button>
                <button class="menu-btn" onclick="this.closest('.popup').remove(); startLevel(${gameState.currentLevel + 1});">
                    下一关 ➡️
                </button>
                <button class="menu-btn" onclick="this.closest('.popup').remove(); showScreen('mainMenu');">
                    主菜单 🏠
                </button>
            </div>
        </div>
    `;
    
    document.body.appendChild(popup);
    playSound('achievement');
}

// 显示游戏结束
function showGameOver() {
    const popup = document.createElement('div');
    popup.className = 'popup';
    popup.style.display = 'flex';
    
    popup.innerHTML = `
        <div class="popup-content">
            <h2 style="color: #ff6b6b; margin-bottom: 1rem;">😔 挑战失败</h2>
            <div style="margin-bottom: 1.5rem;">
                <div style="margin-bottom: 0.5rem;">第${gameState.currentLevel}关</div>
                <div style="font-size: 1.2rem; margin-bottom: 0.5rem;">得分: ${gameState.score.toLocaleString()}</div>
                <div style="opacity: 0.8;">目标: ${gameState.target.toLocaleString()}</div>
                <div style="margin-top: 1rem; font-style: italic; color: #ffd700;">
                    "没关系，再试一次！我相信你一定可以的 💪💕"
                </div>
            </div>
            
            <div style="display: flex; gap: 0.8rem; flex-wrap: wrap; justify-content: center;">
                <button class="menu-btn" onclick="this.closest('.popup').remove(); restartLevel();">
                    重新挑战 🔄
                </button>
                <button class="menu-btn" onclick="this.closest('.popup').remove(); showScreen('levelSelect');">
                    选择关卡 📝
                </button>
                <button class="menu-btn" onclick="this.closest('.popup').remove(); showScreen('mainMenu');">
                    主菜单 🏠
                </button>
            </div>
        </div>
    `;
    
    document.body.appendChild(popup);
}

// 成就检查
function checkAchievements() {
    if (gameState.totalMatches > 0 && !gameState.achievements.has('first_match')) {
        unlockAchievement('first_match');
    }
    
    if (gameState.combo >= 10 && !gameState.achievements.has('combo_master')) {
        unlockAchievement('combo_master');
    }
    
    if (gameState.score >= 5000 && !gameState.achievements.has('score_hunter')) {
        unlockAchievement('score_hunter');
    }
    
    if (gameState.moves >= 30 && gameState.score >= gameState.target && !gameState.achievements.has('perfect_level')) {
        unlockAchievement('perfect_level');
    }
    
    // 检查道具大师成就
    const usedPowerTypes = Object.keys(gameState.powerUps).filter(type => 
        gameState.powerUps[type] < (type === 'hammer' ? 8 : type === 'bomb' || type === 'lightning' ? 5 : 3)
    );
    if (usedPowerTypes.length >= 6 && !gameState.achievements.has('power_master')) {
        unlockAchievement('power_master');
    }
    
    // 检查特殊成就
    if (gameState.gamesPlayed >= 10 && !gameState.achievements.has('ashley_special')) {
        unlockAchievement('ashley_special');
    }
}

function unlockAchievement(achievementId) {
    if (gameState.achievements.has(achievementId)) return;
    
    gameState.achievements.add(achievementId);
    const achievement = ACHIEVEMENTS.find(a => a.id === achievementId);
    
    if (achievement) {
        showAchievement(achievement);
        saveGameData();
    }
}

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

// 其余功能
function useRainbow(row, col) {
    const targetType = gameState.grid[row][col]?.type;
    if (!targetType) {
        showMessage('❌ 请选择一个有苹果的位置！');
        gameState.powerUps.rainbow++;
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
    
    showRainbowEffect();
    
    setTimeout(() => {
        const score = affectedCells.length * 200;
        gameState.score += score;
        
        affectedCells.forEach(({row, col}) => {
            gameState.grid[row][col] = null;
            updateCellDisplay(row, col);
        });
        
        showMessage(`🌈 彩虹消除！获得 ${score} 分！`);
        
        setTimeout(() => fillGrid(), 500);
    }, 1000);
}

function useHammer(row, col) {
    if (!gameState.grid[row][col]) {
        showMessage('❌ 请选择一个有苹果的位置！');
        gameState.powerUps.hammer++;
        updatePowerUpUI();
        return;
    }
    
    gameState.score += 100;
    gameState.grid[row][col] = null;
    updateCellDisplay(row, col);
    
    showMessage('🔨 锤子敲击！获得 100 分！');
    
    setTimeout(() => fillGrid(), 300);
}

function useShuffle() {
    const allApples = [];
    
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            if (gameState.grid[row][col]) {
                allApples.push(gameState.grid[row][col]);
                gameState.grid[row][col] = null;
            }
        }
    }
    
    // Fisher-Yates洗牌算法
    for (let i = allApples.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [allApples[i], allApples[j]] = [allApples[j], allApples[i]];
    }
    
    let appleIndex = 0;
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            if (appleIndex < allApples.length) {
                gameState.grid[row][col] = allApples[appleIndex++];
                updateCellDisplay(row, col);
                
                const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
                if (cell) {
                    cell.style.animation = 'shuffleEffect 0.5s ease-out';
                    setTimeout(() => cell.style.animation = '', 500);
                }
            }
        }
    }
    
    if (!document.querySelector('#shuffleAnimation')) {
        const style = document.createElement('style');
        style.id = 'shuffleAnimation';
        style.textContent = `
            @keyframes shuffleEffect {
                0%, 100% { transform: scale(1) rotate(0deg); }
                50% { transform: scale(1.1) rotate(180deg); }
            }
        `;
        document.head.appendChild(style);
    }
    
    showMessage('🔄 棋盘已重新洗牌！');
}

function showRainbowEffect() {
    const gameGrid = document.getElementById('gameGrid');
    
    const rainbow = document.createElement('div');
    rainbow.style.cssText = `
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(45deg, 
            red 0%, orange 15%, yellow 30%, green 45%, 
            blue 60%, indigo 75%, violet 90%, red 100%);
        opacity: 0;
        animation: rainbowPulse 1s ease-out;
        pointer-events: none;
        border-radius: 15px;
    `;
    
    gameGrid.style.position = 'relative';
    gameGrid.appendChild(rainbow);
    
    if (!document.querySelector('#rainbowAnimation')) {
        const style = document.createElement('style');
        style.id = 'rainbowAnimation';
        style.textContent = `
            @keyframes rainbowPulse {
                0% { opacity: 0; transform: scale(0.8); }
                50% { opacity: 0.7; transform: scale(1.05); }
                100% { opacity: 0; transform: scale(1.2); }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => rainbow.remove(), 1000);
}

function showLightningEffect(row, col) {
    const gameGrid = document.getElementById('gameGrid');
    
    // 创建水平闪电
    const horizontalLightning = document.createElement('div');
    horizontalLightning.style.cssText = `
        position: absolute;
        top: ${(row / 8) * 100}%;
        left: 0;
        width: 100%;
        height: ${100/8}%;
        background: linear-gradient(90deg, transparent 0%, #ffeb3b 50%, transparent 100%);
        opacity: 0;
        animation: lightningFlash 0.8s ease-out;
        pointer-events: none;
    `;
    
    // 创建垂直闪电
    const verticalLightning = document.createElement('div');
    verticalLightning.style.cssText = `
        position: absolute;
        top: 0;
        left: ${(col / 8) * 100}%;
        width: ${100/8}%;
        height: 100%;
        background: linear-gradient(180deg, transparent 0%, #ffeb3b 50%, transparent 100%);
        opacity: 0;
        animation: lightningFlash 0.8s ease-out 0.2s;
        pointer-events: none;
    `;
    
    gameGrid.style.position = 'relative';
    gameGrid.appendChild(horizontalLightning);
    gameGrid.appendChild(verticalLightning);
    
    if (!document.querySelector('#lightningAnimation')) {
        const style = document.createElement('style');
        style.id = 'lightningAnimation';
        style.textContent = `
            @keyframes lightningFlash {
                0%, 100% { opacity: 0; }
                20%, 40%, 60% { opacity: 0.9; }
                30%, 50% { opacity: 0.3; }
            }
        `;
        document.head.appendChild(style);
    }
    
    setTimeout(() => {
        horizontalLightning.remove();
        verticalLightning.remove();
    }, 1000);
}

// 设置和界面功能
function showAchievements() {
    let html = `
        <div class="pause-content" style="max-height: 90vh; overflow-y: auto;">
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
                <h3 style="margin-bottom: 0.8rem;">📊 游戏统计</h3>
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
        <div class="pause-content" style="max-height: 90vh; overflow-y: auto;">
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
                    💕 Version 3.0 - Optimized Edition 💕
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

function toggleSound() {
    gameState.soundEnabled = !gameState.soundEnabled;
    saveGameData();
    showSettings();
    
    showMessage(gameState.soundEnabled ? '🔊 音效已开启' : '🔇 音效已关闭');
}

function clearGameData() {
    if (confirm('⚠️ 确定要清除所有游戏数据吗？\n这将删除所有成就和统计数据！')) {
        localStorage.removeItem('ashleyAppleGameData');
        
        gameState.achievements.clear();
        gameState.totalScore = 0;
        gameState.gamesPlayed = 0;
        gameState.perfectGames = 0;
        gameState.maxCombo = 0;
        
        showMessage('🗑️ 游戏数据已清除');
        showSettings();
    }
}

// 游戏控制
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
            <div style="display: flex; flex-direction: column; gap: 1rem; margin-top: 1.5rem;">
                <button class="menu-btn" onclick="resumeGame()">继续游戏 ▶️</button>
                <button class="menu-btn" onclick="restartLevel()">重新开始 🔄</button>
                <button class="menu-btn" onclick="showScreen('levelSelect'); closePauseMenu();">返回选关 ⬅️</button>
                <button class="menu-btn" onclick="showScreen('mainMenu'); closePauseMenu();">主菜单 🏠</button>
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

function showHint() {
    if (!gameState.isGameActive || gameState.isPaused) return;
    
    const possibleMoves = findPossibleMoves();
    if (possibleMoves.length === 0) {
        showMessage('💡 没有可行的移动，试试使用道具吧！');
        return;
    }
    
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

function findPossibleMoves() {
    const possibleMoves = [];
    
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
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
                
                gameState.grid[row][col + 1] = gameState.grid[row][col];
                gameState.grid[row][col] = temp;
            }
            
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
                
                gameState.grid[row + 1][col] = gameState.grid[row][col];
                gameState.grid[row][col] = temp;
            }
        }
    }
    
    return possibleMoves;
}

// 数据存储 (继续)
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

// 特殊日期检查
function checkSpecialDate() {
    const today = new Date();
    const month = today.getMonth() + 1;
    const day = today.getDate();
    
    // 可以添加特殊日期的彩蛋
    const specialDates = [
        { month: 2, day: 14, message: "💕 情人节快乐！Ashley，你是我的唯一！", effect: 'hearts' },
        { month: 12, day: 25, message: "🎄 圣诞快乐！愿我们永远幸福甜蜜！", effect: 'snow' },
        { month: 1, day: 1, message: "🎉 新年快乐！新的一年也要一起加油！", effect: 'fireworks' }
    ];
    
    const specialDate = specialDates.find(d => d.month === month && d.day === day);
    if (specialDate) {
        setTimeout(() => {
            showMessage(specialDate.message, 5000);
            createSpecialEffect(specialDate.effect);
        }, 1000);
    }
}

// 特殊效果
function createSpecialEffect(effect) {
    const container = document.getElementById('specialDateEffect');
    container.innerHTML = '';
    
    switch (effect) {
        case 'hearts':
            for (let i = 0; i < 20; i++) {
                const heart = document.createElement('div');
                heart.innerHTML = ['💕', '💖', '💗', '💝', '💘', '❤️'][Math.floor(Math.random() * 6)];
                heart.style.cssText = `
                    position: absolute;
                    font-size: 2rem;
                    left: ${Math.random() * 100}%;
                    animation: heartFloat ${Math.random() * 4 + 6}s linear infinite;
                    animation-delay: ${Math.random() * 5}s;
                    pointer-events: none;
                `;
                container.appendChild(heart);
            }
            break;
    }
}

// 设置事件监听器
function setupEventListeners() {
    // 防止页面滚动
    document.addEventListener('touchmove', function(e) {
        e.preventDefault();
    }, { passive: false });
    
    // 防止双击缩放
    document.addEventListener('gesturestart', function(e) {
        e.preventDefault();
    });
    
    // 监听设备方向改变
    window.addEventListener('orientationchange', function() {
        setTimeout(updateGameLayout, 100);
    });
    
    // 监听窗口大小改变
    window.addEventListener('resize', updateGameLayout);
    
    // 设置道具按钮
    setupPowerUpButtons();
    
    // 监听页面可见性变化
    document.addEventListener('visibilitychange', function() {
        if (document.hidden && gameState.isGameActive && !gameState.isPaused) {
            pauseGame();
        }
    });
}

// 更新游戏布局
function updateGameLayout() {
    // 确保游戏网格始终适应屏幕
    const gameGrid = document.getElementById('gameGrid');
    if (gameGrid) {
        const viewportHeight = window.innerHeight;
        const viewportWidth = window.innerWidth;
        const availableSize = Math.min(viewportWidth * 0.9, viewportHeight * 0.5);
        
        gameGrid.style.width = availableSize + 'px';
        gameGrid.style.height = availableSize + 'px';
    }
    
    // 强制重新计算布局
    setTimeout(() => {
        window.scrollTo(0, 0);
    }, 100);
}

// 性能优化函数
function optimizePerformance() {
    // 使用 requestAnimationFrame 优化动画
    let animationFrame;
    
    function animate() {
        // 这里可以放置需要持续更新的动画逻辑
        animationFrame = requestAnimationFrame(animate);
    }
    
    // 启动动画循环
    animate();
    
    // 在页面卸载时清理
    window.addEventListener('beforeunload', () => {
        if (animationFrame) {
            cancelAnimationFrame(animationFrame);
        }
    });
}

// 错误处理
window.addEventListener('error', function(e) {
    console.error('游戏错误:', e.error);
    showMessage('⚠️ 游戏出现了小问题，但不要担心，可以继续游戏！');
});

window.addEventListener('unhandledrejection', function(e) {
    console.error('未处理的Promise错误:', e.reason);
});

// PWA支持
if ('serviceWorker' in navigator) {
    window.addEventListener('load', function() {
        navigator.serviceWorker.register('/sw.js').then(function(registration) {
            console.log('SW registered: ', registration);
        }).catch(function(registrationError) {
            console.log('SW registration failed: ', registrationError);
        });
    });
}

// 触摸优化
function optimizeTouchHandling() {
    let touchStartTime;
    let touchStartPos;
    
    document.addEventListener('touchstart', function(e) {
        touchStartTime = Date.now();
        touchStartPos = {
            x: e.touches[0].clientX,
            y: e.touches[0].clientY
        };
    }, { passive: true });
    
    document.addEventListener('touchend', function(e) {
        const touchEndTime = Date.now();
        const touchDuration = touchEndTime - touchStartTime;
        
        // 如果触摸时间太长，可能是意外触摸
        if (touchDuration > 300) {
            e.preventDefault();
        }
    }, { passive: false });
}

// 内存管理
function manageMemory() {
    // 定期清理不需要的DOM元素
    setInterval(() => {
        const messages = document.querySelectorAll('.game-message');
        messages.forEach(msg => {
            if (msg.style.opacity === '0' || !msg.parentNode) {
                msg.remove();
            }
        });
        
        // 清理动画元素
        const animations = document.querySelectorAll('[style*="animation"]');
        animations.forEach(el => {
            if (el.style.animation === '') {
                el.removeAttribute('style');
            }
        });
    }, 30000);
}

// 初始化完整游戏
function initCompleteGame() {
    // 基础初始化
    initializeGame();
    
    // 性能优化
    optimizePerformance();
    optimizeTouchHandling();
    manageMemory();
    
    // 布局适配
    updateGameLayout();
    
    // 显示加载完成
    setTimeout(() => {
        showMessage('🎮 Ashley专属苹果消消乐已就绪！', 2000);
    }, 500);
}

// 页面加载完成后启动游戏
document.addEventListener('DOMContentLoaded', initCompleteGame);

// 导出游戏状态（用于调试）
window.gameDebug = {
    getState: () => gameState,
    unlockAllAchievements: () => {
        ACHIEVEMENTS.forEach(achievement => {
            unlockAchievement(achievement.id);
        });
    },
    addPowerUps: () => {
        Object.keys(gameState.powerUps).forEach(key => {
            gameState.powerUps[key] += 10;
        });
        updatePowerUpUI();
    },
    skipToLevel: (levelId) => {
        startLevel(levelId);
    }
};

</script>
</body>
</html>
