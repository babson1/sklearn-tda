# sklearn_tda: a scikit-learn compatible python package for Machine Learning and TDA

**Author**: Mathieu Carriere.

# Description

sklearn_tda is a python package for handling collections of persistence diagrams for machine learning purposes.
Various preprocessing methods, vectorizations methods and kernels for persistence diagrams are implemented in a [scikit-learn](http://scikit-learn.org/) compatible fashion.

### Preprocessing

Currently available classes are: 

  * **BirthPersistenceTransform**: applies the affine transformation (x,y) -> (x,y-x) to the diagrams.

    Parameters: None

  * **DiagramPreprocessor**: applies a scaler to the diagrams (such as scalers from [scikit-learn](http://scikit-learn.org/)).

    Parameters:

    | **name** | **description** |
    | --- | --- |
    | **use** = False | whether to use the class or not. |
    | **scaler** = sklearn.preprocessing.StandardScaler() | a scaler to be fit on the diagrams. |

  * **ProminentPoints**: removes points close to the diagonal.

    Parameters:

    | **name** | **description** |
    | --- | --- |
    | **use** = False|     whether to use the class or not. |
    | **num_pts** = 10|    cardinality threshold (points are ordered by persistence). |
    | **threshold** = -1|  distance-to-diagonal threshold. |
    | **point_type** = "upper"|  whether to keep the points above ("upper") or below ("lower") the aforementioned thresholds. |
    

  * **DiagramSelector**: returns the finite or essential points of the diagrams.

     Parameters:

    | **name** | **description** |
    | --- | --- |
    | **limit** = np.inf | diagram points with ordinate equal to **limit** will be considered as essential. |
    | **point_type** = "finite"| specifies the point type to return. Either "finite" or "essential". |

### Vectorizations


Currently available classes are:

  * **Landscape**: implementation of [landscapes](http://jmlr.org/papers/v16/bubenik15a.html).

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**num_landscapes** = 5| number of landscape functions.|
    |**resolution** = 100| resolution of each landscape function.|
    |**ls_range** = [np.nan, np.nan]| range of x-coordinate. If np.nan, min and max on x-axis are computed from the diagrams.|

  * **PersistenceImage**: implementation of [persistence images](http://jmlr.org/papers/v18/16-337.html).

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**bandwidth** = 1.0 | Bandwidth of Gaussian kernel on the plane.|
    |**weight** = lambda x: 1| weight on diagram points. It is a python function.|
    |**resolution** = [20,20]| resolution of image.|
    |**im_range** = [np.nan, np.nan, np.nan, np.nan]| range of coordinates. If np.nan, min and max on each axis are computed from the diagrams.|

  * **BettiCurve**: implementation of [Betti curves](https://www.researchgate.net/publication/316604237_Time_Series_Classification_via_Topological_Data_Analysis).

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**resolution** = 100| resolution of Betti curve.|
    |**bc_range** = [np.nan, np.nan]| range of x-coordinate. If np.nan, min and max on x-axis are computed from the diagrams.|

  * **Silhouette**: implementation of [silhouettes](http://jocg.org/index.php/jocg/article/view/203).

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**weight** = lambda x: 1| weight on diagram points. It is a python function.|
    |**resolution** = 100| resolution of silhouette.|
    |**range** = [np.nan, np.nan]| range of x-coordinate. If np.nan, min and max on x-axis are computed from the diagrams.|

  * **TopologicalVector**: implementation of [distance vectors](https://diglib.eg.org/handle/10.1111/cgf12692).

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**threshold** = 10| number of distances to keep.|

### Kernels

Currently available classes are:

  * **PersistenceScaleSpace**: implementation of [persistence scale space kernel](https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Reininghaus_A_Stable_Multi-Scale_2015_CVPR_paper.pdf). **Requires cython!!**

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**bandwidth** = 1.0| bandwidth of kernel.|

  * **PersistenceWeightedGaussian**: implementation of [persistence weighted gaussian kernel](http://proceedings.mlr.press/v48/kusano16.html). **Requires cython!!**

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**bandwidth** = 1.0 | Bandwidth of Gaussian kernel on the plane.|
    |**weight** = lambda x: 1| weight on diagram points. It is a python function.|
    |**use_pss** = False| whether to add symmetric of points from the diagonal.|

  * **SlicedWasserstein**: implementation of [sliced Wasserstein kernel](http://proceedings.mlr.press/v70/carriere17a.html). **Requires cython!!**

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**num_directions** = 10| number of directions.|
    |**bandwidth** = 1.0| bandwidth of kernel.|

### Metrics

Currently available classes are:

  * **WassersteinDistance**: wrapper for [hera](https://bitbucket.org/grey_narn/hera/src). **Requires cython!!**

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**wasserstein** = 1| index of Wasserstein distance. Set to np.inf for bottleneck distance.|
    |**delta** = 0.001| approximation error.|

  * **SlicedWassersteinDistance**: implementation of [sliced Wasserstein distance](http://proceedings.mlr.press/v70/carriere17a.html). **Requires cython!!**

    Parameters:

    | **name** | **description** |
    | --- | --- |
    |**num_directions** = 10| number of directions.|

### Clustering

  * **GraphInducedComplex**: wrapper for the [Graph Induced Complex](http://gudhi.gforge.inria.fr/python/latest/nerve_gic_complex_ref.html) module of Gudhi. **Requires Gudhi!!**

    Parameters:

    | **name** | **description** |
    | --- | --- |
    | **graph**=-1 | radius for the neighborhood graph built on top of the point cloud. If -1, it is computed automatically from **graph_subsampling**,  
                     **graph_subsampling_power** and  **graph_subsampling_constant**. |
    | **graph_subsampling**=100 | number of subsamples drawn on data. Not used if **graph**>0. |
    | **graph_subsampling_power**=0.001| power for the approximation method. Not used if **graph**>0.|
    | **graph_subsampling_constant**=10| constant for the approximation method. Not used if **graph**>0.|

  * **Mapper**: implementation of the [Mapper](https://research.math.osu.edu/tgda/mapperPBG.pdf).

    Parameters

# Installing sklearn_tda

The sklearn_tda library requires:

* python [>=2.7, >=3.5]
* numpy [>= 1.8.2]
* scikit-learn
* cython (optional but strongly recommended)

For now, the package has to be compiled from source. You have to 

* download the code with:
```shell
git clone https://github.com/MathieuCarriere/sklearn_tda
```
* move to the directory:
```shell
cd sklearn_tda
```
* compile with:
```shell
(sudo) pip install .
```

The package can then be imported in a python shell with:
```shell
import sklearn_tda
``` 

Usage
=====

Sets of diagrams are represented as lists of 2D numpy arrays.
All modules are standard scikit-learn modules: they have fit, transform and fit_transform methods.
Hence, the most common way to use module X on a list of persistence diagrams D is to call X.fit_transform(D).
You can check [this python file](example/example_of_computations.py) and [this notebook](data/3DSegTDA.ipynb) for examples of computations.
