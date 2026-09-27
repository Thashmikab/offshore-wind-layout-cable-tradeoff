# Offshore wind farm layout: energy vs cable length

Spreading turbines apart cuts wake losses, but every extra metre between them is inter-array cable, and cable is where most of an offshore wind farm's copper goes. These notebooks map that trade-off for a small 8-turbine array, first at Horns Rev 1 and then at Dogger Bank in the UK North Sea, using PyWake for the wake physics and NSGA-II for the two-objective search.

<!-- TODO: replace with 04_pareto_front_dogger_bank.png once uploaded to figures/ -->
![Pareto front at Dogger Bank](figures/04_pareto_front_dogger_bank.png)

At Dogger Bank, the layouts on the front range from **TODO GWh at TODO km** of inter-array cable to **TODO GWh at TODO km**, against **TODO GWh at TODO km** for a regular 4×2 grid.

This is a side project alongside my PhD at City St George's, University of London, which looks at copper and other critical materials in UK renewable energy deployment. Notebook 05 is where the two start to meet.

## Notebooks

| | Notebook | What it does | |
|---|---|---|---|
| 01 | [Wake modelling, Horns Rev 1](01_wake_modelling_horns_rev.ipynb) | Wake losses for an 8 × V80 grid, one wind direction vs the full year | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR-USERNAME/offshore-wind-layout-cable-tradeoff/blob/main/01_wake_modelling_horns_rev.ipynb) |
| 02 | [Layout optimisation, TopFarm](02_layout_optimisation_topfarm.ipynb) | Maximises AEP alone with gradient-based SLSQP | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR-USERNAME/offshore-wind-layout-cable-tradeoff/blob/main/02_layout_optimisation_topfarm.ipynb) |
| 03 | [AEP vs cable, NSGA-II](03_aep_vs_cable_nsga2.ipynb) | Two-objective search: energy against minimum-spanning-tree cable length | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR-USERNAME/offshore-wind-layout-cable-tradeoff/blob/main/03_aep_vs_cable_nsga2.ipynb) |
| 04 | [Dogger Bank](04_dogger_bank_real_site.ipynb) | Same problem with Global Wind Atlas data and 10 MW turbines | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR-USERNAME/offshore-wind-layout-cable-tradeoff/blob/main/04_dogger_bank_real_site.ipynb) |
| 05 | [Distance to shore](05_siting_distance_to_shore.ipynb) *(in progress)* | Adds distance offshore as a variable; export cable as a third objective | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR-USERNAME/offshore-wind-layout-cable-tradeoff/blob/main/05_siting_distance_to_shore.ipynb) |

Each notebook runs on its own, top to bottom, in Colab. Notebooks 03–05 take several minutes because every candidate layout is evaluated against the full wind rose.

## Modelling choices and their limits

- **Wake models:** Bastankhah & Porté-Agel (2014) for Horns Rev 1, Niayifar & Porté-Agel (2016) with 6 % turbulence intensity for Dogger Bank.
- **Turbines:** Vestas V80 (2 MW) at Horns Rev 1; DTU 10 MW reference turbine at Dogger Bank.
- **Cable length** is the minimum spanning tree between turbines. That is a lower bound: real array design is limited by how many turbines each cable string can carry, where the substation sits, and seabed routing.
- **Spacing:** at least 4 rotor diameters between any two turbines, inside a fixed rectangular lease area.
- **Wind climate at Dogger Bank** comes from the Global Wind Atlas at 54.75° N, 1.90° E, 119 m. It is downloaded on first run and cached in `data/` so results don't depend on the API afterwards.
- **Notebook 05** uses a placeholder curve for how wind speed grows with distance from the coast. Its outputs show the method working, not a result.

## What's next

1. Replace the placeholder wind-speed gradient in notebook 05 with a Global Wind Atlas transect running out from the Yorkshire coast.
2. Convert array and export cable length into copper mass, using published copper intensities for 66 kV array and 220 kV export cables.
3. Carry copper through to life cycle environmental impact, so the front becomes energy vs impact rather than energy vs kilometres.

If you work on array cable design and think the MST proxy is too crude for a question like this, I'd like to hear how you'd approach it — open an issue or get in touch.

## Running locally

```bash
pip install -r requirements.txt
jupyter lab
```

## Author

Thashmika Bandara — PhD candidate, City St George's, University of London · [LinkedIn](TODO)

Released under the MIT licence.
