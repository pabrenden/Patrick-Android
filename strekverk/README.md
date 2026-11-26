# Strekverk

Gjør et bilde om til tynne, plottervennlige streker og lagrer dem som SVG (i millimeter) eller G-code.
Hele appen er én fil, `index.html`. Åpne den i en nettleser (også på Android). Bildet forlater aldri maskinen.

Idéen og stilene Vekst og Trådkunst er hentet fra [Code Painter](https://github.com/JasBlack/code-painter) og skrevet om
for plotter: millimeter i stedet for piksler, ekte pennebredde, og SVG/G-code i stedet for et maleri på skjerm.

## Stiler
| Stil | Hva den gjør |
|---|---|
| Skravur | 1–4 lag krysskravur; mørkere tone gir flere lag |
| Bølger | Parallelle linjer som svinger mer der bildet er mørkt |
| Spiral | Én spiral fra midten med samme bølgeprinsipp |
| Koter | Topografiske kurver (marching squares) på tonenivåer |
| Prikker | Blå-støy-punkter tegnet som små sirkler eller trykk |
| Én linje | Hele bildet som én sammenhengende linje (TSP, nærmeste nabo + 2-opt) |
| Vekst | Én lukket linje som vokser og folder seg tettere der bildet er mørkt (differensiell vekst, fra code-painter) |
| Code Painter | Maler bildet med penselstrøk (grove til fine, langs formene i bildet). Eller slipp en SVG lagret fra Code Painter («save svg»). Hvert penselstrøk fylles med parallelle linjer som busthår, flater skraveres, det som er malt over skjules, og fargene samles til 1–8 penner |
| Strektegning (AI) | En AI-modell ([Informative Drawings](https://github.com/carolineec/informative-drawings), Chan m.fl. CVPR 2022, MIT-lisens; ONNX fra [ipsilondev/informative-drawings-onnx](https://huggingface.co/ipsilondev/informative-drawings-onnx)) tegner streker av et foto direkte i nettleseren. Tynne streker følges langs midten, tykke svarte partier skraveres og får kontur. Kan også bruke en ferdig strektegning, f.eks. fra APDrawingGAN |
| Trådkunst | Én tråd mellom spiker i en sirkel eller langs kanten (fra code-painter). Bruk tynn penn (0,1 mm) og stort papir |

## For plotteren
- Ekte mål: papirformat (A6–A2, Letter, kvadrat, egendefinert), marg og pennebredde i mm.
- Én penn, to penner (mørk + mellomtone) eller fire penner (CMYK). Hver penn blir et eget Inkscape-lag.
- Optimalisering: forenkling (RDP), fjerning av korte streker, skjøting av nære streker og sortering
  for kortest mulig pennløft. Viser blekklengde, pennløft og omtrentlig plottetid.
- «Simuler plotting» tegner strekene i den rekkefølgen plotteren vil gjøre det.
- Eksport: SVG, én SVG per penn, G-code (GRBL/servo, kommandoene kan endres) eller kopier SVG.
- Innstillingene lagres i SVG-en. Slipp SVG-en tilbake i appen for å hente dem.

AI-stilen laster modellen (ca. 9 MB) fra Hugging Face og onnxruntime-web fra jsDelivr første gang den brukes.
