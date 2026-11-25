<h1 align="center">Check Orientation</h1>

<p align="center">
  Reports whether a T1-weighted or diffusion-weighted NIfTI image is stored in neurological or radiological orientation, using FSL <code>fslorient</code>.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/bl.app.21"><img src="https://img.shields.io/badge/Brainlife-bl.app.21-blue.svg" alt="Run on brainlife.io"></a>
  <a href="https://github.com/brainlife/app-checkOrientation/blob/master/LICENSE"><img src="https://img.shields.io/badge/License-MIT-lightgrey.svg" alt="MIT license"></a>
</p>

> **This branch, `dtiinit`, is the brainlife.io App Check dtiInit Orientation** ([doi:10.25663/bl.app.21](https://doi.org/10.25663/bl.app.21)). The other Apps in this repository are listed under **Versions on brainlife.io** below.

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Reports the orientation (neurological or radiological) of a dtiInit-aligned DWI NIfTI image with FSL fslorient; a quality-control utility that produces no new image data.**

Reads the aligned DWI path from the dtiInit dt6.json, runs fslorient on it and writes the reported orientation (NEUROLOGICAL or RADIOLOGICAL) to product.json. It relies on a host FSL installation (no container) and legacy IU HPC environment variables, so it may not run on current resources.

| | |
|---|---|
| **Inputs** | `neuro/dtiinit` |
| **Outputs** | `raw` |
| **Resources** | 8 CPUs · 0.08 h walltime |
| **Run it** | [doi.org/10.25663/bl.app.21](https://doi.org/10.25663/bl.app.21) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `0` | `neuro/dtiinit` | yes | dtiInit output; the aligned DWI listed in dt6.json (files.alignedDwRaw) is checked. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `0` | `raw` | Placeholder output; the orientation result is reported in product.json rather than as files. |

<!-- brainlife-app:end -->

## Versions on brainlife.io

This repository hosts three quality-control Apps. They do the same check on different datatypes; none of them changes or reorients the image.

| App | Input | Branch | Run it | Status |
|---|---|---|---|---|
| Check T1 Orientation | `neuro/anat/t1w` | [`master`](https://github.com/brainlife/app-checkOrientation/tree/master) | [doi:10.25663/bl.app.19](https://doi.org/10.25663/bl.app.19) | current |
| Check DWI Orientation | `neuro/dwi` | [`master`](https://github.com/brainlife/app-checkOrientation/tree/master) | [doi:10.25663/bl.app.20](https://doi.org/10.25663/bl.app.20) | current |
| **Check dtiInit Orientation** (this branch) | `neuro/dtiinit` | [`dtiinit`](https://github.com/brainlife/app-checkOrientation/tree/dtiinit) | [doi:10.25663/bl.app.21](https://doi.org/10.25663/bl.app.21) | available |

## Running the App

### On brainlife.io

Open the App for your datatype (for example [doi.org/10.25663/bl.app.19](https://doi.org/10.25663/bl.app.19) for a T1-weighted image), choose the dataset from your project and press **Execute**. The App has no options. The orientation it finds (`NEUROLOGICAL` or `RADIOLOGICAL`) is shown on the task's results on brainlife.io; the output dataset itself is only a placeholder.

### Locally

The `master` branch (T1 and DWI Apps) needs [Singularity/Apptainer](https://apptainer.org/) and [`jq`](https://jqlang.github.io/jq/); FSL 5.0.9 is pulled from the `brainlife/fsl:5.0.9` container.

1. Clone this repository.
2. Create `config.json` with the path to the NIfTI image to check:

   ```json
   {
       "input": "testdata/t1.nii.gz"
   }
   ```

3. Run the App:

   ```bash
   ./main
   ```

The `dtiinit` branch instead reads a `dtiinit` key (a dtiInit output directory), checks the aligned DWI listed in its `dt6.json` (`files.alignedDwRaw`) and calls `fslorient` from a host FSL installation, without a container.

## Outputs

- `product.json`: the orientation reported by `fslorient`, for example `{"orientation" : "NEUROLOGICAL"}`.

No image data is written.

## Troubleshooting

- **Check dtiInit Orientation does not start**: the `dtiinit` branch relies on a host FSL installation and legacy Indiana University HPC environment variables (`ENV`, `SERVICE_DIR`) rather than a container, so it may not run on current resources. To check a DWI image, use Check DWI Orientation instead.

## Citing

> [!TIP]
> If you use this App in your work, please cite the App, the software it builds on and brainlife.io (below). GitHub's **Cite this repository** button gives the App citation in APA and BibTeX.

- Check dtiInit Orientation. brainlife.io App. [doi:10.25663/bl.app.21](https://doi.org/10.25663/bl.app.21)
- Jenkinson et al. FSL. *NeuroImage* 62:782-790 (2012). [doi:10.1016/j.neuroimage.2011.09.015](https://doi.org/10.1016/j.neuroimage.2011.09.015)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- Franco Pestilli (project director)
- Lindsey Kitchell

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io is publicly funded, and acknowledging that support helps keep it running. This App was developed with support from Wellcome, the U.S. National Institutes of Health (including the BRAIN Initiative BRAIN CONNECTS program: The Axonal Projectome EXchange, U24NS140384, and the Center for Mesoscale Connectomics, UM1NS132207) and the U.S. National Science Foundation.</sub>

## License

[MIT](https://github.com/brainlife/app-checkOrientation/blob/master/LICENSE). FSL itself is distributed under its own [license](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/Licence).
