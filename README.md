# Indonesian Chatbot (Flask)

Chatbot berbahasa Indonesia berbasis klasifikasi intent, dilayani lewat antarmuka web Flask.

Dibuat pada program **AI for Jobs - Orbit Future Academy (MSIB Batch 3)**, 2022.

## Cara kerja

1. Kalimat pengguna dikirim ke endpoint `/get?msg=...`
2. Teks ditokenisasi dan dilemmatize dengan NLTK WordNetLemmatizer, lalu dipadding ke panjang tetap 10 token
3. Model Keras memprediksi **tag intent** dari kalimat tersebut
4. `LabelEncoder` menerjemahkan hasil prediksi kembali ke nama intent
5. Aplikasi memilih satu jawaban secara acak dari daftar respons milik intent itu

Pasangan intent, pola kalimat, dan responsnya didefinisikan di `dataset/Intent_KM.json`.

## Teknologi

Python - Flask - TensorFlow/Keras - NLTK - scikit-learn

| Berkas | Isi |
|---|---|
| `model/chat_model.h5` | model klasifikasi intent (Keras) |
| `model/tokenizer.pkl` | tokenizer teks |
| `model/labelencoder.pkl` | encoder label intent |
| `dataset/Intent_KM.json` | daftar intent, pola kalimat, dan respons |

## Menjalankan secara lokal

```bash
cd "28 SEPTEMBER"
pip install -r requirements.txt
python app.py
```

Lalu buka http://127.0.0.1:5000

Saat pertama dijalankan, fungsi `preparation()` otomatis mengunduh paket NLTK yang dibutuhkan.

Dependensi dipatok ke versi tahun 2022 (TensorFlow 2.9.1, Flask 2.0.0), jadi paling aman dijalankan di Python 3.10 atau lebih lama.

## Struktur

```
28 SEPTEMBER/
|- app.py            server Flask, route / dan /get
|- process.py        preprocessing teks dan generate_response()
|- model/            chat_model.h5, tokenizer.pkl, labelencoder.pkl
|- dataset/          Intent_KM.json
|- templates/        antarmuka chat
|- static/
|- requirements.txt
```

Laporan lengkap proyek ada di `chatbot28sep.pdf`.
