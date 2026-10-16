<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lamp Login Animation</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{
  min-height:100vh;background:#080906;color:#eee;
  font-family:Arial,sans-serif;display:flex;
  justify-content:center;align-items:center;
  overflow:hidden;padding:20px;
}
.scene{
  width:min(900px,100%);min-height:510px;
  display:grid;grid-template-columns:1fr 1fr;
  align-items:center;gap:25px;position:relative;
}
.lamp-area{
  height:420px;position:relative;display:flex;
  justify-content:center;align-items:flex-start;
}
.lamp{
  position:relative;z-index:2;width:180px;height:250px;
  display:flex;flex-direction:column;align-items:center;
}
.wire{width:3px;height:65px;background:#555}
.shade{
  width:125px;height:58px;
  background:linear-gradient(120deg,#24251e,#080906);
  border-radius:65px 65px 12px 12px;
  border-bottom:5px solid #38372a;
  position:relative;z-index:3;
  box-shadow:0 -3px 12px #7772;
}
.bulb{
  width:27px;height:25px;border-radius:50%;
  background:#fff4b0;opacity:.25;
  transition:.5s;
}
.arm{width:3px;height:110px;background:#444}
.base{
  width:100px;height:10px;border-radius:50%;
  background:linear-gradient(#555,#171717);
}
.light{
  position:absolute;top:110px;left:50%;
  transform:translateX(-50%);
  width:260px;height:280px;
  background:linear-gradient(to bottom,#fff0a5aa,#ffdb6233,transparent);
  clip-path:polygon(42% 0,58% 0,100% 100%,0 100%);
  filter:blur(9px);opacity:.65;transition:opacity .5s;
}
.floor-glow{
  position:absolute;top:345px;left:50%;
  transform:translateX(-50%);width:230px;height:35px;
  background:#e6b84a;filter:blur(35px);opacity:.3;
}
.particles{
  position:absolute;inset:0;pointer-events:none;
  background-image:radial-gradient(#f9d76b 1px,transparent 2px);
  background-size:43px 53px;opacity:.15;
  animation:float 8s linear infinite;
}
.form{
  position:relative;z-index:4;
  background:linear-gradient(145deg,#24251fdd,#10110fee);
  border:1px solid #ffffff19;border-radius:15px;
  padding:28px 24px;box-shadow:0 15px 45px #0009;
}
h1{font-size:26px;text-align:center;margin-bottom:8px}
.subtitle{text-align:center;color:#aaa;font-size:13px;margin-bottom:25px}
.field{margin-bottom:16px}
label{display:block;font-size:12px;color:#c6c6bd;margin-bottom:7px}
input{
  width:100%;padding:12px;border:1px solid #49493e;
  border-radius:7px;background:#0c0d0b;color:white;
  outline:none;transition:.3s;
}
input:focus{border-color:#f1c84d;box-shadow:0 0 12px #e8bc3b22}
.options{display:flex;justify-content:space-between;gap:8px;
  font-size:11px;color:#bbb;margin:8px 0 20px}
.options a,.signup a{color:#f1cf60;text-decoration:none}
button{
  width:100%;padding:13px;border:0;border-radius:7px;
  background:linear-gradient(90deg,#e8bc36,#ffdf68);
  color:#191508;font-weight:bold;cursor:pointer;transition:.3s
}
button:hover{box-shadow:0 0 22px #f6cf4b77;transform:translateY(-2px)}
.signup{text-align:center;font-size:12px;color:#aaa;margin-top:20px}
.status{font-size:12px;color:#f7d66d;text-align:center;margin-top:12px}
body.lit .light{opacity:1}
body.lit .bulb{opacity:1;box-shadow:0 0 22px 9px #ffdf72}
body.lit .shade{box-shadow:0 0 30px #ffdc6255}
body.lit .floor-glow{opacity:.7}
@keyframes float{from{background-position:0 0}to{background-position:80px 150px}}
@media(max-width:620px){
  body{padding:15px;overflow:auto}
  .scene{grid-template-columns:1fr;gap:0;max-width:390px}
  .lamp-area{height:220px;transform:scale(.76);transform-origin:top center;margin-bottom:-45px}
  .light{height:220px}
  .floor-glow{top:315px}
  .form{padding:24px 20px}
}
</style>
</head>
<body>
<div class="particles"></div>
<main class="scene">
  <div class="lamp-area">
    <div class="light"></div>
    <div class="floor-glow"></div>
    <div class="lamp">
      <div class="wire"></div>
      <div class="shade"></div>
      <div class="bulb"></div>
      <div class="arm"></div>
      <div class="base"></div>
    </div>
  </div>

  <form class="form" id="loginForm">
    <h1>Welcome Back</h1>
    <p class="subtitle">Sign in to continue</p>

    <div class="field">
      <label for="email">Email Address</label>
      <input id="email" type="email" placeholder="Enter your email" required>
    </div>

    <div class="field">
      <label for="password">Password</label>
      <input id="password" type="password" placeholder="Enter your password" required>
    </div>

    <div class="options">
      <label><input type="checkbox" style="width:auto"> Remember me</label>
      <a href="#forgot" id="forgot">Forgot password?</a>
    </div>

    <button type="submit">Sign In →</button>
    <p class="status" id="status" aria-live="polite"></p>
    <p class="signup">New here? <a href="#signup" id="signup">Create account</a></p>
  </form>
</main>
<script>
const body = document.body;
const email = document.getElementById('email');
const password = document.getElementById('password');
const status = document.getElementById('status');

email.addEventListener('focus', () => body.classList.add('lit'));
password.addEventListener('focus', () => body.classList.add('lit'));
document.addEventListener('click', e => {
  if (!e.target.closest('.form')) body.classList.toggle('lit');
});

document.getElementById('loginForm').addEventListener('submit', e => {
  e.preventDefault();
  status.textContent = 'Demo only — login is not connected to a server.';
});

document.getElementById('forgot').addEventListener('click', e => {
  e.preventDefault();
  status.textContent = 'Password recovery is not configured in this demo.';
});

document.getElementById('signup').addEventListener('click', e => {
  e.preventDefault();
  status.textContent = 'Account creation is not configured in this demo.';
});
</script>
</body>
</html>
