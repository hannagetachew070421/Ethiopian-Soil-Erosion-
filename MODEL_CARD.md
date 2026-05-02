
# Ethiopian Highlands Erosion Prediction Model
## Production Model Card v1.0.0

### MODEL OVERVIEW
- **Model Type**: CatBoost Gradient Boosting Regressor
- **Target**: Annual Soil Loss (t/ha/yr) - Ethiopia-Modified RUSLE
- **Training Date**: 2026-04-27
- **Framework**: CatBoost + scikit-learn

### PERFORMANCE METRICS
| Metric | Value | Assessment |
|--------|-------|------------|
| R² | 0.926 | Excellent |
| RMSE | 5.43 t/ha/yr | Within field uncertainty |
| MAE | 3.14 t/ha/yr | Precise for planning |
| Mean Reliability | 73.5% | Good confidence |
| Within ±5 t/ha/yr | 76.3% | Reliable envelope |

### INTENDED USE
- Conservation prioritization in Ethiopian Highlands
- SLM (Sustainable Land Management) planning
- Green Legacy initiative support
- Target regions: Northern Shewa, Amhara, Oromia

### LIMITATIONS
1. Dry season NDVI bias (corrected with seasonal scaling)
2. Extreme slope uncertainty (>50°) - flag for review
3. Curvature artifacts in 45.6% of data (documented)
4. P-factor assumed 1.0 (conservative estimate)
5. Not validated outside Ethiopian Highlands

### INPUT FEATURES
- Terrain: Elevation, Slope, Aspect, Curvature, TWI, TRI, TPI
- Climate: Annual Rainfall (mm)
- Vegetation: NDVI (seasonally corrected)
- Soil: Soil Type (FAO classification)
- Land Use: Land cover class
- Hydrology: Drainage Density

### OUTPUT
- Prediction (t/ha/yr)
- Lower/Upper bounds (uncertainty interval)
- Risk class (Very Low to Critical)
- Reliability score (0-100%)
- Quality flags (high_risk, critical, requires_review)

### DEPLOYMENT ARTIFACTS
- catboost_erosion_model.joblib
- feature_scaler.joblib
- label_encoders.joblib
- feature_columns.json
- seasonal_correction_config.json
- extreme_value_config.json
- reliability_layer_config.json
- terrain_artifact_config.json
- pipeline_metadata.json

### MONITORING REQUIREMENTS
- Input drift detection (PSI > 0.1 alert)
- NDVI mean tracking (alert if shift >0.05)
- Prediction distribution monitoring
- Quarterly spatial validation

### CONTACT
Production ML Team
Ethiopian Highlands Erosion Project
