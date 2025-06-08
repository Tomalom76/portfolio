# Projekt aplikacji AI odczytującej zawartość faktur.

* Data wykonania projektu: marzec 2025

Moim zadaniem jest połączenie danych w jeden plik CSV, który będzie zawierał informacje o kliencie, produkcie i fakturze. 
Przygotowanie pliku CSV, który zawiera tylko niezbędne kolumny i nie ma żadnych kolumn powtórzonych.

Jako rezultat wyciągania danych z faktur chcemy mieć w każdym wierszu informacje o zakupionym produkcie, 
ilości, kliencie, cenie jednostkowej.

<figure markdown="1">
  <img src="https://raw.githubusercontent.com/Tomalom76/portfolio/main/docs/Faktury-invoice/images/faktury.png" alt="faktury" width="300">
  <figcaption>Zrzut zawartości notebooka</figcaption>
</figure>

Aplikacja używa modelu gpt-4o-mini, ale jak widać na załączonym obrazku, można zmienić go na jakikolwiek inny.
To pokazuje, że aplikacja jest bardziej elastyczna od zwykłych czatów AI, w których wykorzystujemy, akurat ten
tylko model, do którego jesteśmy akurat zalogowani.

To jest przykład nowoczesnego przykładu działania modelu AI. Model AI potrafi sam znaleźć w pliku .png interesujące
nas informacje. Równie dobrze może być to faktura wskanowana do komputera lub plik przesłany z naszej skrzynki
pocztowej automatycznie za pomocą sztucznego Agenta AI.

<a href="faktury.ipynb" class="md-button md-button--primary">Pobierz Notebook</a>
<a href="products.csv" class="md-button md-button--primary">Pobierz Plik Bazy Danych produktów</a>
<a href="clients.csv" class="md-button md-button--primary">Pobierz Plik Bazy Danych klientów</a>

