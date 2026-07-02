---
name: delegate
description: Dla bardzo złożonych, wieloetapowych, wysokiego ryzyka zadań (dowolnego typu — kod, biznes, treści, research). Fable 5 tworzy szczegółowy plan, użytkownik akceptuje podsumowanie, tańszy model wykonuje. Oszczędzaj koszty bez utraty jakości. Użyj proaktywnie gdy zadanie wymaga głębokich strategicznych decyzji i wieloetapowego planowania.
disable-model-invocation: false
user-invocable: true
allowed-tools: Agent, AskUserQuestion
---

# Skill: `/delegate` — Fable planuje, tańszy model wykonuje

Jesteś orchesteratorem dla bardzo złożonych zadań. Twoja rola: ocenić zadanie, poprosić Fable 5 o szczegółowy plan, pokazać użytkownikowi skrót, czekać na akceptację, i zlecić wykonanie tańszemu modelowi (Sonnet 5 lub Opus 4.8).

## Workflow

### 1. Kwalifikacja zadania

Czytaj zadanie które dostałeś. **Czy rzeczywiście jest na tyle złożone, żeby ten skill się opłacał?**

Skill ma sens gdy:
- Zadanie ma 3+ niezależnych etapów / części
- Wymaga głębokich strategicznych decyzji, architektury, planowania
- Jest wysokiego ryzyka — błęd będzie kosztowny
- Wymaga badania kontekstu (czytania wielu plików, danych, wymagań)
- Nie jest po prostu "napisz funkcję X" albo "popraw ten bug"

**Jeśli NIE** — powiedz użytkownikowi że to zadanie jest zbyt proste dla `/delegate`, i wykonaj je normalnie (bezpośrednio jako główny model albo dymisją do zwykłego Agent toolu jeśli to bardziej biznesowe).

**Jeśli TAK** — idź do kroku 2.

### 2. Planowanie przez Fable 5

Użyj narzędzia Agent z poniższymi parametrami:

```
description: "Fable 5 tworzy szczegółowy plan dla złożonego zadania"
subagent_type: general-purpose
model: fable
prompt: """
## Zadanie do zaplanowania

{wstaw tutaj dosłownie zadanie które dostałeś}

## Twoja rola

Jesteś architektem rozwiązania. Twoje zadanie: **nie wykonywać**, tylko **zaplanować dokładnie jak to powinno być zrobione**.

Stwórz szczegółowy plan z:

1. **Zrozumienie**: Krótka analiza co trzeba zrobić i dlaczego
2. **Kontekst**: Jakie pliki/dane/informacje trzeba przeczytać/zbadać
3. **Plan krok po kroku**: 
   - Każdy krok musi być konkretny (nie "ogólnie", ale "otwórz plik X, zmień linię Y na Z")
   - Uwzględnij warunki brzegowe (edge cases, wyjątki)
   - Dodaj branching logic: "jeśli sytuacja A, to zrób B, jeśli C, to zrób D"
4. **Kryteria sukcesu**: Jak verify że plan został poprawnie wykonany
5. **Ryzyka i mitygacja**: Co może pójść nie tak i jak to obejść
6. **Rekomendacja modelu**: 
   - Na końcu dopisz rekomendację modelu do wykonania
   - Sonnet 5 (tańszy): jeśli zadanie jest MECHANICZNE, dobrze zdefiniowane, wymaga głównie implementacji
   - Opus 4.8 (droższy): jeśli wymaga NIUANSU, STRATEGII, KREATYWNYCH DECYZJI, wymagań niejednoznacznych
   - Podaj 1-2 zdaniowe uzasadnienie

## WAŻNE

- **Nie wykonuj** — tylko plan
- Plan musi być na tyle konkretny, żeby inny model mógł go wykonać bez dodatkowych pytań
- Pisz dla czytelności (nie dla stylu)
"""
```

Po powrocie od Fable — masz teraz szczegółowy plan w zmiennej (wynik call'u Agent).

### 3. Podsumowanie i akceptacja

Przeczytaj plan od Fable. Teraz musisz go **skrócić do 5-10 linijek** dla użytkownika.

Ekstrahuj:
- **Cel**: co będzie zrobione (1 zdanie)
- **Główne kroki**: 3-4 punkty (większe etapy, nie detale)
- **Rekomendowany model**: Sonnet 5 czy Opus 4.8 (z uzasadnieniem od Fable)
- **Ryzyka**: 1-2 główne ryzyka jeśli są

Teraz użyj narzędzia AskUserQuestion:

```json
{
  "questions": [
    {
      "question": "Plan gotowy. Czy go akceptujesz i wykonuję rekomendowanym modelem ({model_recommendation})?",
      "header": "Akceptacja planu",
      "multiSelect": false,
      "options": [
        {
          "label": "Tak, wykonaj {recommended_model}",
          "description": "Przejdź do wykonania planu zgodnie z rekomendacją Fable ({uzasadnienie})"
        },
        {
          "label": "Wykonaj Opus 4.8 zamiast",
          "description": "Jeśli rekomendacja to Sonnet — zmień na Opus dla większej elastyczności"
        },
        {
          "label": "Wykonaj Sonnet 5 zamiast",
          "description": "Jeśli rekomendacja to Opus — zmień na Sonnet dla mniejszych kosztów"
        },
        {
          "label": "Popraw plan",
          "description": "Wróć do Fable z moimi uwagami"
        },
        {
          "label": "Anuluj",
          "description": "Nie robić"
        }
      ]
    }
  ]
}
```

### 4. Obsługa odpowiedzi użytkownika

- **Tak / Wykonaj {model}** → idź do kroku 5
- **Popraw plan** → użyj AskUserQuestion żeby zbiorać uwagi użytkownika, potem wyślij do Fable'a prompt z uwagami i wróć do kroku 2
- **Anuluj** → powiedz "OK, anulujemy" i koniec

### 5. Wykonanie

Użyj narzędzia Agent:

```
description: "Wykonanie szczegółowego planu Fable 5"
subagent_type: general-purpose
model: {wybrany_model — sonnet lub opus}
prompt: """
## Szczegółowy plan do wykonania

{wstaw tutaj CAŁY, szczegółowy plan od Fable — nie skrót}

## Twoja rola

Wykonaj dokładnie ten plan, krok po kroku. 

- Jeśli plan mówi "otwórz plik X i zmień linię Y", to zrób
- Jeśli rzeczywistość nie zgadza się z założeniami planu (np. plik wygląda inaczej), zgłoś to przed kontynuacją
- Zgłaszaj co robisz po każdym znaczącym kroku
- Jeśli pojawia się sytuacja brzegowa nieobjęta planem, wybierz logiczne podejście i opisz dlaczego

## WAŻNE

- Nie improwizuj — trzymaj się planu
- Plan ma być na tyle konkretny że nie potrzebujesz dodatkowych pytań
"""
```

Po powrocie — masz rezultat wykonania.

### 6. Raport końcowy

Krótko podsumuj co zostało zrobione:
- Jakie były główne kroki
- Czy wszystko poszło zgodnie z planem czy były odchylenia
- Linki do zmodyfikowanych plików / rezultatów

Nie powtarzaj całego planu — użytkownik widział skrót, widzisz teraz rezultat.

---

## Przewodnik do Auto-Invokacji

Główny model (Claude w rozmowie z użytkownikiem) powinien **proaktywnie zaproponować** ten skill gdy:
- Użytkownik zdaje się prosić o coś bardzo skomplikowanego (wieloetapowe, strategiczne, wysokiego ryzyka)
- Nie powiedział `/delegate` sam
- Zadanie ma 3+ niezależne części lub wymaga głębokich decyzji architektonicznych

Propozycja powinna wyglądać: _"To zadanie jest bardzo złożone — może powinienem użyć `/delegate`? Fable 5 stworzył szczegółowy plan, Ty go sprawdzisz, a Sonnet/Opus go wykona — oszczędzamy koszty bez utraty jakości."_

Daj użytkownikowi opcję: zgoda czy nie.
