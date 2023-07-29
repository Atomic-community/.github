![](https://komarev.com/ghpvc/?username=Atomic-community&color=00af54)

## Installation
```bash
pip install pywaf
```

## Example 1
```python
import numpy as np
import matplotlib.pyplot as plt
from waf import AtomicKernel

x=np.linspace(-1,1,1000)

up=AtomicKernel.up(x)
up_deriv=AtomicKernel.up_deriv(x)

up3=AtomicKernel.upm(x,3)
up3_deriv=AtomicKernel.upm_deriv(x,3)

plt.figure(figsize=(12,4))

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
<img src="https://github.com/Atomic-community/.github/blob/main/example/example_1.png" >

## Example 2
```python
import numpy as np
import matplotlib.pyplot as plt
import waf

N=100

plt.figure(figsize=(12,4))

plt.subplot(1,2,1)
plt.plot(waf.up(N),label=r'$\mathrm{up}$')
plt.plot(waf.upm(N,m=3),label=r'$\mathrm{up}_3$')
plt.plot(waf.ha(N,a=3),label=r'$\mathrm{h}_3$')
plt.plot(waf.xin(N,n=3),label=r'$\mathrm{\Xi}_3$')
plt.plot(waf.fupn(N,n=3),label=r'$\mathrm{fup}_3$')
plt.plot(waf.chan(N,a=2,n=3),label=r'$\mathrm{ch}_{2,3}$')
plt.plot(waf.fipan(N,a=2,n=1),label=r'$\mathrm{fip}_{2,1}$')
plt.plot(waf.fpmn(N,m=2,n=1),label=r'$\mathrm{fp}_{2,1}$')
plt.title(r'$\mathrm{mode}=max$')
plt.legend()

plt.subplot(1,2,2)
plt.plot(waf.up(N,mode='area'),label=r'$\mathrm{up}$')
plt.plot(waf.upm(N,m=3,mode='area'),label=r'$\mathrm{up}_3$')
plt.plot(waf.ha(N,a=3,mode='area'),label=r'$\mathrm{h}_3$')
plt.plot(waf.xin(N,n=3,mode='area'),label=r'$\mathrm{\Xi}_3$')
plt.plot(waf.fupn(N,n=3,mode='area'),label=r'$\mathrm{fup}_3$')
plt.plot(waf.chan(N,a=2,n=3,mode='area'),label=r'$\mathrm{ch}_{2,3}$')
plt.plot(waf.fipan(N,a=2,n=1,mode='area'),label=r'$\mathrm{fip}_{2,1}$')
plt.plot(waf.fpmn(N,m=2,n=1,mode='area'),label=r'$\mathrm{fp}_{2,1}$')
plt.title(r'$\mathrm{mode}=area$')
plt.legend()

plt.show()
```
<img src="https://github.com/Atomic-community/.github/blob/main/example/example_2.png" >

## Example 3
```python
import numpy as np
import matplotlib.pyplot as plt
import waf

N=30
x=np.arange(N)

wavelet=waf.Wavelet('up')
filter_bank=wavelet.filter(N)

fig=plt.figure(figsize=(12,4))

for i,item in enumerate(filter_bank):
    fig.add_subplot(1,4,i+1)
    plt.scatter(x,filter_bank[item])
    plt.vlines(x,0,filter_bank[item])
    plt.title(item)
    plt.ylim(-1,1)

plt.show()
```
<img src="https://github.com/Atomic-community/.github/blob/main/example/example_3.png" >
