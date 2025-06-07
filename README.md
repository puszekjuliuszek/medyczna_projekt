# Multimodalna Analiza Zmienności Rytmu Serca

## Opis projektu

Projekt polega na wykonaniu multimodalnej analizy zmienności rytmu serca (HRV) z wykorzystaniem różnych modalności sygnałów kardiologicznych:

- **Elektrokardiografia (EKG)** - klasyczne odprowadzenia sercowe
- **Sejsmokardiografia (SCG)** - akcelerometria powierzchni klatki piersiowej  
- **Żyrokardiografia (GCG)** - żyroskopia powierzchni klatki piersiowej

## Datasety

Projekt wykorzystuje trzy publicznie dostępne datasety:

1. **Mechanocardiograms** (katalog `Surowe/`)
   - Zawiera EKG + akcelerometrię
   - 29 subjects (sub_1.txt - sub_29.txt)
   - Częstotliwość próbkowania: 800 Hz

2. **Cardiac Patients with Valvular Diseases** (katalog `Raw_Recordings/`)
   - Pacjenci z wadami zastawkowymi (CP-XX) i kontrola (UP-XX)
   - EKG (4 odprowadzenia) + akcelerometr + żyroskop
   - Format CSV z sensorów Shimmer

3. **CEBSDB** (opcjonalny - do pobrania)
   - Combined measurement of ECG, Breathing and Seismocardiograms
   - Można pobrać: `wget -r -N -c -np https://physionet.org/files/cebsdb/1.0.0/`

## Instalacja

```bash
pip install -r requirements.txt
```

## Struktura projektu

```
medyczna_projekt/
├── multimodal_hrv_analysis.ipynb  # Główny notebook z analizą
├── requirements.txt               # Zależności
├── README.md                     # Ten plik
├── Surowe/                       # Dataset 1 - Mechanocardiograms
│   ├── sub_1.txt
│   ├── sub_2.txt
│   └── ...
└── Raw_Recordings/               # Dataset 2 - Cardiac Patients
    ├── CP-01-Raw.csv
    ├── CP-02-Raw.csv
    └── ...
```

## Cele projektu

1. **Implementacja detektorów tętna** dla różnych modalności:
   - ECGDetector - detektor zespołów QRS (Pan-Tompkins)
   - SCGDetector - detektor dla sygnałów akcelerometru
   - GCGDetector - detektor dla sygnałów żyroskopu

2. **Analiza HRV** w trzech domenach:
   - Dziedzina czasu: AVNN, SDNN, RMSSD, pNN50
   - Dziedzina częstotliwości: VLF, LF, HF, LF/HF
   - Analiza nieliniowa: wykres Poincaré (SD1, SD2)

3. **Porównanie multimodalne**:
   - Porównanie dokładności detektorów
   - Analiza korelacji między modalnościami
   - Różnice między grupami pacjentów

## Użycie

Uruchom notebook `multimodal_hrv_analysis.ipynb` w środowisku Jupyter:

```bash
jupyter notebook multimodal_hrv_analysis.ipynb
```

## Metodologia

### Detektory

- **ECG**: Algorytm Pan-Tompkins z filtracją pasmową (5-15 Hz)
- **SCG**: Filtracja (1-40 Hz) + wzmocnienie + wygładzenie
- **GCG**: Filtracja (1-20 Hz) + detekcja zmian + wygładzenie

### Analiza HRV

- **Filtracja odstępów RR**: usunięcie wartości <300ms i >2000ms
- **Interpolacja**: dla analizy częstotliwościowej (4 Hz)
- **FFT**: analiza spektralna mocy w pasmach VLF, LF, HF

## Wyniki wstępne

[Miejsce na wstępne wyniki analizy]

## Literatura

1. Pan, Jiapu, and Willis J. Tompkins. "A real-time QRS detection algorithm." IEEE transactions on biomedical engineering 3 (1985): 230-236.

2. Kaisti, M., et al. "Stand-alone heartbeat detection in multidimensional mechanocardiograms." IEEE Sensors Journal 19.1 (2019): 234-242.

3. Task Force of the European Society of Cardiology. "Heart rate variability: standards of measurement, physiological interpretation and clinical use." Circulation 93.5 (1996): 1043-1065.

## Autorzy

[Twoje dane]

## Licencja

[Licencja projektu]