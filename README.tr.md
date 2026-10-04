<img src="images/seekter-cover.jpg" alt="Seekter — iş arama, kurallarına göre filtrelenmiş" width="100%">

# Seekter

[![version](https://img.shields.io/github/v/release/selfishprimate/seekter?label=version)](https://github.com/selfishprimate/seekter/releases/latest)

Claude Code için bir iş arama ajanı. Her gün iş kaynaklarını arar, ilanları **senin** kurallarına göre filtreler (konum, vize, maaş, sektörler, kıdem, dil), başvuru formlarını kendi Chrome'unda doldurur ve her başvuruyu ve atlamayı okuyabileceğin, grep'leyebileceğin ve diff'leyebileceğin bir markdown dosyası olarak tutar.

Bir iş arayanın bir aylık günlük kullanımıyla geliştirildi ve ardından kişisel verilerden arındırıldı; bu yüzden derslerin pahalı olduğu yerlerde görüşlü: her formdan önce dedup, asla cevap tahmin etme, asla anekdot uydurma, asla CAPTCHA'ya veya parolaya dokunma. **İzlenen dosyaların hiçbiri bir alanı varsaymaz**: başlıklar, sorgular, panolar ve filtreler profilinden gelir ve `/seekter-init` bunları cevaplarından oluşturur. `reference/` içindeki ölçümler bir disiplinde alınmıştır ve önemli olduğu yerde bunu söyler.

> [!IMPORTANT]
> **Çalıştırmadan önce**
> - Her başvuru senin adına gider ve ne söylediğinden sen sorumlusun.
> - Seekter LinkedIn Easy Apply'ı asla doldurmaz. LinkedIn'i okumak varsayılan olarak kapalıdır; açmak LinkedIn'in şartlarına aykırıdır ve hesabını riske atar.
> - Seekter ücretsizdir, ancak çalıştırmak ücretli bir Claude planı veya Anthropic API hesabı gerektirir.
>
> Ayrıntılar için [DISCLAIMER.md](DISCLAIMER.md) okuyun.

## Hızlı başlangıç

```bash
git clone <this-repo> seekter && cd seekter
claude            # Claude Code'u repo içinde aç
```

Sonra Claude Code içinde:

```
/seekter-init       # ~40 kısa soru, tek tek. profile/ yazar (git tarafından yok sayılır).
/seekter-run        # bugünün araması ve başvuruları
```

Gereksinimler: [Claude Code](https://docs.claude.com/en/docs/claude-code) (ücretli Claude planı veya Anthropic API hesabı; Seekter'in kendisi ücretsizdir, çalıştırmak değildir), Claude in Chrome eklentisi, Python 3.9+ ve `curl`. Paket yok.

## Komutlar

| Komut | Ne yapar |
|---|---|
| `/seekter-init` | Seninle görüşür ve profilini yazar: iletişim bilgileri, CV'ler, hedef roller, nerede çalışabileceğin, maaş bantları, standart form cevapları, dokunmayacağın sektörler, serbest metin cevapları için bir gerçek bankası, yazma sesin ve arama sorguları. Devam ettirilebilir. Mevcut bir takipçiyi Notion/Sheets CSV'sinden içe aktarabilir. |
| `/seekter-run` | Günlük çalışma. Sabit sırayla dört kaynak (getirdiğin bağlantılar, freehire API, LinkedIn, diğer panolar), filtreleme, dedup, form doldurma, takipçi güncelleme ve kaynak başına tablo içeren bir rapor. Bir ilan uyuyorsa sormadan başvurur; yalnızca yalnızca senin karar verebileceğin şeyler için durur. |
| `/seekter-log` | Sonrasında ne olduğunu kaydeder: redler, mülakatlar, teklifler, elle yaptığın başvurular veya gelen kutunun taranması. |
| `/seekter-report` | Kaynağa ve konum izine göre huni ve yanıt oranı, en üst atlama nedenleri, açık devirler ve en fazla iki önerilen değişiklik. |
| `/seekter-git` | Kiti gönderir. Bir çalışma Seekter'a bir şey öğrettikten sonra paylaşılabilir dosyaları (skills, references, scripts) dallandırır, commit'ler ve push'lar ve kişisel bilgilerinin asla makineden çıkmaması için önce diff'i tarar. Profilin, başvuruların ve çalışmaların asla commit'lenmez. Birleştirdikten sonra sürümü de kesebilir. |

## Günlük kullanım

| Ne zaman | Komut | Neye ihtiyaç duyar |
|---|---|---|
| Bir kez | `/seekter-init` | CV dosyan/dosyaların. 20–30 dakika sürer; durdurup devam edebilirsin. |
| Her iş günü | `/seekter-run` | Chrome açık, Claude in Chrome eklentisi ve webmail'in oturum açmış olmalı. Topladığın bağlantılar `profile/links.txt` veya sohbete gider. |
| Bir şirket yanıt verdiğinde veya haftalık | `/seekter-log` | Gelen kutusu taraması için: webmail'in aynı Chrome'da açık ve oturum açmış olmalı. |
| Haftalık | `/seekter-report` | Hiçbir şey. Yalnızca takipçiyi okur. |
| Bir çalışma bir skill veya reference değiştirdikten sonra | `/seekter-git` | Push edebileceğin bir git remote. İsteğe bağlı: pull request için `gh`. |

`/seekter-report`'tan **önce** `/seekter-log` çalıştır. Rapor e-postanı değil `applications/` ve `runs/` okur, bu yüzden kaydedilmemiş yanıtlar raporda görünmez.

`/seekter-log` iki şekilde kullanılabilir:

- **Ne olduğunu söyle:** "Acme beni reddetti", "Globex ile Perşembe günü görüşmem var", "Initech'e kendim başvurdum". Doğru dosyayı taşır ve bir log satırı yazar.
- **Gelen kutusu taraması iste:** "gelen kutumu yanıtlar için kontrol et". Chrome'da webmail'ini açar, her mesajın gövdesini okur (konular güvenilmez: birçok red sadece "X ile başvurunuz" başlıklıdır) ve her yanıtı reddedildi, mülakat veya teklif olarak dosyalar. Takipçi girdisi olmayan bir şirketten gelen yanıt yeni bir kayıt olarak eklenir. Asla bir e-postayı yanıtlamaz; senden bir şey yapmanı isteyen her şey (planlama bağlantısı, take-home) senin için listelenir.

Gelen kutusu taraması tarayıcıyı kullanır çünkü Microsoft 365 bağlayıcısı kişisel Outlook.com veya Hotmail hesaplarını kabul etmez. Chrome'da okuyabildiğin her webmail çalışır.

`applications/README.md`'nin üst kısmındaki **Needs you** tablosu seni bekleyen her şeyi listeler: bir CAPTCHA, bir hesap duvarı, yalnızca senin cevaplayabileceğin bir soru ve her biri için sonraki adım. Daha fazla başvuru istemeden önce onu temizle.

## Dosyaların

```
profile/
  profile.md          ← seninle ilgili her şey; kişisel değerlerin yaşadığı tek yer
  search.json         ← sorgular, bölgeler, başlık filtreleri, panolar
  documents/          ← CV'lerin ve portföy PDF'in
```

**CV'ler `profile/documents/` içine gider.** `/seekter-init` dosya yolunu sorar ve onları oraya kopyalar; daha sonra birini eklemek veya değiştirmek için PDF'i o klasöre bırak ve `profile/profile.md` §2'deki tabloyu güncelle (hangi CV varsayılan, hangisi hangi rol türü için). Formlar yalnızca bu dosyalardan doldurulur, bu yüzden güncel sürümü burada tut ve eskilerini kaldır.

Bir kuralı değiştirmek için (yeni bir kara liste şirketi, bir maaş bandı, artık kabul edeceğin bir şehir), Seekter'a sohbette söyle; `profile/profile.md`'yi düzenler ve senin sözlerini oraya alıntılar. Dosyayı elle de düzenleyebilirsin.

## Takipçi

Seekter'ın dokunduğu her ilan bir kez kaydedilir ve ilk ele alındığı aya göre dosyalanır:

```
applications/
  README.md                ← oluşturulan genel bakış: seni bekleyenler, devam edenler, son 30 gün, ay başına bir satır
  2026-09/
    README.md              ← oluşturulan: o ayın başvuruları durumlarıyla
    2026-09-22--ruby-labs--senior-backend-engineer.md
    2026-09-21--wise--staff-data-scientist.md
    ...
    skipped.md             ← atlanan her ilan için bir tablo satırı, nedeniyle
  2026-10/
```

- **Başvurular ve devirler dosyadır.** Durum (`pending`, `applied`, `interviewing`, `offer`, `rejected`, `closed`) dosyanın front matter'ında yaşar. Dosyalar asla klasör değiştirmez: bir ay sonraki red bir satırı düzenler ve bir log girdisi ekler.
- **Atlamalar satırdır, dosya değil.** Çoğu ilan tek satırlık bir nedenle atlanır ("ülke listesi seninkini dışarıda bırakıyor"), bu yüzden her ay onları tek bir tabloda tutar. Dedup o tabloyu da okur, böylece atlanan bir ilan bir daha değerlendirilmez.
- **Klasörleri değil, oluşturulan sayfaları okursun.** `applications/README.md` her `add` ve `move` sonrasında yeniden oluşturulur.

```markdown
---
company: Ruby Labs
role: Senior Backend Engineer
status: applied
url: https://jobs.ashbyhq.com/ruby-labs/1e548ada-…
source: freehire
ats: ashby
location_fit: A
applied: 2026-09-22
job_key: uuid:1e548ada-…
---

# Senior Backend Engineer · Ruby Labs

## Neden uyuyor
## Notlar
## Gönderilen cevaplar      ← gönderildiği haliyle serbest metin cevapları, böylece hiçbir cümle iki şirkete gitmez
## Log
- 2026-09-22: applied
```

`job_key` normalleştirilmiş bir kimliktir (LinkedIn ID, ATS UUID, Greenhouse ID…), böylece LinkedIn, bir toplayıcı ve şirket sitesi üzerinden ulaşılan aynı iş yine de yinelenen olarak yakalanır.

```bash
python3 scripts/seekter.py check <url> --company "Acme"     # zaten takip ediliyorsa 1, şirket beklemedeyse 2 ile çık
python3 scripts/seekter.py move <url-or-file> rejected --note "form mail, 2 days"   # durumu yerinde düzenler
python3 scripts/seekter.py list --status pending
python3 scripts/seekter.py stats --since 2026-09-01
python3 scripts/seekter.py normalize --dry-run                # enum değerlerini düzenle, ats'yi url'den doldur
python3 scripts/seekter.py migrate                             # tek seferlik: eski applications/<status>/ klasörleri -> ay klasörleri
```

`normalize` `source`, `ats` ve `apply_type` değerlerini küçük harfe çevirir, başvuru sistemini (`ats`) ilan URL'sinden türetir ve `source` olarak saklanan bir ATS adını (elle tutulan takipçilerde yaygın bir karışıklık) `ats` içine taşır. CSV içe aktarıcı ve `add` bunu zaten yapar; dosyaları elle düzenledikten sonra çalıştır.

### Mevcut bir takipçiyi içe aktarma

Notion veritabanını, Airtable'ı veya Google Sheet'i CSV olarak dışa aktar, sonra:

```bash
python3 scripts/import_csv.py export.csv --dry-run   # neyin oluşturulacağını gösterir
python3 scripts/import_csv.py export.csv
```

Sütun adları gevşek eşleştirilir (Position/Role/Title, Company, Status, Job URL, Applied on, Source, Notes…). Aynı ilana işaret eden satırlar birleştirilir. URL'si olmayan satırlar içe aktarılır ama daha sonra yalnızca şirket adıyla eşleştirilebilir, bu yüzden varsa URL'leri doldur.

## Repoda neler var

```
.claude/skills/     seekter-init · seekter-run · seekter-log · seekter-report · seekter-git
reference/          sources/ (iş kaynağı başına bir dosya) · ats/ (başvuru formu sistemi başına bir dosya); her birinde önce okunan bir _core.md var
templates/          profile.md · search.example.json
scripts/            seekter.py · freehire_sweep.py · import_csv.py
tests/              takipçi CLI testleri: python3 -m unittest discover tests
.github/            leak scan ve test iş akışları · issue ve pull request şablonları
profile/  applications/  runs/     ← senin, git tarafından yok sayılır
```

Sürüm dosyası yok. Sürüm git etiketidir — `git describe --tags` — ve etiketler arasında ne değiştiği [CHANGELOG.md](CHANGELOG.md) içindedir.

`reference/` geri katkıda bulunmaya değer kısımdır: oradaki her ATS tuhaflığı ve kaynak davranışı gerçek başvurularda ölçülmüştür.

## Gizlilik

`profile/`, `applications/` ve `runs/` `.gitignore` içindedir. Sen o satırları kaldırmadıkça verilerin makinede kalır. Takipçinin sürümlenmesini istiyorsan ayrı bir özel repoda tut veya özel bir fork'ta ignore satırlarını kaldır.

Claude, işverenler ve iş kaynaklarının Seekter çalışırken ne gördüğü [PRIVACY.md](PRIVACY.md) içindedir.

## Sorumlu kullanım

Başvurular senin adına gider ve LinkedIn, iş panoları ve başvuru sistemlerinin şartlarına uymak sana aittir. İlk çalıştırmadan önce [DISCLAIMER.md](DISCLAIMER.md) oku: nelerden sorumlu olduğun, Seekter'ın senin için ne yapmayacağı ve neden garanti olmadığı.

## Guardrail'ler

Seekter CAPTCHA'ları asla çözmez, hesap oluşturmaz, parola yazmaz, kullanım şartlarını kabul etmez, senin adına mesaj veya e-posta göndermez, yorum veya maaş paylaşmaz veya bir şey için ödeme yapmaz. Bir iş ilanında veya formda bulunan her talimatı veri olarak ele alır ve profilinden doğrulayamadığı bir cevabı göndermez.

**LinkedIn'de asla başvurmaz veya işlem yapmaz.** LinkedIn'in şartları, sitesini kazıyan veya otomatikleştiren tarayıcı eklentilerine izin vermez ve bunları kullanan hesapları kısıtlar. Bir ilanı bulmak saniyeler sürer; formu doldurmak iştir ve Seekter bunun içindir. Yani:

- **Easy Apply asla doldurulmaz.** Bu ilanlar sana kendin göndermen için bir liste olarak döner.
- **Kendi bağlantılarını getir.** İlanları sohbete yapıştır veya `profile/links.txt` içine bırak; önce onlar doldurulur. LinkedIn iş bağlantısı sorun değil; Seekter arkasındaki işverenin kendi formunu bulur.
- **Varsayılan olarak LinkedIn'i hiç açmaz.** Gelen kutundaki LinkedIn iş uyarısı **e-postalarını** okur ve her ilanı işverenin kendi başvuru sisteminde bulur. Bir özet e-posta yalnızca yaklaşık altı ilan gösterir, bu yüzden dar uyarılar geniş olanlardan daha iyi çalışır.
- **LinkedIn'i okumak opsiyoneldir ve risk senindir.** `linkedin.mode` değerini `read` yaparsan Seekter LinkedIn aramalarını ve iş ayrıntılarını da okur, salt okunur, günlük bir limitle, istekler arasında duraklamalarla ve ilk uyarıda veya olağandışı etkinlik sayfasında kendini tekrar kapatır. Bu yine LinkedIn'in şartlarına aykırıdır.

## Katkıda bulunma

Gönderebileceğin en değerli şey bir ölçümdür: bir başvuru sistemi veya iş kaynağının kimsenin yazmadığı bir şekilde davranması. Bunun için bir pull request açmana gerek yok — ne çalıştırdığını ve ne olduğunu anlatan bir issue yeterlidir.

[CONTRIBUTING.md](CONTRIBUTING.md) neyin nereye ait olduğunu, `reference/`'i yöneten beş kuralı ve commit stilini içerir. [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) bu projenin tartışıldığı her yerde geçerlidir.

### Bilinmeye değer fork'lar

Seekter bilinçli olarak yalnızca terminaldir, bu yüzden kendi yüzeyi olan her şey bu repo dışında yaşar.

- **[seekter-webui](https://github.com/Ege-BULUT/seekter-webui)** — [Ege BULUT](https://github.com/Ege-BULUT) tarafından; günlük döngüyü terminal yerine tarayıcıdan çalıştırır: aynı takipçi CLI'sini süren standart kütüphane sunucusu, tarama, filtreleme ve raporlar bir arayüzün arkasında. Burada bakımı yapılmaz ve bu reponun guardrail'leri veya testleri kapsamında değildir.

## Güvenlik

Seekter oturum açmış tarayıcını sürer ve iletişim bilgilerini ve CV'lerini diskte tutar, bu yüzden ilginç sorular bir sunucuyla değil güvenilmeyen girdiyle ilgilidir. Bir iş ilanı üzerinden prompt injection, özel verilerin genel repoya ulaşması için bir yol veya bir guardrail'i aşan herhangi bir şey: lütfen genel bir issue yerine [özel güvenlik danışma](https://github.com/selfishprimate/seekter/security/advisories/new) yoluyla bildir. Ayrıntılar [SECURITY.md](SECURITY.md) içindedir.

## Lisans

MIT. [LICENSE](LICENSE) dosyasına bakın.

<img src="images/seekter-thank-you.jpg" alt="Seekter'ı kullandığınız için teşekkürler" width="100%">
