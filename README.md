# 🐾 Optymalizacja Kampanii Adopcyjnej w Schronisku
Projekt zrealizowany w ramach przedmiotu **Uczenie Maszynowe**.  
Celem projektu jest stworzenie potoku decyzyjnego, który na podstawie danych wytypuje zwierzęta o największej szansie na adopcję, optymalizując przy tym ograniczony budżet marketingowy schroniska.

---

## 💼 Kontekst Biznesowy i Cel

Schronisko dla zwierząt planuje kampanię marketingową w mediach społecznościowych. Budżet akcji jest ściśle ograniczony i wynosi **200$**, a koszt wypromowania jednego zwierzaka to **10$**. Oznacza to, że możemy zareklamować maksymalnie 20 podopiecznych.

**Założenia skuteczności reklam:**
* Reklama zwierzaka o dobrych predyspozycjach adopcyjnych (True Positive) kończy się sukcesem w **70%** przypadków.
* Reklama kandydata o gorszych predyspozycjach (False Positive) przynosi efekt tylko w **10%** przypadków.

**Cel systemu:** Wybór top 20 zwierząt, które wygenerują *największą oczekiwaną liczbę adopcji* (maksymalizacja zysku biznesowego), a niekoniecznie tych, które dają najwyższe ogólne statystyki dokładności (Accuracy) dla całego zbioru.

---

## 📊 Zbiór Danych

* **Plik wejściowy:** `pet_adoption_data.csv`
* **Zmienna objaśniana (Target):** `AdoptionLikelihood` (1 = wysoka szansa na adopcję, 0 = niska szansa).
* **Cechy:** Dane demograficzne i fizyczne zwierząt (np. `PetType`, `Breed`, `Color`, `Size` itp.). Zmienna `PetID` została wykluczona z procesu modelowania.

---

## 🤖 Wybrane Modele

W ramach projektu przetestowaliśmy i poddaliśmy optymalizacji hiperparametrów (poprzez `GridSearchCV`) 3 algorytmy klasyfikacyjne:

| Model | Zakres optymalizacji (Tuning) |
|---|---|
| **Regresja Logistyczna** | Siła regularyzacji (C), typ kary (L1, L2), solver, selekcja cech (ANOVA K-Best). |
| **Drzewa Decyzyjne** | Maksymalna głębokość drzewa, minimalna liczba próbek do podziału, kryterium podziału. |
| **Naiwny Bayes** | [Uzupełnij: np. wygładzanie (var_smoothing dla GaussianNB)] |


---

## 🎯 Metryki i Funkcja Kosztu

Do oceny modeli na etapie CV wykorzystaliśmy własną metrykę **(Custom Scorer)** implementującą logikę biznesową schroniska.

* **Oczekiwana Liczba Adopcji (Priorytet):** Wartość obliczana dla top 20 predykcji wg wzoru: `(TP * 0.70) + (FP * 0.10)`. Model był optymalizowany w celu maksymalizacji tej wartości.

---

## 👥 Podział Obowiązków i Autorzy

**Zespół:** `Lematy`

Większość prac w ramach projektu zrealizowaliśmy **wspólnie**. Razem przeprowadziliśmy następujące etapy:
* **Analiza i Przygotowanie:** Wstępna Analiza Danych (EDA), preprocessing, czyszczenie danych oraz definicja funkcji biznesowej i struktury Pipeline'u.
* **Ewaluacja:** Porównanie wyników biznesowych.
* **Finalizacja:** przygotowanie dokumentacji, prezentacji oraz wniosków końcowych.

Za trenowanie, optymalizację i ewaluację poszczególnych modeli odpowiedzialni byli:
* **Lena Mackiewicz** — model regresji logistycznej
* **Tymon Sawicz** — model drzew decyzyjnych
* **Maciej Troć** — model naiwnego Bayesa

---
