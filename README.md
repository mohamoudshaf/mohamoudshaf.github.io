<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Who Will Win the Biggest Battle Ever!</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial Black', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            position: relative;
        }

        /* Animated background particles */
        .particle {
            position: absolute;
            border-radius: 50%;
            animation: float 6s infinite ease-in-out;
            opacity: 0.3;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
        }

        .container {
            text-align: center;
            z-index: 10;
            padding: 20px;
            max-width: 900px;
            width: 100%;
        }

        h1 {
            color: #fff;
            font-size: clamp(2rem, 6vw, 4rem);
            text-shadow: 4px 4px 8px rgba(0,0,0,0.3);
            margin-bottom: 60px;
            letter-spacing: 2px;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .battle-zone {
            display: flex;
            gap: 40px;
            justify-content: center;
            align-items: center;
            flex-wrap: wrap;
            position: relative;
            min-height: 400px;
        }

        .fighter {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.3);
            transition: transform 0.3s ease;
            cursor: pointer;
            min-width: 250px;
        }

        .fighter:hover {
            transform: scale(1.05);
        }

        #ilyas-fighter {
            position: absolute;
            transition: none;
        }

        #dad-fighter {
            position: relative;
        }

        .avatar {
            width: 150px;
            height: 150px;
            margin: 0 auto 20px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 80px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.2);
        }

        #dad-avatar {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
        }

        #ilyas-avatar {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        }

        .fighter-name {
            font-size: 2rem;
            margin-bottom: 15px;
            color: #333;
            font-weight: bold;
        }

        .fighter-desc {
            color: #666;
            margin-bottom: 20px;
            font-size: 0.9rem;
            font-family: Arial, sans-serif;
        }

        .choose-btn {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.2rem;
            font-weight: bold;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .choose-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }

        #ilyas-btn {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        }

        .vs {
            font-size: 4rem;
            color: #fff;
            text-shadow: 3px 3px 6px rgba(0,0,0,0.3);
            font-weight: bold;
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            z-index: 5;
            animation: rotate 3s infinite linear;
        }

        @keyframes rotate {
            from { transform: translate(-50%, -50%) rotate(0deg); }
            to { transform: translate(-50%, -50%) rotate(360deg); }
        }

        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background: #f0f;
            position: absolute;
            animation: confetti-fall 3s linear infinite;
        }

        @keyframes confetti-fall {
            to {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        @media (max-width: 768px) {
            .battle-zone {
                flex-direction: column;
                gap: 200px;
            }

            .vs {
                font-size: 3rem;
            }

            h1 {
                margin-bottom: 40px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🏆 WHO WILL WIN THE BIGGEST BATTLE EVER! 🏆</h1>
        
        <div class="battle-zone">
            <div class="vs">VS</div>
            
            <div class="fighter" id="dad-fighter">
                <div class="avatar" id="dad-avatar">💪</div>
                <div class="fighter-name">DAD</div>
                <div class="fighter-desc">Big, Strong & Cool!</div>
                <button class="choose-btn" id="dad-btn" onclick="chooseDad()">CHOOSE DAD</button>
            </div>

            <div class="fighter" id="ilyas-fighter">
                <div class="avatar" id="ilyas-avatar">🥷</div>
                <div class="fighter-name">ILYAS</div>
                <div class="fighter-desc">Superhero Ninja!</div>
                <button class="choose-btn" id="ilyas-btn">CHOOSE ILYAS</button>
            </div>
        </div>
    </div>

    <script>
        const ilyasFighter = document.getElementById('ilyas-fighter');
        const ilyasBtn = document.getElementById('ilyas-btn');
        let ilyasX = window.innerWidth > 768 ? window.innerWidth * 0.65 : window.innerWidth / 2;
        let ilyasY = window.innerHeight / 2;

        // Initialize Ilyas position
        function initializeIlyasPosition() {
            if (window.innerWidth > 768) {
                ilyasX = window.innerWidth * 0.65;
                ilyasY = window.innerHeight / 2;
            } else {
                ilyasX = window.innerWidth / 2;
                ilyasY = window.innerHeight * 0.7;
            }
            updateIlyasPosition();
        }

        function updateIlyasPosition() {
            ilyasFighter.style.left = ilyasX + 'px';
            ilyasFighter.style.top = ilyasY + 'px';
            ilyasFighter.style.transform = 'translate(-50%, -50%)';
        }

        // Track mouse movement
        document.addEventListener('mousemove', (e) => {
            const mouseX = e.clientX;
            const mouseY = e.clientY;
            
            const rect = ilyasFighter.getBoundingClientRect();
            const buttonCenterX = rect.left + rect.width / 2;
            const buttonCenterY = rect.top + rect.height / 2;
            
            const distance = Math.sqrt(
                Math.pow(mouseX - buttonCenterX, 2) + 
                Math.pow(mouseY - buttonCenterY, 2)
            );
            
            // If mouse gets within 150px, run away!
            if (distance < 150) {
                const angle = Math.atan2(buttonCenterY - mouseY, buttonCenterX - mouseX);
                const moveDistance = 100;
                
                ilyasX += Math.cos(angle) * moveDistance;
                ilyasY += Math.sin(angle) * moveDistance;
                
                // Keep within bounds
                const margin = 150;
                ilyasX = Math.max(margin, Math.min(window.innerWidth - margin, ilyasX));
                ilyasY = Math.max(margin, Math.min(window.innerHeight - margin, ilyasY));
                
                updateIlyasPosition();
            }
        });

        function chooseDad() {
            // Create confetti effect
            for (let i = 0; i < 100; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.left = Math.random() * window.innerWidth + 'px';
                    confetti.style.top = '-10px';
                    confetti.style.background = `hsl(${Math.random() * 360}, 100%, 50%)`;
                    confetti.style.animationDelay = Math.random() * 0.5 + 's';
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => confetti.remove(), 3000);
                }, i * 30);
            }
            
            alert('🎉 DAD WINS! Of course he does! 💪');
        }

        // Add floating particles
        for (let i = 0; i < 20; i++) {
            const particle = document.createElement('div');
            particle.className = 'particle';
            particle.style.width = Math.random() * 30 + 10 + 'px';
            particle.style.height = particle.style.width;
            particle.style.left = Math.random() * 100 + '%';
            particle.style.top = Math.random() * 100 + '%';
            particle.style.background = `hsl(${Math.random() * 360}, 70%, 60%)`;
            particle.style.animationDelay = Math.random() * 6 + 's';
            document.body.appendChild(particle);
        }

        // Initialize and handle window resize
        initializeIlyasPosition();
        window.addEventListener('resize', initializeIlyasPosition);
    </script>
</body>
</html>
