<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>抓娃娃计划 - 罗思维的睡梦星球</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial Rounded MT Bold', 'Segoe UI', sans-serif;
        }
        
        :root {
            --primary-pink: #FFB7C5;
            --light-pink: #FFE4E9;
            --soft-purple: #D8BFD8;
            --light-purple: #E6E6FA;
            --cream-yellow: #FFFACD;
            --warm-yellow: #FFECB3;
            --text-dark: #5A4A6A;
            --gold: #FFD700;
            --moon-blue: #7BB6E0;
            --star-pink: #FF8E9E;
            --gift-red: #FF6B8B;
            --gift-green: #6BCC8B;
        }
        
        body {
            background: linear-gradient(135deg, var(--cream-yellow) 0%, var(--light-pink) 50%, var(--light-purple) 100%);
            color: var(--text-dark);
            min-height: 100vh;
            padding: 15px;
            overflow-x: hidden;
            position: relative;
        }
        
        /* 背景漂浮元素 */
        .bg-floating {
            position: fixed;
            z-index: 0;
            pointer-events: none;
        }
        
        .bg-floating.star {
            width: 4px;
            height: 4px;
            background: var(--star-pink);
            clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
            animation: floatStar 20s infinite linear;
            opacity: 0.6;
        }
        
        .bg-floating.moon {
            width: 30px;
            height: 30px;
            background: var(--moon-blue);
            border-radius: 50%;
            animation: floatMoon 30s infinite linear;
            opacity: 0.2;
            box-shadow: 0 0 15px var(--moon-blue);
        }
        
        .bg-floating.heart {
            width: 15px;
            height: 15px;
            background: var(--primary-pink);
            clip-path: polygon(50% 0%, 100% 35%, 82% 100%, 50% 75%, 18% 100%, 0% 35%);
            animation: floatHeart 40s infinite linear;
            opacity: 0.3;
        }
        
        @keyframes floatStar {
            0% { transform: translate(0, 0) rotate(0deg); }
            100% { transform: translate(100vw, 100vh) rotate(360deg); }
        }
        
        @keyframes floatMoon {
            0% { transform: translate(0, 0) rotate(0deg); }
            25% { transform: translate(30vw, 40vh) rotate(90deg); }
            50% { transform: translate(60vw, 20vh) rotate(180deg); }
            75% { transform: translate(20vw, 60vh) rotate(270deg); }
            100% { transform: translate(0, 0) rotate(360deg); }
        }
        
        @keyframes floatHeart {
            0% { transform: translate(0, 0) scale(1); }
            33% { transform: translate(40vw, 30vh) scale(1.2); }
            66% { transform: translate(20vw, 50vh) scale(0.8); }
            100% { transform: translate(0, 0) scale(1); }
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            position: relative;
            z-index: 10;
        }
        
        /* 标题区域 - 移动端优化 */
        .header {
            text-align: center;
            margin-bottom: 20px;
            padding: 20px 15px;
            background: rgba(255, 255, 255, 0.85);
            border-radius: 20px;
            box-shadow: 0 8px 20px rgba(255, 183, 197, 0.3);
            border: 3px solid var(--primary-pink);
            position: relative;
            overflow: hidden;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 8px;
            background: linear-gradient(135deg, var(--star-pink), var(--soft-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 2px 2px 0px rgba(255, 255, 255, 0.8);
        }
        
        .title-decoration-text {
            font-size: 1.8rem;
            margin: 0 10px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            color: var(--soft-purple);
            margin-bottom: 10px;
            font-weight: bold;
        }
        
        .theme-text {
            font-size: 1.1rem;
            color: var(--star-pink);
            background: rgba(255, 255, 255, 0.7);
            padding: 6px 15px;
            border-radius: 15px;
            display: inline-block;
            border: 2px dashed var(--primary-pink);
        }
        
        /* 当前时间显示 */
        .current-time {
            font-size: 1.1rem;
            color: var(--star-pink);
            background: rgba(255, 255, 255, 0.7);
            padding: 8px 20px;
            border-radius: 20px;
            display: inline-block;
            border: 2px dashed var(--primary-pink);
            margin-top: 10px;
            font-weight: bold;
        }
        
        /* 娃娃机主体 - 移动端优化 */
        .claw-machine-container {
            background: linear-gradient(180deg, #FFB7C5 0%, #FF8E9E 100%);
            border-radius: 20px;
            padding: 20px 15px;
            box-shadow: 0 15px 25px rgba(255, 142, 158, 0.4);
            position: relative;
            overflow: hidden;
            margin-bottom: 20px;
            border: 5px solid white;
        }
        
        .machine-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(255, 255, 255, 0.9);
            padding: 12px 15px;
            border-radius: 12px;
            margin-bottom: 15px;
            border: 2px solid var(--warm-yellow);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }
        
        .energy-info {
            display: flex;
            flex-direction: column;
            gap: 6px;
            width: 70%;
        }
        
        .energy-label {
            font-size: 1rem;
            color: var(--star-pink);
            font-weight: bold;
        }
        
        .energy-bar-container {
            width: 100%;
            height: 20px;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 10px;
            overflow: hidden;
            border: 2px solid var(--primary-pink);
            position: relative;
        }
        
        .energy-bar {
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, var(--star-pink), var(--soft-purple));
            border-radius: 8px;
            transition: width 1s ease-out;
            position: relative;
            overflow: hidden;
        }
        
        .energy-bar::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
            animation: shimmer 2s infinite;
        }
        
        .energy-text {
            font-weight: bold;
            color: var(--star-pink);
            font-size: 1.3rem;
            text-shadow: 1px 1px 0 white;
        }
        
        /* 娃娃机视窗 - 移动端优化 */
        .claw-window {
            background: radial-gradient(circle at center, rgba(123, 182, 224, 0.2) 0%, rgba(255, 255, 255, 0.6) 70%);
            border: 3px solid white;
            border-radius: 15px;
            height: 220px;
            position: relative;
            overflow: hidden;
            margin-bottom: 15px;
            box-shadow: inset 0 0 15px rgba(0, 0, 0, 0.1);
        }
        
        .window-glass {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.1) 0%, rgba(255, 255, 255, 0.05) 100%);
            z-index: 1;
        }
        
        /* 爪子系统 */
        .claw-system {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 100%;
            z-index: 2;
        }
        
        .claw-rail {
            position: absolute;
            top: 15px;
            left: 50%;
            transform: translateX(-50%);
            width: 4px;
            height: 150px;
            background: var(--text-dark);
            border-radius: 2px;
        }
        
        .claw-arm {
            position: absolute;
            top: 15px;
            left: 50%;
            transform: translateX(-50%);
            width: 50px;
            height: 80px;
            transition: top 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
            z-index: 3;
        }
        
        .claw-head {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 35px;
            height: 15px;
            background: var(--text-dark);
            border-radius: 8px 8px 0 0;
            display: flex;
            justify-content: space-between;
            padding: 0 4px;
        }
        
        .claw-claw {
            width: 8px;
            height: 30px;
            background: var(--text-dark);
            border-radius: 4px;
            position: absolute;
            top: 15px;
        }
        
        .claw-claw.left {
            left: 4px;
            transform-origin: top center;
        }
        
        .claw-claw.right {
            right: 4px;
            transform-origin: top center;
        }
        
        /* 礼物盒娃娃 - 移动端优化 */
        .prize-doll {
            position: absolute;
            width: 80px;
            height: 100px;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            transition: bottom 0.8s cubic-bezier(0.34, 1.56, 0.64, 1);
            z-index: 2;
            filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.2));
        }
        
        .gift-box {
            position: relative;
            width: 100%;
            height: 100%;
            animation: breathe 3s infinite ease-in-out;
        }
        
        .gift-body {
            position: absolute;
            width: 60px;
            height: 50px;
            background: var(--gift-red);
            border-radius: 8px;
            top: 30px;
            left: 10px;
            border: 2px solid white;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .gift-lid {
            position: absolute;
            width: 70px;
            height: 15px;
            background: var(--gift-green);
            border-radius: 8px 8px 0 0;
            top: 15px;
            left: 5px;
            border: 2px solid white;
            border-bottom: none;
        }
        
        .gift-bow {
            position: absolute;
            width: 30px;
            height: 30px;
            top: 0;
            left: 25px;
        }
        
        .bow-center {
            position: absolute;
            width: 15px;
            height: 15px;
            background: var(--star-pink);
            border-radius: 50%;
            top: 7px;
            left: 7px;
            z-index: 2;
        }
        
        .bow-loop {
            position: absolute;
            width: 25px;
            height: 15px;
            background: var(--star-pink);
            border-radius: 50%;
        }
        
        .bow-loop.left {
            top: 4px;
            left: 0;
            transform: rotate(-30deg);
        }
        
        .bow-loop.right {
            top: 4px;
            right: 0;
            transform: rotate(30deg);
        }
        
        .bow-tail {
            position: absolute;
            width: 12px;
            height: 25px;
            background: var(--star-pink);
            border-radius: 8px;
            top: 15px;
        }
        
        .bow-tail.left {
            left: 4px;
            transform: rotate(-20deg);
        }
        
        .bow-tail.right {
            right: 4px;
            transform: rotate(20deg);
        }
        
        .gift-ribbon {
            position: absolute;
            width: 8px;
            height: 50px;
            background: var(--star-pink);
            border-radius: 4px;
            top: 30px;
        }
        
        .gift-ribbon.vertical {
            left: 36px;
        }
        
        .gift-ribbon.horizontal {
            width: 60px;
            height: 8px;
            top: 55px;
            left: 10px;
        }
        
        /* 投币孔网格 - 移动端优化 */
        .coin-grid-section {
            background: rgba(255, 255, 255, 0.9);
            padding: 20px 15px;
            border-radius: 15px;
            margin: 15px 0;
            border: 3px solid var(--primary-pink);
            box-shadow: 0 8px 15px rgba(255, 183, 197, 0.2);
        }
        
        .grid-title {
            text-align: center;
            color: var(--star-pink);
            margin-bottom: 15px;
            font-size: 1.3rem;
        }
        
        .coin-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 8px;
            max-width: 350px;
            margin: 0 auto;
        }
        
        .coin-slot {
            aspect-ratio: 1;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.5rem;
            color: rgba(90, 74, 106, 0.3);
            border: 2px solid var(--primary-pink);
            transition: all 0.5s ease;
            position: relative;
            cursor: pointer;
            box-shadow: 0 0 0 2px white;
        }
        
        .coin-slot::before {
            content: '';
            position: absolute;
            width: 80%;
            height: 80%;
            border: 2px dashed var(--soft-purple);
            border-radius: 50%;
        }
        
        .coin-slot.filled {
            background: var(--gold);
            color: white;
            border-color: #FFA500;
            transform: scale(1.1);
            box-shadow: 0 0 15px var(--gold);
        }
        
        .coin-slot.filled i {
            color: white;
        }
        
        .coin-slot.buff {
            border: 3px solid var(--gold);
            animation: pulse 1.5s infinite;
        }
        
        /* 睡眠时段卡片 - 移动端优化，点击直接打卡 */
        .sleep-cards {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin: 15px 0;
        }
        
        .sleep-card {
            background: rgba(255, 255, 255, 0.9);
            padding: 15px 8px;
            border-radius: 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 3px solid transparent;
            position: relative;
            overflow: hidden;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100px;
        }
        
        .sleep-card:hover, .sleep-card:active {
            transform: translateY(-5px) scale(1.03);
            border-color: currentColor;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        .sleep-card.perfect {
            color: var(--gold);
            background: rgba(255, 217, 61, 0.2);
        }
        
        .sleep-card.safe {
            color: var(--moon-blue);
            background: rgba(123, 182, 224, 0.2);
        }
        
        .sleep-card.late {
            color: #FFA500;
            background: rgba(255, 165, 0, 0.2);
        }
        
        .sleep-card.danger {
            color: #FF6B6B;
            background: rgba(255, 107, 107, 0.2);
        }
        
        .sleep-card.fail {
            color: #888;
            background: rgba(136, 136, 136, 0.2);
        }
        
        /* 禁用状态 */
        .sleep-card.disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none !important;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1) !important;
        }
        
        /* 当前可打卡状态 */
        .sleep-card.active {
            border: 3px solid currentColor;
            box-shadow: 0 0 20px currentColor;
            animation: pulse-active 2s infinite;
        }
        
        @keyframes pulse-active {
            0%, 100% { box-shadow: 0 0 20px currentColor; }
            50% { box-shadow: 0 0 30px currentColor; }
        }
        
        .card-icon {
            font-size: 2.2rem;
            margin-bottom: 8px;
        }
        
        .card-title {
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 4px;
        }
        
        .card-time {
            font-size: 0.9rem;
            opacity: 0.9;
            margin-bottom: 4px;
        }
        
        .card-effect {
            font-size: 0.8rem;
            opacity: 0.9;
        }
        
        /* 时间提示 */
        .time-hint {
            text-align: center;
            color: var(--star-pink);
            font-size: 1.1rem;
            margin: 10px 0;
            font-weight: bold;
        }
        
        /* 动态提示 - 移动端优化 */
        .dynamic-hint {
            text-align: center;
            padding: 20px 15px;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            margin: 15px 0;
            font-size: 1.3rem;
            color: var(--star-pink);
            border: 3px solid var(--primary-pink);
            box-shadow: 0 8px 15px rgba(255, 183, 197, 0.2);
            min-height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }
        
        /* 工具按钮 - 移动端优化 */
        .tool-buttons {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin: 15px 0;
        }
        
        .tool-btn {
            padding: 15px 8px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: all 0.3s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 6px;
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
            min-height: 70px;
        }
        
        .tool-btn:hover, .tool-btn:active {
            transform: translateY(-3px) scale(1.03);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.25);
        }
        
        .tool-btn.ticket {
            background: linear-gradient(135deg, var(--moon-blue), #7BB6E0);
            color: white;
        }
        
        .tool-btn.reminder {
            background: linear-gradient(135deg, var(--soft-purple), #D8BFD8);
            color: white;
        }
        
        .tool-btn.reset {
            background: linear-gradient(135deg, #FF6B6B, #FF6B6B);
            color: white;
        }
        
        .tool-btn i {
            font-size: 1.5rem;
        }
        
        /* 统计数据 - 移动端优化 */
        .stats-section {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin: 15px 0;
        }
        
        .stat-card {
            background: rgba(255, 255, 255, 0.9);
            padding: 20px 10px;
            border-radius: 15px;
            text-align: center;
            border: 3px solid var(--primary-pink);
            box-shadow: 0 8px 15px rgba(255, 183, 197, 0.2);
        }
        
        .stat-value {
            font-size: 2.2rem;
            font-weight: bold;
            color: var(--star-pink);
            margin-bottom: 5px;
        }
        
        .stat-label {
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        /* 弹窗 - 移动端优化 */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            padding: 15px;
        }
        
        .modal-content {
            background: linear-gradient(135deg, white, var(--light-pink));
            padding: 30px 20px;
            border-radius: 20px;
            text-align: center;
            max-width: 400px;
            width: 100%;
            transform: scale(0.8);
            animation: modalPop 0.4s forwards;
            border: 4px solid var(--primary-pink);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
        }
        
        .modal-icon {
            font-size: 4rem;
            margin-bottom: 15px;
        }
        
        .modal-title {
            font-size: 1.8rem;
            margin-bottom: 15px;
            color: var(--star-pink);
        }
        
        .modal-text {
            font-size: 1.3rem;
            margin-bottom: 20px;
            line-height: 1.5;
        }
        
        .modal-close {
            background: var(--star-pink);
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1.2rem;
            box-shadow: 0 4px 10px rgba(255, 142, 158, 0.5);
        }
        
        /* 特效 */
        .coin-effect {
            position: fixed;
            width: 25px;
            height: 25px;
            background: var(--gold);
            border-radius: 50%;
            z-index: 999;
            pointer-events: none;
            animation: coinDrop 1s forwards;
        }
        
        .star-burst {
            position: fixed;
            font-size: 2rem;
            z-index: 999;
            pointer-events: none;
            animation: starFly 1s forwards;
            color: var(--gold);
        }
        
        .repair-effect {
            position: fixed;
            width: 100px;
            height: 150px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 12px;
            z-index: 999;
            pointer-events: none;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 12px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
            border: 3px solid var(--moon-blue);
            animation: repairFly 1.5s forwards;
        }
        
        .repair-stamp {
            color: var(--moon-blue);
            font-size: 3rem;
            margin-bottom: 8px;
        }
        
        /* 平板和桌面端优化 */
        @media (min-width: 768px) {
            .sleep-cards {
                grid-template-columns: repeat(5, 1fr);
                gap: 15px;
            }
            
            .sleep-card {
                min-height: 120px;
                padding: 20px 10px;
            }
            
            .tool-buttons {
                grid-template-columns: repeat(3, 1fr);
                gap: 20px;
            }
            
            .tool-btn {
                flex-direction: row;
                padding: 15px 10px;
                min-height: 60px;
            }
            
            .stats-section {
                grid-template-columns: repeat(4, 1fr);
                gap: 15px;
            }
            
            h1 {
                font-size: 3rem;
            }
            
            .header {
                padding: 25px 20px;
            }
        }
        
        /* 小屏幕手机优化 */
        @media (max-width: 360px) {
            .sleep-cards {
                grid-template-columns: 1fr;
            }
            
            .coin-grid {
                grid-template-columns: repeat(5, 1fr);
                max-width: 280px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .title-decoration-text {
                font-size: 1.5rem;
            }
            
            .subtitle {
                font-size: 1rem;
            }
        }
        
        .footer {
            text-align: center;
            margin-top: 20px;
            padding: 15px;
            color: var(--soft-purple);
            font-size: 0.9rem;
            border-top: 2px dashed var(--primary-pink);
        }
        
        /* 震动效果 */
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            10%, 30%, 50%, 70%, 90% { transform: translateX(-5px); }
            20%, 40%, 60%, 80% { transform: translateX(5px); }
        }
        
        .shaking {
            animation: shake 0.5s;
        }
        
        /* 重置闪光 */
        @keyframes flash {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }
        
        .flashing {
            animation: flash 0.5s;
        }
    </style>
</head>
<body>
    <!-- 背景漂浮元素 -->
    <div id="bgContainer"></div>
    
    <div class="container">
        <!-- 标题区域 -->
        <div class="header">
            <h1><span class="title-decoration-text">🎀</span> 抓娃娃计划 <span class="title-decoration-text">🎀</span></h1>
            <div class="subtitle">21天养成早睡好习惯</div>
            <div class="theme-text">罗思维的睡梦星球</div>
            <div class="current-time" id="currentTime"></div>
        </div>
        
        <!-- 娃娃机主体 -->
        <div class="claw-machine-container">
            <div class="machine-top">
                <div class="energy-info">
                    <div class="energy-label">抓爪充能进度</div>
                    <div class="energy-bar-container">
                        <div class="energy-bar" id="energyBar"></div>
                    </div>
                </div>
                <div class="energy-text" id="energyText">0/21</div>
            </div>
            
            <!-- 娃娃机视窗 -->
            <div class="claw-window">
                <div class="window-glass"></div>
                
                <!-- 爪子系统 -->
                <div class="claw-system">
                    <div class="claw-rail"></div>
                    <div class="claw-arm" id="clawArm">
                        <div class="claw-head">
                            <div class="claw-claw left"></div>
                            <div class="claw-claw right"></div>
                        </div>
                    </div>
                </div>
                
                <!-- 礼物盒娃娃 -->
                <div class="prize-doll" id="prizeDoll">
                    <div class="gift-box">
                        <div class="gift-body"></div>
                        <div class="gift-lid"></div>
                        <div class="gift-ribbon vertical"></div>
                        <div class="gift-ribbon horizontal"></div>
                        <div class="gift-bow">
                            <div class="bow-center"></div>
                            <div class="bow-loop left"></div>
                            <div class="bow-loop right"></div>
                            <div class="bow-tail left"></div>
                            <div class="bow-tail right"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 投币孔网格 -->
        <div class="coin-grid-section">
            <h3 class="grid-title">睡梦星球投币孔 (每打卡一天点亮1个星星)</h3>
            <div class="coin-grid" id="coinGrid">
                <!-- 21个投币孔将由JS生成 -->
            </div>
        </div>
        
        <!-- 当前可打卡提示 -->
        <div class="time-hint" id="timeHint">
            请选择当前时间对应的睡眠时段打卡
        </div>
        
        <!-- 睡眠时段卡片 - 点击直接打卡 -->
        <div class="sleep-cards" id="sleepCards">
            <!-- 卡片将由JS生成 -->
        </div>
        
        <!-- 动态提示 -->
        <div class="dynamic-hint" id="dynamicHint">
            新手抓爪手报道！今天也要加油投币哦～
        </div>
        
        <!-- 工具按钮 -->
        <div class="tool-buttons">
            <button class="tool-btn ticket" id="ticketBtn">
                <i class="fas fa-ticket-alt"></i>
                <span>使用假条</span>
            </button>
            <button class="tool-btn reminder" id="reminderBtn">
                <i class="fas fa-bell"></i>
                <span>今日提醒</span>
            </button>
            <button class="tool-btn reset" id="resetBtn">
                <i class="fas fa-redo"></i>
                <span>重置当天</span>
            </button>
        </div>
        
        <!-- 统计数据 -->
        <div class="stats-section">
            <div class="stat-card">
                <div class="stat-value" id="currentStreak">0</div>
                <div class="stat-label">连续打卡天数</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="safeDays">0</div>
                <div class="stat-label">安全区打卡</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="remainingDays">21</div>
                <div class="stat-label">剩余天数</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="ticketCount">2</div>
                <div class="stat-label">剩余假条</div>
            </div>
        </div>
        
        <div class="footer">
            <p>💤 睡梦星球 | 设计：董纪君 | 目标：21天抓到可爱的礼物盒！</p>
        </div>
    </div>
    
    <!-- 弹窗 -->
    <div class="modal-overlay" id="modalOverlay">
        <div class="modal-content" id="modalContent">
            <div class="modal-icon" id="modalIcon"></div>
            <h3 class="modal-title" id="modalTitle"></h3>
            <p class="modal-text" id="modalText"></p>
            <button class="modal-close" id="modalClose">确定</button>
        </div>
    </div>

    <script>
        // 应用数据
        const appData = {
            currentStreak: 0,
            safeDays: 0,
            tickets: 2,
            energy: 0,
            selectedType: null,
            lastCheckinDate: null,
            todayChecked: false,
            todayType: null,
            todayUsedTicket: false,
            maxStreak: 21,
            history: []
        };
        
        // 睡眠时段配置 - 简化时间判断逻辑
        const sleepTypes = [
            {
                type: 'perfect',
                icon: '✨',
                title: '准时区',
                time: '23:30前',
                effect: '【强力抓爪】充能 + 2',
                description: '抓爪稳稳下降，牢牢抓住娃娃，减免1天进度！',
                energy: 2
            },
            {
                type: 'safe',
                icon: '✅',
                title: '安全区',
                time: '23:30-24:00',
                effect: '【正常投币】充能 + 1',
                description: '抓爪正常抓取，娃娃离你更近一步！',
                energy: 1
            },
            {
                type: 'late',
                icon: '🐢',
                title: '迟到区',
                time: '00:00-00:30',
                effect: '【抓爪打滑】需补能',
                description: '抓爪打滑晃悠，需要补打卡哦！',
                energy: 0
            },
            {
                type: 'danger',
                icon: '🔥',
                title: '高危区',
                time: '00:30-01:00',
                effect: '【机器故障】需额外补能',
                description: '机器故障，爪子不好用了！',
                energy: -1
            },
            {
                type: 'fail',
                icon: '💥',
                title: '失效区',
                time: '01:00后',
                effect: '【抓爪断裂】能量清零',
                description: '抓爪断裂，进度可能清零！可用维修券修复。',
                energy: -100
            }
        ];
        
        // 动态提示语
        const dynamicHints = [
            "新手抓爪手报道！今天也要加油投币哦～",
            "继续努力！每天早睡离娃娃更近一步！",
            "已经坚持3天了，好习惯正在养成！",
            "哇！你已经抓到一半的娃娃啦！继续保持～",
            "太棒了！离娃娃只有7步啦！别让抓爪打滑哦～",
            "最后一天！稳住！娃娃马上就是你的了！",
            "🎉 恭喜！成功抓到娃娃啦！你真是太棒了！"
        ];
        
        // 弹窗消息配置
        const modalMessages = {
            perfect: {
                icon: '✨',
                title: '超强抓爪！',
                text: '提前1天进度！娃娃离你更近了！'
            },
            safe: {
                icon: '✅',
                title: '投币成功！',
                text: '离娃娃更近一步～'
            },
            late: {
                icon: '😣',
                title: '哎呀，抓爪没抓稳',
                text: '需要补卡哦，下次要早点睡！'
            },
            danger: {
                icon: '😣',
                title: '机器故障！',
                text: '爪子打滑了，需要额外补能！'
            },
            fail: {
                icon: '😢',
                title: '抓爪坏了！',
                text: '别灰心，还有维修券可以用～'
            },
            ticket: {
                icon: '🛠️',
                title: '维修券使用成功！',
                text: '机器故障已修复，进度保留！'
            },
            reset: {
                icon: '🔄',
                title: '当天打卡已重置',
                text: '可以重新选择今天的睡眠时段打卡哦！'
            },
            win: {
                icon: '🎉',
                title: '恭喜！抓到娃娃啦！',
                text: '成功完成21天挑战！礼物盒是你的了！'
            },
            alreadyChecked: {
                icon: '⏰',
                title: '今日已打卡',
                text: '今天已经打卡过了哦，明天再来吧！'
            },
            notInTime: {
                icon: '⏰',
                title: '不在打卡时间',
                text: '当前时间不在这个睡眠时段内，请选择正确的时段打卡！'
            }
        };
        
        // 初始化函数
        function init() {
            createBackgroundElements();
            createCoinGrid();
            createSleepCards();
            setupEventListeners();
            loadData();
            updateUI();
            updateDynamicHint();
            updateCurrentTime();
            updateCardAvailability();
            
            // 每秒更新当前时间
            setInterval(() => {
                updateCurrentTime();
            }, 1000);
            
            // 每分钟更新卡片可用性
            setInterval(() => {
                updateCardAvailability();
            }, 60000);
        }
        
        // 更新当前时间显示
        function updateCurrentTime() {
            const now = new Date();
            const hours = now.getHours().toString().padStart(2, '0');
            const minutes = now.getMinutes().toString().padStart(2, '0');
            const seconds = now.getSeconds().toString().padStart(2, '0');
            document.getElementById('currentTime').textContent = `当前时间: ${hours}:${minutes}:${seconds}`;
        }
        
        // 检查当前时间是否在指定时间段内
        function isCurrentTimeInRange(type) {
            const now = new Date();
            const currentHour = now.getHours();
            const currentMinute = now.getMinutes();
            
            // 简化时间判断逻辑
            switch(type) {
                case 'perfect':
                    // 准时区：23:30前
                    if (currentHour < 23) return true;
                    if (currentHour === 23 && currentMinute < 30) return true;
                    return false;
                    
                case 'safe':
                    // 安全区：23:30-24:00
                    if (currentHour === 23 && currentMinute >= 30) return true;
                    if (currentHour === 0 && currentMinute === 0) return true; // 24:00就是0:00
                    return false;
                    
                case 'late':
                    // 迟到区：00:00-00:30
                    if (currentHour === 0 && currentMinute < 30) return true;
                    return false;
                    
                case 'danger':
                    // 高危区：00:30-01:00
                    if (currentHour === 0 && currentMinute >= 30) return true;
                    if (currentHour === 1 && currentMinute === 0) return true;
                    return false;
                    
                case 'fail':
                    // 失效区：01:00后
                    if (currentHour >= 1) return true;
                    return false;
                    
                default:
                    return false;
            }
        }
        
        // 更新卡片可用性
        function updateCardAvailability() {
            const cards = document.querySelectorAll('.sleep-card');
            let activeCards = 0;
            
            cards.forEach(card => {
                const cardType = card.dataset.type;
                
                // 如果今天已经打卡，禁用所有卡片
                if (appData.todayChecked) {
                    card.classList.remove('active');
                    card.classList.add('disabled');
                    card.style.cursor = 'not-allowed';
                    return;
                }
                
                // 检查当前时间是否在卡片对应的时间段内
                if (isCurrentTimeInRange(cardType)) {
                    card.classList.remove('disabled');
                    card.classList.add('active');
                    card.style.cursor = 'pointer';
                    activeCards++;
                } else {
                    card.classList.remove('active');
                    card.classList.add('disabled');
                    card.style.cursor = 'not-allowed';
                }
            });
            
            // 更新时间提示
            const timeHint = document.getElementById('timeHint');
            if (appData.todayChecked) {
                timeHint.textContent = '今天已经打卡过了，如需重新打卡请点击"重置当天"按钮';
                timeHint.style.color = '#888';
            } else if (activeCards > 0) {
                timeHint.textContent = '请选择当前时间对应的睡眠时段打卡';
                timeHint.style.color = 'var(--star-pink)';
            } else {
                timeHint.textContent = '当前时间没有可用的睡眠时段，请等待合适的睡眠时间';
                timeHint.style.color = '#888';
            }
        }
        
        // 创建背景漂浮元素
        function createBackgroundElements() {
            const container = document.getElementById('bgContainer');
            
            // 创建星星
            for (let i = 0; i < 15; i++) {
                const star = document.createElement('div');
                star.className = 'bg-floating star';
                star.style.left = Math.random() * 100 + 'vw';
                star.style.top = Math.random() * 100 + 'vh';
                star.style.animationDelay = Math.random() * 5 + 's';
                container.appendChild(star);
            }
            
            // 创建月亮
            for (let i = 0; i < 2; i++) {
                const moon = document.createElement('div');
                moon.className = 'bg-floating moon';
                moon.style.left = Math.random() * 100 + 'vw';
                moon.style.top = Math.random() * 100 + 'vh';
                moon.style.animationDelay = Math.random() * 10 + 's';
                container.appendChild(moon);
            }
        }
        
        // 创建投币孔网格
        function createCoinGrid() {
            const grid = document.getElementById('coinGrid');
            grid.innerHTML = '';
            
            for (let i = 0; i < 21; i++) {
                const slot = document.createElement('div');
                slot.className = 'coin-slot';
                slot.dataset.index = i;
                slot.innerHTML = '<i class="far fa-star"></i>';
                
                // 添加点击提示
                slot.addEventListener('click', () => {
                    if (i < appData.currentStreak) {
                        const dayType = appData.history[i] || '未知';
                        const typeInfo = sleepTypes.find(t => t.type === dayType) || {title: '未知'};
                        showMessage(`第${i+1}天打卡：${typeInfo.title}`);
                    } else {
                        showMessage(`还需要打卡${i+1 - appData.currentStreak}天才能点亮这个投币孔`);
                    }
                });
                
                grid.appendChild(slot);
            }
        }
        
        // 创建睡眠时段卡片
        function createSleepCards() {
            const container = document.getElementById('sleepCards');
            container.innerHTML = '';
            
            sleepTypes.forEach(type => {
                const card = document.createElement('div');
                card.className = `sleep-card ${type.type}`;
                card.dataset.type = type.type;
                
                card.innerHTML = `
                    <div class="card-icon">${type.icon}</div>
                    <div class="card-title">${type.title}</div>
                    <div class="card-time">${type.time}</div>
                    <div class="card-effect">${type.effect}</div>
                `;
                
                // 添加点击事件
                card.addEventListener('click', () => {
                    handleCardClick(type.type);
                });
                
                // 触摸设备优化
                card.addEventListener('touchstart', (e) => {
                    e.preventDefault();
                    if (!card.classList.contains('disabled')) {
                        card.style.transform = 'scale(0.98)';
                    }
                });
                
                card.addEventListener('touchend', (e) => {
                    e.preventDefault();
                    card.style.transform = '';
                });
                
                container.appendChild(card);
            });
        }
        
        // 处理卡片点击
        function handleCardClick(type) {
            // 如果今天已经打卡
            if (appData.todayChecked) {
                showModal('alreadyChecked');
                return;
            }
            
            // 检查当前时间是否在对应的时间段内
            if (!isCurrentTimeInRange(type)) {
                showModal('notInTime');
                return;
            }
            
            appData.selectedType = type;
            handleCheckin();
        }
        
        // 设置事件监听器
        function setupEventListeners() {
            // 使用假条按钮
            document.getElementById('ticketBtn').addEventListener('click', useTicket);
            
            // 今日提醒按钮
            document.getElementById('reminderBtn').addEventListener('click', showReminder);
            
            // 重置按钮
            document.getElementById('resetBtn').addEventListener('click', resetToday);
            
            // 弹窗关闭按钮
            document.getElementById('modalClose').addEventListener('click', () => {
                document.getElementById('modalOverlay').style.display = 'none';
            });
        }
        
        // 处理打卡
        function handleCheckin() {
            if (!appData.selectedType) return;
            
            const today = new Date().toDateString();
            
            // 检查今天是否已经打卡
            if (appData.todayChecked) {
                showModal('alreadyChecked');
                return;
            }
            
            // 记录今天已打卡
            appData.todayChecked = true;
            appData.todayType = appData.selectedType;
            appData.todayUsedTicket = false;
            
            // 显示投币动画
            showCoinAnimation();
            
            // 延迟执行抓取动画
            setTimeout(() => {
                performClawAnimation(appData.selectedType);
            }, 500);
        }
        
        // 显示投币动画
        function showCoinAnimation() {
            const cards = document.querySelectorAll('.sleep-card');
            const activeCard = Array.from(cards).find(card => card.dataset.type === appData.selectedType);
            
            if (!activeCard) return;
            
            const grid = document.getElementById('coinGrid');
            const targetSlot = grid.children[appData.currentStreak];
            
            if (!targetSlot) return;
            
            const cardRect = activeCard.getBoundingClientRect();
            const targetRect = targetSlot.getBoundingClientRect();
            
            // 创建多个硬币
            for (let i = 0; i < 3; i++) {
                setTimeout(() => {
                    const coin = document.createElement('div');
                    coin.className = 'coin-effect';
                    
                    // 从卡片位置飞到投币孔
                    const startX = cardRect.left + Math.random() * cardRect.width;
                    const startY = cardRect.top + Math.random() * cardRect.height;
                    const endX = targetRect.left + targetRect.width / 2;
                    const endY = targetRect.top + targetRect.height / 2;
                    
                    coin.style.setProperty('--startX', `${startX}px`);
                    coin.style.setProperty('--startY', `${startY}px`);
                    coin.style.setProperty('--endX', `${endX}px`);
                    coin.style.setProperty('--endY', `${endY}px`);
                    
                    document.body.appendChild(coin);
                    
                    setTimeout(() => coin.remove(), 1000);
                }, i * 100);
            }
        }
        
        // 执行爪子动画
        function performClawAnimation(type) {
            const clawArm = document.getElementById('clawArm');
            const prizeDoll = document.getElementById('prizeDoll');
            
            // 爪子下降
            clawArm.style.top = '120px';
            
            // 根据不同类型执行不同动画
            setTimeout(() => {
                switch(type) {
                    case 'perfect':
                        // 强力抓取
                        showStarBurst();
                        updateProgress(type);
                        setTimeout(() => showModal('perfect'), 500);
                        break;
                        
                    case 'safe':
                        // 正常抓取
                        updateProgress(type);
                        setTimeout(() => showModal('safe'), 500);
                        break;
                        
                    case 'late':
                    case 'danger':
                        // 打滑/故障
                        clawArm.classList.add('shaking');
                        setTimeout(() => clawArm.classList.remove('shaking'), 500);
                        updateProgress(type);
                        setTimeout(() => showModal(type), 500);
                        break;
                        
                    case 'fail':
                        // 断裂
                        clawArm.classList.add('shaking');
                        updateProgress(type);
                        setTimeout(() => showModal('fail'), 500);
                        break;
                }
                
                // 爪子上升
                setTimeout(() => {
                    clawArm.style.top = '15px';
                    
                    // 更新娃娃位置
                    updateDollPosition();
                }, 1000);
                
            }, 800);
        }
        
        // 显示星星特效
        function showStarBurst() {
            const cards = document.querySelectorAll('.sleep-card');
            const activeCard = Array.from(cards).find(card => card.dataset.type === appData.selectedType);
            
            if (!activeCard) return;
            
            const cardRect = activeCard.getBoundingClientRect();
            
            for (let i = 0; i < 5; i++) {
                setTimeout(() => {
                    const star = document.createElement('div');
                    star.className = 'star-burst';
                    star.innerHTML = '✨';
                    
                    const startX = cardRect.left + cardRect.width / 2;
                    const startY = cardRect.top + cardRect.height / 2;
                    const angle = (i / 5) * Math.PI * 2;
                    const distance = 80;
                    const endX = startX + Math.cos(angle) * distance;
                    const endY = startY + Math.sin(angle) * distance;
                    
                    star.style.setProperty('--startX', `${startX}px`);
                    star.style.setProperty('--startY', `${startY}px`);
                    star.style.setProperty('--endX', `${endX}px`);
                    star.style.setProperty('--endY', `${endY}px`);
                    
                    document.body.appendChild(star);
                    
                    setTimeout(() => star.remove(), 1000);
                }, i * 100);
            }
        }
        
        // 更新进度
        function updateProgress(type) {
            const sleepType = sleepTypes.find(t => t.type === type);
            if (!sleepType) return;
            
            // 记录打卡日期
            appData.lastCheckinDate = new Date().toDateString();
            
            // 更新能量
            appData.energy += sleepType.energy;
            if (appData.energy < 0) appData.energy = 0;
            
            // 处理不同类型
            switch(type) {
                case 'perfect':
                    appData.currentStreak += 2;
                    appData.safeDays++;
                    appData.history.push(type, type);
                    break;
                    
                case 'safe':
                    appData.currentStreak += 1;
                    appData.safeDays++;
                    appData.history.push(type);
                    break;
                    
                case 'late':
                case 'danger':
                    appData.history.push(type);
                    break;
                    
                case 'fail':
                    if (appData.tickets > 0) {
                        appData.tickets--;
                        appData.todayUsedTicket = true;
                        appData.currentStreak += 1;
                        appData.history.push(type);
                        showRepairEffect();
                    } else {
                        appData.currentStreak = 0;
                        appData.history = [];
                        clearCoinGrid();
                    }
                    break;
            }
            
            // 限制最大进度
            if (appData.currentStreak > appData.maxStreak) {
                appData.currentStreak = appData.maxStreak;
            }
            
            // 保存数据
            saveData();
            
            // 更新UI
            updateUI();
            updateCoinGrid();
            updateDynamicHint();
            
            // 检查是否完成挑战
            if (appData.currentStreak >= appData.maxStreak) {
                setTimeout(() => showModal('win'), 1000);
            }
        }
        
        // 更新娃娃位置
        function updateDollPosition() {
            const prizeDoll = document.getElementById('prizeDoll');
            const newBottom = 20 + (appData.currentStreak * 6);
            prizeDoll.style.bottom = `${Math.min(newBottom, 120)}px`;
        }
        
        // 显示维修特效
        function showRepairEffect() {
            const effect = document.createElement('div');
            effect.className = 'repair-effect';
            effect.innerHTML = `
                <div class="repair-stamp">✓</div>
                <div style="font-size: 0.8rem; color: #333; text-align: center;">
                    维修券使用成功<br>
                    剩余: ${appData.tickets}张
                </div>
            `;
            
            effect.style.left = '50%';
            effect.style.top = '50%';
            
            document.body.appendChild(effect);
            
            setTimeout(() => {
                effect.remove();
                showModal('ticket');
            }, 1500);
        }
        
        // 更新UI
        function updateUI() {
            // 更新统计数据
            document.getElementById('currentStreak').textContent = appData.currentStreak;
            document.getElementById('safeDays').textContent = appData.safeDays;
            document.getElementById('remainingDays').textContent = appData.maxStreak - appData.currentStreak;
            document.getElementById('ticketCount').textContent = appData.tickets;
            
            // 更新能量条
            const energyPercent = (appData.currentStreak / appData.maxStreak) * 100;
            document.getElementById('energyBar').style.width = `${energyPercent}%`;
            document.getElementById('energyText').textContent = `${appData.currentStreak}/${appData.maxStreak}`;
            
            // 更新娃娃位置
            updateDollPosition();
            
            // 更新卡片可用性
            updateCardAvailability();
            
            // 重置选择状态
            appData.selectedType = null;
        }
        
        // 更新投币孔网格
        function updateCoinGrid() {
            const slots = document.querySelectorAll('.coin-slot');
            
            slots.forEach((slot, index) => {
                if (index < appData.currentStreak) {
                    slot.classList.add('filled');
                    slot.innerHTML = '<i class="fas fa-star"></i>';
                    
                    if (appData.history[index] === 'perfect') {
                        slot.classList.add('buff');
                    }
                } else {
                    slot.classList.remove('filled', 'buff');
                    slot.innerHTML = '<i class="far fa-star"></i>';
                }
            });
        }
        
        // 清空投币孔
        function clearCoinGrid() {
            document.querySelectorAll('.coin-slot').forEach(slot => {
                slot.classList.remove('filled', 'buff');
                slot.innerHTML = '<i class="far fa-star"></i>';
            });
        }
        
        // 更新动态提示
        function updateDynamicHint() {
            const hintElement = document.getElementById('dynamicHint');
            let hint = '';
            
            if (appData.currentStreak >= 20) {
                hint = dynamicHints[5];
            } else if (appData.currentStreak >= 14) {
                hint = dynamicHints[4];
            } else if (appData.currentStreak >= 7) {
                hint = dynamicHints[3];
            } else if (appData.currentStreak >= 3) {
                hint = dynamicHints[2];
            } else if (appData.currentStreak > 0) {
                hint = dynamicHints[1];
            } else {
                hint = dynamicHints[0];
            }
            
            if (appData.currentStreak >= appData.maxStreak) {
                hint = dynamicHints[6];
            }
            
            hintElement.textContent = hint;
        }
        
        // 使用假条
        function useTicket() {
            if (appData.tickets <= 0) {
                showMessage('维修券已用完！');
                return;
            }
            
            appData.tickets--;
            appData.currentStreak = Math.max(0, appData.currentStreak - 1);
            saveData();
            updateUI();
            updateCoinGrid();
            
            showRepairEffect();
        }
        
        // 重置当天打卡
        function resetToday() {
            if (!appData.todayChecked) {
                showMessage('今天还没有打卡，无需重置！');
                return;
            }
            
            if (confirm('确定要重置今天的打卡记录吗？可以重新选择今天的睡眠时段打卡，并且会恢复假条数量。')) {
                document.querySelector('.container').classList.add('flashing');
                setTimeout(() => {
                    document.querySelector('.container').classList.remove('flashing');
                }, 500);
                
                const todayType = appData.todayType;
                
                if (todayType) {
                    switch(todayType) {
                        case 'perfect':
                            appData.currentStreak = Math.max(0, appData.currentStreak - 2);
                            appData.safeDays = Math.max(0, appData.safeDays - 1);
                            if (appData.history.length >= 2) {
                                appData.history.pop();
                                appData.history.pop();
                            }
                            break;
                            
                        case 'safe':
                            appData.currentStreak = Math.max(0, appData.currentStreak - 1);
                            appData.safeDays = Math.max(0, appData.safeDays - 1);
                            if (appData.history.length >= 1) {
                                appData.history.pop();
                            }
                            break;
                            
                        case 'fail':
                            appData.currentStreak = Math.max(0, appData.currentStreak - 1);
                            if (appData.history.length >= 1) {
                                appData.history.pop();
                            }
                            if (appData.todayUsedTicket && appData.tickets < 2) {
                                appData.tickets++;
                            }
                            break;
                            
                        default:
                            if (appData.history.length >= 1) {
                                appData.history.pop();
                            }
                            break;
                    }
                }
                
                appData.todayChecked = false;
                appData.todayType = null;
                appData.selectedType = null;
                appData.todayUsedTicket = false;
                
                saveData();
                updateUI();
                updateCoinGrid();
                updateDynamicHint();
                
                setTimeout(() => showModal('reset'), 300);
            }
        }
        
        // 显示今日提醒
        function showReminder() {
            const hour = new Date().getHours();
            let message = '';
            
            if (hour < 12) {
                message = '早上好！记得今晚要早点睡哦，23:30前睡觉可以减免1天进度！';
            } else if (hour < 18) {
                message = '下午好！今晚的计划是23:30前睡觉吗？坚持就是胜利！';
            } else if (hour < 22) {
                message = '晚上好！离睡觉时间越来越近了，准备好打卡了吗？';
            } else if (hour < 23) {
                message = '快23:00了，准备洗漱睡觉吧！早点睡对皮肤好哦~';
            } else if (hour < 24) {
                message = '马上到23:30了，抓紧时间睡觉！准时区打卡有奖励！';
            } else {
                message = '夜深了，尽量在00:00前睡觉，避免进入迟到区！';
            }
            
            showMessage(message);
        }
        
        // 显示弹窗
        function showModal(type) {
            const message = modalMessages[type];
            if (!message) return;
            
            document.getElementById('modalIcon').textContent = message.icon;
            document.getElementById('modalTitle').textContent = message.title;
            document.getElementById('modalText').textContent = message.text;
            document.getElementById('modalOverlay').style.display = 'flex';
        }
        
        // 显示消息
        function showMessage(text) {
            const messageBox = document.createElement('div');
            messageBox.style.cssText = `
                position: fixed;
                top: 20px;
                left: 50%;
                transform: translateX(-50%);
                background: rgba(255, 183, 197, 0.95);
                color: white;
                padding: 12px 20px;
                border-radius: 12px;
                z-index: 1000;
                font-weight: bold;
                border: 3px solid white;
                backdrop-filter: blur(5px);
                max-width: 80%;
                text-align: center;
                box-shadow: 0 8px 16px rgba(0,0,0,0.2);
            `;
            messageBox.textContent = text;
            document.body.appendChild(messageBox);
            
            setTimeout(() => messageBox.remove(), 3000);
        }
        
        // 保存数据到本地存储
        function saveData() {
            localStorage.setItem('sleepPlanetData', JSON.stringify(appData));
        }
        
        // 从本地存储加载数据
        function loadData() {
            const savedData = localStorage.getItem('sleepPlanetData');
            if (savedData) {
                const loadedData = JSON.parse(savedData);
                
                appData.currentStreak = loadedData.currentStreak || 0;
                appData.safeDays = loadedData.safeDays || loadedData.perfectDays || 0;
                appData.tickets = loadedData.tickets || 2;
                appData.energy = loadedData.energy || 0;
                appData.maxStreak = loadedData.maxStreak || 21;
                appData.history = loadedData.history || [];
                
                const today = new Date().toDateString();
                if (loadedData.lastCheckinDate !== today) {
                    appData.todayChecked = false;
                    appData.todayType = null;
                    appData.selectedType = null;
                    appData.todayUsedTicket = false;
                } else {
                    appData.todayChecked = loadedData.todayChecked || false;
                    appData.todayType = loadedData.todayType || null;
                    appData.todayUsedTicket = loadedData.todayUsedTicket || false;
                    appData.selectedType = null;
                }
                
                appData.lastCheckinDate = loadedData.lastCheckinDate || null;
            }
        }
        
        // 页面加载完成后初始化
        window.addEventListener('DOMContentLoaded', init);
        
        // 防止移动端双击放大
        let lastTouchEnd = 0;
        document.addEventListener('touchend', function(event) {
            const now = (new Date()).getTime();
            if (now - lastTouchEnd <= 300) {
                event.preventDefault();
            }
            lastTouchEnd = now;
        }, false);
    </script>
</body>
</html>
