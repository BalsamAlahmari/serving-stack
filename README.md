## W2D3 Containerisation Results

### Predictions

Before building the images, I predicted:

| Prediction | Estimate |
|---|---:|
| Final image size (code + CPU PyTorch, no model weights) | ~800 MB |
| Code edits out of 10 that would re-run `pip install` if `COPY . .` came first | 10/10 |
| Naive image size before slimming | ~1800 MB |
| Expected slim image size | ~800 MB |

### Actual Image Sizes

After building and measuring both images:

| Stage | Actual Image Size |
|---|---:|
| Naive build (full base, cached pip) | **9.69 GB** |
| Slim build (slim base, CPU PyTorch, no pip cache) | **3.43 GB** |

The optimized image was **6.26 GB smaller** than the naive image, a reduction of approximately **65%**.
