# My historical hexagonal-to-orthorhombic codes

These are my recovered thesis codes for *Evolution of Multivariant Microstructures with Anisotropic Misfit: A Phase Field Study*. I also used them to study symmetry breaking and shape transitions. This repository is public.

## Source versions

- `original/Codes/`: my recovered serial and threaded model sources, historical evolution routines, utilities and saved initial fields. Included files are unchanged. Third-party Numerical Recipes files are omitted; the old builds still refer to them and are not the runnable modern version.
- `gsl/`: the working C version with Numerical Recipes allocation and random routines replaced by GSL. Sustained conserved composition noise and nonconserved noise in all three variants are retained.
- `docs/`: recovery records and completed checks. `public-source-manifest.json` lists checksums and explicitly identifies omitted files.

The complete archive, including third-party Numerical Recipes files, is retained in [my private archive repository](https://github.com/saswataiith/anisotropic-misfit-model-from-my-thesis). It can be viewed while signed in with an account that has access. I have not made the third-party files public.

The [Julia repository](https://github.com/saswataiith/anisotropic-misfit-model-julia-from-my-thesis) contains the selected model equations, sustained-noise controls, separate variant coefficients, timestep switching and the tested particle-moment utility. It explains its differences from the historical programs.

## Build the GSL working version

Install a C compiler, FFTW and GSL. On macOS:

```sh
brew install fftw gsl
make -C gsl/src_serial
mkdir -p runs/smoke32
cp gsl/examples/smoke32/InputParams gsl/examples/smoke32/bin1ary runs/smoke32/
cd runs/smoke32
../../gsl/src_serial/binorder
```

On another system set `PREFIX` in the Makefile to the library installation prefix. The selected evolution routine is `evolve12.c`; historical alternatives remain available for inspection.

The recorded GSL check used 32² points, 100 steps, seed −494 and timestep 0.001. It checked finite fields, repeatability and conserved composition. The example retains the original noise scheduling, including a noise event at count zero. The results do not establish long-time morphology or spatial convergence. Other evolution routines and threaded builds have not been validated.

The original moment utility is `original/Codes/utils/calc_singleppt.c`; the GSL copy is `gsl/utils/calc_singleppt.c`. The Julia repository documents the centroid and spacing corrections explicitly.

Strains and composition are dimensionless. Other values use the thesis nondimensionalization; no SI calibration is inferred from the recovered parameter files. My own public source is available under MIT; see [licence scope](LICENSING.md).

I also compiled and ran the public GSL copy on macOS after preparing this repository. `docs/public-gsl-run.json` reports finite fields and a saved composition mean drift of 3.9e−16 between counts 0 and 100. The retained historical loop advances once more after saving count 100; this extra unsaved update is documented rather than removed from the recovered version.

## Using my code

My original source is available under MIT. See [licence scope and dependency terms](LICENSING.md) and the [licence](LICENSE).
