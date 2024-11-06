## SimGrid Programmatic Platform Description of Summit@ORNL

The [programmatic platform description](https://simgrid.org/doc/latest/Platform_cpp.html#beyond-the-xml-the-power-of-c-platforms) approach introduced in SimGrid v3.28 eases the description of larger and more complex computing and storage infrastructures compared to the former XML-based approach. It consists in describing the available computing resources (i.e., number and characteristics of compute nodes), network interconnect (i.e., topology and nominal bandwidth and latency of the network links), and available storage resources (i.e., number and types of disks and file system characteristics), and use this information to instantiate the underlying resource simulation models.

In this repository we propose a description of the [Summit](https://www.olcf.ornl.gov/olcf-resources/compute-systems/summit/) leadership-class supercomputer operated by the [Oak Ridge National Laboraty](https://www.ornl.gov) from 2018 to 2024.
The basic building block of Summit is the IBM Power System AC922 node. Each of the approximately 4,600 compute nodes on Summit contains two IBM POWER9 processors and six NVIDIA Tesla V100 accelerators. The internal organization of a node is described in the picture below:

<img src="https://docs.olcf.ornl.gov/_images/summit_node_architecture.png" alt="Internal organization of a Summit node" style="width:400px;"/>

Summit nodes are interconnected through a Non-blocking Fat Tree topology. This interconnect topology is a three-level tree implemented by a switch to connect nodes within each cabinet (first level) along with Director switches (second and third level) that connect cabinets together. Such a topology can be described in SimGrid (see [documention](https://simgrid.org/doc/latest/Platform_examples.html#fat-tree-cluster)) provided that the correct configuration parameters are used. According to this [article](https://ieeexplore.ieee.org/ielaam/5288520/9093089/8961159-aam.pdf), the paramaters of the fat tree that connects the nodes of Summit together are:
   + **Levels:** 3
   + **Down links:** (18,18,18)
   + **Up links:** (1,2,9)
   + **Link counts:** (1,2,1)

Using these parameters leads to the generation of 5,832 nodes in 324 racks (with a TOR switch each, level 1) and 18 director switches made of 36 level 2 and 18 level 3 switches.