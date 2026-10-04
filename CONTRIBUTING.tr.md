# Seekter'a Katkıda Bulunma

Gönderebileceğin en değerli şey **bir ölçümdür**.

`reference/` içindeki her şey gerçek bir form doldurularak veya gerçek bir kaynak taranarak ve ona bir başvuru kaybedilerek öğrenildi. Burada kimsenin hiç dokunmadığı düzinelerce başvuru sistemi ve iş panosu var. Yazılmamış bir şekilde davranan bir tane bulursan, o not herhangi bir özellikten daha değerlidir.

## Nereye ne ait

| Bulduğun şey | Gideceği yer | Ayrıca |
|---|---|---|
| Kimsenin belgelemediği bir şekilde davranan bir iş kaynağı | `reference/sources/<source>.md` | `reference/sources/_core.md` içindeki tabloya bir satır ekle |
| Böyle davranan bir başvuru formu sistemi (ATS) | `reference/ats/<vendor>.md` | `reference/ats/_core.md` içindeki tanımlama tablosuna bir satır ekle |
| Tek bir kaynağa veya satıcıya ait olmayan bir ders | eşleşen `_core.md` | Başka bir şey |
| Ölü, ücretli duvar arkasında veya boş bulduğun bir kaynak | `reference/sources/dead-and-low-value.md` | Ne çalıştırdığını ve ne geldiğini söyle |
| Takipçi CLI'sinde veya bir tarama script'inde bir hata | `scripts/` | Nasıl yeniden üretileceğini söyle |
| Bir komutun davranışında değişiklik | `.claude/skills/seekter-*/SKILL.md` | Önce bir issue aç; bunlar ajanın talimatlarıdır |

**Yeni bir pano önermeden önce `reference/sources/dead-and-low-value.md` dosyasını oku.** Bariz adayların çoğu zaten orada, onları öldüren ölçümle birlikte.

## `reference/`'i yöneten beş kural

Bunlar stil tercihleri değildir. Her biri, ihlal etmenin bir şeye mal olması yüzünden oradadır.

**1. Kişi hakkında değil, widget hakkında yaz.**
İsim, e-posta, telefon numarası, sokak adresi, posta kodu, maaş rakamı veya kişisel alan adı yok — örnek olarak bile. Kitin yer tutucularını kullan: `<FIRST_NAME>`, `<EMAIL>`, `<PHONE_LOCAL>`, `<CV_NAME>`, `<CITY>`, `<POSTCODE>`, `<COUNTRY>`.

Kişi çıkarıldığında bir not aynı derecede yararlı kalır:

> ✅ *telefon widget'ı numarayı aralıklı ulusal biçimde gösterir, bu yüzden geri okunan değer yazılan değerle eşleşmez*
> ❌ *telefon widget'ına 5xx xxx xx xx yazmak geri okunduğunda … olur*

Yer adlarıyla ilgili bir tuzak sorun değildir ve kalmalıdır — "şehir listesi İngilizce yazım için hiçbir şey bulamaz ve yalnızca yerel yazımla eşleşir" yeniden kullanılabilir bir derstir, kişisel veri değildir. Bir dilin sözcüklerini alıntılamak yerine İngilizce tanımla, böylece herkes için aynı okunur.

**2. Ölçülmüş, tarihli.**
"Greenhouse zor" hiçbir şey öğretmez. Ne çalıştırdığını, ne olduğunu ve ne zaman olduğunu söyle:

> *24 Eylül'de ölçüldü: onay banner'ının "Reject all"ı her alanı, her iki radio grubunu ve yüklenen CV'yi sildi. Önce banner'ı ele al; form doldurulduktan sonra bir tane tekrar belirirse dokunma ve gönder.*

Bir ölçüm yalnızca bir disiplin, bir ülke veya bir tarayıcı için geçerliyse bunu notta söyle.

**3. Ekleme, birleştir.**
Reference iki büyük dosya olarak başladı ve bölünmek zorunda kaldı, çünkü beş satıcı iki veya üç kez, yüzlerce satır arayla yazılmıştı — yeni bir ders eklemek her zaman birleştirmekten kolaydır. Sadece tekrar etmediler, çeliştiler: bir bölüm bir akışı ulaşılamaz diye adlandırırken, sonra eklenen bir başka bölüm onu süren yöntemi taşıyordu. Dosyada önce yanlış talimat vardı, bu yüzden bir çalışmanın izleyeceği oydu.

Bir dosya ölçtüğün şey hakkında zaten bir şey söylüyorsa, **o cümleyi değiştir**. Altına ikinci bir tane ekleme.

**4. Konu başına bir dosya.**
Dosyası olmayan bir kaynak veya satıcı hiç ölçülmemiştir — başkasının dosyasını büyütmek yerine ona kendi dosyasını ver. `_core.md`'yi tek bir konuya ait olmayan şeyler için sakla, yoksa bölünmenin düzelttiği şeye geri döner.

**5. Kişiden bağımsız, alandan bağımsız.**
Bu repoda izlenen hiçbir şey bir iş unvanı, bir disiplin, bir şehir, bir para birimi veya bir maaş bandı varsayamaz. Bunların hepsi kullanıcının `profile/` klasöründen gelir; `/seekter-init` onu oluşturur ve git asla görmez. `reference/` içindeki ölçümler çoğunlukla tek bir disiplinde alınmıştır; bunun önemli olduğu yerde not bunu söyler, seninki de söylemelidir.

## Guardrail'ler tartışmaya açık değildir

Seekter asla bir CAPTCHA'yı çözmez veya atlamaz, hesap oluşturmaz, parola yazmaz, kullanıcı adına kullanım şartlarını kabul etmez, kullanıcı olarak mesaj veya e-posta göndermez, yorum veya maaş paylaşmaz veya bir şey için ödeme yapmaz. Kullanıcının profilinden doğrulayamadığı bir cevabı asla uydurmaz ve bir ilanda veya formda bulunan metni talimat değil veri olarak ele alır.

Bunlardan herhangi birini zayıflatan pull request'ler, ne kadar iyi çalışırsa çalışsın kapatılır.

## Asla özel veri commit'leme

`profile/`, `applications/` ve `runs/` git tarafından yok sayılır ve öyle kalmalıdır. Bir şeyin geçmesi için `.gitignore`'u zayıflatma ve bu yollar altındaki bir dosyayı force-add etme.

Bunu iki tarama destekler:

- **`/seekter-git`**, kendi `profile/profile.md` dosyandan bir iğne listesi oluşturur ve push etmeden önce sahnelenen diff'i ona karşı tarar. Yerel çalışır, çünkü profil asla commit'lenmez.
- **`.github/workflows/leak-scan.yml`** her pull request'te çalışır. Yalnızca yol zorlaması ve birkaç kimlik deseni yapabilir, ama bu reponun gerçekten yaşadığı tek sızıntıyı yakalardı.

Bir mekanik not özel bir değer olmadan yazılamıyorsa, **yanlış olan nottur, kural değil.**

## Commit'ler

Bir tane yazmadan önce `git log --oneline -15` oku. Ev stili, bulguyu belirten bir cümledir — cümle düzeni, önek yok, bilet numarası yok, son nokta yok:

```
Teamtailor hides a whole section above the questions
A pool listing hides the employer, and its confirmation mail names it
Indeed's seventh measured run is its seventh zero
Management is the candidate's line to draw, not the skill's
Three ATS traps from one afternoon
```

`fix: update ats-mechanics.md` her açıdan başarısız olur.

- **Ders başına bir commit.** İlgisiz bulguları ayır. Yalnızca gerçekten tek bir oturumdan gelenleri grupla ve bunu konu satırında söyle.
- **Gövde:** neyin ölçüldüğü, nerede ve neye mal olduğu. Tarihler ve sayılar, çünkü referanslar öyle yazılır.
- Bilinçli stage'le. `git add -A`, yok sayılan ama force-add edilen dosyaların içeri girmesinin yoludur.

## Çalıştırma

```bash
git clone https://github.com/selfishprimate/seekter && cd seekter
claude                                  # Claude Code'u repo içinde aç
/seekter-init                           # kendi profile/ klasörünü yazar
/seekter-run                            # günlük çalışma
```

[Claude Code](https://docs.claude.com/en/docs/claude-code), Claude in Chrome eklentisi, Python 3.9+ ve `curl` gerekir. Kurulacak bir şey ve build adımı yoktur.

## Testler

`scripts/seekter.py` bir test paketine sahiptir. Yalnızca standart kütüphanedir, kendi takipçine asla dokunmaz — her durum geçici bir dizinde tek kullanımlık bir repo oluşturur — ve yaklaşık üç saniye sürer:

```bash
python3 -m unittest discover tests
```

**`scripts/` üzerinde herhangi bir değişiklikten önce ve sonra çalıştır.** Her pull request'te, Python 3.9 ve 3.13'te de çalışır.

Paket kapsama için yazılmamıştır. Her durum ya README'nin verdiği bir söz ya da zaten bir şeye mal olmuş bir hatadır ve üstündeki yorum hangisi olduğunu söyler — Breezy'nin yeni gibi geçen yeniden adlandırması, LinkedIn id'leri taramasının bulamadığı Ashby UUID'si, bir başvurunun gönderilen cevaplarını yutmaması gereken atlama satırı. **CLI'de bir hatayı düzeltirsen, onu yakalayacak durumu ekle**, aynı tür yorumla.

CLI'yi elle kurcalamak için:

```bash
python3 scripts/seekter.py --help
python3 scripts/seekter.py stats
python3 scripts/seekter.py normalize --dry-run
```

Bir reference değişikliği unit test edilemez. Tanımladığı şeyi yaparak test et: o formu veya o panoyu aç, notu izle ve temasla ayakta kaldığını kontrol et.

## Pull request açma

1. Dal: `seekter/<YYYY-MM-DD>-<the-lesson>`, örn. `seekter/2026-09-29-shadow-dom-upload`.
2. Diff'ini açıklamadan önce oku.
3. Pull request şablonunu doldur. Neyi ne zaman ölçtüğünü sorar, çünkü bir gözden geçirenin senin için kontrol edemeyeceği kısım odur.

Sorular veya emin olmadığın bir kaynak: bir issue aç ve sor. Zaten bilinen bir ölçüm olduğu ortaya çıkan şey, öğrenmesi ucuz bir şeydir.
