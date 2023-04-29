---
layout: projects
title: Open Source Digital ASIC Design Tapeout
tag: Electronics
description: My first digital design being manufactured on a real chip.
tools: Verilog, Yosys
img: Media/projects/tt3/tt3-my-cell2d.png
---
View the tapeout for my parallel-to-serial converter in 3D <a href="https://andrewmourcos.github.io/tt03-verilog-demo/">here</a>

I recently heard about the Tiny Tapeout 3 program, which allows hobbyists and students to have their digital ASIC designs manufactured on a real chip. As someone who is passionate about digital electronics, I was excited to take on this challenge.

# My Design
The only problem was that I only heard about the program the morning of the submission deadline. Despite the short notice, I was determined to submit a design so I got to work.

The process was relatively straight-forward: I wrote Verilog code for a parallel to serial converter and did some basic tests in a few hours. Then, the tools did a lot of heavy-lifting: Yosys (open source synthesis tool) used the provided standard cell library to synthesize my circuit from the code:
<img src="/Media/projects/tt3/tt3-my-cell2d.png">
*2D render of my parallel to serial converter; I/O pins along left edge*

I didn't have enough time to do proper testbench tests - so it may have issues - but I managed to get a functional build at the last possible second. This was the timestamp on my last commit (designs due at 2p):
<img src="/Media/projects/tt3/tt3-final-commit-time.png">

## Stats
In the end, my design only used about 6.54% of the allocated chip area of 150 x 170 um - not too bad for a last minute submission. Here's a breakdown of the used cells:

| Category    | Cells                                                        | Count |
| ----------- | ------------------------------------------------------------ | ----- |
| Fill        | [decap](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/decap) [fill](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/fill) | 1951  |
| Tap         | [tapvpwrvgnd](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/tapvpwrvgnd) | 300   |
| Combo Logic | [o41a](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/o41a) [o31a](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/o31a) [a22o](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/a22o) [a221o](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/a221o) [and2b](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/and2b) [o211a](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/o211a) [nor2b](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/nor2b) [or3b](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/or3b) [a221oi](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/a221oi) [o21a](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/o21a) [o31ai](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/o31ai) [a21oi](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/a21oi) [a211o](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/a211o) [or4b](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/or4b) [o22a](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/o22a) [o21ai](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/o21ai) [o41ai](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/o41ai) | 47    |
| Flip Flops  | [dfxtp](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/dfxtp) | 27    |
| OR          | [or4](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/or4) [or2](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/or2) [or3](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/or3) | 22    |
| Buffer      | [clkbuf](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/clkbuf) [buf](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/buf) | 20    |
| Misc        | [conb](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/conb) | 7     |
| NAND        | [nand2](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/nand2) [nand2b](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/nand2b) | 6     |
| Inverter    | [inv](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/inv) | 6     |
| NOR         | [nor2](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/nor2) | 3     |
| Multiplexer | [mux2](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/mux2) [mux4](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/mux4) | 2     |
| Diode       | [diode](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/diode) | 1     |
| AND         | [and2](https://antmicro-skywater-pdk-docs.readthedocs.io/en/test-submodules-in-rtd/contents/libraries/sky130_fd_sc_ls/cells/and2) | 1     |

# Summary
Thankfully, I made the cutoff and made it onto the final chip tapeout that has been sent off for production with Efabless. The final chip render is shown below:

<img src="/Media/projects/tt3/tinytapeout_numbered.png">
*249 designs combined on one die in a scanchain - my section is #25!*

Despite the short notice, the Tiny Tapeout 3 program was a great experience, and I'm grateful for the opportunity to have my first digital ASIC design manufactured on a real chip. I'm looking forward to getting the breakout board back and running some tests!