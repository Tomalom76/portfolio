
# Projekt wdrożenia dwóch modeli ML pracujących w tandemie mających na celu przewidzieć stan mieszkania w podanym ogłoszeniu lub całej bazie ogłoszeń oraz podać jego przewidywaną wartość w PLN.

Czas rozpoczęcia: 2 kwiecień 2025

Celem głównym projektu jest analiza bazy danych ogłoszeń sprzedaży mieszkań, a w następnej 
kolejności na podstawie opisu z ogłoszenia i innych parametrów ocenić jego stan oraz podać
przewidywaną cenę. 
Do projektu użyto algorytmów scikit-learn oraz mechanizmu pyCaret w języku python. Modelowanie 
ML przewiduje stany mieszkań na bazie danych ogłoszeń z całej Polski. 
Po wstawieniu przewidywanego stanu (model ML klasyfikacyjny) przetworzona baza danych przechodzi 
do drugiego modelu (model regresyjny) gdzie tworzony jest model przewidujący ceny. 
Taka dwukrotnie przetworzona baza danych powraca w postaci .csv do klienta z nowymi polami 
stanu mieszkań i przewidywanej ceny.
Stan: gotowe do wdrożenia

<figure markdown="1">
  <img src="https://raw.githubusercontent.com/Tomalom76/portfolio/main/docs/Investoro/images/plan.jpg" alt="Investoro project1" width="300">
  <figcaption>Plan działania aplikacji</figcaption>
</figure>

## Kolejne zadania
Kolejnym krokiem jest opakowanie tych dwóch modeli w aplikację, którą bedzie można uruchomić plikiem .bat
Po jej uruchomieniu program wprowadzi stały nadzór (nasłuch) nad dwoma folderami, jeden do dużej bazy danych
a drugi dla małych plików typu JSON.
Aplikacja po otrzymaniu sygnału, że coś znalazło się w danym folderze będzie sprawdzać czy jest to plik
z bazą danych typu .csv lub, analogicznie dla drugiego folderu, czy jest to .json
Następnie w przypadku dużej bazy, aplikacja będzie rozpoczynała proces trenowania nowego modelu, potem kolejnego, aż
w efekcie do folderu końcowego (wyjściowego) zwracać będzie ową bazę danych wzbogaconą o dwie kolumny: z przewidywanymi
cenami oraz przewidywanym stanem mieszkania.

W drugim przypadku, przy odebraniu pliku typu .json nie będzie dla niego trenować modelu, tylko wykorzysta już ten
model istniejący, wytrenowany na wcześniej dostarczonej dużej bazie, a użyje go w pierwszej kolejności by przewidzieć stan mieszkania,
dla ogłoszenia, lub kilku ogłoszeń dostarczonych w postaci pliku .json. W dalszej kolejności plik, już wzbogacony o przewidziany
stan, zostanie potraktowany modelem cenowym, który wzbogaci go o kolejną predykcję, tym razem ceny. Taki 'bogaty' plik
zostanie ponownie zwrócony do folderu wyjściowego także jako .json. 
Potraktowanie małych danych w ten sposób, jest korzystne dla klienta, który niewielką liczbę rekordów, może w szybki i 
sprawny sposób wzbogacić o wymagane predykcje. Natomiast w godzinach nocnych, może załączyć duże dane, które przygotują
nowe modele na kolejny dzień pracy.

## Dalszy rozwój
Dalsze plany na rozwój, czyli etap II ma polegać na rozwoju aplikacji wykorzystujący model językowy LLM, który na 
podstawie opisu wklejonego z ogłoszenia, lub/także zdjęcia, mógłby w sposób bardziej szczegółowy rozpoznać
stan nieruchomości i dać ocenę. Tutaj oczywiście wchodzą już koszty użycia danego modelu językowego i należy liczyć się
z pewnymi wydatkami, w szczególności kiedy to baza ma liczbę rekordów liczoną w milionach.