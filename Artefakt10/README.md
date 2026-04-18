# Mobile Automation and Security Testing Suite

Prowadzacy: mgr Mariusz Dworniczak  
Student: Jan Anacki  
Numer albumu: 95309

---

## Cel projektu
Repozytorium dokumentuje pelny cykl testowania aplikacji mobilnej Android: od przygotowania infrastruktury, przez analize APK i automatyzacje UI/API, az po audyt bezpieczenstwa i finalny pipeline raportujacy.

Glowna idea: podejscie cloud-ready i headless, czyli jak najwiecej operacji wykonywanych przez CLI, skrypty Python i kontenery Docker.

---

## Stos technologiczny
- Python 3
- Appium 2.x
- Docker i Docker Compose
- Requests, Pytest, JsonSchema
- Allure Report
- Analiza statyczna dekompilowanego APK

---

## Przeglad blokow Artefakt 1-10

### Blok 1 - Artefakt01 (Srodowisko startowe)
Zakres:
- Przygotowanie bazowego obrazu Docker.
- Zdefiniowanie zmiennej srodowiskowej ze wskazaniem studenta.

Rezultat:
- Prosty, powtarzalny kontener testowy uruchamiany przez Dockerfile.

### Blok 2 - Artefakt02 (Dekompilacja i material analityczny)
Zakres:
- Przygotowanie dekompilowanego APK (manifest, zasoby, layouty, smali).
- Udostepnienie danych wejsciowych do dalszej automatycznej analizy.

Rezultat:
- Baza danych technicznych aplikacji do analizy uprawnien, selektorow i ryzyk.

### Blok 3 - Artefakt03 (Pierwsza orkiestracja Appium)
Zakres:
- Konfiguracja docker-compose dla serwera Appium.
- Wystawienie portu 4723 i stabilny restart uslugi.

Rezultat:
- Powtarzalny sposob uruchamiania infrastruktury Appium niezaleznie od systemu hosta.

### Blok 4 - Artefakt04 (Analityka UI i stabilnosc selektorow)
Zakres:
- a11y_check.py: wykrywanie brakow contentDescription w layoutach.
- selector_miner.py: wydobycie identyfikatorow UI z XML.
- stability_auditor.py: metryki dominacji klas i ryzyko niestabilnych locatorow.

Rezultat:
- Raporty JSON oraz logi wspierajace projektowanie odpornych testow UI.

### Blok 5 - Artefakt05 (Integracja danych pod Appium)
Zakres:
- step1_caps.py: automatyczne budowanie desired capabilities z manifestu.
- step2_analysis.py: inspekcja pakietu, activity i uprawnien.
- step3_selectors.py: mapa selektorow biznesowych do JSON.
- step4_session.py: walidacja gotowosci sesji i spojnosci artefaktow.
- step5_final.py: raport koncowy XML z opisowym feedbackiem.

Rezultat:
- Zestaw wejsc do uruchomienia sesji automatyzacji z minimalna konfiguracja reczna.

### Blok 6 - Artefakt06 (Architektura POM)
Zakres:
- BasePage.py i MainPage.py: warstwa obiektow stron i mapowanie kluczy biznesowych.
- 63_pom_test.py: scenariusz testowy oparty o logike Page Object.
- 65_framework_check.py: kontrola integralnosci frameworka i raport XML.

Rezultat:
- Modularna architektura testow, latwiejsza w utrzymaniu i skalowaniu.

### Blok 7 - Artefakt07 (Zaawansowane scenariusze mobilne)
Zakres:
- 71_gestures.py: logika scroll i long press.
- 72_interrupt.py: symulacja przerwan systemowych (polaczenie, low battery).
- 73_state_manager.py: orientacja ekranu i stan zasilania.
- 74_sync.py: inteligentne oczekiwanie na elementy.

Rezultat:
- Pokrycie trudniejszych, produkcyjnych warunkow pracy aplikacji mobilnej.

### Blok 8 - Artefakt08 (Audyt bezpieczenstwa aplikacji)
Zakres:
- 81_manifest_scanner.py: ekstrakcja ryzyk z manifestu do XML.
- 82_secrets_finder.py: wykrywanie potencjalnych wyciekow w strings.xml.
- 83_library_audit.py: analiza podatnosci bibliotek i CVE.
- 84_security_scorer.py: przeliczenie wyniku ryzyka.
- Raporty: 81_permissions_report.md, 82_secrets_found.md, 85_final_audit.md.

Rezultat:
- Koncowa ocena bezpieczenstwa 0/100 i status odrzucenia wydania do czasu napraw.

### Blok 9 - Artefakt09 (Testy API i most hybrydowy)
Zakres:
- 91_api_setup.py: test lacznosci z backendem.
- 92_crud_test.py: test tworzenia zasobu POST.
- 93_schema_test.py: walidacja kontraktu JSON Schema.
- 94_negative_test.py: scenariusze negatywne i obsluga bledow.
- 95_hybrid_test.py: test mostu API + Appium Docker.
- docker-compose.yml: konteneryzacja Appium dla testow hybrydowych.

Rezultat:
- Potwierdzenie, ze warstwa API i infrastruktura Appium moga byc testowane wspolnie.

### Blok 10 - Artefakt10 (Master Pipeline i raportowanie)
Zakres:
- pipeline.py: automatyzuje pelny cykl uruchomienia testow i raportowania.
- Testy Allure: test_101_allure_init.py, test_102_meta_reporting.py, test_103_attachments.py.
- Generowanie allure-results i allure-report.

Rezultat:
- Jeden skrypt uruchamia infrastrukture, testy, raport i sprzatanie srodowiska.

---

## Przeplyw end-to-end
1. Infrastruktura i dane wejsciowe: Bloki 1-3.
2. Budowa analityki UI i gotowosci sesji: Bloki 4-5.
3. Architektura i scenariusze mobilne: Bloki 6-7.
4. Audyt bezpieczenstwa: Blok 8.
5. Testy API i hybrydowe: Blok 9.
6. Pipeline i raportowanie: Blok 10.

---

## Jak uruchomic pipeline koncowy

```bash
cd Artefakt10
python3 pipeline.py
allure serve allure-results
```

Pipeline wykonuje automatycznie:
- start kontenera Appium przez Docker Compose,
- uruchomienie testow Pytest,
- wygenerowanie raportu Allure,
- zamkniecie i posprzatanie infrastruktury.

---

## Wnioski koncowe
Projekt obejmuje caly przekroj praktyki QA mobile: od engineeringu infrastruktury i analizy statycznej, przez automatyzacje UI/API, po security scoring i raportowanie menedzerskie.

 