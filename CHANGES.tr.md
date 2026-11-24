[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/CHANGES.md) | **Türkçe**

# Spark'ta yenilikler

## 0.4.20

0.4.18'den bu yana her şey. (0.4.19 tek bir kafede denenen bir test sürümüydü, hiç yayımlanmadı.) Kurulu bilgisayarlar
kendiliğinden güncellenir; kafe imajı ise bir sonraki imaj güncellemesinde alır ([rehberin](README.tr.md) 3. ve 4.
adımları).

### Kafeler

- **Kaybolan ekran kartı tahminle değil, olduğu gibi ele alınır.** Windows'taki NVIDIA sürücüsü "GPU is lost"
  dediğinde (nvidia-smi) ya da kart Linux tarafında kaybolduğunda Spark bilgisayarı Kinesis'e sunmayı bırakır ve kendi Linux'unu bir kez yeniden başlatır. Kafe
  bilgisayarında Windows da yeniden başlatılabilir; ama yalnızca bilgisayarda kimse yokken (müşteri oturumu yok,
  Windows kilitli ya da oturum açan yok, son zamanlarda klavye veya fare kullanılmamış), herhangi bir tuş ya da fare
  hareketiyle iptal edilen 30 saniyelik bir uyarıdan sonra ve yalnızca Kinesis açtığı yerde; şimdilik her yerde kapalı. Kart geri gelince Spark
  bilgisayarı kendiliğinden yeniden sunar.
- **GPU donma izleyicisi kaldırıldı.** Donmayı güç ölçümlerinden tahmin ediyordu ve biten bir işi donma sanabiliyordu.
  Spark artık yalnızca kartın bildirdiğini kaydeder; yanlış "GPU dondu" ve "GPU düzeldi" uyarıları biter.
- **Orijinal CCBoot ve PanCafe Pro.** 0.4.17'den beri destekleniyor, şimdi daha hızlı: Spark PanCafe'nin kilit
  ekranını, bir sonraki 2 saniyelik kontrolünü beklemeden, Windows onu gösterdiği ya da gizlediği anda fark eder.
- **Açılış türü hemen okunur.** Orijinal CCBoot'ta Spark, bilgisayarın müşteri bilgisayarı olarak mı yoksa düzenleme
  (Super Client) modunda mı açıldığını artık hemen okur. CCBoot'un kaydı bunu söylediğinde müşteri
  bilgisayarları açılıştan hemen sonra çalışmaya başlar, 2,5 dakikalık bekleme olmadan.
- **Hesabınızda sürpriz yeni bilgisayar yok.** Daha önce hiç Spark olmamış bir imajda Spark'ı kurmak, kafedeki her bilgisayarı
  yeni bir node yapar; Spark bu yüzden artık önce sorar: **Devam et: her bilgisayar yeni bir node olsun**. Spark
  zaten kurulu olan bir imaj, eskisi gibi bilgisayarlarını korur.
- **Daha az uyarı.** PanCafe'nin isteğe bağlı iki satırı artık eksik diye bildirilmez; bilgisayarın durumu, içindeki bir alan alışılmadık olsa bile Kinesis'e ulaşır,
  bütünüyle reddedilmez.
- **CafePlus menü yolu.** Kurulum ekranı ve rehber artık **Ayarlar** > **Client Ayarları** > **Açma Kapama Scripti**
  yolunu gösterir.
- **Oyun duraklatması kafe bilgisayarında hiç uygulanmaz** (müşteri olduğunu kafe yazılımı zaten söyler).

### Ev bilgisayarları

- **Gösterge paneli kutuları gerçek değerleri gösterir**: işlemci, bellek ve ekran kartı, her biri tek satırda; bir
  değer okunamıyorsa nedeni yazar.
- **Yönetici onayından önce kontroller.** Kurulum önce bilgisayarı kontrol eder (ekran kartı, işlemci, bellek, boş
  disk alanı, sanallaştırma) ve siz onaylamadan önce Spark'ın Kinesis'e ne gönderdiğini söyler. Eski bir işlemci (AVX2'siz)
  kurulumu durdurmaz, yalnızca not düşülür.
- **Windows 10: uygulamalar ev ağınızdan uzak durur.** Windows 10'da Kinesis işleri yalnızca bu koruma yerindeyken
  çalışır.
- **Uyku ve kapatma.** Spark, bilgisayar uyumadan ya da kapanmadan önce işini duraklatır.
- **Oyun oynarken duraklatma (isteğe bağlı, varsayılan olarak kapalı).** Başka bir program ekran kartını kullanırken
  Spark duraklayabilir.
- **Zorunlu güncelleme hiçbir zaman bir oyunun üstüne açılmaz.**

### Herkes

- **Uygulamanın adı her yerde Spark**: Yüklü uygulamalar, kısayollar, Başlat menüsü, bildirim alanı (başlangıç
  girdisi **Spark Notification Area**) ve kurulum penceresi.
- **İmzalı kod.** Spark'ın kurduğu dosyalar Kinesis Network Inc. tarafından imzalıdır; Windows'un Akıllı Uygulama
  Denetimi bunların çalışmasına izin verir. Yeni bir sürümde Windows yine de "Windows bilgisayarınızı korudu"
  diyebilir: **Ek bilgi**'ye tıklayın, yayımcıyı kontrol edin, sonra **Yine de çalıştır**'a tıklayın.
