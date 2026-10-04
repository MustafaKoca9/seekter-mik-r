# Değişiklik Günlüğü

Sürüm git etiketidir; sürüm dosyası yoktur. Her sürüm ayrıca
[sürümler sayfasında](https://github.com/selfishprimate/seekter/releases) aynı metinle yer alır.

## v0.2.1 — 4 Ekim 2026

Bir hata düzeltme sürümü. Her iki düzeltme de takipçinin durdurması gereken bir şeyi geçirmesiyle ilgilidir ve ikisi de hata olarak görünmedi.

### Aynı şirkete ikinci bir başvuru sessizce reddedilebiliyordu

Greenhouse, bir işverenin bir adayın aynı departmana yaptığı sonraki başvuruları bir pencere içinde veya bir redden sonra otomatik reddetmesine izin verir. Reddedilen başvuru "blocked by auto reject rule" olarak işaretlenir ve aday yalnızca işveren e-postayı açtıysa bilgilendirilir. Seekter aynı şirketteki ikinci rolü yeni bir ilan olarak ele aldı ve iyi bir günde birkaç tane gönderebildi. 2 Ekim'de ölçüldü: bir şirkette iki rol ve bir başka şirkette ikinci bir rol aynı öğleden sonra gitti. İşveren bu kuralı kullanıyorsa ikincisi hiç okunmamış olabilir ve bir işe alım uzmanına göre filtreledikleri toplu başvuru gibi görünür.

`check` artık şirketi bekletiyor: pencerede orada zaten bir başvuru, bekleyen bir devir veya bir ret varsa ya da herhangi bir tarihte bir mülakat veya teklif varsa `HOLD` ile 2 çıkıyor. Çalışma bekletilen ilanı atlar, onu hangi önceki rolün ve tarihin beklettiğini söyler ve raporda kendi başlığı altında listeler ki üzerine gidebilesin. Bir çalışma aynı şirkette iki rol bulduğunda yalnızca daha iyi uyan gider. Kendi getirdiğin bir bağlantı senin kararın sayılır ve bir notla başvurulur. Pencere `profile/search.json` içindeki `same_company_days`, varsayılan 30 gün.

### `check` çıplak bir LinkedIn id'sini yeni olarak geçiriyordu

`check-many` çıplak bir sayıyı her zaman bir LinkedIn iş id'si olarak okudu. `check` okumadı: sayıyı olduğu gibi anahtarladı, hiçbir şeyle eşleştirmedi ve takipçide zaten olan bir iş için NEW yazdı. 0.2.0 çalışmaya uyarı-postası ilanlarını LinkedIn id'siyle dedup etmesini söylediğinden beri, o kontrol bir yineleneni geçirebilirdi. Her iki komut da artık sayıyı aynı şekilde okuyor.

### Ayrıca

- Indeed notlarındaki bir yerel dil arama terimi düz ASCII ile yazılmıştı, bu yüzden 0.2.0 dil taraması onu kaçırdı.

### Yükseltme

Geçirilecek bir şey yok. `profile/search.json` içinde `same_company_days` olmadan pencere 30 gündür; değiştirmek için anahtarı ekle. `profile/`, `applications/` ve `runs/` git tarafından yok sayılır ve dokunulmaz.

## v0.2.0 — 4 Ekim 2026

Seekter'ın LinkedIn'de ne yaptığını değiştiren sürüm. Şimdiye kadar Easy Apply formlarını doldurdu ve LinkedIn'i kendi iç API'si üzerinden aradı ve LinkedIn tam olarak bunun için hesapları kısıtlıyor. Kitteki hiçbir şey bunu söylemiyordu. Bu sürüm LinkedIn'de işlem yapmayı durduruyor, onu okumayı bilerek yaptığın bir seçim haline getiriyor ve ilk çalıştırmadan önce neyi üstlendiğini söylüyor.

### Seekter LinkedIn'i otomatikleştiriyordu ve LinkedIn bunun için hesapları kısıtlıyor

LinkedIn'in yasak yazılım hakkındaki yardım sayfası, "LinkedIn'in web sitesini kazıyan, görünümünü değiştiren veya etkinliği otomatikleştiren" tarayıcı eklentilerine izin vermez ve bunları kullanan hesapların kısıtlanma veya kapatılma riski taşıdığını söyler. Seekter tarayıcını bir eklenti aracılığıyla sürer. 0.1.x'te günlük bir çalışma Easy Apply'ı doldurdu, LinkedIn'in iç API'si üzerinden yaklaşık 40 arama yaptı ve bildirim akışını topladı, hepsi senin kendi hesabından. Günlük çalıştırıyorsan LinkedIn'in gördüğü şey buydu. Kullanıcı Sözleşmesi ikinci bir hesap gibi bariz yedek yolu da dışlar.

Artık:

- **Easy Apply hiçbir modda asla doldurulmaz** ve LinkedIn'de hiçbir işlem yapılmaz: kaydetme, takip etme, mesajlaşma veya uyarı düzenleme yok. Easy Apply ilanları sana raporda kendin göndermen için bir liste olarak döner.
- **Varsayılan olarak Seekter LinkedIn'i hiç açmaz** (`linkedin.mode: email`). Gelen kutundaki LinkedIn iş uyarısı e-postalarını okur ve her ilanı işverenin kendi başvuru sisteminde bulur. Bir özet e-posta eşleşmelerinin yalnızca yaklaşık altısını gösterir (4 Ekim'de ölçüldü: altı kartın üstünde "30+ new jobs"), bu yüzden dar uyarılar geniş olanlardan çok daha az kaybeder.
- **LinkedIn'i okumak opt-in'dir** (`linkedin.mode: read`) ve kurulum, bunun LinkedIn'in şartlarına aykırı olduğuna dair açık bir uyarıyla sorar. Salt okunurdur ve sınırlıdır: çalışma başına en fazla 15 arama ve 60 iş ayrıntısı, 3 saniye arayla, birer birer. Bir "too many requests" hatası, bir güvenlik kontrolü veya giriş yönlendirmesi ya da olağandışı etkinlik sayfası çalışma için durdurur ve modu tekrar `email`'e çevirir.

Maliyet hacimdir. 2 Ekim'de aramalar 352 ilan, uyarı akışı 63 buldu, bu yüzden `email` modu tek başına çok daha az bulur.

### Kendi bağlantıların önce gelir

Bir ilanı bulmak bir kişi için saniyeler sürer; formunu doldurmak iştir. Bağlantıları sohbete yapıştır veya `profile/links.txt` (git tarafından yok sayılır) içine bırak; diğer tüm kaynaklardan önce doldurulurlar. LinkedIn iş bağlantısı sorun değil: Seekter arkasındaki işverenin kendi formunu bulur ya da Easy Apply'sa sana geri verir.

### Kimse neyi üstlendiğini söylemiyordu

Seekter başvuruları senin adına gönderir, diğer siteleri onların şartları altında kullanır ve ücretli bir Claude planıyla çalışır. Bunların hiçbiri yazılı değildi ve "Seekter ücretsizdir" tüm hikaye gibi okunuyordu.

- `DISCLAIMER.md`: nelerden sorumlu olduğun, kimin şartlarına uyduğun, garanti yok, bağlantı yok ve Seekter ücretsiz ama çalıştırmak değil.
- `PRIVACY.md`: Seekter hiçbir şey toplamaz ve çalışırken verilerinin nereye gittiği: Anthropic, başvurduğun işverenler, iş kaynakları ve gelen kutun, salt okunur.
- `/seekter-init` artık bu noktaları kapsayan tek bir cümleyle açılıyor ve yalnızca bir evetle devam ediyor. README'de de aynı üç nokta Hızlı başlangıç'ın üstünde.

### Referanslar tek bir adayın dilini konuşuyordu

Kit tek bir kişinin iş araması sırasında yazıldı ve yirmi küsur referans dosyası o kişinin dilini ve ülkesini örnek olarak kullandı: çevrilmiş düğme etiketleri, yerel arama terimleri, iki şekilde yazılan bir şehir, bir ülke kodu. Başka bir yerdeki kullanıcı her satırın kendi kopyasına ihtiyaç duyardı. Her ders hâlâ orada, artık her dilde ve ülkede geçerli olacak şekilde yazılmış; bir yer gerektiğinde `<CITY>`, `<COUNTRY>` ve `+<code>` ile.

### Ayrıca

2 Ekim'de ölçülen on iki form sistemi tuzağı, aralarında:

- Ashby dolu bir alanı "Missing entry" olarak gösterebilir; onu ikinci bir şekilde doldurmak temizler ve ilk Submit yalnızca alanı blur edebilir.
- Lever her `urls[...]` alanını bir URL olarak doğrular, bu yüzden içine konan serbest metin gönderimi sessizce başarısız eder.
- Teamtailor'un zorunlu Address'i, bir script'in dolduramayacağı bir konum arama kutusu olabilir.
- CleverStaff CV'yi yükler ve sonra yine de formu reddeder, ta ki dosya kendi alanına bağlanana kadar.
- Oracle Cloud HCM ilk ekranında bir hesap oluşturur, bu yüzden sana devredilir.
- Google Forms bir yüklemeyle birlikte oturum açmış Google hesabının e-postasını kaydeder, bu profilinin belirttiği adres olmayabilir.

### Yükseltme

- Bir sonraki `/seekter-run` sana disclaimer'ı bir kez sorar. Bir hayır çalışmayı durdurur.
- Profilin `email` modunda başlar. LinkedIn iş uyarılarını **Email** teslimiyle oluştur, `profile/search.json` içindeki `linkedin.searches` satırı başına bir tane, geniş değil dar. LinkedIn aramalarını kendin okumaya devam etmek için `linkedin.mode` değerini `read` yap; Easy Apply her iki durumda da kapalı kalır.
- Başka geçirilecek bir şey yok. `profile/`, `applications/` ve `runs/` git tarafından yok sayılır ve dokunulmaz.

## v0.1.2 — 2 Ekim 2026

Bir hata düzeltme sürümü. Üç düzeltmeden ikisi kitin sana söylemeden yaptığı şeylerle ilgilidir: biri başvuruyu bir adım erken gönderdi, diğeri redleri açık başvuru gibi bıraktı.

### Tek sayfalık bir Easy Apply formunda "next" Submit'ti

Easy Apply sürücüsü modal içindeki son iptal olmayan düğmeyi alarak ilerler. Çok sayfalı bir formda bu Next veya Review'dur. Tek sayfalı bir formda bu **Submit**'tir ve sürücünün ikisini ayırt etme yolu yoktu.

2 Ekim'de ölçüldü: modal sayfa sayacı olmadan açıldı, ilk ilerleme başvuruyu gönderdi ve review adımı yoktu. Yanlış bir şey gitmedi, çünkü ilerlemeden önce iletişim sayfası kontrol edilir. Ama review adımı aynı zamanda önceden işaretli "follow this company" kutusunun işaretinin kaldırıldığı yerdir ve o opt-in açık kaldı. 0.1.1'de Easy Apply kullanıyorsan tek sayfalık başvurularının bir kısmı muhtemelen aynı şekilde gitmiştir.

Sürücü artık her ilerlemeden önce sayfa sayacını okuyor. Sayacı olmayan bir modal tek sayfadır, bu yüzden sonraki basış gönderir ve çalışma karar vermeden önce formun tamamını okur.

### Kara liste şirket adını hiç görmedi

Toplayıcı listesi ve profilinin kara listesi ikisi de şirket adları listesidir. Filtre onları ilanın başlığı, açıklaması ve başvuru host'u üzerinden çalıştırdı, ki bunlar şirketi taşımaz. 2 Ekim'de ölçüldü: skill'in kendi listesinde adı geçen bir toplayıcı her filtreden geçti ve ancak iş sayfası açıldığında yakalandı. Şirket artık filtrenin okuduğunun bir parçası. LinkedIn'de bunun için güvenilir kaynak detay yanıtındaki ilk `"name"`, çünkü `companyDetails` sık sık `?` olarak gelir.

### Bazı redler ret gibi okunmuyordu

`/seekter-log` redleri bir regex ile bulur. Bir rolün doldurulduğu veya kapatıldığı ifadeleri yoktu ve `not moving forward` vardı ama `unable to move forward` yoktu. 2 Ekim'de ölçüldü: bir ret her iki ifadeyi de kullandı ve hiçbir şeyle eşleşmedi. Bir kaçırma hata gibi görünmez. Hâlâ açık bir başvuru gibi görünür, bu yüzden satır süresiz `applied` kalır. Liste artık filled/closed ifadelerini ve `unable to move` / `unable to proceed`'i kapsıyor.

Aynı tarama Outlook'un `[role=option]` satırlarının dört gün kaybolduktan sonra tekrar çalıştığını buldu. Inbox referansı artık üç liste seçicisinin hepsini yoklamayı ve hangisi cevap veriyorsa onu kullanmayı söylüyor.

### Ayrıca

- `CHANGELOG.md` 0.1.1'den beri yeni. 0.1.1 zip'i onu içermiyordu, bu yüzden bu onu içeren ilk indirme. `/seekter-git` artık sürümleri de kapsıyor: bir pull request birleştirildikten sonra girdiyi yazıp sürümü yayımlayabilir.
- README yeni bir kapak görseliyle açılıyor. Eskiden işaret ettiği görsel silinmişti, bu yüzden ilk satır bozuktu.
- Indeed: onuncu ölçülen geçiş onuncu kez yeni bir şey döndürmedi.
- Jobicy: normalde cevap veren bir API'den sekiz etiket sıfır satır döndürdü.
- LinkedIn: aramalara karşı bildirimler, yedinci kez ölçüldü. 63 id'den 13'ü örtüştü.

### Yükseltme

Geçirilecek bir şey yok. Dosyaları değiştir ve `profile/`, `applications/` ve `runs/` klasörlerini tut; git tarafından yok sayılırlar ve dokunulmazlar.

## v0.1.1 — 1 Ekim 2026

Bir hata düzeltme sürümü. 0.1.0'daysan ve `/seekter-run` çalıştırıyorsan, beş kaynaktan biri senin için sessizce hiçbir şey yapmıyordu ve bu onu düzeltir.

### LinkedIn Easy Apply, LinkedIn'in İngilizce değilse hiç çalışmadı

Easy Apply sürücüsü İngilizce düğme adlarıyla eşleşiyordu: "Easy Apply", "Next", "Review", "Submit application". Başka bir arayüz diline ayarlanmış bir hesapta bu etiketler çevrilir ve her kontrol başarısız olur.

Sessizce başarısız olur, pahalı yapan da budur. Hata yoktur. Tespit yalnızca bir ilanın Easy Apply düğmesi olmadığını bildirir, ki bu tam olarak kapanmış bir ilan gibi okunur. 250 ilanlık bir taramada ölçüldü: Easy Apply katmanının tamamı atlandı, altmış aday açılmadı ve iki canlı ilan kapalı olarak kaydedildi. Çalışmanın kendi öncelik sırası o katmanı kesilecek son katman olarak adlandırır, çünkü yaklaşık altı çağrıya ve hiç yüklemeye mal olur.

Sürücü artık düğme metniyle hiç eşleşmiyor. Modal'ı başlığından bulur ve içindeki son iptal olmayan düğmeyi alır, bu her dilde çalışır.

Aynı zamanda dört Easy Apply mekaniği daha ölçüldü ve yazıldı: modal yalnızca bir JS MouseEvent dispatch'i ile ve başka hiçbir şeyle açılmaz; çalışma izni soruları her iki sırada gelebilir, bu yüzden konuma göre cevaplanmak yerine okunmaları gerekir; koordinat çerçevesi tek bir çalışma içinde iki ilan arasında değişebilir; ve e-posta alanı birden fazla adres tutabilen bir açılır menüdür.

### Skill'in vaat ettiği kuyruk artık gerçekten var

`/seekter-run` sana bir oturum kısa kalırsa "kuyruğun bir sonraki çalışmaya hayatta kaldığını" söylüyordu. Hiçbir şey onu yazmadı. 250 ilanı tarayan ve sekize başvuran bir çalışma yalnızca bir tarayıcı sekmesinde yaşayan 240 başvuru URL'sini çözmüştür ve bir sonraki oturum hiçbir şeyden başlar.

Çalışma artık raporundan önce `runs/<date>/queue-A.md` yazar, işlenmemiş ilan başına bir satır, çözülmüş başvuru URL'siyle ve dosyada A/B/C harfinin bir karar değil bir sıralama ipucu olduğunu söyler.

### Ayrıca

- Ashby: bir formun kendi ülke listesi, ilan başlığındaki konumun üstünde gelir. Dört ülke adlandıran bir başlık kapanmış bir kapı gibi görünür; formun seninkini sunması işverenin aksini söylemesidir.
- Indeed: dokuzuncu ölçülen geçiş, dokuzuncu kez yeni bir şey yok.
- LinkedIn: aramalara karşı bildirimler, altıncı kez ölçüldü. 44 id'den 7'si örtüştü. İki kanal hâlâ birbirinin yerini tutmuyor.

### Yükseltme

Geçirilecek bir şey yok. Dosyaları değiştir, `profile/`, `applications/` ve `runs/` klasörlerini tut; git tarafından yok sayılırlar ve dokunulmazlar.

## v0.1.0 — 30 Eylül 2026

İlk etiketli sürüm. Seekter bir aydır günlük kullanımdaydı; bu, bunun etiketsiz hareketli bir hedef olmayı bıraktığı noktadır.

- **12 belgelenmiş iş kaynağı**, artı ölçülüp çağrılara değmediği bulunanlar hakkında bir dosya.
- **24 belgelenmiş başvuru formu sistemi**, her biri gerçek doldurulmuş formlardan yazılmış, artı tek seferliklerden bir dosya.
- Yalnızca `scripts/seekter.py` üzerinden yazılan bir markdown takipçi, normalleştirilmiş bir `job_key` ile, böylece LinkedIn, bir toplayıcı ve şirketin kendi sitesi üzerinden ulaşılan aynı ilan yine tek olarak yakalanır.
- Takipçi CLI'si üzerinde **39 test**: `python3 -m unittest discover tests`.
- Bükülmeyen guardrail'ler: CAPTCHA yok, hesap oluşturma yok, parola yok, kullanım şartlarını kabul etme yok, senin adına mesaj gönderme yok ve profilinden doğrulayamadığı bir cevap yok.

0.1.0 olarak numaralandırıldı, 1.0.0 değil, çünkü yapı değişmek üzere: sırada bir Claude Code eklentisi var, bu skills'in yer değiştirmesi ve takipçi kökünün "bunu nereye klonladıysan orası" olmayı bırakması anlamına gelir. 1.0.0 bunun oturduğu sürümdür.