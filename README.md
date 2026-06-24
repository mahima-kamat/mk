# WebRTC Screen Sharing Application

A high-performance, secure peer-to-peer screen streaming application built using **React (Vite)**, **Socket.io**, and **WebRTC (RTCPeerConnection)**. It is styled with a modern glassmorphic dark theme and features real-time connection status indicators.

---

## How it Works
1. **Signaling Server (Socket.io)**: Helps the two computers find each other, exchange WebRTC offers, answers, and ICE candidates, and coordinate room memberships.
2. **Peer-to-Peer Stream (WebRTC)**: Once the connection is negotiated, the screen video stream is transmitted directly between the two browsers without passing through any server.
3. **Secure Context (HTTPS)**: Browsers enforce a security rule that `navigator.mediaDevices.getDisplayMedia` (screen sharing) can only be accessed on secure pages (`localhost` or `https://`). If accessed via plain `http://` on an external IP, the browser will block screen sharing.

---

## Quick Start (Localhost Testing)

You can test the entire connection in two browser tabs on the same computer:

### 1. Install Dependencies
Make sure you are in the project folder and run:
```bash
npm install
```

### 2. Start the Signaling Server
Runs on `http://localhost:5000`:
```bash
npm run server
```

### 3. Start the React App
Runs on `http://localhost:5173`:
```bash
npm run dev
```

### 4. Test it
1. Open `http://localhost:5173` in **Tab A**.
2. Open `http://localhost:5173` in **Tab B**.
3. In both tabs, enter the **same Room ID** (e.g., `XYZ`) and click **Join Room**.
4. In **Tab A** (Sender), click **Start Screen Share** and select a screen/window to share.
5. In **Tab B** (Receiver), you will instantly see the live preview of Tab A's screen!

---

## Testing Across Different Devices (HTTPS Tunneling)

If you want to open the app on your desktop and a different computer (like a laptop or phone) and have one be the **Sender** and the other the **Receiver**, you need a secure `https://` connection.

The easiest, free way to do this is using a tunnel tool like **ngrok** or **localtunnel**.

### Method 1: Using localtunnel (Quickest, no signup needed)

1. With your React app running on `5173` and server on `5000`, open a new terminal.
2. Run **localtunnel** for the React frontend:
   ```bash
   npx localtunnel --port 5173
   ```
   This will give you a public URL like: `https://slimy-grapes-run.loca.lt`
3. Run **localtunnel** for the Socket.io backend in another terminal:
   ```bash
   npx localtunnel --port 5000
   ```
   This will give you a backend URL like: `https://silent-moose-wave.loca.lt`
4. **On both devices**:
   - Open the frontend URL (e.g., `https://slimy-grapes-run.loca.lt`).
   - Paste the backend URL (e.g., `https://silent-moose-wave.loca.lt`) into the **Signaling Server URL** input field.
   - Enter the same Room ID (e.g., `XYZ`) and click **Join Room**.
   - Start sharing from one device, and it will stream live to the other!

### Method 2: Using ngrok (Very stable)

1. Download and install [ngrok](https://ngrok.com/).
2. Expose your React dev server:
   ```bash
   ngrok http 5173
   ```
   Copy the secure `https://...` forwarding URL.
3. Expose your Socket.io backend server in a separate terminal:
   ```bash
   ngrok http 5000
   ```
   Copy the backend `https://...` forwarding URL.
4. Paste the backend URL into the **Signaling Server URL** input box in the browser on both machines, enter the same Room ID, and connect!

---

## Code Directory Structure
- [App.jsx](file:///C:/Users/mahim/OneDrive/Desktop/Ai/screen-share-app/src/App.jsx) - Main frontend component containing WebRTC & Socket.io client handlers.
- [index.css](file:///C:/Users/mahim/OneDrive/Desktop/Ai/screen-share-app/src/index.css) - Premium CSS variables, responsive design, animations, and UI styling.
- [server.js](file:///C:/Users/mahim/OneDrive/Desktop/Ai/screen-share-app/server.js) - Node.js Express & Socket.io server to coordinate signaling events.
- [package.json](file:///C:/Users/mahim/OneDrive/Desktop/Ai/screen-share-app/package.json) - Node dependencies and run scripts.
