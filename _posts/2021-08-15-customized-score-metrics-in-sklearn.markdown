---
title: "How to define colormaps in python"
layout: post
date: 2021-08-15 22:48
image: /assets/images/markdown.jpg
headerImage: false
tag:
    - machine-learning
    - metrics
    - scikit-learning
category: blog
author: emdemor
description: How to define colormaps in python
---

```python
import matplotlib.colors


def hex_to_rgb(h:str) -> tuple:
    """
    Converts an hex color code to rgb tuple.
    """
    return tuple(int(h.replace("#", "")[i : i + 2], 16) / 255 for i in (0, 2, 4))


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
