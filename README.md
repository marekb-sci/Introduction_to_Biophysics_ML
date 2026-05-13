# Wstęp do biofizyki dla fizyków - uczenie maszynowe


Wykłady są dostępne [na dysku google](https://drive.google.com/drive/folders/18AweUuUDiipEvnmGJknPt-hmnMkNqnMQ?usp=sharing)

## Przygotowanie środowiska

1. Stwórz środowisko wirtualne o nazwie `venv`
    ```bash
    python -m venv venv
    ```

2. Aktywuj środowisko wirtualne
    ```bash
    source venv/bin/activate
    ```

3. Zainstaluj wymagane pakiety
    ```bash
    pip install -r requirements.txt
    ```

4. (Opcjonalnie) po zakończeniu pracy dezaktywuj środowisko:
    ```bash
    deactivate
    ```

### Przygotowanie środowiska z `uv`
`uv` jest narzędziem do zarządzania projektami w Pythonie, które służy jako znacznie szybszy zamiennik  `pip`/`conda`/`venv`. `uv` jest szybszy i oszczędza przestrzeń dyskową. arzędzie to w pełni wspiera tradycyjne pliki `requirements.txt` (jak w tym repozytorium), jak i nowoczesny standard `pyproject.toml`. Więcej: https://docs.astral.sh/uv/

1. Stwórz środowisko wirtualne `.venv` z wybraną wersją Pythona
    ```bash
    uv venv --python 3.11
    ```

2. Aktywuj środowisko wirtualne
    ```bash
    source .venv/bin/activate
    ```

3. Zainstaluj wymagane pakiety
    ```bash
    uv pip install -r requirements.txt
    ```

4. (Opcjonalnie) po zakończeniu pracy dezaktywuj środowisko:
    ```bash
    deactivate
    ```

### Instalacja Jupyter Lab (opcjonalna)

1. Instalacja w środowisku wirualnym
    ```bash
    pip install jupyterlab
    ```

    lub w środowisku wirualnym z `uv`:
    ```bash
    uv pip install jupyterlab
    ```


2. Uruchomienie
    ```bash
    jupyter lab
    ```


