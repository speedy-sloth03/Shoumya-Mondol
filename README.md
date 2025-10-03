# BloomWatch

BloomWatch is a production-ready, globe-first interactive web app that detects and forecasts flowering/bloom events and pollinator risk in Bangladesh using real NASA satellite vegetation indices (VIIRS/MODIS). The app is multilingual (English & Bangla), accessible, colorblind-friendly, and demo-ready.

## Features

- **3D interactive globe** (Cesium) with Bangladesh divisions overlays
- **Division dashboards**: 2D map (Leaflet), NDVI analytics, bloom clusters, heatmap, forecasts
- **NASA data ingestion pipeline**: VIIRS/MODIS NDVI, QA masking, clustering, seasonal forecasting
- **Multilingual**: Instant EN/BN toggle (i18next)
- **Accessibility**: Keyboard navigation, ARIA, colorblind mode, screen-reader friendly
- **OAuth2**: Google login
- **Exports**: Download CSV/PNG
- **Guided demo tour**: 60s walkthrough
- **Offline demo mode**: Sample Bangladesh data provided
- **Fully dockerized**: One-command local run
- **Tests & QA**: Backend (pytest), Frontend (Jest/RTL), QA-PASSED.md included

## Quick Start (Local Demo)

1. **Clone the repo**:
   ```sh
   git clone https://github.com/speedy-sloth03/BloomWatch.git
   cd BloomWatch
   ```

2. **Set up environment**:
   - Copy and fill `.env.example` as `.env` in `/backend` and `/frontend`.
   - For demo, test Google OAuth client IDs are provided; replace with your own for production.

3. **Run locally** (Docker Compose):
   ```sh
   docker-compose up --build
   ```
   - Frontend: [http://localhost:3000](http://localhost:3000)
   - Backend: [http://localhost:8000/docs](http://localhost:8000/docs) (Swagger UI)

4. **Test**:
   ```sh
   docker-compose exec backend pytest
   cd frontend && npm test
   ```

## Directory Structure

```
bloomwatch/
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── api/
│   │   │   ├── regions.py
│   │   │   ├── blooms.py
│   │   │   └── forecast.py
│   │   ├── services/
│   │   │   ├── nasa_ingest.py
│   │   │   ├── preprocess.py
│   │   │   └── algorithms.py
│   │   └── models/
│   ├── tests/
│   └── Dockerfile
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── App.tsx
│   │   ├── index.tsx
│   │   ├── pages/GlobeHome.tsx
│   │   ├── pages/Dashboard.tsx
│   │   ├── components/Map2D.tsx
│   │   ├── components/CesiumGlobe.tsx
│   │   ├── i18n/
│   │   │   ├── en.json
│   │   │   └── bn.json
│   │   └── styles/
│   ├── tests/
│   └── Dockerfile
├── data/
│   ├── sample_bangladesh.geojson
│   └── sample_ndvi_timeseries.json
├── docker-compose.yml
├── README.md
├── demo/
│   ├── interactive-map.html
│   └── video.mp4
└── docs/
    ├── technical-documentation.md
    ├── impact-story.md
    └── QA-PASSED.md
```

## Environment Variables

See `/backend/.env.example` and `/frontend/.env.example` for required variables:
- NASA LAADS credentials
- Google OAuth client IDs
- CORS origins, etc.

## Demo Data

Sample data for Bangladesh included in `/data/`. The app will run fully offline for demo with these files.

## Production & Security

- Use HTTPS and secure cookies in prod.
- Never commit your real secrets—use `.env.example`.
- Replace test OAuth client IDs with your own.

## References

- [Leaflet.js](https://leafletjs.com/)
- [Cesium 3D Earth Map](https://github.com/fengsiyu/cesium-3D-Earth-Map)
- [NASA Earthdata](https://earthdata.nasa.gov/)
- [prophet (forecasting)](https://facebook.github.io/prophet/)

---

For detailed technical docs and impact story, see `/docs/technical-documentation.md` and `/docs/impact-story.md`.
