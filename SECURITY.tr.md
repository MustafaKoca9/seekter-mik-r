# Güvenlik

Seekter, kendi oturum açmış tarayıcını süren, gelen kutunu okuyan ve iletişim bilgilerini, maaş bantlarını ve CV'lerini diskte tutan bir ajandır. Buradaki ilginç güvenlik soruları bir sunucuyla ilgili değildir, çünkü sunucu yoktur.

## Güvenlik açığı bildirme

**Özel bir [güvenlik danışması aç](https://github.com/selfishprimate/seekter/security/advisories/new).** Lütfen aşağıdaki listedeki herhangi bir şey için genel bir issue açma.

Ne yaptığını, ne olduğunu ve gerçek bir kullanıcıya neye mal olacağını anlat. Çalışan bir örnek — bir ilan, bir form, bir diff — bir açıklamadan daha değerlidir. Birkaç gün içinde bir onay alacaksın; bu tek kişilik bir proje, bu yüzden düzeltme için lütfen sabırlı ol.

## Neler sayılır

**Bir iş ilanı veya form üzerinden prompt injection.** En önemlisi budur. Seekter gün boyu güvenilmeyen metin okur: açıklamalar, form etiketleri, yardım metinleri, onay sayfaları. Hepsini veri olarak, asla talimat olarak ele almak ve AI okuyuculara gizli yönergeler taşıyan ilanları takip etmek yerine bildirmek için tasarlanmıştır.

Bunu aşan bir metin şekli bulursan — bir ilanda veya formda ajanın ne yaptığını değiştiren, doldurmaması gereken bir alanı doldurmasına, bir şey göndermesine, bir bağlantıyı takip etmesine veya kullanıcının profilinin bir kısmını açığa çıkarmasına neden olan bir şey — bu bir hata raporu değil, bir güvenlik raporudur. Metni kelimesi kelimesine ekle.

**Özel verilerin genel repoya ulaşması için bir yol.** `profile/`, `applications/` ve `runs/` git tarafından yok sayılır ve `/seekter-git` ile CI leak scan, sahnelenen diff'i kimlik değerleri için kontrol eder. Bir ad, e-posta adresi, telefon numarası veya CV'nin yine de commit'lenmesi için bir yol bulursan — birini alıntılayan bir referans notu, yok sayılan yolların dışına yazan bir script, atlatılabilen bir tarama — bildir.

**Bir guardrail'i aşan herhangi bir şey.** Seekter asla bir CAPTCHA'yı çözmemeli veya atlamamalı, hesap oluşturmamalı, parola yazmamalı, kullanıcı için kullanım şartlarını kabul etmemeli, kullanıcı olarak mesaj veya e-posta göndermemeli, yorum veya maaş paylaşmamalı, bir şey için ödeme yapmamalı, LinkedIn Easy Apply'ı doldurmamalı veya kullanıcı opt-in yapmadıysa LinkedIn'i okumamalıdır. Bunlardan birini yaptırmak bir güvenlik açığıdır, tetiklemek alışılmadık bir ilan gerektirse bile.

**Görevin dışında işlem yapan herhangi bir şey.** Ajanın gerçek oturum açma bilgileri olan gerçek bir tarayıcı oturumu vardır. Onu önündeki başvuruyu doldurmanın ötesinde bir hesapta işlem yapmaya — ayarları değiştirme, posta silme, paylaşma, bir uygulamayı yetkilendirme — yönlendiren bir yol sayılır.

**Doğru olmayan bir şey göndermesini sağlamanın bir yolu.** Seekter profilinden doğrulayamadığı bir cevabı uydurmayı reddeder. Tahmin edilmiş bir doğum tarihi, maaş veya çalışma izni cevabının gönderilen bir forma girmesini sağlayan bir yol gerçek bir sorundur: o beyanı imzalayan kişi araç değil, kişidir.

## Neler sayılmaz

- **Formları doldurması.** Ürün budur.
- **Oturum açmış tarayıcı oturumunu kullanması.** Tasarım budur; alternatif kimlik bilgilerini bir sunucuya vermektir, bu proje bunu yapmaz.
- **Bir iş panosundaki hız limitleri, kullanım şartları veya bot algılama.** Seekter algılamadan kaçmaz ve bunu yapan değişiklikleri kabul etmez. Bir kaynak otomasyonu engelliyorsa cevap o kaynağı kullanmayı bırakmaktır ve bunun için bir dosya var: `reference/sources/dead-and-low-value.md`.
- **Makinen veya kilidi açık tarayıcın zaten saldırganda olan herhangi bir şey.** O noktada gelen kutun zaten onların olur.

## Tasarımın sana verdikleri

- **Sunucu yok, hesap yok, telemetri yok.** Her şey makinenizde çalışır. Profilin ve takipçin, sen commit'lemedikçe makineden çıkmaz ve `.gitignore` bunu kazara yapmaman için ayarlanmıştır.
- **Bağımlılık yok.** Python 3.9+ standart kütüphanesi ve `curl`. `pip install` edilecek bir şey yok, yani ele geçirilecek bir bağımlılık zinciri yok. Bunu böyle tut; paket ekleyen bir pull request çok iyi bir gerekçe gerektirir.
- **İzlenen hiçbir şey bir kişiyi varsaymaz.** Her kişisel değer git'in asla görmediği `profile/` içinden gelir. Bunun nasıl uygulandığı için `CONTRIBUTING.md`'ye bakın.
- **Ajan tahmin etmek yerine durur.** Doğru bir cevabı olmayan zorunlu bir soru, makul görünen bir cevap değil, **Needs you** tablosunda bir devir olur.

## Seekter kullanıyorsan

- `profile/`, `applications/` ve `runs/` klasörlerini sürüm kontrolünden uzak tut. Takipçinin sürümlenmesini istiyorsan, buradaki ignore satırlarını kaldırmak yerine ayrı bir özel repo kullan.
- `profile/profile.md` içine asla bir parola, API anahtarı veya güvenlik cevabı koyma. Seekter parola yazmaz ve onlara ihtiyacı yoktur.
- Daha fazla başvuru istemeden önce `applications/README.md` içindeki **Needs you** tablosunu oku. Ajanın karar vermeyi reddettiği her şey oraya gider.
- Ne gittiğini gözden geçir. Her başvuru dosyasında, gönderildiği haliyle serbest metin cevaplarını tutan bir `## Answers submitted` bölümü vardır.
