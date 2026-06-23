# 🌱 AgriSmart — Système intelligent d'aide à la décision agricole

## Architecture
- **MODULE 1** : Classification (Random Forest) → recommande la meilleure culture parmi 22
- **MODULE 2** : Régression (Random Forest) → estime le rendement en t/ha (données FAO 1961–2016)

## Lancement

```bash
cd projet_ML_akhirversion/app
pip install -r ../requirements.txt
python app.py
# Ouvrir http://127.0.0.1:5000
```

## Corrections apportées (v2)
1. **app/app.py** connecté aux vrais modèles ML (artifacts/*.pkl) via utils/predictor.py
2. **Prédiction** : formulaire → API `/api/predict` → résultats dynamiques inline (plus de page séparée fake)
3. **Dashboard** : données réelles du dataset par défaut (2 200 cultures + FAO 56 717 rendements), mis à jour après chaque prédiction
4. **Pays** : liste complète des 212 pays du modèle de régression (au lieu de 6 pays hardcodés)
5. **Années** : 1961–2030 (données FAO 1961–2016 + extrapolation)
6. **Historique** : stockage JSON des prédictions réelles avec tous les champs (culture, rendement, rating, pays, paramètres)
7. **Classifier** : utilise DataFrame pandas pour éviter le warning sklearn
8. **Dashboard charts** : rendements moyens réels FAO par culture, tendances décennales réelles, conditions climatiques moyennes du dataset

## Datasets
- `data/Crop_recommendation.csv` : 2 200 exemples, 22 cultures, 7 features (N,P,K,T,H,pH,Pluie)
- `data/yield.csv` : 56 717 enregistrements FAO, 10 cultures, 212 pays, 1961–2016
