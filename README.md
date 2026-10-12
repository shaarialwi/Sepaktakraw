# Sepak Takraw 3D Tracker — Manual Match Video Analysis

A single-file, GitHub Pages–ready website showing a 3D-style sepak takraw court, player positions, simulated replay data, and a browser-based manual video analysis workspace.

## Start

1. Open `index.html` in a modern desktop browser, or publish it on GitHub Pages.
2. Under **MATCH VIDEO**, use the native **Choose File** control or drag-and-drop to load an MP4/WebM or **YouTube URL** to paste a public match link.
3. Start playback using the video player. Pause and seek to a moment you want to annotate. You can use the **Go to time** control (`MM:SS`) to set the analysis playhead. For local files it also seeks the video.
4. Under **MANUAL ANALYSIS**, select a player's marker (A1–A3 / B1–B3) or **Ball**. Choose **Top view** for easier positioning, and click the relevant location on the court. Ball height can be adjusted with its slider.
5. Select an event and player, optionally write a note, and click **Save event at current video time**.
6. Export JSON and save it locally. Use **Import analysis** to restore your annotated positions and events. Reattach the exact matching video file or YouTube ID to continue reviewing without losing the imported annotations.

## What is implemented

- Simulated three-rally sample with animated 3D-style movement, net, ball and estimated distances.
- Local browser video upload with HTML5 video controls, seeking, play/pause, and playback speed.
- YouTube iframe embed for watch links, short links, and shorts/live/embed URLs, with YouTube IFrame API integration when available, plus an **Open video on YouTube** fallback.
- Manual time entry if YouTube player access, time sync, or playback is restricted.
- Annotating six players' court positions by clicking on the 3D court; dedicated ball placement and height controls.
- Saving timestamped serve, receive, set, spike, roll spike, block, dig, point, fault and other rally events.
- Downloading/importing analysis JSON, including frame coordinates, source metadata, and events.
- Existing coordinate JSON import, demo JSON export, camera orbit, overhead camera, and movement trails.

## Important limitations

**This is a manual-analysis prototype, not an automatic AI player tracker.** Selecting a YouTube link or uploading a video does not extract players or the ball from footage. Simulated data is not a real match measurement. In manual-review mode, speed and distance statistics are only approximations derived from your manually placed position markers and are hidden until at least two positions are logged for that player.

Video stays local in your browser; this website does not upload or store your file. YouTube video content is played via YouTube's embedded player; some creators disable embedding. YouTube API functions such as seeking and getting current playback time may be unavailable due to the browser, network, or owner restrictions. When unavailable, use the embedded player's controls and manually align the analysis time field. YouTube videos are not downloaded by this project.

The exported JSON does not contain the underlying match video. Keep the source file/YouTube link separately. This prototype does not have cloud accounts, database persistence or collaborative editing.

## GitHub Pages

1. Create a public or private repository where GitHub Pages is enabled for your plan.
2. Upload `index.html` to the repository root and commit it.
3. In repository **Settings → Pages**, choose **Deploy from a branch**, select branch `main` and folder `/(root)`, then save.
4. Open your published URL once Pages finishes deploying.

No Node, build step, or server is needed. The code uses plain HTML, CSS, and JavaScript. Internet access is required for YouTube playback and integration.

## Analysis JSON

Exports use `format: "takraw-manual-analysis-v1"` and include `meta`, `positions`, `events`, `frames` for replaying the manually annotated positions. The court uses metres: length 13.4 m, width 6.1 m, with coordinates x in [-6.7, +6.7] and y in [-3.05, +3.05].

## Troubleshooting: nothing happens after choosing a video or pasting YouTube URL

- **Use the updated version:** An earlier layout squeezed the video panel to a small height and clipped the video player even when the link had loaded. The updated `index.html` fixes this by keeping its panels at their natural height and making the sidebar scrollable.
- **In ChatGPT or an online HTML preview:** Preview pages may sandbox JavaScript, file picking and YouTube iframes. Download the HTML and open in Chrome, or test from the published GitHub Pages URL.
- **Local video:** Use the visible native **Choose File** button or drag a file onto the dashed drop zone. Prefer an H.264-encoded MP4 or WebM. Video is not uploaded to a server.
- **YouTube:** Switch to **YouTube URL**, paste the Share link, then click **Load Video**. If embedding is not allowed, choose **Open video on YouTube** to watch the match directly and enter timestamps into the tracker manually. No static HTML page can force a video to allow embedding.
- **After replacing on GitHub:** Wait for the Pages deployment to complete, then hard-refresh using Cmd+Shift+R on Mac / Ctrl+Shift+R on Windows.
