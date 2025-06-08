
## Projekt wdrożenia dwóch modeli ML pracujących w tandemie mających na celu przewidzieć stan mieszkania w podanym ogłoszeniu lub całej bazie ogłoszeń oraz podać jego przewidywaną wartość w PLN.



### ETAP II

* Czas rozpoczęcia: 4 czerwiec 2025 


### Zadania
Kolejnym krokiem jest opakowanie tych dwóch modeli w aplikację, którą bedzie można uruchomić plikiem .bat
Po jej uruchomieniu program wprowadzi stały nadzór (nasłuch) nad dwoma folderami, jeden do dużej bazy danych
a drugi dla małych plików typu JSON (zrobione).
Aplikacja po otrzymaniu sygnału, że coś znalazło się w danym folderze będzie sprawdzać czy jest to plik
z bazą danych typu .csv lub, analogicznie dla drugiego folderu, czy jest to .json (zrobione)
Następnie w przypadku dużej bazy, aplikacja będzie rozpoczynała proces trenowania nowego modelu, potem kolejnego, aż
w efekcie do folderu końcowego (wyjściowego) zwracać będzie ową bazę danych wzbogaconą o dwie kolumny: z przewidywanymi
cenami oraz przewidywanym stanem mieszkania (zrobione).

W drugim przypadku, przy odebraniu pliku typu .json nie będzie dla niego trenować modelu, tylko wykorzysta już ten
model istniejący, wytrenowany na wcześniej dostarczonej dużej bazie (w trakcie poprawek), a użyje go w pierwszej kolejności by przewidzieć stan mieszkania,
dla ogłoszenia, lub kilku ogłoszeń dostarczonych w postaci pliku .json. W dalszej kolejności plik, już wzbogacony o przewidziany
stan, zostanie potraktowany modelem cenowym, który wzbogaci go o kolejną predykcję, tym razem ceny. Taki 'bogaty' plik
zostanie ponownie zwrócony do folderu wyjściowego także jako .json(w trakcie poprawek). 

### PLAN

<figure markdown="1">
  <img src="https://raw.githubusercontent.com/Tomalom76/portfolio/main/docs/Investoro/images/skrypty.jpg" alt="Investoro project1" width="300">
  <figcaption>Plan działania skryptów</figcaption>
</figure>

Potraktowanie małych danych w ten sposób, jest korzystne dla klienta, który niewielką liczbę rekordów, może w szybki i 
sprawny sposób wzbogacić o wymagane predykcje. Natomiast w godzinach nocnych, może załączyć duże dane, które przygotują
nowe modele na kolejny dzień pracy.

### Dalszy rozwój
W dalszej kolejności planowane jest potrzymanie i obsługa serwisowa oraz wprowadzanie innowacyjnych poprawek do modeli, 
zapewniających poprawę jego działania (np. normalizacja yeo-johnsona).