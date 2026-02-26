# 🌐 VG's OPEN EYE

> **A real-time 3D geospatial intelligence & situational-awareness interface built around CesiumJS.**

<p align="center">
  <strong>VG31</strong> · <a href="https://github.com/VG31OP">VG31OP</a> · <a href="https://github.com/VG31OP/VG-s-OPEN-EYE">VG-s-OPEN-EYE</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/PROJECT-VG's%20OPEN%20EYE-00D9FF?style=for-the-badge&logo=github&logoColor=white" alt="VG's OPEN EYE">
  <img src="https://img.shields.io/badge/ENGINE-CesiumJS-00AEEF?style=for-the-badge" alt="CesiumJS">
  <img src="https://img.shields.io/badge/MAP-OpenStreetMap-7CB342?style=for-the-badge&logo=openstreetmap&logoColor=white" alt="OpenStreetMap">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/STATUS-ACTIVE-00C853?style=flat-square" alt="Active">
  <img src="https://img.shields.io/badge/API%20KEY-CORE%20GLOBE%20NOT%20REQUIRED-8A2BE2?style=flat-square" alt="Core globe does not require an API key">
  <img src="https://img.shields.io/badge/TESTS-2601%20PASSING-00C853?style=flat-square" alt="2601 tests passing">
</p>

---

### ⚡ The idea

**One globe. Multiple data systems. One operational view.**

VG's OPEN EYE turns a geographic information space into an interactive 3D command-center experience for exploring locations and visualizing supported real-time and reference datasets.

> 🛰️ **Track** · ✈️ **Observe** · 🌋 **Analyze** · 📍 **Navigate** · 🎙️ **Control**

**Developer:** VG31  
**GitHub:** [VG31OP](https://github.com/VG31OP)  
**Repository:** [VG31OP/VG-s-OPEN-EYE](https://github.com/VG31OP/VG-s-OPEN-EYE)

---


---

## Overview

**VG's OPEN EYE** is a cinematic, tactical-style 3D geospatial visualization application designed to bring multiple live and reference data layers together on a single interactive globe.

The project combines a CesiumJS globe with an information-dense command-center interface for exploring geographic locations and visualizing different classes of real-world data, including aircraft, satellites, vessels, earthquakes, CCTV sources, traffic-related information, space missions, weather-oriented layers, and other geospatial datasets supported by the application.

The application is designed around one core idea:

> **Turn a complex geographic information space into one navigable, interactive operational view.**

Instead of presenting every dataset as a separate dashboard, VG's OPEN EYE places the available information into a common spatial context so the user can move around the globe, inspect locations, toggle data layers, search for places, and interact with the scene.

---


---

## ✨ Highlights

- 🌍 **Interactive 3D globe** powered by CesiumJS
- 🗺️ **OpenStreetMap-based imagery** for the keyless map stack
- ⛰️ **3D terrain support** through the existing Re:Earth terrain configuration
- ✈️ **Live aircraft visualization**
- 🛰️ **Satellite and space-object visualization**
- 🚢 **Vessel / AIS visualization**
- 🌋 **Earthquake visualization**
- 📹 **CCTV / camera data layers**
- 🚦 **Traffic and mobility-oriented layers**
- 🚀 **Space mission information**
- 🎙️ **Voice-driven application actions**
- 📍 **Location search and geocoding**
- 🔄 **Layer-based data architecture**
- 🎛️ **Tactical HUD and visualization controls**
- 🎥 **Camera/navigation controls**
- 🧭 **Scene and visual-style controls**
- 🧪 **Automated testing and QA tooling**
- 🔐 **Keyless core globe operation**
- 🧩 **Modular data adapters and visualization layers**

---

# Table of Contents

- [Overview](#overview)
- [Highlights](#-highlights)
- [Core Philosophy](#core-philosophy)
- [Architecture](#architecture)
- [Technology Stack](#technology-stack)
- [Map and Globe Stack](#map-and-globe-stack)
- [Data Layers](#data-layers)
- [Location Search and Geocoding](#location-search-and-geocoding)
- [Voice Interaction](#voice-interaction)
- [User Interface](#user-interface)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Environment Configuration](#environment-configuration)
- [Running the Project](#running-the-project)
- [Production Build](#production-build)
- [Testing](#testing)
- [Development Scripts](#development-scripts)
- [Data Sources](#data-sources)
- [API and Key Philosophy](#api-and-key-philosophy)
- [Performance Considerations](#performance-considerations)
- [Troubleshooting](#troubleshooting)
- [Development Guidelines](#development-guidelines)
- [Adding a New Data Layer](#adding-a-new-data-layer)
- [Security](#security)
- [Privacy](#privacy)
- [Open-Source Attribution](#open-source-attribution)
- [Media and Historical Assets](#media-and-historical-assets)
- [Project Identity](#project-identity)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Testing Checklist](#testing-checklist)
- [License](#license)
- [Credits](#credits)

---


---

# Core Philosophy

<div align="center">

| 🌍 **ONE VIEW** | 🧩 **LAYERED** | 🔓 **KEYLESS CORE** | 🛡️ **RESILIENT** |
|---|---|---|---|
| Geographic context in one place | Independent information layers | No mandatory Google credential for the core globe | External failures should degrade gracefully |

</div>

VG's OPEN EYE is built around a few principles.

### 1. One geographic context

Different information sources become more useful when they can be viewed relative to one another.

Aircraft, vessels, satellites, earthquakes, cameras, locations, and other datasets can all be interpreted geographically.

### 2. Layer everything

The application uses a layer-oriented approach so users can enable and disable individual information systems instead of being forced to view everything simultaneously.

### 3. Keep the globe accessible

The core globe experience should not depend on a mandatory paid Google Maps credential.

The current keyless globe stack uses CesiumJS with OpenStreetMap imagery and the project's existing terrain configuration.

### 4. Preserve the existing application architecture

The project is intentionally modular.

The globe, data management, UI orchestration, voice actions, scenes, proxy configuration, and data adapters are separated so that individual systems can evolve without requiring a complete application rewrite.

### 5. Prefer graceful degradation

External data providers can fail, rate-limit, change availability, or temporarily return incomplete information.

The application should therefore fail gracefully where possible instead of making one unavailable service prevent the rest of the interface from operating.

---


---

# Architecture

At a high level, the application can be viewed as several cooperating systems:

```text
                         ┌──────────────────────┐
                         │    VG's OPEN EYE     │
                         │      Frontend        │
                         └──────────┬───────────┘
                                    │
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
              ▼                     ▼                     ▼
      ┌───────────────┐     ┌───────────────┐     ┌───────────────┐
      │ Cesium Scene  │     │ UI / HUD      │     │ Voice System  │
      │ Globe + View  │     │ Controls      │     │ Actions       │
      └───────┬───────┘     └───────────────┘     └───────┬───────┘
              │                                           │
              ▼                                           ▼
      ┌─────────────────────────────────────────────────────────┐
      │                    Application State                    │
      └──────────────────────────┬──────────────────────────────┘
                                 │
             ┌───────────────────┼───────────────────┐
             │                   │                   │
             ▼                   ▼                   ▼
       Aircraft Data       Satellite Data       Vessel Data
             │                   │                   │
             ├──────────────┬────┴──────────────┬────┤
             ▼              ▼                   ▼    ▼
        Earthquakes       CCTV              Traffic  Space
             │              │                   │    Missions
             └──────────────┴──────────┬────────┴────┘
                                       │
                                       ▼
                              Cesium Data Layers
```

The exact implementation is distributed across the project's source modules, data adapters, scene systems, UI orchestration, and development proxy configuration.

---


---

# Technology Stack

| Area | Technology |
|---|---|
| 🌐 3D Globe | **CesiumJS** |
| ⚡ Frontend / Build | **JavaScript + Vite** |
| 🗺️ Basemap | **OpenStreetMap** |
| ⛰️ Terrain | **Re:Earth quantized-mesh terrain** |
| 📍 Geocoding | **OpenStreetMap Nominatim** |
| 🧪 Testing | **Node/npm test & project QA tooling** |

> 💡 **Design principle:** keep the visualization engine, data adapters, application state, and UI controls modular so one system can evolve without forcing a full rewrite.

## Frontend

- **JavaScript**
- **CesiumJS**
- **Vite**
- HTML / CSS
- Modular browser-side application architecture

## Geospatial Visualization

- **CesiumJS Globe**
- **OpenStreetMap imagery**
- Existing **Re:Earth quantized-mesh terrain** configuration
- Cesium camera and scene systems
- Cesium entities/primitives and visualization layers

## Geocoding

- **OpenStreetMap Nominatim**

Used for place search and reverse-geocoding fallback in the keyless setup.

## Data / Integrations

The project contains adapters and proxy handling for several data systems, including aircraft, satellites, AIS/vessels, earthquakes, CCTV, traffic/mobility, radio-related information, and space-mission data.

The project also contains CelesTrak, OpenSky, AIS, and Radio Browser proxy handling in its development configuration.

---


---

# Map and Globe Stack

The central visualization engine is CesiumJS.

The current keyless map stack is designed around:

```text
CesiumJS
   │
   ├── Cesium Globe
   │
   ├── OpenStreetMap imagery
   │
   └── Existing Re:Earth terrain configuration
```

## OpenStreetMap

OpenStreetMap imagery is used as the current keyless basemap.

This avoids making a Google Maps API key a requirement for the core globe.

## Terrain

The project contains an existing Re:Earth quantized-mesh terrain configuration.

Terrain availability depends on the external terrain service being reachable.

## Important distinction

The globe itself and the live data layers are separate systems.

The application can render its geographic scene independently from whether a particular live data provider is currently responding.

---


---

# Data Layers

<div align="center">

| Layer | Purpose |
|:---:|---|
| ✈️ | **Live Flights** |
| 🛡️ | **Military Flights** |
| 🛰️ | **Satellites** |
| 🚢 | **Vessels / AIS** |
| 🌋 | **Earthquakes** |
| 📹 | **CCTV** |
| 🚦 | **Traffic / Mobility** |
| 🚀 | **Space Missions** |
| 📻 | **Radio / Directory Data** |

</div>

VG's OPEN EYE is designed around independent data layers.

The available project systems include:

## ✈️ Live Flights

Aircraft information can be visualized geographically, allowing users to inspect the global distribution and movement of aircraft supported by the configured data source.

The project also contains dedicated aircraft-related modules for classification, icons, and motion modeling.

## 🛡️ Military Flights

A dedicated military-flight layer provides a separate visualization path for aircraft data classified by the application's military-flight data pipeline.

Availability depends on the upstream source and its current coverage.

## 🛰️ Satellites

Satellite visualization provides a spatial view of supported orbiting objects.

The project contains satellite-related data handling and space-object visualization.

## 🚢 Vessels

The vessel system uses AIS-oriented data and includes an AIS stream adapter.

Vessel information can be represented geographically when the upstream stream is available.

## 🌋 Earthquakes

Earthquake data can be displayed as a geographic layer so seismic events can be interpreted in relation to other map information.

## 📹 CCTV

The CCTV system provides camera-oriented geospatial information.

The repository also contains dedicated development tooling for CCTV source packs.

## 🚦 Traffic / Mobility

Traffic and mobility-oriented data layers can be represented on the globe through the project's data-layer architecture.

## 🚀 Space Missions

The application contains support for space-mission information and a launch-oriented library/data workflow.

## 📻 Radio

The project includes Radio Browser-related proxy handling and directory-oriented functionality.

---


---

# Layer Architecture

Data systems are intentionally separated from the visualization layer.

A typical flow is:

```text
External Data Source
        │
        ▼
   Data Adapter
        │
        ▼
 Normalize / Validate
        │
        ▼
 Application Data Model
        │
        ▼
 Cesium Visualization Layer
        │
        ▼
 Interactive Globe
```

This separation makes it possible to change an upstream source without rewriting the entire visualization system.

---


---

# Location Search and Geocoding

The project supports geographic place lookup.

The current keyless approach uses OpenStreetMap Nominatim when a Google Maps credential is not available.

## Forward geocoding

A place name can be resolved to coordinates and bounding information.

Conceptually:

```text
"Delhi"
   │
   ▼
Nominatim
   │
   ▼
Latitude / Longitude / Bounding Box
   │
   ▼
Camera / Location Framing
```

## Reverse geocoding

Coordinates can be resolved back into a human-readable location.

```text
Latitude + Longitude
        │
        ▼
    Nominatim
        │
        ▼
Human-readable location
```

This functionality is also used by voice-driven location actions.

---


---

# Voice Interaction

VG's OPEN EYE includes a voice-oriented action system.

Voice interaction is designed around application actions rather than directly manipulating the Cesium scene from arbitrary speech.

A simplified flow is:

```text
Voice Input
    │
    ▼
Intent / Action Resolution
    │
    ▼
Application Action
    │
    ├── Search location
    ├── Navigate camera
    ├── Control layers
    ├── Change visualization state
    └── Perform supported scene actions
```

The voice system is integrated with the same application state and scene systems used by the graphical interface.

---


---

# User Interface

The interface uses a tactical command-center visual language.

Major interface concepts include:

- Data layer controls
- HUD information
- Scene controls
- Display controls
- Visualization presets
- Location controls
- Voice controls
- Camera/navigation interaction
- Status indicators
- Layer state indicators

The UI is designed to keep the globe as the primary visual workspace while presenting controls around it.

---


---

# Project Structure

The repository is organized into application source, data systems, scripts, documentation, public assets, and configuration.

A simplified view:

```text
VG-s-OPEN-EYE/
│
├── public/
│   ├── models/
│   └── other public assets
│
├── src/
│   ├── data/
│   │   ├── aircraftClass.js
│   │   ├── aircraftIcons.js
│   │   ├── aisStreamAdapter.js
│   │   ├── flights.js
│   │   ├── militaryFlights.js
│   │   ├── motionModel.js
│   │   ├── cctv.js
│   │   ├── traffic.js
│   │   └── local_data/
│   │
│   ├── annotations/
│   ├── scenes/
│   ├── voice/
│   ├── main.js
│   ├── ui.js
│   └── other application modules
│
├── scripts/
│   ├── development helpers
│   ├── QA scripts
│   └── source-pack tooling
│
├── docs/
│   ├── media/
│   ├── opensky-auth.md
│   └── other documentation
│
├── .github/
│   └── GitHub configuration
│
├── package.json
├── package-lock.json
├── vite.config.js
├── .env.example
├── DATA_SOURCES.md
├── TESTING.md
├── SECURITY.md
└── README.md
```

The exact directory contents may evolve as the project develops.

---


---

# Getting Started

## Requirements

Before starting, install:

- **Node.js**
- **npm**
- A modern Chromium-based browser or another browser with the required WebGL capabilities
- Git, if cloning or working with the repository

Check Node and npm:

```bash
node --version
npm --version
```

---

# Installation

Clone the repository:

```bash
git clone https://github.com/VG31OP/VG-s-OPEN-EYE.git
```

Enter the project:

```bash
cd VG-s-OPEN-EYE
```

Install dependencies:

```bash
npm install
```

---


---

# Environment Configuration

The repository includes:

```text
.env.example
```

Use it as the starting point for local environment configuration.

The current keyless globe setup is designed so that the application can run without a mandatory Google Maps API key.

For a basic keyless run, a `.env` file may not be required.

If you create one, keep secrets local and never commit private credentials.

Example workflow:

```bash
cp .env.example .env
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Then configure only the variables you actually need.

---


---

# Running the Project

Start the development server:

```bash
npm run dev
```

Vite will provide the local development URL.

Open that URL in your browser.

The application should load the Cesium scene and initialize the available data systems.

---


---

# Production Build

Create a production build:

```bash
npm run build
```

The build output is generated by the project's Vite configuration.

A successful build confirms that the application's modules can be transformed and bundled successfully.

---


---

# Testing

### 🧪 Current verification

```text
┌─────────────────────────────────────────────┐
│  TEST SUITE                                 │
│                                             │
│  ✓ 2601 / 2601 tests passed                 │
│  ✓ 100% recorded pass rate                  │
│                                             │
│  BUILD                                      │
│  ✓ Production build successful              │
└─────────────────────────────────────────────┘
```

The exact test count may change as the project evolves.

Run the complete automated test suite:

```bash
npm test
```

The project has a substantial automated test and QA suite.

At the time of the current project audit, the recorded test result was:

```text
2601 / 2601 tests passed
100% pass rate
```

The exact number may change as additional tests are added.

## Recommended verification

After changes, run:

```bash
npm test
npm run build
```

If you changed a feature involving the globe or live data, also perform a manual browser verification.

---


---

# Development Scripts

The repository contains several development helpers.

Examples include:

```text
scripts/dev-cctv.sh
scripts/dev-fresh.sh
scripts/dev-secure.sh
```

These scripts support different development workflows, including CCTV source-pack development, fresh development-server startup, and secure development-server workflows.

Always inspect a script before adapting it to a different operating system.

---


---

# Data Sources

VG's OPEN EYE integrates with multiple external datasets and services.

The project contains dedicated source documentation in:

```text
DATA_SOURCES.md
```

Relevant systems represented in the repository include:

- OpenStreetMap
- Nominatim
- Re:Earth terrain
- OpenSky-related aircraft data
- CelesTrak
- AISStream
- Launch Library / The Space Devs
- Natural Earth
- Radio Browser
- Other source-specific datasets and local assets

Each source has its own availability, rate limits, terms, licensing, and data-quality characteristics.

Always consult the project's source documentation before deploying a data integration commercially or at scale.

---


---

# API and Key Philosophy

> 🟢 **Core globe:** designed to run without a mandatory Google Maps API key.

```text
                 VG's OPEN EYE
                       │
             ┌─────────┴─────────┐
             │                   │
        CesiumJS Globe       Data Systems
             │                   │
       ┌─────┴─────┐       ┌─────┴─────┐
       │           │       │           │
      OSM       Terrain   Live Data   Local Data
```

The current keyless globe stack uses:

**CesiumJS + OpenStreetMap imagery + the project's existing terrain configuration.**

One of the major changes in the current version is the move away from requiring a paid Google Maps credential for the basic globe experience.

## Core globe

The keyless globe uses:

```text
CesiumJS
+
OpenStreetMap imagery
+
existing terrain configuration
```

## Geocoding

The keyless geocoding path uses:

```text
OpenStreetMap Nominatim
```

## Important

"Keyless" does **not** mean "offline."

Live datasets and external services may still require network access.

For example, live aircraft, satellite, vessel, earthquake, CCTV, weather, or mission information can depend on their respective upstream providers.

---


---

# External Service Reliability

Live data is inherently less predictable than local data.

Possible conditions include:

- Provider downtime
- Rate limiting
- Network failure
- Missing records
- Delayed updates
- Invalid or incomplete upstream data
- Provider-side API changes
- Temporary CORS/proxy problems

A failed external source should not automatically be interpreted as an application failure.

When debugging a data layer, first determine whether:

1. The frontend loaded correctly.
2. The proxy initialized correctly.
3. The upstream provider responded.
4. The response contained usable data.
5. The adapter normalized the response.
6. The visualization layer received the normalized data.

---


---

# Performance Considerations

A 3D globe displaying multiple live datasets can become computationally expensive.

Performance depends on:

- Number of rendered entities
- Camera altitude
- Active layers
- Update frequency
- Browser WebGL performance
- Terrain detail
- Model complexity
- Number of simultaneous animations
- Network latency
- Data refresh frequency

## Practical recommendations

If performance drops:

1. Disable unnecessary data layers.
2. Reduce the number of simultaneously displayed entities.
3. Avoid excessive model detail.
4. Check browser GPU/WebGL status.
5. Inspect network requests.
6. Check the browser console for repeated errors.
7. Test each data layer individually.

Do not optimize by removing functionality before identifying the actual bottleneck.

---


---

# Troubleshooting

## The globe does not appear

Check:

```text
Browser console
Network tab
Cesium initialization
WebGL support
```

Then verify that the development server started successfully.

---

## The globe is visible but imagery is missing

Check:

- Network connectivity
- OpenStreetMap tile requests
- Browser console
- Imagery-layer initialization
- Provider availability

---

## Terrain does not load

Terrain is external to the core Cesium rendering engine.

Check:

- Network access
- Terrain endpoint availability
- Browser console
- Terrain initialization errors

The application should still be able to provide a globe when terrain is unavailable, depending on the current configuration.

---

## A live data layer is empty

Check the upstream provider first.

A layer can be empty because:

- The provider returned no records
- The provider is unavailable
- The current geographic area has no records
- Authentication is required for that provider
- A rate limit was reached
- Data parsing failed
- The request was blocked

---

## Location search does not work

Check Nominatim requests in the browser/network logs.

Also verify that the search query is valid and that the external geocoding service is reachable.

---

## Voice actions do not work

Check:

- Browser microphone permission
- Browser speech support
- Voice-system initialization
- Console errors
- Whether the requested action is supported

---


---

# Development Guidelines

## Keep changes focused

VG's OPEN EYE contains several interconnected systems.

When changing one feature:

- Change the smallest appropriate surface.
- Avoid unrelated refactors.
- Preserve existing interfaces.
- Run the test suite.
- Build before committing.

## Do not replace working infrastructure unnecessarily

In particular, do not replace the existing globe architecture simply to solve a visual problem.

Prefer modifying the current Cesium configuration over introducing another rendering stack.

## Preserve data-source attribution

External datasets and libraries may have their own licenses and attribution requirements.

Do not remove third-party attribution merely because it does not match the project's branding.

---


---

# Adding a New Data Layer

A new data layer should generally follow the existing architecture.

A useful conceptual structure is:

```text
1. Source
   ↓
2. Adapter
   ↓
3. Normalized model
   ↓
4. Validation
   ↓
5. State / data manager
   ↓
6. Cesium visualization
   ↓
7. UI layer control
```

## Step 1 — Identify the source

Document:

- Source name
- Endpoint
- Update frequency
- Terms of use
- Authentication requirements
- Geographic coverage
- Expected response format

## Step 2 — Create or extend an adapter

Normalize external data into an application-friendly structure.

Avoid leaking provider-specific response formats throughout the UI.

## Step 3 — Validate data

Handle:

- Missing coordinates
- Invalid timestamps
- Missing IDs
- Duplicate records
- Invalid geometry
- Unexpected provider responses

## Step 4 — Connect to the data manager

The data should become available through the application's existing state/data-management path.

## Step 5 — Render

Use Cesium entities/primitives or the existing visualization abstraction.

## Step 6 — Add controls

Expose the layer through the existing UI rather than creating an unrelated control system.

## Step 7 — Test

Add automated tests for:

- Parsing
- Normalization
- Invalid data
- Empty responses
- Expected records

Then run:

```bash
npm test
```

---


---

# Security

Do not commit secrets.

Never place private API keys directly into source files.

Use environment variables for credentials where a provider requires them.

Before publishing changes, check:

```bash
git diff
git status
```

Also inspect:

```text
.env
.env.local
credentials
tokens
private configuration
```

The repository should not contain private credentials.

---


---

# Privacy

VG's OPEN EYE can process or visualize data obtained from external providers.

Users and developers should understand that:

- External services may receive requests generated by the application.
- Live data providers have their own privacy policies and terms.
- Location searches may be sent to the configured geocoding service.
- Voice functionality may depend on browser/platform capabilities and configured services.
- CCTV and other third-party datasets may have their own restrictions.

Do not assume that external data is private merely because it is displayed locally in the browser.

---


---

# Open-Source Attribution

VG's OPEN EYE incorporates or references multiple external open-source projects and datasets.

Examples documented in the repository include:

### Skylight

Aircraft-related code and algorithms contain attribution to:

```text
https://github.com/cpaczek/skylight
```

### Natural Earth

The project contains Natural Earth geospatial boundary data:

```text
https://github.com/nvkelso/natural-earth-vector
```

### The Space Devs

Launch-related documentation references The Space Devs and its terms:

```text
https://github.com/TheSpaceDevs/Tutorials
```

### AISStream

AIS-related functionality references upstream AISStream resources and issue tracking.

These references should remain intact where required by the applicable licenses or source terms.

---


---

# Media and Historical Assets

The repository contains legacy media assets used for documentation and project history.

Some of the capture GIFs are specifically attributed to their original creator and copyright owner.

Those notices should not be interpreted as claiming that the legacy media was created by VG31.

The current application identity is:

> **VG's OPEN EYE — Developer: VG31**

Historical asset ownership remains separate from current application branding.

---


---

# Project Identity

<div align="center">

# 🌐 VG's OPEN EYE

### `VG31` · `VG31OP`

**A 3D geospatial intelligence interface built for exploration, visualization, and situational awareness.**

[![GitHub](https://img.shields.io/badge/GitHub-VG31OP-181717?style=for-the-badge&logo=github)](https://github.com/VG31OP)
[![Repository](https://img.shields.io/badge/Repository-VG--s--OPEN--EYE-00D9FF?style=for-the-badge)](https://github.com/VG31OP/VG-s-OPEN-EYE)

</div>

## Current identity

**VG's OPEN EYE**

**Developer:** VG31

**GitHub:** VG31OP

**Repository:**  
https://github.com/VG31OP/VG-s-OPEN-EYE

## Git remote

The intended repository remote is:

```text
https://github.com/VG31OP/VG-s-OPEN-EYE.git
```

Verify locally with:

```bash
git remote -v
```

---


---

# Roadmap

> 🚀 **Direction:** make the globe more capable without turning the application into a tangled collection of unrelated systems.

- [ ] Improved layer discovery and management
- [ ] More robust live-data caching
- [ ] Better data-source health indicators
- [ ] More resilient provider fallback handling
- [ ] Expanded geospatial datasets
- [ ] Improved scene presets
- [ ] More advanced camera/navigation actions
- [ ] Additional voice actions
- [ ] Better offline/local-data workflows
- [ ] More detailed operational analytics
- [ ] Improved accessibility
- [ ] Performance optimization for very large entity sets
- [ ] More comprehensive automated integration testing

Potential future directions for the project include:

- Improved layer discovery and management
- More robust live-data caching
- Better data-source health indicators
- More resilient provider fallback handling
- Expanded geospatial datasets
- Improved scene presets
- More advanced camera/navigation actions
- Additional voice actions
- Better offline/local-data workflows
- More detailed operational analytics
- Improved accessibility
- Performance optimization for very large entity sets
- More comprehensive automated integration testing

The roadmap is intentionally flexible because external data providers and the project's requirements can evolve.

---


---

# Contributing

Contributions should preserve the project's modular architecture and existing behavior.

Before submitting a change:

```bash
npm test
npm run build
```

For changes involving external services, also verify:

- provider availability
- rate limits
- attribution requirements
- error handling
- empty-response behavior
- authentication requirements

For changes involving the globe, verify:

- imagery
- terrain
- camera controls
- entity rendering
- layer toggles
- performance

For UI changes, verify:

- desktop layout
- responsive behavior
- controls
- accessibility
- existing HUD behavior

---


---

# Testing Checklist

Use this checklist before considering a major change complete.

## Application

- [ ] Application starts
- [ ] Cesium globe renders
- [ ] OpenStreetMap imagery loads
- [ ] Terrain behaves correctly
- [ ] Camera controls work
- [ ] UI loads correctly
- [ ] HUD loads correctly

## Data

- [ ] Flights layer works
- [ ] Military flights layer works
- [ ] Satellite layer works
- [ ] Vessel layer works
- [ ] Earthquake layer works
- [ ] CCTV layer works
- [ ] Traffic layer works
- [ ] Space/mission layer works where configured

## Interaction

- [ ] Location search works
- [ ] Reverse geocoding works
- [ ] Voice controls work where supported
- [ ] Layer toggles work
- [ ] Visualization controls work
- [ ] Camera navigation works

## Build

```bash
npm test
npm run build
```

- [ ] Tests pass
- [ ] Production build succeeds
- [ ] No unexpected console errors
- [ ] No credentials accidentally committed

---


---

# License

VG's OPEN EYE contains a mixture of project-owned source code, external libraries, datasets, and historical media.

Before redistributing or using individual components commercially, consult the relevant license and source documentation.

In particular, do not assume that all media, datasets, or third-party integrations share the same license as the application's source code.

Refer to:

```text
DATA_SOURCES.md
```

and the individual attribution/license files distributed with the relevant assets.

---


---

# Credits

## Project

**VG's OPEN EYE**

Developed by:

**VG31**

GitHub:

**VG31OP**

Repository:

**VG31OP/VG-s-OPEN-EYE**

## Technologies and sources

The project builds on the work of numerous open-source projects, data providers, and standards, including:

- CesiumJS
- OpenStreetMap
- Nominatim
- Re:Earth terrain
- OpenSky-related data
- CelesTrak
- AISStream
- The Space Devs / Launch Library
- Natural Earth
- Radio Browser
- Skylight
- Numerous npm packages and their maintainers

Please preserve the attribution and licensing information supplied by those projects.

---

# Final Note

<div align="center">

### 🌍 **VG's OPEN EYE**

**One globe. Multiple data systems. One operational view.**

`VG31` · `VG31OP`

</div>

VG's OPEN EYE is intended to be a flexible geospatial visualization platform rather than a replacement for authoritative operational systems.

Live information can be incomplete, delayed, inaccurate, unavailable, or subject to provider limitations.

Treat displayed information as visualization and situational-awareness data, and verify important decisions against authoritative sources.

---

## VG's OPEN EYE

**See the world from a different angle.**

**Developer:** VG31  
**GitHub:** VG31OP  
**Repository:** https://github.com/VG31OP/VG-s-OPEN-EYE
