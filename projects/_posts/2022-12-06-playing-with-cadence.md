---
layout: projects
title: Mini Cadence Projects
tag: Electronics
description: A couple of small digital electronics projects from MTE421.
tools: Cadence Virtuoso
img: /Media/projects/mte421/parametric-nor4.png
hidden: true
---
In my 4A term at UW, I took MTE421: Linear and Nonlinear Electronics, which mainly focused on digital ASIC design principles. In the course, we learned how to design and evaluate logic circuits from the transistor level and use the Cadence suite of tools.

# Mini Project 1: Simple Combinational Logic Optimization
The goal here was to familiarize ourselves with the tools by designing and optimizing an OR8 circuit with a given load and assumed electron mobility ratio (P vs N), then simulating using real transistor parameters.

I'm not sure what possessed me at 1am, but I wrote a program to generate a ton of possible tree-shaped circuits given a target function but didn't end up using it for much. With that said, here are a few topologies I applied path effort optimization on to choose a good starting circuit:
<img src="/Media/projects/mte421/mini-project1-appendixb.png">
*Tabulation of path effort optimization calculations*

Based on these first-order calculations, it seemed that `NAND2(NOR4(X1,X2,X3,X4),NOR4(X5,X6,X7,X8))` would have minimal delay. As such, parametric (variable transistor params) schematics, symbols, and testbenches were made in Cadence for the NAND2 and NOR4 individually:
<img src="/Media/projects/mte421/parametric-nand2.png">
<img src="/Media/projects/mte421/parametric-nor4.png">
*Parametric logic gate schematics in Cadence Virtuoso (ignore ugly labels - required for project submission)*

Of course, a top-level schematic and testbench were made to piece these together and simulate with different transistor sizes:
<img src="/Media/projects/mte421/OR8.png">
*Top-level OR8*

From there, Cadence's ADE XL was used for transient simulation of the circuit by providing each of the 8 inputs a voltage stimulus. This was captured for 5 different transistor ratios applied to the parametric gates to see which would result in the most responsive rise/fall times.

# Mini Project 2: Dynamic (Domino) Logic
The second project had a similar goal but this time employing dynamic logic - specifically Domino logic.

<video autoplay loop muted playsinline>
 <source src="/Media/projects/mte421/virtuoso_dyn_or8.mp4" type="video/mp4">
</video>
*My domino-logic OR8 schematic speedrun in Cadence Virtuoso*

This was my design strategy: develop several logic topologies > evaluate by hand via path effort calculations > implement the best topology in Cadence (w/ parametric transistor sizes) > Simulate w/ different transistor ratios. 

Here's one transient simulation for rising inputs where NMOS widths were varied:
<img src="/Media/projects/mte421/dynOR8_rising_sim.png">

And here's the result of an experiment comparing NMOS width to rise/fall times for a fixed PMOS:
<img src="/Media/projects/mte421/dynOR8_delay_optim.png">
