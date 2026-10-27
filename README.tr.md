[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md) | **Türkçe**

# Kinesis Spark kafe kiti

Spark'ı internet kafenin Windows imajına kurar; böylece imajla açılan her PC, başında müşteri yokken kazanç sağlar.
Yalnızca **imaj PC'sinde**, dondurma / disksiz yazma koruması **KAPALIYKEN** çalıştırın.

1. Kafenin kendi Portal hesabından bir **"1 year (venue image)"** (1 yıl, kafe imajı) token alın (Fleet -> Add machines, yani Fleet -> Makine ekle).
2. Yönetici olarak açılmış bir PowerShell penceresinde: `mkdir C:\kinesis; cd C:\kinesis`, ardından (ilk kısım TLS 1.2'yi açar; Windows PowerShell GitHub'a bağlanmak için buna ihtiyaç duyar)
   `[Net.ServicePointManager]::SecurityProtocol = 'Tls12'; irm https://github.com/kinesis-network/kinesis-spark-releases/releases/latest/download/venue-setup.ps1 -OutFile venue-setup.ps1`
3. `powershell -ExecutionPolicy Bypass -File .\venue-setup.ps1` komutunu çalıştırın. Önce token'ı sorar, sonra kurulumun tamamını yapar; ilk sorunda durur ve neyin düzeltilmesi gerektiğini söyler.
4. Yeniden başlatma isterse: PC'yi yeniden başlatın (Başlat > Güç > Yeniden başlat), sonra aynı komutu tekrar çalıştırın. Kaldığı yerden devam eder.
5. Sizi üç kez bekler: kasa PC'sinde kancayı kurun (aşağıdaki "Kanca (hook) kurulumu" bölümü; 7. adım sayfanın bağlantısını verir ve bu PC'yi kontrol eder), bir kiralama ve bir kilitlemeyi deneyin, ardından imajı hazırlayan ve kiti silen onayları yazın. İmajı kaydedin, sonra korumayı yeniden **AÇIN**.

Tek bir adımı tekrarlamak veya onarmak için: `-Step <n>` ekleyin. `-Help` adımları listeler. İnternet baştan sona çalışır durumda olmalıdır; Spark ve motoru kendilerini günceller. Betiğin ekran çıktıları İngilizcedir.

## Kanca (hook) kurulumu

Kafe yazılımı, müşteri PC'ye oturduğunda ve kalktığında Spark'a haber verir; böylece PC kiralandığı anda Spark durur. Kafe yazılımınızı seçin:

- [AKINSOFT CafePlus](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md)

Başka bir kafe yazılımı mı kullanıyorsunuz? Kinesis ile iletişime geçin.
