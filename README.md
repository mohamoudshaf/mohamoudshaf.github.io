<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Who will win the biggest battle ever!</title>

    <style>

        * {

            margin: 0;

            padding: 0;

            box-sizing: border-box;

            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;

        }

        

        body {

            background: linear-gradient(135deg, #0c2461, #1e3799);

            min-height: 100vh;

            display: flex;

            flex-direction: column;

            align-items: center;

            justify-content: center;

            padding: 20px;

            color: white;

            overflow-x: hidden;

        }

        

        .container {

            max-width: 900px;

            width: 100%;

            text-align: center;

            padding: 30px;

            background-color: rgba(0, 0, 0, 0.4);

            border-radius: 20px;

            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5);

            position: relative;

            overflow: hidden;

        }

        

        h1 {

            font-size: 3.5rem;

            margin-bottom: 10px;

            text-shadow: 3px 3px 0 #ff6b6b;

            color: #fff;

            letter-spacing: 2px;

        }

        

        .subtitle {

            font-size: 1.4rem;

            margin-bottom: 40px;

            color: #f8f8f8;

            opacity: 0.9;

        }

        

        .battle-area {

            display: flex;

            justify-content: space-around;

            align-items: center;

            flex-wrap: wrap;

            margin: 50px 0;

            min-height: 350px;

            position: relative;

        }

        

        .versus {

            font-size: 4rem;

            font-weight: bold;

            color: #ffdd59;

            text-shadow: 2px 2px 0 #ff6b6b;

            position: absolute;

            top: 50%;

            left: 50%;

            transform: translate(-50%, -50%);

            z-index: 5;

        }

        

        .fighter {

            width: 300px;

            text-align: center;

            padding: 20px;

            position: relative;

            z-index: 10;

        }

        

        .fighter h2 {

            font-size: 2.2rem;

            margin-bottom: 20px;

            color: #ffdd59;

            text-shadow: 2px 2px 0 #ff6b6b;

        }

        

        .button-container {

            position: relative;

            display: inline-block;

            margin-top: 20px;

        }

        

        .btn {

            padding: 20px 50px;

            font-size: 1.8rem;

            font-weight: bold;

            border: none;

            border-radius: 50px;

            cursor: pointer;

            transition: all 0.3s ease;

            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);

            position: relative;

            z-index: 20;

        }

        

        #dad-btn {

            background: linear-gradient(to right, #4a69bd, #1e3799);

            color: white;

        }

        

        #dad-btn:hover {

            transform: scale(1.05);

            box-shadow: 0 15px 25px rgba(0, 0, 0, 0.4);

            background: linear-gradient(to right, #5c7cfa, #2c3e9e);

        }

        

        #me-btn {

            background: linear-gradient(to right, #ff6b6b, #ee5a52);

            color: white;

            position: relative;

            transition: transform 0.1s linear;

        }

        

        #me-btn:hover {

            cursor: not-allowed;

        }

        

        .instructions {

            background-color: rgba(255, 255, 255, 0.1);

            border-radius: 15px;

            padding: 20px;

            margin-top: 30px;

            font-size: 1.2rem;

            max-width: 800px;

            line-height: 1.6;

        }

        

        .result {

            margin-top: 40px;

            font-size: 2.2rem;

            font-weight: bold;

            color: #ffdd59;

            text-shadow: 2px 2px 0 #ff6b6b;

            min-height: 70px;

            display: flex;

            align-items: center;

            justify-content: center;

        }

        

        .dad-avatar, .me-avatar {

            font-size: 6rem;

            margin-bottom: 10px;

        }

        

        .dad-avatar {

            color: #4a69bd;

        }

        

        .me-avatar {

            color: #ff6b6b;

        }

        

        .escape-count {

            margin-top: 15px;

            font-size: 1.2rem;

            color: #ffdd59;

        }

        

        @media (max-width: 768px) {

            h1 {

                font-size: 2.5rem;

            }

            

            .battle-area {

                flex-direction: column;

                gap: 40px;

            }

            

            .versus {

                position: relative;

                top: 0;

                left: 0;

                transform: none;

                margin: 20px 0;

            }

        }

    </style>

</head>

<body>

    <div class="container">

        <h1>Who will win the biggest battle ever!</h1>

        <p class="subtitle">Only one can emerge victorious... choose your champion!</p>

        

        <div class="battle-area">

            <div class="fighter">

                <div class="dad-avatar">👨‍🦰</div>

                <h2>Dad</h2>

                <div class="button-container">

                    <button id="dad-btn" class="btn">Dad</button>

                </div>

            </div>

            

            <div class="versus">VS</div>

            

            <div class="fighter">

                <div class="me-avatar">🧒</div>

                <h2>Me</h2>

                <div class="button-container">

                    <button id="me-btn" class="btn">Me</button>

                </div>

                <div class="escape-count">Escapes: <span id="escape-count">0</span></div>

            </div>

        </div>

        

        <div class="result" id="result">

            Click "Dad" to see who wins!

        </div>

        

        <div class="instructions">

            <p><strong>How it works:</strong> The "Me" button has a mind of its own and will dodge your cursor when you try to click it! Your only choice is to click the "Dad" button to see who wins the biggest battle ever. Try to catch the "Me" button if you can!</p>

        </div>

    </div>



    <script>

        // Get the buttons and result element

        const dadBtn = document.getElementById('dad-btn');

        const meBtn = document.getElementById('me-btn');

        const result = document.getElementById('result');

        const escapeCountElement = document.getElementById('escape-count');

        

        // Track how many times the "Me" button escapes

        let escapeCount = 0;

        

        // Function to move the "Me" button away from cursor

        function moveButton(event) {

            // Get button position and dimensions

            const buttonRect = meBtn.getBoundingClientRect();

            const buttonX = buttonRect.left + buttonRect.width / 2;

            const buttonY = buttonRect.top + buttonRect.height / 2;

            

            // Get cursor position

            const cursorX = event.clientX;

            const cursorY = event.clientY;

            

            // Calculate distance between cursor and button center

            const distance = Math.sqrt(

                Math.pow(cursorX - buttonX, 2) + 

                Math.pow(cursorY - buttonY, 2)

            );

            

            // If cursor is within 150px of button, move it away

            if (distance < 150) {

                // Calculate direction away from cursor

                const angle = Math.atan2(buttonY - cursorY, buttonX - cursorX);

                

                // Calculate new position

                const moveDistance = 180;

                const newX = buttonX + Math.cos(angle) * moveDistance;

                const newY = buttonY + Math.sin(angle) * moveDistance;

                

                // Get viewport dimensions

                const viewportWidth = window.innerWidth;

                const viewportHeight = window.innerHeight;

                

                // Keep button within viewport bounds

                const buttonWidth = buttonRect.width;

                const buttonHeight = buttonRect.height;

                

                let finalX = newX;

                let finalY = newY;

                

                // Constrain to viewport

                if (newX < buttonWidth / 2 + 10) finalX = buttonWidth / 2 + 10;

                if (newX > viewportWidth - buttonWidth / 2 - 10) finalX = viewportWidth - buttonWidth / 2 - 10;

                if (newY < buttonHeight / 2 + 10) finalY = buttonHeight / 2 + 10;

                if (newY > viewportHeight - buttonHeight / 2 - 10) finalY = viewportHeight - buttonHeight / 2 - 10;

                

                // Apply the new position using transform for smooth movement

                meBtn.style.transform = `translate(${finalX - buttonX}px, ${finalY - buttonY}px)`;

                

                // Increment escape count

                escapeCount++;

                escapeCountElement.textContent = escapeCount;

            }

        }

        

        // Function to reset button position

        function resetButtonPosition() {

            meBtn.style.transform = 'translate(0, 0)';

        }

        

        // Add event listeners for mouse movement

        document.addEventListener('mousemove', moveButton);

        

        // Also move button when it's touched (for mobile)

        meBtn.addEventListener('touchstart', function(event) {

            // Trigger movement for touch

            const touch = event.touches[0];

            const fakeMouseEvent = new MouseEvent('mousemove', {

                clientX: touch.clientX,

                clientY: touch.clientY

            });

            moveButton(fakeMouseEvent);

            event.preventDefault();

        }, { passive: false });

        

        // Prevent clicking on the "Me" button

        meBtn.addEventListener('click', function(event) {

            event.preventDefault();

            event.stopPropagation();

            result.textContent = "Hey! No clicking on me! I'm too quick for you!";

            result.style.color = "#ff6b6b";

            

            // Reset after a moment

            setTimeout(() => {

                result.textContent = "You can only click on Dad!";

                result.style.color = "#ffdd59";

            }, 2000);

            

            return false;

        });

        

        // Handle the "Dad" button click

        dadBtn.addEventListener('click', function() {

            result.textContent = "Dad wins! (Of course he does, he's Dad!) 🏆";

            result.style.color = "#4a69bd";

            

            // Add some celebration effect

            dadBtn.style.transform = 'scale(1.2)';

            dadBtn.style.boxShadow = '0 0 40px #ffdd59';

            

            setTimeout(() => {

                dadBtn.style.transform = 'scale(1.05)';

                dadBtn.style.boxShadow = '0 15px 25px rgba(0, 0, 0, 0.4)';

            }, 300);

        });

        

        // Reset button position periodically to keep it from going off-screen

        setInterval(resetButtonPosition, 3000);

        

        // Initial instructions

        setTimeout(() => {

            result.textContent = "Try to click the 'Me' button if you dare!";

        }, 3000);

    </script>

</body>

</html>
