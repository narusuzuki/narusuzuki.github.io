# DewHand

Project page for **DewHand: Direct Metric World-Space Hand Motion Reconstruction from Egocentric Videos**.

https://narusuzuki.github.io/projects/26-dewhand/

`index.html` contains the project page, with figures in `assets/`.
Paper: https://arxiv.org/abs/2610.29936 (also set in `window.DEWHAND_ARXIV_URL`).
Add video entries
(`src`, `dataset`, optional `example`, `title` and `poster`) to `window.DEWHAND_VIDEOS` to populate the results gallery.
The `title` is the player's accessible label. Videos do not have visible
captions below them because their headers already identify the dataset.

The teaser has six examples, each with synchronized input and reconstruction
panels in one MP4 and no visible player controls. Example buttons select a
clip; muted inline playback starts while visible and pauses offscreen or in a
background tab. Reduced-motion preferences disable automatic playback.
The files use the `teaser-01` through `teaser-06` prefixes in `assets/videos/`.

1. HOT3D `P0012_d85e10f6__2430`: the paper's teaser example, identified by
   its six original RGB thumbnails (container handling, then reaching for the
   three-tier shelf). All 150 source prediction frames are shown. The dense
   static cloud removes tracked hands/arms and the moving container; the
   container uses current-frame visible depth samples.
2. HOT3D `P0011_76ea6d47__2955`: source frames 37–149, about 3.77 seconds.
   The static scene retains about 3.90 million background samples, excluding
   hands, arms, and an expanded object mask. A separate tracked container mask
   protects current-frame object points from hand removal.
3. ARCTIC `s05_capsulemachine_use_02__450`: 150 frames, including the surrounding
   floor and tabletop (about 1.17 million static points). Depth uses 352 × 256
   images with the native aspect preserved. Saved hand coordinates are brought
   back to camera0 with `ours_verts @ r_canon`; camera poses remain exact. For
   display, ARCTIC world +Z is transformed by the original camera calibration
   and mapped to display +Z, so gravity points down. This was checked against
   the upright SMPL-X torso axis. The legacy dump's gravity field used world Y
   and is not used for this display. Hands, cameras, and points receive the same
   rigid display transform. The coffee machine uses current-frame depth points.
4. In-the-wild home cooking: source RGB `HaWoR/example/segment_037.mp4`,
   frames 0–89 (3 seconds). DewHand is run on RGB with detected HaMeR features;
   no HaWoR predictions or GT poses are used. The pan uses current-frame points.
5. In-the-wild plate carrying: source RGB `HaWoR/example/video_0.mp4`,
   frames 0–119 (4 seconds), with the same independent DewHand inference.
   Moving plates use current-frame points. These are exploratory results;
   hand-to-scene position errors remain, especially during camera movement.
6. HoloAssist printer operation: `z013-june-16-22-printer_small__1380__0`,
   with original DewHand hand and camera predictions and a dense scene cloud
   from 50 masked source timestamps (about 1.34 million points).

Only the scene cloud receives camera-derived similarity registration: scale is
from mean centered camera radii, and rotation/translation are anchored to the
first camera pose. Predicted metric hands and cameras are not fitted or scaled.
Object points use finite positive source depth without the background confidence
cutoff. There is no hidden-surface completion, object shape fitting, or geometric
adjustment to predicted hands. Dataset canonical-frame and gravity metadata are
used for display when available; in-the-wild up is estimated from a predicted
work-surface normal, without inertial or GT gravity.

The in-the-wild clips use the paper comparison checkpoint `base_158848.pt`,
HaMeR mean patch features, nearest-valid feature filling, two flow steps, and
five-sample velocity averaging. Their fixed-length model inputs repeat the last
RGB frame to provide 150 context frames; padded frames are never displayed.
All displayed input and prediction frames are paired in one encoded video.
The HOT3D input panels use calibrated 90-degree views rendered at 900 × 900;
other inputs retain their source aspect ratio inside the same panel.

The display camera moves at constant speed in one direction across 60 degrees
per clip, at a fixed elevation with the vertical kept upright. It restarts
with the input clip's loop. The in-the-wild views track a smoothed interaction
center so that camera movement does not make the hands too small; only the
display camera moves. Source point and prediction geometry are unchanged.

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
