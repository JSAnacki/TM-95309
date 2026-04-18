# Raport końcowy audytu bezpieczeństwa aplikacji ApiDemos

Data: 18.04.2026  
Audytor: Jan 95309  
Projekt: Mobilny System Demonstracyjny (Android)

## 1. Podstawa oceny końcowej
Raport przygotowano na podstawie pliku 84_risk_score.txt.

Wynik końcowy: 0/100  
Status: REJECTED

## 2. Rozliczenie punktacji ryzyka
Model oceny zastosował kary punktowe:
1. -30: Flaga Debuggable jest aktywna (High Risk)
2. -20: Poważna luka w com.google.android.gms (High)
3. -10: Średnia luka w com.squareup.okhttp (Medium)
4. -40: Krytyczna luka w org.apache.commons (Critical)

Suma kar: -100 punktów  
Wynik po odjęciu kar: 0/100

## 3. Najważniejsze ryzyka blokujące publikację
1. Aktywny tryb debugowania podnosi ryzyko nadużyć podczas analizy dynamicznej aplikacji.
2. Komponent org.apache.commons z luką krytyczną jest ryzykiem klasy release blocker.
3. Dodatkowe podatności w bibliotekach Google Play Services i OkHttp zwiększają łączną ekspozycję środowiska.

## 4. Plan naprawczy według priorytetu
1. Priorytet 1: usunąć krytyczną podatność przez aktualizację org.apache.commons do bezpiecznej wersji.
2. Priorytet 1: ustawić android:debuggable=false dla wariantu produkcyjnego.
3. Priorytet 1: zaktualizować com.google.android.gms do wersji bez wskazanej luki wysokiej.
4. Priorytet 2: podnieść com.squareup.okhttp do wersji bez podatności MITM.
5. Priorytet 2: uruchomić ponowny skan i przeliczenie punktacji po wdrożeniu poprawek.

## 5. Warunek akceptacji
Wydanie może zostać dopuszczone dopiero po usunięciu pozycji krytycznych i wysokich oraz po uzyskaniu dodatniego wyniku bezpieczeństwa w kolejnym przebiegu 84_risk_score.txt.

## 6. Podsumowanie
Na bazie danych z 84_risk_score.txt aplikacja nie spełnia minimalnych wymagań bezpieczeństwa do publikacji. Decyzja końcowa: odrzucenie wersji do czasu wdrożenia poprawek.
 
 
