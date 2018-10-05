[Hashcat](https://en.wikipedia.org/wiki/Hashcat "wikipedia:Hashcat") is powerfull utility for recovering passwords from hash. It supports over 200 hash algorithms. It can use CPU, GPU and other hardware accelerators.

## Installation

[Install](/index.php/Install "Install") [hashcat](https://www.archlinux.org/packages/?name=hashcat) package.

Hashcat can't work without [OpenCL](/index.php/OpenCL "OpenCL"), so it is needed to install [GPGPU#OpenCL Runtime](/index.php/GPGPU#OpenCL_Runtime "GPGPU") package for your CPU or GPU.

## Usage

For getting password from *hash_file* with *hash_type* using *dictionary_file*:

```
hashcat -m *hash_type* *hash_file* *dictionary_file*

```

More examples and usage details can be found at [Hashcat wiki](https://hashcat.net/wiki/).

## See also

*   [Official website](https://hashcat.net/hashcat/)