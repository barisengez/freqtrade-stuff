# RISKLER

Yazilimsal bot her yazilim gibi hataya aciktir. Asagidaki riskleri barindirir.

*   Acik pozisyonlar varken bot durabilir ve pozisyonlar acik kalabilir. Manuel mudahale gerektirebilir.
*   Bot ciddi sorunlar yasayip hizli al satlar ile para kaybettirebilir.
*   Sunucular hacklenip Binance API key ler calinabilir. API keyler sadece hesaptaki tutari gormeye ve hesap icinde coin alim-satimi icin kullanilabilir. Hesap disina para transferi riski yoktur.
*   Bot yuksek zararlar edebilir. Konulan stoploss calismayabilir.

# Tanimlar

**Freqtrade:** Bot olarak bahsettigimiz kripto alghoritmic trading yazilimidir.

**Strategy:** Botun alim satima neye gore karar verdiginin mekanizmasidir. Ornegin RSI 70 in uzerine ciktiginda al, 50 nin altina indiginde sat demek bir stratejidir. Ornek strateji adi : NFI v7

![](https://user-images.githubusercontent.com/18678845/125081919-dc5a8b80-e0c6-11eb-9b71-2f9e1977ba1a.png)

**Alim/satim sinyali:** Botun bir coin i almaya/satmaya karar verdigi sinyaldir. Alim islemi candle kapandiktan sonra bir sonraki candle da yapilir. Bot, araliksiz olarak calismaktadir. Alim sinyalleri her bir timeframe de (ornek 5m) bir verilir, yani candle kapandiktan sonra alim karari verilebilir. Satimlar her an olabilir.

![Crypto Trading 101: A Beginner&#39;s Guide to Candlesticks - CoinDesk](https://user-images.githubusercontent.com/18678845/125082935-1710f380-e0c8-11eb-9cac-23da7a81e764.png)

**Timeframe:** Stratejiler 1m (1 dakika), 5m, 1h (1 saat), 4h gibi timeframelerde calisabilir. Bu timeframe sureleri, botun hangi candle lara bakarak karar verdiginin suresidir. Bot, belli bir timeframe de calisirken farkli candle buyukluklerindeki indikatorlerden de faydalanabilir. Ornegin alim satim degerlendirmesi sirasinda 5m timeframe de calisan bot, 1h lik indikatorlere de bakabilir.

**Stoploss:** Acilan bir islemde maksimum kayip oranidir. -%20 stoploss, 100usdt olarak acilan bir islemin degeri 80usdt ye indiginde satilmasi demektir. Sabittir.

**Trailing stoploss:** Yukselen stoplosstur. Acilan pozisyonun fiyati yukseldikce stoploss u yukari ceker. Trailing stoploss sadece artabilir, azalmaz.

![](https://user-images.githubusercontent.com/18678845/125080789-82a59180-e0c5-11eb-8c1a-15aeeff17ffb.png)

**Limit/market emri:** Limit emri coin icin belli bir fiyat koyup bu fiyattan al ya da sat demektir. Market emri borsada ne kadarsa ona gore al ya da sat demektir. Limit emirleri, fiyat istenilen rakama inmezse/cikmazsa gerceklesmeyebilir. Market emrinin avantaji her zaman gerceklesmesidir, dezavantaji limit emrine gore ortalama %0,5 daha kotu fiyata islem yapmasidir. Kacirilan islemlerden kacirilan karlar oranlandiginda market emri daha karli olabilir.

**Pairlist:** Alim/satim icin kullanilan coin listesidir. Volume ya da static olabilir. Static pairlist sabit coin listesi demektir. Volume pair list, en yuksek islem hacmine ait coin listesidir. Volume Pairlist 70 demek, kripto borsasinda en cok islem hacmi olan ilk 70 coin i isle demektir. Volume pairlist 2-6 saat gibi araliklarla guncellenir. Varsayilan olarak kullanilan volume pairlist tir.

**Pairlist filter:** Belirlenen coin listesi uzerinde uygulanan filtrelerdir. Baslicalari:  
\- Min age filter : Coin in piyasada bulundugu minimum gun sayisidir. Default minimum 30 gun  
\- Volatility filter : Coin in son 7 gun icerisindeki standart sapma oranina bakar. Coin fazla hareketli ya da fazla hareketsizse pairlistten cikarir.

**Whitelist:** Botun islem yapmak icin takip ettigi coin listesi

**Blaclist:** Botun asla islem yapmayacagi coin listesidir. Varsayilan olarak BTC, SHIB, tum futbol tokenlari, UP/DOWN token lar ve 5-6 adet shitcoin bulunur.

**Trade limit count:** Botun kullandigi maksimum acik pozisyon sayisidir. Trade limit kadar islem actiktan sonra acilan pozisyonlardan biri satilana kadar bot islem yapmaz. Varsayilan degeri 3.

**Stake amount:** Botun hesaptaki paranin tumunu kullanmasi istenmedigi zaman kullanilir. Stake amount unlimited oldugunda hesaptaki toplam USDT miktari trade limite bolunerek islem basina yatirilacak para hesaplanir. Stake amount rakamsal olarak verildiyse bir islem icin maksimum o tutarda USDT kullanilir. Varsayilan unlimited ve USDT dir.

**Backtesting:** Botun geriye donuk yapilan simulasyonlaridir. Bir stratejiyi gecmis tarihler uzerinde sanki calismis gibi simule etme islemidir. X stratejisi 1 Nisan - 1 Mayis arasinda backtest e sokularak teorik olarak bu donemde ne kadar kar/zarar ettigi, hangi islemleri yaptigi simule edilebilir. Cok gercekci sonuc vermez, o yuzden genellikle stratejileri karsilastirmak icin kullanilir.

**Dry run:** Bir botun hayali para ile calismasidir. Canli bot gibi baslar ve islem yapar fakat herhangi bir Binance hesabina bagli degildir. Stratejileri gercek hayatta denemek icin kullanilir. Live a yakin sonuc verir.

**FreqUI:** Botun browser arayuzudur. Telegramdan ayni bilgiler edilinebilir.

# NFI Strategy

NFI, freqtrade de kullandigimiz bir stratejidir. NFI temel olarak 5m timeframe de calisir fakat alim satim sinyallerine karar verirken 1h indikatorlerden de faydalanir. Ufak oranda scalping, buyuk oranda trending olarak calisir. Cok sayida farkli kondisyona bakarak alim ve satim karari verebilir. Acilan pozisyonlar 5dk ya da gunlerce surebilir, sinir yoktur fakat zaman gectikte strateji beklentiyi dusurur.

NFI stratejileri 5m timeframe ine gore optimize edilmistir. Farkli timeframe lerde denenmemistir ya da daha kotu performans alinmistir.

Yazarinin nicki **iterativ**

# Telegram

Bot ile ilgili islemlerin cogu Telegram uzerinden yapilmaktadir. Telegramda acilan bir grup icerisine bota bagli bir chatbot u bulunur ve bot ile iletisim bu grup icerisinde gerceklesir. Bu Telegram grubu acildiginda mesaj yazilan bolumun saginda, kirmizi isaretli buton ile islem tablosu acilir.

![](https://user-images.githubusercontent.com/18678845/125100529-7fb49c00-e0d9-11eb-9053-7d7f1af8b46f.png)

**profit** : Bugune kadarki kar/zarar durumu  
**whitelist** : Botun o anki whitelist i  
**balance** : Hesaptaki tum coin miktarlari. Cok ufak tutarli coinler not olarak gosterilir. Bunlar Binance uzerinden BNB ye cevrilebilir  
**daily** : Gunluk kar/zarar durumu. Acik olan islemler buradaki hesaba dahil degil  
**count** : Anlik acik ve kullanilan pozisyon sayilari  
**performance** : Simdiye kadar alinip satilmis coinlerin toplam kar zarar oranlari ile listesi  
**\*status table** : Anlik acik pozisyonlar ve bunlarin kar/zarar durumu. En sik kullanilan komuttur  
**reload\_config** : Konfigurasyon yeniden yuklenir, normal kosullarda kullanilmamalidir. Yanlislikla basildiysa bir zarari yok. Konfigurasyon yeniden yuklendikten sonra bot stopped olarak acilir. alimlara devam etmesi icin start yapilmalidir  
**stop** : Botun alim ve satim yapmasini durdurur  
**stopbuy** : Botun alim yapmasini durdurur. Elinde acik pozisyon varsa satislarini yapana kadar devam eder. Botun yeniden alimlara devam etmesi icin reload\_config e basilmalidir.  
**start** : Bot reload\_config sonucu ya da manuel olarak durdurulduysa yeniden baslatmak icin kullanilir.

#### Manuel komutlar

**/forcesell 15** : status table da gorulen acik pozisyonlardan herhangi birini manuel sattirmak icin kullanilir. 15 olarak verilen yere acik pozisyonun tablodaki id si yazilir  
**/forcebuy** : Manuel alim icin kullanilir. Komut girildiginde whitelist listelenir ve buradan secim yapilarak manuel alim yapilir.

Telegramda gosterilen bilgilerin bazilarinin altinda Refresh butonu bulunur. Her seferinde tekrar bu komutlari vermek yerine Refresh butonu kullanilabilir. Mesaj kalabaligini onler

# FAQ

### Bot alim yapmiyor

Alacak duzgun coin bulamamistir. 

### Ayni islemde Bunyamin %30 kar etti, benimki %3 kar hatta -%5 zarar etti

Bot 2-5 saniyelik araliklarla alim satim yapip yapamadigini kontrol eder. 1sn fark ile diger kisi islemi %1 daha ucuza ya da daha pahaliya almis olabilir. Ikiniz farkli noktalardan isleme giris yaptiginiz icin botun algoritmasina gore sattigi noktalar da degisebilir. Bot %5 kar etmeyi bekleyip bir kiside bu kari yakalayip satmis olabilir, oteki kisideki islemin kari %5 e gelmeden geri dusmeye baslamis olabilir, bot da yukselmesi icin bekliyor olabilir, islem yukselmek yerine zarara dogru yonelebilir. Milisaniyelik farklar ya da cok ufak fiyat farklari farkli senaryolar olusturur.

### Bunyamin in botu ETH aldi, benimki neden almadi?

*   Acik pozisyonun olmayabilir
*   ETH senin whitelist inde olmayabilir. Whitelist ler 2-6 saat gibi araliklarla guncellenir, Bunyamin in whitelist i 10dk once guncellenip ETH yi listesine dahil etmis olabilir fakat seninki whitelist i henuz guncellemediyse senin whitelist inde ETH olmayabilir
*   ETH nin fiyati sadece 1sn dusup senin botun bu dusmeyi yakalayamamis olabilir
*   Cok cok nadir olarak botta sorun sebebiyle alim gerceklesmemis olabilir.

### Komisyonlar BNB ile odenir mi?

Evet, Binance de islem ucretlerinin BNB ile odenmesi aciksa ve hesapta BNB varsa kullanilir.
Profit hesaplanirken ve sonuclar verilirken odenen komisyon da hesabin icindedir.

### Yapay zeka, AI, Machine Learning?

Freqtrade de bunlar otomatik olarak yok. ML kullanan baska botlar var ama FreqTrade kadar kar getirdigi gozlenmedi.

### Kaldirac, future, long/short?

Freqtrade de bunlar da yok, sadece spot trading var. Leveraged olarak sadece Binance deki UP/DOWN pairler kullanilabilir. O pairler de tavsiye edilmiyor ve denemeleri basarisiz oldu.

### Minumum/maksimum ne kadar tutarla oynanir?

Binance te minimum islem tutari 15 USDT. Teorik olarak trade limit x 15 USDT ile giris yapilabilir. Komisyonlar ve zarar edildiginde 15 USDT nin altina gecilebilecegi de dusunulurse 100 USDT gibi bir tutarin altinda girmek islevsel degildir. Maksimum sinir bulunmuyor fakat tutarlar yukseldiginde limit emirleri daha zor kapanmaya ve market emirleri daha dezavantajli fiyatlara kapanmaya baslayabilir.

# Kaynaklar

FreqTrade : [https://www.freqtrade.io/en/stable/](https://www.freqtrade.io/en/stable/)

FreqTrade Discord : https://discord.gg/p7nuUNVfP7
