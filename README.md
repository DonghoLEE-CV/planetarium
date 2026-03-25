# Planetarium

> A 3D interactive virtual planetarium built with Unreal Engine 4 — experience constellations anytime, free from light pollution, dust, and weather.

---

## Background

In modern cities, the night sky has become nearly invisible.

Excessive artificial lighting (light pollution), fine dust (PM2.5), rain, and overcast weather prevent urban residents from observing stars in their daily lives. Traditional star-gazing requires escaping to remote areas and waiting for clear weather — an increasingly rare opportunity.

This project was created to answer a simple question: **what if anyone could explore the night sky, anytime, from anywhere?**

---

## Project Overview

**Planetarium** is a real-time 3D virtual environment developed in Unreal Engine 4 that recreates a scientifically accurate night sky. Users can freely navigate a first-person 3D space and explore constellations rendered at correct relative distances using actual stellar distance data.

| Item | Details |
|------|---------|
| Engine | Unreal Engine 4.27 |
| Perspective | First-person 3D navigation |
| Season implemented | Spring (1 season out of 4) |
| Constellations | 12 (3 per cardinal direction) |
| Directions | East / West / South / North |
| Star scaling | Based on real stellar distance data |

> The full 4-season implementation was scoped out due to time constraints. The current build covers spring with 12 constellations across 4 cardinal directions.

---

## Key Features

### Scientifically Scaled 3D Space

Stars are not placed arbitrarily — their positions in 3D space are derived from real astronomical distance data (in light-years/parsecs), then scaled proportionally to fit the virtual environment. This preserves the relative depth relationships between stars within each constellation.

### 12 Constellations, 4 Directions

Spring constellations are organized by the direction you face:

| Direction | Constellations |
|-----------|---------------|
| East | 3 constellations |
| West | 3 constellations |
| South | 3 constellations |
| North | 3 constellations |

Each constellation is navigable — users can fly toward individual stars and observe the 3D structure that is completely invisible from Earth's 2D perspective.

### Interactive Dashboard

An in-world UI dashboard (built with UMG Widget Blueprints) provides:
- Constellation name and mythology background
- Star names within the selected constellation
- Real distance and magnitude data per star

### Accessibility — Always On

Unlike real-world observation, this planetarium is:
- **Weather-independent** — no clouds, no rain, no fine dust
- **Light pollution-free** — every star is fully visible regardless of urban brightness
- **Time-independent** — explore any sky configuration at any hour

---

## System Architecture

```
planetarium/
├── Content/
│   ├── FirstPersonBP/
│   │   ├── Blueprints/          # Game logic (FirstPersonGameMode, HUD)
│   │   ├── Maps/                # Main scene (FirstPersonExampleMap)
│   │   └── Widget/              # UI components
│   │       ├── ConstellationWidget_BP   # Constellation info panel
│   │       ├── Constellation_BP         # Constellation data asset
│   │       ├── DashboardWidget_BP       # Main HUD dashboard
│   │       └── Dashboard_BP             # Dashboard controller
│   ├── FirstPerson/             # Character mesh, animations, textures
│   └── FPWeapon/                # First-person interaction assets
├── Config/                      # Engine and project configuration
├── Source/                      # C++ source (FirstPerson character)
└── planetarium.uproject
```

---

## Technical Implementation

### Star Position Calculation

Real stellar coordinates (Right Ascension, Declination, Distance) are converted to Cartesian (x, y, z) coordinates using standard spherical-to-Cartesian formulas, then scaled to fit within the UE4 scene bounds while preserving inter-star proportions:

```
x = d * cos(dec) * cos(ra)
y = d * cos(dec) * sin(ra)
z = d * sin(dec)
```

Where `d` = scaled distance, `ra` = right ascension (radians), `dec` = declination (radians).

### Blueprint Architecture

The project uses Unreal Engine's Blueprint visual scripting system:

- **Constellation_BP** — stores per-constellation data (star positions, names, distances)
- **ConstellationWidget_BP** — renders the information overlay when a constellation is selected
- **DashboardWidget_BP** — provides the main navigation HUD
- **FirstPersonGameMode** — manages game state and constellation switching

---

## How to Run

**Requirements:** Unreal Engine 4.27, Windows 10/11 64-bit

1. Clone this repository
2. Double-click `planetarium.uproject` to open in UE4
3. Press **Play** in the editor (or package for standalone)
4. Use **WASD + mouse** to navigate the 3D space
5. Approach a constellation to trigger the information panel

> **Note:** Large content packs (StarterContent, PN_GrassLibrary) are excluded from this repository to reduce size. You may need to add StarterContent via the UE4 content browser if prompted on first launch.

---

## Development

| Item | Details |
|------|---------|
| Developer | Dongho Lee |
| Institution | Dong-A University, ISPL (Image Signal Processing Lab) |
| Project type | Undergraduate capstone project |
| Development period | 2022 |
| Report | `report_Planetarium.pdf` (see repository) |

---

## Limitations & Future Work

The current implementation covers spring only. Extending to the full 4-season set is the most natural next step — each season would add 12 more constellations following the same data pipeline.

Additional improvements worth pursuing:

- Physically-based star brightness: scale emissive material intensity by apparent magnitude
- VR headset mode via OpenXR (the first-person architecture is already well-suited for direct adaptation)
- Atmospheric scattering to simulate twilight and dawn sky transitions
- Constellation line-drawing with animated tracing for educational mode

---

## License

This project is for academic and portfolio purposes. Unreal Engine assets are subject to Epic Games' EULA. Stellar coordinate data is derived from publicly available astronomical catalogs (Hipparcos, Yale Bright Star Catalogue).

---

<div align="center">
  <sub>Developed by <a href="https://github.com/LeeDongho-ISPL">Dongho Lee @ Dong-A University ISPL</a></sub>
</div>
