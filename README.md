# Girl_style_test
你的高定风格人格测试

<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>✨ 你的高定风格人格测试 ✨</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Lato:wght@300;400&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-pink: #F8E1E7; /* Chanel Pink */
            --primary-blue: #E3F2FD; /* Baby Blue */
            --text-dark: #333333;
            --accent-gold: #C5A059;
            --white: #FFFFFF;
        }

        body {
            font-family: 'Lato', sans-serif;
            background: linear-gradient(135deg, var(--primary-blue) 0%, var(--primary-pink) 100%);
            margin: 0;
            padding: 0;
            min-height: 100vh;
            color: var(--text-dark);
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            width: 90%;
            max-width: 450px;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            text-align: center;
            position: relative;
            border: 1px solid rgba(255, 255, 255, 0.8);
        }

        h1, h2 {
            font-family: 'Playfair Display', serif;
            color: #2c2c2c;
        }

        h1 { font-size: 24px; letter-spacing: 1px; margin-bottom: 10px; }
        .subtitle { font-size: 12px; color: #888; text-transform: uppercase; letter-spacing: 2px; margin-bottom: 30px; }

        .question-card { display: none; animation: fadeIn 0.5s ease; }
        .question-card.active { display: block; }

        .progress-bar {
            width: 100%;
            height: 4px;
            background: #eee;
            margin-bottom: 25px;
            border-radius: 2px;
        }
        .progress-fill {
            height: 100%;
            background: var(--accent-gold);
            width: 10%;
            transition: width 0.3s ease;
        }

        .option-btn {
            display: block;
            width: 100%;
            padding: 15px;
            margin: 12px 0;
            background: #fff;
            border: 1px solid #eee;
            border-radius: 12px;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.2s;
            text-align: left;
            color: #555;
            box-shadow: 0 2px 5px rgba(0,0,0,0.02);
        }

        .option-btn:hover {
            background: var(--primary-blue);
            border-color: var(--primary-blue);
            color: #333;
            transform: translateY(-2px);
        }

        .result-card { display: none; }
        
        .tag-badge {
            display: inline-block;
            padding: 4px 12px;
            background: var(--text-dark);
            color: #fff;
            font-size: 10px;
            border-radius: 20px;
            margin-bottom: 15px;
        }

        .radar-chart-placeholder {
            width: 200px;
            height: 200px;
            background: radial-gradient(circle, #fff 30%, #f9f9f9 70%);
            border-radius: 50%;
            margin: 20px auto;
            border: 1px dashed #ccc;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
        }
        
        .radar-label { font-size: 10px; position: absolute; color: #888; }
        .r-top { top: 10px; } .r-right { right: 10px; } .r-bottom { bottom: 10px; } .r-left { left: 10px; }

        .analysis-text {
            font-size: 13px;
            line-height: 1.6;
            text-align: left;
            background: #fcfcfc;
            padding: 15px;
            border-left: 3px solid var(--accent-gold);
            margin-top: 20px;
        }

        .btn-restart {
            margin-top: 30px;
            background: var(--text-dark);
            color: #fff;
            border: none;
            padding: 12px 30px;
            border-radius: 30px;
            font-family: 'Playfair Display', serif;
            cursor: pointer;
        }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

    </style>
</head>
<body>

<div class="container">
    <div id="quiz-section">
        <div class="subtitle">Style Archetype Assessment</div>
        <div class="progress-bar"><div class="progress-fill" id="progress"></div></div>
        
        <div id="question-container"></div>
    </div>

    <div id="result-section" class="result-card">
        <div class="subtitle">Your Style Identity</div>
        <h1 id="result-title"></h1>
        <div class="tag-badge" id="result-keywords"></div>
        
        <div class="radar-chart-placeholder">
            <div class="radar-label r-top">气场 (Aura)</div>
            <div class="radar-label r-right">流行 (Trend)</div>
            <div class="radar-label r-bottom">亲和 (Soft)</div>
            <div class="radar-label r-left">质感 (Quality)</div>
            <div id="chart-graphic" style="width: 100px; height: 100px; background: rgba(197, 160, 89, 0.2); transform: rotate(45deg); border: 2px solid var(--accent-gold);"></div>
        </div>

        <p id="result-desc" style="font-size: 14px; margin: 20px 0; font-style: italic;"></p>
        
        <div class="analysis-text">
            <strong>📊 专业风格分析:</strong><br>
            <span id="result-analysis"></span>
        </div>

        <button class="btn-restart" onclick="location.reload()">Replay Test</button>
    </div>
</div>

<script>
    const questions = [
        { q: "周末Brunch，你会首选哪种OOTD？", options: ["A. 粗花呢外套 + 珍珠 (人间富贵花)", "B. 紧身辣妹T + 工装裤 (回头率满分)", "C. 条纹衫 + 阔腿裤 (法式Chic)", "D. 奶油针织 + 碎花裙 (温柔滤镜)"] },
        { q: "你的梦中衣橱色盘是？", options: ["A. 黑白灰驼 (Timeless)", "B. 亮色/撞色 (Dopamine)", "C. 大地/莫兰迪 (Texture)", "D. 软糯粉蓝 (Soft Pastel)"] },
        { q: "最击中你的 Hashtag？", options: ["A. #OldMoney #CleanFit", "B. #Y2K #辣妹", "C. #松弛感 #Atmosphere", "D. #白月光 #Pure"] },
        { q: "出门必带的配饰？", options: ["A. 精致腕表/Logo腰带", "B. 亚克力/复古墨镜", "C. 帆布包/贝雷帽", "D. 锁骨链/毛绒发饰"] },
        { q: "今日妆容重点？", options: ["A. 哑光底妆 + 气场眉", "B. 截断眼妆 + 腮红", "C. 伪素颜 + 野生眉", "D. 卧蚕 + 玻璃唇"] },
        { q: "理想的 Crushed Date 地点？", options: ["A. 画廊/高级西餐", "B. 音乐节/游乐园", "C. 路边小酒馆", "D. 书店/海边"] },
        { q: "必须选一双鞋走完下半生？", options: ["A. 尖头高跟/乐福鞋", "B. 厚底鞋/限量球鞋", "C. 芭蕾平底/穆勒鞋", "D. 玛丽珍/小白鞋"] },
        { q: "朋友怎么评价你？", options: ["A. 自律/有品位", "B. 社牛/有趣", "C. 随和/文艺", "D. 乖巧/治愈"] },
        { q: "对“潮流”的态度？", options: ["A. 风格永存，只买经典", "B. 姐就是潮流，敢穿", "C. 不刻意追，只选适合的", "D. 偏向不易出错的安全牌"] },
        { q: "有预算优先投资什么？", options: ["A. 经典款大牌手袋", "B. 设计师联名/It Bag", "C. 极佳质感的羊绒大衣", "D. 贵妇护肤品"] }
    ];

    const results = {
        A: { title: "智性缪斯 (Old Money)", keywords: "#CleanFit #GossipGirl #Intellectual", desc: "你不需要过多的装饰，因为“你”本身就是最昂贵的单品。", analysis: "偏爱结构化剪裁和中性色调反映了你较高的‘自我监控’能力。你的穿搭传递出秩序感与权威感，推荐 Celine, Ralph Lauren 风格。" },
        B: { title: "辣味甜心 (Spicy Girl)", keywords: "#Y2K #Dopamine #Trendsetter", desc: "你是行走的荷尔蒙，自信且充满生命力。", analysis: "你的风格体现了情绪调节功能。高饱和度色彩能显著提升情绪唤醒度（Heller, Color Psychology）。推荐 Miu Miu, Diesel 风格。" },
        C: { title: "法式慵懒 (Parisian Chic)", keywords: "#Effortless #Atmosphere #Vibe", desc: "不仅是审美，更是一种‘L'art de vivre’的生活哲学。", analysis: "你追求‘不费力的时髦’，拒绝被消费主义裹挟。这种风格在心理学上显示了极高的内在自信与自我接纳。推荐 Jacquemus, Totême 风格。" },
        D: { title: "纯白月光 (Soft Romantic)", keywords: "#PureDesire #Cottagecore #Healing", desc: "你是人群中的情绪稳定剂，温柔得像加了柔光滤镜。", analysis: "柔和、圆润的线条容易引发他人的保护欲（Baby Schema Theory）。你通过服装营造安全、治愈的氛围。推荐 Dior, Chloé 风格。" }
    };

    let scores = { A: 0, B: 0, C: 0, D: 0 };
    let currentQ = 0;

    function init() {
        const container = document.getElementById('question-container');
        questions.forEach((q, index) => {
            const div = document.createElement('div');
            div.className = `question-card ${index === 0 ? 'active' : ''}`;
            div.id = `q-${index}`;
            div.innerHTML = `
                <h2>${q.q}</h2>
                ${q.options.map((opt, i) => `<button class="option-btn" onclick="answer('${String.fromCharCode(65+i)}')">${opt}</button>`).join('')}
            `;
            container.appendChild(div);
        });
    }

    function answer(choice) {
        scores[choice]++;
        const next = currentQ + 1;
        document.getElementById(`q-${currentQ}`).classList.remove('active');
        
        // Update Progress
        document.getElementById('progress').style.width = `${((next)/questions.length)*100}%`;

        if (next < questions.length) {
            currentQ = next;
            document.getElementById(`q-${next}`).classList.add('active');
        } else {
            showResult();
        }
    }

    function showResult() {
        document.getElementById('quiz-section').style.display = 'none';
        document.getElementById('result-section').style.display = 'block';
        
        // Calculate max score
        const winner = Object.keys(scores).reduce((a, b) => scores[a] > scores[b] ? a : b);
        const data = results[winner];
        
        document.getElementById('result-title').innerText = data.title;
        document.getElementById('result-keywords').innerText = data.keywords;
        document.getElementById('result-desc').innerText = data.desc;
        document.getElementById('result-analysis').innerText = data.analysis;
        
        // Adjust radar shape slightly based on result (visual gimmick)
        const shape = document.getElementById('chart-graphic');
        if(winner === 'A') shape.style.borderRadius = '0%'; // Square
        if(winner === 'B') shape.style.borderRadius = '30% 70% 70% 30% / 30% 30% 70% 70%'; // Spiky
        if(winner === 'C') shape.style.borderRadius = '40%'; // Soft square
        if(winner === 'D') shape.style.borderRadius = '50%'; // Circle
    }

    init();
</script>

</body>
</html>
