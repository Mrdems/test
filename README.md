   const { Client, LocalAuth } = require('whatsapp-web.js');
   const qrcode = require('qrcode-terminal');

   const client = new Client({
       authStrategy: new LocalAuth()
   });

   client.on('qr', (qr) => {
       qrcode.generate(qr, { small: true });
       console.log('QR code reçu, scannez-le !');
   });

   client.on('ready', () => {
       console.log('Client est prêt !');
   });

   client.on('message', message => {
       if (message.body === '!ping') {
           message.reply('Pong!');
       }
   });

   client.initialize();
   
