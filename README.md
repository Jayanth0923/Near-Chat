# 🌐 Near Chat — Decentralized P2P Mesh Protocol

[![Flutter Version](https://img.shields.io/badge/Flutter-3.6+-02569B?style=for-the-badge&logo=flutter&logoColor=white)](https://flutter.dev)
[![Platform Support](https://img.shields.io/badge/Android-5.0+ (API 21+)-3DDC84?style=for-the-badge&logo=android&logoColor=white)](https://developer.android.com)
[![Encryption](https://img.shields.io/badge/Security-AES--256--GCM%20Vault-E34F26?style=for-the-badge&logo=security-scorecard&logoColor=white)](#cryptographic-vault)
[![Network Strategy](https://img.shields.io/badge/Strategy-P2P_CLUSTER-orange?style=for-the-badge&logo=broadcom&logoColor=white)](#mesh-protocol)

**Near Chat** (NearNode) is a zero-latency, off-grid communication framework built for environments with zero cellular coverage or internet connectivity. Powered by local Bluetooth and high-speed Wi-Fi cluster mesh technology, it guarantees 100% decentralized, end-to-end encrypted messaging, media streaming, and peer discovery.

---

## 📥 Direct App Download

Get the latest production-ready Android APK directly and start chatting off-grid immediately:

<div align="center">
  <a href="https://drive.google.com/file/d/1mOS7ePOzuNUMpw77jtI3T_orJxjQyVzS/view?usp=sharing" target="_blank">
    <img src="https://img.shields.io/badge/Download_APK-Google_Drive-white?style=for-the-badge&logo=google-drive&logoColor=4285F4&labelColor=0F0F0F" alt="Download APK Button" height="50">
  </a>
</div>

---

## 📸 App Showcase

<div align="center">
  <table border="0">
    <tr>
      <td align="center"><b>1. Discover Peers</b></td>
      <td align="center"><b>2. Enter Room</b></td>
      <td align="center"><b>3. Off-Grid Chat</b></td>
    </tr>
    <tr>
      <td><img src="https://raw.githubusercontent.com/Jayanth0923/Near-Chat/main/Scanning%20Nearprofiles.jpg" width="220" alt="Scanning Nearprofiles"></td>
      <td><img src="https://raw.githubusercontent.com/Jayanth0923/Near-Chat/main/Room%20Code.jpg" width="220" alt="Room Code"></td>
      <td><img src="https://raw.githubusercontent.com/Jayanth0923/Near-Chat/main/Chat%20Screen.jpg" width="220" alt="Chat Screen"></td>
    </tr>
    <tr>
      <td align="center"><b>4. App Settings</b></td>
      <td align="center"><b>5. Profile Setup</b></td>
      <td align="center"><b>6. Interactive Home</b></td>
    </tr>
    <tr>
      <td><img src="https://raw.githubusercontent.com/Jayanth0923/Near-Chat/main/Settings%20screen.jpg" width="220" alt="Settings screen"></td>
      <td><img src="https://raw.githubusercontent.com/Jayanth0923/Near-Chat/main/profile%20setup.jpg" width="220" alt="Profile Setup"></td>
      <td><img src="https://raw.githubusercontent.com/Jayanth0923/Near-Chat/main/Main%20Screen.jpg" width="220" alt="Main Screen"></td>
    </tr>
  </table>
</div>

---

## ⚡ Core Features

*   **100% Offline Messaging**: Communicate locally without mobile data, cellular towers, servers, or active internet connections.
*   **Media & File Sharing**: High-bandwidth offline channel streams images and voice notes directly over peer-to-peer Wi-Fi channels.
*   **QR-Code Instapair**: Generate and scan room code QR cards to automatically establish secure peer channels and exchange handshake data instantly.
*   **Shake to Broadcast**: Triggered via device accelerometer. A rapid physical shake activates emergency broadcast mode, setting up a session, copying the code to the clipboard, and sending beacons.
*   **Premium Glassmorphic UI**: Beautifully optimized Light/Dark themes wrapped in premium frosted-glass visual layers (`BackdropFilter` with blur effects) matching modern visual aesthetics (inspired by Telegram's dynamic styling).
*   **Acoustic & Tactile Chimes**: custom clickless sine-wave notification sound effects (ascending sent chime, descending received chime) with built-in 15% linear amplitude envelopes to prevent pops, combined with medium impact haptic responses.

---

## ⚙️ Technical Specifications & Architecture

```mermaid
graph TD
    A[Near Chat Node] -->|BLE Discovery| B[Peer Discovery]
    A -->|Wi-Fi Direct Stream| C[High-Speed Payloads]
    B -->|QR / Manual Handshake| D[Shared Room Code]
    D -->|PBKDF2 HMAC-SHA256| E[AES-256-GCM Session Key]
    E -->|RAM-Only Volatile Vault| F[Volatile Storage Wiped on Leave]
```

### 📡 Mesh Protocol
*   **Strategy**: `P2P_CLUSTER` via Google's Nearby Connections API.
*   **Discovery**: Bluetooth Low Energy (BLE) advertised beacons allow zero-power device discovery and background mapping.
*   **Transport**: Automatic promotion to Wi-Fi Direct (Wi-Fi P2P) and high-speed local sockets for high-bandwidth media streaming.
*   **Lexicographical Collision Resolution**: Deterministically resolves simultaneous connection requests (Google API Error `8012`) by comparing peer usernames to choose the initiator.
*   **Offline Outbox Sync**: In-flight queues cache outbox frames during momentary radio fade out and automatically flush data once peer connection re-establishes.

### 🔒 Cryptographic Vault
*   **Encryption Standard**: Symmetric **AES-256-GCM** (Galois/Counter Mode) secures all communication frames, providing authenticated encryption and tamper protection.
*   **Key Derivation**: Session keys are derived locally using **PBKDF2** with a **SHA-256 HMAC** (100,000 iterations) from the shared 6-digit Room Code. No keys or master codes are ever transmitted over the air.
*   **Zero-Trace Ephemeral Storage**: Volatile memory design. Messages, decrypted media, and keys are held strictly in RAM. Exiting a room or closing the application triggers a security sweep that permanently clears all session details with zero local disk footprint.

---

## 📱 Hardware & Permission Requirements

To set up local ad-hoc networks without server infrastructure, Near Chat requests the following hardware capabilities:

*   **Near-Field Radios**: Bluetooth (BLE discovery/handshake) and Wi-Fi (ad-hoc streaming socket).
*   **Fine Location**: Required by Android & iOS to perform local BLE scans.
*   **Nearby Devices Permission**: Android 13+ permission for offline local network device discovery without location access.
*   **Microphone**: Record offline voice notes.
*   **Camera**: High-speed QR scanning for secure instant pairing.

---

## 🛠️ Build & Installation

### Prerequisites
*   [Flutter SDK](https://flutter.dev/docs/get-started/install) (v3.6.2 or higher)
*   [Dart SDK](https://dart.dev/tools/sdk) (v3.6.2 or higher)
*   Android SDK (API Level 21+) or iOS SDK (iOS 12.0+)

### Setup Instructions
1.  Clone the repository:
    ```bash
    git clone https://github.com/Jayanth0923/Near-Chat.git
    cd Near-Chat
    ```
2.  Install dependencies:
    ```bash
    flutter pub get
    ```
3.  Analyze codebase:
    ```bash
    flutter analyze
    ```
4.  Run on connected emulator or physical device:
    ```bash
    flutter run
    ```
5.  Build release APK:
    ```bash
    flutter build apk --release
    ```

---

## 🤝 Support & Donate
Near Chat is developed by **Jayanth Muddulur** as a final-year project at RMKCET ('26). 

If you find this decentralized mesh project helpful, consider supporting:
*   **Developer Website**: [ferrypot.in](https://ferrypot.in)
*   **UPI ID**: `jayanthmuddulurt2004-1@oksbi`
