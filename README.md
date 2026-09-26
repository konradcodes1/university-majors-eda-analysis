# University Majors — Exploratory Data Analysis

Eksploracyjna analiza danych (EDA) dotyczących zwrotu z inwestycji w studia. Projekt pokazuje proces poznawania zbioru danych, kontroli jego jakości, porównywania wyników finansowych między kierunkami i kategoriami kierunków oraz prezentowania wyników za pomocą wizualizacji w Pythonie i dashboardu Tableau Public.

**Technologie:** Python, pandas, Matplotlib, Jupyter Notebook / Google Colab, Tableau Public.

[**Zobacz dashboard Tableau**](https://public.tableau.com/views/ROIstudiwwyszychopacalnokierunkw/ROIstudiwwyszych) · [**Otwórz notebook**](https://github.com/konradcodes1/university-majors-eda-analysis/blob/main/majors_eda.ipynb)

> Projekt wykorzystuje dane syntetyczne. Wnioski opisują analizowany zbiór i nie stanowią prognozy zarobków rzeczywistych absolwentów.

## Cel analizy

Analiza odpowiada na następujące pytania:

- Jak różnią się mediana i średnia ROI między kategoriami kierunków?
- W których kategoriach i na których kierunkach najczęściej występuje ujemne ROI?
- Czy wynik całej kategorii dobrze opisuje należące do niej kierunki?
- Czy dane zawierają wartości wymagające dodatkowej weryfikacji?
- Jak koszty studiów, zarobki, odbycie stażu i terminowość ukończenia studiów różnią się między analizowanymi grupami?

Projekt ma charakter opisowy i edukacyjny. Koncentruje się na eksploracji danych, kontroli ich jakości oraz ostrożnej interpretacji obserwowanych zależności.

## Dane i licencja

Źródło: [College Major ROI — Kaggle](https://www.kaggle.com/datasets/sergionefedov/college-major-roi), opublikowane przez użytkownika `sergionefedov`.

**Licencja danych:** [CC0 — Public Domain](https://creativecommons.org/publicdomain/zero/1.0/).

Kopia danych znajduje się w pliku `data/college_major_roi.csv`.

Zbiór zawiera **30 000 rekordów i 18 kolumn**. Dane obejmują m.in. kierunek i kategorię studiów, poziom instytucji, GPA, odbycie stażu, koszty studiów, zadłużenie oraz miary zarobków i ROI w horyzoncie 10 lat.

Najważniejsze zmienne wykorzystywane w analizie:

| Zmienna | Znaczenie |
| --- | --- |
| `major` | Kierunek studiów |
| `major_category` | Kategoria kierunku |
| `institution_tier` | Kategoria instytucji |
| `institution_selectivity_pctile` | Wskaźnik selektywności instytucji; jego zakres wymaga ostrożnej interpretacji |
| `net_roi_usd` | Zwrot netto wyrażony w USD |
| `roi_pct` | Procentowa miara ROI |

Porównania przedstawione w notebooku dotyczą przede wszystkim **`net_roi_usd`**, a nie procentowego ROI. Udział ujemnego ROI jest obliczany jako odsetek rekordów, dla których `net_roi_usd < 0`.

Informacja o CC0 dotyczy źródłowego datasetu. Repozytorium nie zawiera obecnie osobnego pliku licencji dla kodu i dokumentacji.

## Zawartość repozytorium

| Plik | Zawartość |
| --- | --- |
| `majors_eda.ipynb` | Kod analizy, zapisane wyniki, wizualizacje i komentarze |
| `data/college_major_roi.csv` | Źródłowy dataset |
| `README.md` | Opis projektu i instrukcja uruchomienia |

## Zawartość notebooka

1. **Wstępne poznanie danych** — wczytanie CSV, podgląd rekordów, statystyki opisowe, typy danych oraz sprawdzenie kompletności kolumn.
2. **Kontrola zmiennych binarnych** — sprawdzenie rozkładów wartości dla stażu, ukończenia studiów w terminie oraz oznaczeń ROI.
3. **Analiza nietypowych wartości selektywności** — identyfikacja wartości powyżej 100 i porównanie zakresów wskaźnika między kategoriami instytucji.
4. **Porównanie kategorii kierunków** — liczebność grup, mediana i średnia ROI oraz udział ujemnego ROI.
5. **Porównanie poszczególnych kierunków** — zestawienie median ROI i udziałów ujemnych wyników.
6. **Wizualizacja udziału ujemnego ROI** — poziomy wykres słupkowy pokazujący udział rekordów z `net_roi_usd < 0` dla poszczególnych kierunków.
7. **Sprawdzenie struktury kategorii** — ustalenie, które kategorie obejmują pojedynczy kierunek, a które wymagają bardziej szczegółowej analizy.
8. **Dodatkowa eksploracja w Tableau** — analiza kosztów, zarobków, ROI, staży, terminowości ukończenia studiów i zadłużenia według typu instytucji.

## Najważniejsze wyniki

Poniższe wartości pochodzą z tabeli `roi_by_category` zapisanej w notebooku. Średnie zaokrąglono do pełnych USD, a odsetki do dwóch miejsc po przecinku.

| Kategoria | Liczba rekordów | Mediana ROI netto (USD) | Średnia ROI netto (USD) | Ujemne ROI |
| --- | ---: | ---: | ---: | ---: |
| arts | 1 395 | −35 500 | −39 821 | 88,82% |
| humanities | 1 410 | −11 200 | −13 321 | 62,34% |
| education | 1 352 | 8 750 | 11 548 | 41,79% |
| social_science | 5 989 | 22 800 | 31 064 | 33,03% |
| business | 8 361 | 291 700 | 346 099 | 1,57% |
| STEM | 9 904 | 393 350 | 447 000 | 1,31% |
| health | 1 589 | 318 500 | 350 829 | 0,82% |

- **Arts i humanities mają ujemną zarówno średnią, jak i medianę ROI.** Ujemne wyniki dotyczą większości rekordów w obu kategoriach.
- **STEM ma najwyższą średnią i medianę ROI netto spośród analizowanych kategorii.** Najniższy udział ujemnego ROI występuje w kategorii health.
- **Dodatnia mediana nie oznacza, że ujemne wyniki są rzadkie.** W education dotyczą one 41,79% rekordów, a w social_science — 33,03%.
- **Wynik kategorii może ukrywać różnice między kierunkami.** W social_science udział ujemnego ROI wynosi około 48,15% dla psychology, 44,77% dla social_work i 17,11% dla communications.
- **Nie wszystkie kategorie obejmują wiele kierunków.** Arts, humanities, education i health zawierają po jednym kierunku. Porównanie kategorii z odpowiadającym jej kierunkiem nie jest więc niezależnym potwierdzeniem wyniku.

## Wizualizacje

### Udział ujemnego ROI według kierunku — Python

Notebook zawiera poziomy wykres słupkowy przedstawiający odsetek rekordów z `net_roi_usd < 0` dla wszystkich kierunków studiów. Kierunki są uporządkowane według tego odsetka, a słupki opatrzone etykietami procentowymi.

Wykres pokazuje koncentrację ujemnego ROI w wybranych kierunkach:

- `fine_arts`: około **88,8%**;
- `humanities`: około **62,3%**;
- `psychology`, `social_work` i `education`: około **42–48%**.

Wizualizacja ułatwia porównanie kierunków, ale przedstawione zależności dotyczą wyłącznie analizowanego zbioru i nie dowodzą przyczynowego wpływu wyboru kierunku studiów na ROI.

### Dashboard — Tableau Public

[**ROI studiów wyższych | opłacalność kierunków**](https://public.tableau.com/views/ROIstudiwwyszychopacalnokierunkw/ROIstudiwwyszych)

Dashboard rozszerza analizę notebooka o dodatkowe przekroje danych:

- **Macierz opłacalności** — zestawienie średnich kosztów studiów ze średnimi zarobkami w horyzoncie 10 lat.
- **Ranking zwrotu netto** — porównanie średniego `net_roi_usd` między kategoriami kierunków.
- **Czynniki sukcesu** — porównanie średnich zarobków według odbycia stażu i ukończenia studiów w terminie, z podziałem na kategorie kierunków.
- **Obciążenie długiem a prestiż uczelni** — porównanie średniego zadłużenia między kategoriami instytucji.

Notebook dokumentuje wykonane obliczenia, kontrolę jakości danych i interpretacje, natomiast dashboard pozwala interaktywnie przeglądać dodatkowe zależności.

Porównania dotyczące stażu, terminowości ukończenia studiów i kategorii instytucji mają charakter opisowy i nie powinny być interpretowane jako zależności przyczynowe.

## Jakość danych i ograniczenia

Wynik `df.info()` wskazuje brak brakujących wartości we wszystkich 18 kolumnach.

W zmiennej `institution_selectivity_pctile` wykryto **288 rekordów z wartościami 101 lub 102**, czyli **0,96% zbioru**. Wszystkie należą do kategorii `ivy_elite`, której zakres wynosi 90–102.

Notebook pozostawia te rekordy bez zmian i wskazuje możliwy związek ze sposobem konstrukcji syntetycznego wskaźnika. Jest to hipoteza interpretacyjna: spójny zakres wartości nie oznacza, że wartości powyżej 100 są poprawnymi percentylami.

Pozostałe ograniczenia:

- Dane syntetyczne odzwierciedlają założenia ich generatora.
- Porównania grup nie pozwalają ustalić przyczynowego wpływu kierunku studiów na ROI.
- Analiza nie kontroluje jednocześnie kosztów studiów, poziomu instytucji, regionu ani pozostałych cech.
- Zależności obserwowane w dashboardzie nie są modelami predykcyjnymi.
- ROI finansowe nie obejmuje wszystkich korzyści i kosztów związanych ze studiowaniem.

## Uruchomienie lokalne

Wymagane są Python 3 oraz Git.

### 1. Pobierz repozytorium

```bash
git clone https://github.com/konradcodes1/university-majors-eda-analysis.git
cd university-majors-eda-analysis
```

### 2. Utwórz środowisko wirtualne

```bash
python -m venv .venv
```

Aktywacja na macOS / Linux:

```bash
source .venv/bin/activate
```

Aktywacja w Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Zainstaluj zależności

```bash
python -m pip install pandas matplotlib seaborn jupyterlab
```

Repozytorium nie zawiera obecnie pliku z przypiętymi wersjami zależności.

### 4. Uruchom notebook

```bash
jupyter lab
```

Otwórz `majors_eda.ipynb`.

W przypadku uruchamiania notebooka z katalogu głównego repozytorium dane powinny być wczytywane za pomocą:

```python
df = pd.read_csv('data/college_major_roi.csv')
```

Następnie uruchom wszystkie komórki od początku.

## Uruchomienie w Google Colab

1. [Otwórz notebook w Google Colab](https://colab.research.google.com/github/konradcodes1/university-majors-eda-analysis/blob/main/majors_eda.ipynb).
2. Pobierz `data/college_major_roi.csv` z repozytorium i prześlij go do katalogu `/content` przez panel plików Colab.
3. Wczytaj dane za pomocą:

```python
df = pd.read_csv('college_major_roi.csv')
```

4. Uruchom wszystkie komórki od początku.

Otwarcie notebooka bezpośrednio z GitHuba nie pobiera automatycznie datasetu. Po usunięciu środowiska wykonawczego Colab plik trzeba przesłać ponownie.
