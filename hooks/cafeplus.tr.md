[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md) | **Türkçe**

# Kanca (hook) kurulumu: AKINSOFT CafePlus

Bir kez, **kasa PC'sinde** yapılır, imaj PC'sinde değil. CafePlus bu ayarları kafedeki her PC'ye gönderir.

1. **Client Ayarları** > **Açma Kapama Scripti** bölümünü açın.
2. Üstteki kutuya, **Client kullanıma açılırken çalıştırılacak kod satırı** (müşteri oturumu başlarken), tam olarak şunu yapıştırın:

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
   ```

3. Alttaki kutuya, **Client kilitlenirken çalıştırılacak kod satırı** (müşteri kalkınca), tam olarak şunu yapıştırın:

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
   ```

4. Kaydedin. Her kutuya yalnızca bir satır, başka bir şey yok. Yolu yazıldığı gibi bırakın: asla `%ProgramFiles%` kullanmayın (CafePlus satırları 32 bit `cmd` ile çalıştırır; orada bu değişken `C:\Program Files (x86)` demektir).

**Ne zaman geçerli olur:** bir client PC kutuları yalnızca CafePlus istemcisi başlarken alır; pratikte bir sonraki açılışta. Bir PC'nin kutuları hemen almasını isterseniz (bu, o PC'deki oturumu bitirir; PC kilit ekranına döner): o PC'nin CafePlus penceresinde **Yetkili** sekmesinde **Programdan Çık** düğmesine tıklayın, ardından `C:\Program Files (x86)\AKINSOFT\CafePlusClient12\cplusc.exe` dosyasını yeniden başlatın. Sonraki kiralama veya kilitleme, kutunun satırını o PC'nin `script.cmd` dosyasına yazar.

**Spark olmayan PC'ler** aynı satırları çalıştırır ve hiçbir şey yapmaz: `if exist` kısmı onları atlar.

**Çalıştığını kontrol edin** (Spark'lı bir PC'de, yeniden başlattıktan sonra): PC'yi kasadan kiralayın; Spark yaklaşık 20 saniye içinde durur. Kilitleyin; Spark yaklaşık bir dakika içinde yeniden çalışır. Kitin 7. adımı (`-Step 7`) bu PC'nin CafePlus betiğinde satırı arar; 8. adımı (`-Step 8`) PC'yi kilitlemenizi, sonra kiralamanızı ister ve Spark'ın izlediğini kontrol eder.
