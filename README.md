# Google — ściągawka operatorów wyszukiwania (advanced search)
Plik zawiera listę najprzydatniejszych operatorów wyszukiwania w Google z wyjaśnieniami i przykładami. Używaj ich łącznie, by tworzyć precyzyjne zapytania (dorki). Pamiętaj o etyce — nie obchodź zabezpieczeń ani zasad serwisów.

---
## Dobre praktyki i uwagi
- Google często personalizuje wyniki (na podstawie lokalizacji, historii). Używaj trybu incognito / hl=pl i/lub parametrów URL do ujednolicenia wyników.
- Nie wszystkie operatory działają w 100% przewidywalnie — Google czasem zmienia zachowanie (np. link: czy cache: mają ograniczenia).
- site: z wildcardami (np. *.domain) może działać niestabilnie — testuj konkretne subdomeny.
- Unikaj automatycznego scrapingu wyników Google (narusza regulamin). Generuj linki i otwieraj je ręcznie albo używaj oficjalnego API (jeśli konieczne).
- filetype:pdf pomaga znaleźć dokumenty policy/raporty, ale część plików może być osadzona w systemach, do których Google nie ma dostępu.
- AROUND(n) jest przydatne, ale wyniki zależą od sposobu indeksacji treści (nie zawsze precyzyjne).
- Zwracaj uwagę na znaki specjalne i kodowanie URL (escape/quote) przy generowaniu linków.
---

## Podstawowe operatory

#### `""` - wyszukiwanie frazy dokładnej
Wyszukuje dokładne dopasowanie sekwencji słów.
Przykład:
```text
"polityka bezpieczeństwa informacji"
```
#### `-` - wykluczenie
Wyklucza terminy z wyników.
Przykład:
```text
"polityka bezpieczeństwa informacji"
```
---

### OR - operator logiczny (alternatywa)
Szuka wyników zawierających jedno z podanych słów.
Przykład:
```text
ubezpieczenia OR polisа
```
#### `*`- wildcard (joker)
Pasuje do jednego lub więcej słów (użyteczne w frazach).
Przykład:
```text
"raport * 2024"
```
#### `()`- grupowanie
Grupuje operatory/logikę.
Przykład:
```text
(site:gov.pl OR site:gov.ua) "raport" filetype:pdf
```
---

### Operatory lokalizujące w URL/tytule/tekście
#### `site:` - ograniczenie do domeny/poddomeny
Szukaj tylko w danej domenie lub hostu.
Przykład:
```text
site:gov.pl "strategia"
```
Uwaga: site:*.domain działa różnie — bezpieczniej testować konkretne subdomeny (np. site:bip.um.waw.pl).
#### `inurl:` - fraza w adresie URL
Znajduje strony, których URL zawiera podaną frazę.
Przykład:
```text
inurl:regulamin site:allegro.pl
```
#### `intitle:` - fraza w tytule strony
Wyszukuje gdy słowo występuje w <title>.
Przykład:
```text
intitle:"BIP" site:*.pl
```
#### `allintitle:` - wszystkie słowa muszą wystąpić w tytule
Przykład:
```text
allintitle: raport roczny 2024 site:gov.pl
```
#### `intext:` - słowo w treści strony
Przykład:
```text
intext:"incydent bezpieczeństwa" site:gov.pl
```
#### `allintext:` - wszystkie podane słowa w treści
Przykład:
```text
allintext: "backup" "procedura" "przywracanie"
```
#### `inanchor:` - tekst anchorów linków (mniej używane)
Przykład:
```text
inanchor:"więcej informacji" site:example.com
```
---

### Operatory plikowe i formaty
#### `filetype: / ext:` - typ pliku
Szukaj tylko określonego typu pliku (np. pdf, xlsx, docx).
Przykład:
```text
site:um.warszawa.pl filetype:pdf "rejestr umów"
```
ext: jest równoważny filetype: (czasem użyteczny w narzędziach).
---
### Zakresy, numery i daty
#### `..` - zakres liczb (numrange)
Przykład:
```text
"raport" 2018..2024 site:gov.pl
```
Użyteczne do lat, cen itp.
#### `AROUND(n)` - bliskość słów
Znajduje strony, gdzie dwa wyrażenia występują w odległości n słów.
Przykład:
```text
"incident response" AROUND(5) "policy"
```
---

### Specjalne / pomocnicze
#### `cache:` - zobacz kopię Google (może być ograniczone)
Przykład:
```text
cache:example.com
```
#### `related:` - strony podobne do podanego URL
Przykład:
```text
related:gov.pl
```
#### `link:` - strony linkujące do danego URL (często ograniczone / niestabilne)
Przykład:
```text
link:domena.pl
```
#### `source:` - w wyszukiwarce News (ograniczone do news.google.com)
Przykład:
```text
source:Poland "inflacja"
```
---

### Parametry URL (filtry, UI)
Możesz modyfikować linki Google bezpośrednio parametrami URL:
- tbs=qdr:h|d|w|m|y — filtr czasu (hour, day, week, month, year).
Przykład: tbs=qdr:y — ostatni rok.
- num= — liczba wyników na stronę (10..100).
Przykład: num=50.
- hl= — język interfejsu (hl=pl).
- as_qdr= — czas w niektórych kombinacjach (rzadziej używane).

Przykładowy kompletny URL:

`https://www.google.com/search?q=site:gov.pl+filetype:pdf+%22raport%22&tbs=qdr:y&num=50&hl=pl`
