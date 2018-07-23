# nanopq

Nano Product Quantization (nanopq): product quantization for nearest neighbor search in a single python file.

This package contains a vanilla implementation of Product Quantization (PQ) and Optimized Product Quantization (OPQ) written in pure python without any third party dependencies.


## Installing
You can install the package via pip. This library works with Python 3.6+ on linux.
```
pip install nanopq
```

## Documentation
- Tutorial
- API

## Example

```python
import nanopq
import numpy as np

X = np.random.random((10000, 128))
query = np.random.random((128,))

# Instantiate with M=8 sub-spaces
pq = nanopq.PQ(M=8)

# Train with the top 1000 vectors
pq.fit(X[:1000])

# Encode to pq-codes
X_code = pq.encode(X)  # (10000, 8) with dtype=np.uint8

# Results
dtable = pq.dtable(query)  # Compute a distance table online
dists = pq.adist(dtable, X_code)  # Asymmetric distance
```

## Author
- [Yusuke Matsui](http://yusukematsui.me)


## Reference
- [H. Jegou, M. Douze, and C. Schmid, "Product Quantization for Nearest Neighbor Search", IEEE TPAMI 2011](https://ieeexplore.ieee.org/document/5432202/) (the original paper of PQ)
- [T. Ge, K. He, Q. Ke, and J. Sun, "Optimized Product Quantization", IEEE TPAMI 2014](https://ieeexplore.ieee.org/document/6678503/) (the original paper of OPQ)
- [Y. Matsui, Y. Uchida, H. Jegou, and S. Satoh, "A Survey of Product Quantization", ITE MTA 2018](https://www.jstage.jst.go.jp/article/mta/6/1/6_2/_pdf/) (a survey paper of PQ) 
- [PQ in faiss](https://github.com/facebookresearch/faiss/wiki/Faiss-building-blocks:-clustering,-PCA,-quantization#pq-encoding--decoding) (Faiss contains an optimized implementation of PQ. See the difference to ours here)
- [Rayuela.jl](https://github.com/una-dinosauria/Rayuela.jl) (Julia implementation of several encoding algorithms including PQ and OPQ)
- [PQk-means](https://github.com/DwangoMediaVillage/pqkmeans) (clustering on PQ-codes. The implementation of nanopq is compatible to [that of PQk-means](https://github.com/DwangoMediaVillage/pqkmeans/blob/master/tutorial/1_pqkmeans.ipynb))