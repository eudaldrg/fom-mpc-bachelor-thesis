# A Learning Approach to the FOM Problem

Bachelor's thesis in Mathematics (Universitat Politècnica de Catalunya, CFIS), April 2017.
The research was done at the [MIT MCube Lab](https://mcube.mit.edu/) under Alberto Rodríguez,
with Maria Alberich as UPC supervisor.

**[Read the thesis (PDF)](fom_thesis/TFGFINAL.pdf)**

![DFOM tracking a trajectory made of 20 curvatures with a 35 step horizon](fom_thesis/dfom_trajectory_long_horizon.jpg)

## Problem

Pushing an object across a table is a hybrid control problem: at every instant the pusher can
stick to the object or slide left or right along it, and each choice gives different dynamics.
Model predictive control (MPC) over these contact modes is usually solved as a mixed integer
quadratic program (MIQP), whose cost grows exponentially with the horizon. That is far too slow
to run inside a control loop.

Family of modes (FOM), proposed by François Hogan at MIT, is a heuristic that only evaluates a
small, fixed set of mode sequences at each control step. This thesis studies its weaknesses and
proposes ways to make it usable in practice.

## Contributions

- **Nominal mode and chameleon mode.** Reformulations that fix the sequential weaknesses of FOM.
  Without the nominal mode, every controller tested on circular trajectories diverged.
- **MIQP baseline.** A velocity based MIQP formulation solved with Gurobi, plus a clustered
  variant. Simulating 500 steps with a horizon of 7 took around 6 hours, a control rate below
  0.02 Hz, which shows why a fast approximation like FOM is needed.
- **Mode selection protocol.** A systematic way to learn which modes to include in the family.
  It produces families of about 4 modes that track straight lines, circles and combinations of
  both.
- **Dynamic FOM (DFOM).** Switches between learned families depending on the local curvature, so
  it can track trajectories with discontinuities in curvature, as in the figure above.

## Contents

| Path | What it is |
|---|---|
| `fom_thesis/TFGFINAL.pdf` | Final thesis |
| `fom_thesis/TFGEudaldRomo.tex` | LaTeX source |
| `fom_thesis/Videos/` | Simulation videos (chameleon mode, circles, lines, clustered MIQP, DFOM) |
| `templateTFG-GM2016/` | University thesis template |

## Building the PDF

```sh
cd fom_thesis
pdflatex TFGEudaldRomo && bibtex TFGEudaldRomo && pdflatex TFGEudaldRomo && pdflatex TFGEudaldRomo
```

**Keywords:** robotic manipulation, planar pushing, model predictive control, hybrid systems,
MIQP, underactuation.

## License

MIT, see [LICENSE](LICENSE). `templateTFG-GM2016/` is the university thesis template and is not
covered; it belongs to its original authors.
