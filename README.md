# Acid_Video & Acid_Audio

**Acid_Video** is a procedural video generator that leverages FFmpeg and Bash to create algorithmic visual patterns. It supports various mathematical and chaotic generators, along with a stackable modifier system for real-time visual effects.

**Acid_Audio** is a bash-based synthesizer that generates procedural 8-bit Drum & Bass entirely from mathematical formulas (bytebeat). Whether you want to jam locally, record your sessions, or stream chaotic noise to the world, this shell script has you covered.


## Acid_Video Features

- **Procedural Generation**: Generate unique video patterns using various algorithms:
    - `urandom`: Raw entropy stream.
    - `seq`: Standard test source sequence.
    - `fibonacci`: Golden ratio spiral-based mathematical visualizations.
    - `fourier`: Tri-channel interference patterns using sine/cosine functions.
    - `fractal`: Mandelbrot set visualization.
    - `perlin`: Organic clouds/smoke using Perlin noise.
    - `reaction`: Reaction-Diffusion patterns (stripes/mazes).
    - `voronoi`: Voronoi cellular/mosaic patterns.
    - `chaos`: Lorenz/Chaos orbits visualization.
    - `life`: Conway's Game of Life simulation.
- **Visual Modifiers**: Apply effects like zoom, hue shift, pixelation, and edge detection.
- **Customizable**: Configure output resolution, frame rate, and duration.
- **Streaming Support**: Stream directly to RTSP, SRT, or other FFmpeg-supported protocols.

## Acid_Audio Features

- **Procedural Audio Generation**: Creates endless, non-repeating 8-bit audio loops using C-style bitwise expressions.
- **Live Mixing**: Layer multiple formulas, distort them, or boost them in real-time.
- **Multi-Mode Output**:
  - **Local Playback**: Listen directly via `aplay`.
  - **Recording**: Save your sessions to `.mp3` files.
  - **Streaming**: Push your audio to SRT, RTSP, or RTSPS endpoints using `ffmpeg`.
- **Seamless Updates**: Audio engine uses atomic binary swapping for immediate audio synthesis without dropouts.
- **Secure Input**: Strict allowlists for formulas and network endpoints prevent command injection and arbitrary code execution.

  

## Prerequisites

To use this tool, ensure you have the following installed on your system:

- **FFmpeg**: The core engine used for video generation, recording and streaming features (`sudo apt install ffmpeg`).
- **Bash**: Required to execute the generation script.
- **Git**: Required for the self-update feature.
- **GCC**: To compile the bytebeat formulas (`sudo apt install build-essential`).
- **ALSA Utils (`aplay`)**: For local playback (`sudo apt install alsa-utils`).
- **Curl** or **Wget**: For the self-update feature.

## Acid_Video Usage

Use the `Acid_Video.sh` script to generate a video.

```bash
./Acid_Video.sh -t <type> -s <widthxheight> -f <fps> [-d <duration>] [modifiers] [-stream <url> | -save [filename]]
```

### Arguments

- `-t <type>`: **Type** of generator (`urandom`, `seq`, `fibonacci`, `fourier`, `fractal`, `perlin`, `reaction`, `voronoi`, `chaos`, `life`).
- `-s <WxH>`: **Size** (resolution) in `WxH` format (e.g., `1280x720`).
- `-f <fps>`: **Frame Rate** (FPS) (integer between 1 and 60).
- `-d <sec>`: **Duration** in seconds (optional). If omitted, the script runs indefinitely until interrupted (Ctrl+C).
- `-stream <url>`: Stream to the specified URL (e.g., `rtsp://localhost:8554/mystream` or `srt://...`).

### Arguments

- `-t <type>`: **Type** of generator (`urandom`, `seq`, `fibonacci`, `fourier`, `fractal`, `perlin`, `reaction`, `voronoi`, `chaos`, `life`).
- `-s <WxH>`: **Size** (resolution) in `WxH` format (e.g., `1280x720`).
- `-f <fps>`: **Frame Rate** (FPS) (integer between 1 and 60).
- `-d <sec>`: **Duration** in seconds (optional). If omitted, the script runs indefinitely until interrupted (Ctrl+C).
- `-stream <url>`: Stream to the specified URL (e.g., `rtsp://localhost:8554/mystream` or `srt://...`).
- `-save [file]`: Save output to a file. If no filename is provided, a default `AcidVideo_<type>_...webm` file is created.
- `--update`: Self-update the script from GitHub (must be used as the only argument).

*Note: `-stream` and `-save` are mutually exclusive.*

### Modifiers

You can combine multiple modifiers to alter the visual output. They are applied in a preset order.

- `-luma`: Enable Luma Keying (transparency based on brightness).
- `-hue`: Enable Dynamic Hue Shift.
- `-tint`: Enable Color Tint.
- `-vignette`: Enable Vignette effect.
- `-zoom`: Enable Dynamic Zoom.
- `-lagfun`: Enable Lagfun (trails/decay).
- `-pixelate`: Enable Pixelation (Mosaic).
- `-edge`: Enable Edge Detection.

## Examples

**Generate a Fibonacci pattern saved to file:**
Create a 10-second video at 640x480 resolution and 30 FPS.

```bash
./VLX_Acid_Video.sh -t fibonacci -s 640x480 -f 30 -d 10 -save
```
- `-save [file]`: Save output to a file. If no filename is provided, a default `AcidVideo_<type>_...webm` file is created.
- `--update`: Self-update the script from GitHub (must be used as the only argument).

*Note: `-stream` and `-save` are mutually exclusive.*

### Modifiers

You can combine multiple modifiers to alter the visual output. They are applied in a preset order.

- `-luma`: Enable Luma Keying (transparency based on brightness).
- `-hue`: Enable Dynamic Hue Shift.
- `-tint`: Enable Color Tint.
- `-vignette`: Enable Vignette effect.
- `-zoom`: Enable Dynamic Zoom.
- `-lagfun`: Enable Lagfun (trails/decay).
- `-pixelate`: Enable Pixelation (Mosaic).
- `-edge`: Enable Edge Detection.

## Examples

**Generate a Fibonacci pattern saved to file:**
Create a 10-second video at 640x480 resolution and 30 FPS.

```bash
./VLX_Acid_Video.sh -t fibonacci -s 640x480 -f 30 -d 10 -save
```

**Stream a Reaction-Diffusion pattern with modifiers:**
Stream indefinitely to a local RTSP server with zoom and hue shift effects.

```bash
./VLX_Acid_Video.sh -t reaction -s 1280x720 -f 60 -zoom -hue -stream rtsp://localhost:8554/live
```

**Generate a Game of Life simulation with pixelation:**
Run a Game of Life simulation with a pixelated look.

```bash
./VLX_Acid_Video.sh -t life -s 800x600 -f 24 -pixelate -save output.webm
```


## Acid_Audio Usage

First, make the script executable:
```bash
chmod +x Acid_Audio.sh
```

### 1. Local Playback
Start the sequencer and listen on your default audio device:
```bash
./Acid_Audio.sh
```
Or start with a specific seed formula:
```bash
./Acid_Audio.sh "t*(t>>10|t>>8)&123"
```

### 2. Recording
Record your session directly to an MP3 file:
```bash
./Acid_Shell.sh file [filename.mp3]
```
*If no filename is provided, it defaults to a timestamped file (e.g., `Acid_Shell_2023-10-27_123045.mp3`).*

### 3. Streaming
Broadcast your noise to a remote server or media gateway.

**SRT (Secure Reliable Transport):**
```bash
./Acid_Audio.sh srt 127.0.0.1:9000
```

**RTSP (Real Time Streaming Protocol):**
```bash
./Acid_Audio.sh rtsp 192.168.1.10:8554/live
```

**RTSPS (Secure RTSP):**
```bash
./Acid_Audio.sh rtsps 192.168.1.10:322/live
```

### 4. Help
View the built-in help menu and version info:
```bash
./Acid_Audio.sh help
```

## Interactive Commands

Once the shell is running, you are the conductor. Use these commands to manipulate the soundscape:

- **`[ENTER]`**: Add a random layer to the mix.
- **`a <formula>`**: Add a specific bytebeat formula (e.g., `a t>>4`).
  - *Allowed characters*: `0-9 t + - * / % & | ^ ( ) < > ~` and spaces.
- **`d <id>`**: Delete a specific layer by its ID (check the Tracklist).
- **`s`**: Save the current formula configuration to `Acid_Shell_saves.txt`.
- **`r`**: Reset everything to a fresh start.
- **`q`**: Quit the session.

## Updates

Keep your shell fresh with the built-in update command:
```bash
./Acid_Audio.sh update
```

## Technical Notes

- **Temporary Files**: The script creates a temporary directory in the current working directory (e.g., `./tmp_<timestamp>_<PID>`) to store compiled binaries. This directory is automatically cleaned up when the script exits.

---
## License

This project is licensed under the GNU General Public License v3.0 (GPLv3). See the `LICENSE` file for details.

