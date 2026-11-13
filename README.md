# unstructured_environment_selfplay

Project page for the real-car self-play tests in unstructured (off-road) environments:
two cars (Tiguan and Touareg) driving with the RL motion planner.

Live page: <https://treschede.github.io/unstructured_environment_selfplay/> (after GitHub Pages is enabled, see below).

## Pages

| page | what it shows |
|---|---|
| `index.html` | Interactive explorer of the 2026-11-12 Tiguan drive (747 s): the Tiguan's live BEV at each moment over the stitched map, the cars the Tiguan's tracker sees, ghosts and trails, the planned route. Follow the Tiguan, pan freely or show the whole drive; 13 selected events with a short explanation each. |
| `stitched.html` | The stitched figure of each event (as `stitch_scenarios/mcap_stitcher.py` renders them for the paper) and the whole-drive map. Vector PDF and SVG (BEV classes as polygons) plus PNG in `stitched/`. |

## Video

`media/drive_2026-11-12_720p.mp4` (720p, H.264, no audio, 72 MB) is the in-car video. It starts with a 26 s explanation; the player keeps the map at the start
until then and follows the video afterwards. Sync: bag time = video time + 25.8 s, found by matching the sideways image motion in the
windshield to the INS yaw rate (correlation 0.75–0.96 in every 80 s window, offset constant within ±0.15 s).

## Data

- Recording: `continuous_2026-11-12T08-24-42.862Z_lichtblick` (Tiguan, ros2_recorder).
- BEV: `/bevfusion/segmentation_image`, placed with the INS pose (`/sensor/ins/oxts_rt3000/gps/odom`).
- Other road users: `/bevfusion/tracked_objects`, cleaned (pieces shorter than 1.5 s and position jumps dropped,
  broken tracks re-joined). "Touareg" is inferred: the moving car that is the policy's nearest agent most of the time.
- Route: `offroad_selfplay.json` (geo_map_v1), resampled to 1 m. Not yet CCMA-smoothed.
- Coordinates are metres relative to the map corner; no absolute GPS positions are on the pages.

## Enable GitHub Pages

Settings → Pages → Build and deployment → Source: *Deploy from a branch*, Branch: `main`, folder `/ (root)`.
A private repository needs a paid GitHub plan for Pages; otherwise make the repository public first.
