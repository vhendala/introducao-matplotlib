# Introdução ao Matplotlib
- Anotações do Curso de Introdução ao Matplotlib ministrado pelo Prof Felipe na Samsung Ocean
- É a mais famosa biblioteca para criação, visualização e manipulação de gráficos em Python
- É dependente do `numpy` como principal formato de entrada de dados, mas até certo nível, a dependência é quase transparente ao usuário.

```python
import numpy as np
import matplotlib.pyplot as plt
plt.rcParams['figure.figsize'] = [20, 4]
plt.rcParams['figure.dpi'] = 100 

fig, ax = plt.subplots(1, 4, tight_layout=True)

# grafico simples
x = np.linspace(0, 10, 100)
ax[0].plot(x, np.sin(x), '-', label="$sen(x)$")
ax[0].plot(x, np.cos(x), '--', label="$cos(x)$");
ax[0].set_title("$y(x) = sen(x)$ and $y(x) = cos(x)$")
ax[0].legend()

# grafico a partir de pontos
x = np.sort(np.random.uniform(0,1,10))
y = x**2
ax[1].plot(x, y, 'o-');
ax[1].set_title("$(x,y)$ coordinates")

# scatter plot
from sklearn.datasets import load_iris
iris = load_iris()
features = iris.data.T
ax[2].scatter(features[0], features[1], alpha=0.4, s=300*features[3], c=iris.target);
ax[2].set_title("Scatter plot")

# imagem
import matplotlib.cbook as cbook

with cbook.get_sample_data('grace_hopper.png') as image_file:
    image = plt.imread(image_file)

ax[3].imshow(image);
ax[3].set_title("Image");
```
