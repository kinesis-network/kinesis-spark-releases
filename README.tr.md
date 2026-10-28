[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md) | **Türkçe**

# Dynamo Spark sürümleri

Dynamo Spark, bir Windows PC'nin boşta kaldığı sürede kazanç sağlamasını sağlar. Kurulum dosyası burada yayımlanır.

## Kurulum

1. Spark kurulum dosyasını **[son sürüm sayfasından](https://github.com/kinesis-network/kinesis-spark-releases/releases/latest)** indirin: `spark-ui_windows_x64_v….exe` dosyası.
2. Çalıştırın ve ekrandaki adımları izleyin.

## Disksiz imaj kullanan internet kafe (CCBoot ve benzerleri)

Spark **ortak imaja bir kez** kurulur; imajla açılan her PC onu çalıştırır.

### Gerekenler

- [ ] **Disksiz sistem.** Kafedeki PC'ler tek bir ortak Windows imajını sunucudan açar (**CCBoot** gibi bir disksiz açılış yazılımıyla). Normal bir PC'de yapılan her değişiklik yeniden başlatınca kaybolur; bu yüzden her değişiklik **bir kez, imajın üzerinde** yapılır: açılış yazılımının imaj düzenleme modunda (CCBoot'ta **Super Client**) açılmış ve yazma koruması kapatılmış bir PC'de. Ardından imaj kaydedilir ve her PC onu bir sonraki açılışında alır. Bu sayfada o PC'ye **imaj PC'si** diyoruz.
- [ ] İmaj PC'sinde baştan sona **internet**.
- [ ] Kafenin **kendi** Portal hesabından alınmış **1 yıllık kafe token'ı** (yardım eden kişinin hesabı değil): imajla açılan her PC, token'ın alındığı hesaba katılır. Token'ı kurulum sırasında Portal'dan otomatik olarak da alabilirsiniz (**Portal üzerinden bağlan**).
- [ ] [CafePlus ayarları](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md) için **kasa PC'sine erişim**.
- [ ] Her PC'de BIOS'ta **sanallaştırma açık** (SVM / VT-x).
- [ ] GPU'lu PC'lerde **NVIDIA sürücüsü disksiz sistemden gelir**; imaja ayrıca sürücü kurmayın.

### Kurulum adımları

1. **Kasa PC'si:** CafePlus'taki iki kutuyu bir kez ayarlayın: [AKINSOFT CafePlus](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md).
2. **İmaj PC'si:** imaj düzenleme modunda açın (CCBoot: Super Client), korumayı kapatın ve Windows'a giriş yapın.
3. Spark kurulum dosyasını (yukarıdaki) indirip çalıştırın. Sondaki **Launch Dynamo** seçeneğini işaretli bırakın.
4. Spark'ın ilk kurulum adımında küçük **Disksiz bir kafe imajı mı kuruyorsunuz (CCBoot...)? Buraya tıklayın** bağlantısına tıklayın, sayfayı okuyun, **Kafe kurulumuna devam et**'e tıklayın ve tek seferlik yönetici onayını verin.
5. Sihirbazı izleyin. Yeni bir imajda **Kurulum**, içinde zaten Spark olan bir imajda **Güncelleme** açılır. Yeniden başlatma isterse sorun yok: pencere kaldığı yerden açılır.
6. **Token**, **Kinesis'e bağlan** adımında: **Portal üzerinden bağlan**'a tıklayıp kafenin kendi hesabıyla giriş yapın ya da **Bunun yerine token yapıştır**'ı seçin. Token'ı Portal'dan almak için: **Provide** > **Fleet** > **Add machines** > **Windows / WSL** > küçük **Setting up a diskless venue image (CCBoot and similar)? Get a 1-year venue token** bağlantısı > **Create venue token** > kopyalama düğmesi.
   İmaj kaydedildikten sonra o sayfada asla **Regenerate**'e basmayın: henüz katılmamış PC'ler artık katılamaz.
7. **Kaydetmeye hazır:** **Bu bilgisayarı imajın kaydı için hazırla**'ya tıklayın ve **Evet** deyin.
8. 1 saat içinde, PC'yi başka bir iş için kullanmadan: kapatın, imajı açılış yazılımında kaydedin (CCBoot'ta her zamanki gibi) ve yazma korumasını yeniden açın.

İmajı daha sonra güncellemek için (yeni Spark veya yeni token): 2. ve 3. adımları tekrarlayın; Spark kendiliğinden **Bu kafe imajını güncelle** ekranıyla açılır. PC'ler Portal'daki yerlerini korur.

### Kaydettikten sonra: bir PC'yi kontrol edin

Kaydedilen imajla bir kafe PC'sini açın. Birkaç dakika içinde Portal'da **Provide** > **Fleet** altında görünür. Kasadan kiralayın: Spark yaklaşık 20 saniyede durur; kilitleyin: yaklaşık bir dakikada yeniden çalışır.

Görünmezse o PC'de Başlat'a `cmd` yazın, **Komut İstemi**'ne sağ tıklayıp **Yönetici olarak çalıştır**'ı seçin ve şunları çalıştırın:

```
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" status
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue doctor
```

`venue doctor`, PC'nin açılışını aşama aşama gösterir; sorunsuz olmayan ilk satır, PC'nin takıldığı yerdir. İki çıktıyı ve PC'nin adını Kinesis'e gönderin.

## Yardım

**support@kinesis.network**. Kafeyi ve PC'nin adını yazın: Kinesis kurulumu kendi kayıtlarında görür.

CafePlus dışında bir kafe yazılımı mı kullanıyorsunuz? Önce bize yazın.

> Eski "Kinesis Spark disksiz kafe kiti" (PowerShell satırı ve `venue-setup.ps1`) kullanımdan kaldırıldı; sürümleri artık kullanılmıyor. Yukarıdaki kurulum dosyasını kullanın.
