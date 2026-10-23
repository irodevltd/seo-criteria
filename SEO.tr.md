# SEO kriterleri

[English](SEO.md) · **Türkçe**

irodev.net SEO analizinin 99 kontrolü: her birinin neden önemli olduğu, nasıl düzeltileceği ve işe yaradığı yerde bir örnek. Hepsi ölçülebilir ve arama motorlarının kendi belgelerine dayanır; kaynaklar her grubun altında. Sık sayılan ama gerçek bir sıralama kriteri olmayan şeyler [MYTHS.tr.md](MYTHS.tr.md) dosyasında.

Bunları kendi sayfanızda [ücretsiz SEO analiziyle](https://irodev.net/tr/ucretsiz-seo-analizi) çalıştırabilirsiniz. "Site taraması" grubu için sitenin tamamının taranması gerekir.

- [Temeller](#basics) (8)
- [İçerik](#content) (10)
- [Teknik](#tech) (21)
- [Performans](#perf) (11)
- [Güvenlik](#security) (4)
- [Mobil ve erişilebilirlik](#mobile) (7)
- [Sosyal ve şema](#social) (11)
- [Yerel SEO](#local) (6)
- [Core Web Vitals](#vitals) (5)
- [Bağlantılar](#links) (3)
- [Site taraması](#site) (13)

<a name="basics"></a>

## Temeller

Her sayfanın her şeyden önce ihtiyaç duyduğu temel: güvenli adres, başlık ve açıklama, mobil görünüm alanı, dil ve karakter kodlaması.

### HTTPS güvenli bağlantı

*Etki: yüksek · Zorluk: kolay*

Tarayıcılar HTTP sayfaları "Güvenli değil" diye işaretler; Google HTTPS'i sıralama sinyali olarak kullanır. HTTP üzerindeki formlar, ziyaretçinin yazdıklarını açıkta taşır.

**Nasıl düzeltilir**

1. Hosting panelinizden ücretsiz bir sertifika (Let's Encrypt) kurun.
2. Tüm http:// adreslerini 301 ile https:// adresine yönlendirin.
3. İç bağlantıları, canonical etiketlerini ve site haritasını https olarak güncelleyin.

```text
# .htaccess
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

### Geçerli SSL sertifikası

*Etki: yüksek · Zorluk: kolay*

Süresi dolmuş ya da alan adıyla eşleşmeyen bir sertifika, ziyaretçi sayfayı görmeden tam sayfa bir tarayıcı uyarısı çıkarır; çoğu siteden çıkar.

**Nasıl düzeltilir**

1. Sertifikayı yenileyin; hem alanadi.com hem www.alanadi.com adresini kapsadığından emin olun.
2. Yalnızca site sertifikasını değil, ara sertifikalar dahil tam zinciri kurun.
3. Bir daha süresi dolmaması için otomatik yenilemeyi açın.

### Sayfa başlığı (title)

*Etki: yüksek · Zorluk: kolay*

Başlık, arama sonuçlarındaki mavi satırdır ve insanların ilk okuduğu şeydir. Ana hizmetinizi içeren net bir başlık hem sıralamayı hem tıklamayı artırır.

**Nasıl düzeltilir**

1. Kesilmemesi için 30–65 karakter arasında tutun.
2. Önce ana anahtar kelimeyi, sonra markanızı yazın: "Hizmet Şehir | Marka".
3. Her sayfaya kendine özgü bir başlık verin; tekrar etmeyin.

```html
<title>Corporate Web Design in Ankara | Ardena</title>
```

### Meta açıklama

*Etki: orta · Zorluk: kolay*

Açıklama, arama sonuçlarında başlığın altındaki gri metindir. Sıralamayı doğrudan etkilemez ama insanların tıklayıp tıklamayacağını belirler.

**Nasıl düzeltilir**

1. "Neden bu sayfa?" sorusunu yanıtlayan 70–165 karakterlik bir metin yazın.
2. Hizmeti, faydayı ve bir harekete geçirici ifadeyi ekleyin.
3. Her önemli sayfa için ayrı bir açıklama yazın.

```html
<meta name="description" content="Fast, mobile-first corporate websites with a fixed quote. Get a proposal within one business day.">
```

### Mobil uyum (viewport)

*Etki: yüksek · Zorluk: kolay*

Google sitenizin mobil sürümünü sıralar. Viewport etiketi yoksa telefonlar sayfayı küçültülmüş masaüstü görünümüyle açar.

**Nasıl düzeltilir**

1. <head> içine viewport etiketini ekleyin.
2. Sayfayı gerçek bir telefonda kontrol edin: metin yakınlaştırmadan okunmalı.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

### Dil tanımı (lang)

*Etki: düşük · Zorluk: kolay*

Ekran okuyucular telaffuzu lang özniteliğinden seçer; tarayıcılar çeviri ve heceleme için kullanır (WCAG 3.1.1), Bing de okur. Google ise dili görünür metinden belirler.

**Nasıl düzeltilir**

1. <html> etiketine ekleyin: Türkçe için tr, İngilizce için en.

```html
<html lang="tr">
```

### Karakter kodlaması

*Etki: düşük · Zorluk: kolay*

Kodlama tanımlı değilse ş, ğ, İ gibi Türkçe karakterler bazı tarayıcılarda ve arama sonuçlarında bozuk görünebilir.

**Nasıl düzeltilir**

1. <head> içindeki ilk etiket olarak UTF-8 tanımlayın.

```html
<meta charset="utf-8">
```

### Favicon

*Etki: düşük · Zorluk: kolay*

Google mobil sonuçlarda sitenizin yanında favicon gösterir; tarayıcılar sekmede ve yer imlerinde kullanır. Eksik ikon, sitenin yarım kaldığı izlenimini verir.

**Nasıl düzeltilir**

1. Kare bir ikon ekleyin (en az 48×48 px; SVG ya da PNG).
2. iPhone'lar için apple-touch-icon (180×180) ekleyin.

```html
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

**Kaynaklar:** [Title links](https://developers.google.com/search/docs/appearance/title-link) · [Snippets and meta descriptions](https://developers.google.com/search/docs/appearance/snippet) · [Mobile-first indexing](https://developers.google.com/search/docs/crawling-indexing/mobile/mobile-sites-mobile-first-indexing) · [Favicons in Search](https://developers.google.com/search/docs/appearance/favicon-in-search) · [Page experience](https://developers.google.com/search/docs/appearance/page-experience)

<a name="content"></a>

## İçerik

Görünen içerik: insanlara ve arama motorlarına sayfanın ne hakkında olduğunu anlatan başlıklar, metin, görseller ve bağlantılar.

### Ana başlık (H1)

*Etki: orta · Zorluk: kolay*

H1, ziyaretçinin ilk gördüğü başlıktır; Google da sonucunuzun başlık bağlantısını yazarken onu kullanabilir. Birden fazla H1 Google için sorun değildir; hiç olmaması ise sayfayı net bir ana başlıktan yoksun bırakır.

**Nasıl düzeltilir**

1. Sayfaya, ana konuyu içeren net bir <h1> ana başlık verin.
2. Temanız yalnızca logoyu <h1> içine alıyorsa gerçek bir ana başlık da ekleyin.

```html
<h1>Corporate websites that bring in customers</h1>
```

### Başlık yapısı

*Etki: düşük · Zorluk: kolay*

Alt başlıklar uzun metni, ziyaretçilerin göz atabileceği ve ekran okuyucuların aralarında gezinebileceği bölümlere ayırır. Google başlık sırasının sıralamada önemli olmadığını söyler; ama tek bir alt başlığı olmayan uzun bir sayfa zor okunur.

**Nasıl düzeltilir**

1. Her ana bölüme <h2>, alt maddelerine <h3> verin.
2. Seviye atlamayın (<h1>'den hemen sonra <h4> gibi): ekran okuyucu kullananlar bunlarla gezinir.
3. Başlıkları metni büyütmek için değil, yapı için kullanın.

### Metin içeriği

*Etki: orta · Zorluk: orta*

Google'ın bir asgari kelime sayısı yoktur; ama sayfanın ne sunduğunu anlatacak ve arayanın sorusunu yanıtlayacak kadar metni olmalıdır. Neredeyse hiç metin yoksa arama motorlarının ve yapay zekâ asistanlarının anlayıp alıntılayacağı bir şey kalmaz.

**Nasıl düzeltilir**

1. Sayfanın ne sunduğunu, kime sunduğunu ve neden sizi seçmeleri gerektiğini açıkça yazın.
2. Müşterilerin satın almadan önce sorduklarını yanıtlayın: fiyat, süreç, süre, garanti.
3. Kelime sayısı için değil, okuyucu için yazın.

### Görsel alt metinleri

*Etki: orta · Zorluk: kolay*

Alt metin bir görseli Google Görseller'e, ekran okuyuculara ve yapay zekâ modellerine anlatır. Aynı zamanda erişilebilirlik gereğidir.

**Nasıl düzeltilir**

1. Anlam taşıyan her görsele kısa ve somut bir alt metin ekleyin.
2. Yalnızca dekoratif görsellerde alt="" kullanın; ekran okuyucular atlar.
3. Görselin içeriğini anlatın; anahtar kelime doldurmayın.

```html
<img src="team.webp" alt="Our design team reviewing a homepage layout" width="1200" height="800">
```

### Ana konu başlıkta

*Etki: düşük · Zorluk: kolay*

Bir sayfanın en çok kullandığı kelimeler genellikle onun konusudur. Hiçbiri başlıkta yoksa başlık sayfayı anlatmıyor olabilir; Google da başlığı yeniden yazabilir ya da sayfayı başka aramalarda gösterebilir.

**Nasıl düzeltilir**

1. Aşağıdaki kelime tablosuna bakın ve müşterilerin aradığı terimi seçin.
2. Bu terimi doğal bir ifadeyle başlığa ve H1'e yerleştirin.

### İç bağlantılar

*Etki: orta · Zorluk: kolay*

Kendi sayfalarınıza verilen bağlantılar ziyaretçinin sitede ilerlemesini, arama motorlarının diğer sayfalarınızı bulup değerlendirmesini sağlar.

**Nasıl düzeltilir**

1. Metin içinden ilgili hizmetlere, örnek çalışmalara ve iletişim sayfasına bağlantı verin.
2. "Tıklayın" yerine açıklayıcı bağlantı metni kullanın ("kurumsal web tasarımı").

### Okunabilirlik

*Etki: düşük · Zorluk: orta*

Google okunabilirlik puanı kullanmaz; ama ziyaretçiler göz gezdirir: uzun cümleler ve ağır kelimeler onları teklifinize ulaşmadan kaybettirir, sade metni de yapay zekâ asistanları daha doğru alıntılar.

**Nasıl düzeltilir**

1. Cümlelerin çoğunu 20 kelimenin altında tutun; uzun cümleleri ikiye bölün.
2. Jargon yerine gündelik kelimeleri tercih edin; teknik bir terimi ilk kullandığınızda açıklayın.
3. Kısa paragraflar (2–4 cümle), ara başlıklar ve listeler kullanın.

### Başlık ve H1 uyumu

*Etki: düşük · Zorluk: kolay*

Başlık (title) arayanın tıkladığı şeydir; H1 ise sayfaya geldiğinde gördüğü. İkisi farklı şeylerden söz ederse insanlar yanıltıldığını hisseder; Google da başlığınızın yerine H1'i ya da sayfadan başka bir metni gösterebilir.

**Nasıl düzeltilir**

1. H1'in, title'daki ana konuyu tekrar etmesini sağlayın; birebir aynı olması gerekmez.
2. Ana anahtar kelimenizi ikisinde de kullanın.

```html
<title>Corporate Web Design in Ankara | Ardena</title>
<h1>Corporate web design for Ankara businesses</h1>
```

### Açıklayıcı bağlantı metni

*Etki: düşük · Zorluk: kolay*

Bağlantı metni, ziyaretçiye ve arama motoruna bağlantının arkasında ne olduğunu söyler. "Tıklayın" ya da "devamı" hiçbir şey anlatmaz; bağlantıdan bağlantıya geçen ekran okuyucu kullanıcıları aynı ifadelerden oluşan bir liste duyar.

**Nasıl düzeltilir**

1. Genel ifadeleri okuyucunun ne bulacağıyla değiştirin: "Buraya tıklayın" yerine "E-ticaret fiyatlarını görün".
2. Bağlantı metnini kısa (2–6 kelime) ve her hedef için farklı tutun.

```html
<!-- before -->
<a href="/services">Click here</a>
<!-- after -->
<a href="/services">See all our services</a>
```

### Açıklayıcı görsel dosya adları

*Etki: düşük · Zorluk: kolay*

Dosya adı, arama motorunun bir görsel hakkında sahip olduğu az sayıdaki ipucundan biridir. IMG_4821.jpg hiçbir şey anlatmaz; kirmizi-seramik-vazo.jpg görselin görsel aramalarında çıkmasına yardım eder.

**Nasıl düzeltilir**

1. Görselleri yüklemeden önce yeniden adlandırın: tire ile ayrılmış küçük harfli kelimeler.
2. Görselde ne olduğunu, uygun düşüyorsa anahtar kelimenizle birlikte yazın.
3. Dosya adlarında boşluk ve Türkçe karakter kullanmayın (ç, ş, ğ yerine c, s, g).

```text
IMG_4821.jpg   ->  red-ceramic-vase.jpg
DSC00093.png   ->  ankara-office-entrance.png
```

**Kaynaklar:** [SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide) · [Creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) · [Image SEO](https://developers.google.com/search/docs/appearance/google-images) · [Crawlable links](https://developers.google.com/search/docs/crawling-indexing/links-crawlable)

<a name="tech"></a>

## Teknik

Arama motorlarının sayfayı alıp dizine ekleyebilmesi ve anlayabilmesi: durum kodları, yönlendirmeler, canonical, robots kuralları, site haritası, sıkıştırma ve sunucu hızı.

### HTTP durum kodu

*Etki: yüksek · Zorluk: orta*

Yalnızca 2xx kodu dönen sayfalar dizine eklenir. Hatalar (4xx/5xx) sayfayı aramadan düşürür ve ziyaretçi kaybettirir.

**Nasıl düzeltilir**

1. Sunucunun neden bu durum kodunu döndüğünü bulun: kaldırılmış sayfa, sunucu hatası ya da güvenlik duvarı.
2. Sayfayı geri getirin ya da en yakın çalışan sayfaya 301 ile yönlendirin.

### Yönlendirme zinciri

*Etki: orta · Zorluk: kolay*

Her ek yönlendirme, sayfa yüklenmeye başlamadan önce bir tur daha ekler; Google da bir zinciri on adımdan sonra takip etmeyi bırakır.

**Nasıl düzeltilir**

1. Eski adresleri tek bir 301 ile doğrudan son adrese yönlendirin.
2. Bağlantılarda, reklamlarda ve site haritasında son adresi (https, www'li ya da www'siz) kullanın.

### İndekslenebilir

*Etki: yüksek · Zorluk: kolay*

noindex talimatı Google'a sayfayı hiç göstermemesini söyler. Çoğu zaman site yayına alındıktan sonra unutulur.

**Nasıl düzeltilir**

1. robots meta etiketindeki (ve X-Robots-Tag başlığındaki) "noindex" ifadesini kaldırın.
2. WordPress'te Ayarlar › Okuma altındaki "Arama motorlarını engelle" seçeneğini kaldırın.

```html
<meta name="robots" content="index, follow">
```

### Canonical etiketi

*Etki: orta · Zorluk: kolay*

Aynı sayfaya çoğu zaman birden fazla adresle ulaşılır (parametreli, www'li ya da www'siz). Canonical etiketi sıralanması gereken adresi belirtir.

**Nasıl düzeltilir**

1. Sayfanın temiz ve son adresiyle bir canonical bağlantısı ekleyin.
2. Gerçekten başka bir sayfanın kopyası değilse sayfanın kendisini gösterin.

```html
<link rel="canonical" href="https://example.com/services/web-design">
```

### robots.txt erişilebilirliği

*Etki: yüksek · Zorluk: kolay*

Google taramadan önce robots.txt dosyasını okur. Dosyanın olmaması (404) sorun değildir: her şey taranabilir. Ama robots.txt sunucu hatası verir ya da zaman aşımına uğrarsa Google, dosyayı yeniden okuyabilene kadar tüm siteyi taramayı durdurur.

**Nasıl düzeltilir**

1. /robots.txt adresinin metin dosyasıyla 200 ya da dosyaya ihtiyacınız yoksa düz bir 404 döndürmesini sağlayın.
2. Hata veriyorsa önündeki güvenlik duvarı, CDN ya da güvenlik eklentisi kurallarını kontrol edin.

```text
User-agent: *
Allow: /
Disallow: /admin/

Sitemap: https://example.com/sitemap.xml
```

### XML site haritası

*Etki: orta · Zorluk: kolay*

Site haritası dizine eklenmesini istediğiniz tüm sayfaları listeler; yeni ve derindeki sayfalar daha hızlı bulunur.

**Nasıl düzeltilir**

1. /sitemap.xml oluşturun (çoğu CMS ve SEO eklentisi bunu otomatik yapar).
2. robots.txt içinde belirtin ve Google Search Console'a gönderin.

```html
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://example.com/</loc></url>
</urlset>
```

### Sıkıştırma (gzip / Brotli)

*Etki: orta · Zorluk: kolay*

Sıkıştırma HTML, CSS ve JavaScript boyutunu %60–80 küçültür; sayfalar özellikle mobil veride daha hızlı gelir.

**Nasıl düzeltilir**

1. Sunucuda ya da CDN'de Brotli veya gzip'i açın (çoğu zaman hosting panelinde tek bir ayardır).

```text
# .htaccess (Apache)
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/css application/javascript
</IfModule>
```

### Sunucu yanıt süresi

*Etki: yüksek · Zorluk: orta*

Sunucu yanıt vermeden ekranda hiçbir şey görünmez. Geç gelen ilk bayt, diğer tüm hız ölçümlerini ve Core Web Vitals değerlerini geciktirir.

**Nasıl düzeltilir**

1. Sayfa önbelleğini (ya da bir CDN) açın; sayfalar her ziyarette yeniden üretilmesin.
2. Yavaş eklentileri ve veritabanı sorgularını temizleyin; PHP'yi güncel sürüme yükseltin.
3. Ziyaretçilerinize yakın bir sunucu seçin (Türkiye ve İngiltere için Avrupa).

### HTML boyutu

*Etki: düşük · Zorluk: orta*

Ağır bir HTML belgesi (gömülü görseller, devasa menüler, sayfa oluşturucular) telefonlarda işlenmeyi yavaşlatır.

**Nasıl düzeltilir**

1. Gömülü görselleri ve betikleri önbelleğe alınan ayrı dosyalara taşıyın.
2. Kullanılmayan sayfa oluşturucu bölümlerini ve tekrar eden menüleri kaldırın.

### Görsellerde geç yükleme

*Etki: düşük · Zorluk: kolay*

Görseli bol bir sayfada ilk ekranın altındaki görsellerin ziyaretçi kaydırmadan yüklenmesi gerekmez. Bunları sonradan yüklemek ilk görünümü hızlandırır; ana görsel yine de önce yüklenmelidir.

**Nasıl düzeltilir**

1. İlk ekranın altındaki görsellere loading="lazy" ekleyin.
2. Ana (hero) görselde kullanmayın; o ilk yüklenmeli.

```html
<img src="gallery-3.webp" alt="…" loading="lazy" width="800" height="600">
```

### Görsel boyut bilgisi

*Etki: orta · Zorluk: kolay*

Genişlik ve yükseklik verilmezse tarayıcı yer ayıramaz; görseller yüklenirken sayfa kayar (Core Web Vitals ölçütü olan düzen kayması).

**Nasıl düzeltilir**

1. Görselin gerçek oranlarıyla width ve height öznitelikleri ekleyin.
2. Ölçeklenmesi için CSS'te width:100%; height:auto bırakın.

```html
<img src="hero.webp" alt="…" width="1600" height="900">
```

### HTTP'den HTTPS'e yönlendirme

*Etki: yüksek · Zorluk: kolay*

Ziyaretçiler ve eski bağlantılar hâlâ http:// adresine gelir. Kalıcı bir yönlendirme yoksa bu sürüm, sitenizin ayrı ve güvensiz bir kopyası olarak açık kalır ve sıralama sinyallerini böler.

**Nasıl düzeltilir**

1. Her http:// adresini 301 (ya da 308) ile aynı https:// adresine yönlendirin.
2. Araya ek adımlar koymadan, tek adımda yapın.
3. 302'yi yalnızca geçici taşımalar için kullanın.

```text
# .htaccess (Apache)
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

### www'li ve www'siz adres

*Etki: orta · Zorluk: kolay*

alanadi.com ile www.alanadi.com, Google için iki ayrı adrestir. İkisi de siteyi gösterirse bağlantılar ve sıralama iki kopya arasında bölünür.

**Nasıl düzeltilir**

1. Bir sürümü seçin, diğerini ona 301 ile yönlendirin.
2. Sertifikanın iki adı da kapsadığından emin olun.
3. Seçtiğiniz sürümü canonical etiketlerinde, site haritasında ve iç bağlantılarda kullanın.

```text
# .htaccess: www.example.com -> example.com
RewriteEngine On
RewriteCond %{HTTP_HOST} ^www\.(.+)$ [NC]
RewriteRule ^ https://%1%{REQUEST_URI} [L,R=301]
```

### Olmayan sayfalar için gerçek 404

*Etki: orta · Zorluk: kolay*

Olmayan bir sayfa "200 OK" yanıtı verdiğinde arama motorları boş ya da kopya sayfaları dizine ekler (soft 404) ve tarama süresini boşa harcar; ziyaretçi de net bir mesaj almaz.

**Nasıl düzeltilir**

1. Bilinmeyen adresler için 404 (kaldırılan içerik için 410) döndürün.
2. Arama ve bağlantılar içeren yardımcı bir 404 sayfası gösterin; ama 404 durum kodunu koruyun.
3. Olmayan her adresi ana sayfaya yönlendirmeyin.

```text
# .htaccess
ErrorDocument 404 /404.php

<?php // 404.php: keep the status code
http_response_code(404);
```

### Temiz URL yapısı

*Etki: düşük · Zorluk: orta*

Kısa, okunur, küçük harfli adresler daha kolay paylaşılır ve güven verir. Google adresteki kelimelerin sıralamada çok az önemi olduğunu söyler; ama oturum kimlikleri, büyük/küçük harf karışıklığı ve çok sayıda parametre aynı sayfa için yinelenen adresler üretir.

**Nasıl düzeltilir**

1. Tire ile ayrılmış küçük harfli kelimeler kullanın: /hizmetler/web-tasarimi.
2. Dizine eklenmesini istediğiniz bağlantılarda oturum kimliği ve uzun parametre listesi kullanmayın.
3. Bir adresi değiştirdiğinizde eskisini 301 ile yönlendirin.

### Site haritası içeriği

*Etki: orta · Zorluk: kolay*

Site haritası, ancak arama motorları onu okuyabiliyor ve gerçek, güncel sayfalarınızı listeliyorsa işe yarar. Hatalar ya da başka sitelere ait adresler, Google'ın haritanın bir kısmını yok saymasına neden olur.

**Nasıl düzeltilir**

1. XML'i doğrulayın: her sayfa için bir <url><loc>, mutlak https adresleri.
2. <lastmod>'u yalnızca doğru olduğunda ekleyin: Google bu tarihi tutarlı biçimde doğruysa kullanır.
3. Yalnızca bu sitenin dizine eklenebilir sayfalarını listeleyin ve haritayı Search Console'a gönderin.

```html
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/services</loc>
    <lastmod>2026-10-01</lastmod>
  </url>
</urlset>
```

### robots.txt kuralları

*Etki: yüksek · Zorluk: kolay*

robots.txt'deki tek bir yanlış satır tüm siteyi Google'dan gizleyebilir ya da sayfaları ziyaretçinin gördüğü gibi görmesi için gereken CSS ve JavaScript dosyalarına erişmesini engelleyebilir.

**Nasıl düzeltilir**

1. Yayındaki bir sitede asla "Disallow: /" bırakmayın.
2. Tema, CSS ya da JavaScript klasörlerini engellemeyin.
3. Tam site haritası adresiyle bir Sitemap: satırı ekleyin.

```text
User-agent: *
Disallow: /admin/
Allow: /

Sitemap: https://example.com/sitemap.xml
```

### Dil alternatifleri (hreflang)

*Etki: orta · Zorluk: kolay*

hreflang, Google'a hangi dil sürümünü kime göstereceğini söyler. Geçersiz kodlar, eksik öz-referans ya da tekrarlar tüm setin yok sayılmasına ve yanlış dilin sıralanmasına neden olabilir.

**Nasıl düzeltilir**

1. tr, en ya da en-GB gibi ISO kodları ve varsayılan için x-default kullanın.
2. Her dil sürümü, kendisi dahil tüm sürümleri listelemeli.
3. Mutlak adresler ve her dil kodu için tek kayıt kullanın.

```html
<link rel="alternate" hreflang="tr" href="https://example.com/tr/">
<link rel="alternate" hreflang="en" href="https://example.com/">
<link rel="alternate" hreflang="x-default" href="https://example.com/">
```

### Meta refresh yönlendirmesi

*Etki: düşük · Zorluk: kolay*

Meta refresh sayfayı bir gecikmeyle yeniler ya da başka adrese gönderir: ziyaretçi yerini kaybeder, geri düğmesi bozulur. Google bunun yerine sunucu taraflı 301 önerir ve gecikmeli yenilemeyi yalnızca geçici yönlendirme sayar.

**Nasıl düzeltilir**

1. Sunucu tarafında bir 301 yönlendirmesiyle değiştirin.
2. Kendini güncelleyen içerikte sayfayı yeniden yüklemek yerine veriyi JavaScript ile yenileyin.

```html
<!-- remove this -->
<meta http-equiv="refresh" content="0; url=/new-page">
```

### Canonical ayrıntıları

*Etki: orta · Zorluk: kolay*

Başka bir sayfayı gösteren canonical, Google'a bu sayfa yerine o sayfayı dizine eklemesini söyler. İki canonical etiketi ya da göreli bir adres, Google'ın etiketi yok saymasına yol açabilir.

**Nasıl düzeltilir**

1. Her sayfada tam olarak bir canonical etiketi kullanın.
2. Bu sayfanın mutlak ve tercih edilen adresini kullanın (https, seçtiğiniz alan adı).
3. Yalnızca yazdırma sürümü ya da filtre sayfası gibi gerçek kopyalarda başka bir sayfayı gösterin.

```html
<link rel="canonical" href="https://example.com/services/web-design">
```

### JavaScript olmadan içerik

*Etki: yüksek · Zorluk: zor*

Google JavaScript'i sonradan ve her zaman eksiksiz olmayan biçimde çalıştırır; birçok yapay zekâ tarayıcısı ise hiç çalıştırmaz. HTML, scriptler çalışana kadar neredeyse boşsa içeriğiniz hiç okunmayabilir.

**Nasıl düzeltilir**

1. Ana içeriği sunucuda oluşturun (SSR) ya da derleme sırasında önceden üretin.
2. En azından başlığı, giriş metnini ve önemli bağlantıları HTML'e koyun.
3. "Sayfa kaynağını görüntüle" ile kontrol edin: tarayıcıların ilk aldığı şey odur.

**Kaynaklar:** [HTTP status codes and network errors](https://developers.google.com/search/docs/crawling-indexing/http-network-errors) · [Redirects](https://developers.google.com/search/docs/crawling-indexing/301-redirects) · [Canonical URLs](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls) · [robots.txt](https://developers.google.com/search/docs/crawling-indexing/robots/intro) · [Blocking indexing with noindex](https://developers.google.com/search/docs/crawling-indexing/block-indexing) · [Building a sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap) · [Localized versions (hreflang)](https://developers.google.com/search/docs/specialty/international/localized-versions) · [JavaScript SEO basics](https://developers.google.com/search/docs/crawling-indexing/javascript/javascript-seo-basics)

<a name="perf"></a>

## Performans

Bir sayfanın gerçek ziyaretçiler için hızlı açılmasını sağlayanlar.

### HTTP/2 veya HTTP/3

*Etki: orta · Zorluk: kolay*

HTTP/2 ve HTTP/3 birçok dosyayı tek bağlantı üzerinden aynı anda yükler; HTTP/1.1 ise onları sıraya koyar ve çok görselli, çok scriptli sayfaları yavaşlatır.

**Nasıl düzeltilir**

1. Hosting panelinizde ya da CDN'de HTTP/2'yi (sunuluyorsa HTTP/3'ü de) açın.
2. HTTP/2 için HTTPS gerekir; çoğu hosting sertifikayla birlikte açar.
3. Cloudflare gibi bir CDN bunu sunucuda değişiklik yapmadan sağlar.

### Dosya sayısı

*Etki: orta · Zorluk: orta*

Her stil dosyası, script ve görsel ayrı bir indirmedir. Onlarca dosya, özellikle mobil ağlarda ilk görüntülemeyi yavaşlatır.

**Nasıl düzeltilir**

1. Kullanmadığınız eklenti CSS ve JavaScript dosyalarını birleştirin ya da kaldırın.
2. Ekranın altında kalan görselleri tembel yükleyin (lazy-load).
3. İkon görsellerini tek bir SVG sprite ile değiştirin.

### Görüntülemeyi engelleyen kaynaklar

*Etki: yüksek · Zorluk: orta*

Tarayıcı, <head> içindeki her stil dosyası ve eşzamanlı script inene kadar hiçbir şey göstermez. Her biri ilk görüntülemeyi geciktirir.

**Nasıl düzeltilir**

1. <head> içindeki scriptlere defer ekleyin ya da onları <body> sonuna taşıyın.
2. Küçük stil dosyalarını birleştirin; sayfanın üst kısmı için kritik CSS'i satır içine alın.
3. Kritik olmayan CSS'i (yazdırma stilleri, alt bölümler) engellemeden yükleyin.

```html
<script src="/js/app.js" defer></script>
<link rel="stylesheet" href="/css/print.css" media="print">
```

### Tarayıcı önbelleği

*Etki: orta · Zorluk: kolay*

Uzun önbellek süreleriyle geri gelen ziyaretçiler CSS, JavaScript ve görselleri yeniden indirmek yerine kendi cihazından yükler.

**Nasıl düzeltilir**

1. Statik dosyalar için Cache-Control: max-age=31536000 gönderin.
2. Güncellemelerin yine de ulaşması için dosya adlarına sürüm ya da hash ekleyin (app.3f9a.css).
3. HTML'i kısa, varlık dosyalarını uzun süre önbelleğe alın.

```text
# .htaccess (Apache, mod_expires)
<IfModule mod_expires.c>
  ExpiresActive On
  ExpiresByType text/css "access plus 1 year"
  ExpiresByType application/javascript "access plus 1 year"
  ExpiresByType image/webp "access plus 1 year"
  ExpiresByType image/jpeg "access plus 1 year"
  ExpiresByType image/png "access plus 1 year"
</IfModule>
```

### Sıkıştırılmış CSS ve JavaScript

*Etki: orta · Zorluk: kolay*

Metin dosyaları gzip ya da Brotli ile %70–80 küçülür. Sıkıştırmadan sunmak bant genişliğini boşa harcar ve her sayfa görüntülemeyi yavaşlatır.

**Nasıl düzeltilir**

1. Sunucuda ya da CDN'de CSS ve JavaScript için Brotli veya gzip'i açın.
2. Üçüncü taraf dosyalarını da kontrol edin; sunucuları sıkıştırmıyorsa kendiniz barındırın.

```text
# .htaccess (Apache, mod_deflate)
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/css application/javascript application/json image/svg+xml
</IfModule>
```

### Modern görsel formatları

*Etki: orta · Zorluk: kolay*

WebP ve AVIF, aynı kalitede JPEG ve PNG'den genellikle %25–50 daha küçüktür; görsel ağırlıklı sayfaları hızlandırır.

**Nasıl düzeltilir**

1. Fotoğrafları yüklerken WebP'ye (ya da AVIF'e) çevirin veya bunu CMS'inize ya da CDN'inize bırakın.
2. Çok eski tarayıcıları desteklemeniz gerekiyorsa JPEG yedekli <picture> kullanın.

```html
<picture>
  <source srcset="vase.avif" type="image/avif">
  <source srcset="vase.webp" type="image/webp">
  <img src="vase.jpg" width="800" height="600" alt="Handmade red ceramic vase">
</picture>
```

### Görsel dosya boyutları

*Etki: yüksek · Zorluk: kolay*

Tek bir 2 MB'lık fotoğraf, sayfanın geri kalanından daha uzun sürede yüklenebilir. Büyük görseller, yavaş Largest Contentful Paint'in en yaygın nedenidir.

**Nasıl düzeltilir**

1. Görselleri gösterildikleri boyuta küçültün (nadiren 1600 px'ten geniş).
2. Sıkıştırın: kalite 75–85'teki WebP aynı görünür ve çok daha küçüktür.
3. srcset ile telefonlara daha küçük sürümler sunun.

```html
<img src="hero-1200.webp"
     srcset="hero-800.webp 800w, hero-1200.webp 1200w, hero-1600.webp 1600w"
     sizes="(max-width: 800px) 100vw, 1200px"
     width="1200" height="600" alt="…">
```

### Web fontu yükleme

*Etki: düşük · Zorluk: kolay*

font-display: swap olmadan metin web fontu inene kadar görünmez kalır; yavaş bağlantıda ziyaretçi boş bir sayfaya bakar.

**Nasıl düzeltilir**

1. Her @font-face kuralına font-display: swap ekleyin.
2. Google Fonts için adresteki &display=swap parametresini koruyun.
3. Sayfanın üstünde kullanılan bir iki fontu kendiniz barındırın ve önceden yükleyin (preload).

```text
@font-face {
  font-family: "Brand";
  src: url("/fonts/brand.woff2") format("woff2");
  font-display: swap;
}
```

### Sayfa karmaşıklığı (DOM boyutu)

*Etki: orta · Zorluk: zor*

Binlerce HTML öğesi tarayıcının her kaydırma ve dokunuşta daha çok çalışmasına neden olur; orta seviye telefonlarda etkileşimi (INP) yavaşlatır.

**Nasıl düzeltilir**

1. Sayfa oluşturucu düzenlerini sadeleştirin, iç içe gereksiz kapsayıcıları kaldırın.
2. Uzun listeleri sayfalandırın; mega menüleri ancak açıldıklarında oluşturun.
3. Sekme ve açılır pencere içeriklerini baştan göndermek yerine gerektiğinde oluşturun.

### Üçüncü taraf scriptler

*Etki: orta · Zorluk: orta*

Her harici widget, izleme kodu ve font sunucusu DNS sorgusu ve sizin kontrol etmediğiniz kod ekler. Birlikte çoğu zaman yavaş, takılan sayfalara ve gizlilik sorularına yol açarlar.

**Nasıl düzeltilir**

1. Her birinin ne yaptığını listeleyin; kimsenin kullanmadıklarını kaldırın.
2. Sohbet widget'larını ve haritaları ancak ziyaretçi istediğinde yükleyin.
3. Fontları ve küçük kütüphaneleri kendiniz barındırın.

### Küçültülmüş (minify) CSS ve JavaScript

*Etki: düşük · Zorluk: kolay*

Boşluklar, yorumlar ve uzun adlar kod yazarken işe yarar; yayında ise yalnızca bayt ekler.

**Nasıl düzeltilir**

1. Derleme aracınızda, CMS önbellek eklentinizde ya da CDN'de küçültmeyi açın.
2. Kütüphanelerin .min sürümlerini kullanın.

**Kaynaklar:** [Core Web Vitals](https://developers.google.com/search/docs/appearance/core-web-vitals) · [Web Vitals (web.dev)](https://web.dev/articles/vitals) · [Lazy loading and LCP (web.dev)](https://web.dev/articles/lcp-lazy-loading)

<a name="security"></a>

## Güvenlik

Ziyaretçiyi koruyan ve tarayıcı uyarılarını önleyenler.

### HSTS (Strict-Transport-Security)

*Etki: düşük · Zorluk: kolay*

HSTS, tarayıcıların sitenizde her zaman HTTPS kullanmasını sağlar; böylece kimse halka açık bir Wi-Fi'de güvensiz http:// bağlantısına itilemez. Ziyaretçiyi korur; tek başına bir sıralama faktörü değildir.

**Nasıl düzeltilir**

1. HTTPS her yerde çalıştıktan sonra Strict-Transport-Security: max-age=31536000 gönderin.
2. includeSubDomains'i ancak tüm alt alan adlarında HTTPS varsa ekleyin.

```text
# .htaccess (Apache, mod_headers)
Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
```

### Güvenlik başlıkları

*Etki: düşük · Zorluk: orta*

Dört yanıt başlığı ziyaretçilerinize yönelik yaygın saldırıları engeller: Content-Security-Policy hangi scriptlerin çalışabileceğini sınırlar, nosniff dosya türü tahminini durdurur, çerçeve koruması tıklama korsanlığını (clickjacking) önler, referrer politikası adres ayrıntılarını gizli tutar. Sıralama faktörü değildirler; ama saldırıya uğrayan bir site Google sonuçlarında uyarıyla gösterilir ve trafiğini kaybeder.

**Nasıl düzeltilir**

1. Eksik başlıkları sunucu ya da CDN ayarlarınıza ekleyin; CSP'ye report-only modunda başlayın.
2. Yanıt başlıklarını tarayıcınızın geliştirici araçlarında kontrol edin (Network sekmesi).

```text
# .htaccess (Apache, mod_headers)
Header always set X-Content-Type-Options "nosniff"
Header always set X-Frame-Options "SAMEORIGIN"
Header always set Referrer-Policy "strict-origin-when-cross-origin"
Header always set Content-Security-Policy-Report-Only "default-src 'self'"
```

### Karışık içerik (mixed content)

*Etki: yüksek · Zorluk: kolay*

Dosyaları http:// üzerinden yükleyen bir HTTPS sayfası tam güvenli değildir. Tarayıcılar güvensiz script ve çerçeveleri engeller (sayfa bozulur), güvensiz görselleri de işaretler.

**Nasıl düzeltilir**

1. Her http:// kaynak bağlantısını https:// ya da göreli bir yol olarak değiştirin.
2. HTTPS'e geçtikten sonra veritabanındaki içerikte http:// bağlantılarını arayın.
3. Güvenlik ağı olarak CSP'nize upgrade-insecure-requests ekleyin.

```text
Header always set Content-Security-Policy "upgrade-insecure-requests"
```

### Sertifika süresi

*Etki: yüksek · Zorluk: kolay*

Sertifikanın süresi dolduğunda her ziyaretçi tam sayfa bir güvenlik uyarısı görür ve çoğu siteden çıkar.

**Nasıl düzeltilir**

1. Otomatik yenilemeyi açın (Let's Encrypt 60–90 günde bir yenilenir).
2. Ücretli sertifika için bitişten iki hafta önceye bir hatırlatma kurun.

**Kaynaklar:** [Page experience](https://developers.google.com/search/docs/appearance/page-experience)

<a name="mobile"></a>

## Mobil ve erişilebilirlik

Mobil kullanım ve erişilebilirlik: sayfayı telefonda ve yardımcı teknolojilerle kullanılabilir kılanlar.

### Yakınlaştırma izni

*Etki: orta · Zorluk: kolay*

Parmakla yakınlaştırmayı engellemek (user-scalable=no, maximum-scale=1) görme güçlüğü olan kişileri dışarıda bırakır ve WCAG erişilebilirlik ölçütlerine aykırıdır.

**Nasıl düzeltilir**

1. Viewport etiketinden user-scalable=no ve maximum-scale değerlerini kaldırın.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

### Form alanı etiketleri

*Etki: orta · Zorluk: kolay*

Ekran okuyucular bir alanı etiketiyle duyurur. Yer tutucu (placeholder) metni yazarken kaybolur ve etiket yerine geçmez; etiketsiz formlar müşteri kaybettirir.

**Nasıl düzeltilir**

1. Her alana bir <label for="id"> verin; görünür metni gerçekten yoksa aria-label kullanın.
2. Etiketleri alanların üstünde görünür tutun.

```html
<label for="email">Email</label>
<input id="email" name="email" type="email" autocomplete="email">
```

### Sayfa bölümleri (landmark)

*Etki: düşük · Zorluk: kolay*

<main>, <nav>, <header> ve <footer>, ekran okuyucu kullananların önce tüm menüyü dinlemek yerine doğrudan içeriğe atlamasını sağlar.

**Nasıl düzeltilir**

1. Ana içeriği tek bir <main> öğesiyle sarın.
2. Menüler için <nav>, sayfa çerçevesi için <header> ve <footer> kullanın.

```html
<header>…</header>
<nav>…</nav>
<main id="main">…</main>
<footer>…</footer>
```

### Adı olan düğmeler ve bağlantılar

*Etki: orta · Zorluk: kolay*

Yalnızca ikondan oluşan bir düğme ya da alt metni olmayan bir görsel bağlantı, sadece "düğme" veya "bağlantı" olarak okunur. Kimse ne işe yaradığını anlayamaz; arama motorları da bağlantı metni alamaz.

**Nasıl düzeltilir**

1. Menü, arama ve kapat gibi ikon düğmelerine görünür bir metin ya da aria-label="…" ekleyin.
2. Bağlantı içindeki görsellere, bağlantının nereye gittiğini anlatan bir alt metni verin.

```html
<button type="button" aria-label="Open menu">
  <svg aria-hidden="true">…</svg>
</button>
```

### Anlamlı alt metinler

*Etki: düşük · Zorluk: kolay*

"resim" ya da dosya adından oluşan bir alt metni, hiç olmaması kadar işe yaramaz: ekran okuyucular bunu sesli okur, görsel araması ise hiçbir şey öğrenmez.

**Nasıl düzeltilir**

1. Görselin ne gösterdiğini kısa bir cümleyle anlatın.
2. Yalnızca süs amaçlı görsellerde alt="" kullanın.

```html
<img src="vase.webp" alt="Handmade red ceramic vase on a wooden table">
```

### Boş başlıklar

*Etki: düşük · Zorluk: kolay*

Boş <h1>–<h6> etiketleri, ekran okuyucuların ve arama motorlarının sayfa yapısını anlamak için kullandığı ana hattı bozar.

**Nasıl düzeltilir**

1. Boş başlık etiketlerini kaldırın ya da metinlerini geri koyun; boşluk ve görünüm için başlık etiketi değil CSS kullanın.

### Geçerli dil kodu

*Etki: düşük · Zorluk: kolay*

lang="tr_TR" ya da lang="turkish" gibi bir kod geçerli değildir; ekran okuyucular ve tarayıcılar onu yok sayar. tr, en ya da en-GB gibi bölgeli bir biçim kullanın.

**Nasıl düzeltilir**

1. tr, en ya da en-GB gibi bir BCP 47 kodu kullanın (alt çizgi değil, tire).

```html
<html lang="tr">
```

**Kaynaklar:** [Mobile-first indexing](https://developers.google.com/search/docs/crawling-indexing/mobile/mobile-sites-mobile-first-indexing) · [Decorative images (W3C)](https://www.w3.org/WAI/tutorials/images/decorative/)

<a name="social"></a>

## Sosyal ve şema

Sayfanın paylaşıldığında nasıl göründüğü ve onu tanımlayan yapısal veri.

### Open Graph başlık ve açıklama

*Etki: düşük · Zorluk: kolay*

Bağlantınız WhatsApp, LinkedIn ya da Facebook'ta paylaşıldığında önizleme metnini bu etiketler belirler. Yoksa önizleme bozuk görünür.

**Nasıl düzeltilir**

1. og:title ve og:description ekleyin (title ve description ile aynı olabilir).

```html
<meta property="og:title" content="Corporate websites that bring in customers">
<meta property="og:description" content="Fast, mobile-first sites with a fixed quote.">
```

### Paylaşım görseli (og:image)

*Etki: düşük · Zorluk: kolay*

Görselli paylaşımlar, düz metin bağlantılardan çok daha fazla tıklanır.

**Nasıl düzeltilir**

1. Logonuz ve mesajınızla 1200×630 px bir görsel hazırlayın.
2. Mutlak bir https adresiyle belirtin.

```html
<meta property="og:image" content="https://example.com/og.png">
```

### X (Twitter) kartı

*Etki: düşük · Zorluk: kolay*

twitter:card etiketi, bağlantılarınızın X'te büyük görselli önizlemeyle görünmesini sağlar.

**Nasıl düzeltilir**

1. twitter:card ekleyin; geri kalanı için X, Open Graph etiketlerinizi kullanır.

```html
<meta name="twitter:card" content="summary_large_image">
```

### Yapısal veri (JSON-LD)

*Etki: orta · Zorluk: orta*

Schema.org işaretlemesi arama motorlarına ve yapay zekâya sayfanın tam olarak ne olduğunu söyler: şirket, ürün, makale. Tek başına sıralamayı yükseltmez; ama yıldız, fiyat ve iz menüsü gibi zengin sonuçlar için gereklidir.

**Nasıl düzeltilir**

1. Kuruluşunuzu ana sayfada tanımlayın.
2. Her sayfaya uygun türü ekleyin: Product, Service, Article, LocalBusiness, BreadcrumbList.
3. Zengin Sonuç Testi ile doğrulayın.

```html
<script type="application/ld+json">
{"@context":"https://schema.org","@type":"Organization",
 "name":"Example Ltd","url":"https://example.com",
 "logo":"https://example.com/logo.png"}
</script>
```

### Organization (kuruluş) şeması

*Etki: orta · Zorluk: kolay*

Ana sayfadaki Organization ya da LocalBusiness işaretlemesi adınızı, logonuzu, adresinizi ve profillerinizi birbirine bağlar; Google sizinle ilgili gösterdiği logo ve ayrıntılar için bunu kullanır. Tek bir sayfa yeterlidir, genellikle ana sayfa.

**Nasıl düzeltilir**

1. Organization (ya da adres ve çalışma saatleriyle LocalBusiness) ekleyin.
2. Sosyal profillerinizi sameAs içinde listeleyin.

```json
{"@context":"https://schema.org","@type":"LocalBusiness","name":"Example",
 "address":{"@type":"PostalAddress","addressLocality":"Ankara"},
 "sameAs":["https://www.linkedin.com/company/example"]}
```

### Breadcrumb (iz) şeması

*Etki: düşük · Zorluk: kolay*

BreadcrumbList, Google'ın masaüstü sonuçlarında uzun bir adres yerine sayfanın sitedeki yerini ("Ana sayfa › Hizmetler › Web tasarım") göstermesini sağlar ve site yapınızı açıkça belirtir.

**Nasıl düzeltilir**

1. Görünür iz menüsü olan iç sayfalara BreadcrumbList işaretlemesi ekleyin.

```json
{"@context":"https://schema.org","@type":"BreadcrumbList","itemListElement":[
 {"@type":"ListItem","position":1,"name":"Home","item":"https://example.com/"},
 {"@type":"ListItem","position":2,"name":"Services","item":"https://example.com/services"}]}
```

### Paylaşım görseli çalışıyor

*Etki: orta · Zorluk: kolay*

og:image bozuksa ya da oranı uygun değilse sitenizin bağlantıları düz gri bir kutu ya da kırpılmış bir resim olarak paylaşılır ve çok daha az tıklanır.

**Nasıl düzeltilir**

1. 5 MB'ın altında, 1200×630 px bir JPEG ya da PNG kullanın.
2. Giriş gerektirmeden açılan mutlak bir https adresi kullanın.
3. LinkedIn Post Inspector ya da Facebook Paylaşım Hata Ayıklayıcı ile test edin.

### Geçerli JSON-LD

*Etki: orta · Zorluk: kolay*

Yanlış yerdeki tek bir virgül JSON-LD bloğunu okunamaz hâle getirir; Google içindeki tüm yapısal veriyi sessizce yok sayar.

**Nasıl düzeltilir**

1. Bloğu Schema Markup Validator'a (validator.schema.org) yapıştırın ve hataları düzeltin.
2. JSON-LD'yi elle yazmak yerine kodla üretin (örneğin PHP'de json_encode).

```html
<script type="application/ld+json">
<?= json_encode($schema, JSON_UNESCAPED_UNICODE | JSON_UNESCAPED_SLASHES) ?>
</script>
```

### Yapısal veri alanları

*Etki: orta · Zorluk: orta*

Zengin sonuçlar (yorum yıldızları, fiyatlar, etkinlikler, iz menüsü) yalnızca zorunlu özellikler doldurulduğunda görünür; önerilen özellikler onları zenginleştirir.

**Nasıl düzeltilir**

1. Burada listelenen eksik özellikleri JSON-LD'nize ekleyin.
2. Sonucu Google'ın Zengin Sonuçlar Testi'nde kontrol edin.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Ardena",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png"
}
</script>
```

### Arama sonuçlarında site adı

*Etki: düşük · Zorluk: kolay*

Google, sonucunuzun üstünde bir site adı gösterir. Bunu WebSite yapısal verisinden ya da og:site_name'den okur; yoksa tahmin eder ya da yalnızca alan adını gösterir.

**Nasıl düzeltilir**

1. Ana sayfaya marka adınızı içeren WebSite JSON-LD'si ekleyin.
2. Her sayfaya og:site_name ekleyin.

```html
<script type="application/ld+json">
{"@context": "https://schema.org", "@type": "WebSite", "name": "Ardena", "url": "https://example.com/"}
</script>
```

### Profillerinize bağlantılar

*Etki: düşük · Zorluk: kolay*

Resmî sosyal medya profillerinize bağlantı vermek ve onları sameAs'te listelemek, Google'ın ve yapay zekâ asistanlarının sitenizi markanızın başka yerlerdeki varlığıyla eşleştirmesine yardım eder.

**Nasıl düzeltilir**

1. Profillerinize footer'dan bağlantı verin.
2. Aynı adresleri Organization şemanızdaki sameAs içinde listeleyin.

```text
"sameAs": [
  "https://www.linkedin.com/company/your-company",
  "https://www.instagram.com/your-company"
]
```

**Kaynaklar:** [Structured data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) · [Organization markup](https://developers.google.com/search/docs/appearance/structured-data/organization) · [Site names](https://developers.google.com/search/docs/appearance/site-names) · [Breadcrumbs](https://developers.google.com/search/docs/appearance/structured-data/breadcrumb) · [The Open Graph protocol](https://ogp.me/)

<a name="local"></a>

## Yerel SEO

Belirli bir yerde ya da bölgede hizmet veren işletmeler için. Her sayfa için geçerli değildir.

### Telefon numarası

*Etki: orta · Zorluk: kolay*

Yerel bir işletme için telefon araması çoğu zaman dönüşümün kendisidir. Tıkla-ara bağlantısı aramayı tek dokunuşa indirir; numara, Google'daki kayıt bilgilerinizi de doğrular.

**Nasıl düzeltilir**

1. Numarayı header ya da footer'da tel: bağlantısı olarak gösterin.
2. Google İşletme Profilinizdeki numaranın aynısını kullanın.

```html
<a href="tel:+902120000000">+90 212 000 00 00</a>
```

### Adres

*Etki: orta · Zorluk: kolay*

Google İşletme Profilinizle ve rehberlerle aynı olan görünür bir adres (ad, adres, telefon: NAP), müşterilerin sizi bulmasını sağlar ve işletme bilgilerinizi internet genelinde tutarlı tutar.

**Nasıl düzeltilir**

1. Tam adresi footer'a ya da iletişim bölümüne, her yerde aynı biçimde yazın.
2. <address> ile ve JSON-LD'de PostalAddress ile işaretleyin.

```html
<address>Ardena, Atatürk Cad. No: 12, 06100 Çankaya/Ankara</address>
```

### LocalBusiness şeması

*Etki: orta · Zorluk: kolay*

LocalBusiness JSON-LD'si (ya da Dentist, Restaurant gibi bir alt tür) adresinizi, telefonunuzu ve saatlerinizi Google'ın ve yapay zekâ asistanlarının güvenip gösterebileceği bir biçimde bildirir.

**Nasıl düzeltilir**

1. En uygun alt türle LocalBusiness ekleyin: name, address, telephone, openingHoursSpecification ve geo.
2. Google İşletme Profilinizdeki bilgilerin birebir aynısını kullanın.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Dentist",
  "name": "Ardena Dental",
  "telephone": "+90 212 000 00 00",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Atatürk Cad. No: 12",
    "addressLocality": "Ankara",
    "postalCode": "06100",
    "addressCountry": "TR"
  },
  "openingHoursSpecification": [{
    "@type": "OpeningHoursSpecification",
    "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
    "opens": "09:00", "closes": "18:00"
  }]
}
</script>
```

### Harita

*Etki: düşük · Zorluk: kolay*

Bir harita ya da Google Haritalar kaydınıza bağlantı, ziyaretçilerin gelişini planlamasına ve doğru girişi bulmasına yardım eder.

**Nasıl düzeltilir**

1. Google Haritalar konumunuzu iletişim sayfasına yerleştirin; sayfa hızlı kalsın diye tıklayınca yükleyin.
2. Ya da Haritalar profilinize bağlantı verin (maps.app.goo.gl/…).

### Çalışma saatleri

*Etki: düşük · Zorluk: kolay*

İnsanlar "şimdi açık" diye arar. Sitede ve şemada yazan saatler boşa yapılan yolculukları ve aramaları azaltır; Google profilinizle de aynı olmalıdır.

**Nasıl düzeltilir**

1. Çalışma saatlerinizi iletişim sayfasında listeleyin.
2. LocalBusiness şemanıza openingHoursSpecification ekleyin.

### İletişim sayfası bağlantısı

*Etki: düşük · Zorluk: kolay*

Her sayfada görünen net bir iletişim bağlantısı, ziyaretçiler ve Google'ın kalite değerlendiricileri için bir güven işaretidir ve müşteriye giden en kısa yoldur.

**Nasıl düzeltilir**

1. Ana menüde ve footer'da "İletişim" bağlantısı verin.

**Kaynaklar:** [Local business markup](https://developers.google.com/search/docs/appearance/structured-data/local-business)

<a name="vitals"></a>

## Core Web Vitals

Google PageSpeed Insights ile ölçülen Core Web Vitals değerleri ve PageSpeed puanları.

### Mobil hız puanı (Google)

*Etki: yüksek · Zorluk: orta*

Google'ın Lighthouse puanı, orta seviye bir telefonda sayfanın ne kadar hızlı yüklendiğini ve kullanılabilir hâle geldiğini özetler. Ziyaretçilerinizin çoğu telefondan gelir.

**Nasıl düzeltilir**

1. Bu rapordaki hız fırsatları listesinin en büyük maddelerinden başlayın.
2. Görselleri sıkıştırıp küçültün, scriptleri erteleyin, kullanılmayan eklentileri kaldırın.
3. Her değişiklikten sonra yeniden test edin; puan ölçümler arasında birkaç puan oynar.

### En büyük içerik boyaması (LCP)

*Etki: yüksek · Zorluk: orta*

LCP, ana görselin ya da başlığın göründüğü andır. 2,5 saniyenin üzerinde ziyaretçi sayfayı yavaş bulur; Google'ın üç Core Web Vitals ölçütünden biridir.

**Nasıl düzeltilir**

1. Ana görseli küçültün (doğru boyutta WebP ya da AVIF) ve fetchpriority="high" verin.
2. Üstteki ana görseli asla tembel yüklemeyin.
3. Önbellek, daha iyi hosting ya da CDN ile sunucu yanıtını hızlandırın.

```html
<img src="hero.webp" width="1200" height="600" fetchpriority="high" alt="…">
```

### Tepki süresi (INP)

*Etki: yüksek · Zorluk: zor*

INP, sayfanın dokunuş ve tıklamalara ne kadar hızlı tepki verdiğini ölçer. 200 ms'nin üzerinde düğmeler takılıyor gibi gelir; bir Core Web Vitals ölçütüdür. Gerçek kullanıcı verisi yoksa yerine laboratuvar ölçümü TBT kullanılır.

**Nasıl düzeltilir**

1. Ağır JavaScript'i azaltın: kullanılmayan kütüphaneler, slider'lar ve açılışta yüklenen sohbet widget'ları.
2. Uzun görevleri bölün; üçüncü taraf scriptleri sayfa kullanılabilir olduktan sonra yükleyin.

### Düzen kayması (CLS)

*Etki: orta · Zorluk: orta*

CLS, sayfanın yüklenirken ne kadar kaydığını ölçer. Yer değiştiren düğmeler yanlış dokunuşlara yol açar ve özensiz görünür; bir Core Web Vitals ölçütüdür.

**Nasıl düzeltilir**

1. Görsellere ve videolara width ve height öznitelikleri verin.
2. Reklamlar, gömülü içerikler ve çerez bantları için yer ayırın.
3. Benzer bir yedek fontla font-display: swap kullanın.

```html
<img src="team.webp" width="800" height="533" alt="…">
.embed { aspect-ratio: 16 / 9; }
```

### Masaüstü hız puanı (Google)

*Etki: orta · Zorluk: orta*

Aynı Lighthouse testi, masaüstü bağlantısıyla. Düşük bir masaüstü puanı genellikle ağdan çok ağır scriptlere ya da yavaş bir sunucuya işaret eder.

**Nasıl düzeltilir**

1. Bu rapordaki hız fırsatları listesini sırayla uygulayın.
2. Sunucu yanıt süresini ve sayfa önbelleğini kontrol edin.

**Kaynaklar:** [Core Web Vitals](https://developers.google.com/search/docs/appearance/core-web-vitals) · [Web Vitals (web.dev)](https://web.dev/articles/vitals)

<a name="links"></a>

## Bağlantılar

Sayfadaki bağlantıların ve görsellerin çalışıp çalışmadığı.

### Kırık bağlantılar

*Etki: yüksek · Zorluk: kolay*

Olmayan sayfalara giden bağlantılar ziyaretçinin vaktini boşa harcar, güveni zedeler ve Google'ın sitenize ayırdığı tarama bütçesini israf eder.

**Nasıl düzeltilir**

1. Bu raporda listelenen her bağlantıyı düzeltin ya da kaldırın.
2. Bir sayfayı sildiğinizde adresini en yakın karşılığına 301 ile yönlendirin.

### Kırık görseller

*Etki: orta · Zorluk: kolay*

Bulunamayan görseller boş kutular ya da kırık ikonlar gösterir ve siteyi terk edilmiş gibi gösterir.

**Nasıl düzeltilir**

1. Eksik dosyaları yeniden yükleyin ya da bu raporda listelenen referansları kaldırın.

### Yönlendirmeli bağlantılar

*Etki: düşük · Zorluk: kolay*

Bir yönlendirmeden geçen iç bağlantılar her tıklamaya gecikme, tarayıcılara da ek iş ekler. Doğrudan son adrese bağlantı verin.

**Nasıl düzeltilir**

1. İç bağlantıları doğrudan son adrese yönlendirin; neden çoğu zaman eksik bir sondaki / ya da eski bir http:// bağlantısıdır.

**Kaynaklar:** [Crawlable links](https://developers.google.com/search/docs/crawling-indexing/links-crawlable) · [HTTP status codes](https://developers.google.com/search/docs/crawling-indexing/http-network-errors)

<a name="site"></a>

## Site taraması

Sitenin sayfa sayfa taranmasını gerektiren kontroller.

### Hata veren sayfalar

*Etki: yüksek · Zorluk: orta*

4xx ya da 5xx hatası veren sayfalar arama sonuçlarından düşer ve kendi menülerinizden gelen ziyaretçileri hayal kırıklığına uğratır.

**Nasıl düzeltilir**

1. Tarama tablosunda işaretlenen sayfaları düzeltin ya da kaldırın.
2. Sunucu hataları (5xx) genellikle bozuk bir eklenti ya da veritabanı bağlantısı demektir: hata kaydını kontrol edin.

### Tekrarlanan başlıklar

*Etki: orta · Zorluk: kolay*

Birden fazla sayfa aynı başlığı paylaştığında Google hangisini göstereceğini bilemez, başlıkları çoğu zaman kendisi yeniden yazar ve sayfalar birbiriyle yarışır.

**Nasıl düzeltilir**

1. Listedeki her sayfaya kendine özgü bir başlık yazın.
2. CMS'de başlıkları sabit bir metinden değil, sayfa adı ve marka adından oluşturun.

### Tekrarlanan açıklamalar

*Etki: düşük · Zorluk: kolay*

Birçok sayfada aynı meta açıklama, sonuçlarınızın aramada birbirinin aynısı görünmesine yol açar; insanlar neden birini seçeceklerini göremez.

**Nasıl düzeltilir**

1. Her önemli sayfa için onu farklı kılan şeyi anlatan bir açıklama yazın.
2. Site geneli tek bir açıklamayı tekrar etmektense açıklamayı boş bırakın.

### Başlığı olmayan sayfalar

*Etki: yüksek · Zorluk: kolay*

Başlığı olmayan bir sayfa, arama sonuçlarında adresini ya da tahmini bir metni gösterir ve neredeyse hiç tıklanmaz.

**Nasıl düzeltilir**

1. Listelenen her sayfaya 30–65 karakterlik bir başlık ekleyin.

### Açıklaması olmayan sayfalar

*Etki: orta · Zorluk: kolay*

Meta açıklama olmadan Google, sonuçtaki metin için sayfadan rastgele bir parça seçer; bu nadiren sayfayı iyi anlatır.

**Nasıl düzeltilir**

1. Listelenen önemli sayfalar için 70–165 karakterlik bir açıklama yazın.

### H1'i olmayan sayfalar

*Etki: orta · Zorluk: kolay*

H1, ziyaretçiler ve arama motorları için sayfanın ana başlığıdır; o olmadan sayfanın konusu daha az anlaşılır olur.

**Nasıl düzeltilir**

1. Listelenen her sayfaya konusunu söyleyen tek bir H1 verin.

### Neredeyse metinsiz sayfalar

*Etki: orta · Zorluk: orta*

Google'ın bir asgari kelime sayısı yoktur; ama neredeyse hiç metni olmayan sayfalar (boş kategoriler, etiket sayfaları, yer tutucular) nadiren birine yarar ve çok sayıda olmaları Google'ın tüm siteye bakışını olumsuz etkileyebilir.

**Nasıl düzeltilir**

1. Önemli olanları faydalı ayrıntılarla genişletin: müşterilerin sorduğu sorular, fiyatlar, örnekler.
2. Aramada hiçbir zaman işe yaramayacak sayfaları birleştirin ya da noindex yapın.

### noindex sayfalar

*Etki: yüksek · Zorluk: kolay*

noindex etiketi bir sayfayı Google'dan kaldırır. Teşekkür sayfaları için doğrudur; ama bir hizmet sayfasında unutulmuş bir noindex sessizce trafik kaybettirir.

**Nasıl düzeltilir**

1. Listedeki her sayfayı kontrol edin; sıralanması gerekenlerden noindex'i kaldırın.
2. noindex sayfaları site haritasından çıkarın.

### Site haritası kapsamı

*Etki: orta · Zorluk: kolay*

Site haritasında olmayan sayfalar daha geç bulunur; site haritasındaki yönlenen ya da hata veren adresler Google'ı boşuna dolaştırır.

**Nasıl düzeltilir**

1. Taramada bulunan dizine eklenebilir sayfaları site haritasına ekleyin.
2. Yönlenen, hata veren ya da noindex olan adresleri çıkarın.

### İç bağlantı almayan sayfalar

*Etki: orta · Zorluk: kolay*

Bu sayfalar site haritanızda var ama taranan hiçbir sayfa onlara bağlantı vermiyor. Google sayfaları çoğunlukla bağlantılardan bulur; bu yetim sayfalar geç keşfedilir, seyrek taranır ve iç bağlantı değeri alamaz; ziyaretçiler de onlara hiç ulaşamaz.

**Nasıl düzeltilir**

1. Listedeki her sayfaya ilgili bir sayfadan bağlantı verin: menü, kategori ya da ilgili bir yazı.
2. Artık gerekmeyen bir sayfayı site haritasından çıkarın ya da yönlendirin.

### Yavaş sayfalar

*Etki: orta · Zorluk: orta*

Bazı sayfalarda yavaş sunucu yanıtı, genellikle o şablonlardaki ağır veritabanı sorgularına ya da eksik önbelleğe işaret eder.

**Nasıl düzeltilir**

1. Bu şablonlar için sayfa önbelleğini açın.
2. Listelenen sayfalarda yavaş eklenti ya da sorgu arayın.

### Tıklama derinliği

*Etki: düşük · Zorluk: orta*

Ana sayfadan üç tıklamadan daha uzaktaki sayfalar daha seyrek taranır ve daha az iç bağlantı değeri alır.

**Nasıl düzeltilir**

1. Önemli sayfalara menüden, footer'dan ya da merkez sayfalardan bağlantı verin.
2. Sayfalar arasına ilgili içerik bağlantıları ekleyin.

### Sitedeki alt metinler

*Etki: orta · Zorluk: kolay*

Alt metni olmayan görseller, bulundukları her sayfada görsel aramasına ve ekran okuyucu kullanıcılarına görünmezdir.

**Nasıl düzeltilir**

1. Listelenen sayfalardaki görsellere alt metni ekleyin; süs görsellerinde alt="" kullanın.

**Kaynaklar:** [Building a sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap) · [Canonical URLs](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls) · [Blocking indexing with noindex](https://developers.google.com/search/docs/crawling-indexing/block-indexing)

---

[irodev.net](https://irodev.net) araçlarının analiz rehberinden 2026-10-23 tarihinde üretildi. [CC BY 4.0](LICENSE) lisansıyla.
