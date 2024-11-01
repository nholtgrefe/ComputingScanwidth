
# Exact and Heuristic Computation of the Scanwidth of DAGs

Repository corresponding to the paper ["Exact and Heuristic Computation of the Scanwidth of Directed Acyclic Graphs"](https://arxiv.org/abs/2403.12734) by Niels Holtgrefe, Leo van Iersel and Mark Jones.

Citation of the paper (and the repository) in `bibtex` format:

```
@misc{holtgrefe2024exact,
    title={Exact and Heuristic Computation of the Scanwidth of Directed Acyclic Graphs},
    author={Holtgrefe, Niels and van Iersel, Leo and Jones, Mark},
    year={2024},
    month={3},
    eprint={2403.12734},
    archivePrefix={arXiv}
}
```


## Repository structure
The repository contains three folders:
* 'code', which contains the Python files used in the project. The file `ZODS_generator.py` contains the python-code used to generate all synthetic networks, while the file `plotting_module.py` contains some basic plotting-functionality that is imported in the main file. The main file is `scanwidth.py` which contains all the implemented algorithms (see below for more info on how to use it).
* 'networks', containing two subfolders with the real and synthetic phylogenetic networks used in the thesis. All networks are text-files in the edge-list format (`.el`), where each line contains one arc (e.g. `vertex1 vertex2`). The file names of the real networks are the same as in the original source (see http://phylnet.univ-mlv.fr/). The file names of the synthetic networks are in the format `a_ZODS_Lxxxx_Ryyyy_zzzzzz.el`, where 'x' denotes the number of leaves, 'y' the number of reticulations, and 'z' the number of the network.
* 'experimental_results', which contains an `.xlsx`-file for the real networks, and one for the synthetic networks, containing the complete numerical results of all experiments for each network. The experiments are explained in Section 6 of the paper.
## How to use the code
The main-file `scanwidth.py` is meant to be imported in a python script in the same directory. It contains four classes: `DAG`, `Network` (specifically for networks), `Extension`, and `TreeExtension`. The class `DAG` (or `Network`) is the important class for the scanwidth-algorithms, and uses `NetworkX` as its graph implementation. To illustrate its use, we show an example on how to find the exact value of the scanwidth `sw` of a DAG from a file `in_file`, and how to save the optimal extension in the file `out_file`.
```
from scanwidth import DAG, Network, TreeExtension, Extension
in_file = r'path\to\dag\in\edge-list\format.txt'

G = DAG(in_file)
sw, extension = G.optimal_scanwidth()

out_file = r'file\path\where\extension\should\be\saved.txt'
extension.save_file(out_file)
```
The important algorithms discussed in the paper are implemented as methods of the classes `DAG`/`Network`: `optimal_scanwidth`, `greedy_heuristic`, `cut_splitting_heuristic`, and `simulated_annealing`. All of them return a scanwith value, and an extension object. For the specific parameter-settings of these methods, we refer to the documentation in the file.

The different classes also contain some other handy methods, such as the `canonical_tree_extension` method of the `Extension` class, which returns a `TreeExtension` object with the same scanwidth as the extension. For a complete overview of all methods and their uses, we refer to the documentation in the python-file.
