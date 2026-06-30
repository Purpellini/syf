# Co zostało poprawione

## 1. dpad.svgz — uszkodzony plik XML
Plik miał brakujący tag zamykający `</g>`, przez co przeglądarki
mogły w ogóle odmówić wyrenderowania tej grafiki jako tła CSS
(background-image wymaga poprawnego, dobrze sformowanego XML/SVG,
inaczej obrazek się nie wyświetli). Naprawiono brakujące zamknięcie.

UWAGA: część ścieżek (path) wewnątrz tego pliku ma współrzędne
kompletnie poza obszarem viewBox (np. wartości rzędu setek, gdy
viewBox obejmuje tylko niewielki wycinek), co sugeruje, że oryginalny
plik mógł być źle wyeksportowany/posklejany z różnych warstw.
Sama poprawka XML naprawia wczytywanie pliku, ale jeśli po podmianie
d-pad nadal wygląda wizualnie dziwnie (np. ucięte strzałki), to już
kwestia samej grafiki w środku, nie CSS — wymagałoby to poprawek
w edytorze SVG (Illustrator/Inkscape) na oryginalnym źródle.

## 2. Przyciski ABXY świeciły się jako kwadraty
Dodano `border-radius: 50%` do każdej z reguł `.button.triangle/
circle/cross/square`, żeby obwódka (`border`) i poświata
(`box-shadow`) podążały za okrągłym kształtem przycisku zamiast za
prostokątnym divem.

## 3. D-pad w ogóle się nie podświetlał
W oryginalnym CSS brakowało jakichkolwiek reguł dla klas
`.button.up`, `.button.down`, `.button.left`, `.button.right` —
Gamepad Viewer traktuje strzałki d-padu jako osobne przyciski,
niezależne od `.face` (które odpowiada wyłącznie za statyczne tło).
Dodano analogiczne reguły z obwódką/poświatą w kolorze złotym
(`#d4af37`) — możesz oczywiście zmienić kolor pod swój styl.

## 4. Triggery (L2/R2) świeciły się tylko górną częścią
Zamieniono `border` + `box-shadow` na `filter: drop-shadow(...)`.
`drop-shadow` (w odróżnieniu od `box-shadow`) podąża za realnym
kształtem kanału alfa grafiki w tle, a nie za prostokątnym boxem
elementu — dzięki temu poświata kopiuje pełny, zaokrąglony kontur
triggera zamiast tylko fragmentu prostokąta.

# Jak podmienić
1. Wrzuć całą zawartość folderu `svgs/` oraz `style.css` do swojego
   repo (np. na GitHub Pages), zachowując tę samą strukturę co linki
   w `style.css` (`.../svgs/nazwa.svgz`).
2. Wyczyść cache przeglądarki / OBS browser source po podmianie
   (`dpad.svgz` zmienił zawartość, więc stare cache może pokazywać
   wersję sprzed poprawki).
