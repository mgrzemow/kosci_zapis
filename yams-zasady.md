# Gra w kości — pełne zasady (wariant z wagami, anonsem, harmonią i pojedynkami)

> Zasady dla graczy (to „co", bez kodu). Implementacja, model danych i funkcje: [zapis.md](zapis.md). Opis aplikacji: [opis.md](opis.md). Aplikacja: https://mgrzemow.github.io/kosci_zapis/
> Status: aktualne 2026-06-25.

## Materiał i przebieg
- **5 kości** sześciennych. **Każdy gracz ma własną kartę**; karty są zależne (próg „≥ X", patrz niżej).
- Tura: **3 rzuty** (pierwszy wszystkimi, w 2. i 3. odkładasz wybrane i przerzucasz resztę). Po turze **wpisujesz wynik do jednego pola** albo **skreślasz** pole.
- Gra trwa, aż u wszystkich każde pole jest wypełnione lub skreślone.

## Kolumny (6) i wagi
Na start każda kolumna dostaje **losowo jedną z wag: 8, 10, 12, 14, 16, 18** (po jednej, wspólne dla wszystkich). Wynik kolumny mnoży się przez jej wagę — opłaca się ładować wysokie układy do kolumn o dużej wadze.

| Kolumna | Reguła wpisywania |
|---|---|
| Wolne | dowolna kolejność |
| Dół | z góry na dół (po kolei) |
| Góra | z dołu do góry (po kolei) |
| Harmonia | od **kreski** (środka) w górę **albo** w dół — rośnie w obie strony |
| Drugi rzut | wpis po **dokładnie 2 rzutach** |
| Anons | po **1. rzucie** mówisz „Anons" i musisz w tej kolumnie zapisać |

Liczbę rzutów i „Anons" pilnują gracze przy stole — aplikacja w kolumnach **Anons** i **Drugi rzut** pozwala na dowolną kolejność.

## Układ karty (od góry)
1. **Szkółka:** 1, 2, 3, 4, 5, 6.
2. **Suma szkółki** i **Premia za szkółkę** (liczą się same).
3. **─── Kreska ───** — środek planszy; stąd startuje Harmonia (nie jest polem do wpisania).
4. Pod kreską: **− (mniejsze)**, **+ (większe)**.
5. Figury: **Full, Kareta, Strit, Malusie, Poker**.
6. **Wynik kolumny (Σ//10)**, niżej **różnice do przeciwników** i **Wynik ost.** kolumny.

## Co się wpisuje: OCZKA z kości
W polach **Strit, Full, Kareta, Poker, Malusie** wpisujesz tylko **oczka z kości**, a pole samo przelicza na wartość końcową (po wyjściu z pola widać wynik, po wejściu w edycję wraca do oczek; podpowiedzi pokazują oczka).

| Pole | Wpisujesz (oczka) | Pole pokazuje |
|---|---|---|
| Strit | 15 lub 20 | 45 / 50 |
| Full | 5 … 30 | 25 … 50 |
| Kareta | 4 … 24 (co 4) | 34 … 54 |
| Poker | 5,10,…,30 | 75 … 100 |
| Malusie | 5 … 8 | 75 / 70 / 65 / 60 |

Pola **1–6**, **+**, **−** wpisujesz wprost (bez przelicznika).

## Punktacja
### Szkółka 1–6
Suma oczek danego nominału (jedynki = liczba 1, dwójki = 2 × liczba 2, …). Wartość musi być **wielokrotnością nominału** (np. dwójki: 0, 2, 4, 6, 8, 10).

### Pola + i − (pod kreską)
- Wpisujesz **sumę 5 kości**. Obie wartości **≥ 20**, przy czym **„+" > „−"**.
- Obie **dodają się** do sumy dołu. Są **powiązane**: skreślenie jednego **zeruje oba**.

### Figury (wpisujesz oczka)
- **Strit** (5 kolejnych) — mały (15 oczek) → **45**, duży (20) → **50**. Tylko te dwie wartości.
- **Full** (trójka + para; pięć jednakowych też się liczy) — oczka + **20** (25 … 50).
- **Kareta** (4 jednakowe) — liczysz **tylko te 4 kości**: oczka 4, 8, …, 24 (wielokrotność 4) + **30** → 34 … 54.
- **Malusie** (im mniej oczek, tym lepiej) — **tylko 5–8 oczek**: 5 → 75, 6 → 70, 7 → 65, 8 → 60. **9 i więcej = skreślenie (0).**
- **Poker** (5 jednakowych) — oczka 5, 10, …, 30 (wielokrotność 5) + **70** → 75 … 100.

## Premie
- **Premia za szkółkę** (osobno w każdej kolumnie, od sumy nominałów 1–6): ≥ 60 → **+30**, ≥ 70 → **+50**, ≥ 80 → **+100**.
- **Premia za kolumnę: +200** — gdy w kolumnie: suma szkółki **≥ 60** (skreślenia u góry dozwolone) **oraz** **cały dół wypełniony bez ani jednego skreślenia**.

## Wynik kolumny
`(suma szkółki + premia za szkółkę + suma dołu + 200) × waga`, a następnie **÷ 10 i zaokrąglony** do liczby całkowitej (np. 7658 → **766**). To wynik **bazowy** kolumny (na karcie: **Σ//10**).

## Pojedynki (head-to-head) — modyfikacja zapisu
Pod wynikiem bazowym, dla **każdego przeciwnika** liczymy różnicę w **każdej kolumnie**:
- **różnica = mój wynik kolumny − wynik przeciwnika** (dodatnia podbija mój wynik, ujemna obniża).
- **Dublowanie:** jeśli w kolumnie proporcja wyników **≥ 2×** (także gdy ktoś ma 0, a drugi > 0), różnicę liczymy **podwójnie**. Taki wpis jest **pogrubiony** — zielony na „+", czerwony na „−".
- **Wynik ost. kolumny** = wynik bazowy + suma różnic do wszystkich przeciwników (z dublowaniem).
- **Ostateczny wynik gracza** = suma „wyników ost." z 6 kolumn.

Symbole przy imieniu **przeciwnika** (z Twojej perspektywy), **tyle ile kolumn**:
- **★ złota gwiazdka** — w tylu kolumnach **Ty dublujesz** tego przeciwnika.
- **☠ czerwona czaszka** — w tylu kolumnach **on dubluje Ciebie**.

## Skreślanie
- Wpisujesz „x" → pole pokazuje **X** i liczy się za **0** (dobrowolnie lub z konieczności).
- Para **+/−** skreśla się wspólnie; skreślone pole **przestaje wyznaczać próg „≥"** dla innych.
- W kolumnach z kolejnością (Dół/Góra/Harmonia) skreślasz tylko bieżące pole; w **Anonsie** — po zapowiedzi; wyjątek **Drugi rzut** — można skreślić nawet po 3. rzucie (pilnują gracze).

## Zależność między graczami (próg „≥ X")
W danym polu (ta sama figura, ta sama kolumna) możesz wpisać wartość **nie niższą** niż najwyższa, którą wpisali tam już inni. Pole skreślone (X) lub puste u innych **nie** podnosi progu. W aplikacji widać to na żywo: podpowiedź „≥ X" (dla **malusie**, gdzie mniej oczek = więcej punktów, podpowiedź „≤ N" oczek).

## Koniec gry
Gdy karty wszystkich graczy są kompletne → **ranking** (ostateczne wyniki malejąco) u każdego.

## Do potwierdzenia (jedyne otwarte założenie)
Premia **+200** jest obecnie liczona **wewnątrz** mnożenia przez wagę (jak premia za szkółkę). Do ustalenia, czy ma być **płaska** (dodawana po przemnożeniu).
