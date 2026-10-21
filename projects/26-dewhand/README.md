# DewHand

Project page for **DewHand: Direct Metric World-Space Hand Motion Reconstruction from Egocentric Videos**.

https://narusuzuki.github.io/projects/26-dewhand/

`index.html` contains the project page, with figures in `assets/`.
Set `window.DEWHAND_ARXIV_URL` when the paper is available, and add video entries
(`src`, optional `title` and `poster`) to `window.DEWHAND_VIDEOS` to populate the results gallery.

The gallery includes two HOT3D examples and one example each from ARCTIC,
HoloAssist, H2O, and TACO. MP4s and posters are stored in `assets/videos/`.
Video entries specify dimensions to reserve space before loading; the first
example for each dataset has an `id` used by the dataset navigation.
Update the `v` query in both `src` and `poster` when replacing a clip.

All clips contain 150 frames at 30 fps. They use the manuscript's shared
viewpoint, display scale, and joint two-hand SE(3) alignment without scale
correction. HoloAssist GT and ReViV use the anatomical connections for the
exported joint order; ReViV cameras are converted from world-to-camera to
camera-to-world before the same hand alignment is applied. The ARCTIC
HaWoR export does not include a usable camera trajectory, as stated in its
caption; this is a limitation of this visualization's export.
