<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Tienda Credits</title>

<style>

body{
background:#0a0a0a;
color:white;
font-family:Arial;
padding:20px;
margin:0;
}

h1{
text-align:center;
margin-bottom:30px;
}

#loginBox,
#panel{
max-width:1200px;
margin:auto;
}

.card{
background:#111;
border:1px solid #333;
padding:15px;
border-radius:15px;
margin-bottom:20px;
}

input{
width:100%;
padding:12px;
margin-bottom:10px;
background:#111;
color:white;
border:1px solid #444;
border-radius:10px;
}

button{
padding:12px 20px;
border:none;
border-radius:10px;
background:#00ff88;
color:black;
font-weight:bold;
cursor:pointer;
margin:5px;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:20px;
}

.product{
background:#111;
border:1px solid #333;
border-radius:15px;
padding:15px;
}

.product img{
width:100%;
height:200px;
object-fit:cover;
border-radius:10px;
}

.price{
font-size:22px;
color:#00ff88;
margin-top:10px;
}

.creditos{
font-size:20px;
margin-bottom:20px;
}

</style>

</head>
<body>

<!-- LOGIN -->

<div id="loginBox" class="card">

<h1>LOGIN</h1>

<input type="email" id="email" placeholder="Correo">

<input type="password" id="password" placeholder="Contraseña">

<button onclick="login()">
Entrar
</button>

<p id="error"></p>

</div>

<!-- PANEL -->

<div id="panel" style="display:none;">

<h1>TIENDA</h1>

<!-- CREDITOS -->

<div class="card">

<div class="creditos">
💰 Créditos:
<span id="creditos">0</span>
</div>

<h3>Métodos de pago</h3>

<!-- AQUI CAMBIAS LAS CUENTAS -->

<button onclick="mostrarPago('Nequi: 3001234567')">
NEQUI
</button>

<button onclick="mostrarPago('PayPal: pagos@correo.com')">
PAYPAL
</button>

<button onclick="mostrarPago('Binance ID: 123456789')">
BINANCE
</button>

</div>

<!-- PRODUCTOS -->

<div class="grid" id="productos"></div>

</div>

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

import {
getAuth,
signInWithEmailAndPassword,
onAuthStateChanged
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

import {
getFirestore,
doc,
getDoc
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

const firebaseConfig = {

apiKey: "AIzaSyC8cF8i86iqxCUIlOw1ykd_Civxl1qX2FM",
authDomain: "osting-1b3f6.firebaseapp.com",
projectId: "osting-1b3f6",
storageBucket: "osting-1b3f6.firebasestorage.app",
messagingSenderId: "1080144262727",
appId: "1:1080144262727:web:3f42a97c334adb826b2362"

};

const app = initializeApp(firebaseConfig);

const auth = getAuth(app);

const db = getFirestore(app);

// LOGIN

window.login = async function(){

const email =
document.getElementById("email").value;

const password =
document.getElementById("password").value;

try{

await signInWithEmailAndPassword(
auth,
email,
password
);

}catch(err){

document.getElementById("error").innerHTML =
"Login incorrecto";

}

}

// CUANDO INICIA SESION

onAuthStateChanged(auth, async(user)=>{

if(user){

document.getElementById("loginBox").style.display =
"none";

document.getElementById("panel").style.display =
"block";

// CREDITOS

const userRef =
doc(db,"users",user.uid);

const userSnap =
await getDoc(userRef);

if(userSnap.exists()){

const datos =
userSnap.data();

document.getElementById("creditos").innerHTML =
datos.creditos || 0;

}

// =======================
// PRODUCTOS
// =======================

document.getElementById("productos").innerHTML = `

<!-- ================================= -->
<!-- PRODUCTO 1 -->
<!-- ================================= -->

<div class="product">

<!-- AQUI PONES LA IMAGEN -->

<img src="https://i.imgur.com/0rVeh4A.png">

<!-- AQUI PONES EL NOMBRE -->

<h2>Spotify Premium</h2>

<!-- AQUI PONES LA FUNCION -->

<p>
Cuenta premium 1 mes
</p>

<!-- AQUI PONES EL PRECIO -->

<div class="price">
100 créditos
</div>

<button>
Comprar
</button>

</div>

<!-- ================================= -->
<!-- PRODUCTO 2 -->
<!-- ================================= -->

<div class="product">

<img src="https://i.imgur.com/u6dF9V7.png">

<h2>Netflix</h2>

<p>
Cuenta UHD 1 mes
</p>

<div class="price">
150 créditos
</div>

<button>
Comprar
</button>

</div>

`;

}

});

// MOSTRAR PAGOS

window.mostrarPago = function(info){

alert(info);

}

</script>

</body>
</html>
