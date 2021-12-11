---
title: "Como acessar o Jupyter a partir de um servidor remoto"
layout: post
date: 2021-12-11 22:48
image: /assets/images/markdown.jpg
headerImage: false
tag:
    - machine-learning
    - metrics
    - scikit-learning
category: blog
author: emdemor
description: Como acessar o Jupyter a partir de um servidor remoto
---

Desde quando entrei na faculdade, lá em 2011, raramente tive um dia inteiro disponível para trabalho home office. Como meu trabalho sempre envolveu programação, computadores desktops nunca fizeram sentido para mim visto que me dexariam ativo apenas durante uma parte do dia. Desde então, sempre tenho um laptop ao meu alcance. Porém, em virtude da possibilidade do trabalho home office em período integral durante a pandemia, resolvi investir em um desktop. Apesar de ter gostado bastante e não pretender mudar tão cedo, sinto falta da flexibilidade que o trabalho em laptops nos dá. Isso fez com que eu não deixasse de usar completamente o meu velho Yoga 520.

Para pequenos projetos, ele ainda está voando e me atende muito bem. Contudo, em projetos mais complexos de Machine Learning, onde eu preciso usar minha GPU, ou necessito de algumas dezenas de RAM para realizar o processamento de bases de dados, o coitado não aguenta. Nesses casos, vou para o desktop. Isso se tornou uma tremenda dor de cabeça pra mim, visto que o meu escritório é um pouco distante da minha casa e eu preciso ficar o máximo de tempo possível em casa agora que minha filha nasceu. **Solução**? Acessar remotamente o desktop a partir do laptop.

De cara, devo salientar que existem várias formas de se fazer isso, sendo que cada um se adequa melhor a um perfil de uso. No meu caso, quando porventura preciso usar uma interface gráfica, o [TeamViewer](https://www.teamviewer.com/pt-br/) me atende muito bem. Não é esse o caso aqui. Minha maior necessidade é acessar o Jupyter iniciado no meu desktop de um navegador local. Nesse tutorial, estou assumindo o seguinte:

-   Tanto o laptop quanto o servidor desktop rodam sistemas linux
-   O servidor ja tem o jupyter instalado com o caminho para seu binário no PATH. (_Ou seja, digitando `jupyter notebook` no terminal, o jupyter inicia._)

Ambos os sistemas linux. Então vamos lá

## 1. Encontre o IP do dektop e o nome do usuário

Para isso, acesse fisicamente o desktop, abra o terminal e rode:

```bash
hostname -I | awk '{print $1}'
```

O resultado deve ser um código de 9 caracteres numéricos, com a seguinte forma:

`XXX.XXX.X.XX`

que geralmente começa com 192.168. Guarde o IP.

Você precisará também do nome do seu usuário no servidor e a senha. Caso você não saiba, basta rodar o comando

```bash
whoami
```

Guarde essa informação também.

## 2. Acesso remoto ao desktop

O segundo passo é acessar remotamente o desktop com ssh. O procedimento está muito bem descrito nesse [artigo da alura](https://www.alura.com.br/artigos/como-acessar-servidores-remotamente-com-ssh), escrito pelo Yuri Matheus. Basicamente, supondo que o IP é 192.168.0.00 e o usuário "usuario_do_servidor" rode o comando:

```bash
# Substitua "usuario_do_servidor" e "192.168.0.00" pelas suas informações
ssh usuario_do_servidor@192.168.0.00
```

Após o comando, se tudo der certo, você verá no início da linha do seu terminal as informações:

```bash
usuario_do_servidor@nome_do_servidor:~$
```

## 3. Inicie o Jupyter

Dentro do servidor, rode o comando:

```bash
jupyter notebook
```

Quando você faz isso, o jupyter será iniciado em uma porta disponível, geralmente `8888`

```python
import matplotlib.colors


def hex_to_rgb(h:str) -> tuple:
    """
    Converts an hex color code to rgb tuple.
    """
    return tuple(int(h.replace("#", "")[i : i + 2], 16) / 255 for i in (0, 2 4))


def define_colormap(color_list:list) -> matplotlib.colors.ListedColormap:
    """
    Receives a list of hex colors an defines an matplotlib color map.
    """

    color_list = list(map(hex_to_rgb, color_list))

    cim = np.transpose(
        np.array(
            [
                np.concatenate(
                    [
                        np.linspace(color_list[j][i], color_list[j + 1][i], 100)
                        for j in range(len(color_list) - 1)
                    ]
                )
                for i in range(3)
            ]
        )
    )

    cmap = matplotlib.colors.ListedColormap(cim)

    return cmap

colors = ['#ffc801ff','#fff647','#1bcbdcff','0046a0ff',]
cmap = define_colormap(colors)
```

```python
import graphviz
from sklearn import tree
import os

def export_tree(
    model: tree._classes.DecisionTreeClassifier,
    description: str,
    feature_names=None,
    class_names=['0','1'],) -> graphviz.files.Source:
    '''  '''
    dot_data = tree.export_graphviz(model, out_file=f'tree_{description}.dot',
                                    feature_names=feature_names,
                                    class_names=class_names,
                                    filled=True,
                                    proportion = True
                                   )

    os.system(f'dot -Tpng tree_{description}.dot -o results/tree_{description}.png')
    os.system(f'rm -f tree_{description}.dot')
    # !dot -Tpng tree_imput_mean.dot -o tree_imput_mean.png
    # !rm -f tree.dot


    # DOT data
    dot_data = tree.export_graphviz(model, out_file=None,
                                    feature_names=feature_names,
                                    class_names=class_names,
                                    filled=True,
                                    proportion = True
                                   )

    # Draw graph
    graph = graphviz.Source(dot_data, format="png")
    return graph
```

```python
from sklearn.base import TransformerMixin, BaseEstimator
from statsmodels.distributions.empirical_distribution import ECDF

class LogScaler(BaseEstimator, TransformerMixin):

    def __init__(self):
        pass

    def fit(self,X):
        return self

    def transform(self, X):
        return self.__logscale(X)

    def inverse_transform(self,X):
        return self.__expscale(X)

    def fit_transform(self, X):
        self.fit(X)
        return self.transform(X)

    def __logscale(self,x):
        return np.sign(x) * np.log(np.abs(x))

    def __expscale(self,x):
        return np.sign(x) * (np.exp(np.abs(x)))

```
