[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md) | **Türkçe**

# Kanca (hook) kurulumu: AKINSOFT CafePlus

CafePlus, müşteri PC'ye oturduğunda ve kalktığında Spark'a haber verir; böylece PC kiralandığı anda Spark durur. **Bir kez, kasa PC'sinde** yapılır, imaj PC'sinde değil; CafePlus bu ayarları kafedeki her PC'ye gönderir.

1. **Betik ayarlarını açın.** Kasa PC'sinde CafePlus'ta: **Client Ayarları** > **Açma Kapama Scripti**.
   Görmeniz gereken: iki kutu, **Client kullanıma açılırken çalıştırılacak kod satırı** (üstte) ve **Client kilitlenirken çalıştırılacak kod satırı** (altta).

2. **Üstteki kutu** (müşteri oturumu başlarken): tam olarak bu tek satırı yapıştırın.

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
   ```

3. **Alttaki kutu** (PC kilitlenince, müşteri kalkınca): tam olarak bu tek satırı yapıştırın.

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
   ```

4. **Kaydedin.**
   Görmeniz gereken: her kutuda yalnızca bir satır var, başka bir şey yok ve yol `C:\Program Files\Dynamo` olarak açık yazılı (asla `%ProgramFiles%` değil: CafePlus satırları 32 bit `cmd` ile çalıştırır; orada bu değişken `C:\Program Files (x86)` demektir).

5. **Bir sonraki açılışı bekleyin.** Her PC kutuları CafePlus istemcisi başlarken, yani bir sonraki açılışta alır. Spark olmayan PC'ler aynı satırları çalıştırır ve hiçbir şey yapmaz (`if exist` kısmı onları atlar).

6. **Spark'lı bir PC'de kontrol edin**, açılıştan sonra: PC'yi kasadan kiralayın.
   Görmeniz gereken: Spark yaklaşık 20 saniye içinde durur. Kilitleyin: Spark yaklaşık bir dakika içinde yeniden çalışır.

**Bir PC'nin kutuları hemen almasını isterseniz**, yeniden başlatmadan (bu, o PC'deki oturumu bitirir; PC kilit ekranına döner): o PC'nin CafePlus penceresinde **Yetkili** sekmesinde **Programdan Çık**'a tıklayın, sonra bunu yeniden başlatın:

```
C:\Program Files (x86)\AKINSOFT\CafePlusClient12\cplusc.exe
```

Sonraki kiralama veya kilitleme, kutunun satırını o PC'nin `script.cmd` dosyasına yazar. İmaj PC'sinde Spark'ın kafe kurulumu ([kurulum sayfası](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md)) **CafePlus kontrolü** adımında aynı iki satırı **Kopyala** düğmeleriyle gösterir, satırı orada arar ve **CafePlus istemcisini başlat** düğmesi sunar; isteğe bağlı kilitleme ve kiralama testi de Spark'ın buna uyduğunu kontrol eder.
