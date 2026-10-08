# RStudio GxIT image (Bioconductor 3.21) for galaxy.cfdeworkspace.org.
#
# Base image source: https://github.com/afgane/bioconductor_docker/tree/6490e6d2/extensions/galaxy
FROM afgane/bioc-galaxy:3.21@sha256:5586934ac05517e91753e51c3e2799f7ad6d6263d426e6afe134233449cb7116

# Dated Posit Package Manager snapshot for CRAN dependencies.
ARG CRAN_SNAPSHOT=2026-10-08
# MotrpacRatTraining6moData v2.1.0
ARG MOTRPAC_DATA_REF=f831a4fe421ec11687640452484a8247137aa74a
# MotrpacRatTraining6mo v1.6.6
ARG MOTRPAC_REF=bea2ab1120c0bc0a4f4aa9602e93ecf5685e54fb

# MoTrPAC rat endurance training packages. The data package must be installed
# first. Its install step that moves datasets into the lazyload DB takes
# several minutes.
RUN Rscript -e 'options(Ncpus = parallel::detectCores(), \
                repos = c(CRAN = "https://p3m.dev/cran/__linux__/noble/'"${CRAN_SNAPSHOT}"'")); \
        remotes::install_github("MoTrPAC/MotrpacRatTraining6moData@'"${MOTRPAC_DATA_REF}"'", upgrade = "never"); \
        remotes::install_github("MoTrPAC/MotrpacRatTraining6mo@'"${MOTRPAC_REF}"'", upgrade = "never"); \
        library(MotrpacRatTraining6moData); \
        library(MotrpacRatTraining6mo)' && \
    rm -rf /tmp/*
