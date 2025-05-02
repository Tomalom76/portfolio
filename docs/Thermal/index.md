# Projekt Thermal

Data projektu: 2017

Projekt zakłada stworzenie oprogramowania w języku C#, który służy do obsługi drukarek fiskalnych.
Pierwotnie program powstał dla drukarki THERMAL XL firmy POSNET SA (dla tej firmy projekt był także tworzony) 
w celu obsługi podstawowych jej funkcji takich jak: zmiana czasu, dodanie produktów, dodanie cen, obsługa, 
sprzedaż, rozliczenia itp. oraz np. przekazanie danych do nagłówka i stopki w tym (najtrudniejsze) przesłanie
obrazka typu bitmap (.bmp) w rozdzielczości do 300x200 (b&w).
Aplikacja wymaga skonfigurowania połączenia zewnętrznego z drukarką za pomocą łącza COM, dlatego do jej funkcjonalości
dołączony został blok wspierający takie połączenie.

Program jest kompatybilny z wszystkimi drukarkarkami fiskalnymi obsługującymi protokół komunkacyjny posnet.

<figure markdown="1">
  <img src="https://raw.githubusercontent.com/Tomalom76/portfolio/main/docs/Thermal/images/Thermal1.jpg" alt="Thermal project1" width="300">
  <img src="https://raw.githubusercontent.com/Tomalom76/portfolio/main/docs/Thermal/images/zrzutdanych.png" alt="Thermal project2" width="300">
  <figcaption>Image caption</figcaption>
</figure>

