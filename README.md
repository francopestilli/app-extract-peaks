[![Abcdspec-compliant](https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg)](https://github.com/brain-life/abcd-spec)
[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.172-blue.svg)](https://doi.org/10.25663/brainlife.app.172)

# app-extract-peaks

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Computes fibre orientation distributions from DWI with MRtrix3 constrained spherical deconvolution (CSD, multi-shell or 5TT) and extracts the peaks with sh2peaks, using TractSeg's code.**

Uses TractSeg's MRtrix wrapper to estimate the response function and FODs with the selected CSD type, then extracts the FOD peaks at each voxel with sh2peaks; the peaks image is the input expected by TractSeg. A brain mask is computed from the T1w with FSL bet when none is given. The T1w must be skull-stripped and aligned with the DWI; multi-shell DWI is needed for the msmt options.

| | |
|---|---|
| 📥 **Inputs** | `neuro/dwi` · `neuro/anat/t1w` · `neuro/mask` (optional) |
| 📤 **Outputs** | `neuro/peaks` |
| 🐳 **Container** | `giuliaberto/extract-peaks:1.1` |
| ⚙️ **Resources** | 16 CPUs · 10 h walltime |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.172](https://doi.org/10.25663/brainlife.app.172) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `0` | `neuro/dwi` | yes | Dwi raw data |
| `1` | `neuro/anat/t1w` | yes | T1w image. It should be aligned with the dwi data and all non-brain tissue should be removed. |
| `2` | `neuro/mask` | no | Brain mask. It should be aligned with the dwi data. If not provided, the BET algorithm will be used for brain extraction. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `neuro/peaks` | CSD peaks |

<details>
<summary><b>⚙️ Parameters</b> (1)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `csd` | enum |  | CSD type Options: `csd_msmt_5tt`, `csd_msmt`, `csd`. |

</details>

📚 **References used by this App:**
- Tournier J-D, Calamante F, Connelly A. MRtrix: Diffusion tractography in crossing fiber regions. Int J Imaging Syst Technol 22:53-66 (2012). [doi:10.1002/ima.22005](https://doi.org/10.1002/ima.22005)
- Wasserthal J, Neher P, Maier-Hein KH. TractSeg - Fast and accurate white matter tract segmentation. NeuroImage (2018). [doi:10.1016/j.neuroimage.2018.07.070](https://doi.org/10.1016/j.neuroimage.2018.07.070)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. Sci Data 6, 69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

<!-- brainlife-app:end -->

This App extracts the peaks of a spherical harmonic function at each voxel using the MRtrix command `sh2peaks`. This code is part of the TractSeg package developed by (Wasserthal et al., 2018), under Apache-2.0 License: https://github.com/MIC-DKFZ/TractSeg.

### Authors
- [Giulia Bertò](giulia.berto.4@gmail.com)

### Funding Acknowledgement
brainlife.io is publicly funded and for the sustainability of the project it is helpful to Acknowledge the use of the platform. We kindly ask that you acknowledge the funding below in your publications and code reusing this code.

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)

### Citations
We kindly ask that you cite the following articles when publishing papers and code using this code. 

* Tournier, J.‐D., Calamante, F. and Connelly, A. (2012), MRtrix: Diffusion tractography in crossing fiber regions. Int. J. Imaging Syst. Technol., 22: 53-66. https://doi.org/10.1002/ima.22005

* [TractSeg - Fast and accurate white matter tract segmentation](https://doi.org/10.1016/j.neuroimage.2018.07.070) ([free arxiv version](https://arxiv.org/abs/1805.07103))
[NeuroImage 2018]

* Avesani, P., McPherson, B., Hayashi, S. et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. Sci Data 6, 69 (2019). [https://doi.org/10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y) 

### Running the App
### On [Brainlife.io](http://brainlife.io/) 
You can submit this App online at https://doi.org/10.25663/brainlife.app.172 via the “Execute” tab.

Inputs: \
Mandatory inputs are (i) the dwi data (multi-shell and not nomalized) and (ii) the T1 anatomical image. Optionally, you can provide also the brain mask (if not provided, it will be computed using the BET command from FSL).

Output: \
The CSD peaks.

### Running Locally (on your machine)

1. git clone this repo.
2. Inside the cloned directory, create `config.json` with something like the following content with paths to your input files.

```json
{
        "dwi": "./input/dwi/dwi.nii.gz",
	"bvecs": "./input/bvecs/dwi.bvecs",
	"bvals": "./input/bvals/dwi.bvals",
	"t1": "./input/t1.nii.gz",
	"mask": "./input/mask.nii.gz",
	"csd": "csd_msmt_5tt"
}
```

3. Launch the App by executing `main`

```bash
./main
```

### Output
The main output of this App is a file called `peaks.nii.gz`, which is a 4D nifti image containing the peaks of a spherical harmonic function at each voxel (from sh2peaks).

### Dependencies
This App only requires [singularity](https://sylabs.io/singularity/) to run. 

#### MIT Copyright (c) 2020 Bruno Kessler Foundation (FBK)
