# Smallwood / Nelson fire-spread simulations

This repository contains prepared fire-spread scenarios, completed simulation
results, and interactive maps for the Smallwood and Nelson area of British
Columbia. The work compares ignition patterns and weather assumptions using
30 m Canadian Forest Fire Behaviour Prediction (FBP) fuel data.

## Open the interactive maps

| Scenario | Ignitions | Weather | Interactive map |
|---|---:|---|---|
| Named main streams | 500 m grid | 24 h P90 weather | [Open map](https://arkenmap-com.github.io/smallwood-fire-sim/runs/aoi-30m-mrdem-fuel30-named-mainstreams-24h-p90-500m-grid/web-map/) |
| Named main streams | Single centre | 24 h P90 weather | [Open map](https://arkenmap-com.github.io/smallwood-fire-sim/runs/aoi-30m-mrdem-fuel30-named-mainstreams-24h-p90-single-center/web-map/) |
| Falls Creek tributary | 1,000 m grid, 257 points | Wind fixed at 355° | [Open map](https://arkenmap-com.github.io/smallwood-fire-sim/syncrosim/package1/aoi-30m-mrdem-fuel30-p90-24h-1000m-falls-tributary-wind355/web-map/) |
| Falls Creek tributary | 1,000 m grid, 257 points | Observed prevailing wind | [Open map](https://arkenmap-com.github.io/smallwood-fire-sim/syncrosim/package1/aoi-30m-mrdem-fuel30-p90-24h-1000m-falls-tributary/web-map/) |

The maps include fuel and conditional burn-frequency layers. Use the layer
control in each map to compare the available data.

## Standalone SyncroSim run data

The input data for the fixed 355° wind scenario is also available in a focused,
private repository:

**[smallwood-syncrosim-wind355](https://github.com/arkenmap-com/smallwood-syncrosim-wind355)**

That repository contains the aligned terrain and fuel rasters, AOI, weather,
ignitions, FBP lookup table, companion Cell2Fire inputs, configuration,
provenance manifest, and SHA-256 checksums. It is the best starting point for
transferring one scenario into an existing SyncroSim fire-model package.

## Study setup

- **Location:** Nelson / Smallwood area, British Columbia
- **Coordinate system:** NAD83 / BC Albers (`EPSG:3005`)
- **Cell size:** 30 m
- **Grid dimensions for the packaged run:** 712 columns by 736 rows
- **Fuel:** NRCan Canadian FBP fuel classes
- **Topography:** MRDEM elevation with aligned slope and aspect
- **Hydrography:** selected Freshwater Atlas features represented as
  water/non-fuel code `102`
- **Weather station:** Smallwood station 404
- **Weather period:** 24 hourly observations for 20 August 2018
- **Weather selection:** observed day nearest the June–August 2016–2025 daily
  noon FWI 90th percentile

The fixed-wind scenario overrides hourly wind direction to 355° from north.
The companion scenario retains the observed wind sequence.

## What the results mean

These maps show **conditional burn frequency** across an ignition ensemble.
For the packaged 1,000 m experiment, each of 257 ignition points was simulated
under the same fixed 24-hour weather sequence. A value represents the fraction
of those runs in which a cell burned.

The results are not:

- annual burn probability;
- a calibrated estimate of wildfire likelihood;
- a current wildfire perimeter;
- an operational forecast; or
- a replacement for agency fire-behaviour analysis.

They are intended for scenario comparison, workflow development, and spatial
exploration under explicitly defined assumptions.

## Repository layout

```text
runs/
  .../outputs/        Aggregated burn-count and burn-frequency products
  .../web-map/        GitHub Pages-ready Leaflet maps and tiles

syncrosim/package1/
  .../inputs/         Fuel, terrain, weather, AOI, and ignition inputs
  .../cell2fire/      Companion Cell2Fire-formatted input files
  .../outputs/        Completed aggregate results
  .../web-map/        Interactive map for the packaged scenario
  ...-package1.zip    Downloadable scenario data bundles
```

## Software and reproducibility

The repository stores scenario data and selected results; it does not bundle
the SyncroSim, Cell2Fire, or Burn-P3+ applications. The folders under
`syncrosim/package1/` are data bundles rather than native `.ssim` libraries.
To rerun a scenario, install the relevant simulator and model package, then
validate the input mapping against that package's schema and version.

For a compact, checksummed data handoff, use the standalone
[wind-355 SyncroSim repository](https://github.com/arkenmap-com/smallwood-syncrosim-wind355).

## Data notes

Fuel, elevation, slope, aspect, ignition, and weather inputs are aligned to the
scenario grid. Freshwater Atlas lakes, named main streams, and the selected
Falls Creek tributary were applied to the fuel surface as non-burnable water
cells. Provenance and run summaries are recorded in the JSON manifests within
each packaged scenario.
