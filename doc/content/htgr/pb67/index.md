# Conjugate heat transfer simulation of a 67-pebble core

*Contact: John Acierno (Penn State), Dillon Shaver (dshaver.at.anl.gov), and April Novak (anovak.at.anl.gov)* 

In this tutorial we are going to set up and simulate a simple [!ac](CHT) case using a helium (Pr=0.71) cooled 67-pebble bed.
This tutorial was developed from an example case provided with NekRS and couples to MOOSE's [!ac](CHT) module using CARDINAL as a wrapper. 
More information about the NEAMS tool CARDINAL can be found on [github](https://github.com/neams-th-coe/cardinal), or on the [Cardinal website](https://cardinal.cels.anl.gov/).
In each time step MOOSE will solve the energy equation in the the solid subdomain and pass the solution to NekRS, which will in-turn solve both the Navier-Stokes and energy equations in the fluid subdomain.
NekRS will then pass its temperature solve back to MOOSE in the next time step. 
This transfer of information occurs at the boundary between solid and fluid subdomains, which are the pebble surfaces in this case.

!include CardinalandMOOSE.md

# Geometry and computational model

The geometry for this case consists of 67 pebbles in a randomly packed cylindrical bed.
The pebbles have a diameter of 1 (dimensionless) and the cylinder has a diameter of 4.4 (dimensionless).
The pebble bed begins around 2.5 pebble diameters upstream from the cylinder inlet and has a total heigh of about 5 pebble diameters.
A cross section of the fluid domain is shown in [pb67geom] where the fluid is the gray region and the pebbles are the white regions.

!media pb67/fluid_slice.png
       style=width:40%;margin-left:auto;margin-right:auto
       id=pb67geom
       caption=A cross section of the fluid domain for the 67 pebble geometry.

## NekRS

!include nekrs_dimless.md

!include nekrs_LES.md

## Heat Conduction Model

!include steady_hc.md

# Case Setup



## NekRS setup

### oudf file

### udf file

### par file

### usr file

## MOOSE setup

# Results

!media pb67/pb67_3D_renderings.png
  style=width:70%;margin-left:auto;margin-right:auto
  id=pb673D
  caption=3D volumetric renderings done in VisIt of the velocity (left) and the temperature (right) fields. 



!alert note
One should put a copy of the figure at the specific file path.
The VTB media is now arranged by reactor types under the folder +/media+. 
For more detailed instructions on figure formatting, please refer to
the [MooseDocs media tutorial](https://mooseframework.inl.gov/python/MooseDocs/extensions/media.html). 


!devel! example id=example-table caption=Example of adding a table in VTB documentation.
!table id=fuel_salt_properties caption=Thermophysical properties of the fuel salt.
|   |   | Unit  | LiF-BeF$_4$-ZrF$_4$-UF$_4$  |
| :- | :- | :- | :- |
| Melting temperature | $T_{melt}$ | $K$ | $722.15$  |
| Density | $\rho$ | $kg/m^3$  | $2553.3-0.562\bullet T$ |
| Dynamic viscosity | $\mu$ | $Pa\bullet s$ | $8.4\times 10^{-5} exp(4340/T)$ |
| Thermal conductivity | $k$ | $W/(m\bullet K)$ | $1.0$ |
| Specific heat capacity | $c_p$ | $J/(kg\bullet K)$ | $2009.66$ |
!devel-end!

!alert note
For more detailed instructions on table formatting, please refer to
the [MooseDocs table tutorial](https://mooseframework.inl.gov/python/MooseDocs/extensions/table.html). 

NekRS solves the incompressible Navier-Stokes equations:

!alert note
For more detailed instructions on equation formatting, please refer to
the [MooseDocs equation tutorial](https://mooseframework.inl.gov/python/MooseDocs/extensions/katex.html).


### Adding references style=font-size:125%

If the model has been previously published, one should provide the reference to the published works together with key references used for model development. 
+MooseDocs+ supports BibTex style references, and some examples about how to cite technical report, conference proceeding and journal article are given below.  

```language=bash
@techreport{Hu2017,
        address = {Lemont, IL},
        author = {Hu, Rui},
        number = {ANL/NE-17/4},
        mendeley-tags = {ANL/NE-17/4},
        institution = {Argonne National Laboratory},
        title = {{SAM Theory Manual}},
        year = {2017}
}

```

```language=bash
@InProceedings{novak_2021c,
  title       = {{Coupled {Monte} {Carlo} and Thermal-Hydraulics Modeling of a Prismatic Gas Reactor Fuel Assembly Using {Cardinal}}},
  author     = {A.J. Novak and D. Andrs and P. Shriwise and D. Shaver and P.K. Romano and E. Merzari and P. Keutelian},
  booktitle  = {{Proceedings of Physor}},
  year       = 2021
}

```

```language=bash
@article{Fang2021,
        author = {Fang, Jun and Shaver, Dillon R. and Min, Misun and Fischer, Paul
                and Lan, Yu-Hsiang and Rahaman, Ronald and Romano, Paul
                and Benhamadouche, Sofiane and Hassan, Yassin A.
                and Kraus, Adam and Merzari, Elia},
        doi = {10.1016/j.nucengdes.2021.111143},
        journal = {Nuclear Engineering and Design},
        title = {{Feasibility of Full-Core Pin Resolved CFD Simulations of
                Small Modular Reactor with Momentum Sources}},
        volume = {378},
        year = {2021}
}

```


The bibtex entries must be added into the VTB bibliography file +vtb.bib+. 
A reference list will be generated automatically at the end of the VTB documentation page.


!devel! example id=example-refs caption=Example of inserting citations in VTB documentation.
Description part A [!citep](Hu2017), description part B [!citep](novak_2021c), description part C [!citep](Fang2021)
!devel-end!


### Other key model details to provide in the high-level summary style=font-size:125%

- Reactor Type(s): e.g., Liquid Metal Cooled Fast Reactor

- Type of simulation: e.g., 3D core multiphysics (neutronics-TH) transient, 1D system steady-state

- NEAMS MOOSE Codes Used: Griffin, Heat Conduction, Cardinal, etc. 

- NEAMS non-MOOSE Codes Used: MC2-3, Nek5000/RS, etc. 

- Non-NEAMS Codes Used: Cubit, OpenFOAM, etc.


!alert note
More information is available online about [the list of NEAMS codes](https://neams.inl.gov/code-descriptions/) and the codes that have been used for [the models available in VTB repository](https://mooseframework.inl.gov/virtual_test_bed/resources/codes_used.html). 
Providing the related information in documentation can better help the VTB team to categorize/sort the model.

## Computational Model Description

Walk through the main kernel/blocks, show snippets of example inputs when needed. 
The markdown source can be as simple as the following to show the `EOS` block from the `msre_loop.i` input file:

!devel! example id=example-list caption=Example of including input block in VTB documentation.
!listing msr/msre/msre_loop_1d.i block=EOS language=cpp
!devel-end!


## Results

Here one can document the most important results from the related simulations. Please refer to aforementioned examples about how to add figures and tables when discussing the main results and discoveries. 


## Run Command 

Please provide the run command for model execution on INL’s HPC Cluster or otherwise. Below is a simple example how to run a SAM system modeling job. 

```language=bash
mpirun -np 48 /path/to/sam-opt -i sam_input.i

```


