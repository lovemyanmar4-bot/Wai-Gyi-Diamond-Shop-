# Wai-Gyi-Diamond-Shop-
Mobile Legend diamond Shop 
<!DOCTYPE html>
<html>
<head>
<title>My Shop</title>
<style>
body {
  text-align: center;
  font-family: sans-serif;
  background: black;
  color: white;
}
button {
  padding: 15px;
  margin: 10px;
  width: 200px;
  border: none;
  border-radius: 10px;
  font-size: 16px;
  color: white;
  cursor: pointer;
}
.tiktok { background: red; }
.order { background: green; }
</style>
</head>
<body>

<h1>💎 Diamond Shop 💎</h1>
<p>Follow & Order Now</p>

<a href="https://www.tiktok.com/@u.wai.lin.official.blog" target="_blank">
  <button class="tiktok">TikTok</button>
</a>

<a href="https://t.me/MMxWaiGyi" target="_blank">
  <button class="order">Telegram</button>
</a><!DOCTYPE html>
<html lang="my">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>💎 Wai Gyi Diamond Shop 💎</title>
<style>
body{ font-family:sans-serif; text-align:center; background:linear-gradient(to bottom,#00c3ff,#ffff1c); color:white; margin:0; padding:0;}
h1{margin-top:15px;}
.section-title{margin-top:20px; font-size:20px; font-weight:bold;}
.gems{display:flex; flex-wrap:wrap; justify-content:center; max-height:300px; overflow-y:auto;}
.gem{background:#0077ff; margin:5px; padding:10px; border-radius:10px; width:45%; transition:0.3s; box-shadow:0 0 10px #fff;}
.gem:hover{transform:scale(1.05);}
.selected{border:3px solid yellow; box-shadow:0 0 20px yellow,0 0 40px #fff;}
.weekly{background:gold; color:black; font-weight:bold;}
button{margin-top:5px; padding:6px; border:none; border-radius:6px; background:gold; font-weight:bold; cursor:pointer;}
#cartBox{background:black; padding:10px; margin:10px; border-radius:10px;}
input{margin:5px; padding:8px; border-radius:8px; border:none;}
#checkout{background:limegreen; color:white; padding:10px;}
#paymentBox{display:none; background:black; padding:15px; margin:15px; border-radius:10px;}
</style>
</head>
<body>

<h1>💎 Wai Gyi Diamond Shop 💎</h1>

<div class="section-title">💎 Diamonds</div>
<div class="gems" id="diamondBox"></div>

<div class="section-title">🔥 Pass</div>
<div class="gems" id="passBox"></div>

<div id="cartBox">မရွေးရသေးပါ</div>

<input type="text" id="gameId" placeholder="Game ID">
<input type="text" id="serverId" placeholder="Server ID">

<br>
<button id="checkout" onclick="checkout()">💎 Checkout 💎</button>

<div id="paymentBox">
  <h3>💰 ငွေလွှဲရန်</h3>
  <p>KPay / WavePay</p>
  <p><b>09793212143</b></p>
  <p><b>Wai Lin Aung</b></p>
  <hr>
  <p id="finalOrder"></p>
  <button onclick="sendTelegram()">📩 Telegram ပို့မည်</button>
</div>

<script>
// Diamonds & Passes
const diamonds = [
{name:'စိန် 86', price:5600},{name:'စိန် 172', price:11000},{name:'စိန် 275', price:16700},
{name:'စိန် 343', price:21800},{name:'စိန် 429', price:27200},{name:'စိန် 565', price:33200},
{name:'စိန် 600', price:38000},{name:'စိန် 706', price:43400},{name:'စိန် 878', price:54200},
{name:'စိန် 963', price:59600},{name:'စိန် 1135', price:70200},{name:'စိန် 1220', price:74200},
{name:'စိန် 1412', price:86600},{name:'စိန် 1584', price:97200},{name:'စိန် 1756', price:108200},
{name:'စိန် 2195', price:129800},{name:'စိန် 3245', price:194600},{name:'စိန် 3688', price:216200},
{name:'စိန် 4394', price:259200},{name:'စိန် 5532', price:324200},{name:'စိန် 6238', price:367200},
{name:'စိန် 9288', price:540200},{name:'စိန် 11483', price:669200},{name:'စိန် 12976', price:756200}
];

const passes = [
{name:'1 Weekly Pass', price:6500},{name:'2 Weekly Pass', price:13000},{name:'3 Weekly Pass', price:19500},
{name:'4 Weekly Pass', price:26000},{name:'5 Weekly Pass', price:32500},{name:'6 Weekly Pass', price:39000},
{name:'7 Weekly Pass', price:45500},{name:'8 Weekly Pass', price:52000},{name:'9 Weekly Pass', price:58500},
{name:'10 Weekly Pass', price:65200},{name:'Twilight Pass', price:34200},{name:'Epic Pass', price:16700},
{name:'Elite Pass', price:4200}
];

let selectedItem="", selectedPrice=0, selectedDiv=null;

// Generate items
function createItem(box,data,isWeekly=false){
  const container=document.getElementById(box);
  data.forEach(item=>{
    const div=document.createElement('div');
    div.className='gem';
    if(isWeekly) div.classList.add("weekly");
    div.innerHTML=`${item.name}<br>${item.price} Ks<br><button onclick="selectItem(this,'${item.name}',${item.price})">ရွေးမည်</button>`;
    container.appendChild(div);
  });
}

createItem("diamondBox",diamonds);
createItem("passBox",passes,true);

// Select single item only
function selectItem(btn,name,price){
  if(selectedDiv) selectedDiv.classList.remove("selected");
  selectedDiv=btn.parentElement;
  selectedDiv.classList.add("selected");
  selectedItem=name;
  selectedPrice=price;
  document.getElementById('cartBox').innerText=`ရွေးထားသော item: ${name}\nစျေး: ${price} Ks`;
}

// Checkout
function checkout(){
  const id=document.getElementById('gameId').value;
  const server=document.getElementById('serverId').value;
  if(!id||!server){ alert("Game ID + Server ID ထည့်ပါ"); return;}
  if(!selectedItem){ alert("Item တစ်ခုရွေးပါ"); return;}

  const text=`Game ID: ${id}\nServer ID: ${server}\nItem: ${selectedItem}\nစျေး: ${selectedPrice} Ks`;
  document.getElementById('finalOrder').innerText=text;
  document.getElementById('paymentBox').style.display="block";
}

// Auto Telegram send
function sendTelegram(){
  const id=document.getElementById('gameId').value;
  const server=document.getElementById('serverId').value;
  const msg=encodeURIComponent(
`Game ID: ${id}
Server ID: ${server}
Item: ${selectedItem}
စျေး: ${selectedPrice} Ks

ငွေလွှဲပြီးပါပြီ
✔ Screenshot ပို့ပါ`
  );
  window.open(`https://t.me/MMxWaiGyi?text=${msg}`);
}
</script>

</body>
</html>
