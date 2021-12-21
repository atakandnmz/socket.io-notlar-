"# socket.io-notlar-" 

---Socket.io kurulumu

npm install socket.io
veya
npm install socket.io --save

---Sunucu oluşturmak

const socketIO = require('socket.io');
const io = socketIO(1234);

io.on('connection', (socket) => {
  console.log('Bir kullanıcı bağlandı: ' + socket.id);

  socket.on('disconnect', () => {
    console.log('Bir kullanıcı ayrıldı: ' + socket.id);
  });
});

---Sunucuya bağlanmak

<script src="http://localhost:1234/socket.io/socket.io.js"></script>
<script>
  let socket = io("http://localhost:1234");
</script>

---Mesaj göndermek
const socketIO = require('socket.io');
const io = socketIO(1234);

io.on('connection', (socket) => {

  socket.send('Hoşgeldiniz sayın ' + socket.id);
  //socket.emit('message', 'Hoşgeldiniz sayın ' + socket.id);

});

---Özel Olay Oluşturmak

const socketIO = require('socket.io');
const io = socketIO(1234);

io.on('connection', (socket) => {

  socket.emit('merhaba socket.io', 'Merhaba ben özel bir olay tarafından gönderiliyorum.');

});

let socket = io("http://localhost:1234");

socket.on("merhaba socket.io", (mesaj) => {
  document.body.textContent = mesaj;
});
