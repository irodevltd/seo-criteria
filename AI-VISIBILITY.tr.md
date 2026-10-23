# Yapay zekâ görünürlüğü kriterleri

[English](AI-VISIBILITY.md) · **Türkçe**

irodev.net AI görünürlük testinin 46 kontrolü: ChatGPT, Gemini, Perplexity, Claude, Copilot ve Google'ın yapay zekâ özellikleri bir sayfaya ulaşabiliyor, okuyabiliyor, anlayabiliyor ve alıntılayabiliyor mu? Her kriter motorların kendi belgelerine ya da adı verilen bir araştırmaya dayanır; kaynaklar her grubun altında. Hiçbiri kaynak gösterilmeyi garanti etmez: engelleri kaldırırlar.

Eğitim tarayıcıları (GPTBot, ClaudeBot, CCBot ve diğerleri) testte listelenir ama hiçbir zaman puanlanmaz: Sayfalarınızın gelecekteki modelleri eğitmesine izin verip vermemek sizin tercihinizdir ve sizi yapay zekâ aramasından gizlemez. Kontrolleri kendi sayfanızda [ücretsiz AI görünürlük testiyle](https://irodev.net/tr/geo-ai-gorunurluk) çalıştırabilirsiniz.

- [Yapay zekâ erişimi](#access) (15)
- [Varlık ve yapısal veri](#entity) (8)
- [Alıntılanabilirlik](#content) (14)
- [Güven](#trust) (3)
- [Site geneli hazırlık](#site) (6)

<a name="access"></a>

## Yapay zekâ erişimi

Yapay zekâ arama ve yanıt motorları sayfaya ulaşıp okuyabiliyor mu: tarayıcı bazında robots.txt kuralları, güvenlik duvarları, dizine ekleme ve alıntı yönergeleri, JavaScript olmadan metin.

### robots.txt yanıt veriyor

*Etki: yüksek · Zorluk: kolay*

Kurallara uyan her tarayıcı işe /robots.txt dosyasını isteyerek başlar. robots.txt standardına (RFC 9309) göre bu dosyaya sunucu hatası yüzünden ulaşılamazsa tarayıcı hiçbir sayfayı taramamalıdır. Dosyanın hiç olmaması (404) sorun değildir: her şeyin taranabileceği anlamına gelir.

**Nasıl düzeltilir**

1. /robots.txt hızlıca 200 (gerekmiyorsa 404) ile yanıt versin; asla 5xx hatasıyla değil.
2. Güvenlik duvarınızın ya da CDN'inizin bu dosyaya gelen istekleri sınırlamadığından veya doğrulamaya sokmadığından emin olun.

### ChatGPT arama (OAI-SearchBot)

*Etki: yüksek · Zorluk: kolay*

OpenAI, web sitelerini ChatGPT'nin arama sonuçlarında göstermek için OAI-SearchBot'u kullanır ve orada görünmek için ona izin verilmesini önerir. Yalnızca eğitim verisi toplayan GPTBot'tan ayrıdır; yani eğitimi kapatıp yine de bulunabilirsiniz.

**Nasıl düzeltilir**

1. robots.txt içinde OAI-SearchBot'a izin verin. OpenAI'a göre değişikliğin ChatGPT aramaya yansıması yaklaşık 24 saat sürer.
2. Sitenin önünde bir güvenlik duvarı ya da CDN varsa OpenAI'ın yayımladığı IP aralıklarına da izin verin.

```text
User-agent: OAI-SearchBot
Allow: /

# optional: keep model training out
User-agent: GPTBot
Disallow: /
```

### Perplexity (PerplexityBot)

*Etki: yüksek · Zorluk: kolay*

Perplexity, web sitelerini arama sonuçlarında gösterip bağlantı vermek için PerplexityBot'u kullanır ve bunun yapay zekâ modeli eğitiminde kullanılmadığını belirtir. Perplexity her yanıtın altında kaynaklarını listeler; tarayıcıyı engellemek sizi o listeden çıkarır.

**Nasıl düzeltilir**

1. robots.txt içinde PerplexityBot'a izin verin.
2. Sitenin önünde bir güvenlik duvarı ya da CDN varsa Perplexity'nin yayımladığı IP aralıklarına da izin verin.

```text
User-agent: PerplexityBot
Allow: /
```

### Claude arama (Claude-SearchBot)

*Etki: orta · Zorluk: kolay*

Anthropic'in Claude-SearchBot tarayıcısı, Claude'un arama sonuçlarını iyileştirmek için web'i tarar; Anthropic, onu engellemenin bu sonuçlardaki görünürlüğünüzü ve doğruluğunuzu azaltabileceğini belirtir. ClaudeBot ise yalnızca eğitim verisi toplayan ayrı bir tarayıcıdır.

**Nasıl düzeltilir**

1. robots.txt içinde Claude-SearchBot'a izin verin (sayfalarınızın eğitimde kullanılmasını istemiyorsanız ClaudeBot'u yine engelleyebilirsiniz).

```text
User-agent: Claude-SearchBot
Allow: /
```

### Google AI Overviews ve AI Mode (Googlebot)

*Etki: yüksek · Zorluk: kolay*

AI Overviews ve AI Mode, Google Arama'nın parçasıdır. Google'a göre bir sayfa, Googlebot onu tarayabiliyor, sayfa dizine eklenmiş ve snippet gösterilebiliyorsa kaynak olarak çıkabilir; izin verilecek ayrı bir yapay zekâ tarayıcısı ya da eklenecek özel bir dosya veya işaretleme yoktur.

**Nasıl düzeltilir**

1. Googlebot'u bu sayfadan engelleyen robots.txt kuralını kaldırın.
2. Sayfayı Google Search Console'da (URL denetimi) kontrol edin.

```text
User-agent: Googlebot
Allow: /
```

### Microsoft Copilot (Bingbot)

*Etki: yüksek · Zorluk: kolay*

Copilot yanıtlarını, Bingbot'un oluşturduğu Bing dizinine dayandırır. Bingbot bir sayfayı tarayamazsa Bing o sayfayı ne aramada ne de Copilot yanıtlarında kullanabilir.

**Nasıl düzeltilir**

1. robots.txt içinde Bingbot'a izin verin.
2. Siteyi Bing Webmaster Tools'ta doğrulayın: sayfalarınızın nasıl dizine eklendiğini ve Copilot'un onları ne sıklıkla kaynak gösterdiğini gösterir.

```text
User-agent: Bingbot
Allow: /
```

### Güvenlik duvarı yapay zekâ tarayıcılarını içeri alıyor

*Etki: yüksek · Zorluk: orta*

robots.txt erişimin yalnızca yarısıdır: bir CDN ya da güvenlik duvarı, tarayıcıları sayfaya ulaşmadan geri çevirebilir. Google, yapay zekâ özellikleri için en iyi uygulamalar arasında taramaya CDN ve barındırma altyapısının da izin vermesini sayar; OpenAI da sitelerden IP aralıklarına izin vermelerini ister. Bu sayfayı OpenAI, Perplexity ve Anthropic'in arama tarayıcılarının kullanıcı ajanlarıyla istedik.

**Nasıl düzeltilir**

1. CDN'inizin ya da güvenlik duvarınızın bot ayarlarını açın (örneğin Cloudflare'in yapay zekâ tarayıcı denetimleri) ve istediğiniz arama tarayıcılarına izin verin.
2. Onlara yalnızca kullanıcı ajanına göre değil, her firmanın yayımladığı IP aralıklarına göre izin verin: kullanıcı ajanını herkes taklit edebilir.

### Sayfa dizine eklenebilir

*Etki: yüksek · Zorluk: kolay*

AI Overviews, AI Mode ve Copilot kaynaklarını bir arama dizininden seçer. noindex içeren (meta etiketinde ya da X-Robots-Tag başlığında) veya hata ile yanıt veren bir sayfa dizinde yer almaz ve kaynak gösterilemez.

**Nasıl düzeltilir**

1. Bulunmasını istediğiniz sayfalardan noindex'i kaldırın (SEO eklentisi ayarlarına ve sunucu başlıklarına bakın).
2. Sayfanın 200 ile yanıt vermesini sağlayın.

### Yapay zekâ yanıtları metni alıntılayabilir

*Etki: yüksek · Zorluk: kolay*

Google, snippet ayarlarını AI Overviews ve AI Mode'a da uygular: nosnippet ya da max-snippet:0 metninizin gösterilmesini engeller. Bing'e göre NOARCHIVE sayfayı Copilot yanıtlarının dışında tutar, NOCACHE ise Copilot'u adres, başlık ve snippet ile sınırlar.

**Nasıl düzeltilir**

1. Yapay zekâ yanıtlarının dışında kalmak istemiyorsanız nosnippet, max-snippet:0 ve noarchive yönergelerini kaldırın.
2. Yalnızca bir bölümü gizlemek için (fiyat tablosu, yasal not) onu data-nosnippet ile sarın.

```html
<!-- keep one part out of snippets, not the whole page -->
<div data-nosnippet>…</div>
```

### JavaScript olmadan metin

*Etki: yüksek · Zorluk: zor*

Vercel ve MERJ'in 2024 araştırmasına göre büyük yapay zekâ tarayıcıları (OpenAI, Anthropic, Perplexity ve diğerleri) JavaScript çalıştırmaz; Google ve Apple'ınkiler çalıştırır. Metniniz yalnızca betikler çalıştıktan sonra görünüyorsa bu tarayıcılar boş bir sayfa görür.

**Nasıl düzeltilir**

1. Sayfayı sunucuda oluşturun (SSR) ya da önceden üretin (statik veya ön-oluşturulmuş sayfalar).
2. Sayfa kaynağını görüntüleyerek kontrol edin (denetçiyi değil): metin orada olmalı.

### Gemini uygulamaları (Google-Extended)

*Etki: orta · Zorluk: kolay*

Google-Extended bir tarayıcı değil, robots.txt belirtecidir. Google'ın sayfalarınızı Gemini'yi eğitmek ve Gemini uygulamalarındaki yanıtlara dayanak yapmak için kullanıp kullanamayacağını belirler; Google, bunun Google Arama'yı ve sıralamayı etkilemediğini söyler. Eğitime karşıysanız engellemek makul bir tercihtir ama sizi Gemini uygulaması yanıtlarının da dışında bırakır.

**Nasıl düzeltilir**

1. Bilinçli karar verin: Gemini uygulamalarında görünmek sizin için eğitim dışında kalmaktan önemliyse Google-Extended engelini kaldırın.

```text
User-agent: Google-Extended
Allow: /
```

### Siri ve Spotlight (Applebot)

*Etki: düşük · Zorluk: kolay*

Applebot; Siri, Spotlight ve Safari'deki aramayı besler. Apple'a göre eğitim belirteci olan Applebot-Extended'ı engelleyen sayfalar bu sonuçlarda yine çıkabilir. robots.txt'de Applebot kuralı yoksa Applebot, Googlebot kurallarınıza uyar.

**Nasıl düzeltilir**

1. Applebot'a izin verin; yalnızca eğitimi kapatmak istiyorsanız Applebot-Extended'ı engelleyin.

```text
User-agent: Applebot
Allow: /

# optional: keep Apple model training out
User-agent: Applebot-Extended
Disallow: /
```

### DuckDuckGo yapay zekâ yanıtları (DuckAssistBot)

*Etki: düşük · Zorluk: kolay*

DuckAssistBot, kaynak gösteren DuckDuckGo yapay zekâ destekli yanıtları için sayfaları anlık olarak okur. DuckDuckGo, bu verinin yapay zekâ eğitiminde kullanılmadığını ve botu engellemenin organik sıralamayı etkilemediğini belirtir.

**Nasıl düzeltilir**

1. robots.txt içinde DuckAssistBot'a izin verin.

```text
User-agent: DuckAssistBot
Allow: /
```

### Güncelleme tarihli site haritası (Bing, Copilot)

*Etki: orta · Zorluk: kolay*

Bing, site haritasındaki lastmod tarihini yapay zekâ destekli aramada temel bir sinyal olarak tanımlar: hangi sayfaların yeniden okunacağına bu tarihle karar verir; böylece Copilot eski bir sürümden yanıt vermez. Tarih dürüst olmalı: yalnızca içerik değiştiğinde değiştirin. IndexNow ile bir sayfa değiştiği anda Bing'e haber verebilirsiniz.

**Nasıl düzeltilir**

1. Bir XML site haritası yayımlayın ve robots.txt içinde belirtin.
2. Her adrese saatiyle birlikte ISO 8601 biçiminde, yalnızca içerik değiştiğinde güncellenen bir lastmod verin.
3. İsterseniz IndexNow ekleyin (çoğu SEO eklentisi ve CDN sunar).

```html
<url>
  <loc>https://example.com/services</loc>
  <lastmod>2026-10-21T09:30:00+03:00</lastmod>
</url>
```

### llms.txt (isteğe bağlı)

*Etki: düşük · Zorluk: kolay*

llms.txt, yapay zekâ araçları için önerilmiş bir Markdown site özetidir. Büyük yapay zekâ arama motorlarının hiçbiri bu dosyayı okuduğunu açıklamadı; Google da AI Overviews için özel yapay zekâ metin dosyalarına gerek olmadığını söylüyor. Zararı yoktur ve bazı yapay zekâ asistanları ve kodlama araçları okur; bu yüzden yalnızca dosyanız varsa biçimine bakarız: bir # başlık ve önemli sayfalarınıza bağlantılar.

**Nasıl düzeltilir**

1. Dosyanız varsa "# Ad" ile başlayın, tek satırlık bir özet ekleyin ve önemli sayfalarınızı Markdown bağlantısı olarak verin.

```text
# Example Ltd
> Corporate web design studio in Ankara.

## Services
- [Web design](https://example.com/web-design): sites for small firms
```

**Kaynaklar:** [Google: AI features and your website](https://developers.google.com/search/docs/appearance/ai-features) · [Google common crawlers (incl. Google-Extended)](https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers) · [OpenAI crawlers](https://platform.openai.com/docs/bots) · [Perplexity crawlers](https://docs.perplexity.ai/guides/bots) · [Anthropic crawlers](https://support.claude.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler) · [Applebot](https://support.apple.com/en-us/119829) · [DuckAssistBot](https://duckduckgo.com/duckduckgo-help-pages/results/duckassistbot) · [Bing Webmaster Guidelines](https://www.bing.com/webmasters/help/webmaster-guidelines-30fba23a) · [Robots meta tag (nosnippet, max-snippet)](https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag) · [The llms.txt proposal](https://llmstxt.org/)

<a name="entity"></a>

## Varlık ve yapısal veri

Motorların sitenin arkasında kimin olduğunu anlayabilmesi: yapısal veri, kuruluş bilgileri, resmî profillere bağlantılar, tutarlı tek bir ad.

### Yapısal veri (JSON-LD)

*Etki: orta · Zorluk: orta*

Yapısal veri, makinelerin tahmin etmesine gerek bırakmadan bilgileri bildirir: kim olduğunuz, ne sunduğunuz, sayfanın neyle ilgili olduğu. Google, AI Overviews için özel bir işaretlemeye gerek olmadığını söyler ama sayfaları ve içlerindeki varlıkları anlamak için yapısal veriyi kullanır; Microsoft da şemanın içeriği ürün, yorum, SSS ya da etkinlik olarak etiketlemeye yardım ettiğini belirtir.

**Nasıl düzeltilir**

1. Sayfanın gerçekte ne olduğuna uygun JSON-LD ekleyin: ana sayfada Organization ya da LocalBusiness, uygun yerlerde Product, Service, Article veya FAQPage.
2. Google'ın Zengin Sonuç Testi ya da Schema Markup Validator ile test edin.

```html
<script type="application/ld+json">
{"@context":"https://schema.org","@type":"Organization","name":"Example Ltd","url":"https://example.com/","logo":"https://example.com/logo.png"}
</script>
```

### Kuruluş (Organization) işaretlemesi

*Etki: yüksek · Zorluk: kolay*

Ana sayfadaki Organization ya da LocalBusiness işaretlemesi resmî adınızı, logonuzu, adresinizi ve profillerinizi bildirir. Google bunu kuruluşunuzu anlamak ve başkalarından ayırmak için kullanır; bir motor, birbirine benzeyen iki addan hangisinin siz olduğunu böyle anlar.

**Nasıl düzeltilir**

1. Ana sayfaya name, url, logo ve sameAs içeren Organization (ya da size en yakın LocalBusiness türü) ekleyin.

```json
{"@context":"https://schema.org","@type":"Organization","name":"Example Ltd","url":"https://example.com/",
 "logo":"https://example.com/logo.png","sameAs":["https://www.linkedin.com/company/example"]}
```

### Bağlı profiller (sameAs)

*Etki: orta · Zorluk: kolay*

sameAs, sizinle ilgili diğer sayfaları listeler: LinkedIn, Wikipedia ya da Wikidata, sosyal medya profilleri, firma rehberleri. Google'ın Organization belgesi bunu önerir; motorların sizinle ilgili başka yerlerde bulduklarını birbirine bağlar.

**Nasıl düzeltilir**

1. Resmî profillerinizin adreslerini Organization işaretlemesindeki sameAs alanına ekleyin.

```text
"sameAs": ["https://www.linkedin.com/company/example", "https://www.instagram.com/example"]
```

### Kuruluş bilgileri

*Etki: orta · Zorluk: kolay*

Google'ın Organization ve LocalBusiness belgeleri name, url ve logo alanlarını; yerel işletmeler için ayrıca address ve telephone alanlarını önerir. Biri sizi sorduğunda yapay zekâ yanıtlarının tekrar ettiği bilgiler bunlardır; kaynağı siz olmalısınız.

**Nasıl düzeltilir**

1. Organization ya da LocalBusiness işaretlemenizdeki eksik alanları doldurun.

### Yapısal veri sayfayla örtüşüyor

*Etki: orta · Zorluk: kolay*

Google'ın yapay zekâ özellikleri için en iyi uygulamaları, yapısal verinin görünen metinle örtüşmesini içerir; genel kuralları da ziyaretçinin göremediği içeriğin işaretlenmesini yasaklar. Sayfada görünmeyen şeyleri adlandıran işaretleme güvenilmez görünür.

**Nasıl düzeltilir**

1. İşaretlemedeki her ad ve başlığın sayfada aynen görünmesini sağlayın ya da işaretlemeyi düzeltin.

### Wikidata kaydı

*Etki: düşük · Zorluk: orta*

Wikidata, birçok bilgi paneli ve yapay zekâ veri setinin arkasındaki açık bilgi tabanıdır. Resmî web sitesi olarak alan adınızı gösteren bir kayıt, adınızı motorların güvendiği bir kaynakta sitenize bağlar. Yalnızca kuruluşunuz Wikidata'nın kayda değerlik kuralını karşılıyorsa kayıt açın; tanıtım amaçlı kayıtlar silinir.

**Nasıl düzeltilir**

1. Koşulları karşılıyorsanız "resmî web sitesi" (P856) alanında alan adınız olan bir kayıt oluşturun ve bağımsız kaynaklar ekleyin.
2. Ardından kaydın adresini Organization işaretlemenizdeki sameAs alanına ekleyin.

### Site adı (WebSite işaretlemesi)

*Etki: düşük · Zorluk: kolay*

Ana sayfadaki WebSite işaretlemesi ya da og:site_name, sitenin adını bildirir. Google bunu sonuçlardaki site adı için kullanır; motorlar da siteyi kaynak gösterirken sizi bu adla anar.

**Nasıl düzeltilir**

1. Ana sayfaya adınızı içeren WebSite işaretlemesi ekleyin.

```json
{"@context":"https://schema.org","@type":"WebSite","name":"Example","url":"https://example.com/"}
```

### Her yerde aynı marka adı

*Etki: orta · Zorluk: kolay*

Bing'in kuralları varlık adlarının tutarlı olmasını ister. İşaretleme, site adı ve sayfa farklı adlar kullanırsa motorlar bunları farklı işletmeler sayabilir ya da yanlış olanı seçebilir.

**Nasıl düzeltilir**

1. Organization işaretlemesinde, og:site_name'de, başlıkta ve sayfa metninde aynı adı kullanın (Ltd gibi şirket ekleri farklı olabilir).

**Kaynaklar:** [Organization markup](https://developers.google.com/search/docs/appearance/structured-data/organization) · [Site names](https://developers.google.com/search/docs/appearance/site-names) · [Structured data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data)

<a name="content"></a>

## Alıntılanabilirlik

Metnin alıntılanmaya uygun olup olmadığı: doğrudan yanıtlanan sorular, net yapı, rakamlar, alıntılar ve kaynaklar.

### Ana başlık (H1)

*Etki: orta · Zorluk: kolay*

Microsoft'un yapay zekâ yanıtları rehberi, H1'in sayfa başlığıyla örtüşmesini ya da ona çok yakın olmasını söyler. Sayfanın neyle ilgili olduğunun ilk ifadesidir.

**Nasıl düzeltilir**

1. Sayfaya, başlıktaki ifadelerle ne sunduğunu söyleyen net bir H1 verin.

```html
<h1>Corporate web design in Ankara</h1>
```

### Önemli bilgi en üstte

*Etki: orta · Zorluk: kolay*

Bing'in yapay zekâ yanıtları kuralları, önemli bilginin sayfanın üst kısmında olmasını ister. Sayfaya bunun ne olduğunu, kimin için ve nerede olduğunu söyleyen bir iki cümleyle başlayın: bir motorun tek başına kullanabileceği bir özet.

**Nasıl düzeltilir**

1. H1'in hemen altına kısa bir paragraf koyun (iki cümle, sade bir dille, hizmetiniz ve yeriniz).

```html
<h1>Corporate web design in Ankara</h1>
<p>We design and build fast, bilingual websites for small firms in Ankara, from a first sketch to launch in four weeks.</p>
```

### Soru biçiminde başlıklar

*Etki: orta · Zorluk: kolay*

Microsoft, net yanıtı olan soruların insanların yapay zekâ asistanlarına soru sorma biçimiyle örtüştüğünü belirtir. Bir müşterinin soracağı biçimde yazılmış bir başlık ve altındaki yanıt, o soruya tam oturan bir bölümdür.

**Nasıl düzeltilir**

1. Bazı başlıkları müşterilerin gerçekten sorduğu sorulara çevirin ("Bir web sitesi ne kadar sürede biter?").
2. Her birini altındaki ilk cümlede yanıtlayın.

### Ara başlıklı bölümler

*Etki: orta · Zorluk: kolay*

Yapay zekâ asistanları sayfaları küçük parçalara böler ve her parçayı ayrı değerlendirir; Microsoft bu parçaları H2 ve H3 başlıklarının belirlediğini, adımlar ve karşılaştırmalar için listelerin ve tabloların iyi çalıştığını söyler. Ara başlıksız uzun bir sayfa, alıntılanması zor tek bir bloktur.

**Nasıl düzeltilir**

1. Metni açıklayıcı H2 ve H3 başlıklarıyla bölümlere ayırın.
2. Adımlar için liste, karşılaştırmalar için tablo kullanın.

### Alıntılanacak kadar metin

*Etki: yüksek · Zorluk: orta*

Bir motor yalnızca sayfada yazanı kaynak gösterebilir; Google'ın yapay zekâ özellikleri rehberi de metin içeriğin önemini vurgular. Sihirli bir kelime sayısı yoktur: sorun neredeyse boş sayfalardır, çünkü bir yanıta alıntılanacak hiçbir şey vermezler.

**Nasıl düzeltilir**

1. Müşterinin ihtiyaç duyduğu bilgileri sayfanın kendisine yazın: ne, kimin için, nerede, ne kadar, ne kadar sürede.

### Soruların hemen ardından kısa yanıt

*Etki: orta · Zorluk: kolay*

Microsoft, sorunun hemen altında bir iki cümlelik ve tek başına alıntılandığında da anlamlı olan yanıtlar önerir. Her soru başlığının hemen ardından 8 ile 80 kelimelik bir yanıt ya da bir liste ararız.

**Nasıl düzeltilir**

1. Her yanıta doğrudan yanıtla başlayın ("Genellikle dört hafta."), ayrıntıyı sonra ekleyin.

### Uzun metin blokları yok

*Etki: düşük · Zorluk: kolay*

Microsoft, içeriği yapay zekâ yanıtlarının dışında bırakan hatalar arasında uzun metin bloklarını sayar. 150 kelimeyi aşan bir paragraf birkaç fikri bir araya sıkıştırır; her paragraf tek bir fikir anlatacak şekilde bölün.

**Nasıl düzeltilir**

1. Uzun paragrafları bölün: her paragrafta bir fikir, sıralama yaptığınız yerde liste.

### Görsellerin metin açıklaması

*Etki: düşük · Zorluk: kolay*

Microsoft, önemli bilgileri yalnızca görsellere koymaya karşı uyarır: her görsele alt metin verin ve önemli bilgileri HTML metninde de tutun. Alt metin aynı zamanda bir erişilebilirlik gereğidir.

**Nasıl düzeltilir**

1. Her görsele bir alt niteliği ekleyin (yalnızca süs olanlar için alt="").
2. Fiyat, çalışma saati gibi bilgileri asla yalnızca görselin içine koymayın.

### Somut rakamlar

*Etki: orta · Zorluk: kolay*

2024 tarihli GEO araştırmasında (Aggarwal ve ark., KDD 2024) istatistik eklemek, bir sayfanın üretken motor yanıtlarındaki görünürlüğünü en çok artıran değişiklikler arasındaydı. Microsoft da "yenilikçi" gibi sözcükler yerine ölçülebilir bilgilere dayanan ifadeler ister. Yalnızca arkasında durabileceğiniz rakamları kullanın.

**Nasıl düzeltilir**

1. Belirsiz iddiaları bilgilerle değiştirin: teslim süreleri, fiyatlar, ölçüler, kaç yıldır faaliyette olduğunuz, proje sayıları.

### Alıntılar

*Etki: düşük · Zorluk: kolay*

Aynı GEO araştırması, güvenilir kaynaklardan alıntı eklemenin en etkili değişikliklerden biri olduğunu buldu. Yararlı olduğu yerde adı belli bir uzmanı, bir standardı ya da gerçek bir müşteriyi alıntılayın ve alıntı olarak işaretleyin. Asla uydurma alıntı ya da yorum kullanmayın.

**Nasıl düzeltilir**

1. Alıntı için kaynağı belirtilmiş bir <blockquote> kullanın.

```html
<blockquote>
  <p>The site went live in three weeks.</p>
  <footer>Ayşe K., owner of Example Bakery</footer>
</blockquote>
```

### Kaynak gösterme

*Etki: düşük · Zorluk: kolay*

Kaynak göstermek, GEO araştırmasında en çok işe yarayan yöntemlerin üçüncüsüydü. İddialarınızın dayandığı standartlara, araştırmalara ya da resmî sayfalara bağlantı vermek okurların ve motorların bunları doğrulamasını sağlar.

**Nasıl düzeltilir**

1. Rakamlarınızın ve iddialarınızın kaynaklarına doğrudan metnin içinden bağlantı verin.

### Yazılarda görünür tarih

*Etki: orta · Zorluk: kolay*

Microsoft, yapay zekâ yanıtlarının aradığı nitelikler arasında güncelliği sayar; Google da görünür bir tarih göstermeyi ve işaretlemeye datePublished ile dateModified eklemeyi önerir. Tarih, motorlara bilginin ne kadar güncel olduğunu söyler.

**Nasıl düzeltilir**

1. Yayın tarihini (güncellediğinizde güncelleme tarihini de) başlığın yakınında gösterin ve ikisini de Article işaretlemesine ekleyin.

```html
<time datetime="2026-10-21">21 October 2026</time>
```

### Yazılarda yazar

*Etki: düşük · Zorluk: kolay*

Google'ın faydalı içerik rehberi "içeriği kim oluşturdu?" diye sorar ve okurların beklediği yerde yazar adı göstermeyi önerir. Profil sayfası olan, adı belli bir yazar, yazıya güvenmeyi ve onu kaynağına bağlamayı kolaylaştırır.

**Nasıl düzeltilir**

1. Yazıya, kısa bir profil sayfasına bağlanan yazar adı ekleyin; Article işaretlemesine de author alanını ekleyin.

### SSS (FAQPage) işaretlemesi

*Etki: düşük · Zorluk: kolay*

Bir sayfada birkaç soru ve yanıt olduğunda FAQPage işaretlemesi her soru-yanıt çiftini makineler için etiketler; Microsoft da SSS'yi şemanın etiketleyebildiği içerik türleri arasında sayar. Google'da zengin sonuç beklemeyin: Google, SSS zengin sonuçlarını 7 Mayıs 2026'da kaldırdı.

**Nasıl düzeltilir**

1. Sayfada görünen soruları ve yanıtları, kelimesi kelimesine, FAQPage ile işaretleyin.

```json
{"@context":"https://schema.org","@type":"FAQPage","mainEntity":[{"@type":"Question","name":"How long does a website take?",
 "acceptedAnswer":{"@type":"Answer","text":"Usually four weeks from the first meeting."}}]}
```

**Kaynaklar:** [GEO: Generative Engine Optimization (Aggarwal et al., KDD 2024)](https://arxiv.org/abs/2311.09735) · [Creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)

<a name="trust"></a>

## Güven

Sayfanın arkasında gerçek ve ulaşılabilir bir işletme olduğunu gösteren sinyaller.

### Hakkımızda ve iletişim sayfaları

*Etki: orta · Zorluk: kolay*

Google'ın faydalı içerik rehberi sitenin arkasında kimin olduğunun açık olup olmadığını sorar; kalite değerlendirici kuralları da siteden kimin sorumlu olduğuna ve ona nasıl ulaşılacağına bakar. Sizi bir yapay zekâ yanıtında bulan insanlar iletişime geçmeden önce tam olarak bunu kontrol eder.

**Nasıl düzeltilir**

1. Her sayfanın menüsünden ya da alt bilgisinden bir hakkımızda ve bir iletişim sayfasına bağlantı verin.

### İletişim bilgileri

*Etki: orta · Zorluk: kolay*

Sayfadaki telefon, e-posta ve adres (bağlantı olarak ya da Organization işaretlemenizde), biri size nasıl ulaşılacağını sorduğunda motorların tekrar ettiği bilgileri eski bir rehberden değil, kendi sitenizden verir.

**Nasıl düzeltilir**

1. Telefonunuzu tel:, e-postanızı mailto: bağlantısı olarak gösterin ve ikisini Organization işaretlemesine ekleyin.

```html
<a href="tel:+903120000000">+90 312 000 00 00</a> · <a href="mailto:info@example.com">info@example.com</a>
```

### Gizlilik politikası

*Etki: düşük · Zorluk: orta*

Bir site kişisel veri topladığı anda (bir iletişim formuyla bile) gizlilik politikası yasal bir zorunluluktur (KVKK, GDPR). Aynı zamanda bir yapay zekâ yanıtının size yönlendirdiği insanlara işletmenizin hesap verebilir görünmesini sağlar.

**Nasıl düzeltilir**

1. Topladığınız verilere uygun bir gizlilik politikası yayımlayın ve alt bilgiden bağlantı verin.

**Kaynaklar:** [Creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) · [Bing Webmaster Guidelines](https://www.bing.com/webmasters/help/webmaster-guidelines-30fba23a)

<a name="site"></a>

## Site geneli hazırlık

Sitenin yapay zekâ tarayıcılarının okuduğu gibi baştan sona taranmasını gerektiren kontroller.

### Her sayfa JavaScript olmadan okunabiliyor

*Etki: yüksek · Zorluk: zor*

"JavaScript olmadan metin" testinin taranan her sayfadaki hâli: Google ve Apple dışındaki büyük yapay zekâ tarayıcıları betik çalıştırmaz.

**Nasıl düzeltilir**

1. Bu sayfaları sunucuda oluşturun ya da önceden oluşturun.

### Sitenin genelinde yapısal veri

*Etki: orta · Zorluk: orta*

Hiç JSON-LD içermeyen sayfalar, motorları sayfanın ne olduğunu tahmin etmeye bırakır. Ana sayfada Organization, hizmet, ürün ve yazı sayfalarında kendi türleri olmalı.

**Nasıl düzeltilir**

1. CMS'inizde sayfa türüne göre JSON-LD şablonları ekleyin; böylece her yeni sayfa otomatik olarak alır.

### Dizin dışında tutulan sayfalar

*Etki: yüksek · Zorluk: kolay*

noindex bir sayfayı aramanın ve aramaya dayanan yapay zekâ yanıtlarının dışında tutar. Teşekkür ya da hesap sayfaları için doğrudur ama site haritasında listelediğiniz sayfalarda bir hatadır.

**Nasıl düzeltilir**

1. Bulunmasını istediğiniz sayfalardan noindex'i kaldırın ya da onları site haritasından çıkarın.

### Yapay zekâ yanıtlarının alıntılayamayacağı sayfalar

*Etki: yüksek · Zorluk: kolay*

nosnippet ya da max-snippet:0 bir sayfanın metnini Google'ın yapay zekâ özelliklerinin dışında tutar; NOARCHIVE ise Copilot yanıtlarının dışında tutar.

**Nasıl düzeltilir**

1. Alıntılanmasını istediğiniz sayfalardan bu yönergeleri kaldırın (çoğu zaman site geneli bir SEO eklentisi ayarıdır).

### Hata veren sayfalar

*Etki: orta · Zorluk: kolay*

404 ya da 5xx ile yanıt veren bir sayfa taranamaz, dizine eklenemez ve kaynak gösterilemez; ona verilen bağlantılar da taramayı boşa harcar.

**Nasıl düzeltilir**

1. Bozuk sayfaları düzeltin ya da (301 ile) yönlendirin ve onlara giden bağlantıları güncelleyin.

### Yapay zekâ arama tarayıcılarına kapalı sayfalar

*Etki: yüksek · Zorluk: kolay*

robots.txt kuralları, kimse fark etmeden yapay zekâ arama tarayıcılarını sitenin bazı bölümlerinden engelleyebilir: örneğin bir yönetim klasörü için yazılıp hizmet sayfalarınızı da kapsayan bir kural.

**Nasıl düzeltilir**

1. Bu sayfalara uyan kuralları gözden geçirip daraltın.

**Kaynaklar:** [Google: AI features and your website](https://developers.google.com/search/docs/appearance/ai-features)

---

[irodev.net](https://irodev.net) araçlarının analiz rehberinden 2026-10-23 tarihinde üretildi. [CC BY 4.0](LICENSE) lisansıyla.
