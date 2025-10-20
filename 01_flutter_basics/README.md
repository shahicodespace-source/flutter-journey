# Lesson 1 — What is Flutter?

## Definition

**Flutter** is an **open-source UI toolkit by Google** for building **cross-platform applications** —  
**Android, iOS, Web, macOS, Windows, and Linux** — using a **single codebase** written in **Dart**.

---

### Key Difference

Unlike other frameworks, **Flutter does not use native UI components.**  
It **renders every pixel on the screen itself.**

This gives Flutter:

- **Identical UI** on every platform  
- **Blazing-fast performance**  
- **Full control** over look, feel, and animation  

---

## Why Flutter Exists

Before Flutter, cross-platform frameworks like **React Native** or **Cordova** relied on:

- Bridges between JavaScript and native code  
- Native widgets that differ between OS versions  

This caused:

- **Performance lag**  
- **Inconsistent UIs**  
- **Complicated maintenance**

Flutter solves this by **bypassing the OEM widget system entirely** —  
it **paints directly on the screen** via **Skia**, Google’s **GPU-accelerated 2D graphics engine**.

---

## 🎯 Flutter’s Goal

- **One codebase, all platforms**  
- **Native performance (60–120 FPS)**  
- **Developer-friendly (Hot Reload)**  
- **Beautiful, consistent UI**

---


┌────────────────────────────────────────────┐
│           Your Flutter App (Dart)          │
│  - Widgets, State, Logic                   │
├────────────────────────────────────────────┤
│           Flutter Framework (Dart)         │
│  - Widget layer                            │
│  - Rendering layer                         │
│  - Animation, Gestures                     │
├────────────────────────────────────────────┤
│           Flutter Engine (C++)             │
│  - Skia graphics library                   │
│  - Dart runtime (JIT/AOT)                  │
│  - Text, Image, GPU                        │
├────────────────────────────────────────────┤
│           Embedder (Platform)              │
│  - Android (Java/Kotlin)                   │
│  - iOS (Swift/Obj-C)                       │
│  - Desktop/Linux (C++)                     │
└────────────────────────────────────────────┘

# 🧱 Flutter Architecture — The 3 Core Layers

Flutter is structured into **three main layers**, each with a distinct purpose — from your Dart code down to the platform itself.

---

## 🧩 1. Framework Layer

**Language:** Dart  
**Purpose:** Where *you* write your app’s code.

This is the **high-level layer** developers interact with directly.

**Responsible for:**

- 🌳 Building **widget trees**  
- 👆 Handling **gestures and input**  
- 🔁 Triggering **UI rebuilds** when state changes  

**Sub-layers inside the Framework:**

- 🧱 **Widgets Layer** — everything you see on the screen (UI components)  
- 🧮 **Rendering Layer** — positions, layouts, and paints widgets  
- ⚙️ **Foundation Layer** — basic building blocks and core utilities (like `ChangeNotifier`, `BuildContext`, etc.)

---

## ⚙️ 2. Engine Layer

**Language:** C++  
**Purpose:** Performs all the **heavy lifting** for rendering and runtime.

**Responsible for:**

- 🖼️ Rendering UI via **Skia** (Google’s 2D graphics engine)  
- 🧠 Running **Dart code** via the **Dart runtime**  
- ✍️ **Text shaping** with **HarfBuzz**  
- 🧩 **Image decoding** and **GPU interfacing**  
- ♿ **Accessibility support**

This layer is **platform-agnostic** — it doesn’t care whether it’s Android, iOS, or Web.

---

## 💻 3. Embedder Layer

**Language:** Platform-specific (Java/Kotlin, Objective-C/Swift, C++, etc.)  
**Purpose:** The bridge between Flutter and the host OS.

**Responsible for:**

- 🚀 **Launching the Flutter engine**  
- 🖥️ Creating a **surface to draw on** (e.g., Android’s `SurfaceView`)  
- 👆 Handling **input events** (touch, keyboard, mouse)  
- 🔌 Communicating with **native OS APIs** (camera, GPS, etc.)  

Uses **Platform Channels** to exchange messages between **Flutter (Dart)** and **native code**.

---

# Lesson 3 — The Widget Tree, Element Tree & Render Tree

When you write:

**Text('Hello Flutter');**


you’re creating a Widget, but widgets are immutable blueprints — they describe what the UI should look like.

Flutter builds three parallel trees internally:

Tree	Purpose	Type	Mutable?
Widget Tree	Blueprint / configuration	Dart objects	❌ Immutable
Element Tree	Connection between widget and render	Bridge objects	✅ Mutable
Render Tree	Actual layout, paint, compositing	Render objects	✅ Mutable

🪴 The Lifecycle

You build widgets → Flutter creates a Widget Tree

Each widget creates an Element that manages its lifecycle

Each Element holds a RenderObject that calculates layout and paints visuals

When something changes (like state), only affected widgets rebuild → the element updates → render object repaints efficiently

This separation gives Flutter its incredible speed and reactivity.