# MiniEinops – Rearrange from Scratch

This project is a minimal reimplementation of the `einops.rearrange` function using pure NumPy. It supports a range of tensor manipulation operations using a compact and expressive pattern syntax inspired by Einstein notation.

## ✅ Features Supported

- **Reshaping**: split or collapse dimensions using patterns like `(c h)`
- **Transposition**: change axis order, e.g., `'b c h -> h c b'`
- **Splitting**: e.g., `'b (c h) -> b c h'` with known or inferred sizes
- **Merging**: e.g., `'b c h -> b (c h)'`
- **Repeating**: e.g., `'b c -> b c r'` with `r=2`

## ❌ Not Yet Supported

- Ellipsis (`...`) for batch dimensions (implementation partially planned)

## 🧪 Unit Tests

Comprehensive unit tests are provided using Python’s `unittest` module. These test:

- Transposing axes
- Merging and splitting
- Repeating new axes
- Shape validation and error reporting


🛠️ How It Works
The parse_pattern() function tokenizes left and right patterns.
infer_left_axes() resolves the input shape and splits merged groups.

The rearrange() function handles:
1. Transposition via np.transpose
2. Merging/splitting via reshape
3. Repeats via np.repeat along new axes

🧠 Design Decisions
- No external dependencies besides NumPy
- Code prioritizes readability and modularity
- All logic separated by stage: parsing, inferring, applying


🧪 Running Tests in Colab
To run the unit tests:

import unittest
suite = unittest.TestLoader().loadTestsFromTestCase(TestRearrange)
unittest.TextTestRunner(verbosity=2).run(suite)



## 📦 Example Usage

```python
import numpy as np
from minieinops import rearrange

# Transpose
x = np.random.rand(3, 4)
rearrange(x, 'h w -> w h')

# Split an axis
x = np.random.rand(12, 10)
rearrange(x, '(h w) c -> h w c', h=3)

# Merge axes
x = np.random.rand(3, 4, 5)
rearrange(x, 'a b c -> (a b) c')

# Repeat an axis
x = np.random.rand(3, 1, 5)
rearrange(x, 'a 1 c -> a b c', b=4)



