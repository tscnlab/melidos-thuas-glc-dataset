# MeLiDos THUAS GLC Data Package

This repository contains data from the The Hague University of Applied Sciences
(THUAS) site of the MeLiDos field study, refactored as a GLC Schema 3.0.2 data
package. The source dataset is [Aerts et al. (2025)](https://github.com/MeLiDosProject/AertsEtAl_Dataset_2025),
archived at [Zenodo](https://doi.org/10.5281/zenodo.17979893).

The source study enrolled 20 participants. This package contains the 15
participants included in the source dataset's analysis-ready imported data.

## Source processing represented in this package

- Sensor streams were restricted to their documented trial intervals and gaps
  were expanded during upstream import.
- ActLumus streams were regularized to 10-second intervals. `EVENT` was audited
  in all packaged sensor files and is represented as an integer variable.
- Duplicate wrist timestamps for `THUAS_S014` were aggregated after an irregular
  recording start, following the source import script.
- The `THUAS_S015` chest device clock had reset after an empty battery. The
  source import corrected its timestamps by 25 years, 6 months, 5 days,
  12 hours, and 32 minutes using the participant's wrist and head streams as
  temporal references.
- The source correction log documents 41 sleep-diary corrections across 13
  files, including date, AM/PM, swapped-field, and mistyped-time corrections.
- The chronotype import sets `alarm_f` to `FALSE`. The source notes that
  participants who used an alarm on free days should be excluded from formal
  MCTQ analyses; users should account for this in downstream analysis.
- Wrist data are unavailable for `THUAS_S001` and `THUAS_S002`; light-glasses
  data are unavailable for `THUAS_S019` and `THUAS_S020`.

## Calibration-date provenance

Actual device-specific calibration records were not supplied. For devices with
a documented delivery month, `2024-06-01` is used as a provisional proxy. For
the remaining devices, the earliest deployment date documented in
`Study_dates_MeLiDos_THUAS.xlsx` is used. These dates must not be interpreted as
confirmed calibration dates and should be checked against the original records.

## Validation

The package targets GLC Schema 3.0.2 and includes a GitHub Actions workflow for
GLC Validator 0.5.2. The refactoring scripts and their site-specific provenance
mapping are retained in the source repository under `glc_validation/`.
