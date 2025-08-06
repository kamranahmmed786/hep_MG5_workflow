# Sample Generation Guide

Once **MadGraph5\_aMC\@NLO** and all its dependent tools (e.g. LHAPDF, Pythia8) are properly configured, you can start generating simulated event samples using physics models. This document outlines important considerations and best practices for accurate and realistic sample generation.

---

## 1. Choosing the Correct Model (4F vs 5F Scheme)

Depending on the physics process and the treatment of bottom quarks (b-quarks), you should choose between:

* **4F Scheme**: Use `loop_sm`

  * The b-quark is treated as **massive**.
* **5F Scheme**: Use `loop_sm-np_b_mass`

  * The b-quark is treated as **massless**.

Your choice of flavor scheme will affect the accuracy and interpretation of your simulation, especially for processes involving b-jets or top production.

---

## 2. Handling Diagram Removal (DR Scheme) for Single Top

For **single top** production, diagrams may overlap with those contributing to `tt̄` (top pair) production. To avoid **double counting**, the **Diagram Removal (DR) scheme** is used.

This is handled using a plugin called **MadSTR**. To install and use it:

```bash
# Inside the MG5 interface
install MadSTR
```

Then run MadGraph with:

```bash
./bin/mg5_aMC --mode=MadSTR
```

This ensures MadSTR is used to correctly remove overlapping diagrams.

After generating a process using the `generate` and `output` commands in MG5 with MadSTR, navigate to the output directory and run:

```bash
cd /path/to/pp-tt
./bin/generate_events
```

This will launch the event generation process using the configuration stored in the directory.

---

## 3. Merging with FxFx (NLO Samples)

To avoid **double counting** between matrix-element and parton-shower jets when generating NLO samples, use the **FxFx merging** scheme. Edit the following configuration files:

### In `run_card.dat`:

```text
3 = ickkw        # FxFx merging scheme
40.0 = ptj       # Jet pt cut (adjust as needed)
```

### In `shower_card.dat`:

```text
Qcut   = 40.0  # Merging scale (match ptj)
njmax  = 2     # Maximal jet multiplicity
```

**Note**: Adjust `ptj` and `Qcut` according to your process and physics goals.

---

## 4. Applying TuneCP5 in Pythia8

To simulate the underlying event and parton showering realistically, apply the **TuneCP5** in `shower_card.dat`:

```text
Tune:pp 14
Tune:ee 7
MultipartonInteractions:ecmPow= 0.03344 
MultipartonInteractions:bProfile= 2 
MultipartonInteractions:pT0Ref= 1.41 
MultipartonInteractions:coreRadius= 0.7634 
MultipartonInteractions:coreFraction= 0.63 
ColourReconnection:range= 5.176 
SigmaTotal:zeroAXB= off 
SpaceShower:alphaSorder= 2 
SpaceShower:alphaSvalue= 0.118 
SigmaProcess:alphaSvalue= 0.118 
SigmaProcess:alphaSorder= 2 
MultipartonInteractions:alphaSvalue= 0.118 
MultipartonInteractions:alphaSorder= 2 
TimeShower:alphaSorder= 2 
TimeShower:alphaSvalue= 0.118 
SigmaTotal:mode = 0 
SigmaTotal:sigmaEl = 21.89 
SigmaTotal:sigmaTot = 100.309 
PDF:pSet = LHAPDF6:NNPDF31_nnlo_as_0118
```

---

## 5. Sample Cards

Sample configuration cards for several commonly used processes are available in the [`/Cards`](./Cards) directory of this repository. You can use them as templates and modify according to your analysis.

---
