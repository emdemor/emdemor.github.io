---
title: "PC Estate Price Prediction API"
layout: post
date: 2021-06-13 22:10
tag: jekyll
image: #https://raw.githubusercontent.com/emdemor/emdemor.github.io/main/assets/images/pc.jpg
headerImage: false
projects: true
hidden: true # don't count this post in blog pagination
description: "This is an API for prediction of prices in Poços de Caldas, MG, Brazil"
category: project
author: emdemor
externalLink: false
---

<!-- ![Screenshot](https://raw.githubusercontent.com/sergiokopplin/indigo/gh-pages/assets/screen-shot.png) -->

# API Reference

The PC Estate Price Prediction API is organized around REST. It is an aplication for prediction of estate prices in Poços de Caldas, a city from Brazil.

The basic url is:

[https://estate-predict-pc.herokuapp.com/api/predictor](https://estate-predict-pc.herokuapp.com/api/predictor)

The parameters need to predict are:
* **type**, (*string*): the type of the estate. Can be `APARTMENT`, `HOME`, `CONDOMINIUM` or `RESIDENTIAL_ALLOTMENT_LAND`

* **area**, (*real*): in the case of `APARTMENT`, `HOME` and `CONDOMINIUM` types, i is the contructed area. On the other hanf, if the type is `RESIDENTIAL_ALLOTMENT_LAND`, it will be the allotment area.

* **n_bathrooms**, (*integer*): number of bathrooms.

* **n_bedrooms**, (*integer*): number of bedrooms.

* **n_suites**, (*integer*): how many of the bedrooms are suites.

* **n_parking_spaces**, (*integer*): number of parking spaces.

* **neighborhood**, (*string*): the estate neighborhood.

For more accurated results, you can pass to the optional features:

* **iptu**, (*integer*): annual estate tax.

* **condo_fee**, (*real*): monthly condominum fee.

* **units_on_floor**, (*integer*): number of units on the floor (for appartments).

* **n_floors**, (*integer*): number of fllors in the builfing (for appartments).
'
* **resale**, (*integer*): it must be 0 if the estate is new. In the other hand, it must be 1.

* **buildings**, (*integer*): number of buildings in the estate.

---

## List of Valid Neighborhoods
We can see in the box below a list with the neighborhoods of Poços de Caldas:

<div style="height:120px;width:100%;border:1px solid #ccc; overflow:auto;">
<ul>
<li>Aparecida</li>
<li>Area Rural de Pocos de Caldas</li>
<li>Augusto de Almeida</li>
<li>Bela Vista</li>
<li>Bem Bastos</li>
<li>Bianucci</li>
<li>Boa Esperanca</li>
<li>Boa Esperança</li>
<li>Boa Esperanca II</li>
<li>Bortolan</li>
<li>Bortolan Norte I</li>
<li>Caio Junqueira</li>
<li>Campo da Mogiana</li>
<li>Campo do Retirinho</li>
<li>Campos Elíseos</li>
<li>Cascatinha</li>
<li>Castanheiras</li>
<li>Centro</li>
<li>Chácara Alvorada</li>
<li>Chacara dos Cravos</li>
<li>Chácara dos Cravos</li>
<li>Chacara Rancho Azul</li>
<li>Condominio Pitangueiras</li>
<li>Conjunto Habitacional Eng. Pedro Afonso Junqueira</li>
<li>Conjunto Habitacional Pedro Afonso Junqueira</li>
<li>Country Club</li>
<li>Da Saude</li>
<li>Dom Bosco</li>
<li>Dom Bosco I, II, III</li>
<li>Dos Funcionários</li>
<li>Estancia Pocos de Caldas</li>
<li>Estância Poços de Caldas</li>
<li>Estância São José</li>
<li>Funcionarios</li>
<li>Funcionários</li>
<li>Gama Cruz</li>
<li>Gato Preto</li>
<li>Jardim Aeroporto</li>
<li>Jardim Amaryllis</li>
<li>Jardim America</li>
<li>Jardim América</li>
<li>Jardim Bandeirantes</li>
<li>Jardim Bela Vista</li>
<li>Jardim Brasil</li>
<li>Jardim Campos Elísios</li>
<li>Jardim Carolina</li>
<li>Jardim Cascatinha</li>
<li>Jardim Centenario</li>
<li>Jardim Centenário</li>
<li>Jardim Country Club</li>
<li>Jardim Daniele</li>
<li>Jardim Das Acácias</li>
<li>Jardim das Amaryllis</li>
<li>Jardim das Azáleas</li>
<li>Jardim Das Azaléias</li>
<li>Jardim Das Hortênsias</li>
<li>Jardim das Hortênsias</li>
<li>Jardim Del Rey</li>
<li>Jardim do Contorno</li>
<li>Jardim do Ginasio</li>
<li>Jardim dos Estados</li>
<li>Jardim dos Manacas</li>
<li>Jardim dos Manacás</li>
<li>Jardim Doutor Ottoni</li>
<li>Jardim Elvira Dias</li>
<li>Jardim Esmeralda</li>
<li>Jardim Esperança</li>
<li>Jardim Europa</li>
<li>Jardim Filipino</li>
<li>Jardim Formosa</li>
<li>Jardim Ginásio</li>
<li>Jardim Ipê</li>
<li>Jardim Itamaraty I</li>
<li>Jardim Itamaraty I, II, III, IV e V</li>
<li>Jardim Itamaraty II</li>
<li>Jardim Itamaraty III</li>
<li>Jardim Itamaraty V</li>
<li>Jardim Kennedy</li>
<li>Jardim Kennedy I e II</li>
<li>Jardim Monte Almo</li>
<li>Jardim Nova Aparecida</li>
<li>Jardim Novo Mundo</li>
<li>Jardim Ottoni</li>
<li>Jardim Paraíso</li>
<li>Jardim Philadelphia</li>
<li>Jardim Philadélphia</li>
<li>Jardim Philadelphia II</li>
<li>Jardim Planalto</li>
<li>Jardim Quisisana</li>
<li>Jardim Regina</li>
<li>Jardim Santa Augusta</li>
<li>Jardim Santa Lúcia</li>
<li>Jardim Santa Margarida</li>
<li>Jardim Santa Rita</li>
<li>Jardim Santa Rosalia</li>
<li>Jardim São Bento</li>
<li>Jardim Sao Jorge</li>
<li>Jardim São Paulo</li>
<li>Jardim Vitoria</li>
<li>Jardim Vitória</li>
<li>Jardim Vitoria Iv</li>
<li>Jardim Vitoria V</li>
<li>João Pinheiro</li>
<li>José Carlos</li>
<li>Loteamento Caldense</li>
<li>Loteamento Jardim Nova Europa</li>
<li>Loteamento Nova Primavera</li>
<li>Loteamento Residencial Santa Clara II</li>
<li>Loteamento Vila Flora II</li>
<li>Marçal Santos</li>
<li>Marçal Santos </li>
<li>Marco Divisório</li>
<li>Monte Almo</li>
<li>Monte Verde</li>
<li>Morada das Flores</li>
<li>Morada Dos Pássaros</li>
<li>Morada dos Pássaros</li>
<li>Nossa Senhora Aparecida</li>
<li>Nossa Senhora da Saúde</li>
<li>Nova Aparecida</li>
<li>Nova Aurora</li>
<li>Panorama</li>
<li>Parque das Nações</li>
<li>Parque Manuel Marques</li>
<li>Parque Nova Aurora</li>
<li>Parque Pinheiros</li>
<li>Parque Primavera</li>
<li>Parque San Carlo</li>
<li>Parque São Sebastião </li>
<li>Parque Véu das Noivas</li>
<li>Ponte Coberta</li>
<li>Ponte Preta</li>
<li>Pqe Nações</li>
<li>Residencial Greenville</li>
<li>Residencial Mantiqueira</li>
<li>Residencial Morumbi</li>
<li>Residencial Paineiras</li>
<li>Residencial Pitangueiras</li>
<li>Residencial Portal do Sol</li>
<li>Residencial Santa Clara</li>
<li>Residencial São Bernardo</li>
<li>Residencial Summer Ville</li>
<li>Residencial Torre</li>
<li>Residencial Veredas</li>
<li>Santa Angela</li>
<li>Santa Ângela</li>
<li>Santa Angela IV</li>
<li>Santa Augusta</li>
<li>Santa Emilia</li>
<li>Santa Emília</li>
<li>Santa Helena</li>
<li>Santa Lucia</li>
<li>Santa Lúcia</li>
<li>Santa Margarida</li>
<li>Santa Maria</li>
<li>Santa Rosália</li>
<li>Santa Teresa</li>
<li>Santana</li>
<li>Santana do Pedregal</li>
<li>Santo André</li>
<li>São Benedito</li>
<li>São Geraldo</li>
<li>São João</li>
<li>São Jorge</li>
<li>São José</li>
<li>São Sebastião</li>
<li>Vale das Antas</li>
<li>Vila Bela</li>
<li>Vila Cruz</li>
<li>Vila Fátima</li>
<li>Vila Flora</li>
<li>Vila Guaporé</li>
<li>Vila Iguatimara</li>
<li>Vila Iguatimara e Fatima</li>
<li>Vila Jose Carlos</li>
<li>Vila Líder</li>
<li>Vila Matilde</li>
<li>Vila Menezes</li>
<li>Vila Miglioranzi</li>
<li>Vila Nossa Senhora de Fatima</li>
<li>Vila Nova</li>
<li>Vila Olímpica</li>
<li>Vila Rica</li>
<li>Vila Togni</li>
<li>Vila Verde</li>
<li>Village São Luís</li>
<li>Village São Luiz</li>
</ul>
</div>

---

## Example of Usage in Python
``` python
import requests
url = "https://estate-predict-pc.herokuapp.com/api/predictor"
headers = {'Content-type': 'application/json', 'Accept': 'text/plain'}
params = {
    "area": 170,
    "n_bathrooms": 2,
    "n_bedrooms": 3,
    "n_parking_spaces": 2,
    "n_suites": 0,
    "neighborhood": "Jardim Europa",
    "type": "HOME"
}
r = requests.post(url, data=json.dumps(params), headers=headers)
r.json()
```
