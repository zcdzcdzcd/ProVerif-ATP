# ProVerif-ATP

Combining ProVerif and Automated Theorem Provers for Security Protocol Verification

Authors : [Di Long Li](https://github.com/darrenldl) and Alwen Tiu, at The Australian National University, Canberra ACT 2600, Australia

This project is part of our submission to CADE-27

## Installation prerequisites

#### Platform

- The software suite was used largely on the Linux platform. While all components should compile on Windows and Mac, the Makefile and various bash scripts may not function as intended on those platforms.

#### System binaries required

- `wget` (optional)
  - The Makefile will try to download a copy of Vampire if the archive is not present. You can download the archive manually and place it in the repository root directory to skip this. See below for details.

#### Compilers required

- OCaml compiler (for Narrator and ProVerif)

- C++ compiler (for Vampire)

#### OCaml packages required

OCaml packages are easiest to install via the use of the `opam` tool, which should be available on most distros

- For Narrator

  - `dune`

  - `mparser`

  - `core_kernel`

  - `js_of_ocaml`

  - `lwt`

- For ProVerif

  - `ocamlfind`

  - `ocamlbuild`

  - `lablgtk`

#### Notes

- As per Vampire's [license](https://vprover.github.io/licence.html), we are not allowed to redistribute the sources of Vampire, thus we do not bundle it in this repository
  - The Makefile will try to download the file automatically via the HTTPS URL if `4.2.2.tar.gz` is not present
  - If you feel this is unsafe, you can download the archive manually [here](https://github.com/vprover/vampire/releases/tag/4.2.2), and rename it to `4.2.2.tar.gz` and place it in the repository root directory (where Makefile resides in)

## Installation

Simply type

```bash
make install
```

to build and install the software suite to `/usr/local/bin/`

#### Notes

- The installed files will appear as `/usr/local/bin/pvatp` (main executable) and `/usr/local/bin/pvatp_assets/` (files required by the main executable)

- `pvatp` only accesses the copies of ProVerif and Vampire in `/usr/local/bin/pvatp_assets/`, so there is no need to remove prior installation of ProVerif or Vampire in your system

- More generally, `pvatp` accesses t he `pvatp_assets/` folder at where it is stored, so you can relocate the files as long as both `pvatp` and `pvatp_assets/` reside in the same directory

## Documentation

- `doc/pvatp/` contains the user manual and documentations detailing the architecture of ProVerif-ATP

- `doc/proverif/` contains the documentations detailing the modifications we made in ProVerif

- `narrator/doc/` contains the documentations detailing architecture or Narrator

## Usage

`pvatp protocol.pv`

where `protocol.pv` is the protocol specification in typed pi-calculus used by ProVerif

## Index and licenses

- `src/`

  - This contains the main Python script which invokes the following tools to deliver a streamlined user experience. The files inside are published under the MIT license.

- `narrator/`

  - This is part of the original work developed for this project (excluding `node_modules` subdirectory). Narrator provides the interface for viewing the knowledge graph and attack traces. The files (excluding `node_modules` subdirectory) are published under the MIT license.

  - The subdirectory `node_modules` contains downloaded copies of Javascript libraries. They are included in the repository for easier building and usage of the framework only. They are not part of our work, they are not modified by us, and are distrbuted under their respective original licenses.

- `proverif2.00/`

  - This is a modified copy of ProVerif version 2.00. We intend to submit the modifications to the original authors for integrations later on. We license our modifications using the [exact same GPL license](http://prosecco.gforge.inria.fr/personal/bblanche/proverif/LICENSEGPL) used by ProVerif 2.00.
  - However, please note that this is not the final copy we intend to submit to the authors, as we are not completely certain if all modifications are actually safe, and we will need to discuss with the authors prior to submitting any patches etc.

- `examples/`

  - This contains all the protocol specification and related files used in the benchmark

## Acknowledgement

While the TPTP parser code in Narrator was independently developed from scratch according to the [TPTP syntax reference](http://tptp.cs.miami.edu/~tptp/TPTP/SyntaxBNF.html), [zipperposition](https://github.com/c-cube/zipperposition)'s TPTP parser code was used as reference during the final debugging phase.
