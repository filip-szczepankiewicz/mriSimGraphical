# MRI simulators for visualization
Designed by Filip Sz (Lund University) and coded by Claude (Anthropic) and ChatGPT (OpenAI).

Four interactive MRI physics visualisations. Each is a single
self-contained HTML file that should run well on both PCs and phones.

**These are teaching aids, not quantitative simulators.** They are meant for
showing the basic ideas and for making figures and clips, not for predicting
signal or reproducing measurements. The models are deliberately simplified —
single voxel, non-selective hard pulses, one spatial axis, no diffusion or flow,
approximate relaxation values that are not field-strength corrected. 

## `mriRelaxSim.html` — Spin packets

Where T1, T2 and T2\* come from. An isochromat ensemble driven by three separate
mechanisms — T1 relaxation, spin–spin fluctuation with a correlation time, and a
static ΔB₀ spread — shown as a 3D view, a transverse plane and a signal plot with
analytic envelopes. Hard or finite-duration RF pulses, and a spin-echo demo.

## `mriSeqSim.html` — Sequence sim

Bloch-equation spin dynamics for seven sequences (FID, saturation recovery, spin
echo, CPMG, spoiled GRE, IR-SE, bSSFP) plus a nutation demo, with a tissue
library including two-compartment mixtures, STIR/FLAIR nulling, and slow motion
at RF pulses, gradients and acquisition. Records a full pass as a video.

## `mriFieldSim.html` — Field sim

3D view of the ideal gradient field and the concomitant (Maxwell) terms that come
with it: gradients to 200 mT/m, B₀ from 0.01 to 20 T, an optional ΔB surface, and
gradient modulation during capture. Orbit, wiggle or still recording for slides.
The concomitant field itself is computed from the closed-form expression.

## `mriInductSim.html` — Induction bench

A rotating/precessing magnetic dipole beside a pickup coil, showing magnetic flux,
Faraday induction, induced current, flip-angle dependence and distance falloff.
The display can switch between a classical bar-magnet view and a spin-½ density-
operator view. In spin mode the density operator is visualised as an exaggerated
projective-measurement probability surface: an unpolarised state is spherical,
while increasing illustrative polarisation produces a rotating pear-shaped surface,
coloured red toward surplus probability and blue toward deficit probability. The
live 2×2 density matrix is shown alongside the 3D view.

