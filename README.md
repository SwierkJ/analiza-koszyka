# Analiza koszyka: reguły asocjacyjne (EconoShop Express)

Eksploracja danych, laboratorium 6. Dane syntetyczne: 7 968 paragonów sklepu osiedlowego z września i października 2026 r. (`dane/paragony.csv`, jeden wiersz = jeden produkt na paragonie).

| Plik | Co to jest |
|---|---|
| `koszyk.py` | funkcje: macierz koszyków, wsparcie, pewność, lift, Apriori, scenariusz zysku (TODO 1–3 do uzupełnienia) |
| `tests/test_koszyk.py` | testy (`pytest -q`); na start `7 failed`, po TODO 1–3 `7 passed` |
| `lab6_student.ipynb` | notatnik z zadaniami Z1–Z6 |
| `app.py` | dashboard Streamlit |
| `render.yaml` | wdrożenie na Render |
| `.devcontainer/` | konfiguracja GitHub Codespaces (Python 3.13 i biblioteki instalują się same) |
| `.github/workflows/testy.yml` | testy na GitHubie po każdym push |

## 1. Praca w GitHub Codespaces

1. **Code → Codespaces → Create codespace on main**; poczekaj na koniec instalacji.
2. W terminalu: `pytest -q`, uzupełnij TODO 1–3 w `koszyk.py`, aż zobaczysz `7 passed`.
3. Otwórz `lab6_student.ipynb` → **Select Kernel → Python 3.13** → uruchamiaj komórki po kolei (Shift + Enter).
4. `streamlit run app.py` → **Open in Browser** (albo zakładka PORTS → 8501).

## 2. Zapis zmian

Panel **Source Control** → opis → **Commit** → **Sync Changes** (albo `git add .`, `git commit -m "..."`, `git push`). Zakładka **Actions**: zielony znaczek = testy przechodzą.

## 3. Render

**New → Blueprint** → **Connect** przy tym repozytorium → **Deploy Blueprint**. Ręcznie: **New → Web Service**, Build `pip install -r requirements.txt`, Start `streamlit run app.py --server.port $PORT --server.address 0.0.0.0 --server.headless true`, zmienna `PYTHON_VERSION` = `3.13.5`. Usługa Free usypia po 15 min bez ruchu.

## 4. Rekomendacja dla kierownika sklepu

# Analiza koszyka — EconoShop Express

Aplikacja dostępna pod adresem: https://twoja-nazwa-aplikacji.onrender.com

## Rekomendacja dla kierownika sklepu

Na podstawie analizy 7 968 paragonów rekomenduję podjęcie działań dla dwóch silnych reguł asocjacyjnych. Pierwszą z nich jest `makaron -> sos pomidorowy` (207 wspólnych paragonów, pewność 0,312, lift 5,97), dla której zalecam ustawienie sosu pomidorowego na półce bezpośrednio obok makaronu bez wprowadzania jakichkolwiek rabatów. Rabat 20% wygenerowałby stratę w wysokości -273,80 zł w ciągu 2 miesięcy z uwagi na dopłacanie do 207 klientów, którzy i tak kupują oba produkty, podczas gdy sama zmiana ekspozycji przyniesie szacunkowo +47,99 zł czystego zysku. Drugą rekomendowaną regułą jest `pieluchy -> chusteczki nawilżane` (108 paragonów, pewność 0,307, lift 6,33), gdzie warto wprowadzić stałą ofertę zestawu promocyjnego przy kasach. Zdecydowanie nie polecam wdrażania akcji promocyjnej na regułę `węgiel drzewny -> kiełbasa` — mimo wysokiego liftu we wrześniu (6,94 na 117 paragonach), reguła ta w październiku spadła do zaledwie 2 paragonów i uległa przedawnieniu w wyniku pułapki sezonowości po zakończeniu sezonu grillowego. Skuteczność proponowanej zmiany ekspozycji sosu przy makaronie zweryfikujemy poprzez test A/B: w połowie sklepów ustawiamy sos obok makaronu, a drugą połowę pozostawiamy bez zmian, porównując po 4 tygodniach średnią sprzedaż sosu przypadającą na 100 paragonów z makaronem.
