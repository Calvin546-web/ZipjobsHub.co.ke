index.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ZipJobsHub - Jobs</title>
<style>
  body { font-family: Arial, sans-serif; margin: 0; background: #f4f6f8; color: #222; text-align: center; }
  header { background: #0a2540; color: white; padding: 50px 20px; }
  header h1 { font-size: 42px; margin: 0; }
  .topbar { background: white; padding: 12px; box-shadow: 0 2px 10px rgba(0,0,0,0.05); position: sticky; top: 0; z-index: 10; }
  .topbar a { display: inline-block; margin: 0 5px; padding: 8px 13px; border-radius: 20px; text-decoration: none; font-weight: bold; font-size: 14px; }
  .btn-reg { background: #00c389; color: white; } .btn-login { background: #0a2540; color: white; } .btn-pay { background: #ffc439; color: #003087; } .btn-cv { background: #7c3aed; color: white; }
  .card { background: white; max-width: 520px; margin: 20px auto; padding: 30px; border-radius: 12px; box-shadow: 0 5px 20px rgba(0,0,0,0.1); text-align: left; }
  input, select, textarea { width: 100%; padding: 12px; margin: 8px 0 14px; border: 1px solid #ddd; border-radius: 8px; box-sizing: border-box; font-size: 15px; }
  label { font-weight: bold; font-size: 14px; }
  .btn { display: block; width: 100%; padding: 14px; border: none; border-radius: 8px; font-weight: bold; font-size: 17px; cursor: pointer; text-align:center; text-decoration:none; }
  .register { background: #00c389; color: white; } .paypal { background: #ffc439; color: #003087; }
  .jobs { max-width: 800px; margin: 0 auto 40px; padding: 0 15px; text-align: left; }
  .job { background: white; padding: 20px; border-radius: 12px; margin-bottom: 15px; box-shadow: 0 2px 10px rgba(0,0,0,0.07); }
  .featured { border: 2px solid #00c389; background: #f0fff9; }
  .tag { display: inline-block; background: #eef2ff; color: #0a2540; padding: 4px 10px; border-radius: 20px; font-size: 12px; font-weight: bold; margin-right: 5px; }
  .apply { display: inline-block; background: #0a2540; color: white; padding: 10px 18px; border-radius: 8px; font-weight: bold; margin-top: 10px; cursor: pointer; border: none; font-size: 15px; }
  .steps { max-width: 800px; margin: 15px auto; display: flex; gap: 10px; padding: 0 15px; }
  .step { flex: 1; background: white; padding: 12px; border-radius: 10px; font-size: 13px; font-weight: bold; }
  .step.active { background: #0a2540; color: white; } .step.done { background: #00c389; color: white; }
  .welcome { background: #d4edda; color: #155724; padding: 12px; border-radius: 8px; margin: 15px auto; max-width: 800px; display: none; }
  .pay-notice { background: #fff3cd; color: #856404; padding: 12px; border-radius: 8px; margin: 15px auto; max-width: 800px; display: none; }
  /* Modal */
  .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.6); z-index: 100; overflow-y: auto; }
  .modal-content { background: white; max-width: 500px; margin: 40px auto; padding: 25px; border-radius: 12px; text-align: left; position: relative; }
  .close { position: absolute; right: 15px; top: 10px; font-size: 24px; cursor: pointer; }
  .myapps { max-width: 800px; margin: 0 auto 20px; padding: 0 15px; text-align: left; display: none; }
  .app-item { background: #e6fffa; border-left: 4px solid #00c389; padding: 12px; border-radius: 8px; margin-bottom: 10px; font-size: 14px; }
  footer { padding: 20px; font-size: 13px; color: #888; }
</style>
</head>
<body>
<header><h1>ZipJobsHub</h1><p>Curated remote & US job opportunities, delivered weekly.</p></header>
<div class="topbar">
  <span id="userInfo" style="font-size:14px;"></span>
  <a href="#register" class="btn-reg" id="regBtn">1. Register</a>
  <a href="#pay" class="btn-pay">2. Pay $50</a>
  <a href="#cv" class="btn-cv">Upload CV</a>
  <a href="login.html" class="btn-login" id="loginBtn">Login</a>
  <a href="#" id="logoutBtn" style="display:none; background:#eee; color:#333;" onclick="logout()">Logout</a>
</div>
<div class="steps"><div class="step" id="step1">1. Register</div><div class="step" id="step2">2. Pay $50</div><div class="step" id="step3">3. Apply On Site</div></div>
<div class="welcome" id="welcomeBox"></div>
<div class="pay-notice" id="payNotice">⚠️ You are registered! Now Pay $50 below to unlock Apply.</div>

<div class="myapps" id="myAppsBox"><h3>📋 My Applications</h3><div id="myAppsList"></div></div>

<div class="jobs">
  <h2 style="text-align:center;">🔥 Latest Jobs - Everyone Can View</h2>
  <p style="text-align:center; color:#666; font-size:14px;">👀 View free &nbsp;|&nbsp; 📝 Apply ON SITE after Register + Pay $50</p>
  <div class="job featured"><p style="color:#00a878; font-weight:bold; font-size:12px;">⭐ FEATURED</p><h3>ESG Officer</h3><p><span class="tag">On-site</span> <span class="tag">KES 100,000 - 180,000 / mo</span></p><p><b>Location:</b> Nairobi, Kenya</p><p>ESG Officer role in Agriculture, Environment & Natural Resources.</p><button class="apply" onclick="tryApply('ESG Officer - Nairobi')">Apply On Site 🔒</button></div>
  <div class="job"><h3>Remote Customer Service Representative</h3><p><span class="tag">Remote</span> <span class="tag">$15 - $18 / hour</span></p><p><b>Location:</b> USA - Remote</p><p>Help customers via chat & email. Training provided.</p><button class="apply" onclick="tryApply('Remote Customer Service')">Apply On Site 🔒</button></div>
  <div class="job"><h3>Data Entry Specialist</h3><p><span class="tag">Remote</span> <span class="tag">$14 - $17 / hour</span></p><p><b>Location:</b> USA - Remote</p><p>Enter and update data. Flexible hours.</p><button class="apply" onclick="tryApply('Data Entry Specialist')">Apply On Site 🔒</button></div>
  <div class="job"><h3>Virtual Assistant</h3><p><span class="tag">Remote</span> <span class="tag">$18 - $22 / hour</span></p><p><b>Location:</b> USA - Remote</p><p>Manage emails, schedules, and tasks.</p><button class="apply" onclick="tryApply('Virtual Assistant')">Apply On Site 🔒</button></div>
  <div class="job"><h3>Warehouse Associate</h3><p><span class="tag">On-Site</span> <span class="tag">$17 - $20 / hour</span></p><p><b>Location:</b> Texas, USA</p><p>Packing, sorting, and shipping orders. Weekly pay.</p><button class="apply" onclick="tryApply('Warehouse Associate')">Apply On Site 🔒</button></div>
  <div class="job"><h3>Social Media Moderator</h3><p><span class="tag">Remote</span> <span class="tag">$16 - $19 / hour</span></p><p><b>Location:</b> USA - Remote</p><p>Review posts and comments, keep communities safe.</p><button class="apply" onclick="tryApply('Social Media Moderator')">Apply On Site 🔒</button></div>
</div>

<!-- APPLY MODAL - ON SITE -->
<div class="modal" id="applyModal">
  <div class="modal-content">
    <span class="close" onclick="closeModal()">&times;</span>
    <h2 style="margin-top:0;">Apply for Job</h2>
    <p id="applyJobTitle" style="font-weight:bold; color:#0a2540;"></p>
    <form id="applyForm" action="https://formsubmit.co/marketingnetwork633@gmail.com" method="POST" enctype="multipart/form-data">
      <input type="hidden" name="_subject" value="New Job Application - ZipJobsHub">
      <input type="hidden" name="_captcha" value="false">
      <input type="hidden" name="_template" value="table">
      <input type="hidden" id="hiddenJob" name="Job Applied For" value="">
      <label>Full Name</label><input type="text" id="appName" name="Applicant Name" required>
      <label>Email</label><input type="email" id="appEmail" name="Applicant Email" required>
      <label>Phone / WhatsApp</label><input type="tel" name="Phone" required>
      <label>Why should we hire you? (Short message)</label><textarea name="Cover Message" rows="3" placeholder="I am interested because..." required></textarea>
      <label>Upload Your Resume / CV (PDF, Word)</label><input type="file" name="attachment" accept=".pdf,.doc,.docx" required>
      <button type="submit" class="btn" style="background:#0a2540; color:white;">Submit Application →</button>
    </form>
    <p style="font-size:12px; color:#888; text-align:center;">Your CV will be sent to ZipJobsHub and saved in My Applications.</p>
  </div>
</div>

<!-- SUBMIT CV SECTION -->
<div class="card" id="cv" style="border: 2px solid #7c3aed;">
  <h2 style="text-align:center; margin-top:0;">📄 Submit Your Resume / CV</h2>
  <p style="text-align:center; color:#666; font-size:14px;">Don't see a perfect job? Upload your CV once. We will match you to future jobs.</p>
  <form id="cvForm" action="https://formsubmit.co/marketingnetwork633@gmail.com" method="POST" enctype="multipart/form-data">
    <input type="hidden" name="_subject" value="New CV Submitted - ZipJobsHub Talent Pool">
    <input type="hidden" name="_captcha" value="false">
    <input type="hidden" name="_template" value="table">
    <label>Full Name</label><input type="text" name="Name" placeholder="John Doe" required>
    <label>Email</label><input type="email" name="Email" placeholder="you@email.com" required>
    <label>Phone / WhatsApp</label><input type="tel" name="Phone" placeholder="+254..." required>
    <label>What kind of job do you want?</label>
    <select name="Desired Job" required><option value="">Select</option><option>Customer Service</option><option>Data Entry</option><option>Virtual Assistant</option><option>Warehouse</option><option>Social Media</option><option>Other</option></select>
    <label>Your Skills</label><textarea name="Skills" rows="2" placeholder="e.g. Typing, Excel, Communication..."></textarea>
    <label>Upload CV / Resume (PDF, Word)</label><input type="file" name="attachment" accept=".pdf,.doc,.docx" required>
    <button type="submit" class="btn" style="background:#7c3aed; color:white;">Submit My CV →</button>
  </form>
  <p style="font-size:13px; text-align:center; color:#666;">✅ CV goes to marketingnetwork633@gmail.com</p>
</div>

<div class="card" id="register">
  <h2 style="text-align:center; margin-top:0;">Step 1: Create Your Free Account</h2>
  <form id="regForm" action="https://formsubmit.co/marketingnetwork633@gmail.com" method="POST">
    <input type="hidden" name="_subject" value="New ZipJobsHub Registration!"><input type="hidden" name="_captcha" value="false"><input type="hidden" name="_template" value="table">
    <label>Full Name</label><input type="text" id="name" name="Full Name" required>
    <label>Email Address</label><input type="email" id="email" name="Email" required>
    <label>Phone / WhatsApp</label><input type="tel" name="Phone" required>
    <label>Country</label><select name="Country" required><option value="">Select Country</option><option>Kenya</option><option>Uganda</option><option>Tanzania</option><option>Nigeria</option><option>Ghana</option><option>USA</option><option>Other</option></select>
    <label>Create Password</label><input type="password" id="password" name="Password" required>
    <button type="submit" class="btn register">Register → Go to Payment</button>
  </form>
  <p style="text-align:center;">Already have an account? <a href="login.html"><b>Login Here</b></a></p>
</div>

<div class="card" id="pay" style="border: 2px solid #ffc439;">
  <h2 style="text-align:center; margin-top:0;">Step 2: Pay Lifetime Fee - $50</h2>
  <p style="text-align:center;">Pay once. After payment, PayPal auto-returns and unlocks Apply.</p>
  <a class="btn paypal" href="https://www.paypal.com/ncp/payment/WKEGXU8JZHYTW" target="_blank" onclick="return startPay()">Pay $50 with PayPal →</a>
  <p id="paidMsg" style="text-align:center; color:green; font-weight:bold; display:none;">✅ Payment confirmed! You can now Apply.</p>
</div>
<footer>© 2026 ZipJobsHub. All rights reserved.</footer>

<script>
function checkStatus(){
  var logged = localStorage.getItem('zip_logged_in');
  var urlParams = new URLSearchParams(window.location.search);
  if(urlParams.get('paid') === 'yes' && logged){ localStorage.setItem('zip_paid_' + logged, 'yes'); window.history.replaceState({}, '', 'index.html'); }
  var paid = logged ? localStorage.getItem('zip_paid_' + logged) : null;
  if(logged){
    var user = JSON.parse(localStorage.getItem('zip_user_' + logged) || '{}');
    document.getElementById('welcomeBox').style.display = 'block';
    document.getElementById('welcomeBox').innerText = '✅ Welcome, ' + (user.name || logged) + '! You are registered.';
    document.getElementById('userInfo').innerText = 'Hi, ' + (user.name || logged) + ' 👋 ';
    document.getElementById('regBtn').style.display = 'none';
    document.getElementById('loginBtn').style.display = 'none';
    document.getElementById('logoutBtn').style.display = 'inline-block';
    document.getElementById('step1').classList.add('done'); document.getElementById('step1').innerText = '1. Registered ✅';
    if(paid){
      document.getElementById('step2').classList.add('done'); document.getElementById('step2').innerText = '2. Paid ✅';
      document.getElementById('step3').classList.add('done'); document.getElementById('step3').innerText = '3. Apply Unlocked ✅';
      document.getElementById('paidMsg').style.display = 'block';
      document.querySelectorAll('.apply').forEach(function(b){ b.innerHTML = 'Apply On Site ✅'; });
      showMyApps();
    } else { document.getElementById('payNotice').style.display = 'block'; document.getElementById('step2').classList.add('active'); }
  } else { document.getElementById('step1').classList.add('active'); }
}
function tryApply(jobTitle){
  var logged = localStorage.getItem('zip_logged_in');
  if(!logged){ alert('Step 1: Please Register first to apply for: ' + jobTitle); document.getElementById('register').scrollIntoView({behavior:'smooth'}); return; }
  if(!localStorage.getItem('zip_paid_' + logged)){ alert('Step 2: Please Pay $50 Lifetime Fee to apply.'); document.getElementById('pay').scrollIntoView({behavior:'smooth'}); return; }
  // Open on-site form
  document.getElementById('hiddenJob').value = jobTitle;
  document.getElementById('applyJobTitle').innerText = 'Job: ' + jobTitle;
  var user = JSON.parse(localStorage.getItem('zip_user_' + logged) || '{}');
  document.getElementById('appName').value = user.name || '';
  document.getElementById('appEmail').value = logged;
  document.getElementById('applyModal').style.display = 'block';
}
function closeModal(){ document.getElementById('applyModal').style.display = 'none'; }
function startPay(){
  var logged = localStorage.getItem('zip_logged_in');
  if(!logged){ alert('Please Register first before paying.'); document.getElementById('register').scrollIntoView({behavior:'smooth'}); return false; }
  return true;
}
function showMyApps(){
  var logged = localStorage.getItem('zip_logged_in');
  var apps = JSON.parse(localStorage.getItem('zip_apps_' + logged) || '[]');
  if(apps.length > 0){
    document.getElementById('myAppsBox').style.display = 'block';
    document.getElementById('myAppsList').innerHTML = apps.map(function(a){ return '<div class="app-item">✅ <b>'+a.job+'</b> - Applied on '+a.date+' - Status: Received</div>'; }).join('');
  }
}
function logout(){ localStorage.removeItem('zip_logged_in'); location.reload(); }
document.getElementById('regForm').addEventListener('submit', function(){
  var email = document.getElementById('email').value; var pass = document.getElementById('password').value; var name = document.getElementById('name').value;
  localStorage.setItem('zip_user_' + email, JSON.stringify({name: name, email: email, pass: pass}));
  localStorage.setItem('zip_logged_in', email);
});
document.getElementById('applyForm').addEventListener('submit', function(){
  var logged = localStorage.getItem('zip_logged_in');
  var job = document.getElementById('hiddenJob').value;
  var apps = JSON.parse(localStorage.getItem('zip_apps_' + logged) || '[]');
  apps.push({job: job, date: new Date().toLocaleDateString()});
  localStorage.setItem('zip_apps_' + logged, JSON.stringify(apps));
});
document.getElementById('cvForm').addEventListener('submit', function(){ alert('Thank you! Your CV has been submitted. We will match you to jobs.'); });
window.onclick = function(e){ if(e.target == document.getElementById('applyModal')) closeModal(); }
checkStatus();
<div style="max-width:800px; margin:20px auto; padding:0 15px; text-align:left;">
  <h2 style="text-align:center;">🔥 Latest Jobs - From GoKazini</h2>
  <p style="text-align:center; color:#666; font-size:13px;">Source: gokazini.com - Click Apply to view full details on GoKazini</p>

  <!-- JOB 1 -->
  <div style="background:white; padding:20px; border-radius:12px; margin-bottom:15px; box-shadow:0 2px 10px rgba(0,0,0,0.08);">
    <span style="background:#e6f7ee; color:#00a651; padding:4px 10px; border-radius:20px; font-size:12px; font-weight:bold;">OPERATIONS & CUSTOMER SERVICE</span>
    <h3 style="margin:10px 0 5px;">Specialist, Operations</h3>
    <p style="color:#666; margin:5px 0;">📍 Kenya • Remote &nbsp; | &nbsp; 💰 USD 471/mo</p>
    <p>Operations & customer service role, fully remote from Kenya.</p>
    <a href="https://gokazini.com" target="_blank" style="display:inline-block; background:#0a2540; color:white; padding:10px 20px; border-radius:8px; text-decoration:none; font-weight:bold;">Apply on GoKazini →</a>
  </div>

  <!-- JOB 2 -->
  <div style="background:white; padding:20px; border-radius:12px; margin-bottom:15px; box-shadow:0 2px 10px rgba(0,0,0,0.08);">
    <span style="background:#e6f7ee; color:#00a651; padding:4px 10px; border-radius:20px; font-size:12px; font-weight:bold;">OPERATIONS & CUSTOMER SERVICE</span>
    <h3 style="margin:10px 0 5px;">Founding Membership & Community Lead</h3>
    <p style="color:#666; margin:5px 0;">📍 Nairobi, Kenya • On-site &nbsp; | &nbsp; 💰 Est. KES 80,000 - 150,000/mo</p>
    <p>Lead community & membership growth in Nairobi.</p>
    <a href="https://gokazini.com" target="_blank" style="display:inline-block; background:#0a2540; color:white; padding:10px 20px; border-radius:8px; text-decoration:none; font-weight:bold;">Apply on GoKazini →</a>
  </div>

  <!-- JOB 3 -->
  <div style="background:white; padding:20px; border-radius:12px; margin-bottom:15px; box-shadow:0 2px 10px rgba(0,0,0,0.08);">
    <span style="background:#fff3d6; color:#8a6d00; padding:4px 10px; border-radius:20px; font-size:12px; font-weight:bold;">SUPPLY CHAIN & LOGISTICS</span>
    <h3 style="margin:10px 0 5px;">Storekeeper</h3>
    <p style="color:#666; margin:5px 0;">📍 Tatu City, Kiambu • On-site &nbsp; | &nbsp; 💰 Est. KES 40,000 - 70,000/mo</p>
    <p>Manage stock, inventory and store records in Tatu City.</p>
    <a href="https://gokazini.com" target="_blank" style="display:inline-block; background:#0a2540; color:white; padding:10px 20px; border-radius:8px; text-decoration:none; font-weight:bold;">Apply on GoKazini →</a>
  </div>

  <!-- JOB 4 -->
  <div style="background:white; padding:20px; border-radius:12px; margin-bottom:15px; box-shadow:0 2px 10px rgba(0,0,0,0.08);">
    <span style="background:#e6f7ee; color:#00a651; padding:4px 10px; border-radius:20px; font-size:12px; font-weight:bold;">OPERATIONS & CUSTOMER SERVICE</span>
    <h3 style="margin:10px 0 5px;">Senior Operations Specialist - Remote, Global</h3>
    <p style="color:#666; margin:5px 0;">📍 Global • Remote &nbsp; | &nbsp; 💰 USD 50,000/yr</p>
    <p>Senior remote operations role, open globally.</p>
    <a href="https://gokazini.com" target="_blank" style="display:inline-block; background:#0a2540; color:white; padding:10px 20px; border-radius:8px; text-decoration:none; font-weight:bold;">Apply on GoKazini →</a>
  </div>

  <!-- JOB 5 -->
  <div style="background:white; padding:20px; border-radius:12px; margin-bottom:15px; box-shadow:0 2px 10px rgba(0,0,0,0.08);">
    <span style="background:#e3f0ff; color:#0a2540; padding:4px 10px; border-radius:20px; font-size:12px; font-weight:bold;">SKILLED TRADES & GENERAL SERVICES</span>
    <h3 style="margin:10px 0 5px;">Electrician</h3>
    <p style="color:#666; margin:5px 0;">📍 Nairobi, Kenya • On-site &nbsp; | &nbsp; 💰 Est. KES 35,000 - 60,000/mo</p>
    <p>Electrical installation, repair & maintenance in Nairobi.</p>
    <a href="https://gokazini.com" target="_blank" style="display:inline-block; background:#0a2540; color:white; padding:10px 20px; border-radius:8px; text-decoration:none; font-weight:bold;">Apply on GoKazini →</a>
  </div>

</div>
</footer>
</script>
</body>
</html>