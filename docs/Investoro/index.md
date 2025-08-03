
## Projekt wdrożenia trzech modeli ML pracujących wspólnie mających na celu przewidzieć stan mieszkania oraz jego dokładną lokalizację w podanym ogłoszeniu lub całej bazie ogłoszeń oraz podać jego przewidywaną wartość w PLN.



### ETAP II

* Czas trwania: 4 czerwiec - 31 lipiec 2025


### Zadania
Celem tego etapu było zakończenie prac nad całym modelem predykcji składającym się na:

  1. Model LSTM predykcji lokalizacji
  2. Model LSTM predykcji stanu mieszkania
  3. Model SCIKIT-LEARN predykcji cen mieszkania 

Wszystkie modele pracują według uproszczonego schematu:
<figure markdown="1">
  <img src="https://raw.githubusercontent.com/Tomalom76/portfolio/main/docs/Investoro/images/Schemat_uproszczony.png" alt="Investoro project1" width="600">
  <figcaption>Plan działania skryptów</figcaption>
</figure>

# Model predykcji lokalizacji
Jest to najbardziej złożony model całego procesu. Jego dokładność sięga ulicy w danej dzielnicy określonego miasta lub
ulicy w danje wiosce w danym powiecie dla obszaru całej Polski. 
Model wymagał skonstruowania specjalnego słownika pracującego na określonym schemacie stworzonym przez pracowdawcę.
Model pozostaje pod ciągłym nadzorem i jest poprawiany sukcesywnie by osiągnąć odpowiednią wydajność.

# Zmiany
W porównaniu z etapem I zmiany były fundamentalne. Zmienił się cały plan działania. przebudowane zostały oba wcześniejsze modele 
(cen i stanu mieszkania), wtym jeden(stan mieszkania) został przebudoawany na model typu LSTM tensorflow.keras
Predykcje plików typu .json pracują jako oddzielne skrypty stosujące model na pojedynczym pliku. Dodatkowo
do modelu predykcji lokalizacji dodano wzmocnienie w postaci pomocniczego użycia gpt-o4-mini.

### Dalszy rozwój
Aktualna praca polega na wzmacnianiu predykcji i osiąganiu co raz większej wydajności z poszczególnych modeli za pomocą: 
* normalizacji, 
* zbalansowania,
* regulacji parametrów i hyperparametrów oraz 
* różnych innych zabiegów ulepszających np. zwiększanie liczebności komórek neuronowych w poszczególnych warstwach
  lub zmiana charakteru całej warstwy. ReLU -> LeakyReLU