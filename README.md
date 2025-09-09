# 🎥 PotPlayer Video Interpolation
**Interpolasi Video untuk PotPlayer menggunakan AviSynth+**

Repositori ini menyediakan skrip dan konfigurasi untuk mengaktifkan interpolasi video dalam **PotPlayer**, meningkatkan kadar bingkai sehingga **120FPS** untuk pengalaman tontonan yang lebih lancar.

## 📌 Keperluan
- **AviSynth+ Latest Release** → [View](https://github.com/AviSynth/AviSynthPlus/releases)
- **PotPlayer (64-bit atau 32-bit)** → [View](https://potplayer.daum.net/)
- **3 file .dll**

## 🛠 Pemasangan

### 1️⃣ Pasang AviSynth+ dan PotPlayer  
- Muat turun dan pasang **AviSynth+ Latest release**  
- Muat turun dan pasang **PotPlayer**  

### 2️⃣ Salin Fail DLL  
- Salin dan tampal **3 fail .dll**:
  ```
  C:\Program Files (x86)\AviSynth+\plugins64
  ```
### 3️⃣ Tetapan PotPlayer  
1. **Buka PotPlayer**  
2. Pergi ke **Preferences > Filter Control > Video Decoder**  
3. Klik **Built-in Video Codec/DXVA Setting**  
4. Aktifkan **Use DXVA**  
5. Pilih **Prioritize D3D11 DXVA**  
6. Pilih **DXVA2 Copy-Back: D3D11 Auto**  
7. Tekan **OK**  

### 4️⃣ Aktifkan AviSynth  
1. Pergi ke **Video > AviSynth**  
2. Aktifkan **Enable AviSynth processing**  
3. Tampal kod berikut dibawah **Load Script**  
4. Tekan **Save**, namakan sebagai **"120fps"**, kemudian tekan **Apply**  

## 🎞 Skrip Interpolasi (120FPS)
```avs
SetMemoryMax(512)
SetFilterMTMode("DEFAULT_MT_MODE", 2)
SetFilterMTMode("FFVideoSource", 3)
potplayer_source()
LoadPlugin("C:\Program Files (x86)\AviSynth+\plugins64\mvtools2.dll")
super=MSuper(pel=1, hpad=0, vpad=0)
backward_1=MAnalyse(super, chroma=false, isb=true, blksize=32, blksizev=32, searchparam=3, plevel=0, search=3, badrange=(-24))
forward_1=MAnalyse(super, chroma=false, isb=false, blksize=32, blksizev=32, searchparam=3, plevel=0, search=3, badrange=(-24))
backward_2 = MRecalculate(super, chroma=false, backward_1, blksize=8, blksizev=8, searchparam=0, search=3)
forward_2 = MRecalculate(super, chroma=false, forward_1, blksize=8, blksizev=8, searchparam=0, search=3)
MBlockFps(super, backward_2, forward_2, num=120, den=1, mode=2)
Prefetch(4)
```

✅ **Selesai!** Kini PotPlayer anda boleh memainkan video dengan interpolasi 120FPS! 🚀

🎬 **Cara Semak FPS**
Mainkan satu video dan tekan **Tab** (Nota: Periksa FPS) dalam PotPlayer untuk menyemak sama ada video berjaya diinterpolasi ke 120FPS.

