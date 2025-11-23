<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Admin - Cine</title>
  <style>
    body{font-family:system-ui;margin:20px;background:#f5f5f9}
    h1{margin-bottom:10px}
    .panel{background:#fff;padding:14px;border-radius:10px;box-shadow:0 4px 14px rgba(0,0,0,0.1);margin-bottom:18px}
    input,button{padding:8px;border-radius:6px}
    button{border:0;background:#2b6df6;color:#fff;cursor:pointer}
    .room-item{padding:10px;background:#eef2ff;margin:6px 0;border-radius:6px;cursor:pointer}
    .grid{display:grid;gap:8px;margin-top:12px}
    .seat{padding:10px;text-align:center;border-radius:6px;background:#dfe8ff;cursor:pointer;user-select:none}
    .taken{background:#ffd1d1!important;color:#700;pointer-events:auto}
    .row-label{margin-top:10px;font-weight:600}
    #loginPanel{max-width:320px;margin:auto;margin-top:40px;padding:20px;background:#fff;border-radius:10px;box-shadow:0 4px 14px rgba(0,0,0,0.1);text-align:center}
    #loginPanel input{width:90%;margin-bottom:10px;}
  </style>
</head>
<body>

<div id="loginPanel" class="panel">
  <h2>Iniciar sesión (Admin)</h2>
  <input id="username" type="text" placeholder="Usuario" /><br>
  <input id="password" type="password" placeholder="Contraseña" /><br>
  <button id="loginBtn">Entrar</button>
</div>

<div id="home" class="panel" style="display:none">
  <h1>Salas de cine (Admin)</h1>
  <strong>Crear nueva sala</strong><br><br>
  <label>Nombre de la sala / Película<br>
    <input id="roomName" type="text" />
  </label><br><br>
  <label>Número de filas<br>
    <input id="rowCount" type="number" min="1" max="26" value="5" />
  </label><br><br>
  <label>Asientos por fila<br>
    <input id="seatsPerRow" type="number" min="1" max="26" value="8" />
  </label><br><br>
  <label>Fecha y hora de la función<br>
    <input id="roomDateTime" type="datetime-local" />
  </label><br><br>
  <button id="createRoomBtn">Crear sala</button>

  <hr>
  <strong>Salas creadas (en tiempo real)</strong>
  <div id="roomList" style="margin-top:8px"></div>
</div>

<div id="roomView" class="panel" style="display:none"></div>

<!-- Firebase -->
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js"></script>

<script>
// Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyDgbuiYC8m9ExShbS6oniXGEB1YCf2ONNo",
  authDomain: "cine-reserva-online.firebaseapp.com",
  projectId: "cine-reserva-online",
  storageBucket: "cine-reserva-online.firebasestorage.app",
  messagingSenderId: "183959767042",
  appId: "1:183959767042:web:35789d70a73758acf53f1b"
};

firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

function uid(len=10){ const c='0123456789ABCDEF'; let s=''; for(let i=0;i<len;i++) s+=c[Math.floor(Math.random()*c.length)]; return s; }
function letter(n){ return String.fromCharCode(65 + n); }
function escapeHtml(str){ return (str||'').toString().replace(/[&<>"']/g, function(c){ return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',''':'&#39;'}[c]; }); }

const loginPanel = document.getElementById('loginPanel');
const loginBtn = document.getElementById('loginBtn');
const home = document.getElementById('home');
const roomList = document.getElementById('roomList');
const roomView = document.getElementById('roomView');
const createRoomBtn = document.getElementById('createRoomBtn');

loginBtn.addEventListener('click', ()=>{
  const user = document.getElementById('username').value;
  const pass = document.getElementById('password').value;
  if(user==='Hugo' && pass==='Hugo123'){
    loginPanel.style.display='none';
    home.style.display='block';
    startRealtimeRooms();
  } else alert('Usuario o contraseña incorrectos');
});

createRoomBtn.addEventListener('click', async ()=>{
  const name = document.getElementById('roomName').value.trim();
  const rows = parseInt(document.getElementById('rowCount').value,10);
  const per = parseInt(document.getElementById('seatsPerRow').value,10);
  const dateTime = document.getElementById('roomDateTime').value;
  if(!name || !rows || !per || !dateTime) return alert('Datos incompletos');
  try{
    await db.collection('rooms').add({name, rows, seatsPerRow:per, datetime:dateTime, seats:{}, createdAt: firebase.firestore.FieldValue.serverTimestamp()});
    document.getElementById('roomName').value='';
    document.getElementById('roomDateTime').value='';
  }catch(e){ alert('Error al crear sala: '+e.message); }
});

let unsubscribeRooms = null;
function startRealtimeRooms(){
  if(unsubscribeRooms) unsubscribeRooms();
  unsubscribeRooms = db.collection('rooms').orderBy('createdAt','desc').onSnapshot(snapshot=>{
    roomList.innerHTML='';
    if(snapshot.empty){ roomList.innerHTML='<p>No hay salas.</p>'; return; }
    snapshot.forEach(doc=>{
      const r=Object.assign({id:doc.id},doc.data());
      const item=document.createElement('div');
      item.className='room-item';
      const takenCount = r.seats ? Object.keys(r.seats).length : 0;
      item.innerHTML=`<strong>${escapeHtml(r.name)}</strong><br><small>Reservas: ${takenCount}<br>Fecha: ${r.datetime}</small>`;
      item.addEventListener('click',()=>openRoomRealtime(r.id));
      roomList.appendChild(item);
    });
  });
}

let unsubRoomDoc=null;
function openRoomRealtime(roomId){
  if(unsubRoomDoc) unsubRoomDoc();
  home.style.display='none';
  roomView.style.display='block';
  roomView.innerHTML='';
  const backBtn=document.createElement('button');
  backBtn.textContent='Volver';
  backBtn.addEventListener('click', ()=>{ roomView.style.display='none'; home.style.display='block'; if(unsubRoomDoc) unsubRoomDoc(); });
  roomView.appendChild(backBtn);
  const roomRef=db.collection('rooms').doc(roomId);
  unsubRoomDoc = roomRef.onSnapshot(doc=>{
    if(!doc.exists){ alert('Sala eliminada'); backBtn.click(); return; }
    const room = Object.assign({id:doc.id}, doc.data());
    renderRoomView(room, roomRef);
  });
}

function renderRoomView(room, roomRef){
  roomView.innerHTML='';
  const backBtn=document.createElement('button');
  backBtn.textContent='Volver';
  backBtn.addEventListener('click', ()=>{ roomView.style.display='none'; home.style.display='block'; if(unsubRoomDoc) unsubRoomDoc(); });
  roomView.appendChild(backBtn);
  const title=document.createElement('h2'); title.textContent=room.name; roomView.appendChild(title);
  const info=document.createElement('p'); const takenCount = room.seats ? Object.keys(room.seats).length : 0;
  info.innerHTML = `Fecha y hora: ${room.datetime}<br>Reservas: ${takenCount}`; roomView.appendChild(info);
  for(let i=0;i<room.rows;i++){
    const rowLabel=document.createElement('div'); rowLabel.className='row-label'; rowLabel.textContent='Fila '+(i+1); roomView.appendChild(rowLabel);
    const grid=document.createElement('div'); grid.className='grid'; grid.style.gridTemplateColumns=`repeat(${room.seatsPerRow},1fr)`;
    for(let j=0;j<room.seatsPerRow;j++){
      const seat=document.createElement('div'); seat.className='seat'; const seatKey=`${i}-${j}`;
      seat.textContent=letter(j);
      if(room.seats && room.seats[seatKey] && room.seats[seatKey].code) seat.classList.add('taken');
      seat.onclick=function(){
        const name = prompt('Ingrese su nombre para la reserva (admin)');
        if(!name) return;
        const ticketCode = uid(6).toUpperCase();
        db.runTransaction(async tx=>{
          const snap=await tx.get(roomRef);
          const r = snap.data();
          const seats = r.seats || {};
          if(seats[seatKey] && seats[seatKey].code) throw new Error('Asiento ya reservado');
          seats[seatKey]={name, code:ticketCode, createdAt: firebase.firestore.FieldValue.serverTimestamp()};
          tx.update(roomRef, {seats});
        }).then(()=>{ showTicket(name, room, seatKey, ticketCode); }).catch(err=>{ alert(err.message); });
      };
      grid.appendChild(seat);
    }
    roomView.appendChild(grid);
  }
}

function showTicket(name, room, seatKey, ticketCode){
  const seatParts=seatKey.split('-'); const col=parseInt(seatParts[1],10); const fila=parseInt(seatParts[0],10)+1;
  const seatLabel = letter(col);
  const ticketWindow=window.open('','_blank');
  ticketWindow.document.write(`<!DOCTYPE html><html><head><title>Ticket</title><style>body{font-family:system-ui;padding:20px}h2{text-align:center}p{font-size:18px}</style></head><body>
  <h2>Ticket de reserva</h2>
  <p><strong>Nombre:</strong> ${escapeHtml(name)}</p>
  <p><strong>Sala:</strong> ${escapeHtml(room.name)}</p>
  <p><strong>Fecha y hora:</strong> ${escapeHtml(room.datetime)}</p>
  <p><strong>Asiento:</strong> ${seatLabel} - Fila ${fila}</p>
  <p><strong>Código:</strong> ${escapeHtml(ticketCode)}</p>
  <br><button onclick='window.print()'>Imprimir Ticket</button></body></html>`);
  ticketWindow.document.close();
}
</script>
</body>
</html>
