# HPC Ortamında Singularity Sandbox Kullanımı (Best Practice)

### 📦 1. Sandbox İmajı Oluşturma
**Neden**

Sandbox, .sif dosyası gibi salt-okunur değil; bir klasör olarak saklandığı için içine paket ekleyebilir, dosya düzenleyebilirsiniz.

```bash
singularity build --sandbox ml_env docker://ubuntu:22.04
```

<ml_env> → İmajın saklanacağı klasör adı

<docker://ubuntu:22.04> → Temel alınan imaj (istenirse Debian, CentOS vb. olabilir)


