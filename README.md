![Matplotlib](https://github.com/vhendala/imagens/blob/main/matplotilib.png)
# Introdução ao Matplotlib

- Anotações do Curso de Introdução ao Matplotlib ministrado pelo Prof Felipe na Samsung Ocean
- É a mais famosa biblioteca para criação, visualização e manipulação de gráficos em Python
- É dependente do `numpy` como principal formato de entrada de dados, mas até certo nível, a dependência é quase transparente ao usuário.

## Exemplos

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

### Gráficos 3D

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

### Método simples (um plot)

1a. etapa - Importar o numpy e o matplotlib.pyplot (**apenas uma vez por sessão**).

- O **NumPy** é um pacote para a linguagem Python que suporta arrays e matrizes multidimensionais. Possibilita a manipulação de dados de máneira eficiente. Os dados são passados ao Matplotlib como arrays do Numpy.
- O **matplotlib.pyplot** é um conjunto de funções que permite fazer o **Matplotlib** funcionar como o **MATLAB** (software comercial para matemática computacional).
  - É o método quase padrão para utilizar o **Matplotlib**.

``` python
import numpy as np
import matplotlib.pyplot as plt
```

2a. etapa - Definir os dados a serem plotados.

``` python
x = [1, 2, 3, 4, 5]
y = [4, 10, 11, 7, 5]
```

3a. etapa - Plotar!
``` python
plt.plot(x, y);
```
![Matplotlib3](https://github.com/vhendala/imagens/blob/main/matplotilib3.png)

Um código equivalente seria: 

```python
import numpy as np
import matplotlib.pyplot as plt
x = [1, 2, 3, 4, 5]
y = [4, 10, 11, 7, 5]
plt.plot(x, y);
```

- O *format* `fmt` é uma maneira conveniente de passar a formatação do plot em uma string.

`format = '[marker][line][color]'`

[matplotlib - docs](https://matplotlib.org/3.3.3/api/_as_gen/matplotlib.pyplot.plot.html)

``` python
plt.plot(x, y, 'o:b');
```
![Matplotlib4](https://github.com/vhendala/imagens/blob/main/matplotilib4.png)

### Desafio

Plotar um conjunto de dados (5 elementos quaisquer), sendo que: y é o dobro de x.

Os marcadores deverão ser estrelas, as linhas pontilhadas e verdes.

``` python
# coloque sua resposta aqui
import numpy as np
import matplotlib.pyplot as plt
x = [1,2,3,4,5]
y = [2,4,6,8,10]
plt.plot(x, y, '*--g');
```
![Matplotlib5](https://github.com/vhendala/imagens/blob/main/matplotilib5.png)

#### Resposta
``` python
x = [1,2,3,4,5]
y = [2,4,6,8,10]
plt.plot(x, y, '*--g');
```

### Operações matemáticas (simples) com Numpy

- O Numpy permitiria resolver o Desafio anterior de maneira mais simples.

``` python
# Não deve funcionar

x = [1,2,3,4,5]
plt.plot(x, x*2, '*--g');

# x é um `list`. O Python entende operações matemática (exemplo: *2) em `lists`.
```
![Erro](https://github.com/vhendala/imagens/blob/main/erro.png)
![Matplotlib6](https://github.com/vhendala/imagens/blob/main/matplotilib6.png)

Solução para operações matemáticas com arrays: Numpy.

- Vamos converter x de **list** para **numpy.array**.
- Isso permitirá fazer operações matemáticas com os elemento do **numpy.array**.

``` python
x = np.array([1,2,3,4,5])
plt.plot(x, x*2, '*--g');
```
![Matplotlib7](https://github.com/vhendala/imagens/blob/main/matplotilib7.png)
Documetação do Numpy: https://numpy.org/doc/stable/

## Explorando o matplotlib.pyplot

### Mais de uma plot na mesma figura

- Quando fazemos `plt.plot(...)`, duas coisas acontecem por baixo dos panos:
  - Uma figura é criada.
  - Um par de eixos (x,y) é criado dentro da figura.
- Criar a figura e os eixos por conta própria te dá mais liberdade para explorar o pyplot.

``` python
fig = plt.figure() # cria uma figura
ax = plt.axes() # adiciona um eixo na figura

# dados
x = np.array([1,2,3,4,5])

# plot
ax.plot(x,3*x);
```
![Matplotlib8](https://github.com/vhendala/imagens/blob/main/matplotilib8.png)
Mais um plot compartilhando os mesmo eixos:

``` python
fig = plt.figure() # cria uma figura
ax = plt.axes() # adiciona um eixo na figura

# dados
x = np.array([1,2,3,4,5])

# 2 plots nos mesmos eixos
ax.plot(x,3*x)
ax.plot(x,x+2);
```
![Matplotlib9.1](https://github.com/vhendala/imagens/blob/main/matplotilib9.1.png)

Melhor adicionar uma legenda...

``` python
fig = plt.figure() # cria uma figura
ax = plt.axes() # adiciona um eixo na figura

# dados
x = np.array([1,2,3,4,5])

# 2 plots nos mesmos eixos
ax.plot(x,3*x, label='y=3x')
ax.plot(x,x+2, label='y=x+2');

ax.legend();
```
![Matplotlib10](https://github.com/vhendala/imagens/blob/main/matplotilib10.png)

#### Podemos adicionar uma grid ao gráfico...

``` python
fig = plt.figure() # cria uma figura
ax = plt.axes() # adiciona um eixo na figura

# dados
x = np.array([1,2,3,4,5])

# 2 plots nos mesmos eixos
ax.plot(x,3*x, label='y=3x')
ax.plot(x,x+2, label='y=x+2');

ax.legend()

ax.grid(c='r', alpha=0.4, linestyle='--');
```
![Matplotlib11](https://github.com/vhendala/imagens/blob/main/matplotilib11.png)

Quem sabe um título...
``` python
fig = plt.figure() # cria uma figura
ax = plt.axes() # adiciona um eixo na figura

# dados
x = np.array([1,2,3,4,5])

# 2 plots nos mesmos eixos
ax.plot(x,3*x, label='y=3x')
ax.plot(x,x+2, label='y=x+2');

ax.legend()

ax.grid(c='r', alpha=0.4, linestyle='--')

ax.set_title("Um título de teste");
```
![Matplotlib12](https://github.com/vhendala/imagens/blob/main/matplotilib12.png)

Um nome para x e y...
``` python
fig = plt.figure() # cria uma figura
ax = plt.axes() # adiciona um eixo na figura

# dados
x = np.array([1,2,3,4,5])

# 2 plots nos mesmos eixos
ax.plot(x,3*x, label='y=3x')
ax.plot(x,x+2, label='y=x+2');

ax.legend()

ax.grid(c='r', alpha=0.4, linestyle='--')

plt.title("Um título de teste")

ax.set_xlabel("Meu eixo x")
ax.set_ylabel("Meu eixo y");
```
![Matplotlib13](https://github.com/vhendala/imagens/blob/main/matplotilib13.png)

### Anatomia de uma figura
![Anatomia](https://github.com/vhendala/imagens/blob/main/download.webp)




