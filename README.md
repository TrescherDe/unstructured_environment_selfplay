# Self-Play Reinforcement Learning for Interactive Driving in Unstructured Environments

Project page for the real-car self-play tests in unstructured (off-road) environments:
two vehicles (Vehicle A and Vehicle B) driving with the RL motion planner.

Live page: <https://treschede.github.io/unstructured_environment_selfplay/> (after GitHub Pages is enabled, see below).

## Pages

| page | what it shows |
|---|---|
| `index.html` | Replay of the 2026-11-12 Vehicle A drive (52–700 s) next to the synchronised in-car video: Vehicle A's live BEV over the stitched map, the road users its tracker sees with their trails, the planned route, and timed comments on what the car does. Follow Vehicle A, pan freely or show the whole drive. |
| `stitched.html` | The stitched figure of each event (as `stitch_scenarios/mcap_stitcher.py` renders them for the paper) and the whole-drive map. Vector PDF and SVG (BEV classes as polygons) plus PNG in `stitched/`. |

## Video

`media/drive_2026-11-12_720p.mp4` (720p, H.264, no audio, 72 MB) is the in-car video. It starts with a 10 s still and a 16 s explanation; the player skips the still
(playback starts at video 10 s), keeps the map at the start during the explanation and follows the video afterwards. Sync: bag time = video time + 25.8 s, found by matching the sideways image motion in the
windshield to the INS yaw rate (correlation 0.75–0.96 in every 80 s window, offset constant within ±0.15 s).

## Data

- Recording: `continuous_2026-11-12T08-24-42.862Z_lichtblick` (Vehicle A, ros2_recorder).
- BEV: `/bevfusion/segmentation_image`, placed with the INS pose (`/sensor/ins/oxts_rt3000/gps/odom`).
- Other road users: `/bevfusion/tracked_objects`, cleaned (pieces shorter than 1.5 s and position jumps dropped,
  broken tracks re-joined). "Vehicle B" is inferred: the moving car that is the policy's nearest agent most of the time.
- Route: `offroad_selfplay.json` (geo_map_v1), resampled to 1 m. Not yet CCMA-smoothed.
- Coordinates are metres relative to the map corner; no absolute GPS positions are on the pages.

## Enable GitHub Pages

Settings → Pages → Build and deployment → Source: *Deploy from a branch*, Branch: `main`, folder `/ (root)`.
A private repository needs a paid GitHub plan for Pages; otherwise make the repository public first.
