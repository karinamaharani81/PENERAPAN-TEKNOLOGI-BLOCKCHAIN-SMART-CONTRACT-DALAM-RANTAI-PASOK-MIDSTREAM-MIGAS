# 🛢️ PENERAPAN-TEKNOLOGI-BLOCKCHAIN-SMART-CONTRACT-DALAM-RANTAI-PASOK-MIDSTREAM-MIGAS 📦
Proyek ini mengintegrasikan sensor industri dengan sistem penyimpanan data time-series (InfluxDB), visualisasi real-time (Grafana & PyQt), dan pencatatan terdesentralisasi menggunakan teknologi Blockchain Ethereum dan Smart Contract. Tujuan utamanya adalah untuk meningkatkan akurasi, transparansi, dan efisiensi pencatatan data pada rantai pasok midstream migas.

## Anggota Kelompok
1. Muhammad Hadid Qushairi (2042231025)
2. Karina Lailatul Maghfiroh Maharani (2042231035)
3. Greista Tezar Rizki Saputra (2042231079)
4. Ahmad Radhy, S.Si., M.Si. (Dosen Pengampu)

Teknik Instrumentasi - Institut Teknologi Sepuluh Nopember

## 🛠️ Step by Step Eksekusi Sistem
1. Jalankan Program Sensor
``` bash
cd Tubes-ISI
cd sensor
cargo run
```
Sensor akan mengirim data suhu dan kelembaban secara berkala ke server melalui TCP.

2. Jalankan Ganache untuk Blockchain
``` bash
# Terminal baru
cd Tubes-ISI
ganache
```
Akan muncul 10 address dan private key untuk digunakan di Metamask.

3. Jalankan Server & Deploy Smart Contract
``` bash
cd Tubes-ISI
cd Server
```
Buka file main.rs dan ganti wallet address dengan address Ganache
``` bash 
let wallet: LocalWallet = "0x...".parse::<LocalWallet>()?
```
Lalu jalankan:
``` bash
cargo run
```

✅ Output di terminal:
```
✅ Smart contract deployed at: 0xef9ec8f88f74cbac54b9e0065057de6c0b367570
🚪 TCP Server listening on port 9000...
📥 Received sensor data: ...
✅ InfluxDB: data written
📡 Ethereum: tx sent: ...
```

4. Edit File Web Dashboard
``` bash
cd Web31
```

Buka file script.js dan ubah:
``` bash
const contractAddress = "0xef9ec8f88f74cbac54b9e0065057de6c0b367570";
```

5. Jalankan Web Server
``` bash
python3 -m http.server 6969
```
Akses browser ke: http://localhost:6969

6. Simulasi Transaksi Web3
- Buka Metamask, import private key dari Ganache
- Klik Load Sensor Data
- Masukkan nilai suhu dan kelembaban target
- Klik Simulate Purchase
- Sistem akan menampilkan QR code dan total ETH simulasi

## 📸 Hasil Tampilan Sistem
### Dashboard Web3
![image](https://github.com/user-attachments/assets/c8323706-b905-4515-87f4-817a897e185c)
![image](https://github.com/user-attachments/assets/011ac371-f5a0-4b7d-a8d0-7a56fefcabf9)

Gambar di atas menunjukkan tampilan dari Web3 Sensor Dashboard berbasis web yang terhubung dengan data dari smart contract di blockchain Ethereum yang menyajikan data dalam bentuk tabel, yang berisi informasi waktu (timestamp), ID sensor, lokasi (misalnya Mobil Tanki 1), tahap proses (Stage), serta nilai suhu dan kelembaban. Tampilan ini memudahkan pengguna untuk melihat log data sensor secara historis.

### Tampilan Data Explorer InfluxDB
![image](https://github.com/user-attachments/assets/bac6a5a2-894b-4409-89d7-afeb6ebef000)

Gambar tersebut menunjukkan tampilan InfluxDB Data Explorer yang digunakan untuk melakukan query data sensor berbasis waktu. Dalam tampilan tersebut, user sedang menuliskan perintah untuk mengambil data dari bucket bernama "tugas3", menyaring data berdasarkan measurement "monitoring" dan field "temperature", serta menampilkan hasilnya. Grafik di bagian atas belum menampilkan visualisasi karena kemungkinan data belum tersedia dalam rentang waktu yang ditentukan. Antarmuka ini digunakan untuk menganalisis data suhu dan kelembaban yang dikirim oleh sensor secara real-time maupun historis.

 ### Tampilan Dashboard Grafana
![image](https://github.com/user-attachments/assets/a57c0bb7-c7cb-499a-97a6-baa47c504a58)

Gambar tersebut menunjukkan tampilan Grafana Dashboard yang digunakan untuk memvisualisasikan data suhu dan kelembaban secara real-time. Pada panel grafik di bagian atas, terlihat dua garis data yang menunjukkan nilai suhu dan kelembaban yang stabil selama rentang waktu lima menit terakhir. Di bagian bawah terdapat editor query yang menggunakan untuk mengambil data dari bucket "tubes", dengan filter field "temperature" dan "humidity". Tampilan ini membantu pengguna memantau kondisi lingkungan secara langsung dan mudah dipahami dalam bentuk grafik.

### Tampilan PyQT
![image](https://github.com/user-attachments/assets/ade0dbe0-dd11-4741-a640-7b92470ea076)

Gambar tersebut merupakan tampilan antarmuka GUI PyQt dari aplikasi monitoring sensor SHT20 yang terhubung ke InfluxDB. Aplikasi ini menampilkan data suhu dan kelembaban secara real-time di bagian atas dengan nilai numerik yang diperbarui terus-menerus. Di bawahnya terdapat dua grafik: Grafik Suhu dengan titik-titik merah dan Grafik Kelembaban dengan garis dan simbol biru, masing-masing menampilkan tren nilai selama beberapa detik terakhir.

### Tampilan Blockchain Container Purchase Dashboard
![image](https://github.com/user-attachments/assets/b354dade-ec92-4d71-b005-cf596b20cb27)

Gambar diatas merupakan tampilan dari Blockchain Container Purchase Dashboard, yaitu antarmuka berbasis web yang dirancang untuk mensimulasikan pemesanan kontainer berdasarkan kondisi lingkungan (suhu dan kelembaban) yang dicatat oleh sensor dan disimpan ke dalam blockchain. Pada dashboard terdapat form simulasi pemesanan, di mana pengguna dapat memasukkan nama, tanggal, jumlah container, serta suhu dan kelembaban yang diinginkan. Setelah tombol "Filter & Simulate Purchase" ditekan, sistem akan mencari data sensor dari blockchain yang sesuai dengan kriteria tersebut. Jika data cocok ditemukan, akan muncul QR Code simulasi pembayaran dan informasi jumlah total ETH yang harus dibayar sebagai bagian dari simulasi transaksi.


![image](https://github.com/user-attachments/assets/5d6d9f7a-fec1-4e3b-8d0d-5e1b6278868e)

Gambar diatas menunjukkan tampilan tabel data sensor yang memuat timestamp, ID sensor, lokasi, tahap proses, suhu, dan kelembaban dari hasil pembacaan sensor. Seluruh data ini berasal dari event `DataStored` dalam smart contract Ethereum. Di bagian paling bawah, terdapat grafik suhu dan kelembaban yang divisualisasikan secara real-time, memudahkan pengguna memantau kondisi aktual dan mendeteksi perubahan yang signifikan seperti lonjakan suhu. Tampilan tersebut tidak hanya menyajikan informasi monitoring lingkungan secara transparan, tetapi juga mengilustrasikan integrasi antara data IoT dan sistem transaksi berbasis blockchain dalam konteks logistik dan pengiriman.
## Struktur Direktori Proyek
```
Tubes-ISI/
├── sensor/                   # Program pembacaan data sensor (Rust)
│   └── src/
│       └── main.rs           # Program utama pembacaan sensor & pengiriman TCP
│   └── Cargo.toml
│
├── Server/                   # TCP Server + Smart Contract (Rust)
│   └── src/
│       └── main.rs           # Deploy smart contract, terima data TCP, kirim ke Influx & Blockchain
│   └── Cargo.toml
│
├── Web31/                    # Dashboard Web3 (HTML + JS)
│   ├── index.html            # Antarmuka utama dashboard sensor
│   ├── script.js             # Koneksi smart contract & blockchain
│   └── style.css             # Styling halaman dashboard
│
├── gui.py                    # PyQt GUI untuk visualisasi lokal
├── README.md                 # Dokumentasi proyek
│
├── docs/                     # Dokumentasi dan presentasi
│   ├── Laporan_Akhir_Kelompok1.pdf
│   └── Presentasi_Kelompok1.pptx
│
├── images/                   # Gambar hasil tampilan sistem
│   ├── dashboard-web3.png
│   ├── gui-monitor.png
│   └── terminal-output.png
│
└── .gitignore
```
