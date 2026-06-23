# Solar Odyssey

A real-time 3D space exploration simulation built entirely in C using OpenGL and freeGLUT. Pilot a rocket from Space Center, fly across a fully rendered solar system, and land on the surface of any of the eight planets, each with a unique environment built from real spacecraft reference imagery.

> No game engine. No 3D model files. No external assets. Every object is generated purely through code.

---

## Overview:

Solar Odyssey progresses through four distinct phases:

| Phase | Description |
|-------|-------------|
| **Launch** | Full rocket launch sequence from LC-39B — countdown, ignition, SRB separation, atmospheric ascent |
| **Orbit** | Cinematic orbital transition as the Earth curves away beneath you |
| **Space** | Free flight across the solar system — all 8 planets orbiting the sun in real time |
| **Planet** | First/third-person surface exploration as a NASA EMU astronaut on any planet |

---

## Features:

- **Full SLS Rocket** — Orange core stage, twin SRBs with separation physics, RS-25 engine bells, Orion capsule
- **Kennedy Space Center** — VAB, Launch Control Centre, crawlerway, lamp posts, palm trees, ocean
- **Solar System** — All 8 planets with orbital motion, axial tilt, self-rotation, and ring systems
- **Asteroid Belt** — 280 individually tumbling rocks between Mars and Jupiter
- **Particle System** — 4,000-particle pool: engine fire, smoke, SRB debris, space exhaust
- **Per-Planet Physics** — Gravity and jump velocity scale per planet (Mercury 0.38g → Jupiter 2.53g)
- **Planet Surfaces** — Unique environment per planet from real spacecraft reference imagery
- **NASA EMU Astronaut** — Fully articulated spacesuit: helmet, golden visor, PLSS backpack, flag patch
- **HUD System** — Live telemetry, planet science facts panel, controls overlay
- **Audio** — MCI-based WAV: countdown, engine loop, SRB separation, space ambient

---

## Controls:

### Launch Phase:
| Key | Action |
|-----|--------|
| `SPACE` | Begin launch sequence |
| `Mouse` | Look around |
| `R` | Reset simulation |
| `ESC` | Exit |

### Space Phase:
| Key | Action |
|-----|--------|
| `W / S` | Fly forward / backward |
| `A / D` | Strafe left / right |
| `Q / E` | Fly up / down |
| `L` | Land on nearest planet (when prompted) |
| `Mouse` | Steer / look around |
| `R` | Reset |

### Planet Phase:
| Key | Action |
|-----|--------|
| `W / S` | Walk forward / backward |
| `A / D` | Strafe left / right |
| `SPACE` | Jump |
| `B` | Blast off back to space |
| `Mouse` | Look around |
| `R` | Reset |

---

## Requirements:

### Hardware:
- CPU: Intel Core i5 / AMD Ryzen 5 or higher
- RAM: 4 GB minimum
- GPU: OpenGL 1.4 compatible with hardware acceleration
- Storage: ~10 MB
- Display: 1280×720 or higher

### Software:
- OS: Windows 10 or later (64-bit)
- IDE: Microsoft Visual Studio (Community or higher)
- Compiler: MSVC in C mode (`/TC` flag), x86 (32-bit) target

### Dependencies:
| Library | Purpose |
|---------|---------|
| `freeGLUT 3.x` | Window management, input, primitive shapes |
| `OpenGL` (`opengl32.lib`) | 3D rendering pipeline |
| `GLU` (`glu32.lib`) | Quadric tessellation, camera, projection |
| `WinMM` (`winmm.lib`) | WAV audio playback via MCI |

---

## Build Instructions:

### 1. Install freeGLUT

Download the pre-built freeGLUT binaries for MSVC from [freeglut.sourceforge.net](https://freeglut.sourceforge.net) or [transmissionzero.co.uk](https://www.transmissionzero.co.uk/software/freeglut-devel/).

Copy files to your Visual Studio directories:
```
freeglut/include/GL/  →  C:\Program Files\Microsoft Visual Studio\...\VC\Tools\MSVC\...\include\GL\
freeglut/lib/x86/     →  C:\Program Files\Microsoft Visual Studio\...\VC\Tools\MSVC\...\lib\x86\
freeglut/bin/x86/freeglut.dll  →  C:\Windows\System32\
```

### 2. Create the Project

1. Open Visual Studio → **Create a new project** → **Empty Project**
2. Add `main.c` to the project (Source Files)
3. Right-click project → **Properties**

### 3. Configure Project Properties

Set the following under **Project → Properties**:

| Setting | Value |
|---------|-------|
| Configuration Properties → General → Platform Toolset | MSVC (latest) |
| C/C++ → Advanced → Compile As | **Compile as C Code (/TC)** |
| Linker → Input → Additional Dependencies | `freeglut.lib; opengl32.lib; glu32.lib; winmm.lib` |
| C/C++ → Preprocessor → Preprocessor Definitions | `_CRT_SECURE_NO_WARNINGS` |

> Make sure the build target is set to **x86 (32-bit)**, not x64.

### 4. Add Audio Files

Place these WAV files in the **same directory as the compiled `.exe`**:

```
countdown.wav      — launch countdown audio
engine.wav         — rocket engine loop
srb_sep.wav        — SRB separation sound
space.wav          — space ambient loop
```

### 5. Build and Run

Press `Ctrl+F5` to build and run without the debugger.

---

## Project Structure

```
SolarOdyssey/
│
├── main.c                 # Entire simulation — ~1,400 lines
│
├── countdown.wav          # Launch countdown audio
├── engine.wav             # Engine loop
├── srb_sep.wav            # SRB separation sound
└── space.wav              # Space ambient
```

---

## Technical Highlights

### Graphics Concepts Implemented
| Concept | Implementation |
|---------|---------------|
| Translation | `glTranslatef` — every object positioned in world space |
| Rotation | `glRotatef` — orbital motion, axial tilt, SRB tumble, astronaut joints |
| Scaling | `glScalef` — terrain slabs, ellipsoid storm ovals, suit parts |
| Matrix Stack | `glPushMatrix/glPopMatrix` — ~35 nested pairs for the astronaut alone |
| Perspective Projection | `gluPerspective(65°, aspect, 0.05, 3000)` |
| Orthographic Projection | `gluOrtho2D` for the 2D HUD overlay |
| View Transform | `gluLookAt` — 3 distinct camera modes |
| Lighting | `GL_LIGHT0` with ambient + diffuse, Gouraud shading |
| Alpha Blending | Additive (fire/glow) + standard (smoke/clouds/rings/HUD) |
| Depth Buffering | Z-buffer with selective `glDepthMask` for transparency |
| Tessellation | `gluCylinder`, `gluDisk`, `glutSolidSphere` — 4 to 64 slices per object |
| Procedural Geometry | `GL_TRIANGLE_STRIP`, `GL_QUADS`, `GL_LINE_LOOP` for rings, skybox, orbits |
| Colour Gradients | Per-vertex colour interpolation for sky and atmosphere |
| Time-driven Animation | `glutGet(GLUT_ELAPSED_TIME)` drives all motion and effects |

---

## Team:

Riwaz Mahat 
Shreyana Adhikari 
Sulav Pandey 

---

## 📄 License

This project was developed as an academic project for the Computer Graphics course (CSC214), B.Sc. CSIT Semester III, Tribhuvan University. All rights reserved by the authors.
