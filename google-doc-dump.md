# Simulation software validation / physical validation
_copied from the original Google [doc](https://docs.google.com/document/d/17PEGrGyaxYv5KIPS3Y71uXt-o5uZvVIb6M2EtG-JY-s)_

## Summary / Presentation Aug 25 Best-Practice workshop

**Probably 2 documents:**

1. Developer best practices

2. User best practices

### Developer best practices (for simulation software validation / physical validation):

#### Out-of-scope

* Software engineering best practices
    * version control
    * continuous integration
    * unit/system/regression tests (**in scope:** how / what to test)

#### Scope

* Hierarchical test protocol (unit tests / system tests)

#### Scope to be determined

* Scope of proposed tests:
    * List of components to be checked
    * Concrete tests
    * Database of tests (input files, expected output)
	
* Include non-equilibrium simulations?

* Non-dynamics methods (MC, ...)

#### Possible overlaps

* Simulation code comparison

#### Possible collaborations

* Developers of diverse software packages

* "Non-equilibrium experts"

#### Outline draft, (hierarchical) test protocol:

* Particle Properties
    * Forces
    * Torques

* Neighborhood Properties
    * Neighbor list

* System Properties
    * Integrator
    * Periodicity, simulation box
    * Random number generation
    * Temperature / pressure control
    * Fluctuations
    * Electrostatics
    * Energy conversion
    * Drift
    * Error accumulation

### User best practices (for simulation software validation / physical validation):

#### Scope:

* Steps / methods to analyze whether your simulation fulfills basic
  physical validity - ensemble checking, equipartition, ...

#### Scope to be determined

* Include non-equilibrium simulations?

* Non-dynamics methods (MC, …)

#### Possible overlaps

* Sampling / uncertainty

* Various analysis best practices

* Various simulation setup documents

* Developer best practice (for simulation software validation /
  physical validation)

#### Possible collaborations

* "Non-equilibrium experts"

## Notes from presentation discussion

Rectangular results grid of molecular systems (e.g., water,
chloroform, ...) vs. properties (energy, diffusion constant, etc.)
results.  These actual numerical results should be hosted by MolSSI
servers, but this document might specify a minimal set of cases.
These will range from energies and forces for two LJ particles in a
box, to whole boxes of liquids.  Physical properties list should
include many thermodynamic quantities U(t) and < U >, for over a short
simulation, for example.

During presentation discussion it was pointed out that this document
should be called "Verification" rather than "Validation".  Within NIST
the term "validation" means comparison between the simulation results
and experiment.  Validation means checking an experimental or
simulation method against the correct answer.  Verification means
checking that the method has been properly implemented and this is
more the kind of checks we are concerned with here.

* Consistent constants; pull units from modules with historical
  values.
* Unit handling

* **verification** vs validation

* Tests that code needs to pass vs given software to test
    * Give inputs/outputs for user to test
    * Input/output hosted by MolSSI
    * Verification of some common sim packages
    * Tests at all levels
        * Discover where in the hierarchy the test fails
* reference library for more intensive tests (diffusion, etc)


Things that a user should check after a simulation to see if it is valid:

1. is temperature consistent across the various components of the
   material
2. Has the energy been conserved?; has there been heating during the
   course of the simulation.  If so, maybe the neighbor list has not
   been updated frequently enough.
3. In NpT simualtions look at the volume vs. time and check of
   systematic drift of discontinuities.
4. Look for discontinuities or drifts in all observables, suggesting
   you are not at equilibrium
5. For production phase, try to identify (eyeball) the correlation
   time for the slowest observable.
6. Visually check frames with a graphical user interface to make sure
   the material is distributed like you expect - a visual inspection
   can quickly identify if material is aggregating or phase
   separating, bubbles forming, or if there are regions of unusual
   structure, suggesting a problem or the onset of interesting
   physics...
7. ...

## Earlier notes

By Friday July 28th:

* Brainstorm the resources and information needed to generate a best
  practices document for the subject.  Specifically:
    * Identify a point person in each group that you can trust to make
      sure the tasks above are accomplished and indicate this person
      to us.
        * I feel like Pascal would be an excellent choice for this,
          but it might not really be necessary. We seem to be all
          pretty involved in this project which should make this moot.
    * Identify 1-4 additional people who really should be involved to
      make the best practices document. Decide whether to invite them
      at this point or to wait until after the conference.
        * John Chodera would be an excellent resource,
          his [group](https://github.com/choderalab) has excellent
          best practices documents and would be very valuable to have
          involved in this project
    * Identify the papers in the field that the best practices will be
      drawn from.
    * Identify if there are new results that need to be generated to
      nail down certain best practice issues.

* Generate an initial list of best practices
    * Identify all the main points that need to be considered when
      performing the simulations/calculations identified below
        * Doesn’t yet need to be more than 2-4 pages
        * Keep code agnostic for now.
    * Assume, for now, general understanding of molecular simulation
      knowledge.
        * If prerequisite knowledge is expected, pass it to the group
          working on basic simulation training
    * Decide if the topic really should be split into more than one
      document (and decide on which of those documents to focus on).

 

Between July 28th and August 24th, 9:00 a.m. (start of workshop)

* Turn the initial outline into an expanded form with consistent
  shared organization. We will provide an example before July
  20th. For example, we will clarify about what background information
  to include, and what required sections there will be, etc.
* Decide on someone (could be joint) to represent the group present a
  10 min overview for discussion at the workshop.

** This is also a special category. There’s a couple of different
directions for this to go; a focus on checks that each code could run,
which is sort of what I was thinking, but I want to give people a
little freedom, since there was so much interest.  We don’t want a
focus on coding techniques - that’s a useful area, but I think we want
to focus on the usage of and testing of code at this stage.  Another
potential area is comparison between programs; but I think this needs
to be tackled in something a little bigger than just a best practices
document, it might, however, be reasonable to develop a number of test
cases that can be used.

### Papers

* [http://aip.scitation.org/doi/abs/10.1063/1.476021](http://aip.scitation.org/doi/abs/10.1063/1.476021) "Validation
  of molecular dynamics simulation" (1998) - describes five places
  where physical accuracy are lost:
    * physical system/conceptual model interface
    * conceptual model/mathematical or software-implemented model interface
    * statistical sampling and convergence
    * software quality
    * user/software interface

* [http://arxiv.org/abs/1308.5587](http://arxiv.org/abs/1308.5587)
  "The development and expansion of HOOMD-blue through six years of
  GPU proliferation" (2013) - describes methodology and some results
  for LJ systems concerning energy and momentum conservation on
  single/double precision computations, using CPU and GPU

* Zhu, H., Hall, P. A., & May, J. H. (1997). Software unit test
  coverage and adequacy. Acm computing surveys (csur), 29(4), 366-427.
    * [Link here to paper](http://dl.acm.org/citation.cfm?id=267590) 
    * A pretty great paper on software validation, although quite deep
      in the computer science realm. But valuable nonetheless.

* Elbaum, S., Rothermel, G., & Penix, J. (2014, November). Techniques
  for improving regression testing in continuous integration
  development environments. In Proceedings of the 22nd ACM SIGSOFT
  International Symposium on Foundations of Software Engineering
  (pp. 235-245). ACM.
    * [http://cse.unl.edu/~elbaum/pre-prints/fse2014-prePrint.pdf](http://cse.unl.edu/~elbaum/pre-prints/fse2014-prePrint.pdf)
    * Continuous Integration paper, still pretty CS heavy, but the
      info is good

* The Lennard-Jones equation of state revisited (J. Karl Johnson ,
  John A. Zollweg & Keith E. Gubbins, 1993):
  ([http://dx.doi.org/10.1080/00268979300100411](http://dx.doi.org/10.1080/00268979300100411))
    * This paper provides bench mark equation of state data for LJ
      systems

* Structure and Dynamics of the TIP3P, SPC, and SPC/E Water Models at
  298 K (Pekka Mark and Lennart Nilsson, 2001)
    *  This paper provides benchmark data for SPC/ SPC/e, TIP3p water
       model RDF and diffusion coefficients generated via MD using the
       CHARMM package

* Validation of Molecular Simulation: An Overview of Issues (Wilfred
  F. van Gunsteren, Xavier Daura, Niels Hansen, Alan Mark, Chris
  Oostenbrink, Sereina Riniker, Lorna Smith,
  2017)
  [http://onlinelibrary.wiley.com/doi/10.1002/ange.201702945/abstract](http://onlinelibrary.wiley.com/doi/10.1002/ange.201702945/abstract)

* Simple Quantitative Tests to Validate Sampling from Thermodynamic
  Ensembles (Michael Shirts,
  2012)
  [http://dx.doi.org/10.1021/ct300688p](http://dx.doi.org/10.1021/ct300688p) [https://github.com/shirtsgroup/checkensemble](https://github.com/shirtsgroup/checkensemble)

* Round Robin Study: Molecular Simulation of Thermodynamic Properties
  from Models with Internal Degrees of Freedom
  (2017)
  [http://pubs.acs.org/doi/10.1021/acs.jctc.7b00489](http://pubs.acs.org/doi/10.1021/acs.jctc.7b00489)
    * This paper just came out and cross compares computations of the
      same properties across a variety of codes; I haven’t reviewed in
      detail yet but I think it gets at precisely what this is about.

### People to invite

* I think it would be great to get people involved with the development of AMBER, Gromacs, LAMMPS, OPENMM involved. People such as Steve Plimpton, Ross Walker, etc come to mind.
    * Pascal has some contacts, people can be brought in to revise / critique a first draft
* John Chodera
* Jean-Philip Piquemal
* Maybe somebody to help us on non-equilibrium simulations?

### Best practices

* Software validation
    * Unit testing / other validation methods, agnostic means to
      ensure that the modifications to the code still returns sensible
      values
    * Does the package, once compiled and installed, pass the tests on
      the target system?
    * If the package is hardware-accelerated, do you get the same
      results when running with and without hardware acceleration?
    * Neighbor list build check: does the code generate statistically
      equivalent results using a neighbor list in the nonbonded force
      routine as a o(n2) force calculation. This could also be
      extended to check various parts of the neighbor list build. For
      instance, does the linked-list binning + neighbor list build
      yield equivalent results as an o(n2) neighbor list build.

* Physical validation
    * Make sure the timestep size is set correctly: check that energy
      and momentum are conserved in NVE integration for reasonable
      thermalized configurations using your set of forces, for example
    * Check that simple system-specific derived quantities are
      reasonable, like diffusivities, radius of gyration, etc
    * Lennard Jones particles have very nicely calculated equation of
      state data (The Lennard-Jones Equation of State Revisited,
      1993). Validating that the code accurately reproduces this data
      would ensure the validity of the force, integrator, and neighbor
      list build functions.
    * The RDFs of various water models have been very well
      studied. The reproduction of the SPC/E and tip3p RDFs would be a
      nice test. I hesitate to put tip4p and the six-site water model
      here, as these models require additional numerical routines to
      handle the fictitious sites that need not be present in a
      standard MD package
    * [https://github.com/choderalab/software-development](https://github.com/choderalab/software-development)
        * This is a great reference to at least a beginning step for
          best practices for software dev in computational chemistry
    * When reporting equilibrium quantities, check that system is
      equilibrated (refer to other working group on "Ensemble averages
      and uncertainty analysis")
    * Can compare to reference databases of physical quantities, like
      the [CCCBDB](http://cccbdb.nist.gov/alldata2x.asp) at NIST
    * Work in progress at CU Boulder: Physical validation suite
      ([https://shirtsgroup.github.io/physical-validation/](https://shirtsgroup.github.io/physical-validation/))
      allowing to test ensembles & integrator validity. We’re trying
      to suggest a two-fold approach: Testing of the code-validity
      (set of test systems, ran by developers), and testing of
      simulation results (ran by end users using their specific
      systems).

* Validate a set of quantities against each other (unit tests vs known
  values, regression tests vs past versions, comparison vs other
  codes)
    * forces, torques, potentials
    * Pairs of particles
    * boxes of particles
        * comparing potential terms against box of water, for example
    * integrator
        * make sure temperature/pressure control is going to correct
          value
        * make sure conserved quantities are being conserved
        * check scaling of energy variance WRT timestep size (can
          cross-compare drift and energy variance scaling to hoomd
          values at
          [https://arxiv.org/abs/1308.5587](https://arxiv.org/abs/1308.5587) )
    * polarizable vs non-polarizable
    * constrained vs non-constrained
    * neighbor list
    * system properties, thermodynamic observables
    * RNG
    * different phases/interfaces

* Hierarchy of quantities to check
    * particle-local: forces, torques
    * neighborhood-local: neighbor list
    * system (global): long-range electrostatics, periodic boundary
      conditions, integrator, energy/momentum drift

### Out of scope

* Software engineering best practices
    * version control
    * unit/regression/integration tests (**in scope:** mentioning
      which sorts of unit tests people may use for our sorts of
      systems)
    * continuous integration

### TBD/Later

* User-specific guidelines

* equilibrium vs nonequilibrium

* dynamics (MD, ...) vs sampling (MC, ...) algorithms

* size of systems, timesteps, parameters...

## Notes from group discussion Aug 24

### Goal of this Document at the Moment (24, Aug 2017)

* Provide a new user to molecular dynamics a general, basic document
  to verify the validity of the very cornerstone pieces of all
  molecular dynamics simulations.

* This list is not exhaustive, but merely a succinct set of tests and
  sanity checks to ensure that their simulation should proceed with a
  modicum of confidence successfully

* Begin by outlining the hierarchy of the testable and validateable
  basics of a molecular dynamics simulation.
    * Particle-Local
	    * Forces
		* Torques
    * Neighborhood-local	
		* Neighbor lists
    * System-local		
		* E-statics
		* PBC/Box Conditions
		* Integrator
		* Energy Conversion, drift, error accumulation

### Scope Definition

* Molecular dynamics only at the moment

* Basic information about molecular dynamics already covered by other
  best practice document

* Groundwork for basic sanity checks / validation to improve
  confidence that simulation is proceeding correctly

* Build up hierarchy of values/properties to check in simulation from
  the very basic particle properties to the system level properties
    * Particle Properties
        * Forces
        * Torques
    * Neighborhood Properties
        * Neighbor list
    * System Properties
        * Electrostatics
        * Periodic boundary conditions, simulation box
        * Integrator
        * Energy conversion
        * Drift

* Error accumulation
