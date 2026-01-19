<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>神秘图片库 - 点击探索</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Press+Start+2P&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            min-height: 100vh;
            background: linear-gradient(45deg, #0c0c1d, #1a1a2e, #16213e);
            color: #fff;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            padding: 40px 0;
            position: relative;
        }
        
        h1 {
            font-family: 'Orbitron', sans-serif;
            font-size: 4.5rem;
            background: linear-gradient(90deg, #ff3366, #00ccff, #ffcc00);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 30px rgba(255, 51, 102, 0.3);
            margin-bottom: 20px;
            position: relative;
            animation: glow 3s infinite alternate;
        }
        
        @keyframes glow {
            0% { text-shadow: 0 0 20px rgba(255, 51, 102, 0.5); }
            50% { text-shadow: 0 0 30px rgba(0, 204, 255, 0.5); }
            100% { text-shadow: 0 0 20px rgba(255, 204, 0, 0.5); }
        }
        
        .subtitle {
            font-size: 1.4rem;
            color: #a3d9ff;
            max-width: 800px;
            margin: 0 auto 30px;
            line-height: 1.6;
        }
        
        /* 按钮区域 */
        .button-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 25px;
            margin: 50px 0;
        }
        
        .magic-button {
            padding: 22px 45px;
            font-size: 1.6rem;
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.4s;
            position: relative;
            overflow: hidden;
            z-index: 1;
            display: flex;
            align-items: center;
            gap: 15px;
            text-transform: uppercase;
            letter-spacing: 1px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
        }
        
        .magic-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: 0.5s;
            z-index: -1;
        }
        
        .magic-button:hover::before {
            left: 100%;
        }
        
        .magic-button:hover {
            transform: translateY(-10px) scale(1.05);
        }
        
        .magic-button:active {
            transform: translateY(-5px) scale(0.98);
        }
        
        /* 不同按钮样式 */
        .btn-reveal {
            background: linear-gradient(135deg, #ff3366, #ff6699);
            color: white;
        }
        
        .btn-puzzle {
            background: linear-gradient(135deg, #00ccff, #33ccff);
            color: white;
        }
        
        .btn-matrix {
            background: linear-gradient(135deg, #00ff99, #66ffcc);
            color: #111;
        }
        
        .btn-hologram {
            background: linear-gradient(135deg, #9966ff, #cc99ff);
            color: white;
        }
        
        .btn-random {
            background: linear-gradient(135deg, #ffcc00, #ffdd33);
            color: #111;
        }
        
        /* 图片展示区域 */
        .image-container {
            min-height: 600px;
            position: relative;
            margin: 60px auto;
            padding: 30px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
            overflow: hidden;
            display: none;
        }
        
        .image-display {
            width: 100%;
            height: 500px;
            border-radius: 15px;
            overflow: hidden;
            position: relative;
            margin-bottom: 30px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5);
            display: none;
        }
        
        .image-display img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
        }
        
        .image-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 2.5rem;
            text-align: center;
            margin-bottom: 20px;
            color: #ffcc00;
            text-shadow: 0 0 15px rgba(255, 204, 0, 0.5);
        }
        
        .image-description {
            font-size: 1.3rem;
            line-height: 1.7;
            color: #d1e8ff;
            text-align: center;
            max-width: 800px;
            margin: 0 auto;
        }
        
        /* 特效元素 */
        .particle {
            position: absolute;
            border-radius: 50%;
            pointer-events: none;
            z-index: 1;
        }
        
        .matrix-code {
            position: absolute;
            color: #00ff00;
            font-family: 'Courier New', monospace;
            font-size: 1.8rem;
            opacity: 0;
            text-shadow: 0 0 10px #00ff00;
            z-index: 2;
        }
        
        .puzzle-piece {
            position: absolute;
            background-size: cover;
            background-position: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            z-index: 3;
        }
        
        .hologram-line {
            position: absolute;
            background: rgba(0, 255, 255, 0.3);
            box-shadow: 0 0 10px rgba(0, 255, 255, 0.7);
            z-index: 2;
        }
        
        /* 控制面板 */
        .controls {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 40px;
            flex-wrap: wrap;
        }
        
        .control-btn {
            padding: 15px 30px;
            font-size: 1.2rem;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .control-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-5px);
        }
        
        .counter {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.7);
            padding: 15px 25px;
            border-radius: 10px;
            font-size: 1.5rem;
            color: #ffcc00;
            z-index: 100;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
            font-family: 'Orbitron', sans-serif;
        }
        
        .secret-btn {
            position: fixed;
            bottom: 20px;
            left: 20px;
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background: rgba(255, 51, 102, 0.8);
            color: white;
            border: none;
            font-size: 1.8rem;
            cursor: pointer;
            z-index: 100;
            box-shadow: 0 5px 15px rgba(255, 51, 102, 0.5);
            transition: all 0.3s;
        }
        
        .secret-btn:hover {
            transform: scale(1.1) rotate(90deg);
            background: rgba(0, 204, 255, 0.8);
        }
        
        .loading {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            transition: opacity 0.5s;
        }
        
        .loading.hidden {
            opacity: 0;
            pointer-events: none;
        }
        
        .loading-text {
            font-size: 2.5rem;
            margin-top: 30px;
            font-family: 'Orbitron', sans-serif;
            color: #00ccff;
            text-shadow: 0 0 10px #00ccff;
            animation: pulse 1.5s infinite;
        }
        
        @keyframes pulse {
            0% { opacity: 0.5; }
            50% { opacity: 1; }
            100% { opacity: 0.5; }
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            h1 { font-size: 2.8rem; }
            .subtitle { font-size: 1.1rem; }
            .magic-button { padding: 18px 30px; font-size: 1.3rem; }
            .image-display { height: 350px; }
            .image-title { font-size: 1.8rem; }
            .button-container { gap: 15px; }
        }
    </style>
</head>
<body>
    <!-- 加载屏幕 -->
    <div class="loading" id="loadingScreen">
        <div style="width: 100px; height: 100px; border: 5px solid transparent; border-top: 5px solid #00ccff; border-radius: 50%; animation: spin 1s linear infinite;"></div>
        <div class="loading-text">初始化图片库...</div>
    </div>
    
    <!-- 计数器 -->
    <div class="counter">
        <i class="fas fa-eye"></i> 查看次数: <span id="viewCount">0</span>
    </div>
    
    <!-- 秘密按钮 -->
    <button class="secret-btn" id="secretBtn">
        <i class="fas fa-question"></i>
    </button>
    
    <div class="container">
        <header>
            <h1>神秘图片探索器</h1>
            <p class="subtitle">
                点击下方按钮，以各种神奇的方式解锁隐藏的图片。每种效果都有独特的视觉体验，准备好被惊艳了吗？
            </p>
        </header>
        
        <!-- 按钮区域 -->
        <div class="button-container">
            <button class="magic-button btn-reveal" id="revealBtn">
                <i class="fas fa-magic"></i> 魔法揭示
            </button>
            <button class="magic-button btn-puzzle" id="puzzleBtn">
                <i class="fas fa-puzzle-piece"></i> 拼图组合
            </button>
            <button class="magic-button btn-matrix" id="matrixBtn">
                <i class="fas fa-code"></i> 矩阵解码
            </button>
            <button class="magic-button btn-hologram" id="hologramBtn">
                <i class="fas fa-atom"></i> 全息投影
            </button>
            <button class="magic-button btn-random" id="randomBtn">
                <i class="fas fa-random"></i> 随机惊喜
            </button>
        </div>
        
        <!-- 图片展示区域 -->
        <div class="image-container" id="imageContainer">
            <h2 class="image-title" id="imageTitle">神秘图片</h2>
            
            <div class="image-display" id="imageDisplay">
                <img id="displayedImage" src="" alt="神秘图片">
            </div>
            
            <p class="image-description" id="imageDescription">
                图片描述将在这里显示...
            </p>
            
            <!-- 控制面板 -->
            <div class="controls">
                <button class="control-btn" id="prevBtn">
                    <i class="fas fa-arrow-left"></i> 上一张
                </button>
                <button class="control-btn" id="downloadBtn">
                    <i class="fas fa-download"></i> 保存图片
                </button>
                <button class="control-btn" id="shareBtn">
                    <i class="fas fa-share-alt"></i> 分享
                </button>
                <button class="control-btn" id="nextBtn">
                    下一张 <i class="fas fa-arrow-right"></i>
                </button>
            </div>
        </div>
    </div>
    
    <script>
        // 图片数据
        const images = [
            {
                url: "https://images.unsplash.com/photo-1579546929662-711aa81148cf?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80",
                title: "绚丽极光",
                description: "北极天空中的自然光秀，由太阳风与地球磁场相互作用形成。绿色和紫色光带在夜空中舞动，创造出令人惊叹的视觉奇观。"
            },
            {
                url: "https://images.unsplash.com/photo-1506905925346-21bda4d32df4?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80",
                title: "雪山之巅",
                description: "雄伟的雪山在日出时分被染成金色，云海在山间流淌。这是世界之巅的壮丽景色，象征着自然的力量与纯净。"
            },
            {
                url: "https://images.unsplash.com/photo-1518837695005-2083093ee35b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80",
                title: "宇宙星空",
                description: "浩瀚宇宙中的星系和星云，无数恒星在黑暗中闪烁。这张图片展示了我们在宇宙中的位置，唤起对未知的好奇与敬畏。"
            },
            {
                url: "https://images.unsplash.com/photo-1519681393784-d120267933ba?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80",
                title: "神秘森林",
                description: "阳光透过古老森林的树冠，形成神秘的光束。这片原始森林充满了生命与秘密，等待勇敢的探索者去发现。"
            },
            {
                url: "https://images.unsplash.com/photo-1540206395-68808572332f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1426&q=80",
                title: "未来都市",
                description: "霓虹灯下的赛博朋克都市，高耸的建筑与全息广告交织。这个未来主义的城市景观展示了科技与人类文明的融合。"
            }
        ];
        
        // 当前显示的图片索引
        let currentImageIndex = 0;
        let viewCount = 0;
        let activeEffect = null;
        
        // DOM元素
        const loadingScreen = document.getElementById('loadingScreen');
        const imageContainer = document.getElementById('imageContainer');
        const imageDisplay = document.getElementById('imageDisplay');
        const displayedImage = document.getElementById('displayedImage');
        const imageTitle = document.getElementById('imageTitle');
        const imageDescription = document.getElementById('imageDescription');
        const viewCountElement = document.getElementById('viewCount');
        
        // 初始化
        document.addEventListener('DOMContentLoaded', function() {
            // 模拟加载
            setTimeout(() => {
                loadingScreen.classList.add('hidden');
            }, 2000);
            
            // 加载查看次数
            const savedCount = localStorage.getItem('imageViewCount');
            if (savedCount) {
                viewCount = parseInt(savedCount);
                viewCountElement.textContent = viewCount;
            }
            
            // 设置按钮事件
            document.getElementById('revealBtn').addEventListener('click', () => showImageWithEffect('reveal'));
    文件。getElementById('puzzleBtn')。addEventListener('click'，()=>showImageWithEffect('puzzle'))；
    文件。getElementById('matrixBtn')。addEventListener('click'，()=>showImageWithEffect('matrix'))；
    文件。getElementById('hologramBtn')。addEventListener('click'，()=>showImageWithEffect('hologram'))；
    文件。getElementById('randomBtn')。addEventListener('click'，()=>showImageWithEffect('random'))；
            
    // 控制面板事件
    文件。getElementById('prevBtn').addEventListener('click'，showPreviousImage)；
    文件。getElementById('nextBtn').addEventListener('click'，showNextImage)；
    文件。getElementById('downloadBtn').addEventListener('click'，DownloadImage)；
    文件。getElementById('shareBtn')。addEventListener('click'，shareImage)；
            
    // 秘密按钮事件
    文件。getElementById('secretBtn')。addEventListener('click'，showSecretImage)；
            
    // 初始化粒子效果
    createFloatingParticle()；
            
    // 预加载图片
    预加载图像()；
        });
        
    // 预加载图片
    函数preloadImages(){
    images.forEach(img=>{
    Const image=new Image()；
    image.src=img.url；
            });
        }
        
    // 使用指定效果显示图片
    函数showImageWithEffect(effectType){
    // 更新查看次数
    viewcount++；
    viewCountElement.textContent=viewCount；
    localStorage。setitem('imageViewCount'，viewCount.toString())；
            
    // 显示容器
    imageContainer.style.display='block'；
            
    // 如果已有活跃效果，清除
    if(activeEffect){
    clearEffect(activeEffect)；
            }
            
    // 设置当前效果
    activeEffect=effectType；
            
    // 显示图片
    Const currentImage=images[currentImageIndex]；
    displayedImage.src=currentImage.url；
    imageTitle.textContent=currentImage.title；
    imageDescription.textContent=当前图像。描述；
            
    // 根据效果类型应用不同动画
    switch(effectType){
    案例“揭示”：
    revealEffect()；
    imageDisplay.style.display='block'；
    案例“难题”：
    puzzleEffect()；
    打破；
    案例“矩阵”：
    矩阵效应()；
    打破；
    案例“全息图”：
    hologramEffect()；
    打破；
    病例“随机”：
    Const效应=['揭示'，'拼图'，'矩阵'，'全息']；
    常数randomEffect=效果[Math.loor(Math.Random()*效果。长度)]；
    showImageWithEffect(randomEffect)；
    返回；
            }
            
    // 显示图片区域
//显示图片区域imageDisplay.style.display='block'；
            
    // 滚动到图片区域
    imageContainer.scrollIntoView({行为：'光滑的'})；
        }
        
    // 魔法揭示效果
    函数revealEffect(){
    // 清除图片显示
    displayedImage.style.display='none'；
            
    // 创建粒子效果
    for(设i=0；i<100；i++){
    createParticle()；
            }
            
    // 延迟后显示图片
    setTimeout(()=>{
    // 显示图片并添加动画
    displayedImage.style.display='block'；
    displayedImage.style.animation='none'；
                
    // 强制重排以重新启动动画
    void displayedImage.offsetWidth；
                
    // 应用动画
    displayedImage。风格。animation='revealAnimation1.5s向前地'；
                
    //添加CSS动画
    Constyle=document.createElement('style')；
    style.textContent='
    @keyframes revealAnimation{
    0%{不透明度：0；变换：比例(0.5)旋转(-180度)；滤镜：模糊(20px)；}
    70%{transform:scale(1.05)旋转(10度)；}
    100%{不透明度：1；变换：比例(1)旋转(0deg)；滤镜：模糊(0px)；}
                    }
    `;
    document.head.appendChild(style)；
                
    // 动画结束后移除样式
    setTimeout(()=>{
    style.Remove()；
    }, 1500);
    }, 800);
        }
        
    // 拼图效果
    函数puzzleEffect(){
    // 清除图片显示
    displayedImage.style.display='none'；
            
    // 获取图片显示区域尺寸
    常量容器宽度=imageDisplay.offsetWidth；
    Const containerHeight=imageDisplay.offsetHeight；
            
    // 创建拼图块
    Const puzzleSize=100；
    const cols=Math.ceil(containerWidth/puzzleSize)；
    const rows=Math.ceil(containerHeight/puzzleSize)；
    常量totalPieces=cols*rows；
            
    // 创建拼图块
为(让行=0；row<rows；row++)
