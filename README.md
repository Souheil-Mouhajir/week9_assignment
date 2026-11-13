# Redesigning Morocco's unemployment map for every reader

A colour accessibility redesign of a choropleth of Morocco's 2024 census unemployment by region, built for a GW data science assignment (week 9). The original map (week 8) used the red, green and gold of the Moroccan flag. Under simulated deuteranopia, its two end classes (10.6 percent and 31.5 percent unemployment) sit only 9.0 units apart in CAM02-UCS colour space, against 53.7 with normal vision.

The notebook tests six palettes under simulated deuteranopia, protanopia and tritanopia and in grayscale. It replaces the flag colours with the ColorBrewer `PuOr` diverging palette and adds hatching above the national rate of 21.3 percent, with a value label on every region. It verifies the result with the Machado et al. (2009) colour vision simulator and WCAG 2.1 contrast ratios.

The rendered page is `week9_assignment.html`. With GitHub Pages turned on for this repository, it is published at `https://souheil-mouhajir.github.io/week9_assignment/week9_assignment.html`.

## Contents

```
week9_assignment/
  week9_assignment.ipynb    notebook, executed, with outputs
  week9_assignment.qmd      same notebook as plain text
  week9_assignment.html     rendered, self-contained page
  requirements.txt          Python packages
  data/
    mar_adm1.geojson        regional boundaries (geoBoundaries, cached)
    regions_rgph2024.csv    population and unemployment by region (HCP)
    regional_capitals.csv   the 12 regional capitals
  images/
    banner.svg              title banner
```

## Running it

The notebook needs Python 3.10 or later, matplotlib 3.10 or later (for per class hatch colours) and Quarto 1.4 or later. No API key is required.

```
pip install -r requirements.txt
quarto render week9_assignment.ipynb --execute
```

## Findings

| Palette | Smallest gap between classes, worst simulated deficiency | Gap between end classes, protanopia |
|:---|---:|---:|
| Week 8 flag colours | 7.0 | 11.4 |
| RdYlGn (traffic light) | 2.4 | 15.9 |
| RdBu (ColorBrewer) | 24.1 | 24.1 |
| PuOr (ColorBrewer), chosen | 24.2 | 44.6 |

Every WCAG 2.1 contrast check on the redesigned map passes. The value labels reach 21 to 1. Boundary and hatch colours are picked per class by contrast, which raises the border between Fes-Meknes and Draa-Tafilalet from 1.6 to 1 with a white line to 12.9 to 1 with a black one.

## References

- Birch, J. (2012) 'Worldwide prevalence of red-green color deficiency', *Journal of the Optical Society of America A*, 29(3), pp. 313-320.
- Harrower, M. and Brewer, C.A. (2003) 'ColorBrewer.org: an online tool for selecting colour schemes for maps', *The Cartographic Journal*, 40(1), pp. 27-37.
- Haut-Commissariat au Plan (2024) *Recensement General de la Population et de l'Habitat 2024: principaux resultats*. Rabat: HCP.
- Machado, G.M., Oliveira, M.M. and Fernandes, L.A.F. (2009) 'A physiologically-based model for simulation of color vision deficiency', *IEEE Transactions on Visualization and Computer Graphics*, 15(6), pp. 1291-1298.
- Runfola, D. et al. (2020) 'geoBoundaries: a global database of political administrative boundaries', *PLoS ONE*, 15(4), e0231866.
- W3C (2018) *Web Content Accessibility Guidelines (WCAG) 2.1*.

## Author

Souheil Mouhajir, Elliott School of International Affairs, The George Washington University.
