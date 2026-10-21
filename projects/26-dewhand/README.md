# DewHand

Project page for **DewHand: Direct Metric World-Space Hand Motion Reconstruction from Egocentric Videos**.

https://narusuzuki.github.io/projects/26-dewhand/

`index.html` contains the project page, with figures in `assets/`.
Set `window.DEWHAND_ARXIV_URL` when the paper is available, and add video entries
(`src`, `dataset`, optional `example`, `title` and `poster`) to `window.DEWHAND_VIDEOS` to populate the results gallery.
The `title` is the player's accessible label. Videos do not have visible
captions below them because their headers already identify the dataset.

The teaser has three HOT3D examples with synchronized input and reconstruction
panels in one MP4 per example, without visible player controls. Thumbnail
buttons select an example; muted playback
starts while the teaser is visible and pauses offscreen or in a background tab.
Reduced-motion preferences disable automatic playback. MP4s, posters, and thumbnail
images use the `teaser-01`, `teaser-02`, and `teaser-03` prefixes in `assets/videos/`.

The teaser uses existing DewHand hand and camera predictions with cached VGGT-Ω
scene point clouds. Only the cloud uses the existing camera-derived global
similarity registration; hand and camera predictions keep their metric scale.
The input panel is the calibrated 90-degree view rendered from original images
at 900 × 900, with the same optical center and axes as the cached scene input.
Every displayed input frame is paired with its corresponding reconstruction.
Examples 1 and 3 use all valid pixels at 30 masked timestamps (about 0.99 million
points), with the existing confidence filter and camera-derived registration.
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
