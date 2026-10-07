# The Grand Canonical Ensemble, Interactively

An interactive, single-page web demo of the grand canonical ensemble from statistical mechanics: a small system that exchanges both energy and particles with a large reservoir at fixed temperature *T* and chemical potential *μ*.

Created by **Claude Opus 5.5**, based on the lecture notes by **Sang Hoon Lee** (Chapter 7, Quantum Statistics; Section 7.1, the Gibbs factor, with Problems 7.6 and 7.7).

## What's inside

The page follows the lecture notes section by section.

**Particles come and go.** A live ideal gas simulation. Particles move between a reservoir and an open "system" region, and the demo counts them to build a histogram of *N* in real time, overlaid with the Poisson prediction. Sliders control the system size and the animation speed. The measured standard deviation converges to √N̄.

- **Particle types.** You can add up to four non-interacting particle types (A to D), each with its own color, chemical potential, and mass, and remove them again. Particles inside the system are drawn solid and those in the reservoir faded, and the system label shows a separate count for each type.
- **Absolute chemical potential.** *μ* is given in units of k<sub>B</sub>T from the ideal gas relation *μ* = k<sub>B</sub>T ln(*n v<sub>Q</sub>*). A dilute gas has *n v<sub>Q</sub>* ≪ 1, so *μ* is negative; the slider runs from −15 to −9.5 k<sub>B</sub>T. Because *v<sub>Q</sub>* ∝ *m*<sup>−3/2</sup>, the density at fixed *μ* goes as *n* ∝ *m*<sup>3/2</sup> e<sup>*μ*/k<sub>B</sub>T</sup>, so a heavier type is denser as well as slower.
- **Histogram views.** With more than one type, **Side by side** shows each type's measured histogram next to its own Poisson curve, in the type's color, with a per-type table of predicted N̄, measured N̄, σ<sub>N</sub>, and √N̄. You can also view a single type, or **Total N**, which is again Poisson with a mean equal to the sum of the individual means.

**The Gibbs factor.** A short derivation, from the ratio of reservoir multiplicities to the Gibbs factor

```
P(s) = (1/𝒵) exp(−[E(s) − μN(s)] / k_B T),    𝒵 = Σ_s exp(−[E(s) − μN(s)] / k_B T)
```

**Why carbon monoxide wins.** The lecture's single heme-site model of hemoglobin, with three states (empty, O₂ bound, CO bound). You can adjust temperature, the O₂ chemical potential, both binding energies, and how much rarer CO is than O₂. Two presets reproduce the lecture's numbers:

| Scenario | Gibbs factors | O₂ occupancy |
| --- | --- | --- |
| O₂ only, *T* = 310 K, *μ* = −0.6 eV, *ε* = −0.7 eV | 1 + ~40 | ~98% |
| CO at 1/100 of O₂, *ε′* = −0.85 eV | 1 + ~40 + ~120 | ~25% |

The result is compared against a standard oxygen-saturation reference table, and a timeline shows one site hopping between states over time.

**How big are the fluctuations?** Problem 7.6: the derivation of

```
σ_N = sqrt( k_B T ∂N̄/∂μ )
```

and its ideal gas consequence σ_N = √N̄. A log slider runs N̄ from 1 to 10²⁴ to show the relative fluctuation 1/√N̄ vanishing for macroscopic systems. A live check confirms the formula also holds for the two-state heme site, where σ² = p − p².

**The grand free energy.** Problem 7.7: Φ = −k<sub>B</sub>T ln 𝒵. The page plots Φ(μ) for the heme site with a movable tangent line, so you can verify that −∂Φ/∂μ equals N̄ computed from the Gibbs sum.

## Running it

There is nothing to build or install. The whole demo is one self-contained file, `index.html`, with all CSS and JavaScript inline.

Open it locally by double-clicking `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Publishing with GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your main branch and the `/ (root)` folder, then save.
4. After a minute or so, the demo will be live at `https://<your-username>.github.io/<repository-name>/`.

## Technical notes

- Plain HTML, CSS, and vanilla JavaScript drawn on `<canvas>`. No frameworks, no build step.
- Equations are typeset with [MathJax 3](https://www.mathjax.org/) (SVG output, loaded from cdnjs), so they need no extra web fonts.
- The only other external resources are the Newsreader and Instrument Sans fonts from Google Fonts, with system font fallbacks if they fail to load.
- Opening the page requires an internet connection for MathJax; offline, the equations appear as raw TeX.
- Supports light and dark mode via `prefers-color-scheme`, and honors `prefers-reduced-motion` (animations start paused).
- Responsive down to phone widths.
- Boltzmann constant used: k<sub>B</sub> = 8.617 × 10⁻⁵ eV/K.
- In the particle simulation, the box is scaled so that a type of mass *m*<sub>0</sub> at *μ* = −12 k<sub>B</sub>T has 44 particles in the reservoir. To keep the animation smooth, each type is capped at 1,500 particles, and the top of its *μ* slider moves down as its mass goes up so the cap is never reached.

## Caveats

- The hemoglobin model is the lecture's illustrative one-site model. Real hemoglobin has four cooperatively binding sites.
- Ordinary two-wavelength pulse oximeters, including smartwatches, cannot distinguish CO-bound from O₂-bound hemoglobin, so they can read near normal during CO poisoning. The saturation table is for context only, not medical guidance.

## Credits

- Demo: Claude Opus 5.5
- Physics content and examples: lecture notes by Sang Hoon Lee
- Problems 7.6 and 7.7 are from Daniel V. Schroeder, *An Introduction to Thermal Physics*, as used in the lecture notes.

## License

No license has been chosen yet. Add a `LICENSE` file (for example, MIT or CC BY 4.0) before sharing or reusing this project publicly, and confirm that any use of the lecture material is permitted by its author.
