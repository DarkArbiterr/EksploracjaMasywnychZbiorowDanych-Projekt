# Eksploracja masywnych zbiorów danych - projekt

## Opis

Dane które zostały poddane analizie zostały wzięte z [Million Song Dataset](http://millionsongdataset.com/)
Projekt stanowi rozwiązanie 5 zadań z zakresu **analizy i eksploracji danych**.:

### Zadanie 1. - Próbkowanie

Dane: **Zbiór rekomendacji** dla uzyskanej próbki użytkowników.

1. Wczytać dane. Uwaga, bag of words zaczyna się od znaku %. W zbiorze znajdują się wyniki z dwóch serwisów: należy wybrać jeden. (odnosi się do danych **Zbiór musiXmatch**).
2. Zaimplementować technikę **próbkowania proporcjonalnego strumienia**. Zastosować **haszowanie** po użytkownikach.
3. Pobrać 10% próbkę danych i na tej podstawie stworzyć histogram liczby odsłuchań

### Zadanie 2. - Szukanie elementów podobnych

Dane: **Zbiór musiXmatch** podobne.

1. Wczytaj dane.
2. Korzystając z algorytmu **Minhash LSH**, dla zadanego utworu odnaleźć utwory
   
Uwaga:

1. Dane są w formacie bag of words. Należy z tego zbioru wyrzucić stopwords i uporządkować słowa malejąco względem częstotliwości wystąpień.
2. Dla testów można wybrać jakąś charakterystyczną piosenkę, np. świąteczną i zbadać czy utwory podobne też są w tej tematyce.
3. **Shinglety** warto wygenerować po słowach.

### Zadanie 3. - Filtr Blooma

Dane: **Zbiór musiXmatch** (trzeba dobrać odpowiednio parametry). Należy z tego zbioru wyrzucić stopwords i:

1. Wybrać kilka utworów (ok. 10) dowolnego artysty.
2. Stworzyć filtr Blooma bazujący na pierwszych 10 słowach z tych utworów (uwaga,
uporządkować słowa malejąco względem częstotliwości wystąpień). Można przetestować różne funkcje hashujące (i różną ich liczbę).
3. Przetworzyć strumień z danych i wskazać wszystkie elementy, które pasują do wzorca.
4. Utwór uważamy za podobny do utworów danego artysty, jeśli k (np. 10) najczęściej występujących słów znajduje się w filtrze Blooma.

Uwaga:

1. Proszę zwrócić uwagę na inicjalizację w strukturze bitarray. Struktura ta normalnie nie inicjalizuje tablicy zerami tylko kopiuje istniejące obiekty.
2. Operacje bitowe pozwalają dogenerować bardzo szybko nowe hashe za pomocą tzw. double hashing.

### Zadanie 4. - Szukanie społeczności

Dane: **Zbiór rekomendacji**

1. Znajdź na podstawie danych społeczności, do których należą wybrani użytkownicy (ok. 10 użytkowników) poprzez np. trawling, grupowanie spektralne.
2. W celu stworzenia grafu połączeń liczymy korelację Pearsona między dowolnymi dwoma wierzchołkami i łączymy je krawędzią, jeśli jest mniejsza niż pewien parametr (threshold).
3. Zwróćmy uwagę, że nie mamy danej wprost oceny tracków. Można ją stworzyć wykorzystując liczbę odsłuchań i stosując np. krzywą sigmoidalną. Niestety zbiór ten ma bardzo dużo zer, dlatego można losowo wypełnić (powiedzmy 5%) zer ocenami z odpowiedniego zakresu.

Uwaga:

1. Korelację Pearsona należy liczyć tylko dla tych współrzędnych, dla których obydwa wektory mają niezerowe wartości, np. pearsonr (x, y) dla x = [0, 4, 1, 0], y = [3, 0, 0, 2], wynosi 0, a nie −0.7337.

### Zadanie 5. - System rekomendacyjny

Dane: **Zbiór rekomendacji**

1. Stwórz system rekomendacyjny i przetestuj jego działanie.
2. System może być oparty o collaboration filtering. W tym celu należy zaimplementować SVD (dokładniej P QT i znalezienie macierzy P i Q poprzez stochastyczny spadek gradientowy).
3. Zwróćmy uwagę, że nie mamy danej wprost oceny tracków. Można ją stworzyć wykorzystując liczbę odsłuchań i stosując np. krzywą sigmoidalną.
4. Na potrzeby zadania zakładamy, że są tylko dwie ukryte zmienne (tzn. rzutujemy na 2 wymiarową podprzestrzeń).

Uwaga: 

1. Ze względu na rozmiar danych może być konieczność zastosowania macierzy rzadkich.
2. Niestety zbiór danych ma bardzo dużo zer, dlatego można losowo wypełnić (powiedzmy 5%) zer ocenami z odpowiedniego zakresu lub przefiltrować i usunąć użytkowników, ktorzy słabo kontrybuują i mają mało odsłuchań.
