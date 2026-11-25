# app-checkOrientation

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

**Reports the orientation (neurological or radiological) of a T1-weighted NIfTI image with FSL fslorient; a quality-control utility that produces no new image data.**

Runs fslorient on the T1-weighted image and writes the reported orientation (NEUROLOGICAL or RADIOLOGICAL) to product.json, shown on brainlife.io. Use it to check data before processing that assumes a particular voxel orientation. It does not change or reorient the image.

Run it on brainlife.io: [https://doi.org/10.25663/bl.app.19](https://doi.org/10.25663/bl.app.19)

| Input | Datatype | Required | Description |
|---|---|---|---|
| `0` | `neuro/anat/t1w` | yes | T1-weighted NIfTI image whose orientation is checked. |

| Output | Datatype | Description |
|---|---|---|
| `0` | `raw` | Placeholder output; the orientation result is reported in product.json rather than as files. |

Runtime: container `brainlife/fsl:5.0.9`; 8 CPUs; 0.08 h walltime.

<!-- brainlife-app:end -->

This application checks and reports the orientation (neurological or radiological) of a nifti file.
