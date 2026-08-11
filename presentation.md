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

**Jak dane „wyciekają" z organizacji przez narzędzia AI:**

**1. Trenowanie modelu na danych użytkowników**
- Consumer AI tools (ChatGPT Free, Gemini Free) domyślnie wykorzystują conversations do treningu
- Raz użyte dane stają się częścią wag modelu — **nie da się ich „usunąć"**
- Efekt: fragmenty kodu, wzorce, dane klientów mogą „wypłynąć" w odpowiedziach innym użytkownikom

**2. Logowanie i przechowywanie konwersacji**
- Każda interakcja jest zapisywana — retencja od 30 dni do bezterminowej
- Logi dostępne dla zespołów trust & safety, audytorów, a potencjalnie i atakujących
- Data breach u dostawcy AI = wyciek **waszych** danych

**3. Udostępnianie danych third-party**
- Plugins, integracje, Custom GPTs — dane przechodzą przez serwery stron trzecich
- Brak kontroli nad łańcuchem przetwarzania danych (sub-processors)
- Shared links do konwersacji — przypadkowe upublicznienie

**4. Ekstrakcja przez prompt injection**
- Atakujący mogą wyciągnąć system prompts i kontekst z RAG/knowledge base
- Indirect injection w dokumentach → eksfiltracja danych przez model

<!-- end_slide -->

## Wycieki danych — incydenty

**Udokumentowane przypadki — to nie teoria:**

**Samsung Electronics / ChatGPT (2023)**
- Dział semiconductor — 3 osobne incydenty w ciągu 20 dni od zniesienia banu na AI
- Pracownicy wkleili: **kod źródłowy** (debugging), **kod produkcyjny** (optymalizacja), **notatki z meetingów** (summaryzacja)
- Samsung natychmiast zabanował wszystkie generative AI tools
- Dane trafiły do training pipeline OpenAI — nieodwracalnie
- Źródło: TechRadar, The Register, Mashable (kwiecień 2023)

**LiteLLM / BerriAI — supply chain attack (marzec 2026)**
- LiteLLM: Python AI proxy library, **95M pobrań miesięcznie**
- Złośliwe wersje na PyPI zawierały credential harvester + backdoor
- **500 000 maszyn** skompromitowanych w 3 godziny
- ~300 GB danych wyeksfiltowanych, w tym API keys do OpenAI, Anthropic, AWS Bedrock
- Źródło: The Hacker News, Trend Micro (marzec 2026)

**Wspólny mianownik:** zaufanie do narzędzia + brak polityki = katastrofa

**⚠️ Co zrobić, jeśli przypadkowo udostępniłeś dane?**
1. Natychmiast powiadom PBI / Security Team
2. Udokumentuj: co, kiedy, w jakim narzędziu
3. Sprawdź politykę retencji danych dostawcy
4. Złóż żądanie usunięcia danych (jeśli dostępne — np. OpenAI Data Deletion Request)

<!-- end_slide -->

## Wycieki danych — enterprise vs consumer

**Nie wszystkie narzędzia AI są równe — porównanie:**

| Wymiar | Enterprise (Azure OpenAI, AWS Bedrock) | Consumer (ChatGPT Free, Gemini Free) |
|--------|---------------------------------------|--------------------------------------|
| **Data retention** | Konfigurowalne, domyślnie 0-30 dni, możliwość wyłączenia | 30 dni – bezterminowo, limited control |
| **Trening na danych** | ❌ Dane NIE są używane do treningu | ✅ Domyślnie TAK (opt-out dostępny) |
| **Tenant isolation** | Dedykowany deployment, VPC/VNet, encryption at rest | Shared infrastructure, brak izolacji |
| **Compliance** | SOC 2, ISO 27001, HIPAA, RODO | Ograniczone certyfikaty, T&C zmieniają się |
| **Audit logging** | CloudTrail, Azure Monitor — pełna kontrola | Brak wglądu w przetwarzanie |
| **Data residency** | Wybór regionu (EU, US) | Brak gwarancji lokalizacji |

**Praktyczne wnioski dla BEST S.A.:**

- **Copilot for M365** (wasze narzędzie) → tenant-level isolation, dane nie trenują modelu ✅
- **ChatGPT Free** w przeglądarce → dane mogą trenować model ⚠️
- **AWS Bedrock** (docelowy stack) → zero data retention opcjonalnie, VPC isolation ✅

**Zasada:** Enterprise tool z kontraktem > Consumer tool z opt-out > Consumer tool bez opt-out

→ _Wycieki to dopiero początek — zobaczmy co dzieje się, gdy pracownicy sami sięgają po narzędzia poza kontrolą organizacji._

<!-- end_slide -->

## Shadow AI — zagrożenia

**Shadow AI** = narzędzia AI używane przez pracowników **bez wiedzy i akceptacji organizacji** — poza kontrolą IT, compliance i PBI.

**3 kluczowe zagrożenia:**

1. **Wyciek danych do niekontrolowanych modeli**
   - Dane klientów trafiają do modeli trenowanych na inputach użytkowników
   - Brak DLP, brak logowania, brak możliwości audytu — dane znikają nieodwracalnie

2. **Naruszenie regulacji (RODO, KNF, tajemnica bankowa)**
   - Przetwarzanie danych osobowych w narzędziu bez umowy powierzenia
   - Brak podstawy prawnej do transferu danych poza EOG
   - Utrata kontroli nad retencją — nie wiesz, kiedy dane zostaną usunięte

3. **Podejmowanie decyzji na podstawie niezweryfikowanych wyników**
   - Hallucynacje modelu w analizie finansowej → błędne decyzje windykacyjne
   - Brak audit trail — nie wiadomo, kto podjął decyzję i na jakiej podstawie

**Scenariusze w firmie finansowej:**

- 📊 Analityk wkleja bazę dłużników do ChatGPT, żeby „szybciej przygotować raport"
- 📧 Pracownik windykacji generuje pisma do klientów w darmowym narzędziu AI — dane osobowe, kwoty zadłużenia, numery spraw
- 📈 Manager używa niezatwierdzonego AI do prognoz finansowych prezentowanych zarządowi — zero walidacji źródła

<!-- end_slide -->

## Shadow AI — konsekwencje

**Jak Shadow AI omija governance:**

1. **Brak w rejestrze przetwarzania** — narzędzie AI nie figuruje w ROPA (Records of Processing Activities), więc DPO nie wie o przetwarzaniu danych osobowych
2. **Obejście klasyfikacji danych** — pracownik kopiuje dane z systemu chronionego DLP do przeglądarki → żadna kontrola endpoint nie widzi tego jako exfiltration, bo to „legalne" copy-paste do webaplikacji

**Konsekwencje — poziom organizacji:**

| Ryzyko | Potencjalny skutek |
|---|---|
| Kara RODO (Art. 83) | do **€20M** lub 4% globalnego obrotu |
| Sankcje KNF | cofnięcie licencji, kary administracyjne |
| Data breach | utrata zaufania klientów, pozwy zbiorowe |
| Brak compliance | niezaliczenie audytu, wyższe składki ubezpieczeniowe |

**Konsekwencje — poziom pracownika:**

- ⚠️ Postępowanie dyscyplinarne za naruszenie polityki bezpieczeństwa
- ⚠️ Odpowiedzialność osobista za wyciek danych osobowych (Art. 82 RODO)
- ⚠️ Utrata certyfikatów zawodowych (w sektorze regulowanym)
- ⚠️ Odpowiedzialność karna w przypadku celowego działania (Art. 107 ustawy o ochronie danych)

**Kluczowy wniosek:** Shadow AI to nie problem technologiczny — to problem **procesowy i kulturowy**. Rozwiązanie: zatwierdzone narzędzia + edukacja + bezpieczne alternatywy.

→ _Shadow AI to nie jedyne ryzyko — zobaczmy jak AI wzmacnia tradycyjne wektory ataku, zaczynając od phishingu._

<!-- end_slide -->

## AI Phishing — ewolucja ataków

**4000%** wzrost AI-generowanych phishing emails od 2023 (SlashNext 2024)

AI zmienia phishing w **trzech wymiarach**:

<!-- pause -->

**1. Jakość językowa**
- Perfekcyjna gramatyka, interpunkcja, styl — zero literówek
- Dopasowanie rejestru do kontekstu (formalny mail vs luźny Slack)
- Natywny język ofiary — bez „tłumaczenia maszynowego"

<!-- pause -->

**2. Personalizacja**
- Scraping LinkedIn, social media, firmowych stron — automatycznie
- Referencje do realnych projektów, współpracowników, ostatnich eventów
- Timing — wiadomość trafia w kontekście (po spotkaniu, przed deadline)

<!-- pause -->

**3. Skalowalność**
- Tysiące unikatowych, spersonalizowanych wiadomości — koszt ~$5 za kampanię
- Każdy email jest inny → tradycyjne filtry pattern-matching zawodzą
- A/B testing w czasie rzeczywistym — AI optymalizuje skuteczność

→ _Zobaczmy to na konkretnych przykładach — tradycyjny phishing vs AI._

<!-- end_slide -->

## AI Phishing — porównanie tradycyjny vs AI

### Przykład 1: Email z banku

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->
**Tradycyjny phishing:**

_„Szanowny Klięt!_
_Twój konto zostal zablokowany._
_Kliknij tutaj aby odblokować_
_natychmiastowo. Podaj haslo_
_i numer karty._
_Dział Bezpeczności ING"_

❌ Błędy ortograficzne
❌ Generyczny — brak danych
❌ Łatwy do wykrycia

<!-- column: 1 -->
**AI-generated phishing:**

_„Dzień dobry, Panie Marku,_
_W związku z Pana ostatnią_
_transakcją z 14.07 na kwotę_
_2 847,50 PLN w MediaMarkt,_
_prosimy o potwierdzenie_
_tożsamości. Link aktywny 24h._
_Katarzyna Nowak,_
_Zespół Bezpieczeństwa ING"_

✅ Bezbłędny polski
✅ Personalizacja (imię, kwota)
✅ Trudny do odróżnienia

<!-- reset_layout -->

<!-- pause -->

### Przykład 2: SMS o przesyłce

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->
**Tradycyjny phishing:**

_„UWAGA!! Twoja paczka_
_nie mozę byc doręczona!!!_
_Zapłac 2,50zl oplate_
_inpost.tracking-pl.com/pay"_

❌ Wielkie litery, wykrzykniki
❌ Literówki: „mozę", „byc"
❌ Podejrzana domena

<!-- column: 1 -->
**AI-generated phishing:**

_„InPost: Przesyłka_
_nr 6240187295 oczekuje_
_w Paczkomacie KRA42M._
_Termin odbioru: do 16.07._
_Przedłuż o 48h:_
_inpost.pl.delivery-ext.com"_

✅ Realistyczny nr przesyłki
✅ Prawdziwy Paczkomat
✅ Subtelna podmiana domeny

<!-- reset_layout -->

<!-- pause -->

**Wniosek:** tradycyjne red flags (błędy, presja, generyczność) **przestają działać**.
Nowy paradygmat wykrywania wymaga weryfikacji kanałem zwrotnym, nie analizy treści.

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
