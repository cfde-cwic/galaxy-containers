# galaxy-containers

Container images for [galaxy.cfdeworkspace.org](https://galaxy.cfdeworkspace.org).

Each image lives in its own directory.

| Image | Description |
|-------|-------------|
| [`rstudio`](rstudio/) | RStudio interactive tool with Bioconductor and additional R packages |

## rstudio

Image for the RStudio interactive tool (`interactive_tool_rstudio`). Derived from
[`afgane/bioc-galaxy:3.21`](https://hub.docker.com/r/afgane/bioc-galaxy) (source:
[afgane/bioconductor_docker](https://github.com/afgane/bioconductor_docker/tree/6490e6d2/extensions/galaxy)),
which provides RStudio Server, Bioconductor 3.21, and a set of common Bioc/CRAN packages.

Additional packages:

- [MotrpacRatTraining6moData](https://github.com/MoTrPAC/MotrpacRatTraining6moData) (`v2.1.0`)
- [MotrpacRatTraining6mo](https://github.com/MoTrPAC/MotrpacRatTraining6mo) (`v1.6.6`)

Build args:

- `MOTRPAC_DATA_REF`, `MOTRPAC_REF`: commit SHAs of the two MoTrPAC packages.
- `CRAN_SNAPSHOT`: date of the [Posit Package Manager](https://p3m.dev/) CRAN snapshot
  their CRAN dependencies are installed from. Bioconductor dependencies come from the
  base image's (frozen) Bioconductor 3.21 repos.

Published as [`ghcr.io/cfde-cwic/rstudio`](https://github.com/orgs/cfde-cwic/packages/container/package/rstudio).

### Tags

`<bioc version>-<revision>`, e.g. `3.21-1`. Bump the revision on every rebuild; never
overwrite an existing tag. When bumping the revision, consider bumping `CRAN_SNAPSHOT`;
always bump it when changing the base image.

| Tag | CRAN snapshot | Changes |
|-----|---------------|---------|
| `3.21-1` | 2026-10-08 | Initial image: adds MotrpacRatTraining6moData `v2.1.0`, MotrpacRatTraining6mo `v1.6.6` |

### Build

```bash
docker build --platform linux/amd64 -t ghcr.io/cfde-cwic/rstudio:3.21-1 rstudio/
```

### Test locally

```bash
docker run --rm -p 127.0.0.1:8787:8787 -e DISABLE_AUTH=true ghcr.io/cfde-cwic/rstudio:3.21-1
```

Open http://localhost:8787 and run:

```r
library(MotrpacRatTraining6mo)
data(TRNSCRPT_LIVER_DA)
```

### Push

```bash
docker push ghcr.io/cfde-cwic/rstudio:3.21-1
```
