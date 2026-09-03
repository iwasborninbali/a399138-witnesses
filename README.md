# a399138-witnesses — no three collinear points in the n × n × n grid (OEIS A399138)

**Archived release v1.0:** DOI [10.5281/zenodo.22271376](https://doi.org/10.5281/zenodo.22271376) (concept DOI 10.5281/zenodo.22271375).

Witness configurations, an independent verifier, and the symmetry-stratum search behind the lower bounds

| n | best known | this repository | symmetry of the witness | status of the value |
|---|---|---|---|---|
| 7 | 73 | four inequivalent 73-point configurations (14 classes known in total) | trivial / order 2 / order 3 | lower bound (a(7) ≥ 73) |
| 8 | **94** (previously 93) | two inequivalent 94-point configurations | subgroups of order 4 | lower bound |
| 9 | **116** | two inequivalent 116-point configurations | order 4; order 12 (optimal within its stratum) | lower bound |
| 10 | **138** | one 138-point configuration | order 6 | lower bound |
| 11 | **164** | one 164-point configuration | order 12 | lower bound |

a(1..6) = 1, 8, 16, 28, 40, 64 are the certified exact values (Kudriashov 2026, DOI 10.5281/zenodo.22019279); this repository adds the
bounds for n = 8…11 found on 2–3 September 2026 by exact optimisation (CP-SAT, OR-Tools) restricted to configurations invariant under a
subgroup of the symmetry group of the cube (order 48; 33 conjugacy classes of subgroups = 33 "strata"), and the four n = 7 configurations
found by simulated annealing and exchange moves. "Optimal within its stratum" means that the solver closed the bound inside that symmetry
class; nothing here is an upper bound on a(n).

## Verify

Every witness file is plain text: header lines starting with `#` (provenance), then one point `x y z` per line, coordinates 0…n−1.

```
python3 verify_witness_lines.py 11 witnesses/n11_164_c26_ord12_strata.txt
```

checks all C(m,3) triples with exact integer cross products (0 collinear triples expected) and that the points are distinct and inside the grid.
The check is independent of the search code.

## Contents

- `witnesses/` — the configurations of the table (file names: `n<n>_<points>_<stratum>_...txt`; `c<ii>_ord<k>` is the class of the
  stabilising subgroup in the numbering of `strata/cube_strata.py`, `ord` its order).
- `verify_witness_lines.py` — the verifier.
- `strata/cube_strata.py` — the stratum sweep: for each conjugacy class of subgroups H ≤ O_h, a CP-SAT model over H-orbits of cells with
  the constraint "at most two chosen cells on every grid line"; `strata/n<n>_results.json` — best value, bound and status per stratum.
- `classes/classes_n<n>.txt` — equivalence classes of the witnesses under the 48 symmetries of the cube (canonical forms).
- `oeis/a399138.txt` — the a-file submitted to OEIS (witnesses for n = 1…11).

## Provenance

Search and verification were carried out by AI agents (Anthropic Claude) under the direction of the author, on a 32-core VM (2–3 Sep 2026);
each witness was verified by two independent programs before inclusion. Journals and scripts: https://github.com/iwasborninbali/saturation
(`slack/night_2026-09-02/`, `logs/2026-09-02_ночь/`).

## License

Data and text: CC BY 4.0. Code: MIT. Author: Aleksei Kudriashov (Alex Komang), Nusa Dua, Bali — studio@nusadua.dev.
