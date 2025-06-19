# 🐳 Docker Nedir, Ne İşe Yarar? | Tarihçesi

---

## 🚢 Docker Nedir?

**Docker**, uygulamaları ve bağımlılıklarını birlikte paketleyip çalıştıran, **container (kapsayıcı)** tabanlı, hafif bir sanallaştırma teknolojisidir.

> “Docker, yazılımları her yerde çalışabilir hâle getirir.”
> 

---

## 🎯 Ne İşe Yarar?

| Problem | Docker ile Çözüm |
| --- | --- |
| “Benim bilgisayarda çalışıyor, seninkinde bozuluyor.” | Docker ile **herkes aynı ortamı** kullanır. |
| “Projeyi kurmak 3 gün sürdü.” | Docker ile tek komutla kurulabilir (`docker compose up`) |
| “Sunucuda başka bir şey bozulmasın diye bu projeyi kuramıyorum.” | Her uygulama **izole container** içinde çalışır. |
| “Prod ortamı ile test ortamı farklı.” | Docker ile **her ortamda birebir aynı yapı** olur. |

---

## 📦 Docker Neyi Sağlar?

✅ İzolasyon – her uygulama kendi kutusunda çalışır

✅ Hızlı kurulum – saniyeler içinde ayağa kalkar

✅ Tekrar edilebilirlik – tüm ekip aynı ortamda çalışır

✅ Platform bağımsızlık – Linux, Mac, Windows, bulut…

---

## 🧱 Docker Hangi Yapıyı Kullanır?

1. **Dockerfile** ile image (şablon) oluşturulur
2. Bu image’tan **container** (çalışan uygulama) yaratılır
3. Container’lar izole, hafif ve hızlıdır

> Container = Çalışan uygulama
> 
> 
> Image = Uygulamanın dosyalarla birlikte hazır kalıbı
> 

---

## 📜 Docker’ın Tarihçesi

| Yıl | Gelişme |
| --- | --- |
| **2013** | Solomon Hykes tarafından Docker açıklandı (dotCloud firmasında) |
| **2014** | Docker Inc. kuruldu |
| **2015** | Docker Compose ve Swarm tanıtıldı |
| **2016** | Büyük şirketler Docker’ı benimsemeye başladı |
| **2017** | Kubernetes entegrasyonu başladı |
| **2020+** | Docker CLI topluluğa devredildi, **Kubernetes standart hâline geldi** |

---

## 💡 Docker’ı Kısaca Şöyle Düşün

> Docker, uygulamanı bir kutuya koyar ve "nerede çalışacağım?" derdini unutturur.
> 
> 
> — Tıpkı bir konteyner gemisi gibi: içinde ne varsa fark etmez, **standart şekilde taşınır.**
> 

# 🧾 Dockerfile Nedir?

**Bir Docker image oluşturmak için kullanılan tarif dosyasıdır.**

Aynı bir yemek tarifindeki gibi sırayla ne yapılacağı yazılır.

---

## 📦 Ne İşe Yarar?

Dockerfile:

- Uygulamanı alır
- Gerekli ortamı kurar (işletim sistemi, bağımlılıklar vs.)
- Uygulamanı çalıştıracak şekilde image üretir

> Sonuçta ortaya çıkan image, docker run ile container olarak ayağa kalkar.
> 

---

## 🔨 Dockerfile Satırları Ne Yapar?

Aşağıda bir örnek Dockerfile parça parça açıklanarak verilmiştir:

```
# 1️⃣ Base imajı seç
FROM node:18-alpine
```

> ➤ FROM: Hangi işletim sisteminden/ortamdan başlanacağını belirtir
> 
> 
> `alpine`: Çok küçük bir Linux dağıtımı (lightweight)
> 
> `node:18-alpine`: Node.js 18 + Alpine Linux
> 

---

```
# 2️⃣ Çalışma dizinini ayarla
WORKDIR /app
```

> ➤ Bundan sonraki tüm komutlar /app dizini içinde çalışacak
> 
> 
> Container içinde sanal bir klasör
> 

---

```
# 3️⃣ Proje dosyalarını kopyala
COPY . .
```

> ➤ Mevcut dizindeki (örneğin Go, JS, HTML dosyaların) hepsi, container içindeki /app dizinine kopyalanır
> 

---

```
# 4️⃣ Bağımlılıkları yükle
RUN npm install
```

> ➤ Image oluşurken bu komut bir kere çalışır
> 
> 
> Örn: `package.json` içindeki bağımlılıklar indirilir
> 
> ➤ `RUN` komutları image içinde yeni bir *katman* oluşturur
> 

---

```
# 5️⃣ Uygulamayı çalıştır
CMD ["npm", "start"]
```

> ➤ Container çalıştığında otomatik çalıştırılacak komut
> 
> 
> ➤ `CMD` sadece bir tane olabilir (sonuncusu geçerlidir)
> 

---

## 🗂 Dockerfile Akışı (Görsel Olarak)

```
FROM node:18-alpine
    ↓
WORKDIR /app
    ↓
COPY . .
    ↓
RUN npm install
    ↓
CMD ["npm", "start"]
```

---

## 🔁 RUN vs CMD vs ENTRYPOINT

| Komut | Ne zaman çalışır? | Ne işe yarar? |
| --- | --- | --- |
| `RUN` | Image oluşturulurken (`docker build`) | Bağımlılık yükle, build yap |
| `CMD` | Container başlatılırken (`docker run`) | Uygulamayı çalıştır |
| `ENTRYPOINT` | CMD gibi ama daha sabit | Script veya wrapper için kullanılır |

---

## 🧪 Dockerfile ile Image Oluşturma

```bash
docker build -t my-app-image .
```

> . = Dockerfile bulunduğu dizin
> 
> - `t` = tag (isimlendirme)
> 
> Sonuç: `my-app-image` adlı bir Docker image oluşur
> 

---

## ⚠️ Dikkat Edilecekler

✅ Her satır cache’lenir → değişiklik azsa build hızlı olur

✅ `COPY` sırası çok önemlidir (önce `package.json`, sonra kod dosyaları şeklinde yazmak mantıklıdır)

✅ Gereksiz dosyaları `.dockerignore` ile hariç tut (örneğin: `node_modules`, `tmp`, `logs`)

---

## 📄 .dockerignore Örneği

```
node_modules
.git
.env
logs
```

---

## 🎯 Gerçek Hayat Örneği (Go Uygulaması için)

```
FROM golang:1.21-alpine

WORKDIR /app

COPY go.mod ./
COPY go.sum ./
RUN go mod download

COPY . .

RUN go build -o app .

CMD ["./app"]
```

> ➤ Go uygulamasını build edip ./app olarak çalıştırır
> 
> 
> ➤ Bu Dockerfile, Compose ile API servisinde kullanılabilir
> 

---

## 🔚 Özet

| Direktif | Ne Yapar? | Ne Zaman Çalışır? |
| --- | --- | --- |
| `FROM` | Başlangıç imajını belirler | Build sırasında |
| `WORKDIR` | Çalışma dizinini ayarlar | Build sırasında |
| `COPY` | Dosyaları konteynıra kopyalar | Build sırasında |
| `RUN` | Komut çalıştırır (örneğin `npm install`) | Build sırasında |
| `CMD` | Container başladığında ne çalışsın | Çalışma zamanında |

---

Dockerfile’ı iyi yazmak = performanslı, güvenli ve taşınabilir image’lar üretmek demektir.

# 📦 Docker Container Nedir?

## ve Nasıl Çalışır?

---

## 🔍 Tanım

**Docker Container**, bir Docker image’tan oluşturulmuş ve çalışan, **gerçek uygulama ortamıdır**.

> 📦 Image = tarif
> 
> 
> 🔥 Container = pişmiş, çalışan uygulama
> 

---

## 💡 Kısaca:

**Image** sadece bir şablondur.

**Container**, bu şablondan oluşturulan ve RAM, CPU, port, disk gibi kaynakları kullanan **canlı çalışan bir süreçtir**.

---

## 📊 Özellikleri

| Özellik | Açıklama |
| --- | --- |
| İzole | Her container kendi ağında, diskinde çalışır |
| Hafif | Tüm işletim sistemini sanallaştırmaz (VM gibi değil) |
| Hızlı | Saniyeler içinde başlar |
| Taşınabilir | Her yerde aynı şekilde çalışır |
| Geçici ya da kalıcı | Kalıcı veriler volume ile saklanabilir |

---

## 🔁 Container Yaşam Döngüsü

1. `docker run` → yeni container başlatır
2. `docker ps` → çalışanları listeler
3. `docker stop` → çalışmayı durdurur
4. `docker start` → yeniden başlatır
5. `docker rm` → siler
6. `docker logs` → çıktılarını gösterir

---

## 🛠️ Uygulamalı Komutlar

### ✅ Yeni Container Başlat

```bash
docker run -d -p 8080:80 --name web nginx
```

| Parametre | Anlamı |
| --- | --- |
| `-d` | Arka planda çalış |
| `-p` | Port yönlendirmesi: host:container |
| `--name` | Container’a isim ver |
| `nginx` | Kullanılan image ismi |

---

### 📋 Container’ları Listele

```bash
docker ps              # Çalışanlar
docker ps -a           # Tüm (çalışan + durmuş)
```

---

### 🧼 Container’ı Silmek

```bash
docker stop web        # önce durdur
docker rm web          # sonra sil
```

> Not: Durdurulmadan silinemez.
> 

---

### 🧠 İçine Girmek

```bash
docker exec -it web sh
```

Açıklama

---

```
-it
```

= interaktif terminal

---

```
web
```

= container ismi/id

---

```
sh
```

= içine shell ile gir

---

---

### 🔍 Log'ları Görmek

```bash
docker logs web
docker logs -f web    # canlı takip
```

---

## 🧠 Hafızada Nasıl Tutmalı?

> Docker image = buzlu yemek
> 
> 
> Docker container = mikrodalgada ısıtılmış yemek — artık **kullanıma hazır**
> 

---

## 💥 Docker Container vs Virtual Machine

| Özellik | Container | Sanal Makine (VM) |
| --- | --- | --- |
| Başlangıç süresi | Saniyeler | Dakikalar |
| Sistem kaynakları | Çok az | Daha fazla |
| Yalıtım | İşletim sistemi seviyesinde | Donanım seviyesinde |
| Taşınabilirlik | Yüksek | Daha az |
| Tipik kullanım | Mikroservisler | Büyük uygulama ortamı |

---

## 📦 Örnek Akış

```bash
docker build -t myapi .
docker run -d -p 5000:5000 --name myapi-container myapi
```

- Bu image’tan canlı bir container oluşturulur
- Tarayıcıdan: `http://localhost:5000` ile erişilebilir

---

## ✅ Özet

| Kavram | Açıklama |
| --- | --- |
| Image | Dockerfile’dan üretilen tarif |
| Container | O image’tan çalışan uygulama |
| `docker run` | Yeni bir container başlatır |
| `docker ps` | Mevcut container’ları gösterir |
| `docker stop`, `rm` | Container’ı yönetir |

## 📦 Docker Volume Nedir?

- Volume, **Docker konteynerlerinin veri saklaması** için kullandığı özel bir klasördür.
- Konteyner silinse bile **volume içindeki veri kalır**.
- Docker host üzerinde `/var/lib/docker/volumes/` dizininde tutulur.
- Volume’lar konteynerlerden bağımsızdır.

---

### ❓ Neden Volume Kullanılır?

- **Veri kaybını önlemek** için
- **Aynı veriye birden çok konteynerin erişmesini sağlamak** için
- **Veri yedeklemek ve taşımak** için
- **Konteynerler arası bağımsızlık** için

---

### 🛠️ Volume Oluşturma Komutu

```bash
docker volume create mydata
```

- `mydata`: volume’un ismi
- Oluşturulan volume artık Docker host üzerinde kalıcıdır.

---

### 🔍 Volume’ları Listeleme

```bash
docker volume ls
```

- Sisteminizdeki tüm volume’ları listeler.

---

### 🧪 [Uygulama] Volume ile Veri Kalıcılığı

1. **Volume Oluştur:**

```bash
docker volume create mydata
```

1. **Bir Konteyner Çalıştır (Volume Bağlayarak):
BusyBox nedir ?** Linux komut satırı araçlarının **küçük, hafif ve hepsini içinde barındıran** bir versiyonudur. Çok **küçük (yaklaşık 1 MB)** ve hızlıdır. Sana sade bir Linux ortamı sunar. Testler için idealdir.

```bash
docker run -d \
  --name volume-test \
  -v mydata:/app/data \
  busybox sleep 3600
```

> Açıklama:
> 
> - `v mydata:/app/data`: `mydata` adlı volume’u konteyner içinde `/app/data` klasörüne bağlar.
1. **Konteyner İçine Girip Dosya Oluştur:**

```bash
docker exec -it volume-test sh
```

```
echo "Merhaba Volume!" > /app/data/merhaba.txt
exit
```

1. **Konteyneri Sil:**

```bash
docker rm -f volume-test
```

1. **Yeni Konteyner ile Volume’i Tekrar Kullan:**

```bash
docker run -it --rm -v mydata:/app/data busybox sh
```

```
cat /app/data/merhaba.txt
```

> Beklenen çıktı:
> 
> 
> `Merhaba Volume!`
> 

✅ **Veri hâlâ duruyor!** Konteyner silinse bile volume’daki veri kaybolmadı.

---

### 🧼 Volume Silme

Önce kullanılmıyor olması gerekir.

```bash
docker volume rm mydata
```

Tüm kullanılmayan volume’ları topluca silmek için:

```bash
docker volume prune
```

---

### 📚 Özet

| Komut | Açıklama |
| --- | --- |
| `docker volume create NAME` | Yeni volume oluşturur |
| `docker volume ls` | Volume’ları listeler |
| `-v volume:/path` | Volume'u konteyner içine bağlar |
| `docker volume rm NAME` | Volume siler |
| `docker volume prune` | Kullanılmayan tüm volume’ları siler |

---

### 📌 Ekstra Bilgi: Bind Mount vs Volume

| Özellik | Volume | Bind Mount |
| --- | --- | --- |
| Yönetim | Docker tarafından | Manuel |
| Güvenlik | Daha güvenli | Daha az güvenli |
| Yedekleme | Daha kolay | Daha zor |
| Konum | Docker içinde | İstediğiniz dizin |

---

---

## 🔍 Docker Volume vs Bind Mount

### 🧠 Hatırlatma

- Volume = Docker yönetiyor
- Bind Mount = Sen yönetiyorsun
- Volume daha güvenli, Bind Mount daha esnek

### Ne Zaman Hangisini Kullanmalıyım?

---

### 📦 Volume vs 📂 Bind Mount

| Özellik | Volume | Bind Mount |
| --- | --- | --- |
| Tanım | Docker tarafından yönetilen veri alanı | Host sistemdeki klasörü doğrudan bağlama |
| Konum | `/var/lib/docker/volumes/...` | Belirttiğin klasör (örnek: `/home/user/data`) |
| Güvenlik | Daha güvenli | Güvenlik riski olabilir |
| Yedekleme / Taşıma | Kolay | Zor |
| Kullanım Kolaylığı | Docker yönetir | Kullanıcı kontrolünde |
| Performans | Optimize edilmiş | Düşebilir |

---

### 🧪 [Uygulama] Bind Mount ile Çalışma

### 1. Host’ta Bir Klasör Oluştur

```bash
mkdir -p /tmp/bind-data
```

```bash
echo "Selam Bind Mount!" > /tmp/bind-data/selam.txt
```

---

### 2. Konteyneri Bind Mount ile Başlat

```bash
docker run -it --rm \
  -v /tmp/bind-data:/app/data \
  busybox sh
```

### 3. Konteyner İçinde Dosyayı Görüntüle

```
cat /app/data/selam.txt
```

> Çıktı: Selam Bind Mount!
> 

---

### 🧪 [Kıyaslama]: Volume ve Bind Mount Yan Yana

|  | Volume Kullanımı | Bind Mount Kullanımı |
| --- | --- | --- |
| **Komut** | `-v mydata:/app/data` | `-v /tmp/bind-data:/app/data` |
| **Avantaj** | Konteyner bağımsız, taşınabilir, yedeklenebilir | Geliştirme sırasında gerçek dosyalara doğrudan erişim |
| **Senaryo** | Üretim ortamı, kalıcı veritabanı verisi | Geliştirme ortamı, kod senkronizasyonu |

---

### 🎓 Ne Zaman Hangisi?

✅ **Volume** kullan:

- Kalıcı, güvenli ve konteynerden bağımsız veri saklamak istiyorsan
- Üretim ortamında

✅ **Bind Mount** kullan:

- Geliştirme sırasında kodları doğrudan konteyner içinde test etmek istiyorsan
- Lokalde düzenlediğin dosyaları anında konteynerde görmek istiyorsan

---

## 🌐 Docker’da Ağ (Network) Nedir?

Docker, konteynerlerin **birbirleriyle veya dış dünya ile iletişim kurmasını** sağlayan sanal ağlar oluşturur.

---

### 🔌 Neden Docker Network Kullanılır?

- Konteynerler arası **güvenli iletişim** kurmak için
- **Servis keşfi (service discovery)** sağlamak için
- **İzolasyon** ve **kontrol** için
- Çoklu konteynerli mimarilerde (örn. microservices) **iletişim altyapısı** kurmak için

---

### 🧱 Docker Network Türleri

| Tür | Açıklama |
| --- | --- |
| **bridge** | Varsayılan ağ, konteynerler aynı ağdaysa haberleşebilir. |
| **host** | Konteyner, host makinenin ağına doğrudan bağlanır. |
| **none** | Ağ bağlantısı yoktur. |
| **overlay** | Farklı Docker host’ları arasında iletişim sağlar (swarm ile). |
| **macvlan** | Fiziksel ağda kendi IP’si olur (ileri seviye). |

---

### 🔧 Network Listeleme ve Oluşturma

- Mevcut ağları listele:

```bash
docker network ls
```

- Yeni bir `bridge` ağı oluştur:

```bash
docker network create my-bridge
```

---

### 🧪 [Uygulama] Konteynerler Arası İletişim

### Adım 1: Özel Bridge Ağı Oluştur

```bash
docker network create my-net
```

---

### Adım 2: İki Konteyneri Aynı Ağa Dahil Et

```bash
docker run -dit --name container1 --network my-net busybox sh
docker run -dit --name container2 --network my-net busybox sh
```

---

Docker Run Komutundaki `d -i -t` Parametreleri

---

---

### `d` (detached mode)

- Konteyneri **arka planda (detached) çalıştırır.**
- Komut terminali hemen geri döner, konteyner kendi içinde çalışmaya devam eder.
- Örneğin bir web sunucusu gibi sürekli açık kalması gereken uygulamalar için kullanılır.

---

### `i` (interactive)

- Konteynerin **standart girişini (stdin) açık tutar.**
- Yani komut çalışırken konteyner ile etkileşim kurabilirsin.
- Örneğin komut satırına yazı yazmak veya programla iletişim için kullanılır.

---

### `t` (tty)

- Konteyner içinde **sanal bir terminal (tty) oluşturur.**
- Bu sayede komut satırı daha okunaklı, kullanıcı dostu olur.
- Terminalde renkli ve biçimlendirilmiş çıktı için gereklidir.

---

### ⚡ Birlikte Kullanımı: `dit`

- `d` + `i` + `t`
- Kısaca; **konteyner arka planda çalışır, ama etkileşim için hazırdır ve terminal desteği vardır.**

### Adım 3: container2’den container1’e Ping At

```bash
docker exec -it container2 sh
ping container1
```

> ❗ Hostname olarak konteyner ismini kullanabiliriz çünkü aynı Docker ağı içindeler!
> 

---

### 📌 Not: Default Network (bridge)

```bash
docker run -dit --name test busybox sh
```

Varsayılan olarak `bridge` ağına bağlanır, ama bu ağda **hostname ile erişim çalışmaz.** IP adresi gerekir.

---

### 🧼 Network Silme

> Bir network'ü silmeden önce o ağa bağlı konteynerler durdurulmalı/silinmeli.
> 

```bash
docker network rm my-net
```

---

### 🧠 Hızlı Özet

| Komut | Açıklama |
| --- | --- |
| `docker network ls` | Ağları listeler |
| `docker network create NAME` | Yeni ağ oluşturur |
| `--network NAME` | Konteyneri ağa dahil eder |
| `docker network rm NAME` | Ağı siler |

---

### 🎓 Ne Zaman Hangi Ağı Kullanmalı?

| Network Türü | Ne zaman? |
| --- | --- |
| **bridge** | Basit, tek host üzerindeki uygulamalar |
| **host** | Ağa doğrudan erişim gerekiyorsa (örnek: performans önemliyse) |
| **overlay** | Farklı host’lar arasında iletişim gerekiyorsa |
| **none** | Ağ erişimi istenmiyorsa |
| **macvlan** | Fiziksel ağ IP’si atanacaksa (genellikle ileri seviye) |

---

### 📌 Bonus: Network Detaylarını Görüntüle

```bash
docker network inspect my-net
```

Bu komut ile:

- Bağlı konteynerleri
- IP adreslerini
- Ağ yapılandırmasını
    
    görebilirsin.
    

---

## 📦 Docker Registry Nedir?

---

### 🔍 Tanım

Docker Registry, Docker image’larının **saklandığı, paylaşıldığı** merkezi bir depo (repository) hizmetidir.

- Docker Hub: En yaygın kullanılan genel (public) registry.
- Özel Registry: Kurumsal veya özel kullanım için kendi registry’nizi kurabilirsiniz.

---

### 🎯 Neden Registry Kullanırız?

- Image’ları **başkalarıyla paylaşmak** için
- Farklı makinelerde aynı image’ı kullanabilmek için
- CI/CD süreçlerinde otomatik image dağıtımı için

---

### 🧑‍🏫 Örnek Senaryo

- Geliştirdiğin uygulamanın image’ını Docker Hub’a gönder
- Başka bir makinada aynı image’ı indir (pull) ve çalıştır

---

## 🔧 Uygulama

---

### Docker Hub Hesabı Oluşturma

- Adres: https://hub.docker.com
- Sağ üst köşeden **Sign Up** (Kayıt Ol) seçeneğine tıkla
- Gerekli bilgileri doldur (kullanıcı adı, e-posta, şifre)
- E-postanı doğrula (verification mail)

### 1. Docker Hub’a Giriş Yap

```bash
docker login -u $sUSER_NAME
```

- Kullanıcı adı, şifre gir
- Başarılı olursa registry ile bağlantın aktif olur

---

### 2. Image’i Hazırla ve Tag Ver

```bash
docker build -t kullaniciadi/myapp:1.0 .
```

---

### 3. Image’i Push Et (Yükle)

```bash
docker push kullaniciadi/myapp:1.0
```

---

### 4. Başka Makinada Image’ı Çek (Pull)

```bash
docker pull kullaniciadi/myapp:1.0
```

---

## 🏗️ Özel Registry Kurulumu (Opsiyonel)

```bash
docker run -d -p 5000:5000 --restart=always --name registry registry:2
```

- Bu komut yerel makinanda basit bir registry açar
- Image’ları buraya push ve pull yapabilirsin

---

### Özel Registry’ye Image Gönderme

```bash
docker tag myapp localhost:5000/myapp
docker push localhost:5000/myapp
```

---

### Özel Registry’den Image Çekme

```bash
docker pull localhost:5000/myapp
```

---

## 🧠 Özet

| Komut | Açıklama |
| --- | --- |
| `docker login` | Registry’ye giriş yapar |
| `docker push` | Image’i registry’ye yükler |
| `docker pull` | Image’i registry’den çeker |
| `docker tag` | Image’e isim ve tag ekler
 |

## 📝 Docker Commit Nedir?

---

### 🔍 Tanım

- Çalışan bir konteyner üzerinde yaptığın değişiklikleri **yeni bir Docker image** olarak kaydetmeye yarar.
- Yani “konteyner anlık görüntüsünü (snapshot) image’e dönüştürür.”

---

### 🎯 Ne Zaman Kullanılır?

- Konteyner içinde elle yaptığın konfigürasyonları veya değişiklikleri kalıcı hale getirmek istediğinde
- Örneğin; bir uygulama içinde ayar değiştirip, bu değişiklikle yeni image oluşturmak istediğinde

---

## 🔧 Uygulama

---

### 1. Yeni Bir Container Başlat

```bash
docker run -dit --name mycontainer busybox sh
```

---

### 2. Container İçinde Değişiklik Yap

```bash
docker exec -it mycontainer sh
# Container içindeyiz, örneğin bir dosya oluştur:
echo "Merhaba Docker" > /merhaba.txt
exit
```

---

### 3. Commit Komutuyla Yeni Image Oluştur

```bash
docker commit mycontainer kullaniciadi/myimage:v1
```

- `kullaniciadi/myimage:v1` istediğin image ismi ve etiketi olabilir.

---

### 4. Oluşturulan Image’ı Görüntüle

```bash
docker images
```

---

### 5. Yeni Image’dan Container Başlat

```bash
docker run -dit --name yeni_container kullaniciadi/myimage:v1 sh
docker exec -it yeni_container sh
cat /merhaba.txt
```

- Dosyanın içerdiği yazı görünecek.

---

## 🧠 Özet

| Komut | Açıklama |
| --- | --- |
| `docker commit [container] [image:tag]` | Container’daki değişikliği yeni image olarak kaydeder |

---

### ⚠️ Not

- Commit edilen image, **katman katman büyür**, temiz ve minimal Dockerfile kullanmak genellikle daha iyidir.
- Commit genelde hızlı prototip ve testler için kullanılır, üretim için Dockerfile tercih edilir.

## 💾 Docker Save & Load Nedir?

---

### 🔍 Tanım

- **`docker save`**: Docker image’ını bir dosya olarak dışa aktarır (export).
- **`docker load`**: Daha önce `save` ile kaydedilmiş image dosyasını tekrar Docker’a yükler.

---

### 🎯 Ne İşe Yarar?

- İnternet olmayan ortamlarda image transferi için,
- Yedekleme yapmak için,
- Başka makinaya ya da ortama image taşımak için kullanılır.

---

## 💾 Docker Save & Load Örneği — PostgreSQL Image

---

### 1. PostgreSQL Image’ını Çek (Pull)

```bash
docker pull postgres:15
```

---

### 2. PostgreSQL Image’ını Kaydet (Save)

```bash
docker save -o postgres_image.tar postgres:15
```

- `postgres_image.tar` olarak PostgreSQL image’ını dosya halinde kaydettik.

---

### 3. Kaydedilen Dosyayı Kontrol Et

```bash
ls -lh postgres_image.tar
```

---

### 4. PostgreSQL Image’ını Yükle (Load)

```bash
docker load -i postgres_image.tar
```

---

### 5. Yüklenen Image’ı Doğrula

```bash

docker images | grep postgres
```

- `postgres:15` image’ının listede olduğunu göreceksin.

---

Bu şekilde internet bağlantısı olmayan makinaya dosya taşınabilir veya yedekleme yapılabilir.

---

## 🧠 Özet

| Komut | Açıklama |
| --- | --- |
| `docker save -o dosya.tar image` | Image’ı dışa aktarır (dosya olarak kaydeder) |
| `docker load -i dosya.tar` | Dışa aktarılmış image’ı yükler (import eder) |

---

---

### Docker'ın günlük kullanımında en çok karşılaşılan temel komutlarıdan bahsedelim.

1. **Tanım ve ne işe yaradığı**
2. **Gerçek kullanım senaryosu**
3. **Terminal örnekleri**
4. **İpuçları ve dikkat edilmesi gerekenler**

---

### ✅ İlk Komut: `docker run`

Hazırlayıp hemen paylaşacağım. Ardından sırayla diğer komutlara geçeceğim:

Güncel komut sırası:

```
1. docker run (-d, -i, -t, --rm flag’leriyle)
2. docker start, stop, restart, rm
3. docker ps
4. docker images
5. docker inspect
6. docker logs
7. docker exec
8. docker cp
9. docker top
10. docker stats
11. docker prune
12. docker rename
13. docker system df
```

---

## 🏃‍♂️ `docker run` Komutu

---

### 🔍 Tanım

`docker run`, yeni bir container oluşturup çalıştırmak için kullanılır.

Bu komut Docker’ın en temel ve en önemli komutudur.

---

### 🧱 Genel Yapısı

```bash
docker run [seçenekler] image_ismi [komut]
```

---

## 🔧 Uygulamalı Anlatım

---

### 🚀 1. Temel Kullanım

```bash
docker run hello-world
```

- Docker image’ı çeker ve container’ı çalıştırır.
- Çıkışta otomatik durur.

---

### 🎛️ 2. Yaygın Flag'ler ve Anlamları

### 📌 `d` → Arka planda (detached) çalıştırır

```bash
docker run -d nginx
```

### 📌 `i` → Standart input açık kalır (interactive)

```bash
docker run -i ubuntu

```

### 📌 `t` → Terminal emülasyonu sağlar (tty)

```bash
docker run -it ubuntu

```

- Genelde `i -t` birlikte kullanılır: `it`

### 📌 `-rm` → Container durunca otomatik silinir

```bash
docker run --rm ubuntu echo "Merhaba Dünya"
```

---

### 🧪 3. Etkileşimli Terminal Açmak

```bash
docker run -it ubuntu /bin/bash
```

- Ubuntu container’ı başlatır
- `/bin/bash` komutuyla terminal açılır
- İçeride komutlar çalıştırabilirsin

Çıkmak için:

```bash
exit
```

---

### 🧼 4. Geçici Container ile İş Yapmak

```bash
docker run --rm alpine sh -c "echo merhaba"
```

- İşini yapar, çıkar ve silinir

---

## 🧠 Özet Tablo

| Flag | Açıklama |
| --- | --- |
| `-d` | Detached modda arka planda çalıştırır |
| `-i` | Interactive terminal |
| `-t` | Terminal (TTY) açar |
| `--rm` | Çıkınca container’ı siler |
| `-it` | Terminalde etkileşimli kullanım sağlar |

---

## 🧑‍🏫 Eğitici Örnek

```bash
docker run -it --rm ubuntu
```

Bu komutla:

- Ubuntu container’ı başlatılır
- Terminal açılır, komutlar girilir
- `exit` denince container otomatik silinir

## 🧯 Docker Container Yönetim Komutları

---

## 🚦 1. `docker start`

- **Daha önce durdurulmuş (stopped) bir container'ı tekrar başlatır.**

```bash
docker start mycontainer
```

> ❗ docker run ile container oluşturulmuş ve sonrasında durdurulmuş olmalı
> 

---

## 🛑 2. `docker stop`

- **Çalışan bir container'ı durdurur (graceful shutdown).**

```bash
docker stop mycontainer
```

> Uygulamaya SIGTERM sinyali gönderir, düzgün kapanma şansı verir.
> 

---

## 🔄 3. `docker restart`

- **Çalışan bir container'ı önce durdurur, sonra yeniden başlatır.**

```bash
docker restart mycontainer
```

> Güncelleme sonrası yeniden başlatmak veya sorun çözümlerinde kullanılır.
> 

---

## 🗑️ 4. `docker rm`

- **Bir container'ı siler. (sadece durdurulmuş olanlar silinebilir)**

```bash
docker rm mycontainer
```

> Çalışan container'ı zorla silmek için:
> 

```bash
docker rm -f mycontainer
```

---

## 👷‍♂️ Uygulamalı Senaryo

```bash
# 1. Yeni bir container oluştur
docker run -dit --name test-container ubuntu

# 2. Container'ı durdur
docker stop test-container

# 3. Tekrar başlat
docker start test-container

# 4. Yeniden başlat
docker restart test-container

# 5. Sil
docker stop test-container   # önce durdur
docker rm test-container

```

---

## 📌 Bonus: `docker ps -a`

Tüm container'ları görmek için:

```bash
docker ps -a
```

> Hangi container’lar duruyor, hangileri çalışıyor görebilirsin.
> 

# 🐝 Docker Swarm Nedir?

---

## 🔍 Tanım

**Docker Swarm**, birden fazla Docker host’un (sunucunun), tek bir mantıksal grup (cluster) olarak çalışmasını sağlayan **yerleşik container orkestrasyon sistemidir.**

- Swarm mod, Docker Engine’in içine gömülüdür.
- Uygulamaları ölçeklendirmek, yüksek erişilebilirlik sağlamak ve yük dengelemek için kullanılır.

Hayal et ki uygulaman (Nginx + PostgreSQL + arka‑plan çalışanı) bir sunucuda **3 ayrı container** olarak koşturuyor.

Trafik artınca:

1. **Yeni bir sunucu** (Node‑2) ekliyorsun.
2. Swarm’a `docker swarm join …` ile dâhil ediyorsun.
3. Swarm, “kümede artık 2 bilgisayar var” diye kaydediyor.

### 1. Gerçek makine dizilimi

| IP | Rol | Ne yapıyor? |
| --- | --- | --- |
| 192.168.10.5 | Manager | Karar verir, cluster’ı yönetir |
| 192.168.10.6 | Worker | Container çalıştırır |
| 192.168.10.7 | Worker | Container çalıştırır (opsiyonel) |

### 2. Tek komutla ölçekleme

```bash
bash
KopyalaDüzenle
docker service create \
  --name web \
  --replicas 6 \
  -p 80:80 \
  nginx:alpine

```

*Swarm ne yapar?*

- 6 kopyayı **dağıtır** – örneğin 3 tanesini Node‑1’e, 3 tanesini Node‑2’ye.
- Her kopya aynı “service” DNS adına (web) cevap verir.
- Gelen istekler node’lar arasında **otomatik dengelenir**.

> Kubernetes’teki “Deployment + Service” kavramlarının basitleştirilmiş karşılığıdır.
> 

### 3. Otomatik kurtarma senaryosu

1. Node‑2 (192.168.10.6) kapanır.
2. Manager bunu ‘unreachable’ olarak işaretler.
3. Swarm o node’daki 3 web kopyasını **Node‑1’e veya Node‑3’e yeniden başlatır**.
4. Dış dünyadan gelen trafik hâlâ çalışır; kullanıcı hiçbir kesinti hissetmez.

### 4. Uygulama güncelleme (rolling update)

```bash
bash
KopyalaDüzenle
docker service update \
  --image nginx:1.27-alpine \
  --update-parallelism 2 \
  --update-delay 10s \
  web

```

- Swarm önce 2 kopyayı yeni görüntüyle yeniden yaratır,
- 10 saniye bekler, sağlık kontrolü geçerse sonraki 2 kopyaya geçer…
- Bu işlem tamamlanana kadar site sürekli yayında kalır.

### 5. Komutların arkadaki “somut” sonucu

| Komut | Sunucularda gerçekten olan |
| --- | --- |
| `docker service create …` | Her node’da container dosyaları, overlay ağı, dinleyici portu açılır |
| `docker service scale web=10` | Ek 4 container farklı node’lara planlanır |
| `docker node ls` | Etkin node’lar ve sağlık durumu listelenir |
| `docker service ps web` | Hangi kopya hangi sunucuda, hangi IP’de görürsün |
| Node down (kablo çekildi) | “Task State=Failed, Scheduling next…” log’ları ve yeni container yaratma |

---

## Neden bu “küme” mantığı bize yarar?

- **Tek terminalden** (Manager) yüzlerce container’ı idare edersin.
- “Bu container şu makinede, diğeri bu makinede” derdini **Swarm’ın planlayıcısı** çözer.
- Yedeklilik, otomatik iyileşme ve canlı güncelleme adeta “yerleşik özellik” hâline gelir.

---

### Peki neden **Kubernetes** öne çıktı?

| Gelişmiş ihtiyaç | Swarm | Kubernetes |
| --- | --- | --- |
| Config/Secret yönetimi, Ingress, CRD | Sınırlı veya yok | Dahili, eklenti ekosistemi çok zengin |
| Dev‑>Prod aynı manifest | `docker stack` YAML desteği kısıtlı | Aynı YAML her ortamda çalışır |
| Otomatik yatay‑dikey ölçekleme | Basit `replicas` sayısı | CPU/RAM metriğine göre HPA/VPA |
| Topluluk, yeni sürüm/güvenlik yamaları | 2020’den beri **yalnızca bakım** | Aktif geliştirme, büyük ekosistem |

Bu yüzden üretimde “cluster orkestrasyonu” dendiğinde bugün **standart cevap Kubernetes** oluyor; Swarm ise demo, PoC veya küçük ölçekli senaryolarda hâlâ hızlı ve pratik bir seçenek olarak kalıyor.

---

### Kısaca akılda şöyle tutabiliriz

> Docker Swarm = “Birden çok Docker makinesini tek bir büyük Docker gibi çalıştıran, basit ama artık genişlemeyen bir orkestratör.”
> 
> 
> **Somut çıktısı:** tek komutla dağıtım, yük dengeleme, otomatik yeniden başlatma – hepsi Docker Engine’in içinde, ekstra yazılım kurmadan.
> 

---

## 🤝 Docker Swarm ve Kubernetes İlişkisi

### Kubernetes nedir?

**Kubernetes (k8s)**, Google tarafından geliştirilmiş ve günümüzde CNCF tarafından yönetilen, **container orkestrasyonu için endüstri standardı** haline gelmiş güçlü bir platformdur.

### Ortak Noktalar:

| Özellik | Docker Swarm | Kubernetes |
| --- | --- | --- |
| Orkestrasyon sistemi | Evet | Evet |
| Yük Dengeleme | Var | Var |
| Otomatik yeniden başlatma | Var | Var |
| Dağıtık yapı | Var | Var |

---

## ❓ Neden Kubernetes Daha Çok Tercih Ediliyor?

| Kriter | Swarm | Kubernetes |
| --- | --- | --- |
| **Topluluk ve destek** | Az (resmi destek artık durdu) | Büyük, aktif ve kurumsal destek |
| **Özellik zenginliği** | Temel düzeyde | Zengin (pod, configMap, secret, vs.) |
| **Otomasyon** | Sınırlı | Gelişmiş (auto-healing, rollout) |
| **Yaygınlık** | Azalan | Endüstri standardı |
| **3rd party entegrasyon** | Kısıtlı | Çok geniş |

> 📉 Docker, 2020 itibariyle Swarm’a yeni özellik geliştirmeyi durdurdu.
> 
> 
> ✅ **Kubernetes, modern mikroservis altyapılarının temel taşı oldu.**
> 

---

# 🔧 Swarm Mimarisi ve Kavramlar

| Kavram | Anlamı |
| --- | --- |
| **Node** | Swarm içindeki bir Docker sunucusudur (host) |
| **Manager** | Swarm’ı yöneten, karar verici node |
| **Worker** | Görevleri çalıştıran işçi node |
| **Service** | Swarm üzerinde çalışan uygulama tanımı |
| **Task** | Service’in çalıştırdığı her bir container |

---

### 👁️ Swarm Mimarisi

```
less
KopyalaDüzenle
        [Manager Node]
              |
     ---------------------
     |         |         |
 [Worker]   [Worker]   [Worker]

```

---

# 🧪 Uygulamalı Docker Swarm Kullanımı

---

## 1️⃣ Swarm Başlat (Manager Node)

```bash
docker swarm init
```

- Swarm başlatılır ve bu node artık bir **Manager** olur.
- Çıkan çıktıda Worker’ların katılması için bir token verilir.

---

## 2️⃣ Worker Node’ları Katmak

Diğer makinelerde çalıştırılır:

```bash
docker swarm join --token SWMTKN-... manager_ip:2377
```

> Not: Tek makinede test için docker-machine veya kind gibi araçlar gerekebilir.
> 

---

## 3️⃣ Swarm Node’larını Görüntülemek

```bash
docker node ls
```

Manager olarak hangi node’lar var, worker’lar aktif mi görürsün.

---

## 4️⃣ Servis Oluşturmak

```bash
docker service create --name web --replicas 3 -p 8080:80 nginx
```

- `web` adında 3 kopyalık bir nginx servisi başlatılır.

Servis bilgileri:

```bash
docker service ls
docker service ps web
```

---

## 5️⃣ Servisi Güncellemek

```bash
docker service update --image nginx:alpine web

```

> Rolling update ile yeni image’a geçilir.
> 

---

## 6️⃣ Servisi Silmek

```bash
docker service rm web
```

---

## 7️⃣ Swarm’dan Ayrılmak

### Worker Node:

```bash
docker swarm leave
```

### Manager Node:

```bash
docker swarm leave --force
```

---

## ⚖️ Swarm ile Compose Arasındaki Fark

| Özellik | Docker Compose | Docker Swarm |
| --- | --- | --- |
| Amaç | Çoklu container yönetimi | Cluster yönetimi |
| Uygulama tipi | Tek makine | Çoklu makine |
| Ölçekleme | Manuel | Otomatik, HA destekli |
| Load Balancing | Yok | Var |

---

- Swarm, **Kubernetes’e geçiş öncesi mantıksal kavramları öğrenmek** için idealdir: service, node, scale, cluster.
- Ancak **gerçek projelerde Kubernetes tercih edilmelidir.**
- Docker Desktop artık Kubernetes'i doğrudan entegre sunar.

# 🧩 Docker Compose: Çoklu Container Yönetimi İçin

---

## 🔍 Docker Compose Nedir?

**Docker Compose**, birden fazla container’dan oluşan uygulamaları **tek bir YAML dosyasıyla tanımlayıp yönetmeyi** sağlayan Docker aracıdır.

---

### 💡 Neden Gerekli?

Uygulamanız sadece bir API değil, bir veritabanı ve frontend’den oluşuyor olabilir. Bunları ayrı ayrı `docker run` komutlarıyla başlatmak karmaşık ve zahmetlidir.

**Docker Compose** sayesinde:

- Tüm servisleri **tek dosyada tanımlar**,
- Tek komutla **hepsini ayağa kaldırır**,
- Ortak ağ ve volume yapılarını **otomatik oluşturur**.

---

## 🧱 Compose Yapısı (Temel Kavramlar)

```yaml
version: "3.8"
services:
  servis_adi:
    image: image_adi
    ports:
      - "host_port:container_port"
    environment:
      - VAR=value
    volumes:
      - host_path:container_path
    depends_on:
      - diger_servis
volumes:
  volume_adi:
networks:
  network_adi:
```

---

## ⚙️ Docker Compose Komutları

| Komut | Açıklama |
| --- | --- |
| `docker compose up` | Servisleri başlatır |
| `docker compose up -d` | Arka planda başlatır |
| `docker compose down` | Servisleri ve ağı durdurur, siler |
| `docker compose down -v` | + Volumeleri de siler |
| `docker compose logs -f` | Log’ları takip eder |
| `docker compose ps` | Çalışan container’ları listeler |
| `docker compose exec <servis> bash` | Bir servisin içine girer |
| `docker compose build` | Dockerfile'ları kullanarak imajları oluşturur |
| `docker compose up --scale api=3` | Servisten çoklu kopya başlatır (örneğin 3 adet `api`) |

---

## 📁 .env Dosyası ile Ortam Değişkenleri

`.env` dosyasına şu şekilde tanımlar yazılır:

```
POSTGRES_USER=admin
POSTGRES_PASSWORD=secret
POSTGRES_DB=mydb
```

`docker-compose.yml` dosyasında bunları şu şekilde çağırabilirsin:

```yaml
environment:
  - POSTGRES_USER=${POSTGRES_USER}
```

---

## 🧠 Compose ile Ağ ve Volume Yönetimi

- **Ağ (network)**: Tüm servisler aynı özel ağda çalışır. Birbirlerine DNS ismi ile erişirler (örneğin: `db:5432`).
- **Volume**: Veritabanı gibi verisi kaybolmasın istenen servisler için kalıcı depolama sağlar.

---

## 🔨 Gerçek Hayattan Bir Uygulama Örneği

Aşağıdaki örnekte:

- `db` → Postgres
- `api` → Go ile yazılmış bir API (örnek olarak `./api` klasöründe bir Dockerfile var)
- `web` → React/HTML uygulaması Nginx ile servis ediliyor

```yaml
version: "3.8"

services:

  db:
    image: postgres:14
    container_name: db
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: mydb
    volumes:
      - db-data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U admin"]
      interval: 10s
      retries: 5
    networks:
      - app-net

  api:
    build: ./api
    container_name: api
    depends_on:
      db:
        condition: service_healthy
    environment:
      DATABASE_URL: postgres://admin:secret@db:5432/mydb
    ports:
      - "5000:5000"
    networks:
      - app-net

  web:
    build: ./frontend
    container_name: web
    depends_on:
      - api
    ports:
      - "8080:80"
    networks:
      - app-net

volumes:
  db-data:

networks:
  app-net:
    driver: bridge
```

---

## 🚀 Uygulama Adımları

### ✅ İlk Kurulum

```bash
docker compose up -d --build
```

### 🔍 Servisleri Görüntüle

```bash
docker compose ps
```

### 🧹 Durdurmak

```bash
docker compose down
```

Verileri de silmek için:

```bash
docker compose down -v
```

---

## 📊 Avantajları

| Avantaj | Açıklama |
| --- | --- |
| 🧩 Modülerlik | Her servis ayrı tanımlanır |
| ⚙️ Otomasyon | Ağ, volume, image işlemleri otomatik |
| 🚀 Taşınabilirlik | Tüm ekip aynı `docker-compose.yml` ile çalışabilir |
| 🔁 Tekrarlanabilirlik | Her yerde aynı yapı tekrar kurulabilir |
| 🧠 Öğrenmesi kolay | YAML söz dizimi sade ve anlaşılır |

---

## 💡 Docker Compose ile Kubernetes Geçişi

Docker Compose dosyaları, küçük ve orta ölçekli uygulamalar için idealdir.

Ancak büyük sistemlerde daha fazla ihtiyaç ortaya çıkar: otomatik yeniden başlatma, hata toleransı, servis keşfi gibi.

Bu durumda **Docker Swarm** veya **Kubernetes** gibi orkestrasyon çözümleri devreye girer.

İyi haber şu ki: Compose dosyaları, `kompose` gibi araçlarla kolayca Kubernetes manifest’lerine dönüştürülebilir.

---

## 📦 Sonuç

Docker Compose:

✅ Geliştiricinin hayatını kolaylaştırır.

✅ Tüm servisleri bir dosyada tanımlayarak yönetimsel yükü azaltır.

✅ Modern mikroservis yapılarının temel taşıdır.
