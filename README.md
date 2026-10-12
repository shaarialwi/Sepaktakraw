# Sepak Takraw 3D Player Tracker — Interactive Prototype

An HTML-only, browser-based demonstration of a sepak takraw match movement tracker. No server, build process, or API key is needed for the **demo**.

## Features
- Isometric/overhead 3D-style court, using 13.4 m × 6.1 m dimensions with both service circles, four quarter-circles and a net.
- Six labelled players (Tekong, Left Inside, Right Inside for each regu).
- Animated ball, scripted player positions, and selectable example rallies.
- Contact timeline, prev/next, pause/play, playback speed, trails, zoom and drag-to-orbit.
- Movement metrics, speeds and distances calculated from demo coordinates.
- Local video file preview (reference **only** — not synchronized with position data).
- Export/import of tracked player coordinate JSON.
- Responsive desktop and mobile layout.

**Important**: Included player coordinates, scores, plays and team names are illustrative demo data. Uploading a video does **not** detect players, track the ball or generate tracking coordinates. This requires a separate computer-vision backend.

## Try it locally
Double-click `index.html` in your browser. No installation needed.

## Publish to GitHub Pages
1. Create a new repository on GitHub (e.g. `takraw-tracker`).
2. Upload `index.html` to the repository root, and commit.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch** and select **main** and **/(root)**; click **Save**.
5. After deployment, visit `https://YOUR-USERNAME.github.io/takraw-tracker/`.

## Coordinate JSON format
A sample file, `sample_tracking.json`, is provided. Click **Tracking JSON** in the interface to import it.

```json
{
  "frames": [
    { "t": 0.0,
      "players": [
        {"id":"A1", "x":-4.25, "y":0, "z":0},
        {"id":"A2", "x":-1.35, "y":-2, "z":0},
        {"id":"A3", "x":-1.35, "y":2, "z":0},
        {"id":"B1", "x":4.25, "y":0, "z":0},
        {"id":"B2", "x":1.35, "y":2, "z":0},
        {"id":"B3", "x":1.35, "y":-2, "z":0}
      ],
      "ball":{"x":-4.25, "y":0, "z":1.2}
    },
    { "t": 1.0,
      "players": [
        {"id":"A1", "x":-4.25, "y":0, "z":0},
        {"id":"A2", "x":-1.35, "y":-2, "z":0},
        {"id":"A3", "x":-1.35, "y":2, "z":0},
        {"id":"B1", "x":4.25, "y":0, "z":0},
        {"id":"B2", "x":1.35, "y":2, "z":0},
        {"id":"B3", "x":1.35, "y":-2, "z":0}
      ],
      "ball":{"x":0, "y":0, "z":2.1}
    }
  ]
}
```

`x`: court long axis in metres (-6.7 to +6.7), where **team A/Perak** is negative and **team B/Terengganu** is positive. `y`: cross-court axis (-3.05 to +3.05). `z`: height above floor in metres. `t`: seconds from the start of the rally. IDs A1/A2/A3, B1/B2/B3 are the six players. The renderer linearly interpolates positions between supplied timestamps.

## Path to real video-based tracking
1. Accept footage and prepare a calibration of the court corners and perspective/homography.
2. Run player/ball detection plus person identity tracking, using a Python backend (e.g. OpenCV + a fine-tuned detector and multi-object tracker). Detecting a fast small ball typically requires specialist training and frame-rate considerations.
3. Fit player foot locations onto the calibrated court, filter track jitter, classify touches and attacks (where supported by data).
4. Export timestamped player and ball coordinates in the JSON schema above. 3D ball height inferred from a single viewpoint is approximate; a calibrated multi-camera setup is better for reliable vertical trajectories.
5. For production, use authenticated storage, consent/access policies and appropriate rights to video footage.

The dashboard is compatible with GitHub Pages because it is static, but **computer vision inference would run on a separate service**, not on GitHub Pages itself.
