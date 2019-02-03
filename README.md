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
# KOMUTLAR VE ÖZELLİKLERİ
​
| KOMUT ADI | AÇIKLAMA        | GEREKSİNİM | KULLANIM|
| :-------- |:---------------:|  :-----:|-------:|
| ascii     | Mesajınızı "ascii" formatına çevirir| args splitlemeniz lazım | client.komut.ascii(mesaj) |
| hesapla   | Belirttiğiniz matematik işlemini yapar        |   args splitlemeniz lazım | client.komut.hesapla(işlem)|
| eightBall | Sihirli 8ball'a sorunuzu sorar      |    args splitlemeniz lazım |client.komut.eightBall(soru) |
| temizle   | Belirttiğiniz miktar kadar mesaj siler       |    args splitlemeniz lazım | client.komut.temzile(miktar) | 
| çeviri    | Mesajınızı belirttiğiniz dile çevirir       |    args splitlemeniz lazım | client.komut.çeviri(dil, mesaj) |
| atasözü   | Rastgele bir atasözü söyler        |    bir gereksinim yok | client.komut.atasözü()|
| yaz       | Mesajınızı bota yazdırır        |    args splitlemeniz lazım | client.komut.yaz(mesaj) |
| afk       | Biri sizi etiketlediğinde bot cevap verir       |    args splitlemeniz lazım | client.komut.afk(sebep) |
| banner    | Belirttiğiniz yazıyı "banner" haline getirir       |    args splitlemeniz lazım | client.komut.banner(mesaj) |
| bitcoin   | Bitcoin piyasası hakkında bilgi verir      | bir gereksinim yok | client.komut.bitcoin()|
| emojiyazı | mesajınızı "emoji" formatına çevirir        |    args splitlemeniz lazım | client.komut.emojiyazı(mesaj) |
| fakemesaj | Etiketlediğiniz kullanıcı belirtilen mesajı atmış gibi gösterilir|    args splitlemeniz lazım  | client.komut.fakemesaj(kişi, mesaj) |
| oynat     | Link veya şarkı ismi ile şarkı oynatır       |    args splitlemeniz lazım       | client.müzik.oynat(link/isim) |
| radyo     | Bir radyo kanalı oynatır      |  args splitlemeniz lazım | client.müzik.radyo(kanal) |

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
