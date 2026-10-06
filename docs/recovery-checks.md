# Recovery checks

The recovered archive contains 86 files. The checksum manifest records every original file. All four local archive copies have SHA-256 `5338bc34159a48f11e8b926a88f95f60cf099dac4708303c18e5ae617b9f70b5`.

## Serial compile check

The source list in `src_serial/Makefile` uses `evolve12.c`. It compiled and linked successfully on macOS using the system C compiler and Homebrew FFTW 3:

```sh
mkdir -p build
cc -O0 -fcommon -I/opt/homebrew/include \
  original/Codes/src_serial/spino5.c \
  original/Codes/src_serial/get_input_spino2.c \
  original/Codes/src_serial/init_confv2.c \
  original/Codes/src_serial/evolve12.c \
  original/Codes/src_serial/eigen_strain.c \
  original/Codes/src_serial/calc_bn.c \
  original/Codes/src_serial/out_conf.c \
  original/Codes/src_serial/ran1.c \
  original/Codes/src_serial/gasdev.c \
  original/Codes/src_serial/nrutil.c \
  -L/opt/homebrew/lib -lfftw3 -lm -o build/binorder
```

Adjust the FFTW include and library paths for another installation. `-fcommon` supports the shared global variables declared in the historical header.

This is a compilation check only. The simulation has not been executed during recovery, and no published result has been reproduced.

## Older source combinations

`src_serial/Makefile.gcc` selects `evolve11.c`. That routine does not compile against the supplied header: it refers to `sustained_noise_level_uncons`, while the header declares separate parameters for the three variants. No correction has been made to the archived files. The threaded source combination has not been compiled.

## GSL update

The serial GSL working version compiles and runs. All Numerical Recipes implementation files are excluded from `gsl/`. GSL matrix allocation, uniform sampling and Gaussian sampling replace them. The support test checks zero- and one-based matrix bounds, positive/negative seed repeatability and Gaussian moments over 200,000 draws (mean −0.00002196, variance 1.00143). Address and undefined-behaviour sanitizers reported no errors in that test. Original checksums still match.
