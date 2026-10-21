# Capillary effects on the self-similar growth of immiscible Rayleigh–Taylor mixing: data and figures

Data and code for

> M. D. Walker and S. S. Nixon,
> *Capillary effects on the self-similar growth of immiscible Rayleigh–Taylor mixing*, submitted to *Journal of Fluid Mechanics* (Rapids).

The notebook `make_figures.ipynb` reproduces every figure of the paper, the figures of its supplementary material that
are computed from the simulations, table S3 of the supplementary material, and the fits and statistics quoted in the
text, from the curves in `data/`.

The simulations were presented at the 78th Annual Meeting of the APS Division of Fluid Dynamics
([abstract](https://meetings-archive.aps.org/dfd/2025/u30/8/), [talk](https://drive.google.com/file/d/1jgFE_YQC5uhCAsLqNTcmoPDsvbyvzH8O/view?usp=sharing))
and at the 19th International Workshop on the Physics of Compressible Turbulent Mixing
([abstract](https://drive.google.com/file/d/16irNsqovxGmB08cWheF4SVbzx0tQUwVy/view?usp=sharing), [talk](https://drive.google.com/file/d/1QZafiOuN54a5-OdcKpDUJfjF_emxIF6a/view?usp=sharing)).

## Contents

```
make_figures.ipynb      notebook: data extraction, figures, statistics
data/                   curves from the simulations (described below)
figures/                output of the notebook, and the graphical abstract
  simulations/          vector figures of the simulations, from which data/ was extracted
JFM_Rapids/             LaTeX source of the paper and of its supplementary material
notes/                  theory notes with the full derivations
```

## Running

Requires Python 3 with NumPy, Matplotlib and Jupyter (tested with Python 3.13.9, NumPy 2.3.1 and Matplotlib 3.10.6).
PyMuPDF (tested with 1.28.0) is needed only to extract the data again from the vector figures. Open the notebook from
this folder and run all cells, or run

```bash
jupyter nbconvert --to notebook --execute --inplace make_figures.ipynb
```

The notebook writes to `figures/`, as one PDF and one 200 dpi PNG per panel:

- `fig_alpha_time`, `fig_alpha_height`: figure 1(*a*), (*b*) of the paper;
- `fig_capillary_group`, `fig_nu_Ds`: figure 2(*a*), (*b*);
- `fig_excess_width`, `fig_We_exponent`: figure 3(*a*), (*b*);
- `fig_hinze_ratio`, `fig_transition_time`, `fig_alpha_transition`, `fig_Rf_time`: figures S1, S4(*a*), S4(*b*) and S5
  of the supplementary material.

It also prints the fit $`\alpha - \alpha_{We_0=\infty} \approx 8.9\,\ell_\sigma/h`$ with the range of its coefficient and
its slope, the effective exponents at fixed time (table S2), the Hinze-scale constant $`K_H`$ and the related
statistics, the fits of the transition time, the late-time shape factor $`R_f`$, and the decomposition of table S3.

The other figures are not produced by the notebook:

- `figures/simulations/`: the fifteen vector figures of the simulations from which `data/` was extracted. Six of
  them, `immiscible_alpha_time*.pdf` and `alpha_time_misc_imm.pdf` with its `_height` and `_velocity` variants, are
  figures S2 and S3 of the supplementary material.
- `figures/graphical_abstract.jpg`: the graphical abstract, a frame of an isovolume rendering of the
  $`We_0 = 50`$ simulation near the end of the run, 1224 × 1020 px (aspect ratio 1.2:1).

## Result

With $`\bar\rho = (\rho_h + \rho_\ell)/2`$, $`\Delta\rho = \rho_h - \rho_\ell`$ and $`A_t = \Delta\rho/2\bar\rho`$, an
initial perturbation of shortest wavelength $`\lambda_0`$ and surface tension $`\sigma`$ define

```math
We_0 = \frac{\bar\rho\, g\, \lambda_0^2}{\sigma}, \qquad
\ell_\sigma = \left(\frac{\sigma}{\Delta\rho\, g}\right)^{1/2}, \qquad
\frac{\ell_\sigma}{\lambda_0} = (2 A_t We_0)^{-1/2}, \qquad
\tau_0 = \left(\frac{\lambda_0}{A_t g}\right)^{1/2}.
```

The growth parameter is measured as $`\alpha(t) = \dot h^2/4 A_t g h`$, with the full width
$`h = 6 \int \bar V(1 - \bar V)\,\mathrm{d}z`$. Complete self-similarity leaves no dimensionless group containing
$`\sigma`$, so $`We_0`$ can enter only through corrections in $`\ell_\sigma/h`$. Compared at equal mixing width, over
$`7 \le h/\lambda_0 \le 12.5`$, the simulations follow

```math
\alpha - \alpha_{We_0=\infty} \approx 8.9\,\frac{\ell_\sigma}{h},
```

a dependence on $`We_0^{-1/2}`$ at fixed $`h/\lambda_0`$, whereas exponents extracted at fixed $`t/\tau_0`$ drift with
the time of comparison. The mid-plane mass flux defines the shape factor
$`R_f = \Delta\rho\,\dot h/|\overline{\rho' w'}|_0`$ and the decomposition

```math
\alpha = \frac{R_f^2}{16}\, C_r^2\, (1 - \theta_0)\, Fr_0^2, \qquad
\overline{\rho' w'}_0 = -C_r\, \rho'_\mathrm{rms}\, w'_\mathrm{rms}, \qquad
1 - \theta_0 = \left(\frac{2 \rho'_\mathrm{rms}}{\Delta\rho}\right)^2, \qquad
Fr_0^2 = \frac{w'^2_\mathrm{rms}}{A_t g h},
```

evaluated on the mid-plane and averaged over $`8 \le t/\tau_0 \le 9.4`$ in table S3.

## Data

The simulations are those of Walker *et al.* (2025, 2026, 2027*a*, *b*): three-dimensional simulations with
$`1120^3`$ points at $`A_t = 0.5`$ and $`Re_0 = \infty`$, for $`We_0 = 50`$, 100, 200 and $`\infty`$ and a miscible
reference case, computed with the high-order compact finite-difference code Miranda (Cook 2007), localized artificial
diffusivity with interface sharpening (Brill, Olson & Bokman 2025) and a continuum surface force. The initial
wavelength is $`\lambda_0 = L/k_{\max} \approx 1.02`$ cm and the grid spacing $`\Delta x = L/N_\mathrm{pts} \approx 0.114`$ cm.

| File | Quantity | Source figures in `figures/simulations/` | Rows | Used in the paper |
|---|---|---|---|---|
| `growth_parameter.csv` | $`\alpha(t) = \dot h^2/4 A_t g h`$ | `immiscible_alpha_time`, `alpha_time_misc_imm` | 766 | figures 1–3, S4; tables S2, S3 |
| `mixing_width.csv` | $`h/\lambda_0`$ | `immiscible_alpha_time_height`, `alpha_time_misc_imm_height` | 204 | figures 1(*b*), 2(*a*), 3, S1 |
| `growth_velocity.csv` | $`\dot h/(A_t g \lambda_0)^{1/2}`$ | `immiscible_alpha_time_velocity`, `alpha_time_misc_imm_velocity` | 621 | check of $`h/\lambda_0`$ |
| `midplane_mass_flux.csv` | $`\lvert\overline{\rho' w'}\rvert_0/[\Delta\rho\,(A_t g \lambda_0)^{1/2}]`$ | `immiscible_alpha_time_mass_flux`, `alpha_time_misc_imm_mass_flux` | 722 | |
| `midplane_rho_rms.csv` | $`\rho'_{\mathrm{rms},0}/\Delta\rho`$ | `immiscible_alpha_time_rho_rms`, `alpha_time_misc_imm_rho_rms` | 288 | table S3 |
| `midplane_w_rms.csv` | $`w'_{\mathrm{rms},0}/(A_t g \lambda_0)^{1/2}`$ | `immiscible_alpha_time_w_rms`, `alpha_time_misc_imm_w_rms` | 669 | |
| `scaling_ratio.csv` | $`\Delta\rho\,\dot h/\lvert\overline{\rho' w'}\rvert_0`$ for the half-width, $`= R_f/2`$ | `immiscible_alpha_time_flux_ratio`, `alpha_time_misc_imm_flux_ratio` | 808 | figure S5, table S3 |
| `hinze_scale.csv` | Hinze scale $`\ell_H`$ in meters | `immiscible_integral_TKE_hinze_scale` | 338 | figure S1 |
| `transition_times.csv` | $`t_\theta/\tau_0`$, time of maximum $`\mathrm{d}\bar\theta/\mathrm{d}t`$ | markers in the `_height` figures | 5 | figures 3(*b*), S1, S4 |

The curve files are in long format, with columns `case`, `t_over_tau0` and the quantity:

| Column | Meaning |
|---|---|
| `case` | `We50`, `We100`, `We200`, `We_inf` (immiscible, $`We_0 = 50`$, 100, 200, $`\infty`$) or `miscible` (`hinze_scale.csv`: the three finite $`We_0`$) |
| `t_over_tau0` | time $`t/\tau_0`$ |
| `alpha` | growth parameter $`\alpha(t)`$ |
| `h_over_lambda0` | full width $`h/\lambda_0`$ (the axis of the source figures is labeled $`h/2L`$); consistent with $`(\dot h/\sqrt{A_t g \lambda_0})^2/4\alpha`$ to within about 5 % |
| `hdot_norm` | growth velocity $`\dot h/(A_t g \lambda_0)^{1/2}`$ |
| `mass_flux_norm` | magnitude of the turbulent mass flux on the mid-plane, $`\lvert\overline{\rho' w'}\rvert_0/[\Delta\rho\,(A_t g \lambda_0)^{1/2}]`$ |
| `rho_rms_norm` | r.m.s. density fluctuation on the mid-plane over $`\rho_h - \rho_\ell`$ |
| `w_rms_norm` | r.m.s. vertical velocity fluctuation on the mid-plane over $`(A_t g \lambda_0)^{1/2}`$ |
| `scaling_ratio` | scaling ratio $`\dot h(\rho_h - \rho_\ell)/\lvert\overline{\rho' w'}\rvert_0`$ of Walker *et al.*, based on the half-width $`h/2`$; the shape factor for the full width is $`R_f = 2 \times`$ `scaling_ratio` |
| `l_H_m` | Hinze scale $`\ell_H = 0.725\,(\sigma/\bar\rho)^{3/5}\varepsilon^{-2/5}`$ (Hinze 1955), in meters, with the dissipation rate of the simulations |

`transition_times.csv` has the columns `case` and `t_theta_over_tau0`.

The immiscible cases are taken from the `immiscible_*` figures and the miscible case from the `alpha_time_misc_imm_*`
figures, whose second curve repeats $`We_0 = \infty`$. The values were extracted from the vector paths of the figures,
not digitized from images: each plotted line is stored in the PDF as a list of points, which the notebook maps to data
coordinates with a linear fit to the positions of the tick labels (on the logarithmic axis of the Hinze-scale figure,
to the exponents of its labels). The extraction is in section 1 of the notebook and runs when `REEXTRACT = True`; it
reproduces the files in `data/`. Please cite Walker *et al.* when using the data.

## Paper and notes

`JFM_Rapids/JFM_Rapids_alpha_Theory.tex` and `JFM_Rapids/supplementary.tex` are the paper and its supplementary
material, with the bibliography `JFM_Rapids/jfm.bib`. They need the class and style files `jfm.cls` and `jfm.bst` of the
*Journal of Fluid Mechanics* LaTeX template, which are not included, and read their figures from `figures/` through
`\graphicspath`. `notes/alpha_surface_tension.tex` gives the derivations in full, with the bibliography
`notes/citations.bib`.

## References

- Brill, S. R., Olson, B. J. & Bokman, G. T. 2025 An extension of the localized artificial diffusivity method for immiscible and high density ratio flows. *J. Comput. Phys.* **542**, 114366. [doi:10.1016/j.jcp.2025.114366](https://doi.org/10.1016/j.jcp.2025.114366)
- Cook, A. W. 2007 Artificial fluid properties for large-eddy simulation of compressible turbulent mixing. *Phys. Fluids* **19**, 055103. [doi:10.1063/1.2728937](https://doi.org/10.1063/1.2728937)
- Cook, A. W., Cabot, W. & Miller, P. L. 2004 The mixing transition in Rayleigh–Taylor instability. *J. Fluid Mech.* **511**, 333–362. [doi:10.1017/S0022112004009681](https://doi.org/10.1017/S0022112004009681)
- Hinze, J. O. 1955 Fundamentals of the hydrodynamic mechanism of splitting in dispersion processes. *AIChE J.* **1**, 289–295. [doi:10.1002/aic.690010303](https://doi.org/10.1002/aic.690010303)
- Ristorcelli, J. R. & Clark, T. T. 2004 Rayleigh–Taylor turbulence: self-similar analysis and direct numerical simulations. *J. Fluid Mech.* **507**, 213–253. [doi:10.1017/S0022112004008286](https://doi.org/10.1017/S0022112004008286)
- Walker, M. D., Brill, S. R. & Olson, B. J. 2025 Effects of surface tension and viscosity on immiscible Rayleigh–Taylor mixing. *78th Annual Meeting of the APS Division of Fluid Dynamics*, Houston, TX, session U30, abstract 8. [Abstract](https://meetings-archive.aps.org/dfd/2025/u30/8/), [talk](https://drive.google.com/file/d/1jgFE_YQC5uhCAsLqNTcmoPDsvbyvzH8O/view?usp=sharing).
- Walker, M. D., Brill, S. R. & Olson, B. J. 2026 High-fidelity parametric study of surface tension and viscosity effects in immiscible Rayleigh–Taylor mixing. *19th International Workshop on the Physics of Compressible Turbulent Mixing (IWPCTM19)*, Ann Arbor, MI. [Abstract](https://drive.google.com/file/d/16irNsqovxGmB08cWheF4SVbzx0tQUwVy/view?usp=sharing), [talk](https://drive.google.com/file/d/1QZafiOuN54a5-OdcKpDUJfjF_emxIF6a/view?usp=sharing).
- Walker, M. D., Brill, S. R. & Olson, B. J. 2027*a* Immiscible Rayleigh–Taylor turbulence I: macroscopic behavior and growth dynamics. *Phys. Rev. Fluids*, submitted.
- Walker, M. D., Brill, S. R. & Olson, B. J. 2027*b* Immiscible Rayleigh–Taylor turbulence II: mesoscale mixing and spectral characteristics. *Phys. Rev. Fluids*, submitted.
