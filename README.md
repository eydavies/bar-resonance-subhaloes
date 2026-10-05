# The erasure of Galactic bar resonances by dark matter subhaloes

Code, cached data and figures for Davies, Dillamore, Belokurov & Necib, *The erasure of Galactic bar resonances by dark matter subhaloes* (MNRAS, submitted).

Stars trapped in resonance with the Galactic bar occupy a finite width in action space. Encounters with dark matter subhaloes change a star's slow action, and can move it beyond the separatrix so that it leaves the resonance. The notebooks here:

* model a single encounter in the impulse approximation, and test it against test-particle orbit integrations;
* calibrate the kick needed to eject a star from the co-rotation resonance;
* treat the subhalo population as a diffusion process in the slow action, and turn the survival of resonances into a constraint on the subhalo population.

## Layout

```
notebook/   Jupyter notebooks (run them from this folder; paths to the others start with ../)
data/       cached results that the notebooks load instead of recomputing
figures/    the figures of the paper (PDF)
```

## Notebooks

| Notebook | Contents | Paper |
|---|---|---|
| `analytic_model.ipynb` | Pendulum model of the resonance, and the analytic single-encounter kick. | Fig. 1 |
| `simulation_model.ipynb` | Test-particle set-up (Agama, Ferrers bar): a star in co-rotation resonance, and early single-encounter experiments. | Fig. 3 |
| `single_encounter_figures.ipynb` | Test-particle integrations (Agama) of single subhalo encounters with a star in co-rotation resonance. | Figs 7, 8 |
| `ejection_calibration.ipynb` | About $10^4$ simulated encounters ($M=10^5$–$10^{10}\,{\rm M_\odot}$, $r_s/r_s^{\rm CDM}=0.01$–$2$, $b/r_s=10^{-2}$–$10^{2}$). Compares the analytic kick with the simulated one, and calibrates the ejection threshold. | Figs 5, 6; tables of Sec. 3.3 |
| `diffusion_version2.ipynb` | Diffusion coefficient $D_{II}$ and diffusion timescale for CDM and WDM subhalo populations, with the kick measured from a fixed galactic centre. | Figs 9, 10, 11, A1 |
| `diffusion_version2_tidal.ipynb` | As above, with the kick taken relative to the host mass enclosed by the orbit (differential force). | relative-kick versions of Figs 10, 11; `dD_dlogM.pdf` |
| `diffusion_version2_tidal_aniso.ipynb` | As above, with the anisotropic (Fisher) distribution of encounter directions in the relative kick. | |
| `diffusion_constraint_pre_tidal.ipynb` | Suppression of the local subhalo density needed for the resonance to survive, fixed-centre kick. | Fig. 12 |
| `diffusion_constraint.ipynb` | As above, with the relative kick and anisotropic encounter directions. | |

## Figures

| File | Paper | Made by |
|---|---|---|
| `separatrix.pdf` | Fig. 1 | `analytic_model` |
| `resonance_potential.pdf` | Fig. 3 | `simulation_model`\* |
| `impulse_accuracy.pdf` | Fig. 5 | `ejection_calibration` |
| `ejection_threshold.pdf` | Fig. 6 | `ejection_calibration` |
| `subhalo_flyby_xz.pdf` | Fig. 7 | `single_encounter_figures` |
| `orbit_examples.pdf` | Fig. 8 | `single_encounter_figures` |
| `dark_matter_properties.pdf` | Fig. 9 | `diffusion_version2`\* |
| `diffusion_results.pdf` | Fig. 10 | `diffusion_version2`\* (saved as `diffusion_results_m10.pdf`) |
| `timescale_results.pdf` | Fig. 11 | `diffusion_version2`\* (saved as `timescale_results_m10.pdf`) |
| `suppression_constraints.pdf` | Fig. 12 | `diffusion_constraint_pre_tidal`\* |
| `subhalo_type_compare.pdf` | Fig. A1 | `diffusion_version2`\* |
| `diffusion_results_tidal.pdf` | Fig. 10, relative kick | `diffusion_version2_tidal`\* |
| `timescale_results_tidal.pdf` | Fig. 11, relative kick | `diffusion_version2_tidal` |
| `dD_dlogM.pdf` | contribution of each mass decade to $D_{II}$ | `diffusion_version2_tidal` |

\* The `plt.savefig` line for this figure is commented out. Uncomment it to write the figure.

Figs 2, 4 and 13 are schematic diagrams, and are not made by this code.

## Running

Create the environment and start Jupyter from `notebook/`:

```bash
conda env create -f environment.yml
conda activate resonance_subhalo
cd notebook && jupyter lab
```

Every notebook runs in under a minute with the cached data in `data/`. The exception is `simulation_model.ipynb`: run it in order up to the Fig. 3 cell. Its later, exploratory cells depend on the order in which they were first run.

Notes on the cached data:

* **`ejection_calibration.ipynb`** loads the saved sweeps. Set `RERUN = True` (main sweep) or `RERUN_LARGEB = True` (large impact parameter sweep) to run them again. A saved sweep is only loaded if it was made with the settings at the top of the notebook; otherwise the sweep is re-run. Set `SAVE_TABLES = True` to write the LaTeX tables to `../tables/`.
* **The diffusion notebooks** load the geometric factors $\mathcal B(M)$ (`tidal_B_*.npz`) and the per-direction kernels (`tidalS_*.npz`). A missing file is recomputed and saved.

Figure text uses LaTeX if a `latex` executable is on the `PATH`, and matplotlib's mathtext otherwise.

The results were produced with Python 3.8, NumPy 1.24, SciPy 1.10, Matplotlib 3.7, scikit-learn 1.3 and [Agama](https://github.com/GalacticDynamics-Oxford/Agama) 1.0. Agama is installed with pip (`environment.yml` does this), which compiles it and needs a C++ compiler; see the Agama documentation if the build fails.

## Licence

MIT; see `LICENSE`.
