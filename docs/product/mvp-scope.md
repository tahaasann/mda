# Mobil Asistan MVP Kapsamı

**Durum:** Taslak — ilk kapsam gözden geçirmesi
**Ürün hedefi:** Kullanıcının doğal dille isteğini anlattığı, uygun iş akışını arka planda seçen ve gerektiğinde bağlı hizmetlerden kullanıcı izniyle yararlanan kişisel mobil asistan.

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

## Onaylanan ilk beş bağlı hizmet adayı

- Google Drive
- Google Calendar
- Gmail
- Todoist
- Notion

Bu adların MVP kapsamına girmesi, her hizmetin tüm yetkilerinin ilk sürümde isteneceği anlamına gelmez. Her bağlantı için ayrı kapsam/izin açıklaması hazırlanır ve yalnızca o yetenek için gerekli en dar izin istenir. Gmail için ilk sürümde gelen kutusu okuma ve e-posta gönderme yerine, kullanıcı bağlamı paylaştığında taslak oluşturma değerlendirilir. Takvim/görev ekleme gibi yazma işlemleri kullanıcı onayı gerektirir. Her hizmetin yayın ve inceleme gereksinimleri entegrasyon başlamadan kontrol edilir.

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
- UCP/ACP/MCP entegrasyonları; ticaret ve standart bağlantı desteği olgunlaştığında yeniden değerlendirilir.
- Rust tabanlı mobil uygulama veya yerel Rust bileşenleri.
- WhatsApp kişisel gelen kutusunu okuma; yalnızca kullanıcının açıkça paylaştığı içerik işlenebilir.
- Market/teslimat uygulamalarında doğrudan sepete ekleme veya satın alma; iş ortağı API erişimi doğrulanmadan vaat edilmez.
- Referans/ödül sistemi.
- Uzun süren arka plan araştırma işleri ve çoklu-agent orkestrasyonu.

## Açık kararlar — sonraki adımlar

- İlk sürümün beşinci dili (öneri: İspanyolca; kullanıcı onayı bekliyor).
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
