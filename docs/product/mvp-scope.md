# Mobil Asistan MVP Kapsamı

**Durum:** Kararlar kaydediliyor — MVP kapsamı
**Ürün hedefi:** Kullanıcının doğal dille isteğini anlattığı, uygun iş akışını arka planda seçen ve gerektiğinde bağlı hizmetlerden kullanıcı izniyle yararlanan kişisel mobil asistan.

**İlk sürüm dilleri:** İngilizce, Fransızca, Almanca, Türkçe ve İspanyolca.

## MVP'nin başarı ölçütü

Yeni bir Android kullanıcısı, kayıt öncesinde ürünün altı ana yeteneğini örneklerle anlayabilmeli; Google veya e-posta ile ücretsiz hesap oluşturduktan sonra yeni bir sohbet başlatabilmeli, önceki oturumlarına dönebilmeli ve asistanın doğru, anlaşılır, güvenli bir çıktı ürettiğini deneyimleyebilmelidir.

## Kullanıcı akışı

1. Kayıt öncesinde altı yeteneğin örnek giriş ve örnek çıktıları gösterilir.
2. Örnekler açıkça demo olarak etiketlenir; kullanıcının kişisel verileri işlenmiş izlenimi verilmez.
3. Gerçek kullanım öncesinde Google ile veya e-posta/şifre ile ücretsiz hesap oluşturulur ya da mevcut hesaba giriş yapılır.
4. Kullanıcı tek bir genel sohbet arayüzünde isteğini doğal dille yazar. İster yeni sohbet açar, ister önceki oturumuna devam eder.
5. Asistan uygun yeteneği/araçları arka planda seçer. İstek belirsizse işlem yapmadan önce kısa bir açıklama sorar.
6. Dış hizmette veri değiştiren veya üçüncü tarafa ileti gönderen işlemler kullanıcıya önceden gösterilir ve açık onay olmadan çalıştırılmaz.
7. Profilde kalan kullanım hakkı yüzde ve dönem yenilenme bilgisiyle gösterilir; kesir biçiminde sayaç gösterilmez.

## MVP yetenekleri

1. **Belge özeti ve eylemler:** Kullanıcının seçtiği görsel/PDF'den özet, önemli noktalar ve yapılacaklar çıkarma.
2. **Karşılaştırma:** Kullanıcının verdiği seçenekleri ortak ölçütlerle karşılaştırma; gerektiğinde web araştırmasını kaynaklarıyla sunma.
3. **Plan ve checklist:** Kullanıcının hedefi ve tercihleri için adımlı plan/görev listesi oluşturma.
4. **Mesaj taslağı:** Bağlam ve istenen tona göre gönderilmeye hazır taslak hazırlama; MVP'de harici uygulamaya otomatik gönderim yok.
5. **Ses notundan görev:** Ses girdisini yazıya çevirme ve görev/eylem maddelerine dönüştürme. Cihazda yerel tanıma desteklenmiyorsa bulut işleme ancak açık kullanıcı onayıyla kullanılabilir.
6. **Buzdolabı/kiler fotoğrafından tarif:** Fotoğrafta seçilebilen malzemelerden tarif, tahmini hazırlama süresi ve eksik malzeme listesi üretme. Belirsiz tanıma kesin bilgi gibi sunulmaz.

## Bağlı uygulamalar ve MCP kararı

Bağlı uygulama entegrasyonları için **MCP-first** yaklaşımı seçildi: mobil istemci doğrudan üçüncü taraf servis API'lerine bağlanmaz. Asistan sunucusu, yalnızca izin verilen MCP sunucularına bağlanır; kullanıcı bağlantıları ve OAuth yetkileri hizmet bazında yönetilir.

MCP kullanımı tek başına güvenlik garantisi değildir. Her entegrasyonda kimlik doğrulama, en az yetki, kullanıcı başına token izolasyonu, hassas işlem onayı, iptal/bağlantıyı kesme ve prompt injection savunmaları ayrıca uygulanır. Modelin veya MCP aracının harici sistemde yan etki oluşturduğu işlemler kullanıcıya önceden gösterilir ve açık onay alınır.

Onaylanan ilk beş bağlı hizmet adayı:

- Google Drive
- Google Calendar
- Gmail
- Todoist
- Notion

MCP sunucusunun resmî olması yeterli yayın onayı sayılmaz. Her sağlayıcı için yayın durumu, kullanım koşulları, OAuth kapsamları, kullanıcı başına yetkilendirme, veri işleme ve iptal akışı entegrasyon öncesi doğrulanır.

| Hizmet | MVP yaklaşımı | Yayın kapısı |
| --- | --- | --- |
| Todoist | Resmî hosted MCP sunucusunu prototiple ve entegrasyon adayı olarak değerlendir. İlk ürün akışları yalnızca gerekli araçları sunmalı; MCP'nin geniş yetkileri nedeniyle erişim ve yan etkiler ayrıca sınırlandırılmalı. | OAuth/token akışı, araç listesi, yetki kapsamı, koşullar ve iptal davranışı doğrulanmalı. |
| Notion | Resmî Notion MCP bağlantısını prototiple ve entegrasyon adayı olarak değerlendir. | Bağlantının üçüncü taraf MCP istemcisi olarak ürünümüzde kullanılmasına ilişkin OAuth, izin, koşul ve veri akışları doğrulanmalı. |
| Gmail | Google'ın resmî Gmail MCP'si değerlendirme/prototip için incelenebilir. | Google Workspace MCP Developer Preview olarak işaretli. Google, preview özelliklerinin GA'dan önce herkese açık uygulamalara dahil edilemeyebileceğini belirtiyor. GA ve yayın koşulları netleşmeden halka açık MVP'de kullanılamaz. |
| Google Drive | Google'ın resmî Workspace MCP'si değerlendirme/prototip için incelenebilir. | Gmail ile aynı Developer Preview ve halka açık yayın kapısı geçerli. |
| Google Calendar | Google'ın resmî Workspace MCP'si değerlendirme/prototip için incelenebilir. | Gmail ile aynı Developer Preview ve halka açık yayın kapısı geçerli. |

Google Workspace MCP'nin preview koşulları nedeniyle ilk halka açık sürümde beş uygulamanın tamamını sunacağımız varsayılmamalı. Bir entegrasyon bu yayın kapısını geçmezse MCP-first kararını koruyarak o bağlantı ertelenir; doğrudan API'ye sessizce geçilmez. Sağlayıcı MCP'si olgunlaştığında güvenlik ve ürün değerlendirmesi yenilenir.

Kaynaklar: [Google Workspace MCP kurulumu](https://developers.google.com/workspace/guides/configure-mcp-servers), [Google Workspace Developer Preview koşulları](https://developers.google.com/workspace/preview), [Todoist geliştirici platformu](https://developer.todoist.com/), [Notion MCP](https://www.notion.com/help/notion-mcp).

## Güvenlik ve veri ilkeleri

- Model sağlayıcı anahtarları mobil uygulamaya konmaz; sunucu tarafında tutulur.
- Kota ve maliyet sınırları sunucu tarafında uygulanır; yeni hesap açmak veya uygulamayı yeniden kurmak kotayı sıfırlamaz.
- Veritabanı erişimleri kullanıcıya göre sınırlandırılır; bağlı hizmet token'ları güvenli sunucu saklamasında tutulur.
- OAuth izinleri en az yetki ilkesine göre seçilir; bağlantı kesme ve hesap silme akışı bulunur.
- Harici sistemlerde yan etki oluşturan eylemler kullanıcı onayına bağlıdır.
- Ham prompt, fotoğraf, ses ve bağlı uygulama içerikleri ürün analitiğine ve olağan hata loglarına yazılmaz.
- Saklama süresi ve ücretsiz/Premium eşitleme davranışı kullanıcıya açıklanır.

## MVP dışı veya sonradan karara bağlanacak kapsam

- iOS yayını (Android ilk sürümden sonra; hesap, giriş ve mağaza kuralları ayrıca doğrulanır).
- UCP/ACP ticaret entegrasyonları; bağlantı desteği olgunlaştığında yeniden değerlendirilir. Bağlı uygulamalarda MCP-first yaklaşımı seçilmiştir; her sağlayıcı için yayın uygunluğu ayrıca doğrulanır.
- Rust tabanlı mobil uygulama veya yerel Rust bileşenleri.
- WhatsApp kişisel gelen kutusunu okuma; yalnızca kullanıcının açıkça paylaştığı içerik işlenebilir.
- Market/teslimat uygulamalarında doğrudan sepete ekleme veya satın alma; iş ortağı API erişimi doğrulanmadan vaat edilmez.
- Referans/ödül sistemi.
- Uzun süren arka plan araştırma işleri ve çoklu-agent orkestrasyonu.

## Açık kararlar — sonraki adımlar

- Ücretsiz kota birimi, sıfırlanma dönemi ve Premium limitleri.
- Ücretli plan fiyatları, deneme süresi ve paywall'ın tam akıştaki yeri.
- Bağlı beş hizmetin her biri için ilk sürümde desteklenecek somut okuma/yazma işlemleri.
- Her yetenek için ham medya ve üretilen çıktıların saklama/silme varsayılanı.
- Model sağlayıcısı ve model kimliğinin canlı API'de kullanılabilirliği; sağlayıcı değişimine açık sunucu arayüzü.

## İlk yayına kabul ölçütleri

- Kayıt öncesi altı demo görüntülenebilir ve demo olduğu anlaşılır.
- Google ve e-posta/şifre hesap akışları çalışır; kullanıcı hesabını silebilir.
- Altı yetenek sohbetten doğal dille çağrılabilir; belirsiz isteklerde açıklama istenir.
- Yeni sohbet ve oturum geçmişi temel akışları çalışır.
- Harici yazma/gönderme eylemleri onaysız gerçekleşmez.
- Kota sunucu tarafında sınırlandırılır ve profilde yüzde ile yenilenme dönemi görünür.
- Uygulama gerçek Android cihazında temel akıştan geçer; ağ hatası ve izin reddi anlaşılır biçimde ele alınır.
- Gizlilik, saklama, izin ve silme davranışları kullanıcıya açıklanır.
