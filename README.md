<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Password Strength Checker</title>
    <style>
        /* Reset and base styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Roboto', Arial, sans-serif;
            background: url('https://i.ibb.co/yQDzC01/image.png') no-repeat center center/cover;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: #fff;
        }
        .container {
            background: rgba(255, 255, 255, 0.9);
            color: #333;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 400px;
            text-align: center;
            transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
        }
        .container:hover {
            transform: scale(1.02);
            box-shadow: 0px 15px 25px rgba(0, 0, 0, 0.3);
        }
        h1 {
            margin-bottom: 20px;
            font-size: 1.8em;
            font-weight: bold;
            text-transform: uppercase;
            color: #6a11cb;
        }
        .password-container {
            position: relative;
            width: 100%;
        }
        input[type="password"], input[type="text"] {
            width: 100%;
            padding: 12px;
            margin: 15px 0;
            border: 2px solid #ddd;
            border-radius: 8px;
            outline: none;
            font-size: 1em;
            transition: border-color 0.3s ease;
        }
        input:focus {
            border-color: #6a11cb;
        }
        .toggle-password {
            position: absolute;
            right: 10px;
            top: 50%;
            transform: translateY(-50%);
            cursor: pointer;
            font-size: 1.2em;
            color: #6a11cb;
        }
        button {
            background: linear-gradient(135deg, #6a11cb, #2575fc);
            color: #fff;
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            font-size: 1em;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s ease, transform 0.2s ease;
        }
        button:hover {
            background: linear-gradient(135deg, #2575fc, #6a11cb);
            transform: translateY(-2px);
        }
        .strength {
            margin-top: 20px;
            font-size: 1.2em;
            font-weight: bold;
            animation: fadeIn 0.5s ease-in-out;
        }
        .strong {
            color: #28a745;
        }
        .moderate {
            color: #ffc107;
        }
        .weak {
            color: #dc3545;
        }
        /* Fade-in animation */
        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
        /* Responsive design */
        @media (max-width: 768px) {
            .container {
                padding: 20px;
                width: 90%;
            }
            h1 {
                font-size: 1.5em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Password Strength Checker</h1>
        <div class="password-container">
            <input type="password" id="password" placeholder="Enter your password" />
            <span class="toggle-password" onclick="togglePassword()">👁️</span>
        </div>
        <button onclick="checkStrength()">Check Strength</button>
        <div id="strength" class="strength"></div>
    </div>

    <script>
        function checkStrength() {
            const input = document.getElementById('password').value;
            const n = input.length;

            let hasLower = false,
                hasUpper = false,
                hasDigit = false,
                specialChar = false;

            const specialChars = new Set(['!', '@', '#', '$', '%', '^', '&', '*', '(', ')', '-', '+']);

            for (let char of input) {
                if (char >= 'a' && char <= 'z') hasLower = true;
                if (char >= 'A' && char <= 'Z') hasUpper = true;
                if (char >= '0' && char <= '9') hasDigit = true;
                if (specialChars.has(char)) specialChar = true;
            }

            const strengthDiv = document.getElementById('strength');

            // Determine password strength
            if (hasDigit && hasLower && hasUpper && specialChar && n >= 8) {
                strengthDiv.textContent = "Strong";
                strengthDiv.className = "strength strong";
            } else if ((hasLower || hasUpper || specialChar) && n >= 6) {
                strengthDiv.textContent = "Moderate";
                strengthDiv.className = "strength moderate";
            } else {
                strengthDiv.textContent = "Weak";
                strengthDiv.className = "strength weak";
            }
        }

        function togglePassword() {
            const passwordInput = document.getElementById('password');
            const toggleIcon = document.querySelector('.toggle-password');
            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                toggleIcon.textContent = '🙈';
            } else {
                passwordInput.type = 'password';
                toggleIcon.textContent = '👁️';
            }
        }
    </script>
</body>
</html>
