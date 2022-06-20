# da4rdm-vis

## Description
The da4rdm-vis is a python package that allows extracting correlation information in relation to the different phases of Research Development Life Cycle process. The package primarily provides the vizualization of the different correlation values for the different RDLC phases as obtained for a given Project Id and other related arguments. 


## Installation
The package uses Python as a programming language and utilizes basic python packages. Noteworthy, it uses few visualization pckages like plotly express and kaleido.

## Usage
The package has two major functionalities as listed below:
1. Extracting project information in the form of correlation response wherein a dataframe is returned consisting of the correlation values corresponding to each RDLC phase. 
To use the package for retreiving correlation values as a dataframe the function called eval_corr within the module Evaluate can be used. The function eval_corr accepts two required positional arguments namely the datapath for the event log and the Project Id. Other optional arguments included start and end date, path for the operational data json file used for building the operational and RDLC phase identifier, the evaluation feature and type to be used for calculating the similarity.

2. Creating the vizualization of the correlation response from the dataframe retreived using the eval_corr function. To get a vizualization the visualize function within the module Vizualize can be used. This function accepts a dataframe as a required parameter and provides relevant visualizazion as per the choice provided by the user. The various formats supported are jpeg, png, pdf and json. The generated files are saved onto the local repository of the program using the package.

Below is an example execution of the package usage:
![image-1.png](./image-1.png)

The result of the above execution is as shown below:
![image-2.png](./image-2.png)

Outputs of the different formats:
![My animated logo](Readmefiles/Radarchart.png)

<p align="center">
  <img src="https://git.rwth-aachen.de/da4rdm/da4rdm-vis/-/blob/da4rdm-vis-Package-TestPyPi/Packaging/Readmefiles/Radarchart.png" width="350" title="hover text">
</p>

## Project status
The project is currently in test phase.
