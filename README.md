# tal_graph_edge_coloring

**Przedmiot:** Techniki algorytmiczne

# Opis problemu

**Kolorowanie grafu** w ogólności polega na przypisaniu elementom grafu (wierzchołkom lub, rzadziej, krawędziom) wybranych kolorów wedle dokładnie określonych zasad.

**Kolorowanie wierzchołkowe** grafu polega na przyporządkowaniu wierzchołkom liczb naturalnych tak, aby żadne dwa sąsiadujące ze sobą wierzchołki nie miały przyporządkowanej tej samej liczby.

**Kolorowanie krawędziowe** grafu polega na przyporządkowaniu krawędziom liczb naturalnych tak, aby żadne dwie sąsiednie krawędzie nie miały przyporządkowanej tej samej liczby.

Ze względów historycznych, oraz dla lepszego zobrazowania problemu zamiast o liczbach mówi się o kolorach i kolorowaniu.

**Optymalne pokolorowanie** wierzchołków lub krawędzi zachodzi wtedy, gdy użyto najmniejszej liczby kolorów.

W tej pracy zajmę się kolorowaniem krawędziowym z użyciem algorytmu **NC** oraz własnego algorytmu heurystycznego.

# Opis wybranego algorytmu dokładnego

Wybrany przeze mnie algorytm dokładny do NC. Polega on na wybieraniu dowolnej niepokolorowanej krawędzi i przypisywaniu jej zachłannie koloru innego niż kolory sąsiadujących z nią krawędzi. Jeśli takiego koloru brak wśród kolorów wykorzystanych należy dobrać nowy kolor

Algorytm ten ma złożoność pesymistyczną O(nΔ), gdzie n – liczba krawędzi, a Δ – stopień grafu, ponieważ algorytm przechodzi przez każdą krawędź i w najgorszym przypadku sprawdza kolory Δ krawędzi.

# Opis opracowanego algorytmu heurystycznego

Na potrzeby zadania opracowałem dwa algorytmy.

Pierwszy z nich polega na przechodzeniu kolejno wszystkich wierzchołków, od wierzchołka o najwyższym stopniu i kolorowaniu niepokolorowanych krawędzi z nich wychodzących. Niestety okazało się, że algorytm daleki jest od optymalnego, ze względu na swoją złożoność pesymistyczną O(nΔ2), gdzie n – liczba wierzchołków, a Δ – stopień grafu. Złożoność jest tak wysoka, ponieważ algorytm wymaga przejścia przez wszystkie wierzchołki po kolei (stąd bierze się n), a następnie sprawdzenia sąsiadów każdego wierzchołka (stąd Δ). Na końcu należy sprawdzić sąsiadów, ponieważ mogły zostać one pokolorowane wcześniej, co sprawia ryzyko złego doboru koloru (stąd Δ2).

Drugi zaproponowany algorytm jest podobny do algorytmu NC. Polega on na wstępnym losowym przypisaniu kolorów do krawędzi, a następnie sprawdzeniu, czy graf został pokolorowany prawidłowo, czyli czy każda krawędź ma różnokolorowych sąsiadów. Jeśli nie, to krawędź jest rekolorowana. Złożoność pesymistyczna tego algorytmu jest taka sama jak NC, czyli O(nΔ), jednakże sposób kolorowania jest daleki od optymalnego, ze względu na losowość kolorowania, a więc brak panowania nad liczbą kolorów.

Ze względu na wyższą dokładność pierwszego algorytmu, resztę rozważań i obliczeń poświęcono właśnie jemu.

# Złożoność, wrażliwość oraz dokładność wybranych algorytmów

**Złożoność obliczeniowa algorytmu** – ilość zasobów komputerowych potrzebnych do jego wykonania:

**Czasowa złożoność obliczeniowa** – to miara czasu czasu działania algorytmu. Przyjętą miarą złożoności czasowej jest liczba operacji podstawowych w zależności od rozmiaru danych wejściowych.

**Pamięciowa złożoność obliczeniowa** – to miara ilości wykorzystanej przez algorytm pamięci. Jako miarę złożoności pamięciowej najczęściej przyjmuje się użytą pamięć maszyny abstrakcyjnej (np. liczbą komórek pamięci RAM) w funkcji rozmiaru danych wejściowych.

W praktyce złożoność obliczeniową prezentuję się jako funkcję ilości danych, czyli zależną od rozmiarów danych wejściowych algorytmu.

## Pesymistyczna złożoność obliczeniowa

Pesymistyczną złożonością obliczeniową nazywa się złożoność przy założeniu wystąpienia „najgorszych&quot; danych wejściowych, czyli takich, które sprawią, że program będzie chodził najdłużej jak to możliwe. Do zapisu pesymistycznej złożoności obliczeniowej stosuję się notację dużego O.

Pesymistyczną złożoność obliczeniową wyraża wzór:

![](RackMultipart20210823-4-1nujvfu_html_e3ac91b15a6eae37.png)

gdzie

 - algorytm rozwiązujący decyzyjny problem  ;
 Dn - zbiór danych rozmiaru n dla rozważanego problemu;
 t(I- liczba kroków DTM potrzebna do rozwiązania konkretnego problemu IDn o rozmiarze N(z)  n przy pomocy algorytmu 

### Algorytm NC

Algorytm NC przechodzi przez każdą krawędź w celu pokolorowania jej, a więc wykonuje n operacji, gdzie n oznacza liczbę krawędzi grafu. Następnie dla każdej krawędzi sprawdza jej kolory swoich sąsiadów i wybiera kolor inny niż któregokolwiek z nich – oznacza to, że dla każdej z krawędzi wykonuje tyle operacji, ile krawędzi wychodzących ma każdy z incydentnych do niej wierzchołków minus jeden. W najgorszym przypadku każdy z wierzchołków ma najwyższy stopień w grafie, a więc wychodzi z niego Δ krawędzi, a co za tym idzie, dla każdej z n krawędzi wykonywane jest 2 razy Δ-1 sprawdzeń.

Zatem pesymistyczna czasowa złożoność algorytmu NC wynosi O(nΔ). Wzór opisujący liczbę operacji jest postaci:

Algorytm NC przechowuje informacje o n krawędziach oraz o k użytych kolorach, a więc potrzeba n + k komórek pamięci. W najgorszym przypadku zostanie użytych tyle kolorów ile jest krawędzi, zatem pesymistyczna pamięciowa złożoność wynosi O(n + n), czyli O(n).

### Zaproponowany algorytm heurystyczny

Zaproponowany algorytm heurystyczny przechodzi kolejno przez każdy z wierzchołków kolorując gałęzie zachłannie, a więc wykonuje przynajmniej m operacji, gdzie m – liczba wierzchołków. Przy każdej iteracji algorytm przechodzi przez wszystkie krawędzie incydentne do danego wierzchołka sprawdzając ich kolory, lub kolorując te niepokolorowane, co w najgorszym możliwym przypadku daje Δ operacji, gdzie Δ – stopień grafu. Przy każdej operacji kolorowania należy dodatkowo sprawdzić wszystkich sąsiadów kolorowanej gałęzi przy drugim wierzchołku, a więc wykonywane jest Δ-1 operacji. Ponieważ gałęzi bez przydzielonego koloru jest coraz mniej, to w każdym kroku jest sprawdzanych coraz mniej sąsiadów, co daje log(Δ).

Zatem pesymistyczna czasowa złożoność proponowanego algorytmu heurystycznego wynosi O(mΔlog(Δ)), a tak naprawdę O(Δ2log(Δ)), ponieważ w najgorszym przypadku m = Δ + 
Zaproponowany algorytm heurystyczny przechowuje informacje o n krawędziach oraz o k użytych kolorach, a więc potrzeba n + k komórek pamięci. W najgorszym przypadku zostanie użytych tyle kolorów ile jest krawędzi, zatem pesymistyczna pamięciowa złożoność wynosi O(n + n), czyli O(n).

## Oczekiwana złożoność obliczeniowa

Oczekiwaną (średnią) złożonością obliczeniową nazywa się złożoność przy założeniu &quot;typowych&quot; (statystycznie oczekiwanych) danych wejściowych. Do zapisu optymistycznej złożoności obliczeniowej stosuje się notację Θ.

Oczekiwaną złożoność obliczeniową wyraża wzór:

![](RackMultipart20210823-4-1nujvfu_html_4b4860ec9fd03c96.png)

gdzie

p(I) - prawdopodobieństwo występowania danych IDn;
 Xn - zmienna losowa o wartościach t(I) i rozkładzie p(I);
 t(I) - liczba operacji podstawowych (liczba kroków algorytmu ) wykonanych przez algorytm na danych.

### Algorytm NC

Algorytm NC przechodzi przez każdą krawędź w celu pokolorowania jej, a więc wykonuje n operacji, gdzie n oznacza liczbę krawędzi grafu. Następnie dla każdej krawędzi sprawdza jej kolory swoich sąsiadów i wybiera kolor inny niż któregokolwiek z nich – oznacza to, że dla każdej z krawędzi wykonuje tyle operacji, ile krawędzi wychodzących ma każdy z incydentnych do niej wierzchołków minus jeden. Według [20] oraz [21] rozkład stopni wierzchołków w grafie przypomina rozkład Poissona.

Rozkład wierzchołków w losowym grafie opisuje wzór:

![](RackMultipart20210823-4-1nujvfu_html_89333f34f8d95ec8.png)

Zatem wzór opisujący oczekiwaną liczbę operacji jest postaci: n\*E(Xn), gdzie E(Xm) – wartość oczekiwana rozkładu Poissona.

Algorytm NC przechowuje informacje o n krawędziach oraz o k użytych kolorach, a więc potrzeba n + k komórek pamięci. W średnim przypadku zostanie użytych przynajmniej tyle kolorów, ile krawędzi ma największy wierzchołek grafu, zatem średnia pamięciowa złożoność wyniesie (n + Δ), czyli (n).

### Zaproponowany algorytm heurystyczny

Zaproponowany algorytm heurystyczny przechodzi kolejno przez każdy z wierzchołków kolorując gałęzie zachłannie, a więc wykonuje przynajmniej m operacji, gdzie m – liczba wierzchołków. Przy każdej iteracji algorytm przechodzi przez wszystkie krawędzie incydentne do danego wierzchołka sprawdzając ich kolory, lub kolorując te niepokolorowane. Wg [20] oraz [21] rozkład stopni wierzchołków w grafie przypomina rozkład Poissona. Przy każdej operacji kolorowania należy dodatkowo sprawdzić wszystkich sąsiadów kolorowanej gałęzi przy drugim wierzchołku, a więc wykonywane jest E(Xm) operacji. Ponieważ gałęzi bez przydzielonego koloru jest coraz mniej, to w każdym kroku jest sprawdzanych coraz mniej sąsiadów, co daje log(E(Xm)), gdzie E(Xm) – wartość oczekiwana rozkładu Poissona.

Rozkład wierzchołków w losowym grafie opisuje wzór:

![](RackMultipart20210823-4-1nujvfu_html_89333f34f8d95ec8.png)

Zatem wzór opisujący oczekiwaną liczbę operacji jest postaci: n\*E(Xm)\*log(E(Xm)) , gdzie n – liczba krawędzi, m – liczba wierzchołków.

Zaproponowany algorytm heurystyczny przechowuje informacje o n krawędziach oraz o k użytych kolorach, a więc potrzeba n + k komórek pamięci. W średnim przypadku zostanie użytych przynajmniej tyle kolorów, ile krawędzi ma największy wierzchołek grafu, zatem średnia pamięciowa złożoność wyniesie (n + Δ), czyli (n).

## Teoretyczna wrażliwość pesymistyczna

Miara wrażliwości pesymistycznej odzwierciedla to, jak dokładnie funkcja złożoności pesymistycznej odzwierciedla rzeczywisty czas działania algorytmu.

Wrażliwość pesymistyczną wyraża wzór:

![](RackMultipart20210823-4-1nujvfu_html_5a4d550bab03c21.png)

gdzie

Dn- zbiór danych rozmiaru n dla rozważanego problemu;
 t(I)- liczba operacji podstawowych (liczba kroków algorytmu ) wykonanych przez algorytm na danych I Dn.

Dla algorytmu NC wrażliwość pesymistyczna wynosi: nΔ, gdzie n – liczba krawędzi, Δ – stopień grafu.

Dla algorytmu heurystycznego wrażliwość pesymistyczna wynosi: Δ3, Δ – stopień grafu.

## Teoretyczna wrażliwość oczekiwana

Miara wrażliwości oczekiwanej odzwierciedla to, jak dokładnie funkcja złożoności oczekiwanej odzwierciedla rzeczywisty czas działania algorytmu.

Wrażliwość oczekiwaną wyraża wzór:

![](RackMultipart20210823-4-1nujvfu_html_302ba3b1b9813bbd.png)

gdzie

Dn- zbiór danych rozmiaru n dla rozważanego problemu;
 t(I)- liczba operacji podstawowych (liczba kroków algorytmu ) wykonanych przez algorytm na danych I Dn;
 p(I)- prawdopodobieństwo występowania danych I Dn;
 Xn- zmienna losowa o wartościach t(I) i rozkładzie p(I) dla I Dn.

Dla algorytmu NC wrażliwość oczekiwana wynosi: , gdzie n – liczba krawędzi, m – liczba wierzchołków.

Dla algorytmu heurystycznego oczekiwana pesymistyczna wynosi: , gdzie n – liczba krawędzi, m – liczba wierzchołków.

# Eksperymenty

Przeprowadzono szereg eksperymentów na algorytmie NC oraz algorytmie heurystycznym i porównano faktyczną liczbę operacji z wyliczonymi pesymistyczną i średnią złożonością obliczeniową, a także sprawdzono ich złożoność pamięciową oraz dokładność.

## Złożoność obliczeniowa

Z przeprowadzonych testów wynika, że poprawnie wyliczono wartość oczekiwaną rozkładu Poissona oraz pesymistyczną złożoność i wyniki odpowiadają oczekiwaniom.

Wyniki testów algorytmu NC:

![](RackMultipart20210823-4-1nujvfu_html_37a3ef4e56fbabf4.png)

Wyniki testów algorytmu heurystycznego:

![](RackMultipart20210823-4-1nujvfu_html_2feb36d61bd9807.png)

## Złożoność pamięciowa

Z przeprowadzonych eksperymentów wynika, że faktyczna złożoność pamięciowa algorytmów jest znacznie niższa od pesymistycznej złożoności.

Wyniki testów algorytmu NC:

![](RackMultipart20210823-4-1nujvfu_html_bfe4c33b7195498b.png)

Wyniki testów algorytmu heurystycznego:

## ![](RackMultipart20210823-4-1nujvfu_html_c5530e1fb41a3009.png) Dokładność algorytmów

Z twierdzenia Vizinga [16] wynika, że indeks chromatyczny (liczba kolorów użytych do kolorowania) w optymalnym kolorowaniu krawędziowym spełnia nierówność:

![](RackMultipart20210823-4-1nujvfu_html_1f8376d66f23cdf2.png)

gdzie

Δ ![](RackMultipart20210823-4-1nujvfu_html_d27b568f7b44bcae.png) (G) – maksymalny stopień wierzchołka w grafie

- indeks chromatyczny grafu

Z eksperymentów wynika, że algorytm NC spełnia to założenie, za to algorytm heurystyczny spełnił go w dwóch przypadkach na pięć zaprezentowanych poniżej:

Wyniki testów algorytmu NC:

![](RackMultipart20210823-4-1nujvfu_html_a252f35bd323a20a.png)

Wyniki testów algorytmu heurystycznego:

![](RackMultipart20210823-4-1nujvfu_html_9f5400bf5c142ffd.png)

# Bibliografia

**Złożoność obliczeniowa:**

1. [https://repozytorium.amu.edu.pl/bitstream/10593/386/1/rozprawa\_dr\_KR-K.pdf](https://repozytorium.amu.edu.pl/bitstream/10593/386/1/rozprawa_dr_KR-K.pdf)
2. [https://courses.maths.ox.ac.uk/node/view\_material/3347](https://courses.maths.ox.ac.uk/node/view_material/3347)
3. [http://tarapata.strefa.pl/p\_techniki\_algorytmiczne/download/tal\_wyklad\_3.pdf](http://tarapata.strefa.pl/p_techniki_algorytmiczne/download/tal_wyklad_3.pdf)
4. [http://tarapata.strefa.pl/p\_techniki\_algorytmiczne/download/tal\_wyklad\_4.pdf](http://tarapata.strefa.pl/p_techniki_algorytmiczne/download/tal_wyklad_4.pdf)
5. [https://pl.wikipedia.org/wiki/Z%C5%82o%C5%BCono%C5%9B%C4%87\_obliczeniowa](https://pl.wikipedia.org/wiki/Z%C5%82o%C5%BCono%C5%9B%C4%87_obliczeniowa)
6. [https://en.wikipedia.org/wiki/Computational\_complexity](https://en.wikipedia.org/wiki/Computational_complexity)
7. [https://en.wikipedia.org/wiki/Time\_complexity](https://en.wikipedia.org/wiki/Time_complexity)
8. [https://pl.wikipedia.org/wiki/Asymptotyczne\_tempo\_wzrostu#Notacja\_%E2%80%9E%CE%98%E2%80%9D](https://pl.wikipedia.org/wiki/Asymptotyczne_tempo_wzrostu#Notacja_%E2%80%9E%CE%98%E2%80%9D)
9. [http://iswiki.if.uj.edu.pl/images/4/4b/AiSD\_02.\_Analiza\_algorytm%C3%B3w.pdf](http://iswiki.if.uj.edu.pl/images/4/4b/AiSD_02._Analiza_algorytm%C3%B3w.pdf)

**Kolorowanie grafów:**

1. [https://inf.ug.edu.pl/~hanna/grafy/14\_kolorowanie.pdf](https://inf.ug.edu.pl/~hanna/grafy/14_kolorowanie.pdf)
2. [http://www.ecei.tohoku.ac.jp/alg/nishizeki/sub/j/DVD/PDF\_P/P032.pdf](http://www.ecei.tohoku.ac.jp/alg/nishizeki/sub/j/DVD/PDF_P/P032.pdf)
3. [http://www.ecei.tohoku.ac.jp/alg/nishizeki/sub/j/DVD/PDF\_J/J128.pdf](http://www.ecei.tohoku.ac.jp/alg/nishizeki/sub/j/DVD/PDF_J/J128.pdf)
4. [https://en.wikipedia.org/wiki/Edge\_coloring](https://en.wikipedia.org/wiki/Edge_coloring)
5. [https://en.wikipedia.org/wiki/Vizing%27s\_theorem](https://en.wikipedia.org/wiki/Vizing%27s_theorem)
6. [https://pl.wikipedia.org/wiki/Kolorowanie\_kraw%C4%99dzi](https://pl.wikipedia.org/wiki/Kolorowanie_kraw%C4%99dzi)
7. [https://pl.wikipedia.org/wiki/Twierdzenie\_Vizinga](https://pl.wikipedia.org/wiki/Twierdzenie_Vizinga)
8. [https://pl.wikipedia.org/wiki/Kolorowanie\_grafu](https://pl.wikipedia.org/wiki/Kolorowanie_grafu)
9. [http://fileadmin.cs.lth.se/cs/Personal/Andrzej\_Lingas/k-m.pdf](http://fileadmin.cs.lth.se/cs/Personal/Andrzej_Lingas/k-m.pdf)
10. [https://books.google.pl/books?id=fokbCAAAQBAJ&amp;pg=PA19&amp;lpg=PA19&amp;dq=coloring+graph+NTL+algorithm&amp;source=bl&amp;ots=D0cxgisJ2O&amp;sig=ACfU3U3g4uXDvgw1ZXsHLNgXGa6xk8rDZg&amp;hl=en&amp;sa=X&amp;ved=2ahUKEwiwrL2i6fvpAhXQtYsKHe4DDt8Q6AEwC3oECAkQAQ#v=onepage&amp;q=coloring%20graph%20NTL%20algorithm&amp;f=false](https://books.google.pl/books?id=fokbCAAAQBAJ&amp;pg=PA19&amp;lpg=PA19&amp;dq=coloring+graph+NTL+algorithm&amp;source=bl&amp;ots=D0cxgisJ2O&amp;sig=ACfU3U3g4uXDvgw1ZXsHLNgXGa6xk8rDZg&amp;hl=en&amp;sa=X&amp;ved=2ahUKEwiwrL2i6fvpAhXQtYsKHe4DDt8Q6AEwC3oECAkQAQ#v=onepage&amp;q=coloring%20graph%20NTL%20algorithm&amp;f=false)
11. [http://www.if.pw.edu.pl/~agatka/moodle/charakterystyki.html](http://www.if.pw.edu.pl/~agatka/moodle/charakterystyki.html)
12. [https://en.wikipedia.org/wiki/Erd%C5%91s%E2%80%93R%C3%A9nyi\_model](https://en.wikipedia.org/wiki/Erd%C5%91s%E2%80%93R%C3%A9nyi_model)