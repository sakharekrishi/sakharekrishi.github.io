# sakharekrishi.github.io<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Sakhare Krishi Store</title>

<style>
body{margin:0;font-family:Segoe UI,Arial;background:#0b1220;color:#fff}
header{background:#020617;padding:15px;text-align:center;font-size:22px;font-weight:bold;color:#22c55e}
.banner{padding:15px;text-align:center;background:linear-gradient(90deg,#0f172a,#020617);font-size:18px}
.controls{padding:10px;text-align:center}
input,select,textarea{padding:10px;border-radius:10px;border:none;width:90%;max-width:400px;margin:5px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:15px;padding:15px}
.card{background:#111827;border-radius:16px;padding:12px;box-shadow:0 0 10px #22c55e}
.card img{width:100%;height:160px;object-fit:cover;border-radius:12px}
.btn{background:#22c55e;border:none;padding:10px;border-radius:20px;width:100%;cursor:pointer;margin-top:8px}
.btn:hover{background:#16a34a}
.cart-btn{position:fixed;bottom:20px;right:20px;background:#22c55e;color:black;padding:15px;border-radius:50%;font-size:20px;cursor:pointer}
.cart{position:fixed;top:0;right:-100%;width:320px;height:100%;background:#020617;padding:15px;transition:.3s;overflow:auto}
.cart.open{right:0}
.cart-item{border-bottom:1px solid #333;padding:6px 0}
.lang{text-align:center;padding:10px}
</style>
</head>
<body>

<header>🌾 Sakhare Krishi Seva Kendra</header>

<div class="banner">Modern Online Krushi Store – Order directly on WhatsApp</div>

<div class="lang">
<button class="btn" onclick="setLang('en')">English</button>
<button class="btn" onclick="setLang('hi')">हिंदी</button>
<button class="btn" onclick="setLang('mr')">मराठी</button>
</div>

<div class="controls">
<input id="search" placeholder="Search products..." onkeyup="render()" />
<select id="filter" onchange="render()">
<option value="">All Categories</option>
<option value="Herbicide">Herbicide</option>
<option value="Insecticide">Insecticide</option>
<option value="Fungicide">Fungicide</option>
</select>
</div>

<div class="products" id="products"></div>

<div class="cart-btn" onclick="toggleCart()">🛒</div>

<div class="cart" id="cart">
<h2>🧾 Order Cart</h2>
<div id="cartItems"></div>

<h3>Customer Details</h3>
<input id="cname" placeholder="Your Name" />
<input id="cphone" placeholder="Mobile Number" />
<textarea id="caddr" placeholder="Delivery Address"></textarea>

<button class="btn" onclick="checkout()">Place Order on WhatsApp</button>
<button class="btn" onclick="toggleCart()">Close</button>
</div>

<script>
const phone="911234567891";

const products=[
{name:"Bayer Roundup",type:"Herbicide",price:520,img:"https://m.media-amazon.com/images/I/61F0H6X4VtL.jpg"},
{name:"Tata Rallis Coragen",type:"Insecticide",price:1250,img:"https://5.imimg.com/data5/SELLER/Default/2022/6/AF/TS/IN/106841230/tata-rallis-coragen.jpg"},
{name:"UPL Saaf",type:"Fungicide",price:699,img:"https://5.imimg.com/data5/SELLER/Default/2021/2/PU/LC/XJ/12242049/up-50-500x500.jpg"},
{name:"BASF Product",type:"Insecticide",price:850,img:"https://m.media-amazon.com/images/I/61h2JbF7jUL.jpg"},
{name:"Bayer Confidor",type:"Insecticide",price:720,img:"https://5.imimg.com/data5/SELLER/Default/2022/8/DP/ZW/XZ/147372180/confidor-insecticide.jpg"},
{name:"Tata Rallis Koranda",type:"Insecticide",price:480,img:"https://5.imimg.com/data5/SELLER/Default/2021/1/VU/EE/EP/104084507/koranda-insecticide.jpg"}
];

let cart=[]; 
let lang="en";

const labels={
en:{add:"Add to Cart"},
hi:{add:"कार्ट में डालें"},
mr:{add:"कार्टमध्ये जोडा"}
};

function render(){
const s=document.getElementById("search").value.toLowerCase();
const f=document.getElementById("filter").value;
const box=document.getElementById("products");
box.innerHTML="";
products.filter(p=>(!f||p.type===f)&&p.name.toLowerCase().includes(s))
.forEach(p=>{
box.innerHTML+=`
<div class="card">
<img src="${p.img}">
<h3>${p.name}</h3>
<p>${p.type}</p>
<p>₹${p.price}</p>
<button class="btn" onclick="add('${p.name}')">${labels[lang].add}</button>
</div>`;
});
}

function add(n){cart.push(n);alert(n+" added");}
function toggleCart(){document.getElementById("cart").classList.toggle("open");updateCart();}
function updateCart(){
const box=document.getElementById("cartItems");
box.innerHTML="";
cart.forEach(i=>box.innerHTML+=`<div class="cart-item">${i}</div>`);
}

function checkout(){
const name=document.getElementById("cname").value;
const phoneUser=document.getElementById("cphone").value;
const addr=document.getElementById("caddr").value;
if(!name||!phoneUser||!addr||cart.length==0){alert("Fill all details");return;}
const msg=`New Order\nName:${name}\nPhone:${phoneUser}\nAddress:${addr}\nItems:\n${cart.join("\n")}`;
window.open(`https://wa.me/${phone}?text=${encodeURIComponent(msg)}`);
}

function setLang(l){lang=l;render();}

render();
</script>
</body>
</html>
