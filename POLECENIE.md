# Karta pracy -- Git podstawy (dla początkujących)

> **Cel pracy domowej:** Od zera, krok po kroku, przejść przez wszystkie pojęcia z lekcji `git.md`: konfiguracja Gita, repozytorium lokalne i zdalne, gałąź (branch), commit, push/pull, Pull Request i prosty konflikt. Każde zadanie zawiera **dokładne tłumaczenie teorii** zanim zaczniesz klikać oraz **weryfikację każdego praktycznego kroku** -- czyli "co powinieneś zobaczyć po każdej komendzie". Jeśli zobaczysz coś innego, **zatrzymaj się** i sprawdź, w którym miejscu odbiegłeś od scenariusza.

---

## Dla kogo jest ta karta pracy

* Nigdy wcześniej nie używałeś Gita (albo używałeś tylko klikając w IntelliJ bez zrozumienia).
* Słyszałeś słowa "commit", "branch", "pull request", ale nie wiesz, co dokładnie znaczą i jak się ze sobą łączą.
* Chcesz mieć **swoje pierwsze repozytorium na GitHubie**, do którego możesz wrzucić kod i pokazać go innym.

> **Nie przejmuj się, jeśli idzie wolno.** Cel tej karty to zrozumienie, **nie** wyścig. Lepiej zrozumieć 1 polecenie na zajęciach niż przepisać 20.

---

## Jak korzystać z tej karty pracy

Każde zadanie zawiera kilka sekcji -- **przeczytaj je w kolejności**, nie przeskakuj:

1. **Co ćwiczymy** -- 1 zdanie streszczające, co się nauczysz.
2. **Teoria w prostych słowach** -- wyjaśnienie pojęć **zanim** je użyjesz. To najważniejsza część dla początkujących -- przeczytaj ją powoli, dwa razy jeśli trzeba.
3. **Przygotowanie** -- gotowe komendy do skopiowania (najczęściej utworzenie katalogu i repo na GitHubie).
4. **Praktyka krok po kroku** -- ponumerowane kroki, **a po każdym kroku sekcja "Sprawdź:"** z dokładnym opisem, co powinieneś zobaczyć (output komendy, wygląd okna IntelliJ, stan na GitHubie).
5. **Częste błędy** -- co najczęściej się psuje na tym etapie i jak to naprawić.
6. **Pytania kontrolne** -- odpowiedzi wpisujesz do pliku `RAPORT.md` w głównym repo `git-podstawy-pd` (patrz [Sposób oddania pracy](#sposób-oddania-pracy)).

> **Każde zadanie ma swoje osobne repozytorium.** Nie mieszaj wszystkiego w jednym katalogu -- dzięki temu, jeśli coś zepsujesz w zadaniu 3, nie psujesz sobie zadania 4.

> **Najpierw CLI (terminal), potem IntelliJ.** W każdym zadaniu pokazujemy ten sam efekt **najpierw w terminalu** (żebyś zobaczył dokładnie, co Git robi), **potem w IntelliJ** (bo w pracy będziesz głównie klikać w IDE). Mapowanie "komenda CLI ↔ kliknięcie w IDE" to najszybsza droga do biegłości.

---

## Spis treści

1. [Słowniczek pojęć (przeczytaj na początku)](#słowniczek-pojęć-przeczytaj-na-początku)
2. [Zadanie 0 -- Przygotowanie środowiska (jednorazowe)](#zadanie-0--przygotowanie-środowiska-jednorazowe)
3. [Zadanie 1 -- Pierwsze repozytorium lokalne (init, add, commit, log)](#zadanie-1--pierwsze-repozytorium-lokalne-init-add-commit-log)
4. [Zadanie 2 -- Repozytorium na GitHubie (remote, push)](#zadanie-2--repozytorium-na-githubie-remote-push)
5. [Zadanie 3 -- Pierwsza gałąź funkcjonalna (branch, switch)](#zadanie-3--pierwsza-gałąź-funkcjonalna-branch-switch)
6. [Zadanie 4 -- Pierwszy Pull Request i merge do main](#zadanie-4--pierwszy-pull-request-i-merge-do-main)
7. [Zadanie 5 -- Aktualizacja lokalnego repo (fetch, pull)](#zadanie-5--aktualizacja-lokalnego-repo-fetch-pull)
8. [Zadanie 6 -- Pierwszy prosty konflikt (i jak go rozwiązać)](#zadanie-6--pierwszy-prosty-konflikt-i-jak-go-rozwiązać)
9. [Zadanie 7 -- Plik `.gitignore` (czego nie commitować)](#zadanie-7--plik-gitignore-czego-nie-commitować)
10. [Ściąga komend (do druku)](#ściąga-komend-do-druku)
11. [Sposób oddania pracy](#sposób-oddania-pracy)
12. [Materiały do doczytania](#materiały-do-doczytania)

---

## Słowniczek pojęć (przeczytaj na początku)

Zanim zaczniesz cokolwiek klikać, przeczytaj te definicje. **Nie musisz ich uczyć się na pamięć** -- wystarczy, że będziesz wiedział, gdzie wrócić, kiedy w zadaniu pojawi się nowe słowo. Każde pojęcie ma analogię z życia, żeby łatwiej zapamiętać.

* **Repozytorium (repo)** -- folder z Twoim projektem, który Git "obserwuje". W środku jest ukryty katalog `.git/` -- tam Git trzyma całą historię zmian. Analogia: kronika filmowa, w której zapisana jest każda klatka projektu.
* **Commit** -- zapisana migawka stanu projektu w danym momencie + krótki opis ("co zmieniłem"). Analogia: zdjęcie polaroidem z podpisem na odwrocie. Każdy commit ma unikalny **hash** (np. `a3f7b21`), który go identyfikuje.
* **Branch (gałąź)** -- równoległa linia commitów. Najczęściej masz gałąź główną (`main`) i obok niej kilka gałęzi roboczych (`feature/...`), na których pracujesz nad jedną zmianą. Analogia: kserówka książki, na której piszesz swoje notatki, nie ruszając oryginału.
* **`main` (lub `master`)** -- domyślna, główna gałąź. Tu trzymamy "wersję produkcyjną" kodu -- tę, która działa.
* **`feature/<nazwa>`** -- gałąź na konkretną nową funkcję. Konwencja nazewnictwa: `feature/login-form`, `feature/dodaj-koszyk`, itp.
* **Working directory** -- pliki, które widzisz w swoim folderze w danej chwili. Możesz je edytować dowolnie, Git ich jeszcze nie zapisał.
* **Staging area (index)** -- "poczekalnia" przed commitem. Pliki dodane przez `git add` czekają tam na zapisanie. Analogia: koszyk w sklepie -- wkładasz produkty, ale jeszcze nie płacisz. Commit = płatność.
* **Remote** -- zdalne repozytorium (np. na GitHubie). Twój lokalny komputer ma kopię, a "prawdziwa" wersja, do której wszyscy pchają zmiany, leży na serwerze. Domyślnie nazywa się `origin`.
* **`origin`** -- standardowa nazwa dla "głównego" remote'a. Kiedy klonujesz repo, Git automatycznie nazywa źródłowe repo `origin`.
* **Push** -- wysłanie Twoich commitów z komputera na remote (GitHub).
* **Fetch** -- pobranie informacji o zmianach z remote'a (np. nowe commity kolegi), **bez** wpływu na Twoje pliki. Bezpieczna operacja.
* **Pull** -- `fetch` + automatyczne wmergowanie pobranych zmian do Twojej gałęzi. Może zmienić Twoje pliki.
* **Merge** -- połączenie historii dwóch gałęzi w jedną. Najczęściej "wlejemy" gałąź `feature/...` do `main` po skończeniu pracy.
* **Konflikt** -- sytuacja, w której Git nie wie, którą wersję wybrać, bo dwie gałęzie zmieniły **tę samą linię** w tym samym pliku. Musisz mu pomóc -- ręcznie wybrać poprawną wersję.
* **Pull Request (PR) / Merge Request (MR)** -- prośba w GitHubie/GitLabie: "proszę o włączenie mojej gałęzi do `main`". Inni mogą obejrzeć Twój kod (**Code Review**), zostawić komentarze, zaakceptować i zmergować. Na zajęciach mówimy "PR" -- to po prostu mechanizm GitHuba.
* **Code Review (CR)** -- recenzja kodu przez kolegę przed wmergowaniem PR. Łapie błędy i pilnuje jakości.
* **GitHub Flow** -- prosty sposób pracy: (1) tworzysz feature branch, (2) commitujesz na nim, (3) otwierasz PR, (4) ktoś robi review, (5) mergujemy do `main`. Powtarzamy.
* **`.gitignore`** -- plik tekstowy ze wzorcami: "tych plików nigdy nie śledź". Tam wpisujesz `.idea/`, `target/`, `*.log`, `*.env` -- czyli wszystko, co jest tylko Twoje albo zawiera sekrety.

> **Nie martw się, jeśli teraz brzmi to abstrakcyjnie.** Po zadaniach 1-4 te słowa zaczną mieć sens, bo zobaczysz je w działaniu.

---

## Zadanie 0 -- Przygotowanie środowiska (jednorazowe)

**Co ćwiczymy:** Instalacja Gita, konfiguracja `user.name`/`user.email`, założenie konta GitHub, sprawdzenie że IntelliJ widzi Git.

### Teoria w prostych słowach

Zanim cokolwiek skomitujesz, Git musi wiedzieć, **kim jesteś** (imię + e-mail). Te dane wkleja do każdego commita jako "autor" -- inaczej historia byłaby anonimowa. **Robisz to raz w życiu** (na danym komputerze), potem Git pamięta.

Konfigurację Gita można ustawiać na trzech poziomach:

* **`--global`** -- ustawienia dla Twojego użytkownika na tym komputerze (wszystkie repozytoria).
* **`--local`** -- tylko dla jednego konkretnego repozytorium (np. inny e-mail w projekcie firmowym).
* **bez flagi** -- to samo co `--local`.

Dla początkującego: **zawsze używaj `--global`**. `--local` przyda się, jak będziesz miał dwa konta GitHub (firmowe + prywatne).

### Krok 0.1 -- Sprawdź wersję Gita

```bash
git --version
```

**Sprawdź:** Powinno wyświetlić coś w stylu `git version 2.42.0` (numer może być inny, byle ≥ 2.23). Jeśli pojawi się `command not found: git` -- Git nie jest zainstalowany. Pobierz z [https://git-scm.com/downloads](https://git-scm.com/downloads), zainstaluj, otwórz **nowe okno** terminala i powtórz.

### Krok 0.2 -- Ustaw imię i e-mail

Zastąp **swoim** imieniem i e-mailem (tym samym, którego użyjesz na GitHubie):

```bash
git config --global user.name "Jan Kowalski"
git config --global user.email "jan.kowalski@example.com"
```

**Sprawdź:**

```bash
git config --global user.name
git config --global user.email
```

Każda z dwóch komend powinna wypisać dokładnie to, co przed chwilą ustawiłeś. Jeśli wypisze coś innego albo nic -- powtórz krok 0.2.

### Krok 0.3 -- Ustaw domyślną nazwę gałęzi głównej

```bash
git config --global init.defaultBranch main
```

**Sprawdź:**

```bash
git config --global init.defaultBranch
```

Powinno wypisać: `main`. To sprawia, że nowe repozytoria startują z gałęzią `main` (nowoczesny standard) zamiast starszego `master`.

### Krok 0.4 -- Załóż konto na GitHubie

* Wejdź na [https://github.com/signup](https://github.com/signup).
* **Użyj tego samego e-maila**, którego użyłeś w kroku 0.2. To ważne -- inaczej commity nie pokażą się jako Twoje na GitHubie.
* Wymyśl login (krótki, profesjonalny -- pojawi się w URL-ach Twoich projektów).

**Sprawdź:** Zaloguj się na [https://github.com](https://github.com), kliknij swoją ikonkę w prawym górnym rogu → *Your profile*. Powinieneś zobaczyć swoją stronę profilu.

### Krok 0.5 -- Autoryzacja `git push` (token albo SSH)

Aby Git mógł **wrzucać** Twój kod na GitHub, musi się jakoś autoryzować. Są dwie drogi -- wybierz jedną.

**Opcja A (prostsza) -- HTTPS + Personal Access Token (PAT):**

1. Wejdź na [https://github.com/settings/tokens](https://github.com/settings/tokens) → *Generate new token (classic)*.
2. Note: `git-podstawy-pd`. Expiration: `90 days`. Scope: zaznacz **`repo`**.
3. *Generate token* → **SKOPIUJ TOKEN** (pojawi się tylko raz!) i zapisz w bezpiecznym miejscu.
4. Przy pierwszym `git push` (zadanie 2) Git zapyta o login i hasło → jako hasło wklej token.

**Opcja B -- klucz SSH:**

1. W terminalu: `ssh-keygen -t ed25519 -C "twoj@email.com"`. Enter, Enter, Enter (zostawiamy domyślne).
2. Wyświetl klucz publiczny: `cat ~/.ssh/id_ed25519.pub` -- zaznacz cały output, skopiuj.
3. Wejdź na [https://github.com/settings/ssh/new](https://github.com/settings/ssh/new) → Title: `Moj laptop`, Key: wklej. *Add SSH key*.
4. W dalszych zadaniach **zamiast** URL `https://github.com/<USER>/<repo>.git` używaj `git@github.com:<USER>/<repo>.git`.

> **Pierwszy raz?** Wybierz **Opcja A** -- jest najmniej rzeczy do złamania.

### Krok 0.6 -- Sprawdź, że IntelliJ widzi Git

1. Otwórz IntelliJ IDEA → *Settings* (Windows/Linux: `Ctrl+Alt+S`, macOS: `⌘,`) → *Version Control → Git*.
2. Pole **Path to Git executable** -- powinno mieć ścieżkę (np. `/usr/bin/git` na Linux/macOS, `C:/Program Files/Git/cmd/git.exe` na Windows). Jeśli puste, kliknij *Auto-detect*.
3. Kliknij **Test**.

**Sprawdź:** Powinno wyskoczyć małe okienko z wersją Gita (np. `Git version 2.42.0`). Jeśli pisze "Cannot run git" -- IntelliJ nie znalazł Gita. Wróć do kroku 0.1 i upewnij się, że `git --version` w **zwykłym terminalu** działa.

### Krok 0.7 -- Utwórz główne repo na raport

To repozytorium będzie zawierać Twój `RAPORT.md` -- plik z odpowiedziami do wszystkich zadań. Zadania 1-7 to **osobne repozytoria** (po jednym na zadanie).

```bash
mkdir git-podstawy-pd
cd git-podstawy-pd
git init
```

**Sprawdź:**

```bash
ls -a
```

Powinieneś zobaczyć (poza `.` i `..`): folder **`.git`**. To znak, że Git "obserwuje" ten folder. Plik `RAPORT.md` dodamy w zadaniu 2 -- na razie zostaw repo puste.

### Częste błędy w zadaniu 0

* **`command not found: git`** -- Git nie zainstalowany albo nie dodany do PATH. Reinstalacja i restart terminala.
* **E-mail w `git config` różni się od e-maila GitHub** -- commity pojawią się jako "unknown user". Ustaw ten sam e-mail w obu miejscach.
* **IntelliJ nie widzi Gita na Windowsie** -- najczęściej brakuje Git Bash. Reinstalacja Gita z [git-scm.com](https://git-scm.com) (zaznacz "Git from the command line and also from 3rd-party software" podczas instalacji).

---

## Zadanie 1 -- Pierwsze repozytorium lokalne (init, add, commit, log)

**Co ćwiczymy:** `git init`, `git status`, `git add`, `git commit`, `git log` -- pełny cykl życia commita, bez wychodzenia na GitHub.

### Teoria w prostych słowach

Każdy plik w Twoim folderze może być w jednym z **czterech stanów**:

1. **Untracked** -- Git go widzi, ale jeszcze nigdy nie obserwował. W `git status` świeci się na czerwono pod nagłówkiem "Untracked files".
2. **Staged** (poczekalnia) -- wrzucony do "koszyka" przez `git add`. Czeka na commit. W `git status` świeci się na zielono pod "Changes to be committed".
3. **Modified** -- był już kiedyś zacommitowany, ale od tamtej pory zmieniłeś treść. W `git status` świeci się na czerwono pod "Changes not staged for commit".
4. **Committed** -- zapisany w historii. W `git status` nie pojawia się (bo nic nowego się nie dzieje).

**Cykl pracy z każdym plikiem:** `[edytuj]` → `git add` → `git commit`. Powtarzasz to tysiące razy w karierze.

**Po co `git status`?** To Twój najlepszy przyjaciel. Wpisuj go **co chwilę** -- powie Ci, co się dzieje. Każdy dobry deweloper wpisuje `git status` 20 razy dziennie.

### Przygotowanie

```bash
cd ~                              # przejdź do katalogu domowego (lub gdzie chcesz)
mkdir git-zad1-pierwszy-commit
cd git-zad1-pierwszy-commit
git init
```

**Sprawdź:** Po `git init` zobaczysz: `Initialized empty Git repository in .../git-zad1-pierwszy-commit/.git/`. To znak, że repo zostało utworzone.

```bash
git status
```

**Sprawdź:** Powinno wypisać:
```
On branch main
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```

### Praktyka -- Wariant A (CLI / terminal)

**Krok 1.** Utwórz pierwszy plik:

```bash
echo "# Moja pierwsza notatka" > NOTATKI.md
```

**Sprawdź:**

```bash
ls
```
Powinieneś zobaczyć: `NOTATKI.md`.

```bash
git status
```

Powinno pokazać:
```
On branch main
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        NOTATKI.md
nothing added to commit but untracked files present
```

Plik jest **untracked** -- Git go zobaczył, ale nie obserwuje.

**Krok 2.** Dodaj plik do staging area:

```bash
git add NOTATKI.md
```

**Sprawdź:**

```bash
git status
```

Powinno teraz pokazać (pod zielonym nagłówkiem):
```
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   NOTATKI.md
```

Plik jest **staged** -- czeka w "koszyku" na commit.

**Krok 3.** Zrób pierwszy commit:

```bash
git commit -m "init: dodaj pierwszą notatkę"
```

**Sprawdź:**

```bash
git status
```
Powinno teraz pokazać:
```
On branch main
nothing to commit, working tree clean
```
"Working tree clean" = wszystko zacommitowane, nic się nie dzieje. Świetnie.

```bash
git log
```

Powinieneś zobaczyć **jeden** commit:
```
commit a3f7b21...   (hash u Ciebie będzie inny)
Author: Twoje Imię <twoj@email.com>
Date:   Wed May 20 ...

    init: dodaj pierwszą notatkę
```

**Sprawdź:** Imię i e-mail muszą się zgadzać z tymi z zadania 0.5. Jeśli "Author" pokazuje kogoś innego -- masz złą konfigurację. Wróć do zadania 0.

**Krok 4.** Drugi commit -- modyfikujemy istniejący plik:

```bash
echo "" >> NOTATKI.md
echo "## Co zrobiłem dziś" >> NOTATKI.md
echo "- nauczyłem się git add i git commit" >> NOTATKI.md
```

**Sprawdź:**

```bash
git status
```

Powinno teraz pokazać (czerwone):
```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   NOTATKI.md
```

Plik jest **modified** -- był wcześniej zacommitowany, ale od tamtej pory się zmienił.

```bash
git diff
```

Powinieneś zobaczyć dokładnie te trzy linie, które dodałeś, oznaczone zielonym `+`. `git diff` pokazuje **co się zmieniło** od ostatniego commita.

**Krok 5.** Zacommituj zmianę:

```bash
git add NOTATKI.md
git commit -m "docs: dodaj sekcję 'co zrobiłem dziś'"
```

**Sprawdź:**

```bash
git log --oneline
```

Powinieneś zobaczyć dwa commity w jednej linii każdy:
```
b8c4d12 docs: dodaj sekcję 'co zrobiłem dziś'
a3f7b21 init: dodaj pierwszą notatkę
```

`--oneline` to skrócony widok -- najczęściej używany.

**Krok 6.** Ładny widok historii w postaci drzewka:

```bash
git log --oneline --graph --decorate --all
```

Na razie wygląda jak prosta linia (bo masz tylko jedną gałąź), ale w zadaniu 4 pojawią się rozgałęzienia. Zapamiętaj tę komendę -- będziesz jej używał często.

### Praktyka -- Wariant B (IntelliJ IDEA)

> **Reset przed wariantem B** -- żeby zacząć od czystego stanu bez psucia tego, co już masz, **utwórz nowy folder na ten wariant**:
>
> ```bash
> cd ~
> mkdir git-zad1-pierwszy-commit-intellij
> cd git-zad1-pierwszy-commit-intellij
> ```

1. Otwórz IntelliJ → *File → Open* → wskaż `git-zad1-pierwszy-commit-intellij`.
2. *VCS → Enable Version Control Integration…* → wybierz **Git** → OK. (To samo, co `git init` w terminalu.)

   **Sprawdź:** W prawym dolnym rogu okna IntelliJ pojawi się napis `main` -- to nazwa aktualnej gałęzi.

3. *File → New → File* → nazwa: `NOTATKI.md` → OK. IntelliJ zapyta: "Add file to Git?" → kliknij **Add**. (To samo, co `git add`.)

   **Sprawdź:** Nazwa pliku w panelu projektowym (lewo) powinna być **zielona** -- to znak, że plik jest staged.

4. W edytorze wpisz:
   ```
   # Moja pierwsza notatka
   ```
   Zapisz (`Ctrl+S` / `⌘S`).

5. Otwórz **Commit tool window**: `Ctrl+K` (Windows/Linux) lub `⌘K` (macOS).

   **Sprawdź:** Po lewej stronie zobaczysz pole na wiadomość, niżej listę plików do zacommitowania (`NOTATKI.md` z zaznaczonym checkboxem).

6. W polu wiadomości wpisz: `init: dodaj pierwszą notatkę`. Kliknij **Commit**.

   **Sprawdź:** Otwórz *Git tool window* (`Alt+9` / `⌘9`) → zakładka **Log**. Powinieneś zobaczyć jeden commit z Twoją wiadomością.

7. Edytuj `NOTATKI.md` -- dodaj kilka linii. Zapisz.

   **Sprawdź:** Nazwa pliku w panelu projektowym powinna stać się **niebieska** (modified, ale niezacommitowane). Numerek przy ikonce *Commit* w lewym panelu (`Ctrl+K`) pokaże, że masz `1` zmianę do zacommitowania.

8. `Ctrl+K` → wiadomość: `docs: dodaj kolejne notatki` → **Commit**.

   **Sprawdź:** *Git tool window → Log* pokazuje dwa commity. Pierwszy (najnowszy) na górze.

### Częste błędy w zadaniu 1

* **"Please tell me who you are"** przy `git commit` -- nie ustawiłeś `user.name`/`user.email`. Wróć do zadania 0.2.
* **`git add .` zamiast `git add NOTATKI.md`** -- działa, ale dodaje **wszystkie** zmiany w folderze, w tym śmieci. Dla początkującego: dodawaj plik po pliku, żeby kontrolować, co commitujesz.
* **Pomylona wiadomość commita** -- niestety nie da się jej łatwo zmienić w ostatnim commicie (potrzebny `git commit --amend`). Na razie -- po prostu zacommituj kolejny raz z lepszą wiadomością.

### Co ma być po zadaniu (lokalnie)

* [ ] Dwa katalogi: `git-zad1-pierwszy-commit/` i `git-zad1-pierwszy-commit-intellij/`.
* [ ] W obu: `git log --oneline` pokazuje **co najmniej 2 commity**.
* [ ] W obu: `git status` pokazuje "nothing to commit, working tree clean".

### Pytania do RAPORT.md

1. Co dokładnie zrobił `git init`? Co pojawiło się w Twoim folderze?
2. Czym różni się stan "untracked" od "modified"? Podaj przykład każdego.
3. Po co istnieje staging area (czyli krok `git add`)? Dlaczego Git nie commituje od razu wszystkich zmian?
4. Co pokazuje `git log` a co `git log --oneline`? Kiedy używasz którego?
5. Załącz screenshot z `git log --oneline` w terminalu **i** z widoku Log w IntelliJ -- z Twoimi 2 commitami.

---

## Zadanie 2 -- Repozytorium na GitHubie (remote, push)

**Co ćwiczymy:** Utworzenie repo na GitHubie, `git remote add`, `git push -u origin main`. Pierwszy raz wrzucasz kod do chmury.

### Teoria w prostych słowach

Do tej pory cała Twoja praca była **tylko na Twoim komputerze**. Jeśli komputer zgubisz albo skasujesz folder -- praca przepada. Dlatego trzymamy kod także na serwerze (GitHub, GitLab). Nazywamy taki serwer **remote**.

Lokalne repo i remote to **dwie osobne kopie** tego samego projektu. Synchronizujesz je dwiema komendami:

* **`git push`** -- "wyślij moje commity na serwer".
* **`git pull`** -- "ściągnij commity z serwera do mnie".

Każde lokalne repo może być powiązane z **jednym lub kilkoma** remote'ami. Konwencja: główny remote nazywamy **`origin`** (czyli "źródło"). Wskazuje na URL Twojego repo na GitHubie.

Komenda `git push -u origin main` znaczy: "wyślij moją gałąź `main` na remote `origin` i **zapamiętaj** (`-u`), że to jest jej śledzony odpowiednik". Po pierwszym pushu wystarczy potem pisać krótko `git push`.

### Przygotowanie

#### Lokalnie

```bash
cd ~
mkdir git-zad2-github
cd git-zad2-github
git init
git branch -M main           # upewnij się, że gałąź nazywa się main (nie master)
```

**Sprawdź:**

```bash
git status
```
Powinno pokazać: `On branch main`, `No commits yet`.

#### Na GitHubie

1. Otwórz [https://github.com/new](https://github.com/new).
2. **Repository name:** `git-zad2-github`.
3. **Description:** `Pierwsze repo na GitHubie -- nauka push`.
4. **Visibility:** **Public** (żeby prowadzący widział).
5. **NIE zaznaczaj** "Add a README file", "Add .gitignore", "Add a license" -- chcemy puste repo, do którego sami wrzucimy zawartość.
6. Kliknij **Create repository**.
7. Po utworzeniu GitHub pokaże Ci instrukcje "...or push an existing repository from the command line". Skopiuj URL (np. `https://github.com/<TWOJ-USER>/git-zad2-github.git`).

**Sprawdź:** Otwórz `https://github.com/<TWOJ-USER>/git-zad2-github` w przeglądarce. Powinno pokazać puste repo z instrukcjami quick setup.

### Praktyka -- Wariant A (CLI / terminal)

**Krok 1.** Zrób pierwszy lokalny commit (bez tego nie ma czego wypchać):

```bash
echo "# git-zad2-github" > README.md
echo "Moje pierwsze repo na GitHubie -- ćwiczenie z karty pracy." >> README.md
git add README.md
git commit -m "init: dodaj README"
```

**Sprawdź:** `git log --oneline` -- jeden commit `init: dodaj README`.

**Krok 2.** Powiąż lokalne repo z remote'em (zastąp `<TWOJ-USER>`):

```bash
git remote add origin https://github.com/<TWOJ-USER>/git-zad2-github.git
```

**Sprawdź:**

```bash
git remote -v
```

Powinno wypisać:
```
origin  https://github.com/<TWOJ-USER>/git-zad2-github.git (fetch)
origin  https://github.com/<TWOJ-USER>/git-zad2-github.git (push)
```

Dwie linie (jedna do pobierania, druga do wysyłania) -- to normalne. Jeśli pomyliłeś URL i chcesz to zmienić, użyj `git remote set-url origin <nowy-url>`. Jeśli chcesz całkiem usunąć remote: `git remote remove origin`.

**Krok 3.** Pierwszy push:

```bash
git push -u origin main
```

Git zapyta o login i hasło (jeśli używasz HTTPS):
* **Username:** Twój login GitHub.
* **Password:** **token** z zadania 0.5 (NIE hasło do konta GitHub -- GitHub od dawna nie akceptuje hasła).

**Sprawdź:** Output powinien wyglądać mniej więcej tak:
```
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 234 bytes | 234.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/<TWOJ-USER>/git-zad2-github.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main' from 'origin'.
```

**Sprawdź (najważniejsze):** Odśwież stronę repo na GitHubie (`F5`). Powinieneś teraz zobaczyć swój plik `README.md` i jeden commit "init: dodaj README" z Twoim imieniem.

**Krok 4.** Dodaj jeszcze jeden commit i wypchnij:

```bash
echo "" >> README.md
echo "## O mnie" >> README.md
echo "Imię Nazwisko, początkujący programista." >> README.md
git add README.md
git commit -m "docs: dodaj sekcję 'O mnie' do README"
git push
```

(Teraz nie potrzebujesz `-u origin main` -- Git pamięta, bo ustawiłeś to w kroku 3.)

**Sprawdź:** Odśwież stronę repo na GitHubie. README powinien mieć nową sekcję, a w zakładce **Commits** widzisz **2 commity**.

### Praktyka -- Wariant B (IntelliJ IDEA)

> **Reset przed wariantem B:**
>
> 1. Na GitHubie usuń repo: [https://github.com/<TWOJ-USER>/git-zad2-github](https://github.com/) → *Settings* → na dole *Delete this repository*. Potwierdź nazwą.
> 2. Lokalnie usuń folder: `cd ~ && rm -rf git-zad2-github`.
> 3. Utwórz repo na GitHubie ponownie (te same kroki co w "Na GitHubie" powyżej) -- ale tym razem **nazwij je `git-zad2-github-intellij`** (żeby nie kolidowało z wariantem A, jeśli go zachowałeś).

1. IntelliJ → *File → New → Project* → po lewej *Empty Project* → Location: `~/git-zad2-github-intellij`, Name: `git-zad2-github-intellij` → **Create**.
2. *VCS → Enable Version Control Integration…* → Git → OK.
3. *File → New → File* → `README.md`. Wpisz: `# git-zad2-github-intellij`. Zapisz. Kliknij **Add** w okienku "Add file to Git".
4. `Ctrl+K` → wiadomość: `init: dodaj README` → **Commit**.

   **Sprawdź:** *Git tool window → Log* -- jeden commit.

5. *Git → Manage Remotes…* → **+** → Name: `origin`, URL: `https://github.com/<TWOJ-USER>/git-zad2-github-intellij.git` → OK.

   **Sprawdź:** W oknie Manage Remotes widzisz wpis `origin` z Twoim URL.

6. Push: `Ctrl+Shift+K` (Windows/Linux) / `⌘⇧K` (macOS). Pojawi się okno *Push Commits to ...* z Twoim commitem.
7. Kliknij **Push**. Jeśli IntelliJ zapyta o credentials -- login + token jak w wariancie A.

   **Sprawdź:** Na dole IntelliJ pojawi się zielony pasek "Pushed master to origin/main" (lub podobny). Odśwież GitHub w przeglądarce -- README jest tam.

8. Otwórz README w IntelliJ, dodaj sekcję "O mnie", zapisz. `Ctrl+K` → wiadomość: `docs: O mnie` → **Commit and Push** (rozwiń strzałkę przy *Commit*).

   **Sprawdź:** GitHub pokazuje 2 commity.

### Częste błędy w zadaniu 2

* **`fatal: remote origin already exists`** -- już dodałeś remote (np. próbowałeś dwa razy). Usuń go: `git remote remove origin`, potem dodaj ponownie.
* **`! [rejected] main -> main (fetch first)`** przy push -- na GitHubie jest commit, którego nie masz lokalnie (najczęściej zaznaczyłeś "Add a README" podczas tworzenia repo). Rozwiązanie: `git pull origin main --allow-unrelated-histories`, rozwiąż ewentualny konflikt (zadanie 6), potem push.
* **`Support for password authentication was removed`** -- GitHub odrzucił Twoje hasło. Musisz użyć tokena PAT (zadanie 0.5, Opcja A).
* **403 / 401 przy push** -- token z złym scope (musi być `repo`) albo wygasł. Wygeneruj nowy.

### Co ma być na GitHubie po zadaniu

* [ ] Repo `git-zad2-github` (wariant A) publiczne, z 2 commitami i pełnym README.
* [ ] (Opcjonalnie) repo `git-zad2-github-intellij` (wariant B) publiczne, z 2 commitami.
* [ ] W obu: commity podpisane Twoim e-mailem (kliknij commit na GitHubie -- powinieneś zobaczyć swoją ikonkę).

### Pytania do RAPORT.md

1. Czym jest "remote" i dlaczego standardowo nazywamy go `origin`?
2. Co robi flaga `-u` w `git push -u origin main`? Co by się stało, gdybyś jej nie użył przy pierwszym pushu?
3. Co pokazuje `git remote -v`? Dlaczego są tam dwie linie (fetch i push)?
4. Dlaczego GitHub nie pozwala już używać hasła do `git push`? Co używamy zamiast tego?
5. Załącz screenshot strony Twojego repo `git-zad2-github` na GitHubie z widoczną historią 2 commitów.

---

## Zadanie 3 -- Pierwsza gałąź funkcjonalna (branch, switch)

**Co ćwiczymy:** `git branch`, `git switch -c`, praca na gałęzi feature, push gałęzi na remote.

### Teoria w prostych słowach

Wyobraź sobie, że jesteś w połowie pisania nowej funkcji, a w międzyczasie szef prosi Cię o pilną poprawkę bugu na produkcji. Jeśli wszystko commitujesz na `main`, masz problem -- niedokończona funkcja blokuje pilny fix.

**Rozwiązanie: gałęzie (branche).** Tworzysz osobną gałąź na każdą zmianę:

* `main` -- zawsze stabilna, działa, gotowa do wdrożenia.
* `feature/dodaj-koszyk` -- Twoja praca nad koszykiem.
* `feature/zmien-kolory` -- praca kolegi nad UI.
* `bugfix/login-crash` -- pilny fix.

Każda gałąź to **osobna linia commitów**, równoległa do innych. Kiedy skończysz pracę na gałęzi, **mergujesz** ją z powrotem do `main`.

**Konwencja nazw (przyjmij jako standard):**

* `feature/<krótki-opis>` -- nowa funkcja, np. `feature/login-form`.
* `bugfix/<opis>` -- naprawa buga.
* `hotfix/<opis>` -- pilna naprawa na produkcji.
* `chore/<opis>` -- "porządki" (refactor, update zależności).

Nazwy małymi literami, z myślnikami zamiast spacji. Po `/` -- krótko, ale konkretnie.

**Dwie najważniejsze komendy:**

* `git switch -c feature/xyz` -- "utwórz nową gałąź `feature/xyz` i przełącz się na nią". `-c` = create.
* `git switch main` -- "przełącz się na istniejącą gałąź `main`".

(Starsza składnia: `git checkout -b ...` -- działa, ale używaj `switch`, jest jaśniejsza.)

### Przygotowanie

#### Lokalnie

```bash
cd ~
mkdir git-zad3-branch
cd git-zad3-branch
git init
git branch -M main
```

#### Na GitHubie

1. [https://github.com/new](https://github.com/new) → `git-zad3-branch`, Public, BEZ README.
2. *Create repository*.
3. Lokalnie powiąż remote:

```bash
git remote add origin https://github.com/<TWOJ-USER>/git-zad3-branch.git
```

### Skrypt setupowy

```bash
cat > app.txt << 'EOF'
=== Aplikacja TODO ===

Wersja: 1.0
Autor: <Twoje imię>

Funkcje:
- dodawanie zadań
- usuwanie zadań
EOF

git add app.txt
git commit -m "init: szkielet aplikacji TODO"
git push -u origin main
```

**Sprawdź:** Na GitHubie -- 1 commit, plik `app.txt`.

### Praktyka -- Wariant A (CLI / terminal)

**Krok 1.** Sprawdź, jakie masz gałęzie:

```bash
git branch
```

Powinno pokazać:
```
* main
```
Gwiazdka oznacza "tu jesteś". Masz tylko `main`.

**Krok 2.** Utwórz nową gałąź i przełącz się na nią:

```bash
git switch -c feature/dodaj-edycje
```

**Sprawdź:**

```bash
git branch
```

Powinno pokazać:
```
* feature/dodaj-edycje
  main
```
Gwiazdka jest teraz przy `feature/dodaj-edycje`. Jesteś na nowej gałęzi.

```bash
git status
```
Powinno wyświetlić: `On branch feature/dodaj-edycje`.

**Krok 3.** Zrób zmianę w pliku:

```bash
cat > app.txt << 'EOF'
=== Aplikacja TODO ===

Wersja: 1.1
Autor: <Twoje imię>

Funkcje:
- dodawanie zadań
- usuwanie zadań
- edycja zadań
EOF
```

**Sprawdź:**

```bash
git diff
```

Powinno pokazać:
* Linia `Wersja: 1.0` na czerwono z `-`, linia `Wersja: 1.1` na zielono z `+`.
* Nowa linia `- edycja zadań` na zielono z `+`.

**Krok 4.** Zacommituj zmianę:

```bash
git add app.txt
git commit -m "feat: dodaj funkcję edycji zadań"
```

**Sprawdź:**

```bash
git log --oneline
```

Powinieneś zobaczyć **2 commity**: nowy `feat: dodaj funkcję edycji zadań` na górze, niżej `init: szkielet aplikacji TODO`.

**Krok 5.** Wypchnij gałąź na GitHub:

```bash
git push -u origin feature/dodaj-edycje
```

**Sprawdź:**

```
* [new branch]      feature/dodaj-edycje -> feature/dodaj-edycje
```

**Sprawdź (najważniejsze):** Odśwież repo na GitHubie. Nad listą plików zobaczysz **dropdown z gałęziami** (domyślnie `main`) -- kliknij go, powinieneś zobaczyć **dwie** gałęzie: `main` i `feature/dodaj-edycje`. Kliknij `feature/dodaj-edycje` -- zobaczysz `app.txt` z wersją 1.1 (Twoja zmiana).

Wróć na `main` (przez dropdown) -- tam wciąż jest wersja 1.0. **To jest cała magia branchy: dwie wersje równolegle.**

**Krok 6.** Przełącz się z powrotem na `main`:

```bash
git switch main
cat app.txt
```

**Sprawdź:** Plik `app.txt` powinien być w wersji 1.0 (BEZ "edycji zadań") -- bo wróciłeś na gałąź `main`, gdzie tej zmiany nie ma. Git automatycznie podmienia zawartość plików przy zmianie gałęzi.

```bash
git switch feature/dodaj-edycje
cat app.txt
```

Plik znów ma wersję 1.1. Świetnie -- rozumiesz, jak działają branche.

### Praktyka -- Wariant B (IntelliJ IDEA)

> **Reset przed wariantem B:** Otwórz katalog `git-zad3-branch` w IntelliJ -- nie trzeba kasować, kontynuujemy na tym samym repo.

1. Otwórz katalog w IntelliJ (*File → Open*).
2. W **prawym dolnym rogu** zobaczysz nazwę aktualnej gałęzi (np. `feature/dodaj-edycje` -- bo zostawiłeś ją po wariancie A). Kliknij na nią.
3. Otworzy się popup **Git Branches** -- zobaczysz listę gałęzi (Local: `main`, `feature/dodaj-edycje`).
4. Kliknij `main` → **Checkout**.

   **Sprawdź:** Prawy dolny róg pokazuje teraz `main`. Plik `app.txt` w edytorze pokazuje wersję 1.0.

5. Ponownie kliknij branch w prawym dolnym rogu → **+ New Branch** → nazwa: `feature/dodaj-kategorie` → checkbox "Checkout branch" zaznaczony → **Create**.

   **Sprawdź:** Prawy dolny róg pokazuje teraz `feature/dodaj-kategorie`. Jesteś na nowej gałęzi.

6. Edytuj `app.txt` w IntelliJ -- dodaj na końcu linię `- kategorie zadań`. Zapisz.

7. `Ctrl+K` → wiadomość: `feat: dodaj kategorie zadań` → rozwiń strzałkę przy **Commit** → **Commit and Push…** → w okienku Push **Push**.

   **Sprawdź:** Otwórz repo na GitHubie → dropdown gałęzi → powinieneś teraz widzieć **3 gałęzie**: `main`, `feature/dodaj-edycje`, `feature/dodaj-kategorie`.

### Częste błędy w zadaniu 3

* **`fatal: A branch named 'feature/xyz' already exists`** -- nie da się utworzyć gałęzi o nazwie, która już istnieje. Albo użyj innej nazwy, albo `git switch feature/xyz` (bez `-c`), żeby się na nią przełączyć.
* **Switch nie zadziała, bo masz niezacommitowane zmiany** -- Git może odmówić zmiany gałęzi, jeśli miałyby zostać nadpisane. Rozwiązanie: zacommituj zmiany albo użyj `git stash` (w karcie zaawansowanej -- na razie po prostu zacommituj).
* **Po `git push` na nowej gałęzi nie ma jej na GitHubie** -- zapomniałeś `-u origin <nazwa-gałęzi>`. Bez tej części Git nie wie, gdzie wysłać.
* **Plik `app.txt` "zniknął" po przełączeniu gałęzi** -- nie zniknął, tylko Git pokazał wersję z innej gałęzi. Wróć przez `git switch <nazwa>`.

### Co ma być na GitHubie po zadaniu

* [ ] Repo `git-zad3-branch` publiczne.
* [ ] **3 gałęzie**: `main`, `feature/dodaj-edycje`, `feature/dodaj-kategorie`.
* [ ] Na `main`: `app.txt` w wersji 1.0.
* [ ] Na `feature/dodaj-edycje`: `app.txt` z linią `- edycja zadań`.
* [ ] Na `feature/dodaj-kategorie`: `app.txt` z linią `- kategorie zadań`.

### Pytania do RAPORT.md

1. Czym jest gałąź (branch) w Gicie? Po co tworzymy `feature/...` zamiast commitować bezpośrednio na `main`?
2. Co robi `git switch -c <nazwa>`, a co `git switch <nazwa>` (bez `-c`)? Kiedy używasz którego?
3. Jaka jest konwencja nazewnictwa branchy w Twoim zespole? (Wymyśl ją.) Dlaczego dobra konwencja jest ważna?
4. Co zaobserwowałeś, kiedy przełączyłeś się między gałęziami i zawartość pliku się zmieniła? Wyjaśnij swoimi słowami, co się stało.
5. Załącz screenshot strony repo na GitHubie z otwartym dropdownem gałęzi -- powinno być widać wszystkie 3 gałęzie.

---

## Zadanie 4 -- Pierwszy Pull Request i merge do main

**Co ćwiczymy:** Utworzenie PR na GitHubie, opis PR, prosty Code Review (samodzielnie), merge PR do `main`, synchronizacja lokalnego repo po merge.

### Teoria w prostych słowach

Gałąź to początek pracy. **Pull Request (PR)** to jej zakończenie -- moment, w którym mówisz: "skończyłem, wmergujmy to do `main`". Mechanika:

1. Pracujesz na `feature/...`, robisz commity, pushujesz.
2. Na GitHubie tworzysz **Pull Request** -- formularz mówi: "chcę wziąć moją gałąź `feature/...` i wlać ją do `main`".
3. Inni (lub Ty sam, w pracy domowej) **przeglądają** kod -- mogą zostawić komentarze ("zmień to", "literówka tutaj").
4. Jeśli wszystko OK, klikasz **Merge pull request** -- GitHub łączy gałęzie.
5. Lokalnie robisz `git pull` na `main`, żeby ściągnąć zmergowaną zmianę.

**Dlaczego PR a nie po prostu merge?**

* **Code Review** -- ktoś inny patrzy na Twój kod, łapie błędy, których nie zauważyłeś.
* **Historia** -- PR zostaje w GitHubie na zawsze, z całą dyskusją. Za rok możesz wrócić i zobaczyć: "dlaczego to zmieniliśmy?".
* **CI/CD** -- na PR uruchamiają się testy automatyczne. Czerwony PR = nie mergujemy.
* **Polityka** -- w pracy najczęściej `main` jest **chroniony** -- nie da się commitować bezpośrednio, tylko przez PR.

**Dobry PR ma:**

* Tytuł w trybie rozkazującym, do 70 znaków. "Dodaj walidację e-maila", nie "dodalem walidacje".
* Opis: **co** zmieniłem i **dlaczego**. 2-5 zdań.
* (Opcjonalnie) screenshot, jeśli zmiana dotyczy UI.

### Przygotowanie

> Kontynuujemy na repo `git-zad3-branch` z poprzedniego zadania. Jeśli go nie masz -- zrób zadanie 3.

```bash
cd ~/git-zad3-branch
git switch feature/dodaj-edycje
git status
```

**Sprawdź:** `On branch feature/dodaj-edycje`, `nothing to commit, working tree clean`.

### Praktyka -- Wariant A (GitHub UI)

**Krok 1.** Otwórz repo na GitHubie. Jeśli masz świeży push, GitHub może już sam pokazać **żółtą belkę**: *"feature/dodaj-edycje had recent pushes ... Compare & pull request"*. Kliknij ten przycisk i przeskocz do kroku 3.

W przeciwnym razie:

**Krok 2.** Zakładka **Pull requests** (na górze repo) → **New pull request**.

* **base:** `main` (gałąź, do której chcesz wmergować -- czyli "cel").
* **compare:** `feature/dodaj-edycje` (gałąź, z której chcesz wmergować -- czyli "źródło").

**Sprawdź:** Pod spodem zobaczysz **diff** -- to jest dokładnie to, co zostanie wmergowane. Linie czerwone (z `-`) zostaną usunięte z `main`, zielone (z `+`) dodane.

* Powinieneś zobaczyć: usunięta linia `Wersja: 1.0`, dodane: `Wersja: 1.1` i `- edycja zadań`.

Kliknij **Create pull request**.

**Krok 3.** Wypełnij formularz PR:

* **Title:** `Dodaj funkcję edycji zadań`.
* **Description:**
  ```
  ## Co zmieniam
  - Dodaję pozycję "edycja zadań" do listy funkcji.
  - Bumpuję wersję aplikacji 1.0 → 1.1.

  ## Dlaczego
  Edycja była wymagana w specyfikacji, a jej brak był zgłaszany przez użytkowników.

  ## Test plan
  - [x] Sprawdziłem zawartość pliku app.txt lokalnie.
  ```

Kliknij **Create pull request**.

**Sprawdź:** Otworzy się strona PR. Na górze widzisz:
* Status: zielona kropka i **"Able to merge. These branches can be automatically merged."**
* Tabki: **Conversation**, **Commits** (1 commit), **Files changed** (1 plik).

**Krok 4.** "Code Review" -- przejrzyj swój własny PR:

* Kliknij **Files changed**.
* Przejrzyj diff. Spróbuj **najechać myszką na linię** -- pojawi się mały niebieski plus -- kliknij. Otworzy się okienko komentarza.
* Napisz komentarz w stylu: "Mogłem dodać też kropkę na końcu zdania -- poprawię w kolejnym commicie."
* Kliknij **Start a review**, potem na górze **Finish your review** → wybierz **Comment** → **Submit review**.

**Sprawdź:** W tabce **Conversation** widzisz swój komentarz.

**Krok 5.** Merge PR:

Wróć do tabki **Conversation** → na dole kliknij **Merge pull request** → **Confirm merge**.

**Sprawdź:**
* Status PR zmienia się na fioletowy **Merged**.
* Pojawia się przycisk **Delete branch** -- kliknij go. Gałąź na GitHubie zostanie skasowana (lokalnie u Ciebie nadal jest -- usuniemy ją za chwilę).

**Krok 6.** Zsynchronizuj lokalne repo:

```bash
git switch main
git pull
```

**Sprawdź:**

```
remote: ...
Fast-forward
 app.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```
"Fast-forward" znaczy: GitHub miał commity, których Ty lokalnie nie miałeś -- Git je pobrał i Twoja gałąź `main` "doszła" do tego stanu.

```bash
cat app.txt
```
Powinno teraz zawierać `Wersja: 1.1` i linię `- edycja zadań` -- bo merge wlał feature do main.

**Krok 7.** Usuń lokalnie niepotrzebną gałąź:

```bash
git branch -d feature/dodaj-edycje
```

**Sprawdź:** Powinno wypisać `Deleted branch feature/dodaj-edycje (was a3f7b21).`

```bash
git branch
```
Powinieneś zobaczyć tylko:
```
* main
  feature/dodaj-kategorie
```
Gałąź `feature/dodaj-edycje` jest usunięta, bo skończyła pracę. Gałąź `feature/dodaj-kategorie` zostaje -- jeszcze nie była mergowana.

### Praktyka -- Wariant B (IntelliJ IDEA)

> **Reset przed wariantem B:** Kontynuujemy na tym samym repo `git-zad3-branch`. Mamy jeszcze gałąź `feature/dodaj-kategorie` niezmergowaną -- wymergujemy ją przez IntelliJ + GitHub.

1. Otwórz `git-zad3-branch` w IntelliJ.
2. Prawy dolny róg → branch `main` → **Checkout** (na wszelki wypadek).
3. *Git → GitHub → Create Pull Request* (Pierwszy raz może wymagać zalogowania do GitHub w IntelliJ -- *Settings → Version Control → GitHub* → **+** → *Log In via GitHub…*).

   **Sprawdź:** Po prawej otwiera się panel **Pull Request** z formularzem.

4. **Head:** `feature/dodaj-kategorie`, **Base:** `main`. Title: `Dodaj kategorie zadań`. Description: napisz 2-3 zdania.
5. Kliknij **Create Pull Request**.

   **Sprawdź:** Panel pokazuje listę otwartych PR-ów -- Twój jest na górze. Status: **Open**.

6. Kliknij PR → w prawym górnym rogu zakładki PR jest dropdown **Merge** → wybierz **Merge** → potwierdź.

   (Można też zmergować przez przeglądarkę -- otwórz PR na GitHubie i klikaj jak w wariancie A krok 5.)

7. Po merge -- *Git → Pull* (`Ctrl+T` / `⌘T`) → wybierz **Merge incoming changes into the current branch** → **Pull**.

   **Sprawdź:** Plik `app.txt` w IntelliJ teraz pokazuje wersję 1.1 z **edycją zadań** I **kategoriami zadań** (oba feature'y zmergowane).

8. Usuń lokalną gałąź: prawy dolny róg → `feature/dodaj-kategorie` → **Delete**.

### Częste błędy w zadaniu 4

* **Po pushu nie widzę "Compare & pull request"** -- za późno odświeżyłeś, albo gałąź już istniała wcześniej. Idź ręcznie: zakładka **Pull requests → New pull request**.
* **"There isn't anything to compare"** -- pomyliłeś base/compare miejscami. Base = `main` (cel), compare = Twój `feature` (źródło).
* **`git branch -d` mówi "branch not fully merged"** -- gałąź ma commity, które nie zostały zmergowane. Małymi literami `-d` to bezpieczna wersja. Duże `-D` to siłowa (kasuje mimo wszystko). Sprawdź dwa razy, że PR był zmergowany, zanim użyjesz `-D`.
* **`git pull` mówi "Already up to date"** -- nic do pobrania (bo zmergowałeś chwilę temu i już byłeś świeży) albo pomyliłeś gałąź. Sprawdź `git status` -- musisz być na `main`.

### Co ma być na GitHubie po zadaniu

* [ ] Repo `git-zad3-branch` ma **2 zamknięte PR-y** (oba z etykietą `Merged`).
* [ ] Na `main`: `app.txt` w wersji 1.1 z liniami `- edycja zadań` i `- kategorie zadań`.
* [ ] Gałęzie `feature/dodaj-edycje` i `feature/dodaj-kategorie` skasowane na GitHubie.
* [ ] Lokalnie: `git branch` pokazuje tylko `main`.

### Pytania do RAPORT.md

1. Co to jest Pull Request? Wymień 3 powody, dla których w pracy używamy PR zamiast bezpośredniego merge.
2. Czym różni się **base** od **compare** przy tworzeniu PR? Co zwykle ustawiamy w każdym z tych pól?
3. Co znaczy komunikat "Fast-forward" przy `git pull`? Kiedy on się pojawia?
4. Po co usuwamy gałąź feature po merge (lokalnie i na GitHubie)? Co by się stało, gdybyśmy ich nie kasowali?
5. Załącz screenshot zmergowanego PR (z fioletową etykietą **Merged**).

---

## Zadanie 5 -- Aktualizacja lokalnego repo (fetch, pull)

**Co ćwiczymy:** Różnicę między `git fetch` a `git pull`, sytuację "ktoś inny coś zmienił na GitHubie".

### Teoria w prostych słowach

W pracy zespołowej **wszyscy** pchają commity do tego samego repo na GitHubie. Twoja lokalna kopia szybko zaczyna być **nieaktualna** -- ktoś inny zmergował PR, dodał nowy plik, edytował README.

**Dwie komendy do aktualizacji:**

* **`git fetch`** -- "ściągnij informację o nowych commitach z GitHuba, ale **nie zmieniaj** moich plików". To bezpieczna operacja. Tylko aktualizuje Twoją wiedzę o stanie remote'a (referencje `origin/main`, `origin/feature/xxx`).
* **`git pull`** -- "ściągnij i **wmerguj** od razu w moją aktualną gałąź". To `git fetch` + `git merge origin/<aktualna-gałąź>` w jednej komendzie. Może zmienić Twoje pliki, może wywołać konflikt.

**Kiedy fetch, kiedy pull?**

* **`git fetch`** -- kiedy chcesz tylko zobaczyć "co się dzieje na remote'cie" przed podjęciem decyzji.
* **`git pull`** -- kiedy jesteś na czystej gałęzi (`git status` = clean) i chcesz po prostu być na bieżąco. To 90% przypadków.

**Analogia:** `fetch` = sprawdzenie skrzynki pocztowej (są listy, ale jeszcze ich nie otworzyłeś). `pull` = sprawdzenie skrzynki + otwarcie wszystkich listów + wpięcie ich od razu do segregatora.

### Przygotowanie

#### Lokalnie

```bash
cd ~
mkdir git-zad5-fetch-pull
cd git-zad5-fetch-pull
git init
git branch -M main
```

#### Na GitHubie

1. [https://github.com/new](https://github.com/new) → `git-zad5-fetch-pull`, Public, BEZ README.
2. *Create*.
3. Lokalnie:

```bash
git remote add origin https://github.com/<TWOJ-USER>/git-zad5-fetch-pull.git
echo "# git-zad5-fetch-pull" > README.md
echo "Linia 1" >> README.md
git add README.md
git commit -m "init: README z linią 1"
git push -u origin main
```

**Sprawdź:** GitHub pokazuje 1 commit, plik README z dwoma liniami.

### Praktyka -- Wariant A (CLI / terminal)

**Krok 1.** Symulujemy, że **ktoś inny** coś zmienił bezpośrednio na GitHubie. Otwórz repo w przeglądarce → kliknij na `README.md` → kliknij ikonkę ołówka (Edit) → dodaj nową linię:
```
Linia 2 (dodana przez kolegę przez GitHub UI)
```

Na dole strony: **Commit changes** → wpisz wiadomość `docs: kolega dodaje linię 2` → **Commit changes**.

**Sprawdź:** Strona repo pokazuje 2 commity. README ma teraz 3 linie.

**Krok 2.** Teraz Ty (lokalnie) niczego nie wiesz. Sprawdź:

```bash
git log --oneline
```

Widzisz tylko **1 commit** -- ten, który zacommitowałeś. O commitcie "kolegi" nie wiesz.

```bash
cat README.md
```

Plik lokalnie ma **2 linie**, nie 3.

**Krok 3.** Sprawdź, co jest na remote'cie -- BEZ zmiany Twoich plików:

```bash
git fetch
```

**Sprawdź:** Output:
```
From https://github.com/<TWOJ-USER>/git-zad5-fetch-pull
   a3f7b21..b8c4d12  main       -> origin/main
```
Coś przyszło z GitHuba. Ale plik README lokalnie jest **nadal niezmieniony**:

```bash
cat README.md
```
Dalej **2 linie**. `fetch` niczego nie wmergował.

```bash
git status
```

Powinno teraz pokazać:
```
On branch main
Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)
```

To Git mówi: "Wiesz co? Na origin/main jest 1 commit więcej, możesz się zaktualizować przez `git pull`."

**Krok 4.** Wykonaj `git pull`:

```bash
git pull
```

**Sprawdź:** Output:
```
Updating a3f7b21..b8c4d12
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
```

Teraz lokalnie:

```bash
cat README.md
```
Powinieneś zobaczyć **3 linie** -- włącznie z linią dodaną na GitHubie.

```bash
git log --oneline
```

Powinieneś zobaczyć **2 commity**: `init: README z linią 1` i `docs: kolega dodaje linię 2`.

**Krok 5.** Eksperyment: pomyłki na nieczystej gałęzi.

Zacznij **nową** zmianę lokalnie, ale jej nie commituj:

```bash
echo "Linia 3 (moja lokalna, niezacommitowana)" >> README.md
```

Symuluj kolejną zmianę "kolegi" na GitHubie: edytuj README przez UI → dodaj `Linia 4 (kolega znów)` → commit changes.

Teraz lokalnie spróbuj pull:

```bash
git pull
```

Możliwe dwa wyniki:
* **Jeśli "kolega" edytował inną linię niż Ty** → `git pull` zadziała, automatycznie wmerguje, Twoja niezacommitowana linia 3 zostanie w pliku.
* **Jeśli "kolega" edytował tę samą linię co Ty** → Git odmówi:
  ```
  error: Your local changes to the following files would be overwritten by merge:
      README.md
  Please commit your changes or stash them before you merge.
  ```

**Wniosek:** zanim robisz `git pull`, najlepiej **zacommituj** swoje zmiany. Inaczej możesz się natknąć na blokadę. (W kursie zaawansowanym uczymy `git stash` do tymczasowego chowania.)

### Praktyka -- Wariant B (IntelliJ IDEA)

> **Reset:** Kontynuujemy na tym samym repo.

1. Otwórz `git-zad5-fetch-pull` w IntelliJ.
2. Najpierw zacommituj jakąkolwiek niezacommitowaną zmianę (jeśli została z kroku 5) -- `Ctrl+K` → commit i push.
3. Otwórz README na GitHubie → edytuj → dodaj linię `Linia 5 (kolega przez UI - test IntelliJ)` → Commit.
4. W IntelliJ: *Git → Fetch* (w menu Git, na górze).

   **Sprawdź:** W dolnym pasku statusu pojawia się info "Fetched". Plik README w edytorze **niezmieniony**.

5. *Git → Show Git Log* (lub `Alt+9` → zakładka Log). W górnej części paska gałęzi powinieneś zobaczyć powiadomienie typu "1 incoming commit" (małe strzałki w dół przy nazwie gałęzi).

6. *Git → Pull…* (`Ctrl+T` / `⌘T`) → **Pull**.

   **Sprawdź:** README w edytorze automatycznie odświeża się z nową linią. Log pokazuje nowy commit.

### Częste błędy w zadaniu 5

* **`git pull` zwraca "Already up to date"** -- nic do pobrania. Albo nikt nic nie commitował na GitHubie, albo jesteś na złej gałęzi.
* **"Your local changes ... would be overwritten by merge"** -- masz niezacommitowane zmiany kolidujące ze zmianami zdalnymi. Zacommituj je albo `git stash`.
* **`git pull` wciąga merge commit, którego nie chciałeś** -- w domyślnej konfiguracji `git pull` może utworzyć merge commit, jeśli historia się rozjechała. Można skonfigurować "rebase by default": `git config --global pull.rebase true` (ale to temat na kurs zaawansowany).

### Co ma być po zadaniu

* [ ] Repo `git-zad5-fetch-pull` publiczne.
* [ ] README na GitHubie ma **co najmniej 4 linie** (po wszystkich edycjach z wariantów A i B).
* [ ] Lokalnie i na GitHubie zawartość READMEzgodna.

### Pytania do RAPORT.md

1. Jaka jest różnica między `git fetch` a `git pull`? Wytłumacz własnymi słowami.
2. W którym momencie `git status` powiedziało Ci, że jesteś "behind 'origin/main'"? Co to dokładnie oznacza?
3. Co Git zrobił, kiedy próbowałeś pull-a z niezacommitowaną zmianą w tym samym pliku, który zmienił "kolega"? Dlaczego?
4. Wymień sytuację, w której wolisz `git fetch` od `git pull` (a kiedy odwrotnie).
5. Załącz screenshot `git status` w momencie "Your branch is behind 'origin/main'".

---

## Zadanie 6 -- Pierwszy prosty konflikt (i jak go rozwiązać)

**Co ćwiczymy:** Świadome wywołanie konfliktu merge'owego, ręczne rozwiązanie w edytorze, te same kroki w IntelliJ 3-panel.

### Teoria w prostych słowach

**Konflikt** powstaje, kiedy dwie gałęzie zmieniły **te same linie tego samego pliku** w różny sposób. Git nie może zgadnąć, którą wersję wybrać -- zatrzymuje merge i prosi Cię o decyzję.

Jak Git oznacza konflikt w pliku? Wstawia w treść markery:

```
<<<<<<< HEAD
Wersja z gałęzi, na której jesteś (np. main)
=======
Wersja z gałęzi, którą mergujesz (np. feature/xyz)
>>>>>>> feature/xyz
```

Twoim zadaniem jest:
1. Otworzyć plik.
2. Wybrać, którą wersję chcesz zachować (albo połączyć obie ręcznie).
3. **Usunąć markery** (`<<<<<<<`, `=======`, `>>>>>>>`).
4. Zapisać plik.
5. `git add <plik>` -- mówisz Gitowi "rozwiązałem".
6. `git commit` -- Git utworzy specjalny **merge commit** kończący operację.

**Najczęstszy błąd początkujących:** zapomnienie usunąć któryś z markerów. Plik kompiluje się jak przed, ale w środku zostają śmieci typu `>>>>>>> feature/xyz` -- katastrofa w code review.

### Przygotowanie

#### Lokalnie

```bash
cd ~
mkdir git-zad6-konflikt
cd git-zad6-konflikt
git init
git branch -M main
```

#### Na GitHubie

1. [https://github.com/new](https://github.com/new) → `git-zad6-konflikt`, Public, BEZ README.
2. Lokalnie:

```bash
git remote add origin https://github.com/<TWOJ-USER>/git-zad6-konflikt.git
```

### Skrypt setupowy (skopiuj w całości do terminala)

```bash
cat > Powitanie.txt << 'EOF'
Witaj w naszej aplikacji!

Wersja: 1.0
Język: polski

Dziękujemy za korzystanie z naszych usług.
EOF

git add Powitanie.txt
git commit -m "init: powitanie wersja 1.0"
git push -u origin main

# Gałąź feature/po-angielsku -- zmienia linię "Język" na angielski
git switch -c feature/po-angielsku
sed -i.bak 's|Język: polski|Język: angielski|' Powitanie.txt && rm Powitanie.txt.bak
git add Powitanie.txt
git commit -m "feat: język angielski"
git push -u origin feature/po-angielsku

# Wracamy na main i zmieniamy TĘ SAMĄ linię na niemiecki
git switch main
sed -i.bak 's|Język: polski|Język: niemiecki|' Powitanie.txt && rm Powitanie.txt.bak
git add Powitanie.txt
git commit -m "feat: język niemiecki"
git push

git log --oneline --all --graph
```

**Sprawdź:** Output `git log` pokazuje 3 commity w drzewku -- widać, że gałęzie się rozjechały po commitcie initial. Coś w stylu:
```
* feat: język niemiecki (main)
| * feat: język angielski (feature/po-angielsku)
|/
* init: powitanie wersja 1.0
```

### Praktyka -- Wariant A (CLI / terminal)

**Krok 1.** Spróbuj zmergować `feature/po-angielsku` w `main`:

```bash
git switch main
git merge feature/po-angielsku
```

**Sprawdź:** Git wypisze:
```
Auto-merging Powitanie.txt
CONFLICT (content): Merge conflict in Powitanie.txt
Automatic merge failed; fix conflicts and then commit the result.
```

`git status` powinno teraz pokazać:
```
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   Powitanie.txt
```

**Krok 2.** Otwórz plik:

```bash
cat Powitanie.txt
```

Zobaczysz coś takiego:
```
Witaj w naszej aplikacji!

Wersja: 1.0
<<<<<<< HEAD
Język: niemiecki
=======
Język: angielski
>>>>>>> feature/po-angielsku

Dziękujemy za korzystanie z naszych usług.
```

Czytanie markerów:
* Wszystko między `<<<<<<< HEAD` a `=======` to wersja z **bieżącej gałęzi** (`main` -- niemiecki).
* Wszystko między `=======` a `>>>>>>> feature/po-angielsku` to wersja z **mergowanej gałęzi** (angielski).

**Krok 3.** Otwórz plik w edytorze i ręcznie usuń markery. Decydujemy, że chcemy zachować **OBIE** wersje:

Użyj `nano Powitanie.txt` (lub `code Powitanie.txt` jeśli masz VS Code, albo otwórz w IntelliJ -- ale nie używaj jeszcze narzędzia merge, tylko zwykłej edycji).

Zmień zawartość na:
```
Witaj w naszej aplikacji!

Wersja: 1.0
Język: niemiecki / angielski

Dziękujemy za korzystanie z naszych usług.
```

Zapisz i zamknij edytor.

**Sprawdź:**

```bash
cat Powitanie.txt
```
Nie powinno być **żadnego** z markerów `<<<<<<<`, `=======`, `>>>>>>>`. Linia `Język:` powinna mieć obie wartości.

**Krok 4.** Powiedz Gitowi "rozwiązałem":

```bash
git add Powitanie.txt
git status
```

**Sprawdź:** Powinno teraz pokazać:
```
On branch main
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)
Changes to be committed:
        modified:   Powitanie.txt
```

**Krok 5.** Dokończ merge commitem:

```bash
git commit
```

Git otworzy edytor z gotową wiadomością `Merge branch 'feature/po-angielsku'`. **Zostaw ją** -- po prostu zapisz i zamknij (`Ctrl+X`, `Y`, `Enter` w nano).

Jeśli wolisz jedną komendą:
```bash
git commit -m "merge: feature/po-angielsku into main (resolve language conflict)"
```

**Sprawdź:**

```bash
git log --oneline --graph --all
```

Powinieneś teraz zobaczyć **merge commit** łączący dwie gałęzie:
```
*   merge: feature/po-angielsku into main
|\
| * feat: język angielski
* | feat: język niemiecki
|/
* init: powitanie wersja 1.0
```

**Krok 6.** Wypchnij na GitHub:

```bash
git push
```

Otwórz repo na GitHubie → zakładka **Insights → Network** (lub po prostu **Commits**). Powinieneś zobaczyć drzewko z merge commitem.

### Praktyka -- Wariant B (IntelliJ IDEA -- narzędzie 3-panel)

> **Reset przed wariantem B:** Cofnij merge i wróć do stanu sprzed konfliktu:
>
> ```bash
> cd ~/git-zad6-konflikt
> git switch main
>
> # Znajdź hash commitu sprzed merge (czyli "feat: język niemiecki"):
> git log --oneline
> # Skopiuj hash commitu "feat: język niemiecki"
>
> git reset --hard <hash-niemiecki>
> git push --force-with-lease
> ```
>
> Następnie otwórz katalog w IntelliJ.

1. Otwórz `git-zad6-konflikt` w IntelliJ. Prawy dolny róg → checkout `main` (jeśli nie jesteś).
2. *Git → Merge…* → wybierz `feature/po-angielsku` → **Merge**.

   **Sprawdź:** IntelliJ wyświetli okienko **Merge Conflicts** z listą plików w konflikcie (jeden -- `Powitanie.txt`).

3. Kliknij **Merge** przy `Powitanie.txt`. Otwiera się **narzędzie 3-panelowe**:
    * **Lewy panel** -- *Your version* (Twoja gałąź, `main`, niemiecki).
    * **Prawy panel** -- *Their version* (mergowana gałąź, `feature/po-angielsku`, angielski).
    * **Środkowy panel** -- *Result* (wynik, do którego wybierasz fragmenty).

4. Sposób użycia narzędzia 3-panel:
    * Konfliktowy region jest podświetlony na czerwono/żółto w środkowym panelu.
    * Strzałki `>>` (lewa strona) i `<<` (prawa strona) wpychają wybraną wersję do środka.
    * `X` (po obu stronach) odrzuca wersję.
    * Możesz też **edytować ręcznie** środkowy panel.

5. Cel: chcemy "niemiecki / angielski". Edytuj środkowy panel ręcznie → wpisz: `Język: niemiecki / angielski`. Wszystkie inne linie zostaw bez zmian.

6. Kliknij **Apply**.

   **Sprawdź:** Okno znika. IntelliJ pokaże okienko commit -- wpisz wiadomość lub zostaw domyślną → **Commit**.

7. Push: `Ctrl+Shift+K` → **Push**.

   **Sprawdź:** *Git tool window → Log* pokazuje merge commit z dwoma rodzicami (widać "rozwidlenie" w drzewku).

### Częste błędy w zadaniu 6

* **Zapomniany marker** -- najczęściej `>>>>>>> feature/...` na końcu zostaje. Po edycji **zawsze** wpisz `grep -n '<<<<<<<\|=======\|>>>>>>>' Powitanie.txt` -- jeśli wypisze cokolwiek, **nie skończyłeś**.
* **`git merge --abort`** -- jeśli się pogubiłeś podczas rozwiązywania konfliktu, ta komenda cofnie cały merge i wróci do stanu sprzed `git merge`. Bezpieczna ucieczka.
* **"Nothing to commit" po `git add`** -- prawdopodobnie plik wygląda **identycznie** jak przed merge (nic nie zmieniłeś). Edytuj ponownie -- musi pojawić się różnica.
* **W IntelliJ wybrałem złą stronę w 3-panel** -- nic się nie stało: kliknij **Reset** w 3-panelu, zacznij od nowa.

### Co ma być na GitHubie po zadaniu

* [ ] Repo `git-zad6-konflikt` publiczne.
* [ ] Na `main`: plik `Powitanie.txt` z linią `Język: niemiecki / angielski` (lub Twój własny wariant).
* [ ] `git log --graph --oneline --all` (lub Network na GitHubie) pokazuje merge commit łączący dwie gałęzie.

### Pytania do RAPORT.md

1. Kiedy powstaje konflikt? Podaj **najprostszą** sytuację, która go wywoła.
2. Co oznaczają markery `<<<<<<< HEAD`, `=======`, `>>>>>>> feature/xyz`? Co jest między nimi?
3. Jaką decyzję podjąłeś przy rozwiązywaniu konfliktu -- niemiecki, angielski, czy oba? Dlaczego?
4. Wymień 2 powody, dla których narzędzie 3-panel w IntelliJ jest wygodniejsze niż ręczna edycja markerów.
5. Co robi `git merge --abort`? W jakiej sytuacji byś tego użył?
6. Załącz screenshot narzędzia 3-panel IntelliJ podczas rozwiązywania konfliktu **oraz** screenshot `git log --graph --oneline --all` z drzewkiem.

---

## Zadanie 7 -- Plik `.gitignore` (czego nie commitować)

**Co ćwiczymy:** Tworzenie pliku `.gitignore`, wzorce ignorowania, sytuacja "ups, już zacommitowałem śmieć -- jak go usunąć".

### Teoria w prostych słowach

Nie wszystkie pliki w Twoim folderze chcesz mieć w repozytorium. Przykłady **plików-śmieci**, których **nigdy** nie commitujemy:

* **Pliki IDE** -- `.idea/` (IntelliJ), `.vscode/` (VS Code). Konfiguracja IDE jest osobista, każdy ma swoją.
* **Pliki budowania** -- `target/` (Maven), `build/`, `node_modules/`, `*.class`, `*.o`. To kod wygenerowany z Twoich źródeł -- można go odtworzyć w każdej chwili, nie ma sensu wrzucać.
* **Logi i raporty** -- `*.log`, `npm-debug.log`. Lokalne, tymczasowe.
* **Pliki systemowe** -- `.DS_Store` (macOS), `Thumbs.db` (Windows).
* **SEKRETY** -- `.env`, `secrets.yml`, klucze API, hasła do bazy. **Nigdy.** Nawet do prywatnego repo. (Wystarczy, że raz dasz repo komuś, by się okazało, że klucz przeciekł.)

**`.gitignore`** to plik tekstowy w głównym katalogu repo, w którym piszesz wzorce (po jednej na linię) tego, co Git ma ignorować. Przykład:

```
# Pliki IDE
.idea/
.vscode/

# Build
target/
build/
*.class

# Logi
*.log

# Sekrety
.env
*.key

# System
.DS_Store
```

**Bardzo ważne:** `.gitignore` działa **tylko na pliki untracked**. Jeśli już raz zacommitowałeś `.env`, dodanie go do `.gitignore` nie sprawi, że zniknie z repo. Trzeba dodatkowo zrobić `git rm --cached .env` (usuwa z trackingu, zostawia na dysku).

### Przygotowanie

#### Lokalnie

```bash
cd ~
mkdir git-zad7-gitignore
cd git-zad7-gitignore
git init
git branch -M main
```

#### Na GitHubie

1. [https://github.com/new](https://github.com/new) → `git-zad7-gitignore`, Public, BEZ README.
2. Lokalnie:

```bash
git remote add origin https://github.com/<TWOJ-USER>/git-zad7-gitignore.git
```

### Praktyka -- Wariant A (CLI / terminal)

**Krok 1.** Utwórz strukturę projektu udającego aplikację:

```bash
mkdir -p src target logs
echo "public class Main {}" > src/Main.java
echo "binarne smieci" > target/Main.class
echo "INFO: aplikacja wystartowala" > logs/app.log
echo "API_KEY=tajne123" > .env
echo "# Mój projekt" > README.md
```

**Sprawdź:**

```bash
ls -la
git status
```

`git status` powinno pokazać **wszystkie** te pliki jako untracked:
```
Untracked files:
  .env
  README.md
  logs/
  src/
  target/
```

**Krok 2.** Utwórz `.gitignore` zanim cokolwiek zacommitujesz:

```bash
cat > .gitignore << 'EOF'
# Pliki IDE
.idea/
.vscode/

# Build
target/
*.class

# Logi
logs/
*.log

# Sekrety
.env
*.key

# System
.DS_Store
Thumbs.db
EOF
```

**Sprawdź:**

```bash
git status
```

Powinno teraz pokazać **TYLKO**:
```
Untracked files:
  .gitignore
  README.md
  src/
```

Brak: `.env`, `logs/`, `target/` -- bo zostały zignorowane! Sprawdź, że pliki nadal istnieją na dysku:

```bash
ls -la
```
Pliki są -- tylko Git ich "nie widzi".

**Krok 3.** Zacommituj zdrowy stan:

```bash
git add .
git status
```

`git status` pokazuje teraz `.gitignore`, `README.md`, `src/Main.java` w stagingu. **Sprawdź:** Żadnego śmiecia.

```bash
git commit -m "init: projekt z .gitignore"
git push -u origin main
```

**Sprawdź:** Na GitHubie -- 3 pliki: `.gitignore`, `README.md`, folder `src/`. **Brak** `.env`, `logs/`, `target/`. Bezpiecznie.

**Krok 4 (eksperyment).** Co jeśli już zacommitowałeś sekret?

Załóżmy, że zapomniałeś o `.gitignore` i zacommitowałeś `.env`. Symulacja:

```bash
# Symulacja - tymczasowo wyłącz ignorowanie tego pliku
git add -f .env                  # -f = force, zignoruj .gitignore
git commit -m "ups: przypadkiem dodałem .env"
git push
```

Wejdź na GitHub -- niestety, plik `.env` z `API_KEY=tajne123` jest tam widoczny. **Wyciek.**

Jak posprzątać:

```bash
git rm --cached .env             # usuń z trackingu (ale zostaw na dysku)
git commit -m "fix: usuń .env z repo (był w sekretach)"
git push
```

**Sprawdź:** Plik nadal istnieje lokalnie (`cat .env` zwraca `API_KEY=tajne123`), ale na GitHubie **w aktualnym stanie** już go nie ma.

**UWAGA EDUKACYJNA:** `git rm --cached` usuwa plik z **bieżącej wersji**, ale **on nadal jest w historii** repo. Każdy, kto sklonuje repo i wpisze `git log --all -- .env`, znajdzie ten klucz. **Dlatego jeśli kiedykolwiek zacommitujesz prawdziwy sekret -- natychmiast zmień ten sekret** (regeneracja API key, zmiana hasła). Nie ma drogi powrotu. Czyszczenie historii (`git filter-branch`, `BFG Repo-Cleaner`) jest skomplikowane i nie zawsze działa, jeśli ktoś już sklonował.

### Praktyka -- Wariant B (IntelliJ IDEA)

> **Reset:** Otwórz `git-zad7-gitignore` w IntelliJ -- kontynuujemy.

1. *File → Open* → wskaż katalog `git-zad7-gitignore`.
2. Spójrz w lewy panel (Project) -- IntelliJ powinien pokazać `.gitignore` z różowym/szarym kolorem zaznaczającym, że są w nim wpisy ignorujące.
3. Otwórz `.gitignore` w edytorze -- IntelliJ koloruje wzorce (linie ignorujące są wyróżnione).
4. Dodaj nowy wzorzec na końcu: `*.tmp`. Zapisz.
5. Utwórz w IntelliJ nowy plik: *File → New → File* → `notatka.tmp` → wpisz cokolwiek.

   **Sprawdź:** Plik `notatka.tmp` w lewym panelu jest **szary** (ignorowany) -- IntelliJ szanuje `.gitignore`. Brak też pytania "Add to Git?".

6. Commituj `.gitignore`: `Ctrl+K` → wiadomość: `chore: ignoruj *.tmp` → **Commit and Push**.

   **Sprawdź:** Lista plików w oknie commit zawiera tylko `.gitignore`. Plik `notatka.tmp` **nie pojawia się** -- dokładnie tego chcemy.

### Częste błędy w zadaniu 7

* **`.gitignore` nie działa, plik dalej się pojawia w `git status`** -- najczęściej plik został wcześniej zacommitowany (`.gitignore` ignoruje tylko untracked). Rozwiązanie: `git rm --cached <plik>` + commit.
* **Zacommitowałeś sekret -- co teraz?** Zmień sekret **natychmiast** (nowy API key, hasło). Plik usuń przez `git rm --cached` + commit. Pamiętaj, że stary sekret jest w historii i ktoś może go znaleźć.
* **Zignorowałeś za dużo** -- np. dodałeś `*.json` i zignorowałeś sobie `package.json`. Dodaj wyjątek: `!package.json` w `.gitignore` w nowej linii. `!` na początku = "ignoruj, oprócz".
* **Brak `.gitignore` w katalogach IDE templates** -- najprościej skopiować gotowy z [https://github.com/github/gitignore](https://github.com/github/gitignore) (są szablony dla każdego języka).

### Co ma być na GitHubie po zadaniu

* [ ] Repo `git-zad7-gitignore` publiczne.
* [ ] Pliki na GitHubie: `.gitignore`, `README.md`, `src/Main.java`.
* [ ] **BRAK** na GitHubie: `target/`, `logs/`, `.env` (w aktualnym stanie -- mogły być w historii podczas eksperymentu z kroku 4, ale w aktualnej wersji już ich nie ma).
* [ ] `.gitignore` zawiera wpisy: `.idea/`, `target/`, `*.class`, `logs/`, `*.log`, `.env`, `*.key`, `.DS_Store`, `Thumbs.db`.

### Pytania do RAPORT.md

1. Po co istnieje plik `.gitignore`? Co stanie się z plikiem `secrets.yml`, jeśli dodasz `secrets.yml` do `.gitignore` przed jego pierwszym commitem?
2. Wymień **3 typy plików**, których nigdy nie commitujemy do repo. Dlaczego?
3. Co stanie się, jeśli dodasz wpis do `.gitignore`, ale plik **już jest** w repo? Jak to naprawić?
4. Dlaczego "wycofanie" sekretu z repo (np. `git rm --cached .env` + commit) **nie wystarcza**? Co trzeba zrobić dodatkowo?
5. Załącz screenshot Twojego `.gitignore` w edytorze oraz screenshot `git status` po jego utworzeniu (powinno być widać, że pliki śmieci są ignorowane).

---

## Ściąga komend (do druku)

```bash
# === KONFIGURACJA (jednorazowo) ===
git config --global user.name "Imię Nazwisko"
git config --global user.email "twoj@email.com"
git config --global init.defaultBranch main

# === STAN PROJEKTU ===
git status                          # co jest zmienione, w stagingu, untracked -- TWÓJ NAJLEPSZY PRZYJACIEL
git log                             # pełna historia
git log --oneline                   # zwięzła historia (1 linia / commit)
git log --oneline --graph --all     # historia z drzewkiem wszystkich gałęzi
git diff                            # co się zmieniło od ostatniego commita

# === REPO ===
git init                            # utwórz nowe repo lokalnie
git clone <url>                     # ściągnij istniejące repo

# === COMMIT (cykl) ===
git add <plik>                      # dodaj plik do "koszyka" (staging)
git add .                           # dodaj WSZYSTKIE zmiany (uważaj na śmieci)
git commit -m "feat: opis zmiany"   # zacommituj staging
git commit                          # otwórz edytor i napisz dłuższą wiadomość

# === GAŁĘZIE (BRANCHE) ===
git branch                          # lista lokalnych gałęzi
git branch -a                       # lista WSZYSTKICH (lokalne + zdalne)
git switch <branch>                 # przełącz się na istniejącą gałąź
git switch -c feature/xyz           # utwórz NOWĄ gałąź i przełącz się na nią
git branch -d feature/xyz           # usuń gałąź (bezpiecznie, tylko zmergowane)
git branch -D feature/xyz           # usuń gałąź siłowo

# === REMOTE ===
git remote -v                       # lista remote'ów z URL-ami
git remote add origin <url>         # dodaj zdalne repo pod nazwą "origin"
git remote remove origin            # usuń zdalne repo
git remote set-url origin <new-url> # zmień URL istniejącego remote

# === SYNCHRONIZACJA ===
git push                            # wyślij commity na GitHub
git push -u origin <branch>         # PIERWSZY push danej gałęzi (zapamiętuje powiązanie)
git fetch                           # pobierz INFO o zmianach (bezpiecznie, nie wmerguje)
git pull                            # pobierz + wmerguj w bieżącą gałąź

# === MERGE ===
git merge <branch>                  # wmerguj <branch> w aktualną gałąź
git merge --abort                   # anuluj merge w trakcie (gdy konflikt cię przerasta)

# === ROZWIĄZYWANIE KONFLIKTÓW ===
# 1. Otwórz plik, usuń markery <<<<<<< / ======= / >>>>>>>, zostaw wybraną wersję
# 2. Zapisz
git add <plik>                      # mów Gitowi "rozwiązałem"
git commit                          # zakończ merge

# === IGNOROWANIE PLIKÓW ===
# Utwórz plik .gitignore z wzorcami, np.:
#   .idea/
#   target/
#   *.log
#   .env
git rm --cached <plik>              # przestań śledzić plik (zostaw na dysku)
```

### Skróty IntelliJ IDEA (najczęstsze)

| Akcja | Windows/Linux | macOS |
|-------|---------------|-------|
| Git tool window | `Alt+9` | `⌘9` |
| Commit | `Ctrl+K` | `⌘K` |
| Push | `Ctrl+Shift+K` | `⌘⇧K` |
| Update (pull/fetch) | `Ctrl+T` | `⌘T` |
| Terminal IntelliJ | `Alt+F12` | `⌥F12` |
| Branches popup | dolny prawy róg paska statusu | dolny prawy róg |

### Mapowanie CLI ↔ IntelliJ (najważniejsze)

| Komenda CLI | Akcja IntelliJ |
|-------------|----------------|
| `git init` | *VCS → Enable Version Control Integration… → Git* |
| `git status` | *Git tool window* → zakładka *Changes* |
| `git add` + `git commit` | `Ctrl+K` → wpisz wiadomość → *Commit* |
| `git push` | `Ctrl+Shift+K` → *Push* |
| `git pull` | `Ctrl+T` → *Pull* (lub *VCS → Update Project…*) |
| `git switch -c <b>` | *Branches* (prawy dolny) → *New Branch* |
| `git switch <b>` | *Branches* → klik na gałąź → *Checkout* |
| `git merge <b>` | *Git → Merge…* → wybierz gałąź |
| Rozwiązanie konfliktu | okno *Merge Conflicts* → *Merge* przy pliku → 3-panel |
| `git remote add origin <url>` | *Git → Manage Remotes…* → **+** |

---

## Sposób oddania pracy

1. **Utwórz `RAPORT.md`** w katalogu `git-podstawy-pd` (z zadania 0.7).
2. W `RAPORT.md` umieść:
    * Sekcję `# Zadanie 1` -- z odpowiedziami na pytania kontrolne + linki do swoich repo (`https://github.com/<TWOJ-USER>/git-zad1-pierwszy-commit`).
    * Tak samo dla zadań 2-7.
    * Screenshoty wklej do podkatalogu `screenshots/` i linkuj z markdownem: `![opis](./screenshots/zad1-log.png)`.
3. Zacommituj i wypchnij `RAPORT.md`:

   ```bash
   cd ~/git-podstawy-pd
   git add RAPORT.md screenshots/
   git commit -m "docs: raport z karty pracy 'Git podstawy'"
   git push
   ```

4. **Wyślij prowadzącemu link** do repo `git-podstawy-pd` (np. mailem albo na Discordzie kursu).

### Kryteria akceptacji

* [ ] Repo `git-podstawy-pd` zawiera `RAPORT.md` z odpowiedziami na pytania **z wszystkich 7 zadań**.
* [ ] Każde z 7 osobnych repo zadaniowych istnieje, jest publiczne, ma stan z sekcji **"Co ma być na GitHubie"** danego zadania.
* [ ] W repo zadaniowych commity są podpisane Twoim e-mailem (kliknij commit na GitHubie -- powinieneś widzieć swoją ikonkę).
* [ ] W `RAPORT.md` są wszystkie wymagane screenshoty (z zadań 1, 2, 3, 4, 5, 6, 7).

---

## Materiały do doczytania

* **Pro Git book (PL) -- rozdziały 1-3:** [https://git-scm.com/book/pl/v2](https://git-scm.com/book/pl/v2)
* **Atlassian Git Tutorials -- Beginner:** [https://www.atlassian.com/git/tutorials/what-is-version-control](https://www.atlassian.com/git/tutorials/what-is-version-control)
* **GitHub Docs -- Hello World (15 min tutorial):** [https://docs.github.com/en/get-started/start-your-journey/hello-world](https://docs.github.com/en/get-started/start-your-journey/hello-world)
* **IntelliJ IDEA -- Set up a Git repository:** [https://www.jetbrains.com/help/idea/set-up-a-git-repository.html](https://www.jetbrains.com/help/idea/set-up-a-git-repository.html)
* **Oh Shit, Git!?!** -- co zrobić, kiedy coś popsujesz: [https://ohshitgit.com/](https://ohshitgit.com/)
* **Gotowe szablony `.gitignore` dla różnych języków:** [https://github.com/github/gitignore](https://github.com/github/gitignore)

---
