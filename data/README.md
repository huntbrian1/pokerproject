# Data Folder

Raw PHH/PHHS data is intentionally not included in this GitHub-ready folder.

The local project data is over 16 GB, mostly from HandHQ `.phhs` multi-hand container files. Uploading the raw dataset directly to GitHub is not recommended.

Data source:

- Kim, Juho. **A Dataset of Poker Hand Histories**. Zenodo. Version **v2**. DOI: `10.5281/zenodo.13997158`
- Source URL: https://zenodo.org/records/13997158

Important: this project references the Zenodo **v2** record, not v3. The Zenodo page notes that a newer version exists, but the analysis and local file inventory were built from the v2 dataset.

To rerun the notebook, place the source data here:

```text
data/
|-- pluribus/
|-- wsop/
|-- handhq/
|-- alice-carol-wikipedia.phh
|-- antonius-blom-2009.phh
|-- arieh-yockey-2019.phh
|-- dwan-ivey-2009.phh
`-- phua-xuan-2019.phh
```

The notebook uses single-hand `.phh` files for the main analysis. `.phhs` files are audited as multi-hand containers readable with `HandHistory.load_all()`, but are excluded from the main hand-level analysis to avoid mixing incompatible units of observation.
