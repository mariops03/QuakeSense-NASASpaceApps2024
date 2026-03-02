# 🌍 QuakeSense

**Real-time seismic event detection system for planetary missions.**

Built for the [NASA Space Apps Challenge 2024](https://www.spaceappschallenge.org/) — **1st Place Winner**.

QuakeSense tackles a critical problem in planetary seismology: filtering genuine seismic events from noise in constrained deep-space communication links. Using real Apollo 12 ALSEP seismometer data (1970–1974), our ML ensemble achieves **97% accuracy** in detecting seismic events, enabling missions to transmit only what matters back to Earth.

## Key Features

- **ML Ensemble Detector** — LightGBM + XGBoost + Logistic Regression with 30+ engineered features (STA/LTA ratios, wavelet energy, spectral entropy, kurtosis)
- **Real-time Pipeline** — Socket.IO streams seismic data through satellite simulator → backend → detector → frontend with sub-second latency
- **3D Solar System Visualization** — Interactive Three.js scene with planetary bodies, satellite orbits, and live seismic event markers
- **Apollo 12 Dataset** — Trained and validated on real lunar seismometer recordings from NASA's ALSEP experiment
- **Satellite Simulator** — Simulates data relay constraints of deep-space missions
- **Fully Dockerized** — One command to spin up all four microservices

## Architecture

```
┌─────────────┐    Socket.IO    ┌─────────────────┐    HTTP     ┌──────────────┐
│  Satellite   │ ──────────────►│    Backend       │ ──────────►│   Detector   │
│  Simulator   │                │  Express / TS    │            │  Flask / ML  │
│  (Flask)     │                │                  │◄────────── │  LightGBM    │
│  :10000      │                │  :10001          │  results   │  :10002      │
└─────────────┘                └────────┬─────────┘            └──────────────┘
                                        │ Socket.IO
                                        ▼
                               ┌─────────────────┐
                               │    Frontend      │
                               │  Vue.js + Three  │
                               │  Nginx :80       │
                               └─────────────────┘
```

## Tech Stack

| Layer | Technologies |
|-------|-------------|
| Frontend | Vue.js 3, Three.js, Chart.js, Socket.IO Client |
| Backend | Express, TypeScript, Socket.IO |
| ML Detector | Python, Flask, LightGBM, XGBoost, scikit-learn, SciPy, PyWavelets |
| Satellite Sim | Python, Flask |
| Infrastructure | Docker, Docker Compose, Nginx |

## Getting Started

```bash
git clone https://github.com/mariops03/QuakeSense.git
cd QuakeSense
docker-compose up --build
```

Open `http://localhost` to access the dashboard.

## Team

| | Name | GitHub |
|---|------|--------|
| 👤 | Daniel Mulas | [@danimulas](https://github.com/danimulas) |
| 👤 | Mario Prieta | [@mariops03](https://github.com/mariops03) |
| 👤 | Diego Borrallo | [@diegoobh](https://github.com/diegoobh) |
| 👤 | Tomas Perez | [@Tomypv](https://github.com/Tomypv) |
| 👤 | Alvaro Sanchez | [@smalvaro](https://github.com/smalvaro) |
| 👤 | David Sanchez | [@DavidSanSan110](https://github.com/DavidSanSan110) |
