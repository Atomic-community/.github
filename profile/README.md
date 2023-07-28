![](https://komarev.com/ghpvc/?username=Atomic-community&color=00af54)

## Installation
```bash
pip install pywaf
```

## Example 1
```python
import numpy as np
import matplotlib.pyplot as plt
from waf.kernel import AtomicKernel

x=np.linspace(-1,1,1000)

up=AtomicKernel.up(x)
up_deriv=AtomicKernel.up_deriv(x)

up3=AtomicKernel.upm(x,3)
up3_deriv=AtomicKernel.upm_deriv(x,3)

plt.subplot(1,2,1)
plt.plot(x,up,label=r"$\mathrm{up}(x)$",color='red')
plt.plot(x,up_deriv,label=r"$\mathrm{up'}(x)$",color='blue')
plt.legend()

plt.subplot(1,2,2)
plt.plot(x,up3,label=r"$\mathrm{up_3}(x)$",color='red')
plt.plot(x,up3_deriv,label=r"$\mathrm{up'_3}(x)$",color='blue')
plt.legend()

plt.show()
```
<img src="example/example_1.svg">

