<!DOCTYPE html>
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

<div id="loginBox" class="card">

<h1>LOGIN</h1>

<input type="email" id="email" placeholder="Correo">

<input type="password" id="password" placeholder="Contraseña">

<button onclick="login()">
Entrar
</button>

<p id="error"></p>

</div>

<div id="panel" style="display:none;">

<h1>TIENDA</h1>

<div class="card">

<div class="creditos">
💰 Créditos:
<span id="creditos">0</span>
</div>

<h3>Métodos de pago</h3>

<ul>
<li>Nequi</li>
<li>PayPal</li>
<li>Binance</li>
</ul>

<p>
Después de pagar tú agregas créditos manualmente desde Firebase.
</p>

</div>

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
getDoc,
collection,
getDocs,
updateDoc
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

onAuthStateChanged(auth, async(user)=>{

if(user){

document.getElementById("loginBox").style.display =
"none";

document.getElementById("panel").style.display =
"block";


// CARGAR CREDITOS

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


// CARGAR PRODUCTOS

const querySnapshot =
await getDocs(collection(db,"productos"));

let html = "";

querySnapshot.forEach((docu)=>{

const p = docu.data();

html += `

<div class="product">

<img src="${p.imagen}">

<h2>${p.nombre}</h2>

<p>${p.funcion}</p>

<div class="price">
${p.precio} créditos
</div>

<button onclick="comprar('${docu.id}',${p.precio})">
Comprar
</button>

</div>

`;

});

document.getElementById("productos").innerHTML =
html;

}

});

window.comprar = async function(id,precio){

const user =
auth.currentUser;

const userRef =
doc(db,"users",user.uid);

const userSnap =
await getDoc(userRef);

const datos =
userSnap.data();

let creditos =
datos.creditos || 0;

if(creditos < precio){

alert("No tienes suficientes créditos");

return;

}

creditos -= precio;

await updateDoc(userRef,{
creditos:creditos
});

document.getElementById("creditos").innerHTML =
creditos;

alert("Compra realizada");

}

</script>

</body>
</html>
