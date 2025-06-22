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
