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

onst socketIO = require('socket.io');
const io = socketIO(1234);

io.on('connection', (socket) => {

  socket.emit('merhaba socket.io', {
    mesaj: 'Merhaba ben özel bir mesajım.',
    tarih: `${new Date().getHours()}:${new Date().getMinutes()}`
  });

});
Sunucudan gönderilen veri istemci tarafında uygun bir şekilde alınarak gerekli işlemler yapılır.

let socket = io("http://localhost:1234");

socket.on("merhaba socket.io", (veri) => {
  document.body.textContent = veri.mesaj + " " + veri.tarih;
});

Olay sunucudan oluşturulabileceği gibi istemci tarafından da oluşturulabilir.

let socket = io("http://localhost:1234");

socket.emit("merhaba socket.io", {
  mesaj: "Merhaba ben özel bir mesajım.",
  tarih: new Date().getHours() + ":" + new Date().getMinutes()
});
İstemci tarafından tetiklenen olay sunucu tarafında on metodu ile yakalanarak işlem yapılır.

const socketIO = require('socket.io');
const io = socketIO(1234);

io.on('connection', (socket) => {

  socket.on('merhaba socket.io', (veri) => {
    console.log(veri.mesaj + ' ' + veri.tarih);
  });

});

---Diğer istemcilere mesaj atmak
Socket.IO ile bir istemciden diğer istemcilerle iletişim kurmak için socket.broadcast nesnesi kullanılır.

Nesne içerisinde send, on ve emit gibi metotlara sahiptir.

const socketIO = require('socket.io');
const io = socketIO(1234);

io.on('connection', (socket) => {

  socket.broadcast.send('Yeni bir kullanıcı bağlandı: ' + socket.id);
  //socket.broadcast.emit('message', 'Yeni bir kullanıcı bağlandı: ' + socket.id);

});
Sunucu tarafından gönderilen veri benzer şekilde on metodu ile yakalanarak işlem yapılır.

let socket = io("http://localhost:1234");

socket.on("message", (mesaj) => {
  document.body.innerHTML += mesaj + "<br />";
});

Kaynak:https://www.yusufsezer.com.tr/node-js-socket-io/
