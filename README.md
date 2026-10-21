# Simulating Nuclear Fission Chain Reactions
**Author:** Henry O'Rorke

## 📖 Introduction
Nuclear fission is the splitting of a heavy nucleus after it absorbs a neutron. It is one of the most significant discoveries in physics. It was first achieved experimentally by Hahn and Strassmann in 1938 and explained by Meitner and Frisch shortly after.

In this project, I simulate fission chain reactions using a **Monte Carlo model of neutron motion**. Individual neutrons are tracked probabilistically through a fissile material as they scatter, get absorbed, trigger more fission, or escape the material. The focus of the simulation is on the neutron multiplication factor \(k\), which determines whether a chain reaction dies out, sustains itself, or grows exponentially (\(k < 1\), \(k = 1\), or \(k > 1\)).

## 🗂️ Table of Contents
* [1. Fission](#1-fission)
  * [Nuclear Binding Energy](#11-nuclear-binding-energy)
  * [Mass-Energy Equivalence and Q-Value](#12-mass-energy-equivalence-and-q-value)
  * [Why Uranium Fissions and Iron Doesn't](#13-why-uranium-fissions-and-iron-doesnt)
* [2. Monte Carlo Neutron Transport](#2-monte-carlo-neutron-transport)
  * [Cross Sections and Mean Free Path](#21-cross-sections-and-mean-free-path)
  * [Monte Carlo Simulation](#22-monte-carlo-simulation)
  * [Plotting Neutron Paths](#23-plotting-neutron-paths)
* [3. Criticality](#3-criticality)
  * [Running a Full Generation](#31-running-a-full-generation)
  * [Computing \(k\) and Finding Critical Radius and Mass](#32-computing-k-and-finding-critical-radius-and-mass)
* [4. Enrichment](#4-enrichment)
  * [Natural vs. Reactor vs. Weapon Grade Uranium](#41-natural-vs-reactor-vs-weapon-grade-uranium)

## 💻 Requirements & Environment
To run the simulation files in this repository, you will need Python 3 installed with the following scientific computing libraries:
```bash
pip install numpy matplotlib
```

## 1. Fission

### 1.1: Nuclear Binding Energy
* **Concept:** Evaluates nuclear stability using binding energy per nucleon (\(BE/A = \text{Total Binding Energy} / A\)).
* **Physics Framework:** Explains the balance between short-range strong nuclear attraction and long-range electromagnetic repulsion across different mass numbers.
* **Code Implementation:** Contains data mapping from the Atomic Mass Evaluation (AME2020) and uses `matplotlib` to plot the iconic Nuclear Binding Energy Curve, highlighting key elements like Deuterium, Helium-4, Iron-56, and U-235.

### 1.2: Mass-Energy Equivalence and Q-Value
* **Concept:** Applies Einstein's mass-energy equivalence (\(E = \Delta m c^2\)) to calculate energy dynamics in nuclear reactions.
* **Physics Framework:** Utilizes the nuclear Q-value equation to determine whether a reaction is exothermic (\(Q > 0\)) or endothermic (\(Q < 0\)).
* **Code Implementation:** Calculates the exact \(Q\)-value (in MeV) for a standard \(^{235}_{92}\text{U}\) fission event by evaluating precise reactant and product atomic masses in unified atomic mass units (\(u\)).

### 1.3: Why Uranium Fissions and Iron Doesn't
* **Concept:** Connects the geometry of the binding energy curve to the possibility of fission in heavy elements versus light elements.
* **Physics Framework:** Details why splitting \(^{235}_{92}\text{U}\) moves daughter elements toward the stable Iron-56 peak (releasing ~200 MeV), while attempting to split Iron-56 yields an endothermic reaction (\(Q < 0\)).

## 2. Monte Carlo Neutron Transport

### 2.1: Cross Sections and Mean Free Path
* **Concept:** Models the probabilistic interaction types of fast neutrons traveling through a medium: fission, radiative capture, and scattering.
* **Physics Framework:** Maps interaction likelihoods via cross-sections (\(\sigma\)) measured in barns and derives the average distance traveled between collisions using the mean free path formula: \(\lambda = \frac{1}{n \sigma_{\text{total}}}\).
* **Code Implementation:** Establishes physical material constants for U-235 (density of \(19.1 \ \text{g/cm}^3\), Avogadro's number, and fast neutron cross-sections) to compute branching probabilities for the simulation engine.

### 2.2: Monte Carlo Simulation
* **Concept:** Uses random sampling to track individual neutron flight paths and their endpoints inside a boundary.
* **Physics Framework:** Models neutron flight distances using an exponential distribution based on the computed mean free path.
* **Code Implementation:** Defines the `transport_neutron` logic to systematically trace positions and return categorical interaction states such as fission, escape, capture, or scatter.

### 2.3: Plotting Neutron Paths
* **Concept:** Generates graphical tracking lines of separate neutron generations inside a defined geometrical system.
* **Physics Framework:** Evaluates boundary conditions against spatial coordinate changes to count escaping particles.
* **Code Implementation:** Projects three-dimensional mathematical vectors onto a two-dimensional plane, overlaying interaction point color keys for Fission, Escape, Capture, and Scatter over a visual circle boundary.

## 3. Criticality

### 3.1: Running a Full Generation
* **Concept:** Evaluates population variations from one generation of particles to the next.
* **Physics Framework:** Explores neutron production based on localized fission results, applying average fission yields to determine population expansion or contraction.
* **Code Implementation:** Establishes the `run_generation` mechanism to update spatial vector arrays by stripping captured particles and appending multiple new paths at fission coordinate sets.

### 3.2: Computing \(k\) and Finding Critical Radius and Mass
* **Concept:** Calculates the system stability parameter across varying physical scales.
* **Physics Framework:** Links geometric particle escape rates to internal multiplying effects to find where \(k=1\).
* **Code Implementation:** Runs iterative loops across an array of spherical dimensions, calculating stable \(k\) system metrics to output corresponding critical masses using metal density configurations.

## 4. Enrichment

### 4.1: Natural vs. Reactor vs. Weapon Grade Uranium
* **Concept:** Explores fission boundary behaviors under changing chemical concentration bounds.
* **Physics Framework:** Evaluates the introduction of U-238 non-fissile capture agents into a fast neutron field.
* **Code Implementation:** Combines mixed elemental cross-sections to modify mean free paths, generating stability data curves from natural uranium baselines up to high weapon-grade weapon thresholds.
