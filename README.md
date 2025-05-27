# Traefik ile Kubernetes Üzerinde WordPress Dağıtımı

Bu proje, Kubernetes ortamında Traefik ingress controller kullanarak WordPress, MariaDB ve phpMyAdmin servislerinin dağıtımını sağlayan manifest dosyalarını içerir.

## 🚀 Proje Özellikleri

- **Traefik v2.5** - Modern HTTP ters proxy, yük dengeleyici ve Ingress Controller
- **MariaDB 10.6** - WordPress için veritabanı çözümü
- **WordPress** - Popüler içerik yönetim sistemi
- **phpMyAdmin** - Veritabanı yönetim arayüzü
- **RBAC** - Rol tabanlı erişim kontrolü
- **Persistent Storage** - Kalıcı veri depolama çözümleri

## ⚙️ Ön Gereksinimler

1. **Kubernetes Kümesi**:
   - Minikube, k3s veya bulut sağlayıcı (AWS EKS, Google GKE, Azure AKS)
   - Minimum kaynak: 2 CPU, 4GB RAM

2. **Araçlar**:
   - `kubectl` - Kubernetes komut satırı aracı
   - `helm` (isteğe bağlı) - Paket yöneticisi

3. **Depo Erişimi**:
   ```bash
   git clone https://github.com/omandiraci/Traefik-Kubertenes.git
   cd Traefik-Kubertenes
   ```

## 🛠️ Kurulum Adımları

### 1. Manifest Dosyasını Uygulama
```bash
kubectl apply -f manifest.yaml
```

### 2. Dağıtımı Doğrulama
```bash
kubectl get pods -w
```

### 3. Servis Durumunu Kontrol Etme
```bash
kubectl get svc
```

## 📦 Bileşen Detayları

### Traefik Ingress Controller
- **Versiyon**: 2.5
- **Portlar**:
  - `80` HTTP (NodePort: 30080)
  - `443` HTTPS (NodePort: 30443)
  - `8080` Dashboard (NodePort: 30081)
- **Özellikler**:
  - Kubernetes Ingress desteği
  - Canlı yapılandırma güncellemeleri
  - Otomatik TLS sertifikası yönetimi

### MariaDB Veritabanı
- **Versiyon**: 10.6
- **Konfigürasyon**:
  - Veritabanı adı: `wordpress_db`
  - Kullanıcı: `wordpress_user`
  - Şifre: `wordpress_password`
  - Root şifre: `root_password`
- **Depolama**: 1GB kalıcı depolama

### WordPress
- **Versiyon**: En son kararlı sürüm
- **Bağlantılar**:
  - MariaDB servisi ile otomatik bağlantı
- **Depolama**: 1GB kalıcı depolama
- **Ölçeklendirme**: 3 replica pod

### phpMyAdmin
- **Versiyon**: En son kararlı sürüm
- **Özellikler**:
  - MariaDB'ye otomatik bağlanır
  - Root kullanıcı ile giriş yapılabilir

## 🔍 Servislere Erişim

| Servis       | URL                      | Port  |
|--------------|--------------------------|-------|
| Traefik Panosu | http://localhost:30081   | 30081 |
| WordPress    | http://localhost:30082   | 30082 |
| phpMyAdmin   | http://localhost:30083   | 30083 |

## ⚠️ Sorun Giderme

1. **Pod'lar çalışmıyorsa**:
   ```bash
   kubectl describe pod <pod-adı>
   kubectl logs <pod-adı>
   ```

2. **Servislere erişilemiyorsa**:
   - NodePort aralığını kontrol edin
   - Güvenlik duvarı ayarlarını gözden geçirin

3. **Depolama sorunları**:
   ```bash
   kubectl get pvc
   kubectl get pv
   ```

## 📝 Yapılandırma Seçenekleri

`manifest.yaml` dosyasında değiştirilebilecek parametreler:

1. **Kaynak Limitleri**:
   - CPU ve bellek sınırları
   - Replica sayıları

2. **Veritabanı Ayarları**:
   - Kullanıcı adı/şifre
   - Veritabanı adı

3. **Ağ Ayarları**:
   - NodePort değerleri
   - Ingress kuralları

## 📜 Lisans

Bu proje [MIT Lisansı](LICENSE) ile lisanslanmıştır.
