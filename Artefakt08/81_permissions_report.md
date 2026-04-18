# Raport analizy uprawnień i flag bezpieczeństwa

## 1. Źródło danych
Raport przygotowano na podstawie pliku [Artefakt08/RiskyPermission.xml](Artefakt08/RiskyPermission.xml).

Zidentyfikowane metadane audytu:
- `app`: `ApiDemos_Security_Check`
- `status`: `ReviewRequired`

## 2. Wyniki z pliku XML

### 2.1 Flagi konfiguracyjne
- `Debuggable`: `true`

Ocena: wysoki poziom ryzyka. Wersja aplikacji z włączonym debugowaniem może być łatwiejsza do analizy dynamicznej i nadużyć w środowisku produkcyjnym.

### 2.2 Uprawnienia oznaczone jako ryzykowne
W sekcji `<RiskyPermissions>` wykryto 5 pozycji:
1. `android.permission.READ_CONTACTS`
2. `android.permission.INTERNET`
3. `android.permission.WRITE_EXTERNAL_STORAGE`
4. `android.permission.RECORD_AUDIO`
5. `android.permission.CAMERA`

## 3. Wnioski bezpieczeństwa
- Zakres uprawnień obejmuje dostęp do danych osobowych (kontakty), multimediów (mikrofon, kamera), pamięci oraz komunikacji sieciowej.
- Połączenie tych uprawnień z aktywną flagą `Debuggable=true` zwiększa powierzchnię ataku i wymaga przeglądu przed publikacją.
- Status `ReviewRequired` w XML jest spójny z wykrytym profilem ryzyka.

## 4. Rekomendowane działania
1. Ustawić `android:debuggable="false"` dla buildów produkcyjnych.
2. Zweryfikować zasadność każdego ryzykownego uprawnienia i usunąć nieużywane.
3. Ograniczyć dostęp do pamięci zewnętrznej na rzecz bardziej restrykcyjnych mechanizmów.
4. Dodać kontrolę w CI/CD, która blokuje artefakty z `Debuggable=true` oraz raportuje listę ryzykownych uprawnień.

## 5. Podsumowanie
Na podstawie [Artefakt08/RiskyPermission.xml](Artefakt08/RiskyPermission.xml) aplikacja wymaga dodatkowego przeglądu bezpieczeństwa przed dalszym wdrożeniem.

Autor: Jan, 95309  
Data: 18.04.2026


