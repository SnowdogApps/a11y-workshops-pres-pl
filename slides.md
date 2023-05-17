---
theme: ./
author: 'Ania Karoń'
position: 'Specjalista ds. Dostępności'
position2: 'i Senior Frontend Developer'
email: 'anna.karon@snow.dog'
profilePicture: 'anna-karon-photo.jpg'
linkedin: 'https://www.linkedin.com/in/anna-karon/'

---

# Dostępność na froncie

Warsztaty

---
layout: aboutme
---

---

# Plan warsztatów


12:00 - 12:15 Wprowadzenie

12:15 - 12:35 Narzędzia do testowania, instalacja repozytorium

12:35 - 13:00 Poprawiamy dostępność: Struktura i semantyka

13:00 - 13:15 Przerwa

13:15 - 14:00 Poprawiamy dostępność: komponenty

14:00 - 14:15 Przerwa

14:15 - 14:45 Testujemy

14:45 - 15:00 Podsumowanie warsztatów


---
layout: center
class: "text-center"
---

# Accessibility space

## Jak będziemy pracować?

Repozytorium: [https://github.com/anqaka/a11y-space](https://github.com/anqaka/a11y-space)

Strona: [A11y space](https://a11y-space.vercel.app/)

<div>&nbsp;</div>

### Technologie:

[Astro.build](https://astro.build/)

HTML, [Tailwindcss](https://tailwindcss.com/), JS/TS

Deployment: Vercel (SSG)


---

# Testowanie dostępności
<div>&nbsp;</div>

## Testy automatyczne
* [Axe - rozszerzenie do przeglądarki](https://www.deque.com/axe/browser-extensions/)
* [Wave - rozszerzenie do przeglądarki](https://wave.webaim.org/extension/)
* [Lighthouse](https://developer.chrome.com/docs/lighthouse/accessibility/)
<div>&nbsp;</div>

## Testy manualne
* sprawdzenie kodu
* [ANDI](https://www.ssa.gov/accessibility/andi/help/install.html)
* Czytnik ekranu - VoiceOver (macOS), Narrator lub NDVA (Windows), [ChromeVox (rozszerzenie do przeglądarki)](https://chrome.google.com/webstore/detail/screen-reader/kgejglhpjiefppelpmljglcjbhoiplfn)


---

# Struktura i semantyka
<div>&nbsp;</div>

* Dokument HTML - RWD, język, tytuł
* Landmarks: `header`, `main`, `footer`, `section`, `nav`, `aside`
* Semantyczne elementy HTML: `<p>`, `<ul><li>...</li></ul>`, `<button>`, `<a href="/">`, `<article>`, `<address>`, `<time>` etc...
* Nagłówki - `<h1>` - `<h6>`

---


# Struktura i semantyka

```xml
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Page title</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
  </head>
  <body>
    <header>
      ...
    </header>
    <main>
      <h1>Heading</h1>
      ...
    </main>
    <aside>
      ...
    </aside>
    <footer>
      ...
    </footer>
  </body>
</html>
```

---

# Obrazki i teksty alternatywne
<div>&nbsp;</div>

## Obrazky informacyjne

Przekazują prostą koncepcję lub informacje, które można wyrazić w krótkiej frazie lub zdaniu. Alternatywny tekst powinien przekazywać znaczenie lub treść wyświetlaną wizualnie, która zazwyczaj nie jest dosłownym opisem obrazu.

oznaczania informacji, uzupełnienie informacji, przekazywanie wrażeń lub emocji

```xml
<img src="informative-image" alt="alternative text" />
```

---

# Obrazki i teksty alternatywne
<div>&nbsp;</div>

## Obrazki funkcjonalne

Są używane do inicjowania działań, a nie do przekazywania informacji, np w przyciskach i linkach.

```xml
<a href="/">
  <img src="logo-image" alt="Company logo" />
</a>

<a href="/" aria-label="Homepage">
  <img src="logo-image" alt="Company logo" />
</a>
```

---

# Obrazki i teksty alternatywne
<div>&nbsp;</div>

## Obrazki dekoracyjne
Nie dodają informacji do zawartości strony.

```xml
<img src="decorative-image" alt="" aria-hidden="true" />
```

[An alt Decision Tree on WAI Tutorials](https://www.w3.org/WAI/tutorials/images/decision-tree/)

---
layout: two-cols-header
---

# Alternatywny kontent

Elementy graficzne bez widocznej etykiety powinny mieć tekst alternatywny

::left::


## aria-label

Dodajemy bezpośrednio do elementu

```xml
<button type="button" aria-label="Add to cart">
  <svg>Add to cart icon</svg>
</button>
```

[aria-label docs](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-label)

::right::

## aria-labelledby

Podpinamy element (np. nagłówek), który opisuje sekcje używając jego `id`

```xml
<section type="button" aria-labelledby="section-heading">
  <h2 id="section-heading">Heading section</h2>
</section>
```

[aria-labelledby docs](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-labelledby)

---

# Alternatywny kontent

## aria-describedby

Używamy, by dodać dodatkowy opis (np. do pola formularza lub przycisku), podpinamy element, używając jego `id`

```xml
<form>
  <label for="fname">First name</label>
  <input aria-describedby="int2" autocomplete="given-name" id="fname" type="text">
  <p id="int2">Your first name is sometimes called your "given name".</p>
</form>
```

[aria-describedby docs](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-describedby)

---
layout: two-cols-header
---

# Jak skutecznie schować element?

**Warto pamiętać!** Ukrywaj z rozwagą, może to wpłynąć na SEO (np,, wizualne ukrycie nagłówka)

::left::

**Dla wszystkich**

```css
.element {
  display: none;
  visibility: hidden;
}
```

**Dla technologii asystujących, nie wizualnie**

`aria-hidden="true"`

```xml
<span class="aria-hidden">Decorative element</span>
```


::right::

**Tylko wizualnie**

```css
/* Hiding class, making content visible only to screen readers but not visually */
/* "sr" meaning "screen-reader" */

.sr-only:not(:focus):not(:active) {
  clip: rect(0 0 0 0);
  clip-path: inset(50%);
  height: 1px;
  overflow: hidden;
  position: absolute;
  white-space: nowrap;
  width: 1px;
}
```

Tailwindcss - `sr-only`


---

# Focus

**stan `focus` powinien być widoczny**

* css `outline`, przeglądarki dostarczają `focus`, jeśli nie dodajecie swoich styli, nie ustawiajcie `outline: none`
* kolejność elementów fokusowalnych
* `:focus` i `:focus-visible`

---
layout: image
image: '/photo-snowdog.jpeg'
---


---
layout: two-cols-header
---

# Tabs

<style>
li {
  font-size: 0.875rem;
}
</style>

::left::

**Aria - role i atrybuty**

* role=tablist
* role=tab
* role=tabpanel
* aria-selected
* aria-labelledby
* aria-controls


**Nawigacja klawiaturą**

* `Tab` - fokusowanie na aktywny tab
* `Left arrow`, `Right arrow` - przeniesienie fokusu między tabami
* `Space` i `Enter` - aktywacja taba
* `Home` (opcjonalnie) - przeniesienie fokusu na pierwszy tab
* `End` (opcjonalnie) - przeniesienie fokusu na ostatni tab


::right::

```xml
<div>
  <h2 id="heading">Heading</h2>
  <div role="tablist" aria-labelledby="heading">
    <button id="tab-1" type="button" role="tab" aria-selected="true" aria-controls="tabpanel-1">
      <span>Tab 1</span>
    </button>
    <button id="tab-2" type="button" role="tab" aria-selected="false" aria-controls="tabpanel-2" tabindex="-1">
      <span>Tab 1</span>
    </button>
  </div>
  <div id="tabpanel-1" role="tabpanel" aria-labelledby="tab-1">
    <p>
      Content tab 1
    </p>
  </div>
  <div id="tabpanel-2" role="tabpanel" aria-labelledby="tab-3" aria-hidden="true">
    <p>
      Content tab 2
    </p>
  </div>
</div>
```

---
layout: two-cols-header
---

# Dialog

<style>
li {
  font-size: 0.875rem;
}
</style>

::left::

**Aria - role i atrybuty**

* role=dialog
* aria-modal
* aria-labelledby
* aria-hidden


**Nawigacja klawiaturą**

* `Tab` - fokusowanie następnego elementu fokusowalnego wewnątrz modala
* `Shift + Tab` - fokusowanie poprzdniego elementu fokusowalnego wewnątrz modala
* `Escape` - zamknięcie modala i powrót fokusu na trigger


::right::

```xml
<div
  role="dialog"
  aria-modal="true"
  aria-hidden="true"
  class="dialog"
  aria-labelledby="heading"
>
  <div class="dialog-content" autofocus tabindex="0">
    <h2 id="heading">Heading</h2>
    dialog content
    <button type="button">Close</button>
  </div>
</div>
```

---

# Live regions

* `aria-live` - wskazuje AT dynamicznie zmieniające się na stronie (ustawiamy na kontenerze)
* wartość `polite` - informuje o zmianie, kiedy akończone zostanie aktualne zadanie
* wartość `assertive` - informuje o zmianie natychmiast
* `aria-atomic` - informuje, jak elementy w "obserwowanym" regionie (oznaczonym atrybutem `aria-live`) mają zostać przedstawione - tylko zmiany: `false`, czy wszystkie elementy: `true`



---
layout: thankyou

---
