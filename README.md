## **AlphafoldModel** is a package to parse Alphafold PDB structures and PAE Matrices into interactive Python objects.

### The package contains the following important classes:
- `AlphafoldModel.AlphafoldModel`: Parses the Alphafold model PDB file alongside its JSON PAE matrix into an interactive Python object. It allows declarative queries for a model's local PAE and plDDT metrics.
- `ModelPDB.ModelPDB` is the base class that carries the PDB parsing functionalities as well as residue-based nearest-neighbour search methods.
- `ModelPAE.ModelPAE` is the base class that carries the PAE parsing functionalities for `AlphafoldModel`.
- `LoadedKDTree.LoadedKDTree` is a wrapper class which provides an interface over the `scipy.spatial.KDTree` class to instead store and return arbitrary objects with coordinate information.

### Explore the source file in:
`src/alphafoldmodel`

### Installing
```
pip install alphafoldmodel
```

### Import
```python
from alphafoldmodel import *
```

This will give you access to all 4 modules of the `alphafoldmodel` package. Optionally, import individual modules.
```python
from alphafoldmodel import AlphafoldModel as afm
```

### Common Usage
Instantiate by passing a filepaths to the structure's PDB file and its corresponding PAE matrix. These can typically be obtained from the [EBI Alphafold Protein Database](https://alphafold.ebi.ac.uk/).
```python
from alphafoldmodel import AlphafoldModel as afm

# instantiate
alphafoldModel = afm.AlphafoldModel('./path/to/PDB.pdb', './path/to/PAE.json')

# get pLDDT for a specific residue position, returning a tuple of (pLDDT: float, confidence: boolean)
# by default, confidence = True with pLDDT >= 70 and False otherwise
alphafoldModel.get_plddt(1)

# get average pLDDT within some radius (in Å) of a residue
# by default, returns the average pLDDT of all residues within 5Å of the query
alphafoldModel.get_local_plddt(1)

# get pLDDT of individual residues within some radius
# returns a nested tuple of ((residue pLDDT, residue name), ...)
alphafoldModel.get_local_plddt(1, average=False)

# get average PAE within some radius (in Å) of a residue
# by default, returns the average PAE of all possible residue pairs within 5Å
alphafoldModel.get_local_pae(1)

# getting chain information
# returns a dictionary with various fields like length, sequence, etc
# Alphafold models are currently single chain but multi-chain parsing have been built in for future extensibility
alphafoldModel.get_chain('A').get_info()

# iterating through residues in a chain
for residue in alphafoldModel.get_chain('A'):
    # do something
```

Other methods are available and can be explored in `src/alphafoldmodel`. It is recommended to leverage code completion and parameter information features through Intellisense built into VSCode. All important methods have been documented in the source code.






































