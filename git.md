---
title: Git oraz GitHub
verticalSeparator: ---v
theme: night
revealOptions:
    transition: "fade"
---

![tytuł](assets/tytuł.png)

---

### Spis treści

1. Czym jest git?
2. Podstawy pracy z gitem
3. Praca online (GitHub)
4. Co jeszcze można zrobić w GitHubie

---

## Czym jest git?

### Git to rozproszony system kontroli wersji <!-- .element: class="fragment" data-fragment-index="1" -->

---v

**System kontroli wersji** - sposób śledzenia zmian np. w kodzie, albo dowolnych innych plikach. W tym zmian z różnych źródeł.

Przykładem mogą być dokumenty Google. <!-- .element: class="fragment" data-fragment-index="1" -->

---v

![xkcd - dokument](https://imgs.xkcd.com/comics/documents.png)

---v

**Rozproszony** system kontroli wersji - system kontroli wersji w którym każdy komputer ma pełną historię plików, co pozwala na usprawnienia w zarządzaniu wersjami

---

## Co to oznacza w praktyce?

---v

-   Git pozwala śledzić wszystkie zmiany w kodzie, zobaczyć kiedy zostały wprowadzone i przez kogo
-   Umożliwia rozdzielanie gałęzi kodu i ponowne ich łączenie z główną wersją <!-- .element: class="fragment" data-fragment-index="1" -->
-   Pozwala na współpracę w której każdy może pracować nad swoją częścią kodu i później połączyć ją z resztą <!-- .element: class="fragment" data-fragment-index="2" -->

---v

![xkcd - git](https://imgs.xkcd.com/comics/git.png)

---

# Podstawy pracy z gitem

<!-- .element style="width:110%" -->

---

### Jak zacząć?

Należy najpierw oczywiście Gita zainstalować; można go pobrać z https://git-scm.org/downloads.

Po instalacji należy się upewnić, że Git jest w `PATH`!

<!-- .element: class="fragment" data-fragment-index="1" -->

---

### Pierwsze repo programisty

Aby moć skorzystać z możliwości Gita, należy utworzyć repozytorium.

**Repozytorium** (też często **repo**) jest folderem z dodatkowymi informacjami dla Gita, za pomocą których przechowuje on również historię plików.

Git jest narzędziem konsolowym, więc należy otworzyć terminal / wiersz poleceń i przejść do folderu w którym chcemy stworzyć repo.

Aby je utworzyć, należy użyć komendy `git init`.

NOTE: wspomnieć o GUI do Gita! Przykłady: GitKraken, GitHub Desktop, TortoiseGit

---

### Śledzenie zmian w plikach

Dodaliśmy nasz kod źródłowy - co teraz?
Musimy powiedzieć Gitowi, żeby śledził te nowe pliki, co możemy zrobić za pomocą

```shell
$ git add <PLIK | FOLDER>
```

Gdybyśmy przypadkiem dodali zły plik, możemy go wycofać ze śledzenia używając

```shell
$ git rm <PLIK | FOLDER>
```

---v

### Git ma trzy główne komponenty w repozytoriach

-   repozytorium - folder w którym Git przechowuje historię plików <!-- .element: class="fragment" data-fragment-index="1" -->
-   indeks - miejsce do przygotowywania commitów <!-- .element: class="fragment" data-fragment-index="2" -->
-   working tree - pliki nad którymi właśnie pracujesz <!-- .element: class="fragment" data-fragment-index="3" -->

---v

### Podstawowy ciąg pracy w Git

1. modyfikowanie plików w working tree <!-- .element: class="fragment" data-fragment-index="1" -->
2. dodanie ich do indeksu aby mogły być uwzględnione w następnym commicie <!-- .element: class="fragment" data-fragment-index="2" -->
3. commit - pliki zostają przeniesione z indeksu do repozytorium <!-- .element: class="fragment" data-fragment-index="3" -->

---

### Główna waluta repo: commity

Po utworzeniu i zapisaniu naszych zmian, teraz musimy je zakomunikować do Gita robiąc tzw. **commit** - prosto mowiąc, jest on migawką z wszystkimi zmianami w plikach od momentu ostatniego commita.

W Git, wykonujemy commit za pomocą

```shell
$ git commit -m "<OPIS>"
```

Przedtem jednak, musimy mu powiedzieć kim jesteśmy - potrzebny jest username jak i e-mail:

```shell
$ git config --global user.name "Jan Kowalski"
$ git config --global user.email "jan.kowalski@tm1.edu.pl"
```

NOTE: wspomnieć o tym, że user.email musi się zgadzać z tym na GH!

---

### A teraz, kto wszystko zepsuł?

Z Gitem, odpowiedź jest łatwa: wystarczy użyć jednego z kilku narzędzi do badania commitów:

-   `git log`

```shell
$ git log
commit 3ced38946f641021d7ee2ae5608d8a444675d931 (HEAD -> master)
Author: fbrzoz <63065775+fbrzoz@users.noreply.github.com>
Date:   Sat Oct 31 19:35:06 2020 +0100

    Add additional netcode
```

<!-- .element style="width:110%; overflow:hidden !important" -->

-   `git reflog`

```shell
$ git reflog
3ced389 (HEAD -> master) HEAD@{0}: commit: Add netcode
d438591 HEAD@{1}: commit (initial): Add program entrypoint
```

<!-- .element style="width:110%; overflow:hidden !important" -->

---

## Rozgałęzienia

Czyli co gdy ma się wiele wersji jednocześnie

---

-   W dowolnym momencie (z dowolnego commita) można wydzielić nową gałąź (branch)
-   Branche od momentu rozdzielenia są niezależne od zmian w źródle <!-- .element: class="fragment" data-fragment-index="1" -->
-   Można kopiować (łączyć) zmiany z jednego brancha na drugi <!-- .element: class="fragment" data-fragment-index="2" -->

---v

![branche w GitKraken](assets/branches.png)

---

### Wyświetlanie branchy:

```sh [1|2]
> git branch
* master
```

---v

### Tworzenie nowego brancha

```sh
> git branch nazwa
```

Nie zmienia to jednak tego gdzie jesteśmy: <!-- .element: class="fragment" data-fragment-index="1" -->

```sh [1|2-3]
> git branch
* master
  nazwa
```

<!-- .element: class="fragment" data-fragment-index="1" -->

---

### Zmiana obecnego brancha (checkout)

```sh [1|1-2]
> git checkout nazwa
Switched to branch 'nazwa'
```

---

### Commity nie wpływają na inne branche

```sh [1|2|3|3-6|7|7-15]
> echo "on a branch" > branch.txt
> git add .
> git commit -m "commit z brancha"
[nazwa 855277b] branch
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 branch.txt
> git log
commit 855277b1af3fb2b60170698febeab4d975dacfed (HEAD -> nazwa)
Author: oplik0 <25460763+oplik0@users.noreply.github.com>
Date:   Sat Oct 31 19:06:12 2020 +0100
    commit z brancha
commit d041bfcb2b006ec87b9b5ff858aa9fd6417d6821 (master)
Author: oplik0 <25460763+oplik0@users.noreply.github.com>
Date:   Sat Oct 31 19:03:42 2020 +0100
    initial commit
```

<!-- .element style="width:110%;height:110%" -->

---v

```sh [1|2|2-6]
> git checkout master
> git log
commit d041bfcb2b006ec87b9b5ff858aa9fd6417d6821 (master)
Author: oplik0 <25460763+oplik0@users.noreply.github.com>
Date:   Sat Oct 31 19:03:42 2020 +0100
    initial commit
```

NOTE: jak widać jest tu tylko pierwszy commit - drugi nie przeszedł z brancha

---

### Łączenie branchy (merge)

```sh [1|2|2-7]
> git checkout master
> git merge nazwa
Updating d041bfc..855277b
Fast-forward
 test.txt | Bin 0 -> 14 bytes
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 branch.txt
```

NOTE: wspomnieć o konfliktach i ich rezolucji, a także o merge commitach i squashach

---

### Tagi

Służą do zaznaczania ważnych momentów w kodzie (np. nowych wydań)

```sh [1|2|2-3]
> git tag -a v1.0 -m "na pewno działająca aplikacja"
> git tag
v1.0
```

---v

```sh [1|1-11]
> git show v1.0
tag v1.0
Tagger: oplik0 <25460763+oplik0@users.noreply.github.com>
Date:   Sat Oct 31 19:29:14 2020 +0100

na pewno skonczona aplikacja

commit 855277b1af3fb2b60170698febeab4d975dacfed (tag: v1.0, nazwa)
Author: oplik0 <25460763+oplik0@users.noreply.github.com>
Date:   Sat Oct 31 19:06:12 2020 +0100
    branch
```

<!-- .element style="width:110%" -->

---

# Praca online

## (czyli w końcu GitHub)

---

## Jeśli ktoś jeszcze się nie zarejestrował: [github.com/join](https://github.com/join)

### Polecamy też dołączyć do GitHub Education: [education.github.com](https://education.github.com)

NOTE: wspomnieć o GitHub Education!

---

![github interface](assets/github-interface.png)

---v

![github new repo](assets/github-new-repo.png)

NOTE: Zaznaczyć by nie zaznaczać nic w "Initialize this repository with", ponieważ mamy już repo, ale normalnie można tak stworzyć nowe w którym coś już jest

---

### Dodawanie zdalnego repozytorium:

```sh
> git remote add origin https://github.com/nazwa-użytkownika/nazwa-repozytorium.git
```

<!-- .element style="width:115%" -->

NOTE: powiedzieć dlaczego jest tam origin

---

### Przesyłanie do niego swojego kodu:

```sh [1|1-12]
> git push -u origin master
Username for 'https://github.com': nazwa-użytkownika
Password for 'https://nazwa-użytkownika@github.com':
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 8 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (9/9), 1.35 KiB | 106.00 KiB/s, done.
Total 9 (delta 0), reused 0 (delta 0)
To https://github.com/nazwa-użytkownika/nazwa-repozytorium.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

<!-- .element style="width:110%" -->

NOTE: powiedzieć czym jest `-u` - czyli ze ustawia śledzenie origin na przyszłość

---

### Tworzenie kopii zdalnego repozytorium

```sh [1|1-7]
> git clone https://github.com/nazwa-użytkownika/nazwa-repozytorium.git
Cloning into 'nazwa-repozytorium'...
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 0), reused 9 (delta 0), pack-reused 0
Unpacking objects: 100% (9/9), done.
```

<!-- .element style="width:105%" -->

NOTE: zaznaczyć że często się pobiera repo z githuba zamiast tworzyć je lokalnie

---v

### Można też wybrać inną nazwę folderu

```sh
> git clone https://github.com/nazwa-użytkownika/nazwa-repozytorium.git nazwa-folderu
```

<!-- .element style="width:115%" -->

---

### Aktualizacja z remote

```sh
> git pull
```

Albo inaczej

```sh
> git fetch
> git merge FETCH_HEAD
```

NOTE: powiedzieć czym jest FETCH_HEAD i o tym że można dać argumenty do tych komend, ale zwykle nie trzeba

---

## Issues

Issues jest mechanizmem do śledzenia wszelkich problemów, sugestii czy innych typów feedbacku od deweloperów czy użytkowników.

NOTE: głównie praktyczna część, nie ma potrzeby na więcej tekstu

---

## Pull Requests

Pull Requests pozwala proponować zmiany w repozytorium z innego brancha w sposób, który pozwala właścicielom na szybkie przejrzenie i wprowadzenie zmian.

NOTE: głównie praktyczna część, nie ma potrzeby na więcej tekstu

---

### Forkowanie

Czyli jak rozwijać cudze repozytorium

---v
Jak forkować repozytorium?
![fork](assets/fork.png)

---v

Forkowane repozytoria są twoje, ale są powiązane w GitHubie z oryginalnymi
![forked repo](assets/forked-repo.png)

NOTE: pokazać to w praktyce :V

---

## Co jeszcze można zrobić w GitHubie?

---

### GitHub Pages

Prosty darmowy hosting stron statycznych

NOTE: powiedzieć czym są strony statyczne na wszelki wypadek

---v

![github pages](assets/github-pages.png)

---v

![github pages example](assets/github-pages-example.png)

---

### Projects

trochę jak trello, ale w GitHubie

---v

![create project](assets/new-project.png)

---v

![create project - settings](assets/new-project-settings.png)

---v

![example project](assets/existing-project.png)

---

## GitHub Actions ![logo](https://github.githubassets.com/images/modules/site/features/actions-icon-actions.svg)

Automatyzacja!

NOTE: pokazać w praktyce

---

# Pytania?

---

## Zasoby do nauki gita

-   [guides.github.com](https://guides.github.com/)
-   [lab.github.com](https://lab.github.com)
-   [git-scm.com](https://git-scm.com/)
-   [gitkraken.com/resources/learn-git](https://gitkraken.com/resources/learn-git)
-   [github.com/jlord/git-it-electron](https://github.com/jlord/git-it-electron)
-   [git-school.github.io/visualizing-git](https://git-school.github.io/visualizing-git)
