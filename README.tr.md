[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md) | **Türkçe**

# Kafenizdeki bilgisayarlarla kazanç sağlayın

Kinesis, kafenizdeki bilgisayarların ekran kartlarını, işlem gücüne ihtiyacı olanlara kiralar; ama yalnızca o bilgisayarda müşteri yokken. Bu saatler için siz kazanırsınız. Müşteri oturduğu anda iş durur ve bilgisayar tamamen müşterinin olur. Bunu her bilgisayarda yapan programın adı **Spark**.

Bu rehberle kurulumu bütün kafe için tek seferde yaparsınız. Bir kez yapmanız yeterli.

## Başlamadan önce

- **Yaklaşık 30 dakika** ve üzerinde çalışacağınız bilgisayarda internet.
- **Bilgisayarlarınız sunucudan açılıyor olmalı** (CCBoot gibi "disksiz" bir sistem): bilgisayarların kendi Windows'u yoktur, hepsi sunucudaki tek bir ortak Windows kopyasıyla, yani **imajla** açılır. Bilgisayarlarınızın kendi diski varsa bu rehber size göre değil: 4. adımdaki kurulum dosyasını indirip her bilgisayarda çalıştırmanız yeterli.
- Kasa bilgisayarında **desteklenen bir kafe yazılımı**: [aşağıdaki listeye](#desteklenen-kafe-yazılımları) bakın.

## Adım adım

1. **Kinesis hesabınızı açın.** [portal.kinesis.network/signup](https://portal.kinesis.network/signup) adresine gidin ve kafenin kendi e-postasıyla kaydolun. Bu site sizin Kinesis hesabınızdır; bilgisayarlarınızı ve kazancınızı burada görürsünüz. Site İngilizcedir. Menüde **Provide**'a (sağlayıcı bölümü) tıklayın, şartları okuyun, kutuyu işaretleyin ve **Agree & start providing**'e tıklayın.
2. **Kafe yazılımınızı ayarlayın.** Kasa bilgisayarında, kafe yazılımınıza iki satır eklersiniz; böylece yazılım, müşteri oturduğunda ve kalktığında Spark'a haber verir. [Aşağıdaki listeden](#desteklenen-kafe-yazılımları) kendi yazılımınızın sayfasını izleyin.
3. **İmajı düzenlemeye açın.** Bir bilgisayarı disksiz sisteminizin düzenleme modunda, yazma koruması kapalı olarak açın (CCBoot'ta **Super Client** olarak açın; diğer disksiz sistemlerde de başka adla aynı mod vardır). Windows'a giriş yapın. Bundan sonraki her şey bu bilgisayarda yapılır.
4. **Kurulum dosyasını indirip çalıştırın.** [Son sürüm sayfasından](https://github.com/kinesis-network/kinesis-spark-releases/releases/latest) `spark-ui_windows_x64_v….exe` dosyasını indirip çalıştırın. Sonda **Launch Dynamo** işaretli kalsın.
   Görmeniz gereken: Spark penceresi açılır.
5. **Kafe kurulumunu seçin.** Spark'ın ilk ekranındaki küçük bağlantıya tıklayın. Bu bağlantı ilk açılışta İngilizcedir: **Setting up a diskless venue image (CCBoot...)? Click here**. Açılan sayfanın üstündeki **TR** düğmesiyle Türkçeye geçebilirsiniz. Sayfayı okuyun, **Kafe kurulumuna devam et**'e tıklayın ve Windows'un sorusuna evet deyin. Sonra her ekranda çıkan düğmeye tıklayın. Windows yeniden başlatmak isterse sorun yok: Spark kaldığı yerden açılır.
   Görmeniz gereken: **Kurulum** yazan kafe kurulumu. (Bu imajda Spark zaten varsa **Güncelleme** yazar.)
6. **Hesabınızı bağlayın.** **Kinesis'e bağlan** ekranında **Portal üzerinden bağlan**'a tıklayın. Tarayıcıda Kinesis hesabınız açılır: giriş yapın ve **Authorize for this image**'a (bu imaja izin ver) tıklayın.
   Görmeniz gereken: Spark'ta **Bağlandı**. Bu imajla açılan her bilgisayar bu hesapta görünecek.
   <details><summary>Bu bilgisayarda giriş yapamıyor musunuz?</summary>

   Bunun yerine bir kod kullanın. Başka bir bilgisayarda Kinesis hesabınıza girin ve **Provide** > **Fleet** > **Add machines** > **Windows / WSL** yolunu izleyin. **Setting up a diskless venue image (CCBoot and similar)? Get a 1-year venue token** yazan küçük bağlantıya, sonra **Create venue token**'a (kod oluştur), sonra kopyalama düğmesine tıklayın. Kodu bu bilgisayara aktarın. Spark'ta **Bunun yerine token yapıştır**'a tıklayın, kodu yapıştırın ve **Bu token'ı kullan**'a tıklayın. Kod bir yıl geçerlidir.

   Kodu **kendi** hesabınızda oluşturun, size yardım eden birinin hesabında değil: her bilgisayar kodun geldiği hesaba katılır ve kazanç o hesaba gider. İmajı kaydettikten sonra o sayfada asla **Regenerate**'e basmayın: henüz katılmamış bilgisayarlar artık katılamaz.
   </details>
7. **Hazırlayıp kaydedin.** Kalan ekranları geçin. Sonunda **Bu bilgisayarı imajın kaydı için hazırla**'ya tıklayın ve **Evet** deyin. Ardından 1 saat içinde, bu bilgisayarı başka bir şey için kullanmadan: kapatın, imajı disksiz sisteminizde her zamanki gibi kaydedin ve yazma korumasını yeniden açın.
8. **Çalıştığını kontrol edin.** Bir kafe bilgisayarını her zamanki gibi açın. Birkaç dakika içinde Kinesis hesabınızda **Provide** > **Fleet** altında görünür. Kasadan o bilgisayara müşteri oturumu açın: Spark yaklaşık 20 saniyede durur. Yeniden kilitleyin: Spark yaklaşık bir dakikada işe döner.

Bu kadar. İleride güncellemek için 3. ve 4. adımları tekrarlayın: Spark kendiliğinden **Bu kafe imajını güncelle** ekranıyla açılır ve her bilgisayar hesabınızdaki yerini korur.

## Desteklenen kafe yazılımları

<!-- Bakımcılar için: yeni bir kafe yazılımı eklemek için buraya bir satır ekleyin (aynı satırı README.md'ye de),
     ve hooks/cafeplus.md örneğindeki gibi hooks/<yazılım>.md ile hooks/<yazılım>.tr.md yazın.
     Bu README'de başka bir şeyin değişmesi gerekmez. -->

| Kafe yazılımı | Kurulum sayfası |
|---|---|
| AKINSOFT CafePlus | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md) · [English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md) |

Başka bir kafe yazılımı mı kullanıyorsunuz? **support@kinesis.network** adresine yazın, ekleyelim.

## Bir sorun çıkarsa

<details><summary>Bir bilgisayar hesabınızda görünmüyor</summary>

O bilgisayarda Başlat'a `cmd` yazın, **Komut İstemi**'ne sağ tıklayın ve **Yönetici olarak çalıştır**'ı seçin. Şu iki satırı çalıştırın:

```
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" status
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue doctor
```

Çıkan yazıları ve bilgisayarın adını **support@kinesis.network** adresine gönderin.
</details>

> Eski "Kinesis Spark disksiz kafe kiti" (bir PowerShell betiği) kullanımdan kaldırıldı. Yukarıdaki kurulum dosyasını kullanın.
