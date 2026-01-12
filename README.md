<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8"/>
    <meta content="width=device-width, initial-scale=1.0" name="viewport"/>
    <title>Registration </title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet"/>
    <style>
        body, html { margin: 0; padding: 0; height: 100%; overflow: hidden; background: #000; }
        iframe { width: 100%; height: 100%; border: none; }

        #predictionBox {
            position: fixed; bottom: 30px; right: 30px;
            width: 200px; background: rgba(5, 10, 20, 0.98);
            backdrop-filter: blur(15px); border-radius: 20px;
            padding: 20px; color: #fff; text-align: center;
            border: 1px solid #00ffff; 
            box-shadow: 0 0 30px rgba(0, 255, 255, 0.5);
            z-index: 999999; cursor: grab; font-family: 'Orbitron', sans-serif;
        }

        .main-title { font-size: 14px; color: #00ffff; font-weight: 900; margin-bottom: 20px; text-shadow: 0 0 10px #00ffff; }
        
        #loginForm input {
            width: 100%; padding: 12px; margin-bottom: 15px;
            background: rgba(255,255,255,0.05); border: 1px solid #333;
            color: #00ffff; border-radius: 10px; text-align: center; outline: none;
        }
        #loginForm button {
            width: 100%; padding: 12px; background: #00ffff;
            color: #000; border: none; font-weight: 900; border-radius: 10px; cursor: pointer;
        }

        #predictionUI { display: none; }
        #bsText { font-size: 45px; font-weight: 900; margin: 15px 0; text-shadow: 0 0 20px currentColor; }
        
        .timer-wrap { 
            background: rgba(255, 204, 0, 0.15); 
            padding: 10px; border-radius: 12px; 
            margin-top: 15px; border: 1px solid #ffcc0044;
        }
        #timerDisplay { font-size: 16px; color: #ffcc00; font-weight: 900; }

        .loader { position: absolute; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); border-radius: 20px; display: none; align-items: center; justify-content: center; z-index: 100; }
        .spinner { width: 30px; height: 30px; border: 3px solid #111; border-top: 3px solid #00ffff; border-radius: 50%; animation: spin 0.8s linear infinite; }
        @keyframes spin { 100% { transform: rotate(360deg); } }
    </style>
</head>
<body oncontextmenu="return false;">

    <iframe src="https://hgzy.bet/#/register?invitationCode=626361698167"></iframe>

    <div id="predictionBox">
        <div id="loginForm">
            <div class="main-title">Registration </div>
            <input id="passwordInput" placeholder="PASSWORD" type="password"/>
            <button onclick="unlockApp()">LOGIN</button>
        </div>

        <div id="predictionUI">
            <div class="main-title">Registration </div>
            <div id="bsText">--</div>
            
            <div class="timer-wrap">
                <div id="timerDisplay">Syncing...</div>
            </div>
            
            <div class="loader" id="loadingOverlay">
                <div class="spinner"></div>
            </div>
        </div>
    </div>

    <script>
        let lastS = -1;
        let isAuth = false;

        function femaleVoice(text) {
            if (!isAuth) return;
            const synth = window.speechSynthesis;
            const utter = new SpeechSynthesisUtterance(text);
            utter.lang = 'bn-BD';
            utter.pitch = 1.4; // Sweet Female Tone
            utter.rate = 1.0; 
            synth.speak(utter);
        }

        function startClock() {
            setInterval(() => {
                if (!isAuth) return;
                const now = new Date();
                const utc = now.getTime() + (now.getTimezoneOffset() * 60000);
                const bd = new Date(utc + (6 * 3600000));
                
                const sec = bd.getSeconds();
                const rem = 30 - (sec % 30);
                
                document.getElementById("timerDisplay").innerText = "Next: 00:" + String(rem).padStart(2, '0');

                if (sec % 30 === 0 && sec !== lastS) {
                    lastS = sec;
                    getSignal();
                }
            }, 1000);
        }

        function getSignal() {
            const load = document.getElementById("loadingOverlay");
            const txt = document.getElementById("bsText");
            
            load.style.display = "flex";
            
            setTimeout(() => {
                const res = Math.random() > 0.5 ? "BIG" : "SMALL";
                txt.innerText = res;
                txt.style.color = (res === "BIG") ? "#00ffff" : "#ff3b3b";
                
                femaleVoice(res === "BIG" ? " ,    " : " ,    ");
                load.style.display = "none";
            }, 1500);
        }

        function unlockApp() {
            const pass = document.getElementById("passwordInput").value;
            if(pass === "123123") {
                isAuth = true;
                document.getElementById("loginForm").style.display = "none";
                document.getElementById("predictionUI").style.display = "block";
                femaleVoice(" ");
                startClock(); //  
                getSignal();  //  
            } else {
                alert(" !");
                window.location.href = "https://t.me/TRADER_2BROTHERS";
            }
        }

        // Draggable Logic (Mobile Friendly)
        const el = document.getElementById("predictionBox");
        let drag = false, boxX, boxY;
        const start = (e) => {
            drag = true;
            let t = e.touches ? e.touches[0] : e;
            boxX = t.clientX - el.offsetLeft; boxY = t.clientY - el.offsetTop;
        };
        const move = (e) => {
            if (!drag) return;
            let t = e.touches ? e.touches[0] : e;
            el.style.left = (t.clientX - boxX) + "px";
            el.style.top = (t.clientY - boxY) + "px";
            el.style.bottom = "auto"; el.style.right = "auto";
        };
        el.addEventListener("mousedown", start);
        el.addEventListener("touchstart", start);
        document.addEventListener("mousemove", move);
        document.addEventListener("touchmove", move);
        document.addEventListener("mouseup", () => drag = false);
        document.addEventListener("touchend", () => drag = false);
    </script>
</body>
</html>
