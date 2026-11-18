[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md) | **Türkçe**

# Kafenizdeki bilgisayarlarla kazanç sağlayın

Kinesis, kafenizdeki bilgisayarların ekran kartlarını, işlem gücüne ihtiyacı olanlara kiralar; ama yalnızca o bilgisayarda müşteri yokken. Bu saatler için siz kazanırsınız. Müşteri oturduğu anda iş durur ve bilgisayar tamamen müşterinin olur. Bunu her bilgisayarda yapan programın adı **Spark**.

Bilgisayarlarınızın ne kadar kazanabileceğini merak ediyor musunuz? [GPU kazanç hesaplayıcısını](https://kinesis.network/grid/join/gpu-calculator) deneyin.

Bu rehberle kurulumu bütün kafe için tek seferde yaparsınız. Bir kez yapmanız yeterli.

## Başlamadan önce

* Yaklaşık 30 dakikanızı ayırın. Üzerinde çalışacağınız bilgisayarın internet bağlantısı olduğundan emin olun.
* Windows imajları açma, düzenleme, kaydetme ve sistemdeki bilgisayarlara dağıtma yetkiniz olduğundan emin olun.
* Bilgisayarlarınızın sunucudan, ortak bir Windows imajıyla açıldığından emin olun (CCBoot gibi disksiz bir sistem). Bilgisayarlarınızın kendi diski varsa 4. adımdaki kurulum dosyasını her bilgisayarda çalıştırıp **Kendi diski olan bir bilgisayar** altındaki **Bu bilgisayarı kur**'a tıklamanız yeterli.
* Kasa bilgisayarınızda desteklenen bir kafe yazılımı olduğundan emin olun: [aşağıdaki listeye](#desteklenen-kafe-yazılımları) bakın.
* Disksiz sisteminiz LingWo/NetKafem CCBoot değilse (örneğin orijinal CCBoot), imajda çalışan bir NVIDIA sürücüsü olduğundan emin olun: Spark imajın sürücüsünü kullanır ve orada hiçbir zaman sürücü kurmaz. Ekran kartı bu sürücünün kapsamadığı bir bilgisayar ekran kartı olmadan çalışır ve Kinesis bunu `DRV_IMAGE_NO_DRIVER` olarak görür.

## Adım adım

1. **Kinesis hesabınızı açın.** [portal.kinesis.network/signup](https://portal.kinesis.network/signup) adresine gidin ve kafenin kendi e-postasıyla kaydolun. Bu site sizin Kinesis hesabınızdır; bilgisayarlarınızı ve kazancınızı burada görürsünüz. Site İngilizcedir. Menüde **Provide**'a (sağlayıcı bölümü) tıklayın, şartları okuyun, kutuyu işaretleyin ve **Agree & start providing**'e tıklayın.
2. **Kafe yazılımınızı ayarlayın.** [Aşağıdaki listeden](#desteklenen-kafe-yazılımları) kendi yazılımınızın sayfasını izleyin. CafePlus'ta kasa bilgisayarında iki satır eklersiniz; böylece yazılım, müşteri oturduğunda ve kalktığında Spark'a haber verir. PanCafe'de eklenecek bir şey yoktur: Spark her bilgisayarda PanCafe'nin kilit ekranını kendisi görür (ilk kafelerde doğrulanıyor).
3. **İmajı düzenlemeye açın.** Bir bilgisayarı disksiz sisteminizin düzenleme modunda, yazma koruması kapalı olarak açın (CCBoot'ta **Super Client** olarak açın; diğer disksiz sistemlerde de başka adla aynı mod vardır). Windows'a giriş yapın. Bundan sonraki her şey bu bilgisayarda yapılır.
4. **Kurulum dosyasını indirip çalıştırın.** [Son sürüm sayfasını](https://github.com/kinesis-network/kinesis-spark-releases/releases/latest) açın, `spark-ui_windows_x64_v….exe` dosyasını indirip çalıştırın. (Aynı dosya Kinesis hesabınızda da var: **Provide** > **Fleet** > **Add machines** > **Windows / WSL** > **Download Dynamo Spark**.) Sonda **Launch Dynamo** işaretli kalsın.
   Görmeniz gereken: Spark penceresi açılır.
5. **Disksiz kurulumu seçin.** Spark'ın ilk ekranı bu bilgisayarın türünü sorar; ekran ilk açılışta İngilizcedir, yanındaki **TR** düğmesiyle Türkçeye geçebilirsiniz. **Disksiz bir bilgisayar (CCBoot)** altındaki **Disksiz bilgisayarı kur**'a tıklayın. (CCBoot'ta Spark bu sayfayı kendisi de açabilir.) Sayfayı okuyun, **Kafe kurulumuna devam et**'e tıklayın ve Windows'un sorusuna evet deyin. Sonra her ekranda çıkan düğmeye tıklayın. Windows yeniden başlatmak isterse sorun yok: Spark kaldığı yerden açılır.
   Görmeniz gereken: **Kurulum** yazan kafe kurulumu. (Bu imajda Spark zaten varsa **Güncelleme** yazar.)
6. **Hesabınızı bağlayın.** **Kinesis'e bağlan** ekranında **Portal üzerinden bağlan**'a tıklayın. Tarayıcıda Kinesis hesabınız açılır: giriş yapın ve **Authorize for this image**'a (bu imaja izin ver) tıklayın.
   Görmeniz gereken: Spark'ta **Bağlandı**. Bu imajla açılan her bilgisayar bu hesapta görünecek.
   <details><summary>Bu bilgisayarda giriş yapamıyor musunuz?</summary>

   Bunun yerine bir kod kullanın. Başka bir bilgisayarda Kinesis hesabınıza girin ve **Provide** > **Fleet** > **Add machines** > **Windows / WSL** yolunu izleyin. **Setting up a diskless venue image (CCBoot and similar)? Get a 1-year venue token** yazan küçük bağlantıya, sonra **Create venue token**'a (kod oluştur), sonra kopyalama düğmesine tıklayın. Kodu bu bilgisayara aktarın. Spark'ta kodu Portal düğmesinin altındaki **Ya da token yapıştırın** alanına yapıştırın, onay anahtarını açın ve **Bu token'la devam et**'e tıklayın. Kod bir yıl geçerlidir.

   Kodu **kendi** hesabınızda oluşturun, size yardım eden birinin hesabında değil: her bilgisayar kodun geldiği hesaba katılır ve kazanç o hesaba gider. İmajı kaydettikten sonra o sayfada asla **Regenerate**'e basmayın: henüz katılmamış bilgisayarlar artık katılamaz.
   </details>
7. **Bitirip kaydedin.** Kalan ekranları geçin. Son ekranda **Bitir**'e tıklayın. Spark **Kurulum tamamlandı** dediğinde imajı disksiz sisteminizde her zamanki gibi kaydedin (CCBoot: bu bilgisayarın imajını Super Client olarak kaydedin) ve yazma korumasını yeniden açın.
8. **Çalıştığını kontrol edin.** Bir kafe bilgisayarını her zamanki gibi açın. Birkaç dakika içinde Kinesis hesabınızda **Provide** > **Fleet** altında görünür. Kasadan o bilgisayara müşteri oturumu açın: Spark yaklaşık 20 saniyede durur. Yeniden kilitleyin: Spark yaklaşık bir dakikada işe döner.

Bu kadar. İleride güncellemek için 3. ve 4. adımları tekrarlayın: Spark kendiliğinden **Bu kafe imajını güncelle** ekranıyla açılır ve her bilgisayar hesabınızdaki yerini korur.

## Desteklenen kafe yazılımları

<!-- Bakımcılar için: yeni bir kafe yazılımı eklemek için buraya bir satır ekleyin (aynı satırı README.md'ye de),
     ve hooks/cafeplus.md örneğindeki gibi hooks/<yazılım>.md ile hooks/<yazılım>.tr.md yazın.
     Bu README'de başka bir şeyin değişmesi gerekmez. -->

| Kafe yazılımı | Kurulum sayfası |
|---|---|
| AKINSOFT CafePlus | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md) · [English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md) |
| PanCafe Pro | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/pancafe.tr.md) · [English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/pancafe.md) |

Başka bir kafe yazılımı mı kullanıyorsunuz? **support@kinesis.network** adresine yazın, ekleyelim.

## Günlük işleyiş ve imaj güncellemeleri

* Düzenleme (Super Client) açılışındaki oyun ve Windows güncellemeleri Spark'tan bir şey istemez: imajı düzenlerken Spark çalışmaz ve bilgisayar kaydetmez.
* İmajda Spark güncellemesinden ya da yeni bir NVIDIA sürücüsünden sonra: düzenleme açılışında Spark penceresini açın, **Bitir**'e basın, sonra imajı kaydedin.
* **Spark'ı kafe yazılımınızın yasaklı programlar ya da "sonlandırılacak programlar" listesine asla eklemeyin**: kafe yazılımı her bilgisayarda Spark'ı durdurur.

## Bir sorun çıkarsa

<details><summary>Bir bilgisayar hesabınızda görünmüyor</summary>

O bilgisayarda Başlat'a `cmd` yazın, **Komut İstemi**'ne sağ tıklayın ve **Yönetici olarak çalıştır**'ı seçin. Şu iki satırı çalıştırın:

```
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" status
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue doctor
```

Çıkan yazıları ve bilgisayarın adını **support@kinesis.network** adresine gönderin.
</details>
