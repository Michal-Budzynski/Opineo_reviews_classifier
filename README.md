# Opineo Reviews Classifier

## Opis projektu
Ten projekt jest klasyfikatorem opinii i ocen użytkowników pochodzących z serwisów Opineo, Twitter oraz YouTube, napisanych w języku polskim. 

## Agenda
1. Opis problemu
2. Cel analizy i zastosowane narzędzia
3. Wstępna eksploracja danych
4. Przygotowanie danych do modelowania
5. Modele klasyfikacji tematycznej (LDA, LSI, HDP)
6. Potencjalne kierunki rozwoju
7. Mocne i słabe strony modelu
8. Podsumowanie i wnioski

## Opis problemu
Baza danych zawiera informacje o treści recenzji wydanych przez użytkowników oraz ich ocenie firmy:
- **Ocena 1** - oznacza ocenę pozytywną
- **Ocena 0** - oznacza ocenę neutralną
- **Ocena -1** - oznacza ocenę negatywną

Baza danych: [link](https://github.com/Ermlab/pl-sentiment-analysis)

## Cel analizy
1. Wyodrębnienie istotnych elementów z perspektywy klienta. Na co klienci zwracają uwagę?
2. Budowa modelu klasyfikacyjnego, który będzie przypisywał temat wypowiedzi do opinii klienta.

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

### Wnioski z eksploracji danych
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

## Użycie
```python
import model

# Załaduj dane
data = model.load_data('path_to_data')

# Trenuj model
lda_model = model.train_lda(data)

# Przeprowadź predykcję
topics = model.predict(lda_model, data)

# Wyświetl wyniki
model.visualize(lda_model, data)
