# SEO ve yapay zekâ araması efsaneleri

[English](MYTHS.md) · **Türkçe**

Birçok analiz aracının sorun diye saydığı ama arama motorlarının kendi belgelerinin desteklemediği şeyler. Bunları
analizlerimize katmıyoruz. Nedenini her biri için kaynağıyla birlikte aşağıda bulabilirsiniz (kaynaklar İngilizcedir).

### 1. "Anahtar kelime yoğunluğu %2–3 olmalı"

Hedeflenecek bir yoğunluk yok. Google'ın spam politikaları *anahtar kelime doldurmayı* spam sayar; SEO Başlangıç
Rehberi de aynısını söyler. Doğal yazın ve müşterilerinizin kullandığı kelimeleri kullanın.
Kaynaklar: [Spam politikaları](https://developers.google.com/search/docs/essentials/spam-policies) ·
[SEO Başlangıç Rehberi](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)

### 2. "Bir sayfada en az 300 (ya da 1.500) kelime olmalı"

Google'ın SEO Başlangıç Rehberi, içeriğin uzunluğunun tek başına sıralama açısından önemli olmadığını; bir kelime
sayısı hedefi, alt ya da üst sınır bulunmadığını söyler. Analizimiz yalnızca neredeyse hiç metni olmayan sayfaları
işaretler, çünkü ziyaretçinin orada okuyacak bir şeyi yoktur.
Kaynak: [SEO Başlangıç Rehberi](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)

### 3. "Tam olarak bir H1, en az iki H2, kesin sırayla"

Aynı rehber, başlıkların anlamsal sırada olmasının ekran okuyuculara yardımcı olduğunu ama Google Arama açısından
sıralarının önemli olmadığını söyler. Google'ın belgelerinde tek H1 şartı yoktur. Biz
yalnızca sayfada hiç ana başlık yoksa uyarırız, çünkü böyle bir sayfa göz gezdirerek okunmaz.
Kaynak: [SEO Başlangıç Rehberi](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)

### 4. "Meta keywords etiketini doldurun"

Google'ın SEO Başlangıç Rehberi, Google Arama'nın keywords meta etiketini kullanmadığını açıkça belirtir.
Kaynak: [SEO Başlangıç Rehberi](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)

### 5. "Anahtar kelime ilk 100 kelimede geçmeli" ve "metin/HTML oranını yükseltin"

İkisi de Google'ın belgelerinde hiçbir yerde geçmez. Bunun yerine sayfanın ilk paragrafının okurun sorusunu
yanıtlamasını sağlayın; bu hem insanlara hem yapay zekâ yanıtlarına yarar.

### 6. "lang özelliği Google'a sayfanızın dilini söyler"

Google, bir sayfanın dilini görünen içerikten anladığını; lang özelliği ya da URL gibi kod düzeyindeki bilgileri
kullanmadığını söyler. Yine de doğru bir `lang` kullanın: Ekran okuyucular sayfayı doğru telaffuz etmek için ona ihtiyaç duyar.
Analizimiz de onu bu nedenle, bir erişilebilirlik konusu olarak kontrol eder.
Kaynak: [Çok bölgeli ve çok dilli siteleri yönetme](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites)

### 7. "Başlıklar 60 karakterden kısa olmalı"

Google, `<title>` öğesinin uzunluğu için bir sınır olmadığını; başlık bağlantısının gerektiğinde, genellikle cihaz
genişliğine sığacak şekilde kısaltıldığını söyler. Kısaltma karakter sayısına değil genişliğe göre yapılır.
Analizimiz 30–65 karakteri bir kural olarak değil, pratik bir aralık olarak önerir.
Kaynak: [Başlık bağlantıları](https://developers.google.com/search/docs/appearance/title-link)

### 8. "Zengin sonuç için SSS işaretlemesi ekleyin"

Ağustos 2023'ten beri Google SSS zengin sonuçlarını yalnızca iyi bilinen, yetkili devlet ve sağlık sitelerinde
gösteriyor. SSS işaretlemesi bir işletme sitesine bu zengin sonuçları kazandırmaz.
Kaynak: [HowTo ve SSS zengin sonuçlarındaki değişiklikler](https://developers.google.com/search/blog/2023/08/howto-faq-changes)

### 9. "Ana sayfaya breadcrumb (iz) işaretlemesi gerekir"

Breadcrumb izi bir sayfanın sitede nerede durduğunu gösterir. Ana sayfa her izin başladığı yerdir; göstereceği bir
şey yoktur. Breadcrumb iç sayfalara aittir.
Kaynak: [Breadcrumb yapısal verisi](https://developers.google.com/search/docs/appearance/structured-data/breadcrumb)

### 10. "Boş alt özelliği, eksik alt metin demektir"

Yalnızca süs amaçlı görsellerde `alt=""` doğru işaretlemedir: Ekran okuyuculara görseli atlamalarını söyler.
Yalnızca anlam taşıyan görsellerin bir açıklamaya ihtiyacı vardır.
Kaynak: [W3C: Dekoratif görseller](https://www.w3.org/WAI/tutorials/images/decorative/)

### 11. "Her sitede hreflang olmalı"

hreflang, Google'a bir sayfanın *yerelleştirilmiş sürümlerini* bildirir. Tek dilli bir sitenin bildireceği bir
sürüm yoktur.
Kaynak: [Sayfalarınızın yerelleştirilmiş sürümleri](https://developers.google.com/search/docs/specialty/international/localized-versions)

### 12. "Her görsel geç yüklenmeli (lazy loading)"

Sayfanın üstündeki ana görseli geç yüklemek onu geciktirir ve En Büyük İçerikli Boyamayı (LCP) kötüleştirir.
Aşağıdaki görselleri geç yükleyin, açılışta görünen görseli asla.
Kaynak: [web.dev: Geç yükleme ve LCP](https://web.dev/articles/lcp-lazy-loading)

### 13. "Her sayfada video olmalı"

Hiçbir arama motoru videoyu bir gereklilik olarak belgelemez. Video, ziyaretçiye yardımcı olduğunda ekleyin
(örneğin bir ürün tanıtımı) ve `VideoObject` işaretlemesiyle tanımlayın. Bir kutucuğu doldurmak için eklemeyin.

### 14. "Site haritasında `<lastmod>` zorunludur"

Site haritası protokolünde `<lastmod>` isteğe bağlıdır. Kullanıyorsanız doğru tutun: Yalnızca sayfanın içeriği
değiştiğinde değiştirin.
Kaynak: [sitemaps.org protokolü](https://www.sitemaps.org/protocol.html)

### 15. "HTTP/2 ve güvenlik başlıkları sıralama faktörüdür"

Google ikisini de sıralama faktörü olarak belgelemez. Sayfaları daha hızlı ve güvenli yaparlar; bu yeterli bir
nedendir ve HTTPS sayfa deneyiminin bir parçasıdır. Analizimiz onları bu nedenlerle kontrol eder ve bunu açıkça
söyler.
Kaynak: [Sayfa deneyimi](https://developers.google.com/search/docs/appearance/page-experience)

### 16. "Yapay zekâ yanıtlarında çıkmak için llms.txt (ya da özel dosyalar) gerekir"

Google, yapay zekâ özelliklerinde görünmek için yeni makine tarafından okunabilir dosyalara, yapay zekâ metin
dosyalarına ya da özel bir işaretlemeye gerek olmadığını söyler. Hiçbir büyük motor llms.txt okuduğunu belgelemez. Bu dosya onu arayan yapay
zekâ araçları için bir kolaylıktır; AI görünürlük testimiz de bu yüzden onu raporlar ama eksikliğini aleyhinize
saymaz.
Kaynaklar: [Yapay zekâ özellikleri ve web siteniz](https://developers.google.com/search/docs/appearance/ai-features) ·
[llms.txt önerisi](https://llmstxt.org/)

### 17. "GPTBot'u engellerseniz ChatGPT sizi bulamaz" (ya da "ChatGPT'de çıkmak için GPTBot'a izin verin")

OpenAI'nin ayrı tarayıcıları var: arama için OAI-SearchBot, model eğitimi için GPTBot. OpenAI her ayarın bağımsız
olduğunu söyler; yani aramaya izin verip eğitimi reddedebilirsiniz. Aynı ayrım Anthropic, Apple, Google
(Google-Extended) ve diğerlerinde de vardır. AI görünürlük testimiz yalnızca arama tarayıcılarını puanlar.
Kaynak: [OpenAI tarayıcıları](https://platform.openai.com/docs/bots)

---

Gözümüzden kaçan bir efsane ya da değişen bir kaynak mı buldunuz?
[Bir issue açın](https://github.com/irodevltd/seo-criteria/issues). [CC BY 4.0](LICENSE) lisansıyla.
