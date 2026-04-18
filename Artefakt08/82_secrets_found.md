# Raport analizy potencjalnych wycieków

Student: Jan Anacki  
Indeks: 95309  
Data raportu: 18-04-2026

## 1. Podstawa raportu
Raport został przygotowany wyłącznie na podstawie pliku: 82_secrets_found.txt.

## 2. Statystyka znalezisk z pliku TXT
Łącznie wykryto 590 rekordów.

Podział kategorii:
1. URL_Endpoint: 3
2. Potential_Secret: 2
3. API_Key_Format: 585

Wniosek: większość dopasowań pochodzi z szerokiego wzorca API_Key_Format i wymaga filtrowania kontekstowego.

## 3. Znaleziska o najwyższym priorytecie
1. URL_Endpoint -> http://www.example.com/lala/foobar@example.com
   Uzasadnienie: adres e-mail osadzony w URL może wskazywać na utrwalanie danych identyfikujących użytkownika w zasobie testowym lub demonstracyjnym.

2. Potential_Secret -> password
   Uzasadnienie: bezpośrednie słowo kluczowe związane z hasłem jest sygnałem ostrzegawczym i wymaga kontroli miejsca użycia.

3. API_Key_Format -> reset_password_warning
   Uzasadnienie: wpis dotyczy przepływu resetowania hasła; choć może być zwykłym identyfikatorem zasobu, powinien być ręcznie zweryfikowany.

## 4. Przykłady prawdopodobnych false positive
1. URL_Endpoint -> http://www.google.com
   Uzasadnienie: publiczny, ogólnodostępny adres bez danych uwierzytelniających.

2. URL_Endpoint -> https://www.google.com,
   Uzasadnienie: analogicznie, wpis testowy; dodatkowy przecinek sugeruje surowy odczyt tekstu, nie sekret.

3. API_Key_Format -> abc_font_family_display_3_material
   Uzasadnienie: nazwa zasobu UI biblioteki Material, nie token ani klucz.

## 5. Ocena jakości skanu
Skan poprawnie wychwycił sygnały związane z hasłami i URL, ale wygenerował bardzo dużo dopasowań technicznych w kategorii API_Key_Format. Oznacza to wysoką czułość i niską precyzję.

## 6. Rekomendacje
1. Dodać whitelistę wzorców zasobów UI, aby ograniczyć liczbę false positive.
2. Wprowadzić regułę podnoszącą priorytet, gdy URL zawiera adres e-mail lub identyfikator użytkownika.
3. Dla wpisów zawierających słowo password wymuszać ręczny przegląd kodu i konfiguracji.
4. Rozdzielić raport na sekcje: potwierdzone ryzyko, do weryfikacji, false positive.

## 7. Podsumowanie
Na podstawie 82_secrets_found.txt potwierdzono pojedyncze sygnały podwyższonego ryzyka i dużą liczbę dopasowań niskiej jakości wymagających walidacji manualnej.


