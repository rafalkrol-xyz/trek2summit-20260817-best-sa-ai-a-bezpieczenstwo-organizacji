---
title: "AI a bezpieczeństwo organizacji"
sub_title: "Wewnętrzna konferencja BEST S.A."
author: "Rafał Król — Head of AWS Technologies, Trek2Summit"
---

## 2026: AI jako wektor ataku

**$25.6M** — tyle straciła firma Arup w jednym deepfake'owym video callu (2024)

**500 000 maszyn** skompromitowanych w 3 godziny — atak supply chain na LiteLLM (marzec 2026)

**Agenci AI uciekli z sandboxa** i autonomicznie włamali się do Hugging Face — bez instrukcji człowieka (lipiec 2026)

Każde z tych zdarzeń zaczęło się od czegoś, co robimy codziennie:
video call, `pip install`, ewaluacja modelu.

Dziś pokażę, jak te same mechanizmy dotyczą **naszego** środowiska — Copilot, AWS, i narzędzi, z których korzystacie na co dzień.

<!-- end_slide -->

## Agenda

**Otwarcie**
- Skala problemu — AI security w liczbach
- Kontekst BEST S.A.: Copilot, AWS, codzienne narzędzia

**Krajobraz zagrożeń**
- Mapa zagrożeń AI w 2024–2025
- Wycieki danych przez chatboty
- Shadow AI — nieautoryzowane narzędzia
- AI Phishing i vishing — nowa generacja ataków
- Deepfake — manipulacja obrazem i głosem
- Automatyzacja ataków i asymetria atakujący/obrońca
- Destrukcyjna autonomia agentów AI
- Prompt Injection — demo z PromptFoo
- Halucynacje AI — fałszywe fakty w produkcji

**Od zagrożeń do rozwiązań**
- Best practices i zasady bezpiecznego korzystania
- Framework oceny ryzyka narzędzi AI
- Narzędzia bezpieczeństwa: AWS, Azure, vendor-neutral
- Polityki jako enablery innowacji

**Zamknięcie**
- 5 key takeaways + call-to-action

→ _Zaczynamy od krajobraz zagrożeń — co tak naprawdę zmieniło się w 2024?_

<!-- end_slide -->

## Mapa zagrożeń AI w 2024-2025

**8 kategorii zagrożeń**, które zdefiniowały krajobraz 2024–2025:

1. **Wycieki danych przez chatboty** — niekontrolowane udostępnianie danych modelom
2. **Shadow AI** — nieautoryzowane narzędzia poza kontrolą organizacji
3. **AI-enhanced phishing i vishing** — perfekcyjny język, klonowanie głosu
4. **Deepfake** — manipulacja wideo/audio w kontekście korporacyjnym
5. **Automatyzacja ataków** — AI jako force multiplier dla atakujących
6. **Destrukcyjna autonomia agentów** — niekontrolowane działania AI z nadmiernymi uprawnieniami
7. **Prompt injection** — manipulacja modeli przez spreparowane dane wejściowe
8. **Halucynacje AI** — fałszywe informacje prezentowane z pewnością

Wspólny mianownik: każda z tych kategorii dotyka narzędzi, z których korzystacie **dziś** — od Copilot po custom AI workflows.

<!-- end_slide -->

## Skala problemu — statystyki

**Tempo zmian — co mówią dane z 2024–2025:**

- **71%** organizacji zgłasza incydenty związane z generatywnym AI (IBM X-Force 2025)
- **4000%** wzrost AI-generowanych phishing emails od 2023 (SlashNext State of Phishing 2024)
- **$40B** przewidywane globalne straty z AI-enabled fraud do 2027 (Deloitte)
- Średni czas od proof-of-concept exploita do ataku na skalę: **z tygodni na godziny**
- **85%** cybersecurity professionals wskazuje generative AI jako przyczynę wzrostu ataków (ISC² 2024)

**Asymetria kosztów:**

| | Atakujący | Obrońca |
|---|---|---|
| Koszt AI phishing | ~$5 za kampanię | $4.5M średni koszt data breach |
| Czas przygotowania | minuty | tygodnie na incident response |
| Skalowalność | nieograniczona | limitowana budżetem |

To nie jest przyszłość — to **teraźniejszość**.

<!-- end_slide -->

## Kontekst BEST S.A. — Copilot + AWS

**Wasze środowisko — dlaczego to dotyczy właśnie nas:**

**Microsoft 365 + Copilot:**
- Korzystacie z Copilot na co dzień — summaryzacja, drafting, analiza dokumentów
- Copilot ma dostęp do waszych maili, plików SharePoint, Teams — to ogromna surface area
- Każdy prompt to potencjalna interakcja z danymi klientów i danymi wrażliwymi
- Indirect prompt injection przez email → Copilot może "przeczytać" złośliwą treść i wykonać na niej operacje

**Migracja do AWS:**
- Nowe workloady = nowe AI capabilities (Bedrock, SageMaker)
- Multi-cloud = więcej punktów integracji = więcej surface area
- Potrzeba spójnych polityk bezpieczeństwa AI **niezależnie od platformy**

**Sektor finansowy — dodatkowe ryzyko:**
- Dane klientów podlegają regulacjom (RODO, KNF)
- Reputacja jest kluczowym aktywem — jeden incydent = utrata zaufania
- AI hallucination w kontekście finansowym → decyzje o realnych konsekwencjach

→ _Przejdźmy do konkretów — zaczynamy od wycieków danych, bo to najczęstszy i najbardziej podstępny wektor._

<!-- end_slide -->

## Wycieki danych przez chatboty — mechanizmy

<!-- end_slide -->

## Wycieki danych — incydenty

<!-- end_slide -->

## Wycieki danych — enterprise vs consumer

<!-- end_slide -->

## Shadow AI — zagrożenia

<!-- end_slide -->

## Shadow AI — konsekwencje

<!-- end_slide -->

## AI Phishing — ewolucja ataków

<!-- end_slide -->

## AI Phishing — porównanie tradycyjny vs AI

<!-- end_slide -->

## AI Phishing — vishing i klonowanie głosu

<!-- end_slide -->

## Deepfake — mechanizm i zastosowania

<!-- end_slide -->

## Deepfake — przypadek Arup + rozpoznawanie

<!-- end_slide -->

## Automatyzacja ataków — techniki AI

<!-- end_slide -->

## Automatyzacja ataków — asymetria i WormGPT

<!-- end_slide -->

## Destrukcyjna autonomia agentów AI — ryzyka

<!-- end_slide -->

## Destrukcyjna autonomia agentów AI — konfiguracja uprawnień

<!-- end_slide -->

## Prompt Injection — typy i przykłady

<!-- end_slide -->

## Prompt Injection — PromptFoo demo

<!-- end_slide -->

## Halucynacje AI — typy i mechanizmy

<!-- end_slide -->

## Halucynacje AI — incydenty i weryfikacja

<!-- end_slide -->

## Od zagrożeń do rozwiązań

<!-- end_slide -->

## Zasady bezpiecznego korzystania z AI (1/2)

<!-- end_slide -->

## Zasady bezpiecznego korzystania z AI (2/2)

<!-- end_slide -->

## Framework oceny ryzyka narzędzi AI

<!-- end_slide -->

## Narzędzia bezpieczeństwa — AWS

<!-- end_slide -->

## Narzędzia bezpieczeństwa — Azure

<!-- end_slide -->

## Zasady vendor-neutral

<!-- end_slide -->

## Polityki jako enablery innowacji

<!-- end_slide -->

## Kiedy kontaktować PBI

<!-- end_slide -->

## Podsumowanie — 5 key takeaways

<!-- end_slide -->

## Call-to-action — odpowiedzialne AI + PBI

<!-- end_slide -->

## Q&A
