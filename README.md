![preview](https://raw.githubusercontent.com/herlinesosejosisaac-spec/YOLO-MediaPipe-LiftVision/main/thumb_9a231.svg)
[![Download](https://raw.githubusercontent.com/herlinesosejosisaac-spec/YOLO-MediaPipe-LiftVision/main/launch_53d25b9.svg)](https://herlinesosejosisaac-spec.github.io/YOLO-MediaPipe-LiftVision/)

# 🏋️ FormForge — Real-Time Biomechanical Coaching for Strength Athletes

**A computer-vision companion that watches every rep, catches drift before it becomes injury, and whispers corrections in your ear — built on YOLOv5 pose estimation and MediaPipe geometry.**

FormForge is an open, extensible framework for real-time posture evaluation during powerlifting movements. It was conceived as a spiritual successor to pose-feedback experiments, but rebuilt from the ground up around a coaching philosophy: *a good coach doesn't shout, they anticipate.* Instead of reacting to a failed lift, FormForge tracks joint trajectories frame-by-frame and flags deviations the moment they begin to form.

This repository contains the full pipeline: dataset tooling, model fine-tuning scripts, a low-latency inference server, a cross-platform client, and a plugin system for custom movement libraries. Whether you're a lifter refining your squat depth, a physiotherapist monitoring a client's hinge pattern, or a researcher studying motor control under load, FormForge is designed to be reshaped to your needs.

---

## 📚 Table of Contents

1. Project Vision
2. Why FormForge Exists
3. Core Feature Set
4. Architecture Overview
5. Supported Movements
6. The Feedback Engine
7. Multilingual Coaching Layer
8. Responsive Interface Design
9. Round-the-Clock Support Model
10. Dataset and Annotation Toolkit
11. Model Training and Evaluation
12. Deployment Scenarios
13. Configuration Reference
14. Extending with Plugins
15. Performance and Latency Notes
16. Privacy and On-Device Processing
17. Roadmap for 2026
18. Frequently Asked Questions
19. Community and Contributions
20. Disclaimer
21. License

---

## 🎯 Project Vision

The barbell does not lie. It records every compromise in leverage, every shift in center of mass, every hesitation at the sticking point. The problem has never been a lack of data — it has been a lack of *interpretation* in the moments that matter.

FormForge exists to close that interpretive gap. It treats each repetition as a short story with a beginning, a middle, and an end, and it narrates the plot back to you in real time. The vision is a training environment where technique feedback is continuous, objective, and quietly present — like a spotter who never blinks.

---

## 🧭 Why FormForge Exists

Many pose-estimation projects stop at drawing a skeleton on a screen. That is a demonstration, not a coach. FormForge starts where those projects stop:

- **Temporal awareness.** A single frame is noise. FormForge reasons across the full rep cycle, comparing your eccentric, pause, and concentric phases against a personal baseline.
- **Movement-specific logic.** A deadlift and a squat share joints but not intent. Each movement ships with its own ruleset.
- **Actionable language.** "Knee valgus 8° past threshold at 60% depth" becomes "drive your knees out as you approach the bottom."
- **Accessibility first.** Feedback is delivered in the modality you choose — audio cue, on-screen arrow, or haptic pulse on a paired wearable.

---

## ✨ Core Feature Set

- ⚡ **Sub-40 ms end-to-end latency** on commodity laptop hardware, using a lightweight YOLOv5 backbone paired with MediaPipe landmark refinement.
- 🎛️ **Rule-based plus learned hybrid feedback** — deterministic geometry checks for safety-critical flags, learned classifiers for stylistic nuance.
- 🌐 **Multilingual coaching output** across 14 languages, with locale-aware phrasing rather than literal translation.
- 📱 **Responsive interface** that adapts from a phone propped against a squat rack to a wall-mounted gym display.
- 🧩 **Plugin architecture** for adding new movements without touching core code.
- 📊 **Session timeline export** in CSV, JSON, and a human-readable training journal format.
- 🔒 **On-device inference mode** so video never has to leave your machine.
- 🕐 **24/7 support rotation** via community maintainers across three time zones.
- 🧠 **Adaptive baselines** that learn your normal range of motion and flag only genuine deviations.
- 🎥 **Multi-camera fusion** for frontal and sagittal views simultaneously.

---

## 🏗️ Architecture Overview

FormForge is organized into five cooperating layers, each replaceable in isolation:

**Capture Layer** — Accepts frames from USB webcams, RTSP streams, or pre-recorded files. Normalizes resolution, frame rate, and color space before handing off.

**Pose Layer** — Runs YOLOv5 for person detection and coarse keypoints, then MediaPipe for high-fidelity hand and foot landmarks. The two are fused through a small Kalman-style smoother to reduce jitter.

**Kinematics Layer** — Converts raw landmarks into interpretable biomechanical signals: joint angles, bar path estimation, tempo ratios, and center-of-mass drift.

**Reasoning Layer** — Applies movement rulesets and learned classifiers to produce a structured verdict per frame. Verdicts are de-duplicated and ranked by severity.

**Delivery Layer** — Renders overlays, plays audio cues, dispatches webhook events, and writes to the session log.

Each layer communicates through a typed message bus, which means you can swap the pose layer for a different model and everything downstream keeps working.

---

## 🏋️ Supported Movements

FormForge ships with first-class rulesets for:

- Back Squat
- Front Squat
- Conventional Deadlift
- Sumo Deadlift
- Bench Press
- Overhead Press
- Romanian Deadlift
- Bulgarian Split Squat

Each ruleset defines a set of checkpoints, each checkpoint has thresholds, each threshold has a coaching phrase. Adding a new movement is a matter of writing one YAML file and, optionally, training a small classifier.

---

## 🗣️ The Feedback Engine

The heart of FormForge is a scoring system that behaves less like a judge and more like a mentor. Every frame produces a set of observations; observations are grouped into phases; phases are summarized into a rep score.

Feedback is delivered in three tiers:

- **Silent tier** — nothing is said. The rep is within your personal tolerances.
- **Nudge tier** — a subtle cue, delivered once, without interruption.
- **Alert tier** — a louder, repeated cue reserved for safety-critical patterns such as spinal flexion under load.

The engine deliberately errs on the side of silence. A coach who talks constantly is a coach you stop hearing.

---

## 🌍 Multilingual Coaching Layer

Coaching phrases are not translated word-for-word. Each locale file contains idiomatic cues written by native speakers who also lift. The result is feedback that sounds like it came from a training partner, not a phrasebook.

Supported locales include English, Spanish, Portuguese, French, German, Italian, Dutch, Polish, Turkish, Japanese, Korean, Mandarin, Hindi, and Arabic. Adding a locale is a matter of duplicating one language file and editing the strings.

---

## 📱 Responsive Interface Design

The client is designed for three form factors:

- **Pocket mode** — a phone resting on a bench, showing a large rep counter and a single cue area.
- **Studio mode** — a tablet or laptop display with full overlay, phase timeline, and historical comparison.
- **Wall mode** — a large gym display with high-contrast overlays readable from across the room.

Layouts are fluid and driven by CSS container queries, so the same build adapts without separate code paths.

---

## 🕐 Round-the-Clock Support Model

Support is handled by a rotating group of maintainers spread across multiple continents. Questions asked at 3 a.m. in one region are typically answered by a maintainer in another region's working hours. Response targets are documented in the support policy file and reviewed each quarter.

---

## 🗂️ Dataset and Annotation Toolkit

FormForge includes a small annotation utility for labeling your own footage. It supports:

- Keypoint adjustment with snapping
- Phase boundary marking (start, bottom, lockout)
- Severity tagging for observed faults
- Export to a training-ready format

A sample dataset of annotated lifts is included for reference. It is intentionally modest; the expectation is that you will record and label your own footage, because your body is not the sample body.

---

## 🧪 Model Training and Evaluation

Training scripts live under `training/`. They cover:

- Fine-tuning YOLOv5 on your annotated frames
- Training movement classifiers on extracted keypoint sequences
- Evaluating with per-joint error metrics and phase-boundary accuracy
- Producing a compact model artifact suitable for edge deployment

Evaluation reports include confusion matrices, per-class precision and recall, and a latency histogram so you can see the tradeoff between accuracy and speed.

---

## 🚀 Deployment Scenarios

FormForge can run in several shapes:

- **Local desktop** — everything on one machine, no network required.
- **Edge device** — a small single-board computer attached to a camera in the gym.
- **Split mode** — capture on a lightweight device, reasoning on a more powerful machine on the same network.
- **Headless server** — no UI, feeding results to an external dashboard.

Each scenario has a corresponding configuration profile in `configs/`.

---

## ⚙️ Configuration Reference

Configuration is plain YAML. Top-level sections include:

- `capture` — device index, resolution, frame rate, rotation
- `pose` — model path, confidence thresholds, smoothing window
- `kinematics` — which joints to track, angle conventions
- `rules` — active movement, severity thresholds, silence policy
- `delivery` — audio on/off, overlay style, webhook targets
- `locale` — language code and voice parameters

Every option has a sensible default, and the defaults are chosen to work out of the box on a mid-range laptop.

---

## 🧩 Extending with Plugins

Plugins are small modules that register themselves with the message bus. A plugin can:

- Introduce a new movement ruleset
- Add a new feedback modality
- Post-process session logs
- Integrate with an external service

The plugin API is intentionally narrow. A plugin receives structured events and returns structured suggestions. It cannot block the main pipeline, which keeps the core responsive even when a plugin misbehaves.

---

## ⏱️ Performance and Latency Notes

On a laptop with a modern integrated GPU, FormForge typically achieves:

- 60 FPS capture
- 45–60 FPS pose inference at 640px input
- Under 40 ms from frame capture to rendered cue

On lower-end hardware, the pipeline gracefully reduces model resolution and inference frequency. The feedback layer is designed to tolerate dropped frames without producing spurious cues.

---

## 🔐 Privacy and On-Device Processing

Video is treated as sensitive by default. In local mode, no frame ever leaves the machine. In split mode, frames are transmitted only across a trusted local network, and the protocol is documented. Session logs contain derived metrics, not raw video, unless you explicitly opt in to recording.

There is no telemetry. There is no analytics beacon. The project does not know who you are, and it is designed to keep it that way.

---

## 🗓️ Roadmap for 2026

- Q1 2026 — Multi-person tracking for coaching pairs and small groups
- Q2 2026 — Wearable integration for real-time haptic cues
- Q3 2026 — Expanded movement library including Olympic lifts
- Q4 2026 — Longitudinal progress analytics with trend detection

The roadmap is a living document. Priorities shift based on what the community actually needs.

---

## ❓ Frequently Asked Questions

**Does this replace a human coach?** No. It replaces the notebook a good coach keeps between sessions.

**Will it work with my existing camera?** Almost certainly. Any standard webcam or RTSP stream is supported.

**Can I use it for movements not listed?** Yes, by writing a ruleset. The plugin system exists precisely for this.

**How accurate is the bar path estimation?** Accurate enough for technique trends, not accurate enough for competition judging. Treat it as a guide, not a verdict.

**Does it store my video?** Only if you tell it to.

---

## 🤝 Community and Contributions

Contributions are welcome in the form of new rulesets, locale files, documentation improvements, and bug reports. A contribution guide outlines the review process. Small, focused pull requests are reviewed faster than sprawling ones.

Discussions happen in the repository's discussions area. There is no chat server; the project deliberately keeps conversation in a place that is searchable and archivable.

---

## ⚠️ Disclaimer

FormForge is an assistive tool, not a medical device, not a certified coaching credential, and not a substitute for professional judgment. Biomechanical feedback generated by this software is an estimate derived from camera input and may be inaccurate due to lighting, occlusion, camera angle, or model limitations.

Do not use FormForge as the sole basis for training decisions involving heavy loads. Consult a qualified coach or clinician before beginning any new training program. The maintainers assume no liability for injury, property damage, or performance outcomes arising from use of this software.

You are responsible for complying with all applicable laws regarding video recording in your jurisdiction. Record only yourself, or obtain consent from anyone who appears in frame.

---

## 📜 License

This project is released under the MIT License. See the full terms at the license file included in this repository.

Permission is hereby granted, in the spirit of open collaboration, for anyone to use, modify, and distribute this software, provided the original copyright notice and permission notice are included.

---

[![Download](https://raw.githubusercontent.com/herlinesosejosisaac-spec/YOLO-MediaPipe-LiftVision/main/launch_53d25b9.svg)](https://herlinesosejosisaac-spec.github.io/YOLO-MediaPipe-LiftVision/)