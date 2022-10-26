![Matplotlib](https://github.com/vhendala/imagens/blob/main/matplotilib.png)
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
![Matplotlib1](https://github.com/vhendala/imagens/blob/main/matplotilib1.png)

``` python
from mpl_toolkits.mplot3d import Axes3D
import matplotlib.tri as mtri


fig = plt.figure(figsize=plt.figaspect(0.5))

# Make a mesh in the space of parameterisation variables u and v
u = np.linspace(0, 2.0 * np.pi, endpoint=True, num=50)
v = np.linspace(-0.5, 0.5, endpoint=True, num=10)
u, v = np.meshgrid(u, v)
u, v = u.flatten(), v.flatten()

# This is the Mobius mapping, taking a u, v pair and returning an x, y, z
# triple
x = (1 + 0.5 * v * np.cos(u / 2.0)) * np.cos(u)
y = (1 + 0.5 * v * np.cos(u / 2.0)) * np.sin(u)
z = 0.5 * v * np.sin(u / 2.0)

# Triangulate parameter space to determine the triangles
tri = mtri.Triangulation(u, v)

# Plot the surface.  The triangles in parameter space determine which x, y, z
# points are connected by an edge.
ax = fig.add_subplot(1, 2, 1, projection='3d')
ax.plot_trisurf(x, y, z, triangles=tri.triangles, cmap=plt.cm.Spectral)
ax.set_zlim(-1, 1);

plt.rcParams['figure.figsize'] = [8, 4]
plt.rcParams['figure.dpi'] = 100 ;
```

![Matplotlib2](https://github.com/vhendala/imagens/blob/main/matplotilib2.png)

# Um gráfico simples

- Todo gráfico, em 2D, é um conjunto de pontos (coordenadas) $(x,y)$.
- Gráfico (plot) dos pontos abaixo.

| x | y  |
|---|----|
| 1 | 4  |
| 2 | 10 |
| 3 | 11 |
| 4 | 7  |
| 5 | 5  |
