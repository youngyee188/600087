<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>花园世界 - 公会鲜花图鉴</title>
    <!-- 引入 GitHub 风格的字体和图标（CDN 适配） -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/github-markdown-css@5.5.1/github-markdown.min.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css">
    <style>
        /* 基础重置 + GitHub 风格融合 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
        }
        body {
            background-color: #f8f9fa; /* GitHub 背景色 */
            background-image: linear-gradient(120deg, #f8f9fa 0%, #e9ecef 100%);
            padding: 16px;
            touch-action: manipulation;
            max-width: 1200px;
            margin: 0 auto; /* 居中显示，适配宽屏 */
        }
        /* 头部样式优化 */
        .garden-header {
            text-align: center;
            color: #24292e; /* GitHub 主色调 */
            margin-bottom: 20px;
            padding: 12px 0;
            border-bottom: 1px solid #e1e4e8; /* GitHub 分隔线风格 */
        }
        .garden-header h1 {
            font-size: 24px;
            margin-bottom: 8px;
            line-height: 1.3;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        .garden-header h1 i {
            color: #2ea44f; /* GitHub 绿色强调色 */
        }
        .garden-header p {
            font-size: 14px;
            color: #6a737d; /* GitHub 次要文本色 */
            line-height: 1.4;
        }
        /* 搜索框优化 - GitHub 输入框风格 */
        .search-box {
            width: 100%;
            max-width: 600px;
            margin: 0 auto 20px;
            position: relative;
        }
        .search-box input {
            width: 100%;
            padding: 12px 20px;
            border: 1px solid #d1d5da;
            border-radius: 6px; /* GitHub 输入框圆角 */
            outline: none;
            font-size: 14px;
            color: #24292e;
            background: #fff;
            box-shadow: inset 0 1px 2px rgba(27, 31, 35, 0.075);
        }
        .search-box input:focus {
            border-color: #2188ff;
            box-shadow: 0 0 0 3px rgba(3, 105, 161, 0.1);
        }
        .search-box input::placeholder {
            color: #959da5;
        }
        /* 统计区域 - GitHub 卡片风格 */
        .score-count {
            width: 100%;
            max-width: 100%;
            margin: 0 auto 20px;
            padding: 16px;
            background: #fff;
            border-radius: 6px;
            border: 1px solid #e1e4e8;
            text-align: center;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 12px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
        }
        .count-item {
            flex: 1;
            min-width: 80px;
            margin: 0;
        }
        .count-item p {
            font-size: 12px;
            color: #6a737d;
            margin-bottom: 4px;
            font-weight: 500;
        }
        .count-number {
            font-size: 18px;
            font-weight: 600;
            color: #24292e;
        }
        /* 鲜花列表 - 响应式优化（PC 4列，平板2列，手机1列） */
        .flower-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 16px;
            max-width: 100%;
            margin: 0 auto;
        }
        /* 鲜花卡片 - GitHub 卡片风格优化 */
        .flower-card {
            background: #fff;
            border-radius: 6px;
            padding: 12px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
            transition: all 0.2s ease;
            border: 1px solid #e1e4e8;
            height: 120px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }
        .flower-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            border-color: #d1d5da;
        }
        .flower-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 100%;
            margin-bottom: 8px;
            gap: 8px;
        }
        .flower-name {
            font-size: 13px;
            color: #24292e;
            font-weight: 600;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            flex: 1;
            text-align: left;
            line-height: 1.2;
        }
        .flower-score {
            font-size: 16px;
            font-weight: 600;
            min-width: 38px;
            text-align: center;
            line-height: 1.2;
            padding: 2px 4px;
            border-radius: 3px;
        }
        .flower-rarity {
            font-size: 10px;
            padding: 2px 6px;
            border-radius: 12px;
            display: inline-block;
            line-height: 1.2;
            min-width: 40px;
            text-align: center;
            font-weight: 500;
        }
        /* 分数颜色 - 适配 GitHub 配色 */
        .score-14 { 
            color: #0366d6; 
            background-color: #e6f7ff;
        }
        .score-21, .score-23 { 
            color: #6f42c1; 
            background-color: #f3e8ff;
        }
        .score-25 { 
            color: #d93f0b; 
            background-color: #fff3cd;
        }
        .score-28, .score-30 { 
            color: #d73a4a; 
            background-color: #fce4ec;
        }
        /* 成员区域优化 */
        .flower-members {
            font-size: 12px;
            color: #24292e;
            font-weight: 500;
            line-height: 1.6;
            border-top: 1px dashed #e1e4e8;
            padding-top: 8px;
            margin-top: 4px;
            flex: 1;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
        }
        .member-label {
            font-size: 11px;
            color: #6a737d;
            display: block;
            margin-bottom: 2px;
        }
        /* 稀有度标签配色 - 更鲜明的区分 */
        .rarity-normal { 
            background: #e6f7ff; 
            color: #0366d6; 
        }
        .rarity-rare { 
            background: #f3e8ff; 
            color: #6f42c1; 
        }
        .rarity-epic { 
            background: #fff3cd; 
            color: #d93f0b; 
        }
        .rarity-legend { 
            background: #fce4ec; 
            color: #d73a4a; 
        }
        /* 空状态优化 */
        .empty-tip {
            text-align: center;
            color: #6a737d;
            font-size: 16px;
            margin-top: 60px;
            padding: 20px 12px;
            background: #fff;
            border-radius: 6px;
            border: 1px solid #e1e4e8;
        }
        .empty-tip i {
            font-size: 24px;
            margin-bottom: 8px;
            display: block;
            color: #959da5;
        }
        /* 底部版权信息（GitHub 风格） */
        .footer {
            text-align: center;
            margin-top: 40px;
            padding: 16px 0;
            border-top: 1px solid #e1e4e8;
            color: #6a737d;
            font-size: 12px;
        }
        .footer a {
            color: #0366d6;
            text-decoration: none;
            margin: 0 4px;
        }
        .footer a:hover {
            text-decoration: underline;
        }
        /* 适配打印样式 */
        @media print {
            body {
                background: #fff;
                padding: 0;
            }
            .flower-list {
                grid-template-columns: repeat(3, 1fr);
            }
            .flower-card {
                box-shadow: none;
                border: 1px solid #ddd;
            }
            .search-box, .footer {
                display: none;
            }
        }
    </style>
</head>
<body>
    <div class="garden-header">
        <h1><<i class="fa fa-pagelines" aria-hidden="true"></</i> 花园世界 - 公会鲜花图鉴</h1>
        <p>共收录 238 种鲜花 | 支持搜索花名/成员 | <a href="https://github.com" target="_blank" rel="noopener noreferrer">GitHub 仓库</a></p>
    </div>

    <div class="search-box">
        <input type="text" id="flowerSearch" placeholder="输入鲜花名称或成员名字搜索...">
    </div>

    <div class="score-count">
        <div class="count-item">
            <p>总鲜花数</p>
            <div class="count-number" id="totalCount">0</div>
        </div>
        <div class="count-item">
            <p>普通 (14分)</p>
            <div class="count-number score-14" id="normalCount">0</div>
        </div>
        <div class="count-item">
            <p>紫花 (21/23分)</p>
            <div class="count-number score-21" id="rareCount">0</div>
        </div>
        <div class="count-item">
            <p>金花 (25分)</p>
            <div class="count-number score-25" id="epicCount">0</div>
        </div>
        <div class="count-item">
            <p>红花 (28/30分)</p>
            <div class="count-number score-28" id="legendCount">0</div>
        </div>
    </div>

    <div class="flower-list" id="flowerList"></div>

    <div class="footer">
        <p>© 2024 花园世界公会 | 数据实时更新 | <a href="https://github.com/your-username/your-repo" target="_blank" rel="noopener noreferrer"><<i class="fa fa-github" aria-hidden="true"></</i> 源码地址</a></p>
    </div>

    <script>
        // 核心数据区（保持原数据不变）
        const flowerData = [
            // 14分 普通花 (Normal)
            { name: "薄粉蕙兰", score: 14, rarity: "normal", members: [ "贝儿", "珊珊"] },
            { name: "忽地笑", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "月白格桑花", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "紫麦冬花", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "绿叶苏铁", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "金钟连翘", score: 14, rarity: "normal", members: ["贝儿", "珊珊"] },
            { name: "香水百合", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "凤梨花", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "迎春花", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "红鹤芋", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "白鹤芋", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "明黄矮牵牛", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "淡粉矮牵牛", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "白色满天星", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "粉色满天星", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "蓝色满天星", score: 14, rarity: "normal", members: [] },
            { name: "粉矢车菊", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "蓝矢车菊", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "紫矢车菊", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "浅紫落新妇", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "水红落新妇", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "浅蓝落新妇", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "浅白乒乓菊", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "浅橘乒乓菊", score: 14, rarity: "normal", members: [] },
            { name: "浅粉乒乓菊", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "素雪玉簪花", score: 14, rarity: "normal", members: [] },
            { name: "紫晶玉簪花", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "霜蓝玉簪花", score: 14, rarity: "normal", members: [] },
            { name: "淡茜蜀葵花", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "金盏蜀葵花", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "丹红蜀葵花", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "淡粉非洲堇", score: 14, rarity: "normal", members: [] },
            { name: "轻紫非洲堇", score: 14, rarity: "normal", members: [] },
            { name: "玫红非洲堇", score: 14, rarity: "normal", members: [] },
            { name: "绛红报春花", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "桃粉报春花", score: 14, rarity: "normal", members: [] },
            { name: "鹅黄报春花", score: 14, rarity: "normal", members: ["贝儿"] },
            { name: "丹紫夹竹桃", score: 14, rarity: "normal", members: [] },
            { name: "浅粉夹竹桃", score: 14, rarity: "normal", members: [] },
            { name: "黄色海棠花", score: 14, rarity: "normal", members: [] },
            { name: "橘红海棠花", score: 14, rarity: "normal", members: [] },
            { name: "紫红杜鹃", score: 14, rarity: "normal", members: [] },
            { name: "嫣红杜鹃", score: 14, rarity: "normal", members: [] },
            { name: "杏黄杜鹃", score: 14, rarity: "normal", members: [] },
            { name: "绯雪杰奎琳", score: 14, rarity: "normal", members: [] },
            { name: "桃夭杰奎琳", score: 14, rarity: "normal", members: [] },
            { name: "碧落杰奎琳", score: 14, rarity: "normal", members: [] },
            { name: "薄藤铁线莲", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "正红大丽花", score: 14, rarity: "normal", members: ["贝儿"] },
            { name: "殷红灯笼花", score: 14, rarity: "normal", members: [] },
            { name: "雾粉千鸟花", score: 14, rarity: "normal", members: [] },
            { name: "圣诞一品红", score: 14, rarity: "normal", members: [] },
            { name: "粉色酢浆草", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "黄白酢浆草", score: 14, rarity: "normal", members: [] },
            { name: "橙黄酢浆草", score: 14, rarity: "normal", members: ["贝儿"] },
            { name: "嫩黄马齿苋", score: 14, rarity: "normal", members: [] },
            { name: "白花马齿苋", score: 14, rarity: "normal", members: ["贺靖荷", "贝儿"] },
            { name: "星蓝婆婆纳", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "浅粉婆婆纳", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "梦蓝香豌豆", score: 14, rarity: "normal", members: [] },
            { name: "雾白香豌豆", score: 14, rarity: "normal", members: ["贺靖荷"] },
            { name: "轻紫翠珠", score: 14, rarity: "normal", members: [] },
            { name: "盈粉翠珠", score: 14, rarity: "normal", members: [] },
            { name: "银白翠珠", score: 14, rarity: "normal", members: [] },
            { name: "橘粉忘忧草", score: 14, rarity: "normal", members: [] },
            { name: "轻紫忘忧草", score: 14, rarity: "normal", members: [] },
            { name: "杏白忘忧草", score: 14, rarity: "normal", members: [] },
            { name: "朱橙魔杖花", score: 14, rarity: "normal", members: [] },
            // 21/23分 稀有花 (Rare)
            { name: "黛紫玉兰", score: 23, rarity: "rare", members: ["瑶瑶"] },
            { name: "鸳鸯茉莉", score: 21, rarity: "rare", members: ["凉薄", "小曹睡不着", "一夜星光", "贝儿", "珊珊", "余念凉"] },
            { name: "香槟玫瑰", score: 21, rarity: "rare", members: ["凉薄", "豆豆", "在燕然菲", "蛙哒瓜嚓", "一一", "吟风客", "珊珊"] },
            { name: "月影摇光", score: 23, rarity: "rare", members: [] },
            { name: "星耀灵蕊", score: 21, rarity: "rare", members: ["南宫静梅"] },
            { name: "玛瑙石榴花", score: 21, rarity: "rare", members: [] },
            { name: "幻紫铁线莲", score: 23, rarity: "rare", members: ["初见", "贺靖荷"] },
            { name: "冰蓝黑种草", score: 21, rarity: "rare", members: [] },
            { name: "双辉忍冬", score: 21, rarity: "rare", members: ["一一"] },
            { name: "紫苑番红花", score: 21, rarity: "rare", members: ["一一"] },
            { name: "玉紫雪割草", score: 21, rarity: "rare", members: [] },
            { name: "瑶晖缅栀子", score: 21, rarity: "rare", members: [] },
            { name: "绯色腊梅", score: 21, rarity: "rare", members: ["土豆花", "凉薄", "豆豆", "一一", "吟风客", "珊珊"] },
            { name: "蓝叶苏铁", score: 21, rarity: "rare", members: ["初见", "花瑶", "珊珊"] },
            { name: "粉米露薇花", score: 23, rarity: "rare", members: ["一一"] },
            { name: "冰蓝矮牵牛", score: 21, rarity: "rare", members: ["耶律洛妃", "小曹睡不着", "桃桃", "在燕然菲", "一一", "贺靖荷", "花瑶"] },
            { name: "轮生冬青", score: 21, rarity: "rare", members: ["耶律洛妃", "小曹睡不着", "桃桃", "一夜星光", "在燕然菲", "蛙哒瓜嚓", "贺靖荷", "贝儿", "花瑶"] },
            { name: "粉色木槿花", score: 21, rarity: "rare", members: ["耶律洛妃", "小曹睡不着", "桃桃", "瑶瑶", "一夜星光", "在燕然菲", "蛙哒瓜嚓", "贺靖荷", "贝儿", "花瑶"] },
            { name: "粉胭海棠花", score: 21, rarity: "rare", members: ["一一"] },
            { name: "赤焰火焰兰", score: 21, rarity: "rare", members: ["凉薄", "桃桃", "一夜星光", "贝儿"] },
            { name: "轻紫大葱花", score: 21, rarity: "rare", members: ["宇文半青", "土豆花", "桃桃", "一夜星光", "一一", "贝儿"] },
            { name: "碧落夹竹桃", score: 23, rarity: "rare", members: ["一一"] },
            { name: "粉鹤芋", score: 21, rarity: "rare", members: ["土豆花", "小曹睡不着"] },
            { name: "蜜合月见草", score: 21, rarity: "rare", members: ["初见"] },
            { name: "粉樱月见草", score: 21, rarity: "rare", members: ["桃桃", "豆豆", "在燕然菲", "一一", "吟风客", "珊珊", "余念凉"] },
            { name: "碧落月见草", score: 21, rarity: "rare", members: ["凉薄", "桃桃", "在燕然菲", "一一", "花瑶"] },
            { name: "樱红跳舞兰", score: 23, rarity: "rare", members: ["神兜兜", "初见"] },
            { name: "明黄跳舞兰", score: 21, rarity: "rare", members: ["宇文半青", "耶律洛妃", "桃桃"] },
            { name: "奶桃大丽花", score: 21, rarity: "rare", members: ["土豆花", "小曹睡不着", "紫火祥云"] },
            { name: "黑曜大丽花", score: 21, rarity: "rare", members: ["土豆花", "蛙哒瓜嚓", "吟风客", "珊珊"] },
            { name: "白粉蕙兰", score: 21, rarity: "rare", members: ["土豆花", "一夜星光", "豆豆", "贝儿"] },
            { name: "春绿蕙兰", score: 23, rarity: "rare", members: ["神兜兜", "瑶瑶"] },
            { name: "雾粉麦冬花", score: 21, rarity: "rare", members: ["小曹睡不着"] },
            { name: "霜色麦冬花", score: 23, rarity: "rare", members: ["一一"] },
            { name: "紫晶灯笼花", score: 23, rarity: "rare", members: ["神兜兜", "初见"] },
            { name: "落霞灯笼花", score: 23, rarity: "rare", members: ["紫火祥云"] },
            { name: "烟粉格桑花", score: 23, rarity: "rare", members: ["南宫静梅"] },
            { name: "轻紫格桑花", score: 23, rarity: "rare", members: ["瑶瑶", "一一"] },
            { name: "粉黛德鸢", score: 21, rarity: "rare", members: ["夏夜", "紫火祥云"] },
            { name: "金白德鸢", score: 21, rarity: "rare", members: ["花瑶"] },
            { name: "杏绯德鸢", score: 21, rarity: "rare", members: ["一一"] },
            { name: "鹅黄铁筷花", score: 21, rarity: "rare", members: [] },
            { name: "褐红铁筷花", score: 21, rarity: "rare", members: ["土豆花", "耶律洛妃", "一一", "吟风客"] },
            { name: "粉菲铁筷花", score: 23, rarity: "rare", members: [] },
            { name: "毛蕊紫银莲", score: 21, rarity: "rare", members: ["土豆花", "一一"] },
            { name: "玫瑰粉银莲", score: 21, rarity: "rare", members: ["神兜兜", "花瑶"] },
            { name: "黑蕊银莲花", score: 21, rarity: "rare", members: ["在燕然菲", "贝儿"] },
            { name: "浅黄绿绒蒿", score: 21, rarity: "rare", members: ["土豆花", "桃桃", "瑶瑶", "贝儿"] },
            { name: "幽蓝绿绒蒿", score: 21, rarity: "rare", members: ["神兜兜", "一一", "贝儿"] },
            { name: "黛紫绿绒蒿", score: 23, rarity: "rare", members: ["初见"] },
            { name: "霜白海葵", score: 23, rarity: "rare", members: ["瑶瑶"] },
            { name: "烟绯海葵", score: 21, rarity: "rare", members: ["宇文半青", "小曹睡不着", "吟风客"] },
            { name: "金橙海葵", score: 21, rarity: "rare", members: ["宇文半青"] },
            { name: "粉紫华珊", score: 21, rarity: "rare", members: ["宇文半青", "夏夜", "苏息", "神兜兜"] },
            { name: "橘霞华珊", score: 21, rarity: "rare", members: ["宇文半青", "神兜兜"] },
            { name: "青碧华珊", score: 21, rarity: "rare", members: ["神兜兜", "一一", "珊珊", "余念凉"] },
            { name: "白茜剑兰", score: 21, rarity: "rare", members: ["花瑶"] },
            { name: "芋紫剑兰", score: 21, rarity: "rare", members: ["一一", "花瑶"] },
            { name: "橙心剑兰", score: 23, rarity: "rare", members: [] },
            { name: "胭脂芍药", score: 23, rarity: "rare", members: ["耶律洛妃", "一夜星光", "花瑶", "吟风客"] },
            { name: "云锦芍药", score: 21, rarity: "rare", members: ["小曹睡不着", "一一"] },
            { name: "盈粉芍药", score: 21, rarity: "rare", members: [] },
            { name: "纯白木香花", score: 23, rarity: "rare", members: ["南宫静梅", "一一"] },
            { name: "桃云木香花", score: 23, rarity: "rare", members: ["南宫静梅", "夏夜"] },
            { name: "春晓木香花", score: 23, rarity: "rare", members: ["南宫静梅", "夏夜"] },
            { name: "曼陀罗华", score: 21, rarity: "rare", members: ["宇文半青", "凉薄", "桃桃"] },
            { name: "曼珠沙华", score: 21, rarity: "rare", members: ["没事种花", "凉薄", "神兜兜"] },
            { name: "粉羽朱顶红", score: 23, rarity: "rare", members: ["神兜兜"] },
            { name: "火蕊朱顶红", score: 23, rarity: "rare", members: ["一一"] },
            { name: "橘光朱顶红", score: 23, rarity: "rare", members: ["一一"] },
            { name: "柔蓝飞燕草", score: 23, rarity: "rare", members: ["一一"] },
            { name: "绀紫飞燕草", score: 21, rarity: "rare", members: ["宇文半青", "苏息", "一夜星光"] },
            { name: "桃夭飞燕草", score: 23, rarity: "rare", members: ["吟风客"] },
            { name: "藕粉长寿花", score: 23, rarity: "rare", members: ["神兜兜"] },
            { name: "半见长寿花", score: 21, rarity: "rare", members: ["土豆花", "在燕然菲", "一一", "珊珊"] },
            { name: "朱柿长寿花", score: 21, rarity: "rare", members: ["土豆花", "在燕然菲"] },
            { name: "青山银桂", score: 21, rarity: "rare", members: ["土豆花", "初见"] },
            { name: "波叶金桂", score: 21, rarity: "rare", members: ["宇文半青", "初见", "一一", "珊珊"] },
            { name: "朱砂丹桂", score: 21, rarity: "rare", members: ["土豆花", "神兜兜", "在燕然菲", "初见"] },
            { name: "蜜桃花毛茛", score: 23, rarity: "rare", members: ["温贝贝", "紫火祥云", "一一"] },
            { name: "橙霞花毛茛", score: 23, rarity: "rare", members: ["贺靖荷"] },
            { name: "奶黄花毛茛", score: 23, rarity: "rare", members: [] },
            { name: "浅绀紫藤花", score: 23, rarity: "rare", members: [] },
            { name: "暮粉紫藤花", score: 23, rarity: "rare", members: [] },
            { name: "霁蓝紫藤花", score: 21, rarity: "rare", members: [] },
            { name: "紫苑凤眼莲", score: 23, rarity: "rare", members: [] },
            { name: "凝夜紫薇", score: 21, rarity: "rare", members: [] },
            { name: "桃夭美人蕉", score: 21, rarity: "rare", members: [] },
            { name: "暮山耧斗菜", score: 23, rarity: "rare", members: [] },
            { name: "晴蓝耧斗菜", score: 21, rarity: "rare", members: ["孟乐双"] },
            { name: "丹红耧斗菜", score: 23, rarity: "rare", members: ["孟乐双"] },
            { name: "橘焰冠华", score: 21, rarity: "rare", members: ["孟乐双"] },
            { name: "岚岫紫云英", score: 23, rarity: "rare", members: ["孟乐双"] },
            { name: "银白雪柳", score: 23, rarity: "rare", members: ["夏夜", "神兜兜", "紫火祥云"] },
            { name: "淡粉雪柳", score: 23, rarity: "rare", members: ["一一"] },
            { name: "飞黄玉兰", score: 23, rarity: "rare", members: ["苏息", "初见", "一一"] },
            { name: "甜橙美女樱", score: 23, rarity: "rare", members: ["土豆花", "桃桃", "一一"] },
            { name: "浅韵美女樱", score: 23, rarity: "rare", members: ["凉薄", "苏息", "一一"] },
            { name: "藤黄露薇花", score: 21, rarity: "rare", members: ["一夜星光", "在燕然菲"] },
            { name: "莹白露薇花", score: 21, rarity: "rare", members: ["土豆花", "紫火祥云", "一夜星光"] },
            { name: "晴山蔷薇花", score: 23, rarity: "rare", members: ["神兜兜", "一一", "吟风客"] },
            { name: "夕岚蔷薇花", score: 21, rarity: "rare", members: ["在燕然菲"] },
            { name: "黄莺蔷薇花", score: 23, rarity: "rare", members: ["南宫静梅", "瑶瑶", "一一"] },
            { name: "粉韵石竹花", score: 23, rarity: "rare", members: ["一一", "吟风客"] },
            { name: "赤晖石竹花", score: 23, rarity: "rare", members: ["凉薄", "一一"] },
            { name: "紫晕石竹花", score: 23, rarity: "rare", members: ["紫火祥云", "瑶瑶", "一一"] },
            { name: "薄红虞美人", score: 23, rarity: "rare", members: ["宇文半青", "初见"] },
            { name: "橙黄虞美人", score: 23, rarity: "rare", members: ["凉薄", "夏夜"] },
            { name: "黛紫虞美人", score: 23, rarity: "rare", members: ["紫火祥云", "一一"] },
            { name: "彤云六初花", score: 23, rarity: "rare", members: ["宇文半青"] },
            { name: "碧玉六初花", score: 23, rarity: "rare", members: ["在燕然菲", "一一"] },
            { name: "缃桃六初花", score: 23, rarity: "rare", members: ["在燕然菲"] },
            { name: "秋枫跳舞兰", score: 23, rarity: "rare", members: [] },
            { name: "伯利恒之星", score: 23, rarity: "rare", members: ["凉薄", "在燕然菲", "一一", "贺靖荷", "吟风客"] },
            { name: "棉花小熊", score: 23, rarity: "rare", members: ["凉薄", "小曹睡不着", "桃桃", "一夜星光", "在燕然菲", "蛙哒瓜嚓", "贺靖荷", "贝儿", "珊珊", "余念凉"] },
            // 25分 史诗花 (Epic)
            { name: "宝珠玉兰", score: 25, rarity: "epic", members: ["宇文半青", "凉薄", "南宫静梅", "夏夜", "苏息", "李开心", "神兜兜", "一夜星光", "宿司", "豆豆", "陈诗云", "姚雯嫣", "林可新", "不可回笔", "初见", "一一", "花瑶", "吟风客", "珊珊", "余念凉"] },
            { name: "粉樱蝶舞玫瑰", score: 25, rarity: "epic", members: ["没事种花", "凉薄", "夏夜", "孟乐双", "李开心", "神兜兜", "紫火祥云", "宿司", "陈诗云", "姚雯嫣", "余念凉"] },
            { name: "冰蓝蝶舞玫瑰", score: 25, rarity: "epic", members: ["没事种花", "孟乐双", "宿司", "林可新", "不可回笔", "一一", "余念凉"] },
            { name: "红香妃腊梅", score: 25, rarity: "epic", members: ["夏夜", "孟乐双", "李开心", "宿司", "姚雯嫣", "林可新", "不可回笔", "一一", "余念凉"] },
            { name: "玉玲珑腊梅", score: 25, rarity: "epic", members: ["苏息", "孟乐双", "李开心", "瑶瑶", "宿司", "不可回笔", "余念凉"] },
            { name: "白灵逐浪", score: 25, rarity: "epic", members: ["没事种花", "宇文半青", "神兜兜", "宿司", "不可回笔", "初见", "余念凉"] },
            { name: "幽蓝逐影", score: 25, rarity: "epic", members: ["没事种花", "南宫静梅", "宿司", "姚雯嫣", "余念凉"] },
            { name: "桃影浮澜", score: 25, rarity: "epic", members: ["没事种花", "苏息", "李开心", "宿司", "林可新", "不可回笔", "余念凉"] },
            { name: "霁澜牡丹", score: 25, rarity: "epic", members: ["没事种花", "南宫静梅", "苏息", "李开心", "神兜兜", "瑶瑶", "宿司", "陈诗云", "林可新", "不可回笔", "余念凉"] },
            { name: "紫曜牡丹", score: 25, rarity: "epic", members: ["宿司", "姚雯嫣", "一一", "余念凉"] },
            { name: "瑶光牡丹", score: 25, rarity: "epic", members: ["宿司", "姚雯嫣", "不可回笔", "余念凉"] },
            { name: "杏色春衫", score: 25, rarity: "epic", members: ["宿司", "姚雯嫣", "余念凉"] },
            { name: "姑苏雨蒙", score: 25, rarity: "epic", members: ["南宫静梅", "夏夜", "瑶瑶", "宿司", "陈诗云", "林可新", "不可回笔", "余念凉"] },
            { name: "仙女散花", score: 25, rarity: "epic", members: ["南宫静梅", "苏息", "宿司", "林可新", "初见", "余念凉"] },
            { name: "花笼流芳", score: 25, rarity: "epic", members: ["瑶瑶", "宿司", "不可回笔", "吟风客", "即墨凡琪", "余念凉"] },
            { name: "花笼星语", score: 25, rarity: "epic", members: ["凉薄", "南宫静梅", "神兜兜", "宿司", "林可新", "即墨凡琪", "余念凉"] },
            { name: "花笼琼光", score: 25, rarity: "epic", members: ["孟乐双", "温贝贝", "宿司", "不可回笔", "一一", "即墨凡琪", "余念凉"] },
            { name: "馥香花饼", score: 25, rarity: "epic", members: ["南宫静梅", "紫火祥云", "瑶瑶", "一夜星光", "宿司", "林可新", "不可回笔", "即墨凡琪", "余念凉"] },
            { name: "芳蕊琼浆", score: 25, rarity: "epic", members: ["宿司", "即墨凡琪", "余念凉"] },
            { name: "火耀金丹", score: 25, rarity: "epic", members: ["宇文半青", "土豆花", "凉薄", "李开心", "桃桃", "紫火祥云", "瑶瑶", "一夜星光", "宿司", "在燕然菲", "姚雯嫣", "林可新", "不可回笔", "一一", "贺靖荷", "吟风客", "即墨凡琪", "余念凉"] },
            { name: "琼台玉露", score: 25, rarity: "epic", members: ["宿司", "余念凉"] },
            { name: "霓光映树", score: 25, rarity: "epic", members: ["宇文半青", "李开心", "宿司", "陈诗云", "林可新", "余念凉"] },
            { name: "恬梦圣铃", score: 25, rarity: "epic", members: ["温贝贝", "瑶瑶", "宿司", "陈诗云", "不可回笔", "余念凉"] },
            { name: "元气破蛋", score: 25, rarity: "epic", members: ["温贝贝", "宿司", "姚雯嫣", "林可新", "余念凉"] },
            { name: "曜绯帝王花", score: 25, rarity: "epic", members: ["神兜兜", "温贝贝", "宿司", "陈诗云", "姚雯嫣", "林可新", "不可回笔", "余念凉"] },
            { name: "珠匣粉芙蓉", score: 25, rarity: "epic", members: ["没事种花", "夏夜", "神兜兜", "宿司", "林可新", "不可回笔", "余念凉"] },
            { name: "珠匣紫芙蓉", score: 25, rarity: "epic", members: [] },
            { name: "珠匣橘芙蓉", score: 25, rarity: "epic", members: [] },
            { name: "映粉云光月季", score: 25, rarity: "epic", members: [] },
            { name: "沐光映黄月季", score: 25, rarity: "epic", members: ["没事种花", "神兜兜", "即墨凡琪", "余念凉"] },
            { name: "橙光拂晓月季", score: 25, rarity: "epic", members: ["即墨凡琪", "余念凉"] },
            { name: "玉兔揽月", score: 25, rarity: "epic", members: [] },
            { name: "鹤寄星河", score: 25, rarity: "epic", members: [] },
            { name: "紫灵福禄", score: 25, rarity: "epic", members: [] },
            { name: "捣蛋幽幽", score: 25, rarity: "epic", members: ["没事种花", "余念凉"] },
            { name: "欢闹南瓜", score: 25, rarity: "epic", members: ["没事种花", "李开心", "一夜星光", "豆豆", "余念凉"] },
            { name: "星槎仙舟", score: 25, rarity: "epic", members: ["孟乐双", "宿司", "余念凉"] },
            { name: "瑶枝桂影", score: 25, rarity: "epic", members: ["宿司" ] },
            { name: "灵松照夜", score: 25, rarity: "epic", members: ["孟乐双",] },
            { name: "竹映金辉", score: 25, rarity: "epic", members: ["孟乐双"] },
            // 28/30分 传说花 (Legend)
            { name: "巧月·星眸应水", score: 28, rarity: "legend", members: [] },
            { name: "桂月·秋千稚语", score: 28, rarity: "legend", members: ["孟乐双"] },
            { name: "菊月·花间飞鸢", score: 28, rarity: "legend", members: ["没事种花", "孟乐双", "即墨凡琪", "余念凉", "宿司"] },
            { name: "阳月·芙香盈袖", score: 28, rarity: "legend", members: ["没事种花", "南宫静梅", "夏夜", "孟乐双", "李开心", "宿司", "陈诗云", "林可新", "一一", "即墨凡琪", "余念凉", "神兜兜"] },
            { name: "葭月·栖舟泛漪", score: 28, rarity: "legend", members: ["孟乐双", "李开心", "温贝贝", "宿司", "即墨凡琪", "余念凉", "神兜兜"] },
            { name: "星河映蕊", score: 28, rarity: "legend", members: ["没事种花", "夏夜", "苏息", "孟乐双", "李开心", "神兜兜", "桃桃", "宿司", "在燕然菲", "陈诗云", "姚雯嫣", "林可新", "初见", "吟风客", "即墨凡琪", "余念凉"] },
            { name: "星夜奇遇", score: 28, rarity: "legend", members: ["没事种花", "李开心", "一夜星光", "余念凉"] },
            { name: "花宴流芳", score: 28, rarity: "legend", members: ["没事种花", "苏息", "孟乐双", "温贝贝", "宿司", "姚雯嫣", "即墨凡琪", "余念凉"] },
            { name: "芳华寻蝶", score: 28, rarity: "legend", members: ["夏夜", "孟乐双", "李开心", "温贝贝", "瑶瑶", "宿司", "陈诗云", "林可新", "即墨凡琪", "余念凉", "神兜兜"] },
            { name: "繁花满筑", score: 28, rarity: "legend", members: ["宿司", "余念凉"] },
            { name: "欢雪颂冬", score: 28, rarity: "legend", members: ["宇文半青", "夏夜", "孟乐双", "李开心", "神兜兜", "温贝贝", "宿司", "陈诗云", "姚雯嫣", "林可新", "余念凉", "神兜兜"] },
            { name: "碧羽青鸾", score: 28, rarity: "legend", members: [] },
            { name: "金鳞飞渡", score: 30, rarity: "legend", members: ["孟乐双", "宿司", "即墨凡琪"] },
            { name: "有龙则灵", score: 30, rarity: "legend", members: [] },
            { name: "天上宫阙", score: 30, rarity: "legend", members: ["夏夜", "陈诗云", "即墨凡琪", "神兜兜", "宿司"] }
        ];

        // 稀有度文字映射
        const rarityText = {
            normal: "普花",
            rare: "紫花",
            epic: "金花",
            legend: "红花"
        };

        // 获取页面元素
        const flowerSearch = document.getElementById('flowerSearch');
        const flowerList = document.getElementById('flowerList');
        
        // 统计数据元素
        const totalCount = document.getElementById('totalCount');
        const normalCount = document.getElementById('normalCount');
        const rareCount = document.getElementById('rareCount');
        const epicCount = document.getElementById('epicCount');
        const legendCount = document.getElementById('legendCount');

        // 初始化加载
        renderFlowerList(flowerData);
        updateStatistics(flowerData);

        // 搜索功能：搜花名/成员名都可以匹配
        flowerSearch.addEventListener('input', function() {
            const keyword = this.value.trim().toLowerCase();
            const filterFlowers = flowerData.filter(item => 
                item.name.toLowerCase().includes(keyword) || 
                item.members.some(member => member.toLowerCase().includes(keyword))
            );
            renderFlowerList(filterFlowers);
            updateStatistics(filterFlowers);
        });

        // 渲染鲜花列表
        function renderFlowerList(flowers) {
            if (flowers.length === 0) {
                flowerList.innerHTML = `
                    <div class="empty-tip">
                        <<i class="fa fa-search" aria-hidden="true"></</i>
                        <p>暂无匹配结果</p>
                        <p style="font-size: 14px; margin-top: 4px;">请尝试其他关键词搜索</p>
                    </div>
                `;
                return;
            }
            
            // 排序：先按分数降序，再按名称升序
            flowers.sort((a, b) => {
                if (b.score !== a.score) {
                    return b.score - a.score;
                } else {
                    return a.name.localeCompare(b.name);
                }
            });

            let html = '';
            flowers.forEach(flower => {
                const memberText = flower.members.length > 0 ? flower.members.join('、') : '暂无成员';
                html += `
                    <div class="flower-card">
                        <div class="flower-top">
                            <div class="flower-name">${flower.name}</div>
                            <div class="flower-score score-${flower.score}">${flower.score}</div>
                            <div class="flower-rarity rarity-${flower.rarity}">${rarityText[flower.rarity]}</div>
                        </div>
                        <div class="flower-members">
                            <span class="member-label"><<i class="fa fa-user-o" aria-hidden="true"></</i> 拥有成员</span>
                            ${memberText}
                        </div>
                    </div>
                `;
            });
            flowerList.innerHTML = html;
        }

        // 更新统计数据
        function updateStatistics(flowers) {
            totalCount.innerText = flowers.length;
            const counts = { normal: 0, rare: 0, epic: 0, legend: 0 };
            flowers.forEach(f => { counts[f.rarity]++; });
            normalCount.innerText = counts.normal;
            rareCount.innerText = counts.rare;
            epicCount.innerText = counts.epic;
            legendCount.innerText = counts.legend;
        }

        // GitHub Pages 兼容：添加页面加载完成提示（可选）
        window.addEventListener('load', function() {
            console.log('花园世界公会鲜花图鉴加载完成 - GitHub Pages 版');
        });
    </script>
</body>
</html>
