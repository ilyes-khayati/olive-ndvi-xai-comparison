# olive-ndvi-xai-comparison

Do different model classes explain the same wavelet-decomposed NDVI signal the
same way? XGBoost, Random Forest and Ridge regression are fitted to identical
inputs at a delineated olive orchard in Jendouba, Tunisia, and their feature
attributions compared.

Companion to `olive-ndvi-wavelet-xai`, which reproduces the framework this work
builds on. That repository is frozen; this one is not a reproduction.

This is the olive half of a two-site comparison. The forest half is
[`forest-ndvi-xai-comparison`](https://github.com/ilyes-khayati/forest-ndvi-xai-comparison);
notebooks 01–05 run the same code at both sites (protocol in its README), so
differences between the sites come from the vegetation, not from the pipeline.

## Study area

`olive-jendouba-polygon.geojson` — 0.644 km², delineated by hand on
high-resolution imagery where the olive planting grid is visible. About 10 MODIS
NDVI pixels at 250 m, and 0.64 of one MODIS LST pixel at 1 km.

## Notebooks

01  data acquisition        polygon extraction, MODIS quality screening, SPEI 1-48 months
02  wavelet decomposition   discrete Meyer at native cadence; look-ahead quantified
03  feature derivation      every predictor justified from evidence; drought memory
04  model training          XGBoost, Random Forest, Ridge; noise floor; rolling origin
05  attribution             permutation, drop-column, grouped and SHAP, across models
06  selection               stratified, and Ridge weights as a neutral selector
07  rashomon                explanations across equally good configurations
08  synthetic ground truth  which explanation recovers known importances

Notebooks 01–05 follow the shared two-site protocol. Notebooks 06–08 are olive-only
extensions; their saved outputs come from the earlier protocol (branch `master`)
and have not been re-run on this one.

## Running it

```sh
git clone https://github.com/ilyes-khayati/olive-ndvi-xai-comparison.git
cd olive-ndvi-xai-comparison
python3.12 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m ipykernel install --user --name olive-xai
```

Open the notebooks with the `olive-xai` kernel and run them in order from 02. The
extracted series in `data/raw/` are committed, so no Earth Engine account is needed.
Notebook 01 re-extracts them and needs one:

```sh
earthengine authenticate
export EE_PROJECT=<your Earth Engine project id>
```
