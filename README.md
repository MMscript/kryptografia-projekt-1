# Projekt 1: Kryptosystem (Szyfrowanie i Deszyfrowanie)

Wersja online: https://mmscript.github.io/kryptografia-projekt-1/

Projekt realizuje trzy klasyczne algorytmy kryptograficzne w postaci samodzielnej strony internetowej (jeden plik HTML + CSS + JavaScript) z graficznym interfejsem użytkownika (GUI), menu wyboru i obsługą błędów.

---

## Zasada działania i wybór szyfru

Wybór algorytmu opiera się na sumie numerów indeksów członków grupy modulo 3:
* **a) Szyfr podstawieniowy (Cezara)** (`suma % 3 == 0`):
  * Klucz ustalany przez użytkownika: dowolna liczba całkowita $k \in \mathbb{Z}$ (np. `3`, `-5`).
  * Przesunięcie znaków: $C_i = (P_i + k) \pmod{26}$.
* **b) Szyfr Vigenère'a** (`suma % 3 == 1`):
  * Klucz ustalany przez użytkownika: słowo kluczowe o minimalnej długości 8 liter (bez cyfr i spacji).
  * Szyfrowanie polialfabetyczne: $C_i = (P_i + K_j) \pmod{26}$.
* **c) Szyfr permutacyjny** (`suma % 3 == 2`):
  * Permutacja jest zdefiniowana na stałe w kodzie (długość 6):
    $$\pi = [4, 1, 6, 2, 5, 3] \quad (\text{1-based}) \iff [3, 0, 5, 1, 4, 2] \quad (\text{0-based})$$
  * W przypadku, gdy długość tekstu nie dzieli się przez 6, stosowane jest automatyczne dopełnienie (padding) znakiem `_`.

W aplikacji znajduje się także kalkulator indeksu, który po wpisaniu numeru studenta oblicza sumę modulo 3 i od razu ustawia odpowiedni szyfr.

---

## Uruchomienie projektu

Aplikacja jest dostępna w przeglądarce pod adresem:  
https://mmscript.github.io/kryptografia-projekt-1/

Lokalnie wystarczy otworzyć plik `index.html` w dowolnej przeglądarce internetowej (nie wymaga instalacji dodatkowych bibliotek):
* Dwuklik na plik `index.html`, lub
* Z poziomu terminala:
  ```bash
  # macOS
  open index.html

  # Linux
  xdg-open index.html

  # Windows
  start index.html
  ```

---

## Przykłady działania i obsługa błędów

1. **Szyfr podstawieniowy:**
   * Poprawny klucz: `3`
   * Tekst jawny: `KRYPTOGRAFIA` -> Szyfrogram: `NUBSWRJUDILD`
   * Obsługa błędów: wpisanie liter (np. `abc`), ułamka (`3.14`) lub pustego pola skutkuje komunikatem o błędzie.

2. **Szyfr Vigenère'a:**
   * Poprawny klucz: `BEZPIECZENSTWO` (14 liter)
   * Tekst jawny: `TAJNY KOMUNIKAT` -> Szyfrogram: `UEICG OQLYAADWH`
   * Obsługa błędów: klucz krótszy niż 8 liter lub zawierający cyfry i spacje jest blokowany.

3. **Szyfr permutacyjny:**
   * Stała permutacja w kodzie: `[4, 1, 6, 2, 5, 3]`
   * Tekst jawny: `KRYPTO` -> Szyfrogram: `RPOKTY`

4. **Walidacja tekstu:**
   * Pusty tekst lub ciąg bez liter alfabetu (np. same spacje lub cyfry) jest odrzucany z czytelnym komunikatem.
