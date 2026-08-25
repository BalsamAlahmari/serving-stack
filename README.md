## W2D3 Containerisation Results

### Actual Image Sizes

After building and measuring both images:

| Stage | Actual Image Size |
|---|---:|
| Naive build (full base, cached pip) | **9.69 GB** |
| Slim build (slim base, CPU PyTorch, no pip cache) | **3.43 GB** |

The optimized image was **6.26 GB smaller** than the naive image, a reduction of approximately **65%**.
