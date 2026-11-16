# Flyby Change Detection

Fly a slow pass over a site with a cheap drone. Build a 3D map from the video alone. Fly again later. The computer localizes the second pass against the first map with no GPS, then reports what changed and where, in meters.

This is a separate project from `/Users/srijan/Documents/Dodgeball Drone/`. Separate folder, separate git repo. Do not merge them.

## Why this problem

- GPS-denied navigation: GPS jamming is a live problem. A drone must know where it is from video alone. This is what visual-inertial systems like Skydio's are built for.
- Change detection on a patrol route: "what is new since the last pass" is a core question for perimeter security and site checks.
- Object geolocation: reporting an object's position on a map is the kind of shared picture operators use.

Framing: site mapping and change detection. No tracking of people who have not agreed to it. If people appear, they are consenting volunteers in a search-and-rescue style test.

## Hardware

- Ascend Aeronautics ASC-2400 (toy drone): 720p, 25 fps, video to a phone app, 2.4 GHz remote, altitude hold only. Pilot flies it by hand. No computer control, no modification of the remote.
- Phone to record or move clips (confirm the app can save clips; unverified).
- Laptop (Mac, no GPU path for COLMAP, so it is slow but workable for 1 to 2 minute clips; unverified).
- Props: cones, boxes, a cardboard "vehicle". Tape measure.
- Extra cost target: about $0.

## Plan

Stage 0: confirm the ASC-2400 app saves clips and that I can get them onto the laptop. Check weight and local drone rules (US: TRUST certificate and Remote ID apply above 250 g).

Stage 1: no-flight pipeline check. Walk a textured yard with a phone, 1 minute video. Run COLMAP. Does it recover the camera path and a point cloud?

Stage 2: scale. Fix scale from one tape-measured distance between two fixed features. No markers.

Stage 3: ASC-2400 flyby, pass 1. Build the map from its video. Record how good the 720p, rolling-shutter video is for mapping.

Stage 4: pass 2 after adding, moving or removing props. Localize pass 2 against the pass 1 map without GPS.

Stage 5: change detection. Compare the two, list what changed with x, y, z positions.

Stage 6: score it. Position error against tape measure. Detections, misses, false alarms. Failure cases with video.

## Honest limits (estimates, to be measured)

- 720p video with rolling shutter and heavy compression can break structure from motion.
- Plain, textureless surfaces will fail. Test on a textured area such as grass, brick or a cluttered garage.
- Accuracy will be rough, not survey grade. The claim is a measured small-scale test, not a product.

## Safety

- Fly only over my own space, clear of other people, with an adult present.
- Keep the drone in sight. Land if it drifts or video lags.
- Check the drone's weight and legal rules before the first flight.

## Results table (fill with real numbers only)

| Measure | Value | Stage |
|---|---|---|
| Pipeline works on phone walk video | not tested | 1 |
| Scale error (cm over a known distance) | not measured | 2 |
| Localization success of pass 2 | not measured | 4 |
| Position error of changed objects (cm) | not measured | 6 |
| Detections, misses, false alarms | not measured | 6 |

## Log

2026-11-15: scope set. Nothing built or flown.
