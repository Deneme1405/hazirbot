# HAZIRBOT MODÜLÜ
​
- Bu modül sayesinde en kompleksi komutları bile yalnızca bir satır kod ile kullanabileceksiniz!
​
- Yapmanız gereken yalnızca `const hazirbot = require('hazirbot')` kodu ile modülümüzü tanıtıp, `npm install github:barbarbar338/hazirbot` komutu ile modülü indirmek
​
- Modülün kullanıldığı örnek bir bot olarak [Pinkie Pie](https://discordapp.com/oauth2/authorize?client_id=442380790542630912&scope=bot&permissions=2146958591) botunu sunucunuza davet edebilirsiniz!
# KURULUM
​
- `npm init` komutu ile `package.json` dosyasını oluşturun
- [Discord Developer](https://discordapp.com/developers/applications/) sayfasından botunuzu oluşturun, `token` ve `client id` değerlerini bir yere kaydedin
- Bot klasörünüzün ana dizinine `bot.js | app.js | index.js | server.js` adlı bot dosyanızı oluşturun ve içerisine verdiğimiz örnek taslağı atın
- Bot klasörünüzin ana dizinine `komutlar` klasörü oluşturun. içerisine komutlarımızı atacağız.
- Komutlar klasörünün içerisine `komut_adı.js` adlı dosya oluşturup içerisine verdiğimiz komut taslağını atın.
- Bot dosyanızın içerisindeki bilgileri doldurduğunuzda botunuz otomatik olarak çevrimiçi hale gelir!
​
# KOMUTLAR VE KULLANIMI
​
**ascii**       =>  client.komut.ascii(mesaj) 
**hesapla**     =>  client.komut.hesapla(işlem)
**eightBall**   =>  client.komut.eightBall(soru) 
**temizle**     =>  client.komut.temzile(miktar)
**çeviri**      =>  client.komut.çeviri(dil, mesaj)
**atasözü**     =>  client.komut.atasözü()|
**yaz**         =>  client.komut.yaz(mesaj) 
**afk**         =>  client.komut.afk(sebep) 
**banner**      =>  client.komut.banner(mesaj)
**bitcoin**     =>  client.komut.bitcoin()
**emojiyazı**   =>  client.komut.emojiyazı(mesaj)
**fakemesaj**   =>  client.komut.fakemesaj(kişi, mesaj)
**oynat**       =>  client.müzik.oynat(link/isim)
**radyo**       =>  client.müzik.radyo(kanal)

​
# TASLAKLAR
​
- `bot.js | app.js | index.js | server.js` taslağı
```js
const hazirbot = require("hazirbot");
const client = new hazirbot.HazirPie({
    token: "  ", //bot tokeniniz
    prefix: "  ", //tercih ettiğiniz prefiz
    sahip: ["  "] //kendi id'niz ( "," ile ayırarak birden çok ekleyebilirsiniz)
});
​
client.on("message", message => {
  if (message.author.bot) return;
  if (message.content.indexOf(client.ayarlar.prefix) !== 0) return;
​
  const args = message.content.slice(client.ayarlar.prefix.length).trim().split(/ +/g);
  const komut = args.shift().toLowerCase();
​
  try {
    let komutDosyası = require(`./komutlar/${komut}.js`);
    komutDosyası.run(client, message, args);
  } catch (err) {
    console.error(err);
  }
});
​
client.giris();
```
​
- `komutlar/komut_adı.js` taslağı
```js
const Discord = require('discord.js')
const hazirbot = require("hazirbot")
​
module.exports.run = async (client, message, args) => {
