# Raport dziennej pracy nad aplikacja codex_clone

Data: 2026-05-18
Projekt: `/home/l/APP2/codex_clone`
Paczka do wyslania: `/home/l/Desktop/apka ver2.zip`

## Cel dnia

Celem bylo doprowadzenie lokalnej aplikacji CLI z prostego wrappera na Gemini do malego, dzialajacego agenta terminalowego. Priorytet byl praktyczny: uzytkownik wpisuje prosbe typu `stworz folder AI_TEST na pulpicie`, a aplikacja sama rozpoznaje intencje, wykonuje operacje lokalnie, loguje wynik i potwierdza sukces bez kopiowania komend przez uzytkownika.

## Stan poczatkowy

Aplikacja miala dzialajacy dostep do Gemini, podstawowe logowanie i proste wykonanie komend przez `subprocess`, ale zachowywala sie glownie jak chatbot. Model zuzywal zapytania na rzeczy, ktore Linux i Python mogly wykonac lokalnie. Wystepowaly problemy z:

- tworzeniem folderow na pulpicie,
- obsluga `~` i sciezek Desktop/Pulpit,
- zapisem plikow tekstowych,
- wieloetapowymi komendami,
- odmowami modelu mimo istnienia lokalnego executora,
- limitem Gemini `429 RESOURCE_EXHAUSTED`,
- zbyt silnym uzaleznieniem aplikacji od jednego providera.

## Najwazniejsze przebudowy

1. Dodano lokalny router przed modelem.

   Plik: `router/local_router.py`

   Router przechwytuje proste zadania i wykonuje je bez wywolania Gemini. Obejmuje to m.in. pytania o date, `pwd`, `ls`, sprawdzenie `curl --version`, proste tworzenie folderu na pulpicie oraz podstawowe odpowiedzi o linkach/statusie.

2. Dodano warstwe providerow.

   Pliki:
   - `providers/base.py`
   - `providers/config.py`
   - `providers/gemini_provider.py`
   - `providers/openai_compatible.py`

   Aplikacja nie jest juz sztywno przywiazana do Gemini. Ma `ProviderManager`, ktory obsluguje konfiguracje modelu i przelaczanie przez `/model`. Wspierane sa nazwy typu:

   - `gemini/...`
   - `openai/...`
   - `openrouter/...`

   Klucze API sa czytane lokalnie ze zmiennych srodowiskowych albo z `~/.config/<provider>/api.env`, a nie trzymane w paczce projektu.

3. Dodano lokalne komendy slash.

   Pliki:
   - `commands/base.py`
   - `commands/local_commands.py`

   Dzialaja komendy:

   - `/status`
   - `/model`
   - `/model NAZWA_MODELU`
   - `/tools`
   - `/help`

   Te komendy nie powinny zuzywac tokenow modelu.

4. Uporzadkowano executor narzedzi.

   Plik: `tools/executor.py`

   Executor zostal przestawiony na rejestr narzedzi zamiast jednego dlugiego bloku warunkow. Obsluguje akcje JSON, m.in.:

   - `shell_execute`
   - `create_folder`
   - `write_file`
   - `read_file`
   - `append_file`
   - akcje browserowe
   - akcje odpowiedzi tekstowej

5. Poprawiono walidacje komend.

   Plik: `tools/validator.py`

   Walidacja pozwala na potrzebne konstrukcje shellowe, w tym przekierowania, potoki i komendy wieloetapowe, ale klasyfikuje tryby ryzyka. Instalacje i polecenia typu `sudo apt install curl` wymagaja potwierdzenia.

6. Dodano logike oszczedzania tokenow.

   W `main.py` aplikacja najpierw probuje wykonac oczywiste operacje lokalnie. Dopiero zadania niejednoznaczne, wieloetapowe lub wymagajace interpretacji ida do modelu.

7. Dodano obsluge URL przed modelem.

   Aplikacja potrafi lokalnie wykryc URL, odwinac redirect z Facebooka (`l.facebook.com`) i uruchomic bootstrap przegladarki przed prosba o analize do modelu. Dzieki temu model nie marnuje zapytan na samo otwieranie linku.

8. Dodano banner startowy.

   W `main.py` dodano mniejszy, czytelny terminalowy napis:

   - `flAmeBornLLC | LLM Academy`
   - `LOCAL AI TERMINAL + BROWSER AGENT`

## Problemy i naprawy

1. Problem: `mkdir ~/Desktop/LINZ2` nie dzialalo stabilnie.

   Przyczyna: sciezka `~` i lokalizacja pulpitu byly zbyt naiwnie obslugiwane. Dodano wykrywanie pulpitu przez XDG i lokalny routing do `create_folder`.

2. Problem: model odpowiadal tekstem zamiast wykonywac akcje.

   Przyczyna: architektura byla blizej chat-wrappera niz runtime agenta. Dodano JSON action loop, executor i jasniejszy system prompt.

3. Problem: pliki tekstowe i wieloetapowe komendy byly blokowane.

   Przyczyna: zbyt restrykcyjny parser/walidator. Rozszerzono walidacje o redirection, pipes i chaining, przy zachowaniu potwierdzen dla bardziej ryzykownych polecen.

4. Problem: Gemini zuzywal limit dzienny na proste rzeczy.

   Przyczyna: brak lokalnej warstwy routingu przed LLM. Dodano `LocalRouter` i komendy slash, ktore dzialaja bez modelu.

5. Problem: blad Python `.format()` na JSON w promptach, np. `KeyError: '\n "type"'`.

   Przyczyna: przyklady JSON w prompt templates mialy pojedyncze klamry. Poprawiono prompt examples przez escapowanie klamer tam, gdzie bylo to potrzebne.

6. Problem: limit Gemini `429 RESOURCE_EXHAUSTED`.

   Przyczyna: dzienny limit free tier. Dodano obsluge bledow quota i prace nad przelacznikiem modeli przez `/model`, aby mozna bylo przejsc na OpenAI/OpenRouter, jesli lokalnie sa dostepne klucze.

7. Problem: testy przegladarki w sandboxie.

   Przyczyna: Chromium/Playwright w srodowisku narzedzia potrafi pasc na `sandbox_host_linux.cc` z `Operation not permitted`. To jest ograniczenie srodowiska testowego Codex, nie logiki aplikacji. W normalnym terminalu poza sandboxem przegladarka powinna byc testowana osobno.

## Testy i walidacja

W raporcie przebudowy zapisano wynik:

- 14 testow,
- 14 passed,
- kompilacja `py_compile` dla glownych modulow.

Po przywroceniu sesji ponownie sprawdzono:

- `py_compile` dla `main.py`, `commands`, `providers`, `router`, `tools` przechodzi,
- testy bez przegladarki przechodza,
- dwa testy browserowe padaja w sandboxie przez ograniczenie Chromium,
- zwykly systemowy `python3` nie ma modulu `google.genai`, ale projektowe `.venv` ma zaleznosci potrzebne do aplikacji.

## Bezpieczenstwo API

Sprawdzono paczke i projekt pod katem typowych sekretow. Nie znaleziono realnych kluczy API w plikach pakietu. W README jest tylko placeholder:

`GEMINI_API_KEY=your_real_key_here`

Paczka `apka ver2.zip` nie zawiera `.env`, `~/.config`, `venv`, `.venv`, logow runtime ani prywatnych plikow konfiguracyjnych z kluczami.

## Aktualny stan aplikacji

Aplikacja jest teraz malym lokalnym agentem terminalowym, a nie tylko chatbotem. Ma:

- lokalny executor,
- lokalny router oszczedzajacy tokeny,
- provider manager z `/model`,
- filesystem tools,
- shell tools,
- browser tools,
- logi sesji i komend,
- walidacje ryzyka,
- banner startowy,
- paczke zip na pulpicie.

## Znane ograniczenia

- Lokalny router jest celowo konserwatywny. Nie kazda fraza zostanie wykonana bez modelu.
- OpenAI/OpenRouter zadzialaja dopiero po dodaniu lokalnych kluczy API.
- Browser/Playwright wymaga testu poza sandboxem Codex.
- W katalogu projektu sa stare pomocnicze pliki patchy i backupy, ktore mozna pozniej posprzatac, ale nie sa potrzebne do paczki zip.

## Nastepne sensowne kroki

1. Uruchomic aplikacje normalnie:

   `cd /home/l/APP2/codex_clone`
   `.venv/bin/python main.py`

2. Przetestowac lokalnie:

   - `/status`
   - `/model`
   - `jaki dzis dzien`
   - `stworz folder AI_TEST na pulpicie`
   - `ls`

3. Jesli celem jest dalsza rozbudowa, nastepny etap powinien objac:

   - lepszy planner wielokrokowy,
   - prosty tryb task queue,
   - osobny smoke test bez Playwright,
   - czyszczenie starego root projektu przed publicznym wydaniem.

