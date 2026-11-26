# Strekverk

Gjør et bilde om til tynne, plottervennlige streker og lagrer dem som SVG (i millimeter) eller G-code.
Hele appen er én fil, `index.html`. Åpne den i en nettleser (også på Android). Bildet forlater aldri maskinen.

Idéen er inspirert av [Code Painter](https://github.com/JasBlack/code-painter), men koden er skrevet fra bunnen av
(Code Painter er «All rights reserved», og den lager malerier for skjerm, ikke streker for plotter).

## Stiler
| Stil | Hva den gjør |
|---|---|
| Skravur | 1–4 lag krysskravur; mørkere tone gir flere lag |
| Bølger | Parallelle linjer som svinger mer der bildet er mørkt |
| Spiral | Én spiral fra midten med samme bølgeprinsipp |
| Koter | Topografiske kurver (marching squares) på tonenivåer |
| Prikker | Blå-støy-punkter tegnet som små sirkler eller trykk |
| Én linje | Hele bildet som én sammenhengende linje (TSP, nærmeste nabo + 2-opt) |

## For plotteren
- Ekte mål: papirformat (A6–A2, Letter, kvadrat, egendefinert), marg og pennebredde i mm.
- Én penn, to penner (mørk + mellomtone) eller fire penner (CMYK). Hver penn blir et eget Inkscape-lag.
- Optimalisering: forenkling (RDP), fjerning av korte streker, skjøting av nære streker og sortering
  for kortest mulig pennløft. Viser blekklengde, pennløft og omtrentlig plottetid.
- «Simuler plotting» tegner strekene i den rekkefølgen plotteren vil gjøre det.
- Eksport: SVG, én SVG per penn, G-code (GRBL/servo, kommandoene kan endres) eller kopier SVG.
- Innstillingene lagres i SVG-en. Slipp SVG-en tilbake i appen for å hente dem.
