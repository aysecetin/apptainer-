# _HPC Ortamında Singularity Sandbox Kullanımı (Best Practice)_

### 📦 1. Sandbox İmajı Oluşturma
**Neden**

Sandbox, .sif dosyası gibi salt-okunur değil; bir klasör olarak saklandığı için içine paket ekleyebilir, dosya düzenleyebilirsiniz.

```bash
singularity build --sandbox ml_env docker://ubuntu:22.04
```

- ml_env → İmajın saklanacağı klasör adı

- <docker://ubuntu:22.04> → Temel alınan imaj (istenirse Debian, CentOS vb. olabilir)

### 🛠 2. Sandbox’ı Yazılabilir Modda Açma

```bash
singularity shell --writable ml_env
```
📌 Bu modda konteynerin içine girip kalıcı değişiklik yapabilirsiniz.

**Örnek kurulum:**
```bash
apt-get update && apt-get install -y python3 python3-pip git
pip install numpy pandas scikit-learn matplotlib jupyter
```

### 📂 3. Proje Dosyaları ile Çalışma

- Projelerinizi konteyner içine ekleyin:

```bash
mkdir /opt/myproject
cp ~/local_path/train.py /opt/myproject/
```

Veya bind mount kullanarak direkt host’tan erişin:

```bash
singularity exec --bind /host/path:/container/path ml_env python3 /container/path/train.py
```

### ⚡ 4. GPU Desteği (Opsiyonel)
Eğer HPC GPU sunucusu kullanıyorsanız:

```bash
singularity shell --nv --writable ml_env
```
- --nv → NVIDIA GPU sürücülerini konteynere aktarır.

### 📦 5. Son Halini .sif Olarak Paketleme
- Geliştirme bittikten sonra:

``bash
singularity build ml_env.sif ml_env
```
- .sif dosyası salt-okunur ve taşınabilir

- HPC’de paylaşmak ve tekrar çalıştırmak için idealdir.


![Sandbox Kullanım Örneği](assets/sandbox%20kullanım%20örneği.png)

