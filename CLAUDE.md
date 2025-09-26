# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **brutalist music application** called "SENSOR MUSIC - BRUTALIST INTERFACE" that creates interactive music using device sensors (motion, orientation, accelerometer) as input controllers. The application features a distinctive brutalist design aesthetic with high-contrast visuals and grid-based layouts.

## Development Commands

### Essential Commands
```bash
npm install        # Install dependencies (Vite)
npm run dev        # Start development server
npm run build      # Build for production
npm run preview    # Preview production build
```

### Testing and Linting
Currently no testing framework or linting is configured. The project uses Vite's default configuration without additional code quality tools.

## Architecture

### Core Structure
- **Single-file architecture**: The entire application is contained in `index.html` (919 lines)
- **Vite setup**: Uses Vite as build tool, but all code is inline rather than modularized in `src/`
- **Main class**: `BrutalistSensorMusic` handles all sensor interactions and audio generation

### Key Components
1. **Audio Engine** (Web Audio API)
   - Multiple oscillators with different wave types
   - Real-time frequency and volume modulation
   - Sound envelope controls

2. **Sensor System**
   - Device Orientation API (tilt controls)
   - Device Motion API (shake detection)
   - Fallback to mouse events for desktop

3. **UI Controller**
   - Brutalist design with CSS Grid overlays
   - Real-time sensor value displays
   - Status indicators and visual feedback

### Critical Implementation Details

#### iOS Permission Handling
The application includes iOS-specific permission handling in the `requestPermissions()` method:
```javascript
// Lines 607-626 in index.html
async requestPermissions() {
    if (
        typeof DeviceOrientationEvent !== "undefined" &&
        typeof DeviceOrientationEvent.requestPermission === "function"
    ) {
        // Shows permission prompt and requests access
        const permission = await DeviceOrientationEvent.requestPermission();
    }
}
```

#### Browser Requirements
- Modern browser with Web Audio API support
- Device Orientation/Motion API support (mobile features)
- HTTPS context required for sensor APIs on iOS

#### Known Issues
- Dependencies may not be installed (check if Vite is available)
- No modular code structure - everything in index.html
- No testing or linting configured
- iOS permission system implemented but may need UX improvements

## Development Notes

When working with this codebase:
1. The application is fully self-contained in index.html
2. All styling is inline within <style> tags
3. Brutalist design uses specific color palette (black, white, red, yellow, green, magenta, cyan)
4. Sensor functionality requires testing on actual mobile devices
5. Audio context must be user-initiated (handled via start/stop buttons)