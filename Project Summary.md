# RoomPulse AI — The Invisible Health Guardian 🫀

> **Contactless Vital Sign Monitoring via Standard Webcams & Client-Side rPPG Architecture**

RoomPulse AI transforms ordinary consumer RGB cameras (webcams or mobile cameras) into real-time vital sign monitors without physical contact, wearables, or cloud video streaming.

---

## 🔗 Project Links

* **Live Web Application:** [roompulseai.lovable.app](https://roompulseai.lovable.app)
* **Video Demonstration:** [YouTube Demo Walkthrough](https://youtu.be/hrY0d0BEmIc)
* **Project Creator:** Hossam Elshahaby

---

## 🌟 Key Features

1. **Touchless Vital Sign Monitoring:** Extracts heart rate (BPM) and blood volume pulse (BVP) from micro-color variations in skin tissue.
2. **Triple Region-of-Interest (ROI) Tracking:** Simultaneously monitors the forehead and both cheek regions with motion-compensated alignment.
3. **Multi-Algorithm Signal Engine:**
   * **POS (Plane-Orthogonal-to-Skin):** Rejects specularity and skin-tone motion artifacts.
   * **CHROM (Chrominance-based):** High temporal contrast signal extraction.
   * **GREEN Channel:** Direct oxygenated hemoglobin light absorption tracking.
4. **Dynamic Trust Score & Anti-Spoofing:** Evaluates ambient light, face stability, and signal quality to reject static photo inputs or bad illumination.
5. **Validation Lab:** Allows testing against real reference ECG/PPG datasets for accuracy evaluation.
6. **100% On-Device Privacy:** Frame processing executes entirely inside the user's browser using HTML5 Canvas & WebAssembly. Video never leaves the machine.

---

## 🛠 Tech Stack

* **Frontend:** React / Vite / TypeScript
* **UI/UX Design:** Tailwind CSS, Lucide Icons, Custom CSS Glow Effects
* **Signal Processing:** HTML5 Canvas API, WebGL, rPPG (POS, CHROM, Green algorithms)
* **Hosting:** Lovable Platform

---

## 🚀 Quick Start & Local Setup

```bash
# Clone the repository
git clone https://github.com/hossamelshahaby/roompulse-ai.git

# Navigate into project folder
cd roompulse-ai

# Install dependencies
npm install

# Start local dev server
npm run dev
```

---

## 📜 Citation & License

Created by **Hossam Elshahaby**. Provided for healthcare, research, and non-invasive physiological monitoring applications.