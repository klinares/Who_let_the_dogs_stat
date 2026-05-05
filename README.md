# 🐕 Who_let_the_dogs_stat

> *"Who let the dogs stat? Who? Who? Who?"*

![](images/clipboard-1442720004.png)

An interactive data visualization dashboard exploring modern dog breeds through AKC behavioral trait data — developed as the final project for **SURV 752: Data Visualization** at the University of Maryland. Originally framed as a data science presentation to Nestlé Purina administrators, this tool lets users explore breed distributions, behavioral profiles, geographic origins, and side-by-side trait comparisons across hundreds of recognized breeds.

**Author:** Kevin Linares · University of Maryland

------------------------------------------------------------------------

\## What's in the Dashboard

The rendered HTML file is fully self-contained and interactive. It includes five sections:

| Section | What It Shows |
|------------------------------------|------------------------------------|
| **KPI Cards** | At-a-glance stats: total breeds, average lifespan, most common AKC group, healthiest size class |
| **Distribution of Breeds** | Mosaic plot of breed size × group; Very Large breeds dominate at 53% |
| **Distinct Breed Characteristics** | Small-multiples line graph of 6 behavioral traits (adaptability, friendliness, trainability, energy, etc.) across AKC breed groups |
| **Important Comparison Dimensions** | Scatterplot of weight (log scale) vs. lifespan — reveals a 4-year lifespan gap between very small and very large breeds (r = −0.47) |
| **Interactive Breed Comparison Tool** | Radar chart for comparing 2–4 breeds across 8 behavioral dimensions, powered by JavaScript + Plotly with no Shiny server required |
| **Geographic Origins** | Leaflet bubble map showing breed counts and average traits by country of origin |

------------------------------------------------------------------------

\## Data

Source: [DogTime](https://dogtime.com/) via a [Kaggle dataset](https://www.kaggle.com/code/yonkotoshiro/dogs-breed) scraped and aggregated at the breed level. Ratings use a 1–5 scale (1 = low, 5 = high) for behavioral traits. Geographic coordinates were obtained using the `tidygeocoder` R package from country-of-origin fields.

The dataset covers AKC-registered breeds plus hybrid wolf breeds and emerging breeds (e.g., Goldendoodle).

------------------------------------------------------------------------

\## Repository Structure

```         
Who_let_the_dogs_stat/
│
├── data/
│   └── dogs_breed_aggregated.csv     # Aggregated breed-level dataset
│
├── dog_breed_explorer.qmd            # Main Quarto source file
├── dog_breed_explorer.html           # Rendered standalone output
│
└── README.md
```

------------------------------------------------------------------------

\## Reproducing the Output

\### Prerequisites

R 4.x with the following packages (loaded via `pacman`):

``` r
pacman::p_load(
viridis,
leaflet,
scales,
patchwork,
crosstalk,
ggmosaic,
plotly,
htmltools,
jsonlite,
tidyverse
)
```

### Data path

Update `repo_path` at the top of `dog_breed_explorer.qmd` to point to your local `data/` directory:

``` r
repo_path <- "path/to/your/data/"
```

### Render

``` bash
quarto render dog_breed_explorer.qmd --to html
```

The output is a fully self-contained `dog_breed_explorer.html` — no server, no Shiny, no dependencies beyond the file itself.

------------------------------------------------------------------------

\## Key Findings

**Size & Lifespan Tradeoff** — Very small breeds live \~4 years longer on average than very large breeds (r = −0.47). Prospective owners face a real tradeoff between size preference and expected companionship time.

**Behavioral Signatures by Group** — Sporting breeds lead in trainability (4.1) and affection (4.8). Herding breeds score high across all dimensions (3.8–4.3). Terriers are independent and energetic but less adaptable (2.9).

**Geographic Concentration** — Europe (UK, Germany, France) remains the historical center of breed development. The US contributes 165 breeds, primarily modern mixed breeds and recent crossbreeding innovations.

**Breed Distribution** — Very Large breeds make up 53% of recognized breeds. Working and Mixed breeds dominate larger size classes; Companion breeds cluster small.

------------------------------------------------------------------------

\## Technical Notes

The interactive radar chart converts breed data to JSON and passes it through inline JavaScript using `htmlwidgets::onRender()`, enabling dynamic updates without a Shiny server. Several strategies were iterated before landing on this approach — see the AI use statement in the source file for context.

------------------------------------------------------------------------

\## Course Context

Final project for **SURV 752: Data Visualization**, University of Maryland Joint Program in Survey Methodology (JPSM), 2025. Dashboard framed as a simulated data science presentation to Nestlé Purina administrators.

------------------------------------------------------------------------

\## Author

Kevin Linares — University of Maryland / Michigan ISR
