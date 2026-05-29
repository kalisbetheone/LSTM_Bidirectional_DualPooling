# Deep Learning-based Malware Detection using Sequential API/Syscall Data

Reproduce & Extend: Catak et al., PeerJ Comput. Sci. 6:e285 (2020)

## Tong quan

Project nay thuc hien:

1. **Thu nghiem lai bai bao goc** — Reproduce ket qua phan loai ma doc bang LSTM tren tap Mal-API-2019 (Windows API calls, 8 lop)
2. **Ung dung LSTM tren dataset moi** — Ap dung kien truc LSTM goc va de xuat LSTM Bidirectional-DualPooling tren CICMalDroid2020 (Linux syscalls, nhi phan)
3. **So sanh da mo hinh** — Danh gia 6 mo hinh (LSTM Goc, LSTM Bi-DualPooling, MalBERT, TCN-ATT, Random Forest, XGBoost) tren CICMalDroid2020

## Cau truc thu muc

```
PJ_ATDD/
├── README.md
├── dataset/
│   ├── mal-api-2019.rar          # Mal-API-2019: 7,107 mau, 8 lop ma doc
│   └── CIC-MalDroid2020.rar      # CICMalDroid2020: 11,598 mau, 5 lop
├── src/
│   ├── lstm_malware_full_demo.ipynb        # Notebook 1: Reproduce bai bao goc
│   ├── lstm_cic_comparison.ipynb           # Notebook 2: LSTM Goc vs Bi-DualPooling
│   └── multimodel_malware_detection.ipynb  # Notebook 3: So sanh 6 mo hinh
└── figure/
    ├── class_distribution.png              # Phan phoi 8 lop Mal-API-2019
    ├── fig_compare_*.png                   # So sanh ket qua voi bai bao goc
    ├── fig_cic_*.png                       # Bieu do CICMalDroid2020
    ├── fig_multi_*.png                     # So sanh 6 mo hinh
    ├── fig_a3_*.png                        # Phu luc 3 — phan tich chi tiet
    ├── single_lstm_*.png                   # Ket qua Single-layer LSTM
    ├── two_lstm_*.png                      # Ket qua Two-layer LSTM
    ├── lstm_original.png                   # LSTM Goc tren CICMalDroid
    ├── lstm_improved.png                   # LSTM Bi-DualPooling tren CICMalDroid
    └── comparison_lstm.png                 # So sanh ROC + CM
```

## Notebooks

### 1. `lstm_malware_full_demo.ipynb` — Reproduce bai bao

- **Dataset:** Mal-API-2019 (7,107 mau, 8 lop ma doc, 280 unique API calls)
- **Mo hinh:**
  - 8 binary LSTM (1-vs-rest) — Table 1 bai bao
  - Single-layer LSTM da lop — Table 3-5
  - Two-layer LSTM da lop — Table 6-8
- **Ket qua:** Tuong duong bai bao goc (chenh lech ±5% F1)

### 2. `lstm_cic_comparison.ipynb` — LSTM tren CICMalDroid2020

- **Dataset:** CICMalDroid2020 (9,449 mau sau dedup/filter, nhi phan: Benign vs Malware)
- **Mo hinh:**
  - LSTM Goc (Catak et al.): Acc=0.9291, F1=0.9602, AUC=0.8796
  - LSTM Bidirectional-DualPooling: Acc=0.9704, F1=0.9831, AUC=0.9917
- **Cai tien:** BiLSTM + GlobalMaxPool/AvgPool thay Flatten, BatchNorm, SpatialDropout1D

### 3. `multimodel_malware_detection.ipynb` — So sanh 6 mo hinh

| Mo hinh | Loai | F1 | AUC | Train time |
|---------|------|----|-----|------------|
| LSTM Goc | DL | 0.9568 | 0.8320 | 347.5s |
| LSTM Bi-DualPooling | DL | 0.9821 | 0.9859 | 133.9s |
| MalBERT | DL | 0.9591 | 0.9538 | 170.8s |
| TCN-ATT | DL | 0.9767 | 0.9804 | 69.0s |
| Random Forest | ML | 0.9916 | 0.9985 | 0.9s |
| XGBoost | ML | 0.9935 | 0.9978 | 0.8s |

## Datasets

### Mal-API-2019
- **Nguon:** Catak et al. — [GitHub](https://github.com/ocatak/malware_api_class)
- **Nen tang:** Windows API calls
- **So mau:** 7,107
- **So lop:** 8 (Adware, Backdoor, Downloader, Dropper, Spyware, Trojan, Virus, Worms)

### CICMalDroid2020
- **Nguon:** Canadian Institute for Cybersecurity
- **Nen tang:** Android (Linux syscalls)
- **So mau:** 11,598 (CSV) / 9,449 (PKL — sau dedup + filter log loi)
- **So lop:** 5 (Adware, Banking, Benign, Riskware, SMS) → nhi phan: Benign vs Malware

## Moi truong

- Python 3.x, Google Colab (GPU T4/A100)
- TensorFlow 2.20, Keras
- scikit-learn, XGBoost, seaborn, matplotlib

## Tai lieu tham khao

- Catak, F.O., et al. (2020). "Deep learning based Sequential model for malware analysis using Windows exe API Calls." PeerJ Comput. Sci. 6:e285.
