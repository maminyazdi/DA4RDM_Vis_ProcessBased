# da4rdm-vis

## Description
The da4rdm-vis is a python based package that allows extracting correlation data for to the different phases of Research Development Life Cycle process. The package can also be used to get vizualizations of the different correlation values for the different RDLC phases as obtained for a given Project Id and other related arguments.


## Installation
The package is built using Python as a programming language and utilizes basic python packages. Noteworthy, it uses few visualization packages like plotly express and kaleido to get the vizualizations. Please make sure the necessary packages are installed before execution. Few other packages include scipy, json etc. The test package can be installed using the pip command provided below.

pip install -i https://test.pypi.org/simple/ da4rdm-vis

## Usage and Examples
The package has two major functionalities as listed below:
1. Extracting correlation data for the project. the correlation data is returned as a dataframe consisting of the correlation values corresponding to each RDLC phase corresponding to the project. To use the package for retreiving the correlation data, the function "eval_corr" within the module Evaluate should be used. 

Function Inputs:<br />
The function **eval_corr** accepts two mandatory positional arguments namely the path for the event log and the Project Id. The project id must be provided to uniquely identify the projects.  
The optional arguments include start and end date, path for the operational data json file that will be used to build the operational list and RDLC phase identifier, the evaluation feature and type to be used for calculating the similarity. The operationa data is computed from a defalut json file if an external file path is not specified by the user. If the user wishes to provide a customized operational data file then the path must be provided at the arguments position while function invoking. Please refer to the file format as shown below.
```python
{
"Operation_List": ["Add Project", "Edit Project", "Open Resource(RCV)", "Add Resource", "Edit Resource", "Delete Resource", "Upload File",  "Upload MD", "Download File", "View MD", "Delete File", "Update File", "Update MD", "Open User Management", "View Users", "Add Member", "Change Role", "Remove User", "Open Search", "View Search Results", "PID Enquiry", "Create Application Profile",  "Admin Project Quota Change", "Owner Project Quota Change", "Owner Resource Quota Change", "Invite External User", "Archive Resource", "Unarchive Resource", "Merge Request" ],
"Planning": [
        1,        1,        0,        1,        1,        1,        0,        0,        0,
        0,        0,        0,        0,        1,        1,        1,        1,        1,
        0,        0,        0,        1,        1,        1,        1,        1,        0,
        0,        0    ],
"Production": [
        0,        0,        0,        0,        0,        0,        1,        1,        0,
        0,        0,        0,        0,        0,        0,        0,        0,        0,
        0,        0,        0,        0,        0,        0,        0,        0,        0,
        0,        1    ],
"Analysis": [
        0,        0,        0,        0,        0,        0,        0,        0,        1,
        1,        1,        1,        1,        0,        0,        0,        0,        0,
        0,        0,        0,        0,        0,        0,        0,        0,        0,
        1,        1    ],
"Archival": [
        0,        0,        0,        0,        1,        0,        0,        0,        0,
        0,        0,        0,        0,        0,        0,        0,        0,        0,
        0,        0,        0,        0,        0,        0,        0,        0,        1,
        0,        0
    ],
"Access": [
        0,        0,        1,        0,        0,        0,        0,        0,        1,
        1,        0,        0,        0,        1,        1,        1,        0,        0,
        1,        1,        0,        0,        0,        0,        0,        1,        0,
        0,        0    ],
"Reuse": [
        0,        0,        0,        0,        0,        0,        0,        0,        0,
        0,        0,        0,        0,        0,        0,        0,        0,        0,
        0,        0,        1,        0,        0,        0,        0,        0,        0,
        0,        1    ]
}
```

Example Usage:<br />
Below is an execution of the function with all parameters provided.
```python
from da4rdm_vis import Evaluate

correlation = Evaluate.eval_corr("RDM_lifecycle_analysis_-_28-04-2022.csv", 'BA1FD94A-CC71-4D32-80AE-67DD2C3BF19A', '2021-04-28', '2023-04-28', "OperationalDatamodify.json", 'cosine', 'binary')
print(corr)
```
Below is an execution of the function with only required parameters provided.
```python
from da4rdm_vis import Evaluate

correlation = Evaluate.eval_corr("RDM_lifecycle_analysis_-_28-04-2022.csv", 'BA1FD94A-CC71-4D32-80AE-67DD2C3BF19A')
print(corr)
```
Below is an example of function execution with no value passed for the parameter corresponding to the path of operational data json file. In order to skip a optional argument, the parameter value should be passed as an empty string at its position. Please refer below for example.
```python
correlation = Evaluate.eval_corr("RDM_lifecycle_analysis_-_28-04-2022.csv", 'BA1FD94A-CC71-4D32-80AE-67DD2C3BF19A', '2021-04-28', '2023-04-28', "", 'cosine', 'binary')
print(corr)
```

Outputs:<br />
All the above executions invokes the function **eval_corr** with the passed parameter values.The correlation values are calculated and returned by the function. Finally, the results received will be printed as shown below.

```python
   RDLC_phase  Correlation_value
0    Planning           0.966092
1  Production           0.000000
2    Analysis           0.000000
3    Archival           0.188982
4      Access           0.356348
5       Reuse           0.000000
```

2. Generating vizualizations or transforming the correlation data retreived using the eval_corr function as discussed in the sections above. To get a vizualization of the results the **visualize** function within the module Vizualize should be used.

Function Inputs:
 This function accepts a dataframe with correlation data and a vizualization format as required parameters and provides relevant visualizazio. The user can choose from the various allowed formats such are jpeg, png, pdf and json. If a user selects the format as jpeg, png or pdf, the result is a RadarChart vizualization of the correlation data. Please refer below for examples.

Example Usage:<br />
Below is an execution of the function with all parameters provided.
```python
from da4rdm_vis import Evaluate

correlation = Evaluate.eval_corr("RDM_lifecycle_analysis_-_28-04-2022.csv", 'BA1FD94A-CC71-4D32-80AE-67DD2C3BF19A')
Visualize.visualize(correlation, 'jpeg')
```


If json is the selected format the function outputs a json representation of the correlation values as shown below:
```python
{"Similarity": {"corr_res": [0.9654746681256314, 0.3613249509436927, 0.2388835160664533, 0.5, 0.46176404435490637, 0.4037749551350624, 0.9654746681256314], "rdlc_phase": ["Planning", "Production", "Analysis", "Archival", "Access", "Reuse", "Planning"]}}
```
The generated files are saved onto the local repository of the program using the package.

## Project status
The project is currently in test phase.
