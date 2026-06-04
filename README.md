# 🚀 NHAI Netra

### Secure Offline Facial Recognition & Liveness Detection System

### Hackathon 7.0 Submission

---

# Problem Statement

Develop a mobile-based secure offline facial recognition and liveness detection system capable of authenticating field personnel in remote and zero-network locations while maintaining high accuracy, low latency, and lightweight deployment on standard mobile devices.

---

# Our Solution

NHAI Netra is a fully offline facial authentication system developed using React Native and TensorFlow Lite, specifically designed for field operations in remote environments where internet connectivity is unavailable.

Unlike conventional cloud-based authentication systems, the entire authentication pipeline executes directly on the mobile device without requiring any network connection.

The system authenticates personnel through a multi-stage verification process consisting of:

1. Video-based user verification
2. Offline liveness detection
3. Face quality enhancement
4. Face recognition using an optimized YOLO Classification model
5. Local secure storage
6. Automatic cloud synchronization when connectivity becomes available

---

# System Workflow

```text
3–5 Second Video Capture
           │
           ▼
Frame Extraction
(10 Equal Interval Frames)
           │
           ▼
ML Kit Face Detection
           │
           ▼
Liveness Detection
(Blink + Smile Verification)
           │
   ┌───────┴────────┐
   │                │
Failed          Passed
   │                │
Request New      Select Best Face
Video Input      (Largest Bounding Box)
                    │
                    ▼
Image Enhancement
(Blur Removal + Noise Reduction)
                    │
                    ▼
Face Cropping
                    │
                    ▼
YOLO Classification Model
                    │
                    ▼
Identity Recognition
                    │
                    ▼
Authentication Result
                    │
                    ▼
Local Storage
                    │
                    ▼
Auto Sync to MongoDB
When Internet Available
```

---

# Detailed Working

## Step 1: Video-Based Authentication

The user records or uploads a short video of approximately 3–5 seconds.

Using video rather than a single image allows the system to verify natural facial movements and perform liveness analysis.

This approach significantly reduces spoofing attacks caused by printed photographs or mobile screen replays.

---

## Step 2: Frame Extraction

The captured video is divided into 10 equally spaced frames.

These frames provide temporal information required for liveness verification while keeping computational overhead extremely low.

---

## Step 3: Offline Liveness Detection

Google ML Kit Face Detection is used on every extracted frame.

The following facial attributes are analyzed:

### Blink Detection

Eye state transitions are monitored across frames:

```text
Eye Open
   ↓
Eye Closed
   ↓
Eye Open
```

A valid blink confirms natural eye movement.

### Smile Detection

Smile probability is monitored across frames.

```text
Neutral Expression
        ↓
Smile Detected
```

The system verifies genuine facial movement rather than static images.

### Liveness Decision

Authentication proceeds only when at least one natural facial movement is detected.

If neither blinking nor smiling is observed, the user is prompted to record another video.

This provides an effective offline anti-spoofing mechanism without requiring specialized hardware.

---

## Step 4: Face Selection

Among all detected faces, the system automatically selects the frame containing the largest facial bounding box.

This typically corresponds to the clearest and most detailed facial image.

The selected face is then passed to the recognition pipeline.

---

## Step 5: Image Enhancement

Before recognition, the selected face undergoes preprocessing:

* Noise reduction
* Blur correction
* Image normalization
* Resolution standardization

This improves robustness under:

* Harsh sunlight
* Shadows
* Outdoor environments
* Low-light conditions

---

## Step 6: Face Cropping

The face region is cropped using the ML Kit bounding box.

Only the facial area is retained, reducing background noise and improving recognition accuracy.

---

## Step 7: Face Recognition

The cropped face is supplied to a custom-trained YOLO Classification model optimized for mobile deployment.

The model performs identity classification entirely offline.

### Recognition Logic

```text
Confidence < 40%
        ↓
Unknown Person

Confidence ≥ 40%
        ↓
Known Identity
```

If the confidence score exceeds 40%, the person's identity is displayed.

The application simultaneously displays:

```text
Face Authenticity Verified
Liveness Detection Passed
```

This indicates successful authentication.

---

# Authentication Output

For every successful authentication:

* Employee Name
* Employee ID
* Authentication Timestamp
* Confidence Score
* Captured Face Image
* Liveness Verification Status

are generated and stored locally.

---

# Offline Data Storage

The system is designed for uninterrupted operation in remote locations.

All authentication logs are stored securely on the mobile device.

Stored information includes:

* Face image
* Employee name
* Employee ID
* Date
* Time
* Verification result

No internet connection is required during authentication.

---

# Automatic Sync & Purge Mechanism

When network connectivity becomes available:

1. Stored authentication records are automatically synchronized.
2. Data is uploaded to MongoDB.
3. Local records can be purged after successful synchronization.

```text
Offline Verification
          │
          ▼
Local Storage
          │
Internet Available
          ▼
MongoDB Sync
          │
          ▼
Local Data Purge
```

This directly satisfies the mandatory Sync & Purge requirement of Hackathon 7.0.

---

# Hackathon Requirement Mapping

| Requirement                | Implementation                        |
| -------------------------- | ------------------------------------- |
| React Native Compatibility | React Native CLI                      |
| Android Support            | Android 8+                            |
| iOS Support                | iOS 12+                               |
| Offline Recognition        | Fully Offline                         |
| Offline Liveness Detection | Blink + Smile Analysis                |
| Lightweight AI Model       | Optimized YOLO Classification         |
| Mid-Range Device Support   | 3GB RAM Compatible                    |
| Processing Time < 1 sec    | Optimized Edge Inference              |
| Anti-Spoofing              | Video-Based Liveness Verification     |
| Open Source Technologies   | React Native, ML Kit, TensorFlow Lite |
| Source Code Available      | Yes                                   |
| Sync & Purge Capability    | MongoDB Synchronization               |
| Zero Network Dependency    | Fully Supported                       |

---

# Key Features

✅ Completely Offline Authentication

✅ Offline Liveness Detection

✅ Blink Verification

✅ Smile Verification

✅ Anti-Spoofing Protection

✅ Face Recognition using YOLO Classification

✅ Real-Time Authentication

✅ Mobile Optimized

✅ Android & iOS Support

✅ Local Secure Storage

✅ Automatic Cloud Synchronization

✅ Future Enterprise Integration Ready

---

# APK Download

### Click below to install the latest application build

👉 [Download APK Here](https://drive.google.com/file/d/1MTREN508HE_KeP6IrbSkWjqTOOrxc51r/view?usp=sharing)

---

# Application Screenshots

## Home Screen

<img width="180" height="400" alt="image" src="https://github.com/user-attachments/assets/1e491643-c93d-4561-b441-61399d90f2f6" />
<img width="180" height="400"alt="image" src="https://github.com/user-attachments/assets/2717dec3-5599-4397-af0d-4d7765785621" />


---

## Video Capture Screen

<img width="180" height="400" alt="image" src="https://github.com/user-attachments/assets/d3168087-6de3-4ca0-a222-30dd498e49ba" />


---

## Liveness Detection


<img width="180" height="400" alt="image" src="https://github.com/user-attachments/assets/c48387a9-504b-4f99-bb38-1af04f1d411a" />

--- 

## Face Recognition Result

<img width="180" height="400" alt="image" src="https://github.com/user-attachments/assets/11a6c024-89f6-4d55-9754-1f81ff061bce" />


---

## Authentication Success

<img width="180" height="400" alt="image" src="https://github.com/user-attachments/assets/edd46617-2754-42aa-a845-07e44e68a3cf" />
<img width="180" height="400" alt="image" src="https://github.com/user-attachments/assets/51da474c-c56d-4590-adcf-7172e5b4a25e" />

## Syncing Online

<img width="1000" height="400" alt="image" src="https://github.com/user-attachments/assets/e5e21a39-b3af-4bb8-af76-6ef661c4cba9" />

---

# Installation Guide

## Clone Repository

```bash
git clone https://github.com/Tiruvikraman/nhai_netra.git
```

```bash
cd NHAI-Netra
```

## Install Dependencies

```bash
npm install
```

## Android

```bash
npx react-native run-android
```

## iOS

```bash
cd ios
pod install
cd ..
npx react-native run-ios
```

## Build Release APK

```bash
cd android
.\gradlew assembleRelease
```

Generated APK:

```text
android/app/build/outputs/apk/release/app-release.apk
```

---

# Conclusion

NHAI Netra delivers a lightweight, fully offline, secure facial authentication solution capable of operating in remote environments with zero network connectivity. Through video-based liveness detection, face enhancement, optimized YOLO classification, and automatic synchronization capabilities, the solution directly addresses all functional and technical requirements defined in Hackathon 7.0.
