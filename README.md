# DAAN DAAN

### Optimizing Metro Manila Traffic with the Braess' Paradox

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![Status](https://img.shields.io/badge/status-proof--of--concept-green.svg)]()

---

**DAAN DAAN is a graph-based simulation model that identifies strategic road closures to reduce, rather than worsen, overall network travel time in Metro Manila.**

## The Problem: ₱3.5 Billion Daily Loss

[cite_start]Metro Manila's traffic congestion results in an estimated economic loss of **₱3.5 billion per day**[cite: 17, 21]. [cite_start]Traditional solutions, like building more roads, often fail to provide long-term relief and can sometimes exacerbate the problem[cite: 19, 24]. [cite_start]This project introduces a counter-intuitive but scientifically-backed approach derived from the **Braess' Paradox**: sometimes, less is more[cite: 20, 25, 26].

## The Solution: A Proactive, Data-Driven Model

[cite_start]DAAN DAAN leverages the Braess' Paradox by systematically simulating the impact of closing individual road segments within a given traffic network[cite: 8, 32]. [cite_start]It's a proactive, automated tool designed to provide actionable insights for urban planners and local government units (LGUs)[cite: 14, 134].

### How It Works

The model follows a three-step process:

1.  [cite_start]**Input**: It takes user-defined parameters (location, trip samples, congestion severity) and geospatial data from OpenStreetMap[cite: 46, 47, 48, 50, 51, 52, 53, 54].
2.  [cite_start]**Process**: Using Python with `OSMnx` and `NetworkX`, it builds a road network graph[cite: 6, 56, 57, 58]. [cite_start]It then runs iterative simulations, closing one road segment at a time, re-routing traffic, and calculating the net change in total system travel time[cite: 8, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89].
3.  [cite_start]**Output**: The system generates a ranked list of the most beneficial road closures, quantifying the time saved and providing a "Winners vs. Losers" analysis to understand the distributive impact[cite: 70, 71, 72, 76, 77].

## Key Findings & Results

[cite_start]The model was tested on two distinct, high-traffic urban networks: **Alabang** and **Port Area, Manila**[cite: 7, 142].

* [cite_start]**Alabang**: The optimal road closure (Ilaya Street) resulted in a total system travel time saving of **1,343.90 minutes** across 5,000 simulated trips[cite: 157].
* [cite_start]**Port Area**: The best-performing closure (Main Road 2) saved **36.94 minutes** in system-wide travel time[cite: 163].

[cite_start]In both cases, a paired sample t-test confirmed that the reductions in travel time were **statistically significant ($p < .001$)**[cite: 11, 165].

## Why DAAN DAAN?

| Tool                 | Approach                 | Description                                                                                                        |
| :------------------- | :----------------------- | :----------------------------------------------------------------------------------------------------------------- |
| **Waze / Google Maps** | **REACTIVE** | [cite_start]Responds to existing traffic conditions in real-time but doesn't address the root cause of congestion[cite: 132, 136].  |
| **DAAN DAAN** | **PROACTIVE & AUTOMATED** | Identifies systemic improvements *before* they are implemented. [cite_start]It's user-friendly and built for rapid analysis[cite: 134, 139]. |
| **SUMO / VISSIM** | **EXPERT-DRIVEN** | [cite_start]Powerful but highly technical simulation platforms requiring specialized knowledge and extensive manual setup[cite: 133, 137]. |

## Project Roadmap

This project was developed over an 8-week timeline, from initial planning and system architecture to data simulation and final analysis.



[Image of the project's 8-week Gantt chart timeline]


## Getting Involved

[cite_start]DAAN DAAN is currently a proof-of-concept with the potential to become a powerful decision-support tool for traffic management in the Philippines[cite: 14]. We welcome collaboration with urban planners, data scientists, and LGUs.

* **Read the Full Research Paper**: `https://drive.google.com/file/d/1dYpm29cCUe28CfWgTP421KB13n0SnngC/view?usp=sharing`
* **Contact the Team**: `mailto:contact@daandaan.ph?subject=Inquiry%20about%20the%20DAAN%20DAAN%20Project`

---

*© 2025 DAAN DAAN Initiative.*
