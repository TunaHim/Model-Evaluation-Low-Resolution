# model-evaluation

Multi-model evaluation of  from the Low-Resolution Archive (LRA): three coupled storm-resolving models — **IFS-FESOM**, **IFS-NEMO**, and **ICON** — are compared against observational references (ERA5, ESA-CCI, EN4) over the historical period **1990–2014**.

Developed on the DKRZ **Levante** HPC system.

## Scientific purpose

DestinE Climate DT models run at storm-resolving resolution; their LRA output (r100, ~1° regular grid) enables systematic multi-decadal evaluation. These notebooks assess whether the three models reproduce observed climate signals consistently across independent components of the climate system:

- **2 m temperature** — warming trends and detrended variability vs. **ERA5**
- **Total cloud cover** — means, trends, and Taylor statistics vs. **ESA-CCI**
- **Ocean potential temperature** — time–depth evolution vs. **EN4**
- **Sea ice** — concentration and thickness climatologies (inter-model)
- **Surface energy closure** — a process-space diagnostic linking radiation, clouds, and turbulent fluxes

## Notebooks / workflow

| Notebook | Purpose |
|---|---|
| `comLRA_t2m.ipynb` | 2 m temperature: global-mean series, decadal trend maps vs. ERA5, detrended variability, seasonal-cycle removal, zonal means. |
| `comLRA_tcc.ipynb` | Total cloud cover: annual/multi-year means, model−ESA-CCI difference maps, Taylor diagram, 1990–2014 trends. |
| `comLRA_thetao.ipynb` | Ocean potential temperature: domain-mean time–depth (Hovmöller) anomalies for 3 models + EN4. |
| `comLRA_si.ipynb` | Sea-ice concentration & thickness: multi-year consolidation and climatological comparison maps. |
| `comLRA_SLC.ipynb` | Surface energy closure: process-space consistency of radiation, clouds, and turbulent fluxes. |

Each notebook starts with **"Why this notebook matters"** and **"Key techniques demonstrated"** sections, then is self-contained and follows the same pattern:

1. **Configure** data locations (documented placeholder variables in the config cell near the top).
2. **Load & consolidate** monthly LRA NetCDF files (1990–2014) with `xarray`.
3. **Compute** climatologies, trends (per-gridpoint linear regression), variability, or domain means.
4. **Compare** against the observational reference (regridding with `xesmf` where needed).
5. **Plot** global maps (`cartopy`), Hovmöller diagrams, Taylor diagrams, and time series.

## Example outputs

The notebooks retain their executed outputs, so representative figures can be viewed directly inside each notebook. Representative outputs include:

- 2 m temperature trends (models vs. ERA5)
- Arctic sea-ice concentration climatology (March & September)
- Total cloud cover trends (models vs. ESA-CCI)

## Required Python packages

See `environment.yml`. Core dependencies: `xarray`/`netcdf4`, `numpy`, `scipy`, `matplotlib`, `cartopy`, `xesmf` (regridding), `astropy-healpix` (HEALPix quick-look section only).

The notebooks retain their executed outputs, so **all results and figures can be browsed directly on GitHub** without installing anything.

## Expected input data

Paths are set via placeholder variables documented in each notebook's config cell:

| Placeholder | Content |
|---|---|
| `LRA_ROOT` | DestinE LRA Phase 2 archive: `climatedt-o25.1/<MODEL>/historical-*/r100/monthly/<var>_*.nc` for IFS-FESOM, IFS-NEMO, ICON |
| `EVA_DIR` | Working directory for derived NetCDF files (consolidated series, trends, variability) |
| `ERA5_DIR` | ERA5 2 m temperature (regular lat/lon, 1940–2024) |
| `ESACCI_DIR` | ESA-CCI cloud fraction record (monthly, 1982–2016) |
| `EN4_DIR` | Extracted EN4.2.2 monthly ocean analysis files |
| `FESOM_DATA_ROOT`, `MN5_DIR` | Auxiliary data used only in optional side checks |

## Data sources and access

| Data | Format | Access |
|---|---|---|
| DestinE Climate DT Low-Resolution Archive (LRA): IFS-FESOM, IFS-NEMO, ICON, historical 1990–2014, r100 (~1°) monthly | NetCDF | DKRZ Levante file system (DestinE project access); not redistributable |
| ERA5 reanalysis (2 m temperature) | NetCDF, regular lat/lon | Copernicus Climate Data Store (C3S) |
| ESA-CCI cloud fraction (1982–2016) | NetCDF | ESA Climate Change Initiative data portal |
| EN4.2.2 ocean analysis | NetCDF | UK Met Office Hadley Centre |

Paths are set once in each notebook's config cell (see *Expected input data*), so the notebooks can be pointed at another copy of the same datasets.

## Limitations

- **The input data are not included.** DestinE LRA output, ERA5, ESA-CCI, and EN4 datasets reside on DKRZ Levante and are subject to their own licences; the notebooks cannot be re-executed without access to equivalent data. Set the placeholder variables to your own copies.
- All embedded outputs and figures document the analysis as originally performed; printed paths in outputs show sanitised placeholders (e.g. `<LRA_ROOT>`).

## Notes

- The original climate datasets are not included because of their size and access restrictions.
- Absolute HPC paths have been replaced with placeholder variables for portability.
- These notebooks are provided as examples of scientific analysis workflows and are intended primarily as a software engineering and research portfolio.

## Licence

Code: MIT, see [LICENSE](LICENSE). Data: see *Data sources and access*; third-party data keep their own terms.
