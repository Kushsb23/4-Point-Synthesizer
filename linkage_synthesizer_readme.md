# 4-Bar Linkage Synthesizer

An interactive, web-based engineering tool for designing and visualizing 4-bar mechanisms. This application allows users to synthesize linkages that pass through four defined target points using both **Analytical** (computational) and **Graphical** (geometric) methods.

## ✨ Features

* **Dual Synthesis Modes**:
  * **Analytical Mode**: Utilizes a high-performance Web Worker to solve complex dyad equations (Burmester theory), evaluating over 1.3 million permutations in milliseconds to find exact or fallback 3-point solutions.
  * **Graphical Mode**: A guided, step-by-step interactive geometric construction tool using midnormals and intersecting arcs to manually lock in ground hinges (HC, HR) and moving pivots.
* **2D & 3D Visualization**:
  * **2D Canvas View**: Crisp, blueprint-style rendering with pan, zoom, path tracing, and real-time coordinate tracking.
  * **3D View**: Fully modeled 3D rendering powered by Three.js, complete with orbit controls, dynamic lighting, and depth. (Automatically switches to Dark Mode).
* **Kinematic Analysis**: Real-time classification of the linkage's Grashof condition (e.g., Crank-Rocker, Double Rocker, Double Crank) and exact link length calculations.
* **Circuit Defect Resolution**: Automatically detects circuit defects and provides a built-in toggle to switch linkage branch configurations (Config 1 vs Config 2).
* **Live Animation & Playback**: Adjust animation speed, visualize crank/rocker sweeps, and trace the coupler curve dynamically.

## 🚀 How to Use

### Getting Started
1. Clone or download the repository.
2. Open `index.html` in any modern web browser. (No local server required, though an internet connection is needed to fetch the Three.js library).

### Analytical Synthesis
1. Click anywhere on the 2D canvas to define **4 target points** (P1, P2, P3, P4) that you want the mechanism's coupler to pass through.
2. Click **Run Synthesizer**.
3. The background Web Worker will calculate the optimal linkage.
4. Once generated, click **Play Animation** to see the mechanism in motion. 
5. Toggle to **3D View** to inspect the generated geometry.

### Graphical Synthesis
1. Click the **Analytical/Graphical** toggle to switch modes.
2. Define your 4 target points on the canvas.
3. **Step 1 & 2**: Select 2 target points to generate a midnormal line. Hover near the line to snap, and click to lock the Rocker Ground Hinge (**HR**).
4. **Step 3**: Adjust the Outer Radius (**R**) and Inner Radius (**r**) sliders. The system will mathematically scan for a valid Crank Ground Hinge (**HC**). If a green dot appears, click it to lock it in.
5. **Step 4**: Click **Generate Mechanism** to finalize the linkage and animate it.

## 🧠 Under the Hood

* **Frontend**: Pure HTML5, CSS3, and ES6 JavaScript. No heavy frontend frameworks used.
* **Math Engine**: The analytical solver implements complex number formulations of the standard dyad equations for rigid body guidance. It runs asynchronously in a JavaScript `Worker` to prevent UI freezing during heavy calculations.
* **Rendering**: 
  * 2D rendering uses the native HTML5 `<canvas>` API.
  * 3D rendering uses [Three.js](https://threejs.org/) (`r128` via CDN) to procedurally generate extruded geometries for the linkages, pins, and ground plates.

## 🛠️ File Structure

The entire application is self-contained within a single HTML file:
* **CSS**: Handles the UI layout, responsive toggles, sliders, and Light/Dark mode variables.
* **Web Worker (Inline)**: A stringified JavaScript worker block that handles the `solveDyad4Pos_fast` math.
* **Main Script**: Manages the Three.js scene, Canvas 2D context, UI event listeners, state management, and graphical construction logic.

## 📝 License
This project is open-source and free to use for educational, academic, and personal engineering projects.