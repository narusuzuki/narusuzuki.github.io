# DewHand

Project page for **DewHand: Direct Metric World-Space Hand Motion Reconstruction from Egocentric Videos**.

https://narusuzuki.github.io/projects/26-dewhand/

`index.html` contains the project page, with figures in `assets/`.
Set `window.DEWHAND_ARXIV_URL` when the paper is available, and add video entries
(`src`, `dataset`, optional `example`, `title` and `poster`) to `window.DEWHAND_VIDEOS` to populate the results gallery.
The `title` is the player's accessible label. Videos do not have visible
captions below them because their headers already identify the dataset.

The teaser has one ARCTIC and two HOT3D examples with synchronized input and reconstruction
panels in one MP4 per example, without visible player controls. Thumbnail
buttons select an example; muted playback
starts while the teaser is visible and pauses offscreen or in a background tab.
Reduced-motion preferences disable automatic playback. MP4s, posters, and thumbnail
images use the `teaser-01`, `teaser-02`, and `teaser-03` prefixes in `assets/videos/`.

The teaser uses existing DewHand hand and camera predictions with VGGT-Ω
scene point clouds. Only the cloud uses the existing camera-derived global
similarity registration; hand and camera predictions keep their metric scale.
Example 1 uses the ARCTIC capsule coffee machine clip
`s05_capsulemachine_use_02__450`, with all 150 original prediction frames.
The native 1400 × 1000 input is fitted into the 900 × 900 panel with its aspect
ratio preserved. Saved canonical hand coordinates are converted back to the
first-camera frame with `ours_verts @ r_canon`; the saved camera poses are kept
exactly. VGGT-Ω depth is inferred from the corresponding RGB frames. A single
camera-derived similarity uses the mean camera-radius ratio for scale and the
first camera pose for rotation and translation; no trajectory or hand fitting
is used. The static scene retains about 1.17 million points from 30 timestamps,
including the surrounding floor and tabletop and excluding tracked body
and expanded object masks. Depth uses the native image aspect at 352 × 256.
For display, the physical ARCTIC world +Z axis is transformed into the first
camera frame and mapped to display +Z, so gravity points down. The world
vertical was checked against the upright SMPL-X torso axis; the legacy dump
field named gravity incorrectly used world Y and is not used for display.
All hands, cameras, and scene points receive the same rigid display transform. The
machine uses only its current frame's visible depth points, without hidden
surface completion or object fitting. Masks have reviewed anchors at frames
0, 37, 75, 112, and 149.
For the HOT3D examples, the input panel is the calibrated 90-degree view
rendered from original images at 900 × 900, with the same optical center and
axes as the cached scene input. Every displayed input frame is paired with
its corresponding reconstruction. Example 3 uses all valid pixels at 30
masked timestamps (about 0.99 million points), with the existing confidence
filter and camera-derived registration.
Example 2 shows source frames 37–149 of a container-manipulation clip
(about 3.77 seconds).
Its static cloud uses source timestamps 30–149, removes hand/arm masks and a
one-pixel-expanded object mask, and retains about 3.90 million background points.
A separately tracked object mask protects the container from hand removal;
only the current frame's visible object-depth samples are rendered. Object points
use finite positive cached depth without the global background confidence cutoff.
No hidden surface completion, object pose/shape fitting, temporal interpolation,
or adjustment to the predicted hands is applied. SAM2 object masks use reviewed
anchors at source frames 29, 37, 75, 112, and 149; the first 37 frames are omitted.
The hand and camera predictions, metric scale, and scene registration stay unchanged.
A perspective display camera orbits ±30 degrees in azimuth and 3 degrees in
elevation around the interaction, with a constant target and distance per clip.

The gallery includes two HOT3D examples and one example each from ARCTIC,
HoloAssist, H2O, and TACO. MP4s and posters are stored in `assets/videos/`.
Video entries specify dimensions to reserve space before loading; the first
example for each dataset has an `id`. Dataset and example buttons show one
video at a time; switching pauses the previous player and loads the chosen
video on demand. Selection is preserved in the URL hash for direct links,
and each dataset remembers its last selected example during the visit.
Update the `v` query in both `src` and `poster` when replacing a clip.

DewHand panels use a green header, border, and light background for emphasis;
panel dimensions and rendering scale remain shared with the other methods.

All gallery comparison clips contain 150 frames at 30 fps. They use the
manuscript's shared viewpoint, display scale, and joint two-hand SE(3) alignment without scale
correction. HoloAssist GT and ReViV use the anatomical connections for the
exported joint order; ReViV cameras are converted from world-to-camera to
camera-to-world before the same hand alignment is applied. The ARCTIC
HaWoR export does not include a usable camera trajectory, as noted inside
the video; this is a limitation of this visualization's export.
