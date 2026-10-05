<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>PIZTOK - Fixed</title>
<script src="https://cdn.tailwindcss.com"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
body{background:#000;color:#fff;margin:0;font-family:sans-serif;overflow:hidden}
.video-feed{height:100vh;overflow-y:scroll;scroll-snap-type:y mandatory}
.video-item{height:100vh;scroll-snap-align:start;position:relative;background:#111;display:flex;align-items:center;justify-content:center}
.video-item video,.video-item img{width:100%;height:100%;object-fit:cover}
.overlay{position:absolute;bottom:80px;left:10px;right:70px}
.actions{position:absolute;right:10px;bottom:100px;display:flex;flex-direction:column;gap:20px;align-items:center}
.action-btn{width:50px;height:50px;background:rgba(255,255,255,0.15);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:22px}
</style>
</head>
<body>
<div id="auth" class="fixed inset-0 bg-black z-[100] flex items-center justify-center p-6">
<div class="w-full max-w-sm">
<h1 class="text-4xl font-black text-center">PIZTOK</h1>
<p class="text-center text-zinc-400 mb-6">Fixed - No Key Needed</p>
<input id="username" placeholder="Username (type admin for admin)" class="w-full bg-zinc-900 p-4 rounded-xl mb-3 outline-none">
<input id="password" type="password" placeholder="Password" class="w-full bg-zinc-900 p-4 rounded-xl mb-4 outline-none">
<button onclick="login()" class="w-full bg-white text-black p-4 rounded-xl font-bold">Login / Create</button>
<p id="authMsg" class="text-red-500 text-center mt-3"></p>
</div>
</div>
<div class="video-feed" id="feed"></div>
<div class="fixed bottom-0 left-0 right-0 bg-black border-t border-zinc-800 flex justify-around p-3 z-50">
<button class="text-white"><i class="fa fa-home"></i><br><span class="text-[10px]">Home</span></button>
<button onclick="document.getElementById('uploadModal').classList.remove('hidden')"><i class="fa fa-plus"></i><br><span class="text-[10px]">Post</span></button>
<button onclick="showProfile()"><i class="fa fa-user"></i><br><span class="text-[10px]">Profile</span></button>
</div>
<div id="uploadModal" class="hidden fixed inset-0 bg-black z-[80] p-4">
<h2 class="text-xl font-bold">Create Post</h2>
<input type="file" id="fileInput" accept="video/*,image/*" class="w-full bg-zinc-900 p-4 rounded-xl my-3">
<div id="preview" class="hidden mb-3"><video id="prevVideo" class="w-full h-64 bg-zinc-900 rounded-xl" controls></video><img id="prevImg" class="w-full h-64 object-cover rounded-xl hidden"></div>
<select id="filter" class="w-full bg-zinc-900 p-3 rounded-xl mb-3"><option value="">No Filter</option><option value="grayscale(100%)">Grayscale</option><option value="sepia(100%)">Sepia</option><option value="contrast(150%)">Contrast</option><option value="blur(2px)">Blur</option></select>
<input id="sound" placeholder="Sound name" class="w-full bg-zinc-900 p-3 rounded-xl mb-3">
<input id="caption" placeholder="Caption #fyp" class="w-full bg-zinc-900 p-3 rounded-xl mb-3">
<button onclick="postVideo()" class="w-full bg-[#fe2c55] p-4 rounded-xl font-bold">POST</button>
<button onclick="this.parentElement.classList.add('hidden')" class="w-full mt-2 bg-zinc-800 p-3 rounded-xl">Close</button>
</div>
<div id="profileModal" class="hidden fixed inset-0 bg-black z-[70] overflow-y-auto pb-20 p-4">
<button onclick="this.parentElement.classList.add('hidden')"><i class="fa fa-arrow-left"></i> Back</button>
<div class="text-center mt-6">
<img id="avatar" src="https://via.placeholder.com/100" class="w-24 h-24 rounded-full mx-auto object-cover">
<input type="file" id="avatarInput" accept="image/*" class="mt-2 text-xs">
<h2 id="profileName" class="text-xl font-bold mt-3">@user</h2>
<p id="profileBio" class="text-zinc-400 text-sm"></p>
<div class="mt-6 space-y-3 text-left">
<button class="w-full bg-zinc-900 p-4 rounded-xl" onclick="editBio()">Edit Bio & Link</button>
<button class="w-full bg-zinc-900 p-4 rounded-xl">💼 Business Account</button>
<button class="w-full bg-zinc-900 p-4 rounded-xl">💰 Wallet Balance: $<span id="balance">0.00</span></button>
<button class="w-full bg-zinc-900 p-4 rounded-xl">⭐ Monetization Request</button>
<button class="w
