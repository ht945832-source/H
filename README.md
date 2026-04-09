


          <!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>VIP TOOL HOANGDZ v13 - ROBOT</title>
    <style>
        :root { --neon: #00ffff; --gold: #ffcc00; --bg: rgba(15, 15, 15, 0.95); }
        * { margin:0; padding:0; box-sizing:border-box; touch-action:none; -webkit-user-select:none; }
        body { background:#000; overflow:hidden; font-family: 'Segoe UI', sans-serif; }
        
        iframe { width:100vw; height:100vh; border:none; position:absolute; z-index: 1; }

        /* THÔNG BÁO ADMIN */
        #overlay {
            position: fixed; inset: 0; background: rgba(0,0,0,0.9);
            z-index: 10001; display: flex; align-items: center; justify-content: center;
            backdrop-filter: blur(12px);
        }
        .popup {
            width: 85%; max-width: 380px; background: var(--bg);
            border: 2px solid var(--neon); border-radius: 25px; padding: 30px;
            text-align: center; color: white; box-shadow: 0 0 40px rgba(0,255,255,0.3);
        }
        .popup h2 { color: var(--neon); margin-bottom: 15px; text-transform: uppercase; }
        .popup b { color: var(--gold); }
        .close-btn {
            background: var(--neon); color: #000; border: none; padding: 12px 40px;
            border-radius: 50px; font-weight: bold; margin-top: 20px; cursor: pointer;
        }

        /* GIAO DIỆN TOOL CHÍNH */
        #drag-tool {
            position: fixed; top: 15%; left: 50%;
            transform: translate3d(-50%, 0, 0) scale(1) rotate(0deg);
            z-index: 9999; display: flex; align-items: center;
            background: var(--bg); backdrop-filter: blur(25px);
            padding: 15px 35px; border-radius: 100px;
            border: 1.5px solid rgba(0,255,255,0.4); gap: 25px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.8);
            cursor: grab; will-change: transform;
        }

        .lamp { width: 55px; height: 55px; border-radius: 50%; border: 4px solid #222; }
        .active-t { background: #00ff00; box-shadow: 0 0 40px #00ff00; border-color: #fff; animation: blink 0.5s infinite alternate; }
        .active-x { background: #ff0000; box-shadow: 0 0 40px #ff0000; border-color: #fff; animation: blink 0.5s infinite alternate; }
        @keyframes blink { from { opacity: 0.4; } to { opacity: 1; } }

        /* PHẦN ROBOT VÀ THÔNG TIN */
        .info { text-align: center; color: white; min-width: 130px; position: relative; }
        #robot-img { width: 45px; margin-bottom: 5px; filter: drop-shadow(0 0 5px var(--neon)); }
        #p-txt { color: var(--gold); font-weight: bold; font-size: 16px; margin-bottom: 2px; }
        
        .status-msg { font-size: 11px; font-weight: bold; }
        #ana-text { color: #00ff00; animation: pulse 0.7s infinite; display: none; }
        #res-rate { color: var(--neon); }
        @keyframes pulse { 50% { opacity: 0.2; } }

        /* MENU 3 GẠCH & NÚT PHÓNG TO */
        #menu-btn {
            position: fixed; bottom: 25px; left: 25px; z-index: 10000;
            width: 55px; height: 55px; background: var(--neon);
            border-radius: 15px; display: flex; flex-direction: column;
            justify-content: center; align-items: center; gap: 5px; cursor: pointer;
            box-shadow: 0 0 20px rgba(0,255,255,0.4);
        }
        #menu-btn span { width: 30px; height: 4px; background: #000; border-radius: 2px; }

        #menu-content {
            position: fixed; bottom: 90px; left: 25px; z-index: 10000;
            background: rgba(10,10,10,0.98); border: 1.5px solid var(--neon);
            padding: 15px; border-radius: 20px; display: none; flex-direction: column; gap: 10px;
        }
        .btn-item {
            color: white; background: #222; padding: 12px 25px;
            border-radius: 12px; font-size: 13px; text-align: center;
            font-weight: bold; min-width: 160px;
        }
        .btn-item:active { background: var(--neon); color: #000; }
    </style>
</head>
<body>

    <div id="overlay">
        <div class="popup">
            <h2>ROBOT AI PREDICT</h2>
            <p>Chào mừng <b>Trần Hoàng</b> quay trở lại.<br>Hệ thống đã đồng bộ thời gian 45 giây.<br><br>Liên hệ: <b>@tranhoang2286</b></p>
            <button class="close-btn" onclick="document.getElementById('overlay').style.display='none'">VÀO TOOL</button>
        </div>
    </div>

    <iframe src="https://68gbvn88.bar"></iframe>

    <div id="drag-tool">
        <div style="text-align:center;"><b style="color:#555; font-size:10px;">TÀI</b><div id="lt" class="lamp"></div></div>
        
        <div class="info">
            <img id="robot-img" src="https://i.postimg.cc/rwkZQhxp/Robot.gif">
            <div id="p-txt">#PHIÊN_WAIT</div>
            
            <div id="status-container">
                <div id="ana-text" class="status-msg">🔎 ĐANG PHÂN TÍCH...</div>
                <div id="res-rate" class="status-msg">WIN RATE: 0%</div>
            </div>
        </div>
        
        <div style="text-align:center;"><b style="color:#555; font-size:10px;">XỈU</b><div id="lx" class="lamp"></div></div>
    </div>

    <div id="menu-btn" onclick="toggleMenu()">
        <span></span><span></span><span></span>
    </div>
    
    <div id="menu-content">
        <div class="btn-item" onclick="location.reload()">🔄 LÀM MỚI TOOL</div>
        <div class="btn-item" onclick="scaleTool(0.1)">➕ PHÓNG TO (+)</div>
        <div class="btn-item" onclick="scaleTool(-0.1)">➖ THU NHỎ (-)</div>
        <div class="btn-item" onclick="rotateTool(90)">🔄 XOAY 90 ĐỘ</div>
        <div class="btn-item" onclick="rotateTool(0)">🏠 MẶC ĐỊNH</div>
    </div>

    <script>
        let currentScale = 1;
        let currentRotation = 0;
        const tool = document.getElementById("drag-tool");

        function toggleMenu() {
            const m = document.getElementById("menu-content");
            m.style.display = (m.style.display === "flex") ? "none" : "flex";
        }

        function scaleTool(v) { currentScale = Math.max(0.5, Math.min(2, currentScale + v)); updateUI(); }
        function rotateTool(v) { currentRotation = v; updateUI(); }
        
        function updateUI() {
            tool.style.transform = `translate3d(-50%, 0, 0) scale(${currentScale}) rotate(${currentRotation}deg)`;
        }

        // ĐỒNG BỘ DỮ LIỆU TỪ API (THỜI GIAN CHẠY ẨN)
        async function syncData() {
            try {
                const res = await fetch("https://api-hoangdz2-2.onrender.com/api/get-data");
                const d = await res.json();
                
                document.getElementById("p-txt").innerText = "#" + d.phien;
                
                const ana = document.getElementById("ana-text");
                const rate = document.getElementById("res-rate");
                const lt = document.getElementById("lt"), lx = document.getElementById("lx");

                if (d.is_analyzing) {
                    // Trạng thái quét ẩn
                    ana.style.display = "block";
                    rate.style.display = "none";
                    lt.className = "lamp"; lx.className = "lamp";
                } else {
                    // Hiện kết quả
                    ana.style.display = "none";
                    rate.style.display = "block";
                    rate.innerText = "WIN RATE: " + d.rate;
                    
                    lt.className = "lamp"; lx.className = "lamp";
                    if(d.dudoan === "TÀI") lt.classList.add("active-t");
                    if(d.dudoan === "XỈU") lx.classList.add("active-x");
                }
            } catch(e) {}
        }
        setInterval(syncData, 1000);

        // KÉO THẢ MƯỢT MÀ
        let isDragging = false, startX, startY, initL, initT;
        
        tool.addEventListener('touchstart', (e) => {
            isDragging = true; const t = e.touches[0];
            startX = t.clientX; startY = t.clientY;
            initL = tool.offsetLeft; initT = tool.offsetTop;
            tool.style.transition = "none";
        });

        window.addEventListener('touchmove', (e) => {
            if (!isDragging) return;
            const t = e.touches[0];
            tool.style.left = (initL + t.clientX - startX) + "px";
            tool.style.top = (initT + t.clientY - startY) + "px";
            updateUI();
        });

        window.addEventListener('touchend', () => {
            isDragging = false;
            tool.style.transition = "transform 0.3s cubic-bezier(0.1, 0.7, 0.1, 1)";
        });
    </script>
</body>
</html>
