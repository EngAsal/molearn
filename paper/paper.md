---
title: 'Molearn: a Python package streamlining the design of generative models of biomolecular dynamics'
tags:
  - Python
  - machine learning
  - molecular dynamics
  - proteins
  
authors:
  - name: Samuel C. Musson
    orcid: 0000-0002-2189-554X
    equal-contrib: false
    affiliation: 1
  - name: Matteo T. Degiacomi
    orcid: 0000-0003-4672-471X
    equal-contrib: false
    corresponding: true
    affiliation: 1
affiliations:
 - name: Department of Physics, Durham University, United Kingdom
   index: 1
date: 09 May 2023
bibliography: paper.bib

---

# Summary

We present `molearn`, a Python package streamlining the implementation of machine learning models dedicated to the generation of protein conformations from example data obtained via experiment or molecular simulation.


# Statement of need

Most biological mechanisms directly involve proteins. The specific task each of these biopolymers carries out is linked to their three-dimensional shape, enabling them to bind to designated binding partners such as small molecules, ions, or other biopolymers. Crucially though, biomolecules are flexible and so are continuously jostling and reconfiguring due to Brownian motion. Thus, their function emerges from characteristic conformational dynamics. Characterising the structure and dynamics of biomolecules at the atomic level provides us with a fundamental understanding of the mechanisms underpinning life and is the first step in numerous technological applications. Progress in these areas has been spearheaded by the development of a diverse palette of dedicated experimental techniques [@dobson2019]. Unfortunately, none is singlehandedly capable of routinely reporting on the full fine structure of biomolecular conformational spaces. As such, our understanding of life at the molecular level is inherently biased by the techniques we adopt to observe it [@Marsh2015]. Molecular dynamics (MD) simulations yield atomistic insights into the conformational landscape of biomolecules, complementing and extending data gathered experimentally. MD simulations estimate the true conformational landscape of biomolecules by iteratively generating new conformers based on an initial, known atomic arrangement and physical models of atomic interactions. While MD enables obtaining key insight into biomolecular function, it is not a silver bullet: exhaustive sampling of processes such as folding or ligand binding usually lay beyond what can be routinely observed.

Generative Neural Networks have been shown to be effective predictors of a protein's 3D structure from its sequence [@Jumper2021; @Baek2021]. Several efforts have also demonstrated that a neural network trained with MD conformers can learn a meaningful dimensionality reduction of the data, usable for reaction coordinate definition [@frassek2021extended; @chen2018collective], or driving conformational space sampling [@noe2019boltzmann; @sidky2020molecular; @mehdi2022accelerating]. In this context, we have previously presented generative neural networks capable of producing protein conformations based on small pools of examples produced by MD [@Degiacomi2019; @Ramaswamy2021]. The issue is that developing a Machine Learning model to study biomolecular dynamics is a lengthy process. This requires setting up means of transforming conformational space data into tensor data submittable to a model, as well as assessing a model's quality (e.g., in terms of their energy or according to structural descriptors).

Here we present `molearn`, a Python framework facilitating the implementation of generative neural networks learning protein conformational spaces from examples obtained via experiments or MD simulations.


# Package Description

 Classes available provide support for the following tasks:
 
*	*Data loading*. `molearn` provides methods to parse molecular conformers using biobox [@rudden2022biobox], and convert them into a PyTorch [@paszke2019pytorch] tensor format suitable for training.
*	*Model design*. `molearn` comes with a range of pre-implemented models, ready to be trained on any desired datasets or subclassed to create custom models.
*	*Loss function definition*. While the classical loss function in a generative model typically builds upon a mean square error between input and output, here we provide the capability of directly interacting with the OpenMM molecular dynamics engine [@eastman2017openmm]. Specifically, we have implemented means of transferring PyTorch Tensor data directly into OpenMM's backend on GPU (without data transfer via the CPU). This enables quickly evaluating the energy of a generated model according to any force field accepted by OpenMM. This also enables directly running MD simulations with generated conformers while the model trains.
*	*Model analysis*. Once a model is trained, it is important to gather metrics defining the quality of the protein structures it can generate. We provide tools to quickly quantify structure quality in terms of root mean square deviation between the coordinates of atoms in input and output, DOPE score [@shen2006statistical], Ramachandran plot, and user-defined functions. Analysis data is returned in the form of numpy arrays [@harris2020array], for ease of manipulation and plotting. We also provide a graphical user interface (GUI), enabling the visualisation of neural network latent space, and generation of interpolations between states visualised in an interactive 3D panel by a combination of MDAnalysis [@michaud2011mdanalysis] and NGLview [@nguyen2018nglview].

![`molearn` analysis tools include a graphical user interface, enabling the on-demand generation of protein conformations. The panel on the left controls how the neural network latent space is presented, the central panel is a Plotly interactive graph displaying the latent space, and the panel on the right is a 3D representation of an interpolation through the latent space supported by NGLview\label{fig:gui}.](gui_MurD.png)


# Usage

`molearn` comes with a series of examples, usable as-is, to train and analyse a neural network. Tutorials on neural network analysis are also available, including a GUI to directly interact with a trained neural network \autoref{fig:gui}. Results obtainable via `molearn` are exemplified in [@Ramaswamy2021]. There, we designed and trained a 1D convolutional autoencoder against protein molecular dynamics simulation data. The neural network was trained via a loss function directing the neural network to both faithfully reconstruct training data, and produce low-energy interpolations between them, whereby the internal energy of produced models is assessed according to the Amber ff14SB force field [@maier2015ff14sb].


# Acknowledgements

We thank Cameron Stewart, Ryan Zhu, and Marco Mattia for their feedback. Matteo T. Degiacomi acknowledges support from the Engineering and Physical Sciences Research Council (EP/P016499/1).


# References
