# Nasazení webu Aktivní Jablonec

## Co je v této složce
- `index.html`, `o-nas.html`, `akce.html`, `404.html` — stránky webu
- `style.css` — veškerý vzhled
- `favicon.svg` — ikona do záložky prohlížeče
- `sitemap.xml`, `robots.txt` — pro vyhledávače (Google apod.)
- `images/kandidati/` — fotky kandidátů
- `CNAME` — pro GitHub Pages (viz níže), obsahuje `www.aktivnijablonec.cz`
- `og-image-sablona.html` — návrh obrázku pro náhled při sdílení odkazu na Facebooku/WhatsAppu (viz níže, není ještě aktivní)

## Nasazení na GitHub Pages (zvolený hosting)
1. Vytvořte na GitHubu nový repozitář (veřejný, stačí free účet) a nahrajte do něj obsah této složky (kromě `og-image-sablona.html` a `DEPLOY.md`, ty nejsou pro web potřeba).
2. V repozitáři: **Settings → Pages** → jako zdroj vyberte větev (např. `main`) a složku `/ (root)`.
3. Tamtéž do pole **Custom domain** zadejte `www.aktivnijablonec.cz` a uložte — GitHub si sám dopíše/ověří soubor `CNAME` (ten už v repozitáři je).
4. V DNS u Forpsi nastavte (viz DNS sekce níže) A záznamy pro `aktivnijablonec.cz` a CNAME pro `www`.
5. Po propsání DNS (může trvat od minut po pár hodin) se v GitHub Pages nastavení zpřístupní zaškrtávátko **Enforce HTTPS** — zaškrtněte ho, GitHub si sám vyřídí certifikát.

### DNS záznamy u Forpsi
Doména `aktivnijablonec.cz` (bez www) — 4× A záznam na pevné IP adresy GitHub Pages:
| Typ | Název | Hodnota |
|---|---|---|
| A | @ (nebo prázdné) | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

`www.aktivnijablonec.cz` — CNAME na váš GitHub Pages název:
| Typ | Název | Hodnota |
|---|---|---|
| CNAME | www | `vase-github-jmeno.github.io.` |

(`vase-github-jmeno` nahraďte svým skutečným uživatelským jménem na GitHubu.)

Až bude web nasazený, zkontrolujte, že:
1. `https://www.aktivnijablonec.cz/` zobrazuje `index.html`
2. `https://www.aktivnijablonec.cz/robots.txt` a `/sitemap.xml` jsou dostupné
3. Zaškrtnuté **Enforce HTTPS** v nastavení GitHub Pages

## Než pole živě
Pokud se doména liší od `aktivnijablonec.cz`, nahraďte ji v těchto souborech:
- `sitemap.xml` (3× `<loc>`)
- `robots.txt` (řádek `Sitemap:`)
- `index.html`, `o-nas.html`, `akce.html` — tagy `og:url` a `canonical`

## Registrace u Googlu (volitelné, ale doporučené)
1. Přidat web do [Google Search Console](https://search.google.com/search-console)
2. Odeslat `sitemap.xml`
3. Během pár dní se stránky začnou objevovat ve vyhledávání

## Obrázek pro sdílení na sociálních sítích (volitelné)
`og-image-sablona.html` je hotový návrh (1200×630 px) v barvách webu. Až bude potřeba, otevřete ho v prohlížeči, vyexportujte jako `og-image.png` (screenshot přesně 1200×630 px) a uložte do této složky. Pak do `<head>` každé stránky přidejte:
```html
<meta property="og:image" content="https://www.aktivnijablonec.cz/og-image.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:image" content="https://www.aktivnijablonec.cz/og-image.png">
```
Bez toho web funguje normálně, jen odkaz sdílený v chatu/na sociálních sítích nebude mít náhledový obrázek.
