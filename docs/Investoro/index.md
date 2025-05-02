
# Projekt wdrożenia dwóch modeli ML pracujących w tandemie mających na celu przewidzieć stan mieszkania w podanym ogłoszeniu lub całej bazie ogłoszeń oraz podać jego przewidywaną wartość w PLN.

Celem głównym projektu jest analiza bazy danych ogłoszeń sprzedaży mieszkań, a w następnej 
kolejności na podstawie opisu z ogłoszenia i innych paramatrów ocenić jego stan oraz podać
przewidywaną cenę. 
Do projektu użyto algorytmów scikit-learn oraz mechanizmu pyCaret. Modelowanie ML przewiduje
stany mieszkań na bazie danych ogłoszeń z całej Polski. Po wstawieniu przewidywanego stanu
(model ML klasyfikacyjny) przetworzona baza danych przechodzi do drugiego modelu (model
regresyjny) gdzie tworzony jest model przewidujący ceny. Taka dwukrotnie przetworzona 
baza danych powraca w postaci .csv do klienta z nowymi polami stanu mieszkań i przewidywanej
ceny.