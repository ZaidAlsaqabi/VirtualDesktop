# Virtual Desktop Demo

This project demonstrates a basic **virtual desktop environment** using **Three.js**. It allows users to stream their desktop onto a virtual monitor in a 3D scene, viewable in VR mode.

## Features
- **Virtual Monitor**: A 16:9 aspect ratio plane representing a monitor.
- **Desktop Streaming**: Streams the user's desktop using the WebRTC API (`getDisplayMedia`).
- **VR Mode**: Fully VR-compatible using Three.js's VR capabilities and `VRButton`.

## How It Works
1. **Scene Setup**:
   - A Three.js scene with a camera, renderer, and ambient light.
   - A virtual monitor (plane geometry) is positioned in the 3D scene.

2. **Desktop Capture**:
   - The `navigator.mediaDevices.getDisplayMedia` API streams the desktop.
   - The stream is rendered as a texture (`VideoTexture`) on the virtual monitor.

3. **VR Integration**:
   - The project includes a VR button for entering VR mode using the Three.js `VRButton`.

## Usage
1. Clone or download the project.
2. Open the `index.html` file in a WebXR-compatible browser.
3. Click the "Start Desktop Capture" button to begin streaming your desktop onto the virtual monitor.
4. Enter VR mode using the VR button to experience the virtual desktop in a VR headset.

## Dependencies
- [Three.js](https://threejs.org/)
  - Includes `VRButton` for VR compatibility.

## Code Example
```html
const monitorGeometry = new THREE.PlaneGeometry(4, 2.25);
const monitorMaterial = new THREE.MeshBasicMaterial({ color: 0x000000 });
const monitor = new THREE.Mesh(monitorGeometry, monitorMaterial);
scene.add(monitor);

async function startDesktopCapture() {
    const stream = await navigator.mediaDevices.getDisplayMedia({ video: true });
    const video = document.createElement('video');
    video.srcObject = stream;
    video.play();
    monitor.material.map = new THREE.VideoTexture(video);
    monitor.material.needsUpdate = true;
}
```

## License
This code is provided for educational purposes and may be modified and used freely.

