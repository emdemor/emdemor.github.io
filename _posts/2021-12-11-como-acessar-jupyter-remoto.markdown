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
-   O servidor ja tem o Jupyter instalado com o caminho para seu binário no PATH. (_Ou seja, digitando `jupyter notebook` no terminal, o Jupyter inicia._)

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

## 3. Relacione a porta no servidor remoto com uma porta local

Precisamos conectar a porta remota com uma porta local para conseguirmos acessar o Jupyrt. Para isso, você pode configurar um tunnel SSH. Vamos supor que você escolheu a porta local `8888` e uma porta remota `1234`. O comando será:

```bash
ssh -L 8888:localhost:1234 usuario_do_servidor@192.168.0.00
```

Após isso, o que o Jupyter do servidor transmitir na porta remota `1234` será acessível na porta local `8888`.

> **Atenção**: deve ficar claro que essas portas foram escolhidas para fins de exemplo, cabendo a você escolher aquelas de maior conveniência. Particularmente, eu uso `8888` tanto para porta local quanto para porta remota. Contudo, ficaria bastante confuso se usasse esses valores aqui!

## 4. Inicie o Jupyter

Ok. Agora, no servidor, precisamos rodar Jupyter na porta especificada. Dentro do servidor, se rodarmos o comando:

```bash
jupyter notebook --no-browser
```

iremos abrir o Jupyter no servidor. O argumento opcional `no-browser` impede que seja aberta uma aba no navegador do servidor com uma sessão do Jupyter. Contudo, quando fazemos isso, o Jupyter será iniciado em uma porta disponível, geralmente a `8888`

![Minha imagem](https://raw.githubusercontent.com/emdemor/emdemor.github.io/main/assets/images/blog/2021-12-11-como-acessar-jupyter-remoto/porta8888.png)

Contudo, precisamos especificar a porta que configuramos no tunel. No caso, é a `1234` rode o comando:

```bash
jupyter notebook --no-browser --port=1234
```

Olha a diferença:

![Minha imagem](https://raw.githubusercontent.com/emdemor/emdemor.github.io/main/assets/images/blog/2021-12-11-como-acessar-jupyter-remoto/port1234.png)

No decorrer do tutorial, vamos assumir essa porta `1234`, mas saiba que você pode escolher aquela que lhe é conveniente.

## 5. Acesse o Jupyter remotamente

Após todo o procedimento, basta acessar o Jupyter de um navegador de sua preferência pelo endereço:

```
http://localhost:8888/tree
```

## 6. Feche as conexões

Após terminar o trabalho, você pode fechar o tunel matando o processo referente à ele. Para fazer isso, rode o comando:

```bash
netstat -lpn | grep :8888
```

para acessar o ID do processo (PID). LEmbrando que `8888` foi a porta local que escolhemos. Atente-se caso tenha utilizado outra. O resultado deve ser algo como a figura abaixo onde o PID está em evidência.

![Minha imagem](https://raw.githubusercontent.com/emdemor/emdemor.github.io/main/assets/images/blog/2021-12-11-como-acessar-jupyter-remoto/getpid.png)

Com o PID em mãos, rode:

```bash
kill 17362
```

onde 17362 é o PID do exemplo em questão.

## Leia Também

https://ljvmiranda921.github.io/notebook/2018/01/31/running-a-jupyter-notebook/

https://docs.anaconda.com/anaconda/user-guide/tasks/remote-jupyter-notebook/
