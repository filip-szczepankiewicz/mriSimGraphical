# MRI simulators for visualization
Designed by Filip Sz (Lund University) and coded by Claude (Anthropic) and ChatGPT (OpenAI).

Seven interactive MRI physics visualisations. Each is a single self-contained HTML
file with no build step, no server and no network access, and should run well on
both PCs and phones. The 3D views use WebGL, with Three.js bundled inside the
file.

All seven share one look: the simulator name in capitals at the top left of the
control rail, a version chip and a light/dark chip at the right of the same line,
a one-line description underneath, and uppercase section headings below that. The
light/dark choice is shared between the files and remembered, and follows the
operating-system setting on a first visit.

**These are teaching aids, not quantitative simulators.** They are meant for
showing the basic ideas and for making figures and clips, not for predicting
signal or reproducing measurements. The models are deliberately simplified. Each
simulator states its own simplifications under the version chip in its header,
which also opens the credits and changelog. Typical simplifications are a single
voxel, one spatial axis, no diffusion or flow, and approximate relaxation values
that are not corrected for field strength.

| Simulator | Topic |
|---|---|
| [`mriRelaxSim.html`](#mrirelaxsimhtml--relaxation-sim) | T1, T2 and T2\* relaxation |
| [`mriSeqSim.html`](#mriseqsimhtml--sequence-sim) | Bloch simulation of common sequences |
| [`mriFieldSim.html`](#mrifieldsimhtml--field-sim) | Gradient and concomitant (Maxwell) fields |
| [`mriInductSim.html`](#mriinductsimhtml--induction-sim) | Signal induction in a receive coil |
| [`mriSliceSim.html`](#mrislicesimhtml--slice-sim) | Slice-selective excitation and the rewinder |
| [`mriReadoutSim.html`](#mrireadoutsimhtml--readout-sim) | K-space trajectories in spin-echo imaging |
| [`mriArtifactSim.html`](#mriartifactsimhtml--artifact-sim) | Image artifacts: chemical shift, aliasing, Gibbs ringing |

## How to use

The simulators must be downloaded and opened in a local browser. Clicking an
`.html` file here on GitHub only shows its source code; it does not run it.

1. Download one simulator, or all of them:
   - **One file:** click the file in the list above the README, then use the
     *Download raw file* button (↓) at the top right of the code view.
   - **All files:** click the green **Code** button and choose **Download ZIP**,
     then unzip. Or clone the repo:
     `git clone https://github.com/filip-szczepankiewicz/mriSimGraphical.git`
2. Open the downloaded `.html` file in a browser, for example by double-clicking
   it or dragging it into a browser window.

No installation, server or internet connection is needed; everything runs
inside the file. A recent version of Chrome, Edge, Firefox or Safari is
recommended. Video recording in the Sequence sim and Field sim relies on the
WebCodecs API, which is best supported in Chromium-based browsers (Chrome, Edge).

On a phone, save the file to the device and open it from the file manager in a
browser. Some mobile file viewers show the source instead of running the page.

## `mriRelaxSim.html` — Relaxation sim

![Relaxation sim](docs/img/mriRelaxSim.png)

Where T1, T2 and T2\* come from. An isochromat ensemble driven by three separate
mechanisms — T1 relaxation, spin–spin fluctuation with a correlation time, and a
static ΔB₀ spread — shown as a 3D view, a transverse plane and a signal plot with
analytic envelopes. Hard or finite-duration RF pulses, and a spin-echo demo.

## `mriSeqSim.html` — Sequence sim

![Sequence sim](docs/img/mriSeqSim.png)

Bloch-equation spin dynamics for seven sequences (FID, saturation recovery, spin
echo, CPMG, spoiled GRE, IR-SE, bSSFP) plus a nutation demo, with a tissue
library including two-compartment mixtures, STIR/FLAIR nulling, and slow motion
at RF pulses, gradients and acquisition. Records a full pass as a video.

## `mriFieldSim.html` — Field sim

![Field sim](docs/img/mriFieldSim.png)

3D view of the ideal gradient field and the concomitant (Maxwell) terms that come
with it: gradients to 200 mT/m, B₀ from 0.01 to 20 T, an optional ΔB surface, and
gradient modulation during capture. Orbit, wiggle or still recording for slides.
The concomitant field itself is computed from the closed-form expression.

## `mriInductSim.html` — Induction sim

![Induction sim](docs/img/mriInductSim.png)

A rotating/precessing magnetic dipole beside a pickup coil, showing magnetic flux,
Faraday induction, induced current, flip-angle dependence and distance falloff.
The display can switch between a classical bar-magnet view and a spin-½ density-
operator view. In spin mode the density operator is visualised as an exaggerated
projective-measurement probability surface: an unpolarised state is spherical,
while increasing illustrative polarisation produces a rotating pear-shaped surface,
coloured red toward surplus probability and blue toward deficit probability. The
live 2×2 density matrix is shown alongside the 3D view.

## `mriSliceSim.html` — Slice sim

![Slice sim](docs/img/mriSliceSim.png)

Slice-selective excitation, and why the rewinder is needed. A row of spins along
the slice direction is driven by a sinc RF pulse (adjustable time-bandwidth
product, optional Hanning apodisation) played during a trapezoidal slice-select
gradient G<sub>s</sub>. The floor under the spins is coloured by the local field
ΔB<sub>z</sub> = G<sub>s</sub>·x. The resulting |M<sub>xy</sub>| profile is
coloured by transverse phase, so the phase dispersion before the rewinder and the
coherent slice after it can be seen directly, with a Fourier (small-tip) estimate
for comparison. A second panel maps the RF spectrum onto position through
f = γ̄G<sub>s</sub>x to show how bandwidth and gradient set the slice thickness.

Four lecture presets step through the argument: RF without a gradient, slice
selection without a rewinder, slice selection with a rewinder, and a two-slice
multiband pulse. Flip angle, slice thickness or gradient, slice offset, pulse
duration, rewinder area and rewinder duration are adjustable. The model uses the
rotating-frame Bloch equation without relaxation or off-resonance.

## `mriReadoutSim.html` — Readout sim

![Readout sim](docs/img/mriReadoutSim.png)

The effective k-space trajectory of a spin-echo acquisition, drawn in 3D and kept
in sync with an RF/gradient/ADC sequence diagram. Acquired samples accumulate on
the k-space grid shot by shot, and the 180° pulse is shown as the k → −k
mapping of the transverse coherence. The x/y prewinders can be placed before or
after the refocusing pulse to show how that changes the path.

Eight acquisition modes, grouped by readout type. Cartesian line by line:
line-by-line and multi-echo spin echo (three echoes per shot). EPI: one-shot,
segmented in kx, segmented in ky, and segmented as propeller blades. Spiral:
one-shot and segmented. Phase-encoding resolution is adjustable, and the spiral
density follows it: the lap count is N/2, since a radial line crosses a spiral
twice per lap, so 30 samples per EPI line corresponds to 15 laps and all modes
are comparable at the same resolution. Gradient areas define the path; ramps,
hardware limits and relaxation are simplified.

In the propeller variant each shot is a short EPI blade of eight parallel lines through the
centre of k-space, and successive blades are rotated by 180°/blades, so the
blades cover k-space as a fan and every blade re-samples the centre. The blade
count follows π/2·N/L, as in PROPELLER/BLADE. For these blades the sequence diagram switches its
gradient rows to the blade axes, since the physical Gx and Gy are their rotation
by the blade angle.

## `mriArtifactSim.html` — Artifact sim

![Artifact sim](docs/img/mriArtifactSim.png)

Image artifacts as consequences of the signal equation rather than as pictures.
A 2D analytic phantom (ellipses and rectangles, water and fat as separate
species) has a closed-form Fourier transform, so k-space is computed exactly at
every acquired sample. Each sample also carries the time at which it was
measured, and the image is a plain inverse DFT. The artifacts are not drawn.
They follow from the fat phase term, the field offset around a susceptibility
source, the sampling step Δk = 1/FOV and the finite k-space extent.

Four panels: the true object (or its field map) with the FOV, k-space coloured
by acquisition time, the reconstructed image, and the signal equation with the
term that causes the chosen artifact highlighted, live numbers and a diagnostic
plot. A dropdown selects the artifact and loads a preset. All physics stays on
in every mode, so effects combine as they would on a scanner.

- **Chemical shift, 1st kind.** Fat is shifted f<sub>F</sub>/BW<sub>px</sub>
  pixels along each low-bandwidth direction. In line-by-line imaging (and
  multi-echo spin echo) the phase direction has effectively infinite bandwidth,
  so the shift is along readout only. In EPI it is f<sub>F</sub>·N<sub>PE</sub>·ESP
  pixels along phase, which is tens of pixels, and a faint fat ghost appears at
  N/2 from the alternating readout direction.
- **Chemical shift, 2nd kind.** In-phase and opposed-phase gradient echoes, the
  dark boundary outline and the signal drop in fatty liver. A spin echo
  refocuses the effect. Single-peak or six-peak fat.
- **Aliasing.** Phase wrap-around, readout and phase oversampling.
- **Gibbs ringing.** Truncation overshoot of about 9 %, k-space filters (Tukey,
  Hann, Hamming) against PSF width, and zero-filling.
- **Susceptibility.** A sphere of air, titanium, Co–Cr or steel, which can be
  dragged over the object, with the analytic dipole field
  Δf = γ̄B₀(Δχ/3)(a/r)³(3cos²θ − 1) and B₀ through or in the slice. The same
  field offset is displaced along whichever direction has the lowest bandwidth
  per pixel. In line-by-line imaging that is readout (pile-up, voids, extra
  dephasing in gradient echoes, view-angle tilting with its blur of about
  BW<sub>RF</sub>/BW<sub>px</sub> pixels). In EPI it is phase: stretching and
  compression by Δf·N<sub>PE</sub>·ESP/R pixels, which flips with the blip
  polarity. Quick buttons switch between metal with spin echo and air with EPI.
- **Eddy currents and gradient delay.** Modelled as errors in the k-space
  trajectory, k(t) + γ̄∫[G(t′−δt) − G(t′) + g<sub>ec</sub>(t′)]dt′ with
  g<sub>ec</sub> = −(dG/dt) ⊗ a·e<sup>−t/τ</sup>. They are computed from the full
  gradient waveforms of the shot, and the analytic object is evaluated exactly at
  the actual k. This gives the EPI Nyquist (N/2) ghost, with an idealised
  reference-scan correction, and the diffusion eddy-current distortions of EPI:
  scaling (phase), shear (readout) and shift (slice at an offset). A button
  freezes the b = 0 image for comparison, and a plot shows the gradients and
  eddy fields over the shot. Line-by-line sequences are shown to be robust.

- **Flow.** Pulsatile blood in the superior sagittal sinus, flowing through
  the slice. The vessel's k-space is exact, and each phase-encoding line gets the
  vessel's complex amplitude at the time it was acquired, M(v)·e<sup>i2πM₁v</sup>.
  M₁ is computed from the through-slice gradients (including spin-echo
  crushers), and M(v) covers spin-echo washout and gradient-echo inflow. Ghosts
  emerge along phase at multiples of N<sub>PE</sub>·TR/T<sub>c</sub>, with flow
  compensation and a saturation band as remedies. EPI barely ghosts.
- **Spike and RF interference.** One corrupted k-space sample, placed by
  clicking the k-space panel, gives stripes of wavelength 1/|k₀| across the
  whole image. An external tone that is not phase-locked to the excitations
  gives the zipper along phase at f/BW<sub>px</sub>.

A Simple/Advanced switch sits under the artifact list. Simple offers the
artifact, three worked examples of it, and the notes, with no sliders at
all. Advanced adds the full control stack in collapsible sections.

Spin echo, gradient echo, and single-shot gradient-echo and spin-echo EPI.
Adjustable B₀, TE, bandwidth, FOV, matrix, readout direction and polarity, fat
saturation and noise. The noise per k-space sample scales with √bandwidth, so
the SNR cost of a higher bandwidth is visible. Four phantoms: abdomen,
Shepp–Logan head with a fat ring, a QA phantom with oil and water vials, and a
20 mm grid. A frozen reference with a draggable split view allows before/after
comparison.

With a susceptibility source, every point of a fine sub-pixel grid is shifted
and phase-weighted by its own frequency. Only the difference from the exact
analytic image is computed, so the image away from the source is unchanged.
Proton density only: no relaxation, so no T2\* blurring in EPI. Sources are
spheres centred in the slice, with a field linear in Δχ, and through-plane slice
bending is not modelled. Eddy currents are linear fields with one exponential
per axis and no cross-terms, and diffusion lobes drive eddy currents without
attenuating the signal. Flow is plug flow through the slice in a single
vessel, without velocity profiles or turbulence.

## Licence

The simulators are released under the MIT License (see [`LICENSE`](LICENSE)).
See [`NOTICE`](NOTICE) for attribution, the use of AI-assisted development, and
the bundled third-party software.
