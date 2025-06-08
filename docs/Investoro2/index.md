## Projekt wdrożenia dwóch modeli ML pracujących w tandemie mających na celu przewidzieć stan mieszkania w podanym ogłoszeniu lub całej bazie ogłoszeń oraz podać jego przewidywaną wartość w PLN.



### ETAP I

* Czas rozpoczęcia: 2 kwiecień 2025 - 3 czerwca 2025

Celem głównym projektu jest analiza bazy danych ogłoszeń sprzedaży mieszkań, a w następnej 
kolejności na podstawie opisu z ogłoszenia i innych parametrów ocenić jego stan oraz podać
przewidywaną cenę. 
Do projektu użyto algorytmów scikit-learn oraz mechanizmu pyCaret w języku python. Modelowanie 
ML przewiduje stany mieszkań na bazie danych ogłoszeń z całej Polski. 
Po wstawieniu przewidywanego stanu (model ML klasyfikacyjny) przetworzona baza danych przechodzi 
do drugiego modelu (model regresyjny) gdzie tworzony jest model przewidujący ceny. 
Taka dwukrotnie przetworzona baza danych powraca w postaci .csv do klienta z nowymi polami 
stanu mieszkań i przewidywanej ceny.
Status: wdrożone

<figure markdown="1">
  <img src="https://raw.githubusercontent.com/Tomalom76/portfolio/main/docs/Investoro2/images/plan.jpg" alt="Investoro project1" width="300">
  <figcaption>Plan działania aplikacji</figcaption>
</figure>

### MLFLOW
Do aplikacji modelującej wprowadzony został moduł zarządzający zebranymi modelami w formie webowej. Można w nim wybierać najbardziej
aktualne modele produkcyjne oraz śledzić metryki modeli oraz porównywać je ze sobą. 

<figure markdown="1">
  <img src="https://raw.githubusercontent.com/Tomalom76/portfolio/main/docs/Investoro2/images/mlflow.jpg" alt="przykład mlflow" width="300">
  <figcaption>Przykład MLFLOW w użyciu</figcaption>
</figure>