# RDKit_ML_Comparison

A simple comparative illustration on predicting molecular properties from chemical structure using RDKit, scikit-learn, and PyTorch. 

Here I use the MoleculeNet ESOL dataset (https://moleculenet.org/datasets-1), which provides water solubility data (log solubility in mols/L) for common organic small molecules. Various molecular representations (RDKit fingerprint, Morgan fingerprint, and a vector of selected molecular features) are used to train a series of regression models (linear, ridge, lasso, and multilayer perceptron). Finally, a graph convolutional neural network is used on a node and edge representation of the atoms and bonds respectively to address drawbacks with the previous methodologies.

As expected, the simplest linear regression is poorly performant at predicting properties, while the lasso regression which incorporates regularization penalizing the absolute value magnitude of coefficients performs better, and the deep learning multilayer perception approach performs the best. For these regressors, using a limited vector of selected chemical features that directly represent physical attributes provides better results than the more complicated fingerprints that fully encode each molecule, as we have already pre-selected key information from each molecule.  

The drawbacks of this approach however are that 1) a priori selection of features is required for best performance - which is not always possible, especially in the most interesting regimes of novel discovery and 2) the deep learning multilayer perceptron requires training many parameters, in this case ~70k.

To mitigate these issues, I next represent each molecule as a graph, where atoms are nodes and bonds are undirected edges, and use a graph convolutional network to perform graph regression. In this way, 1) I do not need to encode a priori selected features that are relevant to the prediction task and 2) I am able to achieve comparable performance to the multilayer perceptron with a fraction of the parameters, in this case ~13k or <20% of the multilayer perceptron. 
