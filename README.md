
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Giftora - Register</title>
  <link rel="stylesheet" href="register.css">
  <script defer src="register.js"></script>
</head>
<body>
  <div class="container">
    <h2>🎁 Welcome to Giftora 🎁</h2>
    <form id="registerForm" class="form">
      <input type="text" id="username" placeholder="👤 Username" required>
      <input type="email" id="email" placeholder="📧 Email" required>
      <input type="text" id="phone" placeholder="📱 Phone Number" required>
      <div class="password-wrapper">
        <input type="password" id="password" placeholder="🔐 Create Password" required>
        <span class="toggle" onclick="togglePassword('password')">👁️</span>
      </div>
      <div class="password-wrapper">
        <input type="password" id="confirmPassword" placeholder="🔁 Confirm Password" required>
        <span class="toggle" onclick="togglePassword('confirmPassword')">👁️</span>
      </div>
      <button type="submit">🎉 Register</button>
      <p id="message"></p>
    </form>
    <a href="login.html">Already have an account? Login</a>
  </div>
</body>
</html>

REGISTER.CSS
/* General styling */
body {
  font-family: 'Comic Sans MS', cursive, sans-serif;
  background: linear-gradient(to right, #ffe3e3, #ffc6ff);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

/* Container */
.container {
  background: white;
  padding: 2em;
  border-radius: 1em;
  box-shadow: 0 0 20px #ffb6b9;
  text-align: center;
  width: 90%;
  max-width: 400px;
  animation: slideIn 1s ease;
}

.container h2 {
  color: #ff66b3;
  margin-bottom: 20px;
}

/* Form Styling */
.form input {
  display: block;
  width: 100%;
  padding: 10px;
  margin: 10px 0;
  border-radius: 10px;
  border: 1px solid #ddd;
  font-size: 16px;
}

.password-wrapper {
  position: relative;
}

.toggle {
  position: absolute;
  right: 15px;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  font-size: 16px;
}

/* Register Button */
button {
  background-color: #ff66b3;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 10px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
  margin-top: 10px;
}

button:hover {
  background-color: #ff1493;
}

/* Message Text */
#message {
  margin-top: 10px;
  color: #ff1493;
  font-weight: bold;
}

/* Animation */
@keyframes slideIn {
  from {
    transform: translateY(-50px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

/* Responsive */
@media (max-width: 500px) {
  .container {
    padding: 1.5em;
  }
}


REGISTER.JS

// Toggle password visibility
function togglePassword(id) {
  const input = document.getElementById(id);
  input.type = input.type === 'password' ? 'text' : 'password';
}

// Register form submit handler
document.getElementById("registerForm").addEventListener("submit", function (e) {
  e.preventDefault();

  const username = document.getElementById("username").value.trim();
  const email = document.getElementById("email").value.trim();
  const phone = document.getElementById("phone").value.trim();
  const password = document.getElementById("password").value.trim();
  const confirmPassword = document.getElementById("confirmPassword").value.trim();
  const message = document.getElementById("message");

  const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[\W_]).{6,}$/;

  if (!passwordRegex.test(password)) {
    message.textContent = "Password must include upper, lower, digit & special char.";
    return;
  }

  if (password !== confirmPassword) {
    message.textContent = "DO NOT MATCH PASSWORD";
    return;
  }

  // Check if user already exists
  const users = JSON.parse(localStorage.getItem("users")) || [];
  const exists = users.some(user => user.email === email || user.username === username);
  if (exists) {
    message.textContent = "User already exists.";
    return;
  }

  // Store new user
  users.push({ username, email, phone, password });
  localStorage.setItem("users", JSON.stringify(users));

  // Also set current profile for profile page
  localStorage.setItem("giftoraUser", JSON.stringify({ username, email, phone, address: "Not Provided" }));

  message.textContent = "REGISTRATION SUCCESSFUL!";
  setTimeout(() => window.location.href = "login.html", 2000);
});





