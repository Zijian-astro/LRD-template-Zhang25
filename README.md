# LRD-template-Zhang25
<img width="764" height="305" alt="Screenshot 2025-12-05 at 09 37 47" src="https://github.com/user-attachments/assets/8a33c260-74ea-496d-961c-ee52f9512b96" />

<img width="1399" height="444" alt="Screenshot 2025-12-05 at 15 51 42" src="https://github.com/user-attachments/assets/30b5c784-ea7e-4344-96e1-0aca9af3c59f" />


Empirical template library for Little Red Dots (LRDs) constructed from JWST/NIRSpec prism spectra of 44 spectroscopically confirmed LRDs at z ≈ 2.3–7.
See details in Zhang+2025: https://arxiv.org/abs/2512.05180v1
These templates are designed for use with photometric-redshift fitting codes such as EAZY, and provide coverage of the observed diversity in LRD UV–optical continua.

This repository contains:

  •	LRD_template_12grid/ — LRD templates binned in the (β_UV, β_opt) plane with 12 grids
  
  •	LRD_template_4grid/ — LRD templates binned in the (β_UV, β_opt) plane with 4 grids

  •	Hainline24+LRD/ — LRD templates with 4 grids plus the template from Hainline et al. (2024)

⸻

🔍 Overview

LRDs are a recently identified population with extreme compactness and red UV–optical colors and are not represented in standard photometric-redshift template libraries.
Using conventional templates can lead to biased photometric redshift (z_ph) estimates.
To address this issue, we construct a template library based on real LRD spectra from JWST/NIRSpec.

This library is intended to improve robustness and accuracy of z_ph estimates for photometrically selected LRDs.

⸻

📦 Data sources

The 44 LRDs included in this library are mainly drawn from:
	•	RUBIES (de Graaff et al. 2025)
	•	UNCOVER (Bezanson et al. 2024)
	•	JADES (Eisenstein et al. 2023)

and also include several well-studied LRDs from:
	•	Furtak et al. 2023
	•	Wang et al. 2024b
	•	de Graaff et al. 2025
	•	Naidu et al. 2025

Their NIRSpec prism spectra are retrieved from the DAWN JWST Archive (DJA) using version 4 public datasets, reduced with msaexp and the official JWST Calibration Pipeline.


⸻

🛠️ Template construction

1. Preprocessing
	•	All spectra are shifted to the rest frame
	•	Re-sampled onto a common logarithmic wavelength grid: 0.7–2.5 μm
	•	Normalized at 5500 Å
	•	Pixels with S/N < 3 blueward of the Lyman limit (912 Å) are masked

2. Global composite

A global full-sample composite is constructed using:
	•	3σ sigma-clipped median
	•	Mild boxcar smoothing below 1216 Å
	•	Provides robust far-UV behavior

3. Color-binned subsamples (12-grid templates)

To capture continuum diversity, spectra are divided on the
(β_UV, β_opt) plane:
	•	β_UV bins: [-2.0, –1.0]
	•	β_opt bins: [-0.65, 0, 0.5, 1.4]

→ 12 subsamples, each containing 2–7 LRDs.

Each bin is stacked using the same procedure as the global composite.

4. UV patching

Because many spectra lack clean far-UV coverage:
	•	Pixels below 2000 Å with S/N < 1
or missing data
→ replaced with the full-sample template
	•	Scaled to match median flux around 2500 Å

This ensures smooth Lyman-break behavior without altering continuum slopes.


⸻

📦 Using the templates in EAZY

Add the template files to your EAZY templates/ directory and include them in your templates.param:

TEMPLATES_FILE LRD_template_12grid/*.spec

Or mix with default EAZY templates:

TEMPLATES_FILE  eazy_v1.3.spectra.param
TEMPLATES_FILE  LRD_template_12grid/*.spec


⸻

📜 Citation

If you use this template library, please cite:

Zhang et al. 2025.


⸻

📮 Contact

For questions or issues:
Zijian Zhang — zjz.kiaa@stu.pku.edu.cn
