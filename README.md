# Opineo Reviews Classifier
Available only in polish language

## Opis projektu
Projekt jest klasyfikatorem opinii i ocen użytkowników pochodzących z serwisów Opineo, Twitter oraz YouTube, napisanych w języku polskim. Projekt ma na celu klasyfikację opinii jako pozytywne, neutralne oraz negatywne. Ponadto, projekt ma na celu ukazanie tematów najczęściej poruszanych w recenzjach.

## Spis treści

1. [Cel analizy](#cel-analizy)
2. [Struktura projektu](#struktura-projektu)
3. [Baza danych](#baza-danych)
4. [Zastosowane narzędzia](#zastosowane-narzedzia)
5. [Wstępna eksploracja danych](#wstępna-eksploracja-danych)
6. [Przygotowanie danych do modelowania](#przygotowanie-danych-do-modelowania)
7. [Modele klasyfikacji tematycznej(LDA, LSI, HDP)](#modele-klasyfikacji-tematycznej)
8. [Mocne i słabe strony modelu](#mocne-i-słabe-strony-modelu)
9. [Potenjalne kierunki rozwoju](#potencjalne-kierunki-rozwoju)
10. [Podsumowanie i wnioski](#podsumowanie-i-wnioski)
11. [Instrukcja instalacji](#instrukcja-instalacji)

## Cel analizy
1. Wyodrębnienie istotnych elementów z perspektywy klienta. Na co klienci zwracają uwagę?
2. Budowa modelu klasyfikacyjnego, który będzie przypisywał temat wypowiedzi do opinii klienta.

## Struktura projektu
Projekt składa się z trzech głównych części:
1. **Jupyter Notebook**: `code.ipynb` - plik zawiera kod użyty do przeprowadzenia analizy
2. **Dokument PDF**: `project_presentation.pdf` - plik zawiera szczegółową prezentację projektu  
3. **Zbiory danych niezbędnych do przeprowadzenia analizy**: 'polishstopwords.csv' oraz 'polish_sentiment_dataset.csv' (UWAGA. Zbiór 'polish_sentiment_dataset.csv' należy samodzielnie pobrać z dysku Google wskazanego w następnym rozdziale)

## Baza danych
Baza danych zawiera informacje o treści recenzji wydanych przez użytkowników oraz ich ocenie firmy:
- **Ocena 1** - oznacza ocenę pozytywną
- **Ocena 0** - oznacza ocenę neutralną
- **Ocena -1** - oznacza ocenę negatywną

Bazę danych należy samodzielnie pobrać pod adresem: [link](https://drive.google.com/file/d/1vXqUEBjUHGGy3vV2dA7LlvBjjZlQnl0D/view). Wspomniana baza danych pochodzi bezpośrednie z następującego repozytorium Github [link](https://github.com/Ermlab/pl-sentiment-analysis)

## Zastosowane narzędzia
- Podstawowa analiza statystyczna
- Analiza „n-gramów”
- Tokenizacja
- Usuwanie „stopwords”
- Stemming, lemmatization
- Bag of words
- Latent Dirichlet Allocation (LDA)
- Hierarchical Dirichlet Process (HDP)
- Latent Semantic Indexing (LSI)
- Współczynnik spójności (coherence score)

## Wstępna eksploracja danych
Struktura opinii:
- Pozytywna: 734 250 (78%)
- Neutralna: 18 547 (2%)
- Negatywna: 183 391 (20%)
- **Suma**: 936 188

Wnioski:
- Widoczna asymetria prawostronna wskazuje na tendencje klientów do formowania relatywnie krótkich wypowiedzi.
- Wysoka wariancja informuje o dużym zróżnicowaniu pod względem długości wypowiedzi.
- Dane zagregowane do słów są bardziej interpretowalne. Połowa klientów używa od 6 do 14 słów w swojej wypowiedzi.

## Przygotowanie danych do modelowania
1. Usuwanie braków danych
2. Usuwanie „stopwords” oraz nie-liter (np. znaki interpunkcyjne, liczby)
3. Zamiana na małe litery
4. Lemmatization, stemming
5. Bag of words
6. Tokenizacja

## Modele klasyfikacji tematycznej
### Model LDA
- Początkowo oszacowano model LDA dla 40 tematów.
- Koherencja (coherence score) modelu wyniosła 0.49.
- Dalsza analiza prowadzona była dla modeli z mniejszą liczbą tematów (2, 4).

### Model LSI
- Tworzony w oparciu o 4 tematy.
- Koherencja modelu wyniosła 0.62.

### Model HDP
- Koherencja modelu wyniosła 0.39.

### Porównanie modeli
| Model | Miara koherencji (coherence score) |
|-------|------------------------------------|
| LDA (4 tematy) | 0.56 |
| LSI (4 tematy) | 0.62 |
| HDP | 0.39 |

Finalnie do dalszych predykcji wykorzystano model LSI z 4 tematami.

## Mocne i słabe strony modelu
### Mocne strony
- Dobra jakość modelu, wysoka spójność (coherence score)
- Relatywnie szybka implementacja do nowych danych

### Słabe strony
- Niska interpretowalność zbioru słów w temacie
- Statyczność modelu
- Problem głośnych słów (overfitting to high-frequency words)

## Potencjalne kierunki rozwoju
1. Lemmatization zamiast stemming’u
2. Indywidualne dopasowanie ilości tematów dla modelu
3. Zwiększenie udziału opinii neutralnych oraz negatywnych w próbie do budowy modeli
4. Minimalizacja problemu overfittingu modelu do słów głośnych
5. Dodatkowe usunięcie stopwords
6. Ważenie częstotliwości terminów (TF-IDF)

## Podsumowanie i wnioski
- Cel projektu został spełniony.
- Wykazano, że konsumenci najbardziej cenią sobie szybka realizacja zamówienia, profesjonalizm i szybkość obsługi oraz zgodność zamówionego towaru z jego opisem.
- Najbardziej efektywny model klasyfikacyjny okazał się model LSI.

## Instrukcja instalacji
1. Sklonuj repozytorium:
    ```sh
    git clone https://github.com/TwojeRepozytorium/project.git
    ```
2. Przejdź do katalogu projektu:
    ```sh
    cd project
    ```
3. Zainstaluj wymagane biblioteki:
    ```sh
    pip install -r requirements.txt
    ```
