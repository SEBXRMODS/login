<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sebxr Mods Store</title>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial,sans-serif;
}

body{
background:#050505;
color:white;
padding:20px;
}

h1{
text-align:center;
margin-bottom:20px;
font-size:40px;
color:#00ff88;
text-shadow:
0 0 10px #00ff88,
0 0 20px #00ff88;
}

.card{
background:#111;
border:1px solid #00ff88;
border-radius:20px;
padding:20px;
margin-bottom:20px;
box-shadow:
0 0 20px rgba(0,255,136,0.2);
}

.grid{
display:grid;
grid-template-columns:
repeat(auto-fit,minmax(280px,1fr));
gap:20px;
}

.product{
background:#111;
border:1px solid #00ff88;
border-radius:20px;
padding:15px;
transition:0.3s;
}

.product:hover{
transform:scale(1.03);
box-shadow:
0 0 20px #00ff88;
}

.product img{
width:100%;
height:220px;
object-fit:cover;
border-radius:15px;
margin-bottom:10px;
}

button{
width:100%;
padding:12px;
margin-top:10px;
border:none;
border-radius:12px;
background:#00ff88;
color:black;
font-weight:bold;
cursor:pointer;
transition:0.3s;
}

button:hover{
transform:scale(1.03);
box-shadow:
0 0 15px #00ff88;
}

input{
width:100%;
padding:12px;
margin-top:10px;
border-radius:12px;
border:1px solid #00ff88;
background:#0d0d0d;
color:white;
}

.popup{
display:none;
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,0.85);
justify-content:center;
align-items:center;
z-index:999;
}

.popup-content{
background:#111;
border:2px solid #00ff88;
border-radius:20px;
padding:25px;
width:340px;
max-height:90vh;
overflow:auto;
text-align:center;
}

.cerrar{
float:right;
font-size:30px;
cursor:pointer;
color:#00ff88;
}

#creditos{
font-size:30px;
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
🔥 SEBXR MODS
</h1>

<div class="card">

<h2>
💰 Créditos:
<span id="creditos">0</span>
</h2>

<button onclick="abrirCreditos()">
RECARGAR CRÉDITOS
</button>

</div>

<!-- KEYS -->

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

<!-- PRODUCTOS -->

<div class="grid">

<!-- PRODUCTO -->

<div class="product">

<img src="https://yt3.googleusercontent.com/pAJ7h-NCLwPkeqvO6qZu4_prNDaVGKgocR41XnCv0rCXzw_iJ7qX7rMkOnMVpGAVSEU9XDdKzns=s160-c-k-c0x00ffffff-no-rj">

<h2>
Panel Sebxr Mods
</h2>

<p>
Panel premium sin blacklist
</p>

<button onclick="abrirDuraciones('Panel Sebxr Mods')">
COMPRAR
</button>

<button onclick="mostrarDescripcion(
'✔ Sin blacklist<br><br>✔ Anti ban<br><br>✔ Premium'
)">
DESCRIPCIÓN
</button>

</div>

<!-- PRODUCTO -->

<div class="product">

<img src="https://i.imgur.com/u6dF9V7.png">

<h2>
Aimbot Premium
</h2>

<p>
Aimbot estable anti ban
</p>

<button onclick="abrirDuraciones('Aimbot Premium')">
COMPRAR
</button>

<button onclick="mostrarDescripcion(
'✔ Aim suave<br><br>✔ Configurable'
)">
DESCRIPCIÓN
</button>

</div>

<!-- PRODUCTO -->

<div class="product">

<img src="https://i.imgur.com/fdKQxYh.png">

<h2>
Spotify Premium
</h2>

<p>
Spotify sin anuncios
</p>

<button onclick="abrirDuraciones('Spotify Premium')">
COMPRAR
</button>

<button onclick="mostrarDescripcion(
'✔ Música ilimitada<br><br>✔ Premium'
)">
DESCRIPCIÓN
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
💰 RECARGAR CRÉDITOS
</h2>

<input
type="number"
id="cantidadCreditos"
placeholder="Cantidad de créditos"
oninput="calcularPrecio()">

<input
type="text"
id="cuponInput"
placeholder="Cupón">

<button onclick="aplicarCupon()">
APLICAR CUPÓN
</button>

<p id="cuponInfo"></p>

<h3>
💵 Total:
<span id="precioFinal">
0
</span>
COP
</h3>

<p id="creditosFinal">
0 créditos
</p>

<button onclick="mostrarPagos()">
CONTINUAR
</button>

<div id="metodosPago" style="display:none;">

<hr style="margin:15px 0; border-color:#00ff88;">

<div class="card">

<h3>
NEQUI
</h3>

<p>
3001234567
</p>

<button onclick="copiarNumero()">
COPIAR
</button>

</div>

<div class="card">

<h3>
PAYPAL
</h3>

<p>
tucorreo@paypal.com
</p>

<a
href="https://paypal.me/"
target="_blank">

<button>
ABRIR PAYPAL
</button>

</a>

</div>

<a
id="btnComprobante"
target="_blank">

<button>
ENVIAR COMPROBANTE
</button>

</a>

</div>

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
✅ COMPRA EXITOSA
</h2>

<p>
Tu key:
</p>

<h3 id="keyGenerada"></h3>

<button onclick="copiarKey()">
COPIAR KEY
</button>

<button onclick="cerrarKey()">
CERRAR
</button>

</div>

</div>

<!-- POPUP DESCRIPCION -->

<div id="popupDescripcion" class="popup">

<div class="popup-content">

<span class="cerrar"
onclick="cerrarDescripcion()">

×

</span>

<h2>
DESCRIPCIÓN
</h2>

<p id="descripcionTexto"></p>

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
collection,
addDoc,
query,
where,
getDocs
}
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

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

let descuento = 0;

// LOGIN

window.login =
async function(){

try{

await signInWithEmailAndPassword(
auth,
email.value,
password.value
);

}catch(err){

error.innerHTML =
err.message;

}

}

// REGISTER

window.register =
async function(){

try{

const cred =
await createUserWithEmailAndPassword(
auth,
email.value,
password.value
);

await setDoc(
doc(db,"users",cred.user.uid),
{

email:email.value,
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

const userRef =
doc(db,"users",user.uid);

const userSnap =
await getDoc(userRef);

const datos =
userSnap.data();

creditos.innerHTML =
datos.creditos || 0;

// KEYS

const q =
query(
collection(db,"keys"),
where("uid","==",user.uid)
);

const snap =
await getDocs(q);

let html = "";

snap.forEach((docu)=>{

const data =
docu.data();

html += `

<div class="product">

<h3>${data.producto}</h3>

<p>🔑 ${data.key}</p>

<p>⏳ ${data.duracion}</p>

</div>

`;

});

if(html == ""){

html =
"<p>No tienes keys</p>";

}

misKeys.innerHTML =
html;

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

metodosPago.style.display =
"none";

}

// PRECIO

window.calcularPrecio =
function(){

const cantidad =
Number(
cantidadCreditos.value
)||0;

// 1 CREDITO = 500 COP

let precio =
cantidad * 500;

if(descuento > 0){

precio =
precio - (
precio *
descuento / 100
);

}

precioFinal.innerHTML =
precio.toLocaleString();

creditosFinal.innerHTML =
cantidad + " créditos";

}

// CUPONES

window.aplicarCupon =
function(){

const cupon =
cuponInput.value
.toUpperCase();

if(cupon == "SEBXR10"){

descuento = 10;

cuponInfo.innerHTML =
"✅ 10% OFF";

}
else if(cupon == "SEBXR20"){

descuento = 20;

cuponInfo.innerHTML =
"✅ 20% OFF";

}
else{

descuento = 0;

cuponInfo.innerHTML =
"❌ CUPÓN INVÁLIDO";

}

calcularPrecio();

}

// PAGOS

window.mostrarPagos =
function(){

if(!cantidadCreditos.value){

alert(
"PON UNA CANTIDAD"
);

return;

}

metodosPago.style.display =
"block";

const mensaje =

`Hola quiero recargar ${cantidadCreditos.value} créditos por ${precioFinal.innerText} COP`;

btnComprobante.href =

`https://wa.me/573001234567?text=${encodeURIComponent(mensaje)}`;

}

// COPIAR

window.copiarNumero =
function(){

navigator.clipboard.writeText(
"3001234567"
);

alert(
"NÚMERO COPIADO"
);

}

// DESCRIPCION

window.mostrarDescripcion =
function(texto){

popupDescripcion.style.display =
"flex";

descripcionTexto.innerHTML =
texto;

}

window.cerrarDescripcion =
function(){

popupDescripcion.style.display =
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

await updateDoc(
doc(db,"users",user.uid),
{

creditos:
creditosActuales - precio

});

await addDoc(
collection(db,"keys"),
{

uid:user.uid,
producto:
tituloDuracion.innerHTML,
duracion:duracion,
key:nuevaKey,
estado:"activa"

});

creditos.innerHTML =
creditosActuales - precio;

popupKey.style.display =
"flex";

keyGenerada.innerHTML =
nuevaKey;

cerrarDuraciones();

}catch(err){

alert(
"ERROR EN LA COMPRA"
);

console.log(err);

}

}

// KEY

window.copiarKey =
function(){

navigator.clipboard.writeText(
keyGenerada.innerText
);

alert(
"KEY COPIADA"
);

}

window.cerrarKey =
function(){

popupKey.style.display =
"none";

}

</script>

</body>
</html>
