<h1 align="center">ANTsRegistration</h1>

<p align="center">
  Registers a skull-stripped T1-weighted image to the MNI152 1 mm template with an ANTs SyN warp and outputs the registered T1w and the warp and affine files.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.581"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.581-blue.svg" alt="Run on brainlife.io"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Registers a skull-stripped T1-weighted image to the MNI152 1 mm template with an ANTs SyN warp and outputs the registered T1w and the warp and affine files.**

Runs ANTS (cross-correlation metric, SyN) from the T1w to the bundled masked MNI152 1 mm template, with the iteration schedule set by intense (false: 100x100x50, true: 100x100x100x25, test: 1x1x1), then applies the warp and affine with WarpImageMultiTransform. The input should already be skull-stripped. optional_params is read but not used.

| | |
|---|---|
| **Inputs** | `neuro/anat/t1w` |
| **Outputs** | `neuro/anat/t1w` · `neuro/transform/nifti` |
| **Container** | `brainlife/ants:2.2.0-1bc` |
| **Resources** | 2 GB memory · 5 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.581](https://doi.org/10.25663/brainlife.app.581) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `skullstripped_nifti` | `neuro/anat/t1w` | yes | t1w to be registered to template space |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `registered` | `neuro/anat/t1w` | t1w registered to template space |
| `output` | `neuro/transform/nifti` | warp files |

<details>
<summary><b>Parameters</b> (3)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `template` | string | `template/mni_t1_template_masked.nii.gz` | currently the only option is mni 1 mm with a dilated mask |
| `optional_params` | string | `null` | currently no optional parameters at this time |
| `intense` | string | `false` | you must enter one of the following values: true, false, test. true = more intense; iterates 100x100x100x25 false = less intense; iterates 100x100x50 test = for testing only; iterates 1x1x1 |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.581](https://doi.org/10.25663/brainlife.app.581), choose `neuro/anat/t1w` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/anat/t1w`, `neuro/transform/nifti`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/ants:2.2.0-1bc`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "t1": "/path/to/skullstripped_nifti/t1",
       "template": "template/mni_t1_template_masked.nii.gz",
       "optional_params": "null",
       "intense": "false"
   }
   ```

3. Run `./main`.

## Troubleshooting

- **you must choose a value for intense: true, false, test**: Set intense to true, false or test.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- ANTsRegistration. brainlife.io App. [doi:10.25663/brainlife.app.581](https://doi.org/10.25663/brainlife.app.581)
- Avants et al. A reproducible evaluation of ANTs similarity metric performance in brain image registration. *NeuroImage* 54:2033-2044 (2011). [doi:10.1016/j.neuroimage.2010.09.025](https://doi.org/10.1016/j.neuroimage.2010.09.025)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

Maintained by [@vnbcs](https://github.com/vnbcs).
