<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tienda Sebxr Mods</title>

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

.popup{
display:none;
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,0.8);
justify-content:center;
align-items:center;
z-index:999;
}

.popup-content{
background:#111;
border:2px solid #00ff88;
padding:30px;
border-radius:15px;
width:320px;
text-align:center;
max-height:90vh;
overflow:auto;
}

.cerrar{
float:right;
font-size:30px;
cursor:pointer;
color:#00ff88;
}

</style>
</head>
<body>

<!-- LOGIN -->

<div id="loginBox" class="card">

<h1>
LOGIN / REGISTRO
</h1>

<input
type="email"
id="email"
placeholder="Correo">

<input
type="password"
id="password"
placeholder="Contraseña">

<button onclick="login()">
INICIAR SESIÓN
</button>

<button onclick="register()">
REGISTRARSE
</button>

<p id="error"></p>

</div>

<!-- PANEL -->

<div id="panel" style="display:none;">

<h1>
TIENDA SEBXR MODS
</h1>

<div class="card">

<h2>
💰 Créditos:
<span id="creditos">0</span>
</h2>

<button onclick="abrirCreditos()">
Recargar Créditos
</button>

</div>

<!-- MIS KEYS -->

<div class="card">

<h2>
🔑 Mis Keys
</h2>

<div id="misKeys">

<p>
No tienes keys
</p>

</div>

</div>

<!-- HISTORIAL -->

<div class="card">

<h2>
🧾 Historial
</h2>

<div id="historialCompras">

<p>
Sin compras
</p>

</div>

</div>

<!-- PRODUCTOS -->

<div class="grid">

<!-- PRODUCTO 1 -->

<div class="product">

<img src="https://yt3.googleusercontent.com/pAJ7h-NCLwPkeqvO6qZu4_prNDaVGKgocR41XnCv0rCXzw_iJ7qX7rMkOnMVpGAVSEU9XDdKzns=s160-c-k-c0x00ffffff-no-rj">

<h2>
Panel Sebxr Mods
</h2>

<p>
Panel premium sin blacklist
</p>

<button onclick="abrirDuraciones('Panel Sebxr Mods')">
Comprar
</button>

</div>

<!-- PRODUCTO 2 -->

<div class="product">

<img src="https://i.imgur.com/u6dF9V7.png">

<h2>
Aimbot disimulado
</h2>

<p>
Aimbot premium estable
</p>

<button onclick="abrirDuraciones('Aimbot disimulado')">
Comprar
</button>

</div>

<!-- PRODUCTO 3 -->

<div class="product">

<img src="https://i.imgur.com/fdKQxYh.png">

<h2>
Spotify Premium
</h2>

<p>
Spotify sin anuncios premium
</p>

<button onclick="abrirDuraciones('Spotify Premium')">
Comprar
</button>

</div>

</div>

</div>

<!-- POPUP CREDITOS -->

<div id="popupCreditos" class="popup">

<div class="popup-content">

<span class="cerrar"
onclick="cerrarCreditos()">

×

</span>

<h2>
RECARGAR
</h2>

<input
type="number"
id="cantidadCreditos"
placeholder="Cantidad créditos"
oninput="calcularPrecio()">

<p id="precioFinal">
Total: $0 COP
</p>

<input
type="text"
id="cuponInput"
placeholder="Cupón">

<button onclick="aplicarCupon()">
Aplicar Cupón
</button>

<p id="cuponEstado"></p>

<button onclick="mostrarMetodos()">
Continuar
</button>

<div id="metodosPago" style="display:none;">

<button onclick="mostrarPago('NEQUI','3001234567')">
NEQUI
</button>

<button onclick="mostrarPago('PAYPAL','correo@paypal.com')">
PAYPAL
</button>

<br><br>

<a
href="https://wa.me/573001234567"
target="_blank">

<button>
ENVIAR COMPROBANTE
</button>

</a>

</div>

</div>

</div>

<!-- POPUP PAGO -->

<div id="popupPago" class="popup">

<div class="popup-content">

<span class="cerrar"
onclick="cerrarPago()">

×

</span>

<h2 id="tituloPago"></h2>

<p id="infoPago"></p>

</div>

</div>

<!-- POPUP DURACIONES -->

<div id="popupDuraciones" class="popup">

<div class="popup-content">

<span class="cerrar"
onclick="cerrarDuraciones()">

×

</span>

<h2 id="tituloDuracion"></h2>

<button onclick="seleccionarDuracion('1 Día',20)">
1 Día - 20 créditos
</button>

<button onclick="seleccionarDuracion('7 Días',80)">
7 Días - 80 créditos
</button>

<button onclick="seleccionarDuracion('1 Mes',150)">
1 Mes - 150 créditos
</button>

<button onclick="seleccionarDuracion('1 Año',1000)">
1 Año - 1000 créditos
</button>

</div>

</div>

<!-- POPUP KEY -->

<div id="popupKey" class="popup">

<div class="popup-content">

<h2>
COMPRA EXITOSA
</h2>

<p>
Tu key:
</p>

<h3 id="keyGenerada"></h3>

<button onclick="copiarKey()">
COPIAR KEY
</button>

<br><br>

<button onclick="cerrarKey()">
CERRAR
</button>

</div>

</div>

<script type="module">

import { initializeApp }
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

import {
getAuth,
signInWithEmailAndPassword,
createUserWithEmailAndPassword,
onAuthStateChanged
}
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

import {
getFirestore,
doc,
getDoc,
setDoc,
updateDoc,
increment,
collection,
addDoc,
query,
where,
getDocs,
deleteDoc
}
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

// FIREBASE

const firebaseConfig = {

apiKey: "AIzaSyBtbovWtH-fnSA2KqbobIFjtbNtcicsi-k",

authDomain:
"pagina-de-productos-680db.firebaseapp.com",

projectId:
"pagina-de-productos-680db",

storageBucket:
"pagina-de-productos-680db.firebasestorage.app",

messagingSenderId:
"393545047716",

appId:
"1:393545047716:web:07fb512bc7ee970bdbd031",

measurementId:
"G-EZBWVZDK5E"

};

const app =
initializeApp(firebaseConfig);

const auth =
getAuth(app);

const db =
getFirestore(app);

let descuentoActual = 0;

// GENERAR KEY

function generarKey(){

const chars =
"ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";

let key = "SEBXR-";

for(let i=0;i<4;i++){

key += chars.charAt(
Math.floor(
Math.random()*chars.length
)
);

}

key += "-";

for(let i=0;i<4;i++){

key += chars.charAt(
Math.floor(
Math.random()*chars.length
)
);

}

return key;

}

// LOGIN

window.login =
async function(){

const emailValue =
email.value;

const passwordValue =
password.value;

try{

await signInWithEmailAndPassword(
auth,
emailValue,
passwordValue
);

}catch(err){

error.innerHTML =
err.message;

}

}

// REGISTER

window.register =
async function(){

const emailValue =
email.value;

const passwordValue =
password.value;

try{

const cred =
await createUserWithEmailAndPassword(
auth,
emailValue,
passwordValue
);

await setDoc(
doc(db,"users",cred.user.uid),
{

email:emailValue,

uid:cred.user.uid,

creditos:0

});

alert(
"CUENTA CREADA"
);

}catch(err){

error.innerHTML =
err.message;

}

}

// AUTH

onAuthStateChanged(
auth,
async(user)=>{

if(user){

loginBox.style.display =
"none";

panel.style.display =
"block";

// ONLINE USER

await setDoc(
doc(db,"onlineUsers",user.uid),
{

email:user.email,

uid:user.uid,

device:
navigator.userAgent,

lastSeen:
new Date().toISOString(),

online:true

});

const userRef =
doc(db,"users",user.uid);

const userSnap =
await getDoc(userRef);

const datos =
userSnap.data();

creditos.innerHTML =
datos.creditos || 0;

// KEYS

const keysQuery =
query(
collection(db,"keys"),
where("uid","==",user.uid)
);

const keysSnap =
await getDocs(keysQuery);

let htmlKeys = "";

keysSnap.forEach((docu)=>{

const data =
docu.data();

htmlKeys += `

<div class="product">

<h3>${data.producto}</h3>

<p>
🔑 ${data.key}
</p>

<p>
📌 ${data.estado}
</p>

</div>

`;

});

if(htmlKeys == ""){

htmlKeys =
"<p>No tienes keys</p>";

}

misKeys.innerHTML =
htmlKeys;

// HISTORIAL

const comprasQuery =
query(
collection(db,"purchases"),
where("uid","==",user.uid)
);

const comprasSnap =
await getDocs(comprasQuery);

let htmlCompras = "";

comprasSnap.forEach((docu)=>{

const data =
docu.data();

htmlCompras += `

<div class="product">

<h3>${data.producto}</h3>

<p>
📅 ${data.fecha}
</p>

<p>
💰 ${data.creditos}
 créditos
</p>

</div>

`;

});

if(htmlCompras == ""){

htmlCompras =
"<p>Sin compras</p>";

}

historialCompras.innerHTML =
htmlCompras;

}

});

// CERRAR ONLINE

window.addEventListener(
"beforeunload",
async()=>{

const user =
auth.currentUser;

if(user){

await deleteDoc(
doc(
db,
"onlineUsers",
user.uid
)
);

}

});

// CREDITOS

window.abrirCreditos =
function(){

popupCreditos.style.display =
"flex";

}

window.cerrarCreditos =
function(){

popupCreditos.style.display =
"none";

}

window.calcularPrecio =
function(){

let c =
parseInt(
cantidadCreditos.value
)||0;

let total =
c * 50;

if(descuentoActual > 0){

total =
total -
(total * descuentoActual / 100);

}

precioFinal.innerHTML =

"Total: $" +

Math.floor(total)
.toLocaleString()

+ " COP";

}

// CUPON

window.aplicarCupon =
async function(){

const codigo =
cuponInput.value
.toUpperCase();

if(!codigo){

return;

}

try{

const ref =
doc(db,"coupons",codigo);

const snap =
await getDoc(ref);

if(!snap.exists()){

cuponEstado.innerHTML =
"❌ Cupón inválido";

return;

}

const data =
snap.data();

if(!data.activo){

cuponEstado.innerHTML =
"❌ Cupón desactivado";

return;

}

if(data.usos >= data.maxUsos){

cuponEstado.innerHTML =
"❌ Cupón agotado";

return;

}

descuentoActual =
data.descuento;

cuponEstado.innerHTML =

"✅ Cupón aplicado";

calcularPrecio();

await updateDoc(ref,{

usos:
increment(1)

});

}catch(err){

console.log(err);

}

}

// METODOS

window.mostrarMetodos =
function(){

metodosPago.style.display =
"block";

}

// PAGO

window.mostrarPago =
function(titulo,info){

popupPago.style.display =
"flex";

tituloPago.innerHTML =
titulo;

infoPago.innerHTML =
info;

}

window.cerrarPago =
function(){

popupPago.style.display =
"none";

}

// DURACIONES

window.abrirDuraciones =
function(prod){

popupDuraciones.style.display =
"flex";

tituloDuracion.innerHTML =
prod;

}

window.cerrarDuraciones =
function(){

popupDuraciones.style.display =
"none";

}

// COMPRAR

window.seleccionarDuracion =
async function(
duracion,
precio
){

try{

const user =
auth.currentUser;

let creditosActuales =
Number(
creditos.innerText
)||0;

if(creditosActuales < precio){

cerrarDuraciones();

abrirCreditos();

return;

}

const nuevaKey =
generarKey();

const userRef =
doc(db,"users",user.uid);

await updateDoc(userRef,{

creditos:
creditosActuales - precio

});

// KEY

await addDoc(
collection(db,"keys"),
{

key:nuevaKey,

producto:
tituloDuracion.innerHTML,

duracion:duracion,

estado:"activa",

uid:user.uid,

email:user.email,

creada:
new Date().toISOString()

});

// HISTORIAL

await addDoc(
collection(db,"purchases"),
{

uid:user.uid,

producto:
tituloDuracion.innerHTML,

duracion:duracion,

creditos:precio,

fecha:
new Date()
.toLocaleString()

});

creditos.innerHTML =

creditosActuales - precio;

popupKey.style.display =
"flex";

keyGenerada.innerHTML =
nuevaKey;

cerrarDuraciones();

}catch(err){

console.log(err);

alert(
"ERROR EN LA COMPRA"
);

}

}

// KEY

window.cerrarKey =
function(){

popupKey.style.display =
"none";

}

window.copiarKey =
function(){

navigator.clipboard.writeText(
keyGenerada.innerText
);

alert(
"KEY COPIADA"
);

}

</script>

</body>
</html>
