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
plt.plot(x,up,label=r"$\mathrm{up}(x)$")
plt.plot(x,up_deriv,label=r"$\mathrm{up'}(x)$")
plt.legend()

plt.subplot(1,2,2)
plt.plot(x,up3,label=r"$\mathrm{up_3}(x)$")
plt.plot(x,up3_deriv,label=r"$\mathrm{up'_3}(x)$")
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

## Example 4
```python
import numpy as np
import matplotlib.pyplot as plt
import waf

x=np.linspace(-10,10,1000)
wavelet=waf.Wavelet('up')

plt.figure(figsize=(9,4))

plt.subplot(121)
plt.plot(x,wavelet.phi(x),label='Scaling function')
plt.plot(x,wavelet.psi(x),label='Wavelet')
plt.legend()

plt.subplot(122)
plt.plot(x,wavelet.phi_f(x),label='Scaling function')
plt.plot(x,np.abs(wavelet.psi_f(x)),label='Wavelet')
plt.legend()

plt.show()
```
<img src="https://github.com/Atomic-community/.github/blob/main/example/example_4.png" >

## Example 5
```python

import numpy as np
import matplotlib.pyplot as plt
from PIL import Image
import pywt
import waf

image = Image.open(path)

N = 62

wavelet=waf.Wavelet('up')
filter_bank = [wavelet.filter(N)['dec_lo'],wavelet.filter(N)['dec_hi'],wavelet.filter(N)['rec_lo'],wavelet.filter(N)['rec_hi']]
pywt_wavelet=pywt.Wavelet(filter_bank=filter_bank)

matrix=np.array(image)
matrix_R=matrix[:,:,0]
matrix_G=matrix[:,:,1]
matrix_B=matrix[:,:,2]

def filtration(matrix):
    new_matrix=[]
    cA9,cD9,cD8,cD7,cD6,cD5,cD4,cD3, cD2, cD1 = pywt.wavedec(matrix, pywt_wavelet, mode='symmetric', level=9)
    coeffs = [cA9,cD9*0,cD8*0,cD7*0,cD6*0,cD5*0,cD4*0,cD3*0, cD2*0, cD1*0]
    new_matrix.append(pywt.waverec(coeffs, pywt_wavelet))
    return np.array(new_matrix)

filtered_matrix_R=filtration(matrix_R)
filtered_matrix_G=filtration(matrix_G)
filtered_matrix_B=filtration(matrix_B)

matrix_RGB=np.zeros(matrix.shape)
matrix_RGB[:,:,0]=filtered_matrix_R
matrix_RGB[:,:,1]=filtered_matrix_G
matrix_RGB[:,:,2]=filtered_matrix_B

filtered_image = Image.fromarray(np.uint8(matrix_RGB))

plt.figure(figsize=(9,5))

plt.subplot(121)
plt.imshow(image)
plt.axis('off')
plt.title('Original')

plt.subplot(122)
plt.imshow(filtered_image)
plt.axis('off')
plt.title('Filtered')

plt.show()
```
<img src="https://github.com/Atomic-community/.github/blob/main/example/example_5.png" >
