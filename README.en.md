# Mechanical Stop Watch

An interactive mechanical stopwatch component built with Vue 3, TypeScript, and Vite. The project recreates the look and feel of a physical stopwatch with layered image assets, rotating hands, precise crown hit detection, and a mechanical ticking sound.

[中文 README](./README.md)

## Features

- Mechanical stopwatch visuals: composed from separate dial, hand, crown, and hover indicator image layers.
- Accurate elapsed time: powered by `performance.now()` and `requestAnimationFrame`.
- Two-hand display: the second hand completes a full turn every 60 seconds, and the minute hand completes a full turn every 60 minutes.
- Crown interaction: click the crown to start or pause, and double-click the crown to reset while stopped.
- Precise hit testing: reads the alpha channel from the crown mask image to detect whether the pointer is inside the clickable crown area.
- Sound feedback: plays a ticking mechanical sound while the stopwatch is running and stops it when paused.
- Responsive sizing: keeps the original stopwatch aspect ratio while scaling to fit the available width.

## Tech Stack

- Vue 3
- TypeScript
- Vite
- HTML Canvas for reading the crown mask alpha channel
- Web Audio / `HTMLAudioElement` for ticking sound playback

## Getting Started

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

Build for production:

```bash
npm run build
```

Preview the production build locally:

```bash
npm run preview
```

## Usage

After starting the project, interact with the stopwatch on the page:

- Move the pointer over the crown area to show the crown hover indicator.
- Single-click the crown to start or pause the stopwatch.
- Double-click the crown to reset the timer. The current implementation resets only when the stopwatch is stopped.

Modern browsers may require a user interaction before allowing audio playback because of autoplay policies.

## Project Structure

```text
.
├── public/
│   ├── assets/
│   │   ├── MechanicalStopwatch/   # Stopwatch dial, crown, hands, and related image assets
│   │   └── audio/                 # Mechanical ticking sound
│   └── favicon.svg
├── src/
│   ├── common/
│   │   ├── MechanicalStopwatch/
│   │   │   ├── MechanicalStopwatch.vue
│   │   │   └── MechanicalStopwatch.ts
│   │   └── audiotool/
│   │       └── PlayAudio.ts
│   ├── App.vue
│   ├── main.ts
│   └── style.css
├── index.html
├── package.json
└── vite.config.ts
```

## Implementation Notes

`src/common/MechanicalStopwatch/MechanicalStopwatch.vue` defines the component template and layered layout. The dial, hover indicator, minute hand, and second hand are stacked with absolute positioning, and the hands rotate through dynamic `transform` styles.

`src/common/MechanicalStopwatch/MechanicalStopwatch.ts` contains the stopwatch state and interaction logic, including elapsed-time tracking, hand rotation calculation, crown hit detection, click and double-click handling, and sound control.

`src/common/audiotool/PlayAudio.ts` wraps audio playback and cleanup. It supports repeated playback and stops the active audio when the stopwatch is paused.

## Assets

Stopwatch image assets are stored in `public/assets/MechanicalStopwatch/`, and the sound effect is stored in `public/assets/audio/`. These resources are served from Vite's public directory and can be referenced with root-relative paths, for example:

```ts
/assets/MechanicalStopwatch/MechanicalStopwatch.png
/assets/audio/TickdaTickda.wav
```

If you replace the image assets later, also review the dial size, hand pivot coordinates, and crown mask configuration in `MechanicalStopwatch.ts`.
