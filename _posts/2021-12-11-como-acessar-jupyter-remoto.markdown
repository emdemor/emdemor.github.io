---
title: "How to access the Jupyter from a remote server"
layout: post
date: 2021-12-11 22:48
image: /assets/images/blog/2021-12-11-como-acessar-jupyter-remoto/banner.png
headerImage: true
tag:
    - jupyter
    - remote host
    - ssh
    - tunel
category: blog
author: emdemor
description: Como acessar o Jupyter a partir de um servidor remoto
---

Since I started college back in 2011, I've rarely had a full day available for home office work. As my work has always involved programming, desktop computers never made sense to me as they would only keep me active for part of the day. Since then, I have always had a laptop in my hands. However, due to the possibility of working at home office full time during the pandemic, I decided to invest some money in a desktop. I really enjoyed it but, sometimes I miss the flexibility that working on laptops gives us. This has kept me using my old Yoga 520 until now.

For small projects it is still good and works very well. However, in more complex Machine Learning projects, where I need to use my GPU, or I need a few dozen RAM to perform database processing, the old friend can't take it. In those cases, I go to the desktop. This turned out to be quite problematic for me as my office is a bit far from home and I need to stay home as long as possible now that my daughter is born. **Solution**? Remotely access the desktop from the laptop.

Right away, I should point out that there are several ways to do this, each one being better suited to a usage profile. In my case, when I need to use a graphical interface, [TeamViewer](https://www.teamviewer.com/pt-br/) works very well. That is not the case here. I need to access Jupyter launched on the remote desktop from a local browser in the laptop. In this tutorial, I'm assuming the following:

-   Both the laptop and the desktop host run linux systems
-   The server already has Jupyter installed with the path to its binary in the PATH variable. (_Ie typing `jupyter notebook` in the terminal, Jupyter starts._)

Let`s go

## 1. Find desktop IP and username

To do this, physically access the desktop, open the terminal and run:

```bash
hostname -I | awk '{print $1}'
```

The result should be a 9-character numeric code, with the following form:

`XXX.XXX.X.XX`

which usually starts with 192.168. Save the IP.

You will also need your host username and password. In case you don't know, just run the command

```bash
whoami
```

Keep this information too.

## 2. Remote desktop access

The second step is to remotely access the desktop with ssh. The procedure is very well described in this [alura article](https://www.alura.com.br/artigos/como-acessar-servidores-remotamente-com-ssh), written by Yuri Matheus. Basically, suppose the IP is 192.168.0.00 and the user "host_user" runs the command:

```bash
# Substitua "host_user" e "192.168.0.00" pelas suas informações
ssh host_user@192.168.0.00
```

After the command, if everything goes well, you will see at the beginning of your terminal line the information:

```bash
host_user@host_name:~$
```

## 3. Link the port on the remote server to a local port

We need to connect the remote port with a local port in order to be able to access Jupyter. To make this you can set up an SSH tunnel. Let's assume you have chosen local port `8888` and remote port `1234`. The command will be:

```bash
ssh -L 8888:localhost:1234 host_user@192.168.0.00
```

After that, what the server's Jupyter streams on remote port `1234` will be accessible on local port `8888`.

> **Warning**: it should be clear that these ports were chosen for example purposes, and it is up to you to choose those of greatest convenience. Particularly, I use `8888` for both local and remote port. However, it would be quite confusing to use these values ​​here!

## 4. Start Jupyter

Okay. Now, on the server, we need to run Jupyter on the specified port. Inside the server, if we run the command:

```bash
jupyter notebook --no-browser
```

we will open Jupyter on the server. The optional `no-browser` argument prevents a tab from being opened in the server browser with a Jupyter session. However, when we do this, Jupyter will start on an available port, usually `8888`.

![Porta8888](https://raw.githubusercontent.com/emdemor/emdemor.github.io/main/assets/images/blog/2021-12-11-como-acessar-jupyter-remoto/porta8888.png)

However, we need to specify the port we configured in the tunnel. In this case, it's `1234` run the command:

```bash
jupyter notebook --no-browser --port=1234
```

Look at the difference:

![Porta1234](https://raw.githubusercontent.com/emdemor/emdemor.github.io/main/assets/images/blog/2021-12-11-como-acessar-jupyter-remoto/port1234.png)

In this tutorial, we'll assume this `1234` port, but be aware that you can choose the one that suits you.

## 5. Access Jupyter remotely

After all the procedure, just access Jupyter from a browser of your choice at the address:

```
http://localhost:8888/tree
```

## 6. Feche as conexões

After finishing the job, you can close the tunnel by killing the process related to it. To do this, run the command:

```bash
netstat -lpn | grep :8888
```

to access the process ID (PID). Remembering that `8888` was the local port we chose. Pay attention if you have used another one. The result should look something like the figure below where the PID is in evidence.

![PID](https://raw.githubusercontent.com/emdemor/emdemor.github.io/main/assets/images/blog/2021-12-11-como-acessar-jupyter-remoto/getpid.png)

With the PID in hand, run:

```bash
kill 17362
```

where 17362 is the PID of the example.

---

## Read too

L. J. Miranda [Running a Jupyter notebook from a remote server](https://ljvmiranda921.github.io/notebook/2018/01/31/running-a-jupyter-notebook/)

Anaconda Docs [Running Jupyter Notebook on a remote server](https://docs.anaconda.com/anaconda/user-guide/tasks/remote-jupyter-notebook/)
