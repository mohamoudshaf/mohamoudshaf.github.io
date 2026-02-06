<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Who will win the biggest battle ever!</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #0c0c3d 0%, #1a1a5e 100%);
            color: white;
            min-height: 100vh;
            overflow-x: hidden;
            text-align: center;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 10;
        }
        
        header {
            margin-bottom: 50px;
            padding-top: 30px;
        }
        
        h1 {
            font-size: 3.5rem;
            text-transform: uppercase;
            margin-bottom: 20px;
            text-shadow: 0 0 15px rgba(255, 255, 255, 0.7);
            background: linear-gradient(to right, #ff6b6b, #ffd93d);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            animation: pulse 2s infinite alternate;
        }
        
        @keyframes pulse {
            0% { text-shadow: 0 0 10px rgba(255, 107, 107, 0.7); }
            100% { text-shadow: 0 0 20px rgba(255, 217, 61, 0.9); }
        }
        
        .subtitle {
            font-size: 1.5rem;
            margin-bottom: 40px;
            color: #a0a0ff;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            line-height: 1.5;
        }
        
        .battlefield {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-wrap: wrap;
            gap: 80px;
            margin: 60px 0;
            min-height: 300px;
            position: relative;
        }
        
        .vs-text {
            font-size: 4rem;
            font-weight: bold;
            color: #ff6b6b;
            text-shadow: 0 0 20px rgba(255, 107, 107, 0.7);
            z-index: 5;
        }
        
        .fighter {
            display: flex;
            flex-direction: column;
            align-items: center;
            transition: transform 0.3s;
        }
        
        .fighter-name {
            font-size: 2rem;
            margin-bottom: 20px;
            padding: 10px 20px;
            border-radius: 10px;
            font-weight: bold;
            text-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
        }
        
        .dad .fighter-name {
            background-color: rgba(41, 128, 185, 0.7);
            color: #d6eaf8;
        }
        
        .ilyas .fighter-name {
            background-color: rgba(231, 76, 60, 0.7);
            color: #fadbd8;
        }
        
        .button-container {
            position: relative;
            width: 280px;
            height: 280px;
        }
        
        .action-button {
            width: 100%;
            height: 100%;
            border: none;
            border-radius: 50%;
            font-size: 1.8rem;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 15px;
            transition: all 0.3s;
            position: absolute;
            top: 0;
            left: 0;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
        }
        
        .action-button:active {
            transform: scale(0.95);
        }
        
        .dad-button {
            background: linear-gradient(145deg, #2980b9, #1c5d87);
            color: white;
            z-index: 3;
        }
        
        .dad-button:hover {
            background: linear-gradient(145deg, #3498db, #2980b9);
            box-shadow: 0 0 30px rgba(52, 152, 219, 0.8);
            transform: scale(1.05);
        }
        
        .ilyas-button {
            background: linear-gradient(145deg, #e74c3c, #c0392b);
            color: white;
            z-index: 2;
        }
        
        .button-emoji {
            font-size: 4rem;
        }
        
        .instructions {
            max-width: 800px;
            margin: 40px auto;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            font-size: 1.2rem;
            line-height: 1.6;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .instructions h2 {
            margin-bottom: 15px;
            color: #ffd93d;
        }
        
        .fireworks-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 100;
            opacity: 0;
            transition: opacity 1s;
        }
        
        .firework {
            position: absolute;
            width: 5px;
            height: 5px;
            border-radius: 50%;
            box-shadow: 0 0 10px #fff;
        }
        
        .explosion {
            position: absolute;
            width: 5px;
            height: 5px;
            border-radius: 50%;
        }
        
        .result-message {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0);
            background: rgba(0, 0, 0, 0.9);
            padding: 40px;
            border-radius: 20px;
            text-align: center;
            z-index: 200;
            width: 90%;
            max-width: 600px;
            border: 3px solid gold;
            box-shadow: 0 0 50px rgba(255, 215, 0, 0.8);
            transition: transform 0.8s;
        }
        
        .result-message h2 {
            font-size: 3.5rem;
            color: gold;
            margin-bottom: 20px;
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.7);
        }
        
        .result-message p {
            font-size: 1.5rem;
            margin-bottom: 30px;
            line-height: 1.6;
        }
        
        .close-result {
            background: gold;
            color: #000;
            border: none;
            padding: 12px 30px;
            font-size: 1.2rem;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        .close-result:hover {
            background: #ffed4e;
            transform: scale(1.05);
        }
        
        footer {
            margin-top: 50px;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.2);
            color: #a0a0ff;
            font-size: 0.9rem;
        }
        
        /* Responsive design */
        @media (max-width: 768px) {
            h1 {
                font-size: 2.5rem;
            }
            
            .subtitle {
                font-size: 1.2rem;
            }
            
            .battlefield {
                gap: 30px;
            }
            
            .vs-text {
                font-size: 2.5rem;
                order: 3;
                width: 100%;
                margin-top: 20px;
            }
            
            .button-container {
                width: 200px;
                height: 200px;
            }
            
            .button-emoji {
                font-size: 3rem;
            }
            
            .action-button {
                font-size: 1.4rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Who will win the biggest battle ever!</h1>
            <p class="subtitle">Two contenders enter, but only one can claim victory. Will it be Dad with his legendary strength, or Ilyas with his ninja skills? Place your bet!</p>
        </header>
        
        <div class="battlefield">
            <div class="fighter dad">
                <div class="fighter-name">Dad</div>
                <div class="button-container">
                    <button class="action-button dad-button" id="dadButton">
                        <span class="button-emoji">💪</span>
                        <span>Choose Dad</span>
                    </button>
                </div>
            </div>
            
            <div class="vs-text">VS</div>
            
            <div class="fighter ilyas">
                <div class="fighter-name">Ilyas</div>
                <div class="button-container">
                    <button class="action-button ilyas-button" id="ilyasButton">
                        <span class="button-emoji">🥷</span>
                        <span>Try to Choose Ilyas</span>
                    </button>
                </div>
            </div>
        </div>
        
        <div class="instructions">
            <h2>How This Battle Works</h2>
            <p><strong>Dad's Button:</strong> Stays in place and can be clicked. When clicked, it triggers a victory celebration with fireworks!</p>
            <p><strong>Ilyas's Button:</strong> Uses ninja skills to dodge your mouse cursor. The closer you get, the faster it moves away, making it impossible to click. A true test of reflexes!</p>
            <p><em>Hint: Try to click on Ilyas's button if you can, but Dad is the only choice that will work!</em></p>
        </div>
        
        <footer>
            <p>The Biggest Battle Ever &copy; 2023 | May the best contender win!</p>
        </footer>
    </div>
    
    <!-- Fireworks container -->
    <div class="fireworks-container" id="fireworksContainer"></div>
    
    <!-- Victory message -->
    <div class="result-message" id="resultMessage">
        <h2>Victory for Dad! 🏆</h2>
        <p>Dad's mighty strength has prevailed in the biggest battle ever! The celebration begins with a spectacular fireworks display!</p>
        <p>Ilyas put up a good fight with his ninja skills, but in the end, experience and power won the day.</p>
        <button class="close-result" id="closeResult">Close Celebration</button>
    </div>
    
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const dadButton = document.getElementById('dadButton');
            const ilyasButton = document.getElementById('ilyasButton');
            const fireworksContainer = document.getElementById('fireworksContainer');
            const resultMessage = document.getElementById('resultMessage');
            const closeResult = document.getElementById('closeResult');
            
            // Variables for Ilyas button movement
            let ilyasX = 0;
            let ilyasY = 0;
            let mouseX = 0;
            let mouseY = 0;
            const buttonRadius = 140;
            const movementFactor = 0.3;
            
            // Position Ilyas button in center initially
            const buttonContainer = ilyasButton.parentElement;
            const containerRect = buttonContainer.getBoundingClientRect();
            ilyasX = containerRect.width / 2;
            ilyasY = containerRect.height / 2;
            
            // Track mouse movement for Ilyas button
            document.addEventListener('mousemove', function(e) {
                mouseX = e.clientX;
                mouseY = e.clientY;
                
                // Get Ilyas button position relative to viewport
                const buttonRect = ilyasButton.getBoundingClientRect();
                const buttonCenterX = buttonRect.left + buttonRect.width / 2;
                const buttonCenterY = buttonRect.top + buttonRect.height / 2;
                
                // Calculate distance between mouse and button center
                const distanceX = mouseX - buttonCenterX;
                const distanceY = mouseY - buttonCenterY;
                const distance = Math.sqrt(distanceX * distanceX + distanceY * distanceY);
                
                // If mouse is close to the button, move it away
                if (distance < 150) {
                    // Calculate movement direction (away from mouse)
                    const moveX = (distanceX / distance) * movementFactor * (150 - distance);
                    const moveY = (distanceY / distance) * movementFactor * (150 - distance);
                    
                    // Update button position
                    ilyasX -= moveX;
                    ilyasY -= moveY;
                    
                    // Keep button within container bounds
                    ilyasX = Math.max(buttonRadius, Math.min(containerRect.width - buttonRadius, ilyasX));
                    ilyasY = Math.max(buttonRadius, Math.min(containerRect.height - buttonRadius, ilyasY));
                    
                    // Apply new position
                    ilyasButton.style.left = (ilyasX - buttonRadius) + 'px';
                    ilyasButton.style.top = (ilyasY - buttonRadius) + 'px';
                }
            });
            
            // Dad button click handler - show fireworks
            dadButton.addEventListener('click', function() {
                // Show fireworks container
                fireworksContainer.style.opacity = '1';
                
                // Create multiple fireworks
                for (let i = 0; i < 50; i++) {
                    setTimeout(() => {
                        createFirework();
                    }, i * 200);
                }
                
                // Show victory message
                setTimeout(() => {
                    resultMessage.style.transform = 'translate(-50%, -50%) scale(1)';
                }, 1000);
                
                // Play victory sound (if allowed)
                playVictorySound();
            });
            
            // Ilyas button click handler - try to prevent clicking
            ilyasButton.addEventListener('click', function(e) {
                // Make it very hard to click by moving the button when attempted
                ilyasX = Math.random() * (containerRect.width - 2 * buttonRadius) + buttonRadius;
                ilyasY = Math.random() * (containerRect.height - 2 * buttonRadius) + buttonRadius;
                
                ilyasButton.style.left = (ilyasX - buttonRadius) + 'px';
                ilyasButton.style.top = (ilyasY - buttonRadius) + 'px';
                
                // Show a brief message that it can't be clicked
                const tempMsg = document.createElement('div');
                tempMsg.textContent = 'Ninja dodged!';
                tempMsg.style.position = 'absolute';
                tempMsg.style.color = '#e74c3c';
                tempMsg.style.fontWeight = 'bold';
                tempMsg.style.fontSize = '1.2rem';
                tempMsg.style.top = (e.clientY - 30) + 'px';
                tempMsg.style.left = (e.clientX - 40) + 'px';
                tempMsg.style.pointerEvents = 'none';
                tempMsg.style.zIndex = '1000';
                document.body.appendChild(tempMsg);
                
                setTimeout(() => {
                    document.body.removeChild(tempMsg);
                }, 1000);
            });
            
            // Close result message
            closeResult.addEventListener('click', function() {
                resultMessage.style.transform = 'translate(-50%, -50%) scale(0)';
                fireworksContainer.style.opacity = '0';
                
                // Clear fireworks after they fade out
                setTimeout(() => {
                    fireworksContainer.innerHTML = '';
                }, 1000);
            });
            
            // Function to create a single firework
            function createFirework() {
                // Create firework particle
                const firework = document.createElement('div');
                firework.classList.add('firework');
                
                // Random position
                const x = Math.random() * window.innerWidth;
                const y = Math.random() * window.innerHeight;
                
                // Random color
                const hue = Math.floor(Math.random() * 360);
                firework.style.backgroundColor = `hsl(${hue}, 100%, 60%)`;
                firework.style.boxShadow = `0 0 10px hsl(${hue}, 100%, 60%)`;
                
                // Position the firework
                firework.style.left = `${x}px`;
                firework.style.top = `${y}px`;
                
                // Add to container
                fireworksContainer.appendChild(firework);
                
                // Create explosion after a delay
                setTimeout(() => {
                    createExplosion(x, y, hue);
                    fireworksContainer.removeChild(firework);
                }, 500);
            }
            
            // Function to create explosion effect
            function createExplosion(x, y, hue) {
                const particles = 15 + Math.floor(Math.random() * 10);
                
                for (let i = 0; i < particles; i++) {
                    const particle = document.createElement('div');
                    particle.classList.add('explosion');
                    
                    // Set color
                    particle.style.backgroundColor = `hsl(${hue}, 100%, 60%)`;
                    particle.style.boxShadow = `0 0 10px hsl(${hue}, 100%, 60%)`;
                    
                    // Initial position
                    particle.style.left = `${x}px`;
                    particle.style.top = `${y}px`;
                    
                    // Random direction and distance
                    const angle = Math.random() * Math.PI * 2;
                    const distance = 30 + Math.random() * 70;
                    const targetX = x + Math.cos(angle) * distance;
                    const targetY = y + Math.sin(angle) * distance;
                    
                    // Add to container
                    fireworksContainer.appendChild(particle);
                    
                    // Animate particle
                    particle.animate([
                        { transform: 'scale(1) translate(0, 0)', opacity: 1 },
                        { transform: `scale(0.5) translate(${Math.cos(angle) * distance}px, ${Math.sin(angle) * distance}px)`, opacity: 0 }
                    ], {
                        duration: 800 + Math.random() * 700,
                        easing: 'cubic-bezier(0.1, 0.8, 0.9, 0.1)'
                    });
                    
                    // Remove particle after animation
                    setTimeout(() => {
                        if (particle.parentNode) {
                            fireworksContainer.removeChild(particle);
                        }
                    }, 1500);
                }
            }
            
            // Function to play victory sound
            function playVictorySound() {
                // Create audio context for simple beep sounds
                try {
                    const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                    
                    // Play a victory fanfare using beeps
                    playNote(audioContext, 523.25, 0.3, 0);   // C5
                    playNote(audioContext, 659.25, 0.3, 300); // E5
                    playNote(audioContext, 783.99, 0.3, 600); // G5
                    playNote(audioContext, 1046.50, 0.5, 900); // C6
                } catch (e) {
                    console.log("Audio not supported or autoplay prevented");
                }
            }
            
            // Function to play a single note
            function playNote(audioContext, frequency, duration, startTime) {
                setTimeout(() => {
                    const oscillator = audioContext.createOscillator();
                    const gainNode = audioContext.createGain();
                    
                    oscillator.connect(gainNode);
                    gainNode.connect(audioContext.destination);
                    
                    oscillator.frequency.value = frequency;
                    oscillator.type = 'sine';
                    
                    gainNode.gain.setValueAtTime(0, audioContext.currentTime);
                    gainNode.gain.linearRampToValueAtTime(0.3, audioContext.currentTime + 0.01);
                    gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + duration);
                    
                    oscillator.start(audioContext.currentTime);
                    oscillator.stop(audioContext.currentTime + duration);
                }, startTime);
            }
            
            // Initialize Ilyas button position
            ilyasButton.style.position = 'absolute';
            ilyasButton.style.left = (ilyasX - buttonRadius) + 'px';
            ilyasButton.style.top = (ilyasY - buttonRadius) + 'px';
        });
    </script>
</body>
</html>
