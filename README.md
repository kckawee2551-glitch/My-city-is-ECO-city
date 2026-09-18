# My-city-is-ECO-city
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EcoCity: พลังงานสร้างอนาคต (Hardcore Mode)</title>
    <!-- ฟอนต์ Prompt จาก Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Prompt', sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            position: relative;
        }
        .container {
            width: 100%;
            max-width: 950px;
            background: #ffffff;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.12);
            transition: all 0.3s ease;
        }

        h1 { 
            color: #c0392b; 
            margin-bottom: 5px; 
            font-weight: 600;
            font-size: 28px;
            text-align: center;
        }
        .subtitle {
            color: #e74c3c;
            font-size: 14px;
            margin-bottom: 20px;
            text-align: center;
            font-weight: 500;
        }
        
        .timer-bar {
            background: #c0392b;
            color: white;
            text-align: center;
            padding: 8px;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 500;
            margin-bottom: 20px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }

        .stats {
            display: flex;
            justify-content: space-between;
            background: #f8f9fa;
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 25px;
            border: 1px solid #e9ecef;
        }
        .stat-box {
            text-align: center;
            flex: 1;
        }
        .stat-box span {
            display: block;
            font-size: 22px;
            font-weight: 600;
            color: #2c3e50;
            margin-top: 5px;
        }

        .main-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 10px;
        }
        @media (max-width: 768px) {
            .main-grid {
                grid-template-columns: 1fr;
            }
        }

        .panel {
            padding: 20px;
            border: 1px solid #e9ecef;
            border-radius: 12px;
            background: #fafbfc;
            display: flex;
            flex-direction: column;
        }
        .panel h3 {
            margin-top: 0;
            font-size: 18px;
            color: #34495e;
        }
        .button-group {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 10px;
        }
        .button-full {
            display: grid;
            grid-template-columns: 1fr;
            margin-bottom: 10px;
        }
        button {
            font-family: 'Prompt', sans-serif;
            background-color: #27ae60;
            color: white;
            border: none;
            padding: 10px 8px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 13px;
            font-weight: 500;
            transition: all 0.2s ease;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        button:hover { background-color: #219653; transform: translateY(-2px); }
        button:active { transform: translateY(0); }
        button.coal { background-color: #e74c3c; }
        button.coal:hover { background-color: #c0392b; }
        button.filter-btn { background-color: #2980b9; }
        button.filter-btn:hover { background-color: #2471a3; }
        button.credit-btn { background-color: #8e44ad; }
        button.credit-btn:hover { background-color: #732d91; }
        button:disabled { background-color: #bdc3c7; cursor: not-allowed; transform: none; box-shadow: none; }
        
        .log {
            background: #1e1e1e;
            color: #4af626;
            padding: 15px;
            border-radius: 8px;
            text-align: left;
            font-family: 'Courier New', Courier, monospace;
            flex-grow: 1;
            height: 250px;
            overflow-y: auto;
            font-size: 13px;
            line-height: 1.5;
        }

        #obstacle-banner {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0, 0, 0, 0.85);
            color: white;
            padding: 30px 50px;
            border-radius: 15px;
            text-align: center;
            z-index: 1000;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            animation: fadeInOut 3s ease forwards;
        }
        #obstacle-icon {
            font-size: 50px;
            margin-bottom: 10px;
        }
        #obstacle-text {
            font-size: 20px;
            font-weight: 500;
        }
        @keyframes fadeInOut {
            0% { opacity: 0; transform: translate(-50%, -40%); }
            15% { opacity: 1; transform: translate(-50%, -50%); }
            85% { opacity: 1; transform: translate(-50%, -50%); }
            100% { opacity: 0; transform: translate(-50%, -60%); }
        }

        .modal-overlay {
            display: flex;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.7);
            justify-content: center;
            align-items: center;
            z-index: 2000;
        }
        .modal-content {
            background: white;
            padding: 40px;
            border-radius: 20px;
            text-align: center;
            max-width: 420px;
            width: 90%;
            box-shadow: 0 15px 35px rgba(0,0,0,0.3);
            animation: popUp 0.3s ease;
        }
        @keyframes popUp {
            0% { transform: scale(0.8); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
        .modal-content h2 { font-size: 28px; margin-top: 0; color: #c0392b; }
        .modal-content p { color: #666; font-size: 15px; margin-bottom: 25px; line-height: 1.6; }
        .modal-content button {
            width: 100%;
            padding: 12px;
            font-size: 16px;
            background-color: #c0392b;
        }
        .modal-content button:hover { background-color: #a93226; }
    </style>
</head>
<body>

    <!-- หน้าต่างต้อนรับท่านนายกตอนเริ่มเกม -->
    <div id="welcome-screen" class="modal-overlay">
        <div class="modal-content">
            <h2>🔥 โหมดท้าทายพิเศษ!</h2>
            <p>ยินดีต้อนรับสู่ภารกิจด่วน <b>3 นาที</b><br><br><b>เป้าหมาย:</b> สร้างพลังงานให้ถึง <b>1000 MW</b><br><b>ข้อแม้เหล็ก:</b> มลพิษห้ามเกิน <b>10%</b> เด็ดขาด! (ถ้าเกินหรือหมดเวลาแล้วไม่ถึง 1000 MW จะแพ้ทันที)</p>
            <button onclick="startAppGame()">🚀 ลุยเลย!</button>
        </div>
    </div>

    <div id="obstacle-banner">
        <div id="obstacle-icon">⚠️</div>
        <div id="obstacle-text">เกิดอุปสรรคขึ้นในเมือง!</div>
    </div>

    <!-- หน้าต่างจบเกม -->
    <div id="game-over-screen" class="modal-overlay" style="display: none;">
        <div class="modal-content">
            <h2 id="modal-title" style="color: #e74c3c;">คุณแพ้แล้ว</h2>
            <p id="modal-desc">เมืองของคุณไม่สามารถไปต่อได้...</p>
            <button onclick="restartGame()" style="background-color: #2c3e50;">🔄 เล่นใหม่อีกครั้ง</button>
        </div>
    </div>

    <div class="container" id="game-container">
        <h1>⚡ EcoCity: Hardcore Mode</h1>
        <div class="subtitle">เป้าหมาย: 1000 MW ใน 3 นาที | มลพิษห้ามเกิน 10%</div>

        <!-- แถบแสดงเวลาที่เหลือ -->
        <div class="timer-bar">
            ⏱️ เวลาที่เหลือ: <span id="timer-display">03:00</span> นาที
        </div>

        <div class="stats">
            <div class="stat-box">
                💰 งบประมาณ
                <span id="money" style="color: #27ae60;">1500 G</span>
            </div>
            <div class="stat-box">
                ⚡ พลังงานไฟฟ้า
                <span><span id="energy">0</span> / <span id="demand">100</span> MW</span>
            </div>
            <div class="stat-box">
                ☁️ มลพิษ
                <span id="pollution" style="color: #e67e22;">0%</span>
            </div>
        </div>

        <div class="main-grid">
            <div class="panel">
                <h3>🎛️ แผงควบคุมการสร้าง</h3>
                <div class="button-group">
                    <button id="btn-coal" class="coal" onclick="buildPlant('coal')">🔥 ถ่านหิน (150G)<br><small>+50MW | +15% มล.</small></button>
                    <button id="btn-solar" onclick="buildPlant('solar')">☀️ โซลาร์ (200G)<br><small>+30MW | 0% มล.</small></button>
                    <button id="btn-wind" onclick="buildPlant('wind')">🌬️ กังหันลม (180G)<br><small>+25MW | 0% มล.</small></button>
                </div>
                <div class="button-full">
                    <button id="btn-filter" class="filter-btn" onclick="buildPlant('filter')">🌿 ระบบกรองคาร์บอน (400G)<br><small>ลดมลพิษ 10% | เสียพลังงาน -10MW</small></button>
                </div>
                <div class="button-full">
                    <button id="btn-credit" class="credit-btn" onclick="buildPlant('credit')">💳 ซื้อ Credit มลพิษ (<span id="credit-cost">800</span>G)<br><small>ลดมลพิษ 50% | ราคาแพงขึ้นทุกครั้ง</small></button>
                </div>
            </div>

            <div class="panel">
                <h3>📜 บันทึกเหตุการณ์เมือง</h3>
                <div id="log" class="log">[ระบบ] โหมดฮาร์ดคอร์เริ่มขึ้นแล้ว! เร่งมือผลิตพลังงานให้ถึง 1000 MW โดยคุมมลพิษไม่ให้เกิน 10% ให้ได้!</div>
            </div>
        </div>
    </div>

    <script>
        let money = 1500;
        let energy = 0;
        let demand = 100;
        let pollution = 0;
        let creditPrice = 800;
        let gameStarted = false; 
        let gameActive = false;
        
        let timeLeft = 180; // 3 นาที (180 วินาที)
        let gameSeconds = 0; 
        let afkTimer = 0; 
        const AFK_LIMIT = 600;

        function startAppGame() {
            // [แก้ไขจุดที่ผิดพลาด]: เพิ่มคำสั่งซ่อนหน้าต่างต้อนรับตรงนี้
            document.getElementById("welcome-screen").style.display = "none";
            gameStarted = true;
            gameActive = true;
            logMessage("[ระบบ] นาฬิกา 3 นาทีเดินเครื่องแล้ว ขอให้โชคดีท่านนายก!");
        }

        function updateUI() {
            document.getElementById("money").innerText = money + " G";
            document.getElementById("energy").innerText = energy;
            document.getElementById("demand").innerText = demand;
            document.getElementById("pollution").innerText = pollution + "%";
            document.getElementById("credit-cost").innerText = creditPrice;

            let minutes = Math.floor(timeLeft / 60);
            let seconds = timeLeft % 60;
            document.getElementById("timer-display").innerText = 
                (minutes < 10 ? "0" : "") + minutes + ":" + (seconds < 10 ? "0" : "") + seconds;
        }

        function showObstaclePopup(icon, message) {
            const banner = document.getElementById("obstacle-banner");
            document.getElementById("obstacle-icon").innerText = icon;
            document.getElementById("obstacle-text").innerText = message;
            
            banner.style.display = "none";
            setTimeout(() => {
                banner.style.display = "block";
            }, 10);
        }

        function logMessage(msg, type = "") {
            const logBox = document.getElementById("log");
            let colorStyle = "";
            if (type === 'danger') colorStyle = "color: #ff6b6b;";
            if (type === 'success') colorStyle = "color: #51cf66;";
            if (type === 'warning') colorStyle = "color: #fcc419;";
            
            logBox.innerHTML += `<br><span style="${colorStyle}">${msg}</span>`;
            logBox.scrollTop = logBox.scrollHeight;
        }

        function resetAfkTimer() {
            afkTimer = 0; 
        }

        function buildPlant(type) {
            if (!gameActive) return;
            resetAfkTimer();

            if (type === 'coal') {
                if (money >= 150) {
                    money -= 150;
                    energy += 50;
                    pollution += 15;
                    logMessage("❌ สร้างโรงไฟฟ้าถ่านหินสำเร็จ (+50 MW, +15% มลพิษ)");
                } else {
                    logMessage("⚠️ งบประมาณไม่พอสร้างโรงไฟฟ้าถ่านหิน!", "warning");
                }
            } else if (type === 'solar') {
                if (money >= 200) {
                    money -= 200;
                    energy += 30;
                    logMessage("☀️ สร้างโซลาร์เซลล์สำเร็จ (+30 MW, พลังงานสะอาด)");
                } else {
                    logMessage("⚠️ งบประมาณไม่พอสร้างโซลาร์เซลล์!", "warning");
                }
            } else if (type === 'wind') {
                if (money >= 180) {
                    money -= 180;
                    energy += 25;
                    logMessage("🌬️ สร้างกังหันลมสำเร็จ (+25 MW, พลังงานสะอาด)");
                } else {
                    logMessage("⚠️ งบประมาณไม่พอสร้างกังหันลม!", "warning");
                }
            } else if (type === 'filter') {
                if (money >= 400) {
                    money -= 400;
                    pollution = Math.max(0, pollution - 10); 
                    energy = Math.max(0, energy - 10);
                    logMessage("🌿 เปิดใช้งานระบบกรองคาร์บอนสำเร็จ! (มลพิษลดลง 10%, เสียพลังงาน 10 MW)", "success");
                } else {
                    logMessage("⚠️ งบประมาณไม่พอสร้างระบบกรองคาร์บอน (ต้องการ 400G)!", "warning");
                }
            } else if (type === 'credit') {
                if (money >= creditPrice) {
                    money -= creditPrice;
                    pollution = Math.max(0, pollution - 50); 
                    let oldPrice = creditPrice;
                    creditPrice += 800;
                    logMessage(`💳 ซื้อ Credit มลพิษสำเร็จ ${oldPrice}G (มลพิษลดฮวบ 50% | ราคาครั้งต่อไป: ${creditPrice}G)`, "success");
                } else {
                    logMessage(`⚠️ งบประมาณไม่พอซื้อ Credit มลพิษ (ต้องการ ${creditPrice}G)!`, "warning");
                }
            }
            updateUI();
            checkGameStatus();
        }

        function triggerGameOver(reasonText) {
            if (!gameActive) return;
            gameActive = false;
            document.getElementById("modal-title").innerText = "❌ คุณแพ้แล้ว";
            document.getElementById("modal-title").style.color = "#e74c3c";
            document.getElementById("modal-desc").innerText = reasonText;
            document.getElementById("game-over-screen").style.display = "flex";
        }

        function triggerVictory(reasonText) {
            if (!gameActive) return;
            gameActive = false;
            document.getElementById("modal-title").innerText = "🎉 คุณชนะแล้ว!";
            document.getElementById("modal-title").style.color = "#27ae60";
            document.getElementById("modal-desc").innerText = reasonText;
            document.getElementById("game-over-screen").style.display = "flex";
        }

        function restartGame() {
            location.reload();
        }

        function checkGameStatus() {
            if (!gameActive) return;

            if (pollution > 10) {
                triggerGameOver("มลพิษในเมืองทะลุ 10%! ผิดเงื่อนไขข้อบังคับด้านสิ่งแวดล้อมขั้นเด็ดขาด");
            } else if (money < 0) {
                triggerGameOver("งบประมาณเมืองติดลบ รัฐบาลล้มละลาย!");
            } else if (afkTimer >= AFK_LIMIT) {
                triggerGameOver("คุณปล่อยทิ้งไว้ไม่เล่น เมืองถูกทอดทิ้ง!");
            } else if (timeLeft <= 0) {
                if (energy >= 1000) {
                    triggerVictory("ยอดเยี่ยม! คุณทำพลังงานทะลุ 1000 MW ภายใน 3 นาที และรักษามลพิษไม่ให้เกิน 10% สำเร็จ!");
                } else {
                    triggerGameOver(`หมดเวลา 3 นาทีแล้ว! พลังงานทำได้ ${energy} MW (ต้องการ 1000 MW)`);
                }
                return;
            }

            if (energy >= 1000 && pollution <= 10 && timeLeft > 0) {
                triggerVictory("สุดยอดมหานคร! คุณทำพลังงานถึง 1000 MW และคุมมลพิษใต้ 10% ได้ก่อนหมดเวลา!");
            }
        }

        let gameLoopCounter = 0;
        setInterval(function() {
            if (!gameStarted || !gameActive) return;

            afkTimer++; 
            gameSeconds++;
            if (timeLeft > 0) {
                timeLeft--;
            }
            
            checkGameStatus();
            updateUI();

            gameLoopCounter++;
            if (gameLoopCounter >= 5) { 
                gameLoopCounter = 0;

                let income = Math.min(energy, demand) * 3;
                money += income;

                let demandIncrease = 10;
                let stormCost = 150; 
                let protestCost = 250;
                let diseasePollution = 4;
                let difficultyPhase = "ปกติ";

                if (gameSeconds >= 90) { 
                    demandIncrease = 20;
                    stormCost = 300;
                    protestCost = 450;
                    diseasePollution = 6;
                    difficultyPhase = "เข้มข้น";
                }
                if (gameSeconds >= 120) { 
                    demandIncrease = 35;
                    stormCost = 500;
                    protestCost = 800;
                    diseasePollution = 9;
                    difficultyPhase = "โกลาหลช่วงท้ายเกม!";
                }

                demand += demandIncrease;
                logMessage(`💰 สิ้นรอบ [ความยาก: ${difficultyPhase}]: ได้รับภาษี ${income}G | ความต้องการไฟฟ้าพุ่งเป็น ${demand} MW`);

                let eventChance = Math.random();
                let eventThreshold1 = gameSeconds >= 120 ? 0.45 : (gameSeconds >= 90 ? 0.35 : 0.25);
                let eventThreshold2 = gameSeconds >= 120 ? 0.80 : (gameSeconds >= 90 ? 0.65 : 0.50);

                if (eventChance < eventThreshold1) {
                    money -= stormCost;
                    logMessage(`🌪️ พายุเฮอริเคนถล่มโรงไฟฟ้า! ค่าซ่อมแซมฉุกเฉิน ${stormCost}G`, "warning");
                    showObstaclePopup("🌪️", `พายุเฮอริเคนถล่มเมือง! เสียค่าซ่อม ${stormCost}G`);
                } else if (eventChance < eventThreshold2) {
                    money -= protestCost;
                    logMessage(`🪧 ม็อบประชาชนประท้วงความกดดันด้านพลังงานและสิ่งแวดล้อม! ค่าจัดการ ${protestCost}G`, "danger");
                    showObstaclePopup("🪧", `ประชาชนประท้วงครั้งใหญ่! เสียค่าจัดการ ${protestCost}G`);
                } else {
                    pollution += diseasePollution;
                    logMessage(`🦠 เกิดภาวะหมอกควันพิษสะสม! มลพิษพุ่ง +${diseasePollution}%`, "danger");
                    showObstaclePopup("🦠", `หมอกควันพิษหนาแน่น! มลพิษพุ่ง +${diseasePollution}%`);
                }

                updateUI();
                checkGameStatus();
            }
        }, 1000);

        updateUI();
    </script>

</body>
</html>
