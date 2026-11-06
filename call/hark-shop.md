# Shop components

Components for a page that helps someone choose something to buy: a plain
title, a shelf of the library's photo cards standing each product on a studio
sweep, and the library's compare with its photos on the same sweep.
`hark-shop.css` styles them and is already in the site's folder. A page that
uses any of them links it after `hark.css` and the photo cards' files:

```html
<link rel="stylesheet" href="hark.css" />
<link rel="stylesheet" href="hark-cards.css" />
<link rel="stylesheet" href="hark-shop.css" />
...
<script src="hark.js"></script>
<script src="hark-cards.js"></script>
```

Each block of the page after the shelf is the library's `section` with its
`head`; on a shop page the head stays left-aligned.

## shop title

The page's title with no hero, left-aligned on the page.

| part    | markup                               | notes                                                         |
| ------- | ------------------------------------ | ------------------------------------------------------------- |
| wrapper | `<header class="shop-title">`        | required, first in `main`                                     |
| title   | `<h1>`                               | required; what is being bought, in plain words                |
| eyebrow | `<p class="shop-title__eyebrow">`    | optional; a short line under the title, such as when prices were checked |
| intro   | `<p class="shop-title__intro">`      | optional; the answer in two sentences at most, linking to the card it names with `link` |

```html
<header class="shop-title">
  <h1>The five best-selling Rimowa carry-ons</h1>
  <p class="shop-title__eyebrow">US prices as of Oct 23, 2026</p>
  <p class="shop-title__intro">Our pick is the <a class="link" href="#classic">Classic Cabin</a>. The <a class="link" href="#essential">Essential Cabin</a> is the value.</p>
</header>
```

## shelf

The products as the library's photo cards, in the order the request ranks
them. On a shop page each card stands its product on a studio sweep: the photo
is a square that fits the product whole, so use cutout product shots, and the
cards add the product's colors before the store link.

Use it for: the products the page compares, up to about eight, right after
the title.

Skip it when: there are many more products than a reader would scan as cards
(use a table for the long tail).

The cards are the library's photo cards, inside the shelf. These are the
shelf's own parts, and what a product card adds to the library's:

| part    | markup                                                         | notes |
| ------- | -------------------------------------------------------------- | ----- |
| shelf   | `<section class="shelf" id="products" data-nav="Products">`    | required; not a `section`, so it has no `head`; holds the library's `photo-cards` row |
| label   | `<div class="shelf__head"><p class="shelf__label">...</p></div>` | required; one line on how the products are ranked |
| meta    | the card's meta line                                           | material, size or edition |
| warning | `<p class="dot dot--no">` after the note                       | optional; one thing that rules it out for some readers, such as "Too big for most US carry-on limits" |
| colors  | `<p class="photo-card__colors"><span class="minis" aria-hidden="true"><i style="--swatch:#b4b4b4" title="Silver"></i></span>2 colors</p>` | optional, before the link; one dot per color, then the count |
| hark    | the card's Hark button, labelled _Buy with Hark_               | when Hark can buy the product for the reader, before the link |
| link    | the card's link                                                | required when there is one; name the store: _Shop on rimowa.com_ |

Every photo is a file or URL in the markup itself.

```html
<section class="shelf" id="products" data-nav="The five">
  <div class="shelf__head">
    <p class="shelf__label">In Rimowa's best-seller order.</p>
  </div>
  <div class="photo-cards">
    <article class="photo-card" id="classic">
      <div class="photo-card__stage">
        <p class="photo-card__rank">Our pick</p>
        <div class="photo-card__photos">
          <img src="classic-front.webp" alt="Classic Cabin in silver, front" />
          <img src="classic-side.webp" alt="Classic Cabin in silver, side" loading="lazy" />
          <img src="classic-back.webp" alt="Classic Cabin in silver, back" loading="lazy" />
        </div>
      </div>
      <div class="photo-card__body">
        <div class="photo-card__head"><h3>Classic Cabin</h3><p class="photo-card__price">$1,650</p></div>
        <p class="photo-card__meta">Anodized aluminum · latches</p>
        <p class="photo-card__note">The heritage icon in grooved metal. The heaviest here, and it dents into a patina.</p>
        <p class="photo-card__colors"><span class="minis" aria-hidden="true"><i style="--swatch:#b4b4b4" title="Silver"></i><i style="--swatch:#877e6c" title="Titanium"></i></span>2 colors</p>
        <a class="btn" data-hark-action="buy-classic">Buy with Hark</a>
        <a class="link" href="https://www.rimowa.com" target="_blank" rel="noopener">Shop on rimowa.com</a>
      </div>
    </article>
  </div>
</section>
```

## compare

The products side by side use the library's compare, as it shows, with each
option's photo, a chip for its rank label, and the specs that decide the
choice; bold the best value in a row with `<strong>`. On a shop page its photos
sit on the same stage as the cards. A number worth reading at a glance, such
as weight or volume, can carry `<span class="meter" style="--v:0.71"></span>`
after it: a bar on one scale for its whole row, from zero, where `--v` is the
value over the row's scale. A yes or no row reads as `<span class="dot">Fits
most</span>` or `<span class="dot dot--no">Too big</span>`. Under a count of
colors, `<span class="minis">` shows them as small dots. For shopping comparisons,
use compare over tables even if the number of items exceeds five.
