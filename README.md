# gnark-crypto

[![License](https://img.shields.io/badge/license-Apache%202-blue)](LICENSE)  [![Go Report Card](https://goreportcard.com/badge/github.com/ConsenSys/gnark-crypto)](https://goreportcard.com/badge/github.com/ConsenSys/gnark-crypto) [![PkgGoDev](https://pkg.go.dev/badge/mod/github.com/consensys/gnark-crypto)](https://pkg.go.dev/mod/github.com/consensys/gnark-crypto) [![DOI](https://zenodo.org/badge/249487917.svg)](https://zenodo.org/badge/latestdoi/249487917)

`gnark-crypto` provides:
* [Elliptic curve cryptography](ecc/ecc.md) (+pairing) on BN254, BLS12-381, BLS12-377, BW6-761, BLS24-315, BW6-633, BLS12-378 and BW6-756
* [Finite field arithmetic](field/field.md) (fast big.Int)
* FFT
* Polynomial commitment schemes
* MiMC
* EdDSA (on the "companion" twisted edwards curves)



`gnark-crypto` is actively developed and maintained by the team (gnark@consensys.net | [HackMD](https://hackmd.io/@gnark)) behind:
* [`gnark`: a framework to execute (and verify) algorithms in zero-knowledge](https://github.com/consensys/gnark) 


## Warning
**`gnark-crypto` has not been audited and is provided as-is, use at your own risk. In particular, `gnark-crypto` makes no security guarantees such as constant time implementation or side-channel attack resistance.**

`gnark-crypto` packages are optimized for 64bits architectures (x86 `amd64`) and tested on Unix (Linux / macOS).


## Getting started

### Go version

`gnark-crypto` is tested with the last 2 major releases of Go (1.16 and 1.17).

### Install `gnark-crypto`

```bash
go get github.com/consensys/gnark-crypto
```

Note if that if you use go modules, in `go.mod` the module path is case sensitive (use `consensys` and not `ConsenSys`).

### Documentation

[![PkgGoDev](https://pkg.go.dev/badge/mod/github.com/consensys/gnark-crypto)](https://pkg.go.dev/mod/github.com/consensys/gnark-crypto)

The APIs are consistent accross the curves. For example, [here is `bn254` godoc](https://pkg.go.dev/github.com/consensys/gnark-crypto/ecc/bn254#pkg-overview).

### Development

Most (but not all) of the code is generated from the templates in `internal/generator`.

The generated code contains little to no interfaces and is strongly typed with a base field (generated by the `gnark-crypto/field`). The two main factors driving this design choice are:

1. Performance: `gnark-crypto` algorithms manipulates millions (if not billions) of field elements. Interface indirection at this level, plus garbage collection indexing takes a heavy toll on perf.
2. No generics in Go: need to derive (mostly) identical code for various moduli and curves, with consistent APIs

To regenerate the files, see `internal/generator/main.go`. Run:
```
go generate ./internal/...
```

## Benchmarks

[Benchmarking pairing-friendly elliptic curves libraries](https://hackmd.io/@gnark/eccbench) 

>The libraries are implemented in different languages and some use more assembly code than others. Besides the different algorithmic and software optimizations used across, it should be noted also that some libraries target constant-time implementation for some operations making it de facto slower. However, it can be clear that consensys/gnark-crypto is one of the fastest pairing-friendly elliptic curve libraries to be used in zkp projects with different curves.

## Citing

If you use `gnark-crypto` in your research a citation would be appreciated.
Please use the following BibTeX to cite the most recent release.

```bib
@software{gnark-crypto-v0.6,
  author       = {Gautam Botrel and
                  Thomas Piellard and
                  Youssef El Housni and
                  Arya Tabaie and
                  Ivo Kubjas},
  title        = {ConsenSys/gnark-crypto: v0.6.0},
  month        = jan,
  year         = 2022,
  publisher    = {Zenodo},
  version      = {v0.6.0},
  doi          = {10.5281/zenodo.5815454},
  url          = {https://doi.org/10.5281/zenodo.5815454}
}
```

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/consensys/gnark-crypto/tags).


## License

This project is licensed under the Apache 2 License - see the [LICENSE](LICENSE) file for details
