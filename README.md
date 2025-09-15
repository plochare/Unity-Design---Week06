# Unity Design - Week 06

## Agenda

1. [Unity Visual Scripting](#Unity-Visual-Scripting)  
2. [Unity AR Foundation](#Unity-AR-Foundation)  
3. [Mobile AR Development](#Mobile-AR-Development)  
4. [Unity Vuforia SDK](#Unity-Vuforia-SDK)  
5. [Niantic ARDK](#Niantic-ARDK)  
6. [Class Assignment - Week #06](#Class-Assignment-week06)  

---

# Unity Visual Scripting ⚡

Unity Visual Scripting (formerly Bolt) lets you create gameplay mechanics, interactions, and logic **without writing code**. Instead of typing C#, you connect nodes in a graph. This makes it easier for designers, artists, and non-programmers to prototype and build complete systems while still integrating seamlessly with Unity.

---

## 🎯 Why Use Visual Scripting?
- 🖱 **No-code approach** → Build logic with drag-and-drop nodes.  
- 🎮 **Rapid prototyping** → Try ideas without worrying about syntax.  
- 🔄 **Fully integrated with Unity** → Works with GameObjects, components, and events.  
- 🤝 **Team-friendly** → Designers can script behaviors while programmers handle complex systems.  

---

## 🛠 Requirements
- Unity **2021 LTS or newer** (Visual Scripting is included by default).  
- Works on all Unity build targets (desktop, mobile, VR/AR, consoles).  

---

## 📥 Setup
1. Open **Unity → Window → Package Manager**.  
2. Search for **Visual Scripting**.  
3. Install the package (if not already installed).  
4. Unity will prompt you to **generate nodes** (C# API exposed as nodes). Click **Regenerate Nodes**.  

---

## 🚀 Quick Start Tutorial

### 1. Create a Visual Script
1. In the **Project Window**, right-click → `Create → Visual Scripting → Script Graph`.  
2. Name it (e.g., `PlayerController`).  
3. Drag it onto a **GameObject** to add it as a component.

### 2. Open the Graph
- Select the GameObject, click on the **Script Graph** field, then click **Edit Graph**.  
- This opens the **Graph Editor** where you’ll build node-based logic.

### 3. Add a Simple Movement Script
Let’s move a player with `WASD`:

- Add a **`Update` Event** (runs every frame).  
- Add **`Get Axis`** (set to `"Horizontal"`) and **`Get Axis`** (set to `"Vertical"`).  
- Combine them into a **Vector2**.  
- Multiply by `Time.deltaTime` and a **Speed** variable.  
- Connect to **`Translate`** node on the GameObject’s Transform.  

✅ Result: The player GameObject now moves based on keyboard input.

---

## 🧩 Example: Trigger an Animation
- Add **`On Collision Enter` Event**.  
- Connect it to **`Set Trigger`** (Animator node).  
- Enter trigger name (e.g., `"Hit"`).  

✅ Result: When the object collides with something, the Animator plays the `"Hit"` animation.

---

## 🧪 Best Practices
- Keep graphs **modular**: split logic into multiple smaller graphs.  
- Use **Sub-Graphs** to reuse common logic (like health systems or UI interactions).  
- Expose important values as **Variables** so designers can tweak them without opening the graph.  
- Use **Comments & Groups** to keep graphs readable.  

---

## ⚡ Advanced Features
- **Custom Events** → Trigger node graphs across different objects.  
- **State Graphs** → Build finite state machines (FSMs) for AI, UI, or game states.  
- **Variables**:
  - **Graph Variables** → Local to the graph.  
  - **Object Variables** → Stored on a GameObject.  
  - **Scene Variables** → Shared across a scene.  
  - **Application Variables** → Global, persistent across scenes.  
- **Integration with C#** → Any public method/property can be accessed as a node.  

---

## 📚 Learning Resources
- [Unity Docs – Visual Scripting](https://docs.unity3d.com/Manual/com.unity.visualscripting.html)  
- [Unity Learn – Visual Scripting Pathway](https://learn.unity.com/pathway/visual-scripting)  
- [Community Graph Examples (GitHub)](https://github.com/Unity-Technologies/visual-scripting-samples)  

---

## Tutorial 

https://learn.unity.com/tutorial/about-unity-visual-scripting

---

# Unity AR Foundation (v6.2) 🚀

A guide and tutorial for getting started with **Unity AR Foundation 6.2.0**, including setup, core concepts, sample workflows, and tips & best practices.

---

## 🎯 What is AR Foundation?

AR Foundation is Unity’s cross-platform framework for building augmented reality (AR) applications. It provides common interfaces for AR features, and delegates implementation to platform-specific provider packages (e.g. ARCore for Android, ARKit for iOS). This lets you write once in Unity and target multiple AR-capable platforms. :contentReference[oaicite:0]{index=0}

Features AR Foundation supports include:  
- Session management (start, stop, pause AR) :contentReference[oaicite:1]{index=1}  
- Device pose / camera tracking :contentReference[oaicite:2]{index=2}  
- Plane detection (e.g. floor, walls) :contentReference[oaicite:3]{index=3}  
- Image & object tracking :contentReference[oaicite:4]{index=4}  
- Anchors (fixed points in real world space) :contentReference[oaicite:5]{index=5}  
- Raycasts against tracked surfaces or feature points :contentReference[oaicite:6]{index=6}  
- Light estimation, occlusion, environment probes, meshing (depending on platform) :contentReference[oaicite:7]{index=7}  

---

## ✅ Official Unity Documentation

-[AR Fopundation Docs](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation%406.2/manual/index.html)

---
## 🧰 Requirements & Setup

Before you begin, make sure you have:

- Unity 2021 LTS or newer (preferably one of the more recent LTS releases for compatibility and stability).  
- AR device(s) to test on (Android with ARCore, iOS device with ARKit, etc.).  
- Unity XR Plugin architecture. You’ll need AR Foundation plus provider/plug-in package(s) for your target platforms. :contentReference[oaicite:8]{index=8}  

### Installing Packages

1. Open **Unity → Window → Package Manager**.  
2. Add the **AR Foundation** package (v6.2.0).  
3. Also install the provider plug-in(s) matching your target platform(s), for example:  
   - Google ARCore XR Plug-in (for Android)  
   - Apple ARKit XR Plug-in (for iOS)  
   - OpenXR, visionOS, etc. :contentReference[oaicite:9]{index=9}  

4. Make sure in **Project Settings → XR Plug-in Management** the correct plug-in(s) are enabled for each build target (Android, iOS).  

---

## 🔍 Quick Start Tutorial

Here’s a typical workflow to get a basic AR scene up and running, including plane detection and simple raycasting.

### 1. Create a new AR Scene

- In Unity, create a new Scene (e.g. `ARScene`).  
- Set up scene components:

  - Add an **AR Session** game object: this manages the AR lifecycle.  
  - Add an **AR Session Origin**: handles translating AR space into Unity scene space (usually has a Camera child for AR rendering).  
  - Under the Session Origin, add an **AR Camera** (with AR Camera component, often setup automatically).  

### 2. Enable Plane Detection

- On the AR Session Origin or a manager GameObject, add an **ARPlaneManager** component.  
- Configure detection mode (horizontal, vertical, or both).  

### 3. Add Raycasting to Place Objects

- Add an **ARRaycastManager** component.  
- Create a UI or script so that when the user taps (or touches) the screen, you perform a raycast from the touch position into the AR world. If the raycast hits a detected plane, instantiate/place a prefab (e.g. a cube) at that point.

```csharp
using UnityEngine;
using UnityEngine.XR.ARFoundation;
using UnityEngine.XR.ARSubsystems;
using System.Collections.Generic;

public class ARTouchPlacement : MonoBehaviour
{
    [SerializeField]
    private GameObject placeablePrefab;

    private ARRaycastManager raycastManager;
    private List<ARRaycastHit> hitResults = new List<ARRaycastHit>();

    void Awake()
    {
        raycastManager = GetComponent<ARRaycastManager>();
    }

    void Update()
    {
        if (Input.touchCount > 0)
        {
            Touch touch = Input.GetTouch(0);
            if (touch.phase == TouchPhase.Began)
            {
                if (raycastManager.Raycast(touch.position, hitResults, TrackableType.Planes))
                {
                    Pose hitPose = hitResults[0].pose;
                    Instantiate(placeablePrefab, hitPose.position, hitPose.rotation);
                }
            }
        }
    }
}
````

### 4. Build & Test on Device

* Switch platform in Unity Build Settings to **Android** or **iOS**.
* Make sure the provider plug-in is enabled and you have required permissions (camera, etc.).
* Build & run on your device.
* Test detecting planes, placing objects via touch, and moving around.

---

## ⚙ Supported Features & Platform Differences

Some features are only available on certain platforms. The core features like session, device tracking, plane detection, camera, raycasting are broadly supported. Others (object tracking, meshing, environment probes, occlusion, etc.) may require specific hardware / platform. ([Unity Documentation][1])

Unity’s XR Simulation (inside the Editor) can help emulate some aspects during development, but usually you'll need real devices to test full AR functionality. ([Unity Documentation][1])

---

## 💡 Tips & Best Practices

* Always check **AR permissions** (camera, etc.) especially for mobile platforms.
* Keep visuals lightweight: AR scenes need to run smoothly, latency matters. Use optimized meshes & textures.
* Handle loss of tracking gracefully (e.g. pause AR content or provide feedback).
* Use anchoring to maintain stable positioning of virtual content.
* Consider user UX: guidance for first time users (e.g. “move device until surface visible”).
* Regularly test on target devices to catch platform-specific bugs.


---

# Mobile AR Development

https://learn.unity.com/pathway/mobile-ar-development?version=2022.3
 
---

# Unity Vuforia SDK 🔍✨

Vuforia is a leading **Augmented Reality (AR) SDK** for Unity that allows developers to recognize images, objects, and environments, then overlay interactive 3D content. It’s widely used for AR apps in education, retail, training, and entertainment.

---

## 🎯 What is Vuforia?
Vuforia is an **AR engine** that integrates with Unity to provide:
- 📷 **Image Target Recognition** → Detect and augment 2D images.  
- 🛠 **Model Target Tracking** → Recognize 3D objects.  
- 🌍 **Ground Plane** → Place AR objects on real-world surfaces.  
- 🎭 **VUMarks** → Custom markers (like QR codes but stylized).  
- 🕹 **Virtual Buttons** → Trigger actions with physical marker interactions.  
- 🧩 **Multi-targets** → Track multiple objects at once.  

---

## 🛠 Requirements
- Unity **2021 LTS or newer**.  
- [Vuforia Engine SDK](https://developer.vuforia.com/downloads/sdk) installed in Unity.  
- A supported device (Android/iOS) with a working camera.  
- [Vuforia Developer Account](https://developer.vuforia.com/) (for license keys).  

---

## 📥 Installation

1. **Enable Vuforia in Unity**  
   - Go to: `Edit → Project Settings → Player → XR Settings`.  
   - Enable **Vuforia Augmented Reality Support**.  

2. **Get a License Key**  
   - Sign up at [Vuforia Developer Portal](https://developer.vuforia.com/).  
   - Create a new project → Copy your **App License Key**.  
   - Paste it into: `Vuforia Configuration → App License Key`.  

3. **Import Vuforia SDK**  
   - Via Unity **Package Manager** or `.unitypackage` download from the Vuforia portal.  

---

## 🚀 Quick Start Tutorial

### 1. Setup AR Camera
- Delete the default Unity **Main Camera**.  
- Add a **Vuforia AR Camera** (GameObject → Vuforia Engine → AR Camera).  
- In **AR Camera Inspector**, paste your License Key.  

### 2. Add an Image Target
1. Go to [Vuforia Target Manager](https://developer.vuforia.com/target-manager).  
2. Upload a reference image → Generate a **Database**.  
3. Download the `.unitypackage` and import into Unity.  
4. In Unity:  
   - Add **GameObject → Vuforia Engine → Image Target**.  
   - Assign your imported database + image.  

### 3. Place 3D Content
- Drag a 3D model (e.g., Cube, Character prefab) as a **child of the Image Target**.  
- When the target is detected via camera, the object appears on top of it.  

### 4. Build & Test
- Switch platform: **Android/iOS**.  
- Build & run on a device.  
- Point your camera at the image target → Watch your AR content appear.  

---

## 🧩 Example Script: Rotate Object on Target
```csharp
using UnityEngine;
using Vuforia;

public class RotateOnTarget : MonoBehaviour, ITrackableEventHandler
{
    private TrackableBehaviour trackable;

    void Start()
    {
        trackable = GetComponent<TrackableBehaviour>();
        if (trackable) trackable.RegisterTrackableEventHandler(this);
    }

    public void OnTrackableStateChanged(
        TrackableBehaviour.Status prev, TrackableBehaviour.Status newStatus)
    {
        if (newStatus == TrackableBehaviour.Status.DETECTED ||
            newStatus == TrackableBehaviour.Status.TRACKED)
        {
            // Target found → Start rotating
            StartCoroutine(Rotate());
        }
    }

    private System.Collections.IEnumerator Rotate()
    {
        while (true)
        {
            transform.Rotate(Vector3.up * 50 * Time.deltaTime);
            yield return null;
        }
    }
}
````

✅ This script rotates a 3D object whenever the target image is detected.

---

## ⚡ Advanced Features

* **Ground Plane** → Place objects on horizontal surfaces without markers.
* **Model Targets** → Recognize and augment real 3D products.
* **VUMarks** → Brandable AR markers (customized QR-like codes).
* **Virtual Buttons** → Add interactivity by defining button zones on targets.

---

## 💡 Best Practices

* Use **high-contrast, non-repetitive images** for targets.
* Test target ratings in the Vuforia Target Manager (⭐ stronger = better).
* Optimize 3D assets (low poly, compressed textures) for mobile performance.
* Handle lost tracking gracefully (fade or pause AR content).
* Always test on real devices — AR is hardware dependent.

---

## 📚 Resources

* [Vuforia Developer Portal](https://developer.vuforia.com/)
* [Unity Vuforia Documentation](https://library.vuforia.com/)
* [Vuforia Sample Repository](https://github.com/PTCInc/VuforiaEngineSamples)
* [Unity AR Foundation vs Vuforia](https://unity.com/partners/vuforia)

---

# Niantic ARDK 🌍✨

Niantic’s **Augmented Reality Developer Kit (ARDK)** empowers developers to build **multiplayer, context-aware AR experiences** in Unity. With ARDK, you can blend the real world with digital content, leveraging Niantic’s expertise in AR (Pokémon GO, Peridot, Pikmin Bloom).  

---

## 🎯 What is ARDK?
Niantic ARDK provides advanced AR capabilities in Unity:
- 🧩 **Semantic Segmentation** → Understand real-world surfaces (sky, ground, buildings, people).  
- 🔍 **Meshing** → Scan & generate meshes of your environment in real-time.  
- 🌐 **Multiplayer** → Share AR experiences with multiple users via Lightship Networking.  
- 🕹 **Occlusion** → Make digital objects appear naturally behind real-world objects.  
- 🧭 **Persistent AR** → Save and reload AR content at specific real-world locations.  

---

## 🛠 Requirements
- Unity **2021 LTS or newer** (recommended).  
- AR-capable device (iOS with ARKit, Android with ARCore).  
- [Niantic Lightship Account](https://lightship.dev/) (for API keys).  
- ARDK package installed in Unity.  

---

## 📥 Installation

### 1. Create a Lightship Account
- Sign up at [lightship.dev](https://lightship.dev/).  
- Create an app and retrieve your **API key**.  

### 2. Install ARDK
1. Open Unity → `Window → Package Manager`.  
2. Click the **+** icon → *Add package from Git URL*.  
   ```text
   https://github.com/niantic-lightship/ardk-unity-package.git
````

3. Import samples for example scenes.

### 3. Configure API Key

* Go to: `Edit → Project Settings → Niantic Lightship`.
* Paste your API key in the **API Key field**.

---

## 🚀 Quick Start Tutorial

### 1. Create a New AR Scene

* Delete the default **Main Camera**.
* Add an **AR Session** prefab from ARDK (handles lifecycle).
* Add an **AR Camera** (child of AR Session).

### 2. Add Meshing

* Add **AR Mesh Manager** to your AR Session Origin.
* When running on device, ARDK will generate a mesh of your environment in real-time.

### 3. Place Objects with Tap

Example script to place an object when the user taps on a surface:

```csharp
using Niantic.ARDK.AR;
using Niantic.ARDK.AR.Camera;
using Niantic.ARDK.AR.ARSessionEventArgs;
using Niantic.ARDK.Extensions;
using UnityEngine;

public class TapToPlace : MonoBehaviour
{
    public GameObject prefab;
    private IARSession _session;

    void Start()
    {
        ARSessionFactory.SessionInitialized += OnSessionInitialized;
    }

    private void OnSessionInitialized(AnyARSessionInitializedArgs args)
    {
        _session = args.Session;
    }

    void Update()
    {
        if (_session == null || Input.touchCount == 0) return;

        Touch touch = Input.GetTouch(0);
        if (touch.phase != TouchPhase.Began) return;

        var hitResults = _session.CurrentFrame.HitTest
        (
            Camera.main.pixelWidth,
            Camera.main.pixelHeight,
            touch.position
        );

        if (hitResults.Count > 0)
        {
            var hit = hitResults[0];
            Instantiate(prefab, hit.WorldTransform.ToPosition(), hit.WorldTransform.ToRotation());
        }
    }
}
```

✅ This script spawns a prefab where the user taps, anchored to real-world surfaces detected by ARDK.

---

## 🔗 Multiplayer with Lightship

1. Add a **Multipeer Networking Manager** prefab.
2. Configure it for **Host** or **Client** mode.
3. Use `NetworkingManager.Instance.BroadcastData(...)` to sync game state across devices.

💡 Example: Multiple users can see and interact with the same AR object in real-time.

---

## ⚡ Advanced Features

* **Semantic Segmentation** → Mask out sky, ground, buildings, water, etc.
* **Occlusion** → Hide AR objects behind real-world objects.
* **Persistent AR** → Store anchors to return to the same AR scene later.
* **Shared Multiplayer AR** → Niantic’s peer-to-peer networking system.

---

## 🧪 Best Practices

* Always test on real devices (Editor play mode won’t simulate full AR).
* Optimize assets for mobile AR (low poly, compressed textures).
* Use **anchors** to keep AR objects stable.
* Handle **tracking loss** gracefully.
* Limit network payloads for smoother multiplayer AR.

---

## 📚 Resources

* [Niantic Lightship Docs](https://lightship.dev/docs/)
* [ARDK Unity API Reference](https://lightship.dev/docs/ardk/)
* [Lightship GitHub Samples](https://github.com/niantic-lightship/ardk-unity-samples)
* [Community Forum](https://lightship.dev/forums/)

---

## ✅ Summary

With Niantic’s ARDK you can:

* Build AR experiences that understand the real world (meshes, segmentation).
* Create **multiplayer shared AR sessions**.
* Make AR objects behave naturally with occlusion.
* Deliver persistent, location-based AR apps.

---
