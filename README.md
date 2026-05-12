<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tienda Sebxr Mods</title>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial;
}

body{
background:
linear-gradient(
180deg,
#050505,
#0d0d0d,
#050505
);

color:white;
padding:20px;
min-height:100vh;
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

h2{
margin-bottom:10px;
color:#00ff88;
}

.card{

background:
rgba(20,20,20,0.95);

border:
1px solid #00ff88;

padding:20px;

border-radius:20px;

margin-bottom:20px;

box-shadow:
0 0 15px rgba(0,255,136,0.2);

backdrop-filter:blur(10px);

transition:0.3s;
}

.card:hover{

transform:translateY(-3px);

box-shadow:
0 0 25px rgba(0,255,136,0.5);

}

.grid{

display:grid;

grid-template-columns:
repeat(auto-fit,minmax(280px,1fr));

gap:20px;

}

.product{

background:
rgba(15,15,15,0.95);

border:
1px solid #00ff88;

border-radius:20px;

padding:15px;

transition:0.3s;

box-shadow:
0 0 15px rgba(0,255,136,0.15);

}

.product:hover{

transform:scale(1.03);

box-shadow:
0 0 25px rgba(0,255,136,0.45);

}

.product img{

width:100%;
height:220px;
object-fit:cover;
border-radius:15px;
margin-bottom:10px;
}

button{

background:
linear-gradient(
45deg,
#00ff88,
#00cc6f
);

color:black;

border:none;

padding:12px 20px;

border-radius:12px;

cursor:pointer;

font-weight:bold;

margin-top:10px;

transition:0.3s;

width:100%;
}

button:hover{

transform:scale(1.03);

box-shadow:
0 0 20px #00ff88;

}

input{

width:100%;

padding:12px;

margin-bottom:10px;

border-radius:12px;

border:
1px solid #00ff88;

background:#111;

color:white;

outline:none;

}

.popup{

display:none;

position:fixed;

top:0;
left:0;

width:100%;
height:100%;

background:
rgba(0,0,0,0.85);

justify-content:center;
align-items:center;

z-index:999;

}

.popup-content{

background:
#111;

border:
2px solid #00ff88;

padding:30px;

border-radius:20px;

width:340px;

max-height:90vh;

overflow:auto;

text-align:center;

box-shadow:
0 0 30px rgba(0,255,136,0.4);

animation:popupAnim 0.25s ease;

}

@keyframes popupAnim{

from{

opacity:0;
transform:scale(0.8);

}

to{

opacity:1;
transform:scale(1);

}

}

.cerrar{

float:right;

font-size:30px;

cursor:pointer;

color:#00ff88;

transition:0.3s;

}

.cerrar:hover{

transform:rotate(90deg);

}

#creditos{

color:#00ff88;

font-size:28px;

text-shadow:
0 0 10px #00ff88;

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
🔥 TIENDA SEBXR MODS
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
COMPRAR
</button>

<button onclick="mostrarDescripcion(
'✔ Sin blacklist<br><br>✔ Anti ban<br><br>✔ Keys automáticas<br><br>✔ Actualizaciones premium<br><br>✔ Soporte incluido'
)">
DESCRIPCIÓN
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
COMPRAR
</button>

<button onclick="mostrarDescripcion(
'✔ Aim suave<br><br>✔ Configurable<br><br>✔ Anti ban<br><br>✔ Estable'
)">
DESCRIPCIÓN
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
COMPRAR
</button>

<button onclick="mostrarDescripcion(
'✔ Sin anuncios<br><br>✔ Música ilimitada<br><br>✔ Calidad alta<br><br>✔ Premium estable'
)">
DESCRIPCIÓN
</button>

</div>

</div>

</div>

<!-- POPUP DESCRIPCION -->

<div id="popupDescripcion" class="popup">

<div class="popup-content">

<span
class="cerrar"
onclick="cerrarDescripcion()">

×

</span>

<h2>
DESCRIPCIÓN
</h2>

<p id="descripcionTexto"></p>

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

<p>
⏳ ${data.duracion}
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

}

});

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

alert(
"NO TIENES CRÉDITOS"
);

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

</script>

</body>
</html>
