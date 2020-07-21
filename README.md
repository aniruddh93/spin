# Synchronized Progress in Interconnection Networks (SPIN)
This repsository contains the code for Synchronized Progress in Interconnection Networks (SPIN)
[paper](https://ieeexplore.ieee.org/abstract/document/8416866). This paper was presented at *45th
Annual International Conference on Computer Architecture (ISCA)* and was subsequently selected for
[IEEE Micro Top Picks in Computer Architecture from Conferences in 2018](https://ieeexplore.ieee.org/document/8709946).

The architectural and micro-architectural details of SPIN are implemented in
[garnet2.0](https://www.gem5.org/documentation/general_docs/ruby/garnet-2/) (part of
[gem5](https://www.gem5.org) simulator).

Code is organized as follows:

**garnet_spin:** Contains the implementation of SPIN (in C++), FAvORS (**F**ully
**A**dapti**v**e **O**ne-VC
**R**outing with **S**pin routing algorithm and baseline routing algorithms (UGAL, Minimal, Escape-VC
and West-first).

**topologies:** Contains implementation (in Python) of *dragonfly* and *3-D flattened butterfly*
topologies.

**config:** Defines configuration options specific to SPIN.

To run full-system simulation, code in this repro will have to be integrated with rest of the gem5 code.

Sample run cmd with options (will need other gem5 components along with code in this repo):


       gem5/build/Garnet_standalone/gem5.opt gem5/configs/example/garnet_synth_traffic.py
       --network=garnet2.0
       --num-cpus=<num of cpus in topology>
       --num-dirs=<num of memory controllers>
       --topology=<network topology : mesh, dragonfly, fbfly3d, etc.>
       --dfly-group-size=<group size of dragon-fly topology>
       --sim-cycles=<simulation cycles>
       --injectionrate=<packet injection rate>
       --synthetic=<traffic pattern : uniform-random, transpose, etc.>
       --enable-spin-scheme=<1 to enable spin, 0 to disable>
       --dd-thresh=<deadlock detection threshold>
       --routing-algorithm=<routing algorithm : UGAL, minimal, XY, etc.>
       --max-turn-capacity=<no. of turns after which SPIN probe is dropped>
       --enable-variable-dd=<1 to enable variable deadlock detection threshold>
       --vcs-per-vnet=<virtual channels per virtual network>
       --enable-dfly-dlock-avoidance=<1 to enable dragon-fly deadlock avoidance using VC switching>
       