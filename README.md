# molearn

*molecular conformational spaces meet machine learning*

This software trains a generative neural network on an ensemble of molecular conformations (typically obtained by molecular dynamics).
The trained model can be used to generate new, plausible conformations repesentative of poorly sampled transition states.

Included in this repository are the following:
* Torch functions for calculating the energy of a protein conformation
  * Documentation for this is in the `doc` folder.
  * Source code is in the `molearn` folder
* `example_script.py` detailing:
  * An example of how to prepare and use the above code
  * A convolutional autoencoder
  * Loading and saving *.pdb* files with biobox
* An example *.pdb* file in the **test** folder
* The [Amber parameters](https://ambermd.org/AmberModels.php) released in the [AmberTools20 package](https://ambermd.org/AmberTools.php) published under a GNU General Public Licence. These are loaded in by the Torch potential to calculate the energy of a protein conformation.

## Requirements ##

Molearn requires Python 3.x and the following packages (and their associated packages):
* numpy
* PyTorch (1.7+)
* [Biobox](https://github.com/Degiacomi-Lab/biobox)

## Installation ##

molearn requires no installation. Simply clone the repository and make sure the requirements above are met.
molearn can also be obtained through Anaconda: `conda install molearn -c conda-forge`

## Usage ##
* The example script `example_script.py` and the documentation in the `doc` folder
* Jupyter notebook tutorials are available [here](https://github.com/Degiacomi-Lab/molearn_notebook).

## Reference ##

If you use molearn in your work, please cite:
[V.K. Ramaswamy, S.C. Musson, C.G. Willcocks, M.T. Degiacomi (2021). Learning protein conformational space with convolutions and latent interpolations, Physical Review X 11](
https://journals.aps.org/prx/abstract/10.1103/PhysRevX.11.011052)

## Contact ##

If you have any issues or questions please contact samuel.musson@durham.ac.uk
