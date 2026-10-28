[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md) | **Türkçe**

# Kinesis Spark disksiz kafe kiti

Spark'ı internet kafenin ortak Windows imajına kurar; imajla açılan her PC, başında müşteri yokken kazanç sağlar.

## Hızlı kurulum: yapılacak iki şey

1. **Kasa PC'sinde** kancaları (hook) bir kez ayarlayın: [AKINSOFT CafePlus](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md).
2. **İmaj PC'sinde**, imaj düzenleme modundayken: Windows tuşu → `powershell` yazın → **Windows PowerShell**'e sağ tık → **Yönetici olarak çalıştır** → **Evet**; açılan mavi pencereye bu satırı yapıştırıp Enter'a basın ve ekrandakileri izleyin:

   ```
   powershell -NoProfile -ExecutionPolicy Bypass -Command "[Net.ServicePointManager]::SecurityProtocol='Tls12'; iwr https://github.com/kinesis-network/kinesis-spark-releases/releases/latest/download/venue-setup.ps1 -UseBasicParsing -OutFile ([IO.Path]::GetTempPath()+'venue-setup.ps1'); & ([IO.Path]::GetTempPath()+'venue-setup.ps1')"
   ```

Hepsi bu. Aşağısı aynı işin adım adım anlatımıdır.

## Gereksinimler

- [ ] **Disksiz sistem.** Kafenin PC'leri tek bir ortak Windows imajıyla bir sunucudan açılır (**CCBoot** gibi bir disksiz açılış yazılımı; benzerleri: diğer disksiz / imaj sistemleri ve dondurma yazılımları). Normal bir PC'de yapılan her değişiklik yeniden başlatınca kaybolur. Bu yüzden her değişiklik **bir kez, imajın üzerinde**, açılış yazılımının imaj düzenleme modunda yapılır (CCBoot'ta buna **Super Client** denir), sonra imaj kaydedilir ve her PC onu bir sonraki açılışında alır. Bu kılavuzda bu moddaki PC'ye **imaj PC'si** denir.
- [ ] **İnternet**, imaj PC'sinde, baştan sona.
- [ ] **Token**: kafenin **kendi** Portal hesabından bir **"1 year (venue image)"** token. Hesabı kafe olarak Kinesis işaretler; önce sorun.
  Portal'da: **Provide** > **Fleet** > **Add machines** > **Home or office** > geçerlilik **1 year (venue image)** > kopyalama düğmesi.
  24 saatlik token yalnızca deneme içindir: imajı bir gün sonra ilk kez açan PC'ler katılamaz. İmajdan sonra o sayfada asla **Regenerate**'e basmayın.
- [ ] **Kasa PC'sine erişim** (CafePlus ayarları için).
- [ ] BIOS'ta **sanallaştırma açık** (SVM / VT-x), her PC'de.
- [ ] GPU'lu PC'ler için **NVIDIA sürücüsü disksiz sistemden** gelir; imaja ayrıca sürücü kurmayın.

<!-- TODO(owner): ekran görüntüleri gelince ekleyin: images/portal-token.png (Portal'da token), images/admin-powershell.png (Yönetici olarak çalıştır), images/kit-done.png (BİTTİ ekranı). -->

## Kurulum (ilk kez)

1. **Kasa PC'sinde kancaları ayarlayın.** [CafePlus sayfası](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md)ndaki adımları izleyin (iki kutu, bir kez).

2. **İmaj PC'sini imaj düzenleme modunda açın** (CCBoot: Super Client) ve Windows'a giriş yapın.

3. **Yönetici penceresi açın.** Windows tuşuna basın, `powershell` yazın, **Windows PowerShell** üzerine sağ tıklayıp **Yönetici olarak çalıştır**'ı seçin, **Evet**'e tıklayın.
   Görmeniz gereken: başlığında **Yönetici: Windows PowerShell** yazan mavi bir pencere.

4. **Satırı yapıştırın** (pencereye sağ tık yapıştırır) ve Enter'a basın:

   ```
   powershell -NoProfile -ExecutionPolicy Bypass -Command "[Net.ServicePointManager]::SecurityProtocol='Tls12'; iwr https://github.com/kinesis-network/kinesis-spark-releases/releases/latest/download/venue-setup.ps1 -UseBasicParsing -OutFile ([IO.Path]::GetTempPath()+'venue-setup.ps1'); & ([IO.Path]::GetTempPath()+'venue-setup.ps1')"
   ```

   Görmeniz gereken: `=== Kinesis Spark disksiz kafe kiti 1.3.0 - KURULUM ===` ve altında `Neden: bu PC'de kafe modu henüz açık değil.`

5. **Token'ı sorduğunda** token'ı (veya Portal'ın kopyaladığı komutun tamamını) yapıştırıp Enter'a basın.
   Görmeniz gereken: `Kullanılan token: 1b2c3d4e...` Ardından kit kendi kendine çalışır; her satır `TAMAM`, `UYARI` veya `HATA` ile başlar.

6. **Yeniden başlatma isterse** (`YENİDEN BAŞLATMA GEREKİYOR`): **Başlat** > **Güç** > **Yeniden başlat** (Kapat değil), PC düzenleme modunda kalsın. Sonra 3. ve 4. adımı tekrarlayın: aynı satır kaldığı yerden devam eder.

7. **Kasa sorusu** (`İki kutu kasa PC'sinde kaydedilince burada Enter'a basın`): 1. adımı yaptıysanız Enter'a basın.
   CafePlus'ın yeniden başlatılıp başlatılmayacağını sorarsa (`...buradan yeniden başlatılsın mı? [e/H]` veya `...Şimdi başlatılsın mı? [e/H]`), `h` yazın: bu PC kutuları zaten bir sonraki açılışta alır.
   Ardından `Şimdi kilitleme ve kiralama testi yapılsın mı?` sorusuna `h` yazıp geçebilirsiniz; asıl test 10. adımdadır.

8. **İmajı hazırlayın.** Kit `İmajı hazırlamak için PREPARE yazıp Enter'a basın` dediğinde `PREPARE` yazın ve Enter'a basın. Bu, geri dönüşü olmayan adımdır: imajı mühürler.
   Görmeniz gereken: `TAMAM hazırlandı.`, `TAMAM kit silindi: ...` ve yeşil `=== BİTTİ. İMAJI şimdi (12 saat içinde) ... KAYDEDİN ...`

9. **İmajı kaydedin.** 12 saat içinde, PC'yi başka bir şey için kullanmadan, açılış yazılımında imajı kaydedin (CCBoot: Super Client'ı kapatırken değişiklikleri imaja kaydetmeyi seçin) ve yazma korumasını yeniden açın.

10. **Bir PC'yi kontrol edin.** Bir PC'yi imajla açın. Birkaç dakika içinde Portal'da **Provide** > **Fleet**'te görünür. Kasadan kiralayın: Spark yaklaşık 20 saniyede durur; kilitleyin: yaklaşık bir dakikada yeniden çalışır.
    Kiraya vermek için: **Fleet** > **Set up** > notice **0 h** > **List as spot capacity**.

## İmajı güncelleme (yeni Spark, yeni motor veya yeni token)

Yukarıdaki 2-4. adımları yapın: **aynı satır**. Kit kafe modunun açık olduğunu görür ve güncelleme yapar.

- Görmeniz gereken: `=== ... imajı GÜNCELLE ===` ve `Her PC kendi node'unu korur`.
- Token sorusunda token'ı değiştirmek için yenisini yapıştırın; korumak için yalnızca Enter'a basın.
- Kit mührü açar, akışta daha yeni Spark varsa kurar, motoru en son sürüme getirir, kontrol eder ve `PREPARE` ister. Sonra 9. adımdaki gibi imajı kaydedin.
- PC'ler node'larını korur: Portal'da yeni kayıt oluşmaz.

## Sorun çıkarsa

Kit ilk sorunda durur ve neyi düzelteceğini `HATA` satırında yazar. Düzeltip **aynı satırı yeniden yapıştırın**: biten adımları atlar.

| Ekranda gördüğünüz | Yapılacak |
|---|---|
| `Bu pencere yönetici olarak çalışmıyor` | Pencereyi kapatın; 3. adımdaki gibi **Yönetici olarak çalıştır** ile açın. |
| `İşlemci sanallaştırması (SVM / VT-x) BIOS'ta KAPALI` | BIOS'a girip SVM (AMD) / Intel VT-x'i açın, sonra satırı yeniden yapıştırın. |
| `Sürüm akışı hiçbir kaynaktan okunamadı` veya `İndirme başarısız` | Bu PC'nin internetini kontrol edin (tarayıcıda github.com açılıyor mu), sonra yeniden. |
| `SHA-256 akışla UYUŞMUYOR` veya `İmza KABUL EDİLMEDİ` | İndirilen dosya silindi; bir kez yeniden deneyin. Tekrarlarsa durun ve Kinesis'e bu PC'nin adını söyleyin. |
| `YENİDEN BAŞLATMA GEREKİYOR` | Başlat > Güç > Yeniden başlat, düzenleme modunda kalarak; sonra satırı yeniden. |
| `Yeniden başlatmadan önceki değişiklikler kayboldu` | PC düzenleme modunda değildi (yazma koruması açık). Düzenleme modunu açın, satırı yeniden. |
| `BİTMEDİ: ... bekliyor (WAIT satırları)` | Her `WAIT` satırının dediğini yapın (çoğunlukla yeniden başlatma), sonra satırı yeniden. |
| `script.cmd içinde henüz Spark satırı yok` | Durdurmaz; kasadaki iki kutuyu [CafePlus sayfası](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md)na göre kontrol edin. Satır, PC yeniden açıldıktan ve bir kiralama / kilitleme olduktan sonra görünür. |
| `Sürücüsüz devam edilsin mi?` | Bu PC'de hiç NVIDIA sürücüsü yok. GPU'lu PC'ler sürücüyü disksiz sistemden alıyorsa `e`, emin değilseniz `h` yazıp Kinesis'e sorun. |
| Başka bir `HATA` | Satırın dediğini yapın. Tek bir adımı tekrarlamak için kitin yazdığı `-Step <n>` komutunu kullanın. |

**Yardım isterken** Kinesis'e bu PC'nin adını (ve kafeyi) söyleyin: Kinesis kurulumu Spark'ın yüklediği kendi kayıtlarında görür. İmaj hazırlanana kadar kit bu PC'de çalıştırmanın tam kaydını da tutar, `C:\kinesis\venue-setup.log`; 8. adım onu kitle birlikte siler.

Ekran dili Windows diline göre seçilir. Başka dilde sürdürmek için (kit kendini `C:\kinesis` klasörüne kopyalar):

```
powershell -ExecutionPolicy Bypass -File C:\kinesis\venue-setup.ps1 -Lang en
```

Spark'ın kendi kontrol satırları (`OK` / `FIXED` / `WARN` / `WAIT` / `FAIL`) İngilizcedir.

Başka bir kafe yazılımı mı kullanıyorsunuz? Kinesis ile iletişime geçin.
