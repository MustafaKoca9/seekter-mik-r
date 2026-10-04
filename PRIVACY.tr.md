# Gizlilik

Seekter hiçbir şey toplamaz. Sunucusu, hesabı ve telemetrisi yoktur ve onu yapanlar verilerini asla görmez. Bu sayfa, kullanırken verilerinin nereye gittiğini söyler, böylece profiline ne koyacağına karar verebilirsin.

Bu sayfa bu repoyu, kiti kapsar. seekter.dev sitesi ayrıdır.

## Bilgisayarında kalanlar

`profile/` (bilgilerin, maaş bantların, CV'lerin, topladığın bağlantılar), `applications/` (gönderilen her cevap dahil takipçi) ve `runs/` (günlük raporlar). Git tarafından yok sayılırlar, yani sen bunu değiştirmedikçe bir repoya ulaşmazlar. Bu klasörleri silmek Seekter'ın verilerinin kopyasını siler.

## Seekter çalışırken nereye gider

- **Anthropic.** Seekter Claude Code içinde çalışır, bu yüzden Claude çalışırken okuduğu şeyler işlenmek üzere Anthropic'e gönderilir: profilin, CV metni, iş ilanları, form sayfaları ve gelen kutunda açtığı e-postalar. Bu, Claude planının veya API hesabının şartları ve gizlilik politikası kapsamında gerçekleşir ([Anthropic gizlilik politikası](https://www.anthropic.com/legal/privacy)).
- **Başvurduğun işverenler** ve kullandıkları başvuru sistemleri. Her başvuru, formun istediği bilgileri gönderir: genellikle adın, iletişim bilgilerin, CV'n ve cevapların. O andan itibaren o işverenin gizlilik politikası geçerlidir.
- **İş kaynakları.** Çalıştırdığı aramalar arama terimlerini o sitelere gönderir. LinkedIn `read` modunda LinkedIn bu istekleri oturum açmış oturumundan görür, tıpkı sen geziyormuşsun gibi.
- **Tarayıcın ve gelen kutun.** Seekter oturum açtığın tarayıcıda çalışır. Mevcut oturumlarını kullanır; bir parolayı asla görmez, saklamaz veya yazmaz. Webmail'inde yalnızca okur: başvuru yanıtları ve LinkedIn iş uyarısı e-postaları. Asla posta göndermez.

## Verilerinle yapmayacakları

- Onları genel bir repoya koymak. `/seekter-git` ve CI sızıntı taraması her commit'i adın, e-postan, telefon numaran ve diğer kimlik değerlerin için kontrol eder (`SECURITY.md`'ye bakın).
- Başvurular için profilinin belirttiğinden başka bir e-posta adresi kullanmak.
- Bir web sayfası, e-posta veya belgenin önerdiği herhangi bir adrese veya forma göndermek. Nereye gideceğine yalnızca sen karar verirsin.