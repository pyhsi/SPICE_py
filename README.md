# SPICE
Sparsity Promoting Iterated Constrained Endmembers

***
NOTE: If the SPICE Algorithm is used in any publication or presentation, the following reference must be cited:

Zare, A.; Gader, P.; , "Sparsity Promoting Iterated Constrained Endmember Detection in Hyperspectral Imagery,"" IEEE Geoscience and Remote Sensing Letters, vol.4, no.3, pp.446-450, July 2007.
****

The SPICE Algorithm in Python is run using the function:

```python
from SPICE import *

endmembers, P = SPICE(inputData, parameters)
```

If you would like to use the default parameters (described below), use the command:

`parameters = SPICEParameters()`

The inputData input is a DxM matrix of M input data points with D dimensions.  Each of the M pixels has D spectral bands.  Each pixel is a column vector.   

This form can be achieved from a three-dimensional hyperspectral numpy array using the following commands:

```python
import numpy as np

inputData = np.reshape(inputData, (inputData.shape[0]*inputData.shape[1], inputData.shape[2]))

```

The parameters input is a struct with the following fields:

    parameters.u :  This is the regularization parameter that trades off between the RSS and SPT terms.
    parameters.gamma : Gamma constant for the SPT term, controls the degree of sparsity desired
    parameters.changeThresh : Stopping Criteria, Set this to the desired change threshold for the objective function
    parameters.M : Number of Initial Endmembers
    parameters.iterationCap : Maximum Number of Iterations
    parameters.endmemberPruneThreshold : This is the pruning threshold for endmembers
    parameters.produceDisplay : Set this to 1 if progress display is desired, 0 otherwise
    parameters.initEM = None : By setting this to None, the algorithm randomly selects initial endmembers from the input data. You can also provide initial endmembers by inputting a matrix of endmembers.  Every column is one endmember.  The number of endmembers should match parameters.M.

The parameters structure can be generated using the SPICEParameters.m function.  
unmix2, which is imported with ```from SPICE import *```, is a required helper function which unmixes the data points given the endmembers. 

**Note: Often the parameters must be adjusted for a particular data set. Generally, u is set to between 0.001 and 0.1 depending on noise levels in the data. gamma is generally set to a value between 1 and 10 depending on the data set.   We have also found that SPICE has improved performance if the data has been normalized between 0 and 1 before running SPICE (e.g. Subtracting the minimum and then dividing by the max OR normalizing each spectrum by its L2 norm).**


If you have any questions, please contact:  

Alina Zare  
Electrical and Computer Engineering  
University of Florida    
azare@ufl.edu  

This program uses the python packages in the requirements.txt file. Those can be installed using the command:
```pip install -r requirements.txt```

Note that the newer versions of the packages in requirements.txt are untested, but they should still work.



% This product is Copyright (c) 2018 
% All rights reserved.
