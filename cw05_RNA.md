# RNA

W tym ćwiczeniu będziemy pracować z ERNIE-RNA, jednym z dużych modeli RNA: [Yin et al. 2025](https://doi.org/10.1038/s41467-025-64972-0)

Artykułowi towarzyszy kod, do którego na użytek ćwiczeń zostały dodane skrypty ułatwiające instalację, pobranie modeli i wizualizację: https://github.com/marekb-sci/ERNIE-RNA/tree/main

## 1. Instalacja

Instalacja i pobranie wag wg intruckji z repozytorium


## 2. Przykłady z repozytorium

Sprawdzenie czy skrypty działają, zapoznanie się z ich wynikami.

Każdy skrypt ma opcję `-h` zwracającą argumenty

1. Embeddingi
    - co model zwraca
    - wizualizacja atencji w notatniku `view_results.ipynb` 


2. Predykcja struktury drugorzędowej
    - pliki wyjściowe `.ct` są plikami tekstowymi

3. Predykcja bliskości 3D
    - wynikiem są pliki `.npy` i wykresy

4. Predykcja MRL (powinowactwa rybosomów)


## 3. Własne przykłady

1. kodujące RNA: https://www.ensembl.org (gen -> "transcript table")

2. niekodujące RNA: https://rnacentral.org/

## 4. Wykorzystanie embeddingów ERNIE

Klasyfikacja transkryptów (sekwencji RNA) wg gatunku

Należy pobrać dane skryptem `download_classification_dataset.py`

Przykład wykorzystania znajduje się w notatniku `knn_classification.ipynb`