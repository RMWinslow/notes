---
title: Economics Notes Index
layout: default
nav_exclude: true
---

# Economics Notes Index

This file tracks economics notes that have not yet been migrated into the nav-indexed markdown folder structure. As each file is converted to Jekyll markdown and placed in the appropriate section, it should be removed from this list.

```
_detritus/research/arrowroot/
├── arrowrootnotes.html
├── arrownotes.html
├── rootnotes.html              (empty)
├── Root - Incentive Stuff.pdf
└── debug.log                   (junk)

econ/macroprelim/
├── prelimindex.html
├── roadmapTODO.html
├── Chari/
│   ├── privatemoney.html
│   ├── productionrisk.html
│   ├── sustainabledebt.html
│   └── FriedmanRule.png
├── Concepts/
│   ├── envelope.html
│   └── flowchartkey/
│       ├── FlowChartKey.html
│       ├── FCchance.png
│       ├── FCchoice.png
│       ├── FCincome.png
│       ├── FClabel.png
│       ├── FCprocess.png
│       └── FCtime.png
├── Jones/
│   ├── HumanCapital.html
│   ├── dynamicprogramming.html
│   └── questions.txt
└── Kehoe/
    ├── Search.html
    ├── dp.html                 (duplicate of Search.html)
    ├── crossingProof.html
    ├── KehoeSearchLabels.png
    ├── laser1.png
    ├── laser2.png
    └── laser3.png
```

## Arrow / Root (mechanism design)

`_detritus/research/arrowroot/arrowrootnotes.html`
: Detailed study notes on Root's constrained allocation paper. Covers strategy-proofness, group strategy-proofness, nonbossiness, Maskin monotonicity, local dictatorship, Root's proof of Gibbard–Satterthwaite, and a side-by-side comparison of GS vs Root's setup. Heavy MathJax.

`_detritus/research/arrowroot/arrownotes.html`
: Rough lecture/reading notes on Arrow's impossibility theorem — decisiveness, independence of irrelevant alternatives, ordinal vs cardinal preferences. Also contains scattered idea fragments (control theory, O-ring, farming) mixed in with the Arrow material.

`_detritus/research/arrowroot/Root - Incentive Stuff.pdf`
: The Root paper itself (976 KB PDF). Reference copy.

## Macro prelim notes (Chari)

`econ/macroprelim/Chari/privatemoney.html`
: Worked prelim problem on a cash-credit economy with private money. Defines a competitive equilibrium, derives FOCs, characterizes the steady state under constant money growth, identifies the critical inflation threshold for a nonmonetary equilibrium, and shows the Friedman Rule is optimal. Includes an image (`FriedmanRule.png`). Substantial and complete.

`econ/macroprelim/Chari/sustainabledebt.html`
: Worked prelim problem on government debt with sustainability constraints. Defines a CE with default risk, derives the implementability constraint, sets up the Ramsey problem, defines sustainable equilibrium with history-dependent strategies, characterizes the worst (autarky) and best sustainable equilibria. Substantial and complete.

`econ/macroprelim/Chari/productionrisk.html`
: Brief outline for a consumption/saving problem with production risk. Only contains a sketch of the approach and the recursive equilibrium definition — no worked solutions. Incomplete.

## Macro prelim notes (Jones)

`econ/macroprelim/Jones/HumanCapital.html`
: Two problems concatenated in one file. The first half is a neoclassical growth model with human capital (planner's problem, homogeneity of the value function), but the proof is incomplete ("add term including initial condition... badabing"). The second half is a complete McCall search problem (identical content to Kehoe's `Search.html`). Uses blue (Jones) styling.

`econ/macroprelim/Jones/dynamicprogramming.html`
: Two problems concatenated in one file. The first half covers dynamic programming in the one-sector growth model — sequential form, Bellman equation, sufficient conditions for uniqueness, FOC and envelope condition with inelastic labor. The second half is again the same McCall search problem duplicated from `HumanCapital.html` and Kehoe's files. The human capital homogeneity section is also duplicated here. Uses blue (Jones) styling.

`econ/macroprelim/Jones/questions.txt`
: One-line question about value function representation. Not useful.

## Macro prelim notes (Kehoe)

`econ/macroprelim/Kehoe/Search.html`
: McCall job search model. Setup, reservation wage characterization, comparative statics for unemployment benefits and mean-preserving spreads. This is the "canonical" version of the search content that also appears duplicated in both Jones files. Uses pink (Kehoe) styling. Substantial and complete.

`econ/macroprelim/Kehoe/dp.html`
: Identical content to `Search.html` — the same McCall search problem with the same comparative statics. Appears to be an accidental duplicate. Uses pink styling but without the background color override.

`econ/macroprelim/Kehoe/crossingProof.html`
: A standalone proof that if one increasing function dominates another, their crossing points are ordered. Illustrated with a "laser beam" analogy and three diagrams (`laser1.png`, `laser2.png`, `laser3.png`). Used as a supporting lemma for the mean-preserving-spread comparative static. Uses pink styling.

`econ/macroprelim/Kehoe/KehoeSearchLabels.png`
: Flowchart diagram for the McCall search model. Referenced by both Kehoe and Jones files.

## Macro prelim notes (Concepts)

`econ/macroprelim/Concepts/envelope.html`
: Explanation of the envelope condition in dynamic programming. Starts with a Bellman equation example, gives a multivariate chain rule refresher, then derives the envelope condition showing why the indirect effect vanishes at the optimum. Ends with a flower emoji note. Uses default styling. Substantial.

`econ/macroprelim/Concepts/flowchartkey/FlowChartKey.html`
: Legend for the custom flowchart notation used in the search problem notes. Defines period boundary, income, choice, chance, process, and present-value-label nodes with images. Includes a digression on the state-machine interpretation. References six PNG icons (`FCtime.png`, `FCincome.png`, `FCchoice.png`, `FCchance.png`, `FCprocess.png`, `FClabel.png`).

## Macro prelim index and scaffolding

`econ/macroprelim/prelimindex.html`
: Hub page linking to the Chari notes. Most entries are plain text without links (Kehoe and Jones sections are stubs). Contains commented-out homework links and personal reminders. Could be replaced by a proper Jekyll nav parent.

`econ/macroprelim/roadmapTODO.html`
: Scratch file experimenting with nested HTML layouts for a concept roadmap. Contains a topic outline (constrained optimization, competitive equilibrium, Pareto efficiency, search, Bellman equations) but no actual content — just test formatting and brainstorming. Not useful as a standalone page.

```
econ/tradeprelim/
├── prelimindex.html
├── amador/
│   ├── multipleborrowers.html
│   └── EatonG notes.lyx
├── fitzgerald/
│   ├── armingtongravity.html
│   ├── melitzottaviano.html        (problem only; duplicate below)
│   ├── melitzottaviano_problem.html (duplicate of above)
│   ├── melitzottaviano_solution.html
│   ├── mellitz work.lyx
│   └── melitzottaviano/
│       └── melitzottaviano.html    (another duplicate)
└── kehoe/
    ├── hecksherohlin.html
    ├── hecksherwork.lyx
    ├── debtcrisiswork.lyx          (empty)
    ├── learningbydoing.html        (stub)
    ├── monopolisticcompetition.html
    ├── self-fulfillingdebt.html
    └── LBD/
        ├── LBDconcepts.html        (empty)
        ├── LBDprelim.html
        └── LBDprelimSolutionA.html
```

## Trade prelim notes (Amador)

`econ/tradeprelim/amador/multipleborrowers.html`
: Worked prelim problem on a dynamic two-country Heckscher–Ohlin model with capital accumulation and factor reallocation across sectors. Includes setup, equilibrium definition, social planner's problem, international equilibrium, and theorems. Substantial and complete.

`econ/tradeprelim/amador/EatonG notes.lyx`
: Brief LyX notes on Eaton and Gersovitz (1981) on sovereign borrowing and default, referencing the Bulow–Rogoff argument about asset market access. Stub.

## Trade prelim notes (Fitzgerald)

`econ/tradeprelim/fitzgerald/armingtongravity.html`
: Complete worked problem deriving the gravity equation from an Armington model with differentiated products. Covers resource constraints, cross-country prices, consumer optimization, price indices, and data applications.

`econ/tradeprelim/fitzgerald/melitzottaviano.html`
: Problem statement for a symmetric Melitz–Ottaviano model with monopolistic competition and endogenous firm entry/exit. Eleven parts (a–k) covering consumer preferences, firm pricing, free entry, trade effects, and CES comparison. Problem only, no solutions.

`econ/tradeprelim/fitzgerald/melitzottaviano_problem.html`
: Duplicate of `melitzottaviano.html`.

`econ/tradeprelim/fitzgerald/melitzottaviano/melitzottaviano.html`
: Another duplicate of `melitzottaviano.html` in a subdirectory.

`econ/tradeprelim/fitzgerald/melitzottaviano_solution.html`
: Full solutions to the Melitz–Ottaviano problem with detailed derivations of equilibrium conditions and trade effects. Covers all eleven parts, though some welfare and intuition sections have TODO notes. Substantial.

`econ/tradeprelim/fitzgerald/mellitz work.lyx`
: LyX working notes and derivations for the Melitz–Ottaviano model — price setting, firm profits, free entry conditions, effects of opening to trade, and CES utility comparisons. Scratchwork.

## Trade prelim notes (Kehoe)

`econ/tradeprelim/kehoe/hecksherohlin.html`
: Complete worked problem on a two-sector dynamic Heckscher–Ohlin model with capital accumulation and international trade. Multi-part with setup, equilibrium definitions, social planner problem, and theorems.

`econ/tradeprelim/kehoe/hecksherwork.lyx`
: LyX working notes with derivations for the dynamic Heckscher–Ohlin model — production equations, factor constraints, optimization. Scratchwork.

`econ/tradeprelim/kehoe/debtcrisiswork.lyx`
: Empty placeholder. No content.

`econ/tradeprelim/kehoe/monopolisticcompetition.html`
: Complete worked problem on international trade with monopolistic competition and heterogeneous firms. Covers pricing rules, equilibrium definition, productivity thresholds, trade equilibrium, and symmetric equilibria.

`econ/tradeprelim/kehoe/self-fulfillingdebt.html`
: Worked problem on sovereign debt with sunspot-driven self-fulfilling crises. Covers recursive equilibrium definition, debt thresholds, debt rundown, crisis conditions, equilibrium construction, and an application to the 1994 Mexican crisis. Substantial and complete.

`econ/tradeprelim/kehoe/learningbydoing.html`
: Stub for a Ricardian trade model with learning-by-doing. Title and setup only, no solutions.

`econ/tradeprelim/kehoe/LBD/LBDconcepts.html`
: Empty placeholder for learning-by-doing concepts.

`econ/tradeprelim/kehoe/LBD/LBDprelim.html`
: Problem statement for a two-country Ricardian model with learning-by-doing and multiple equilibrium configurations. Five parts (a–e). Problem only, no solutions.

`econ/tradeprelim/kehoe/LBD/LBDprelimSolutionA.html`
: Full solution to the LBD prelim problem with five equilibrium cases, dynamics analysis, and discussion of technology gap effects. Substantial and complete.

## Trade prelim index

`econ/tradeprelim/prelimindex.html`
: Navigation hub linking to all trade prelim problem sets by professor. Could be replaced by a proper Jekyll nav parent.
