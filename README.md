# 7 Days Of Code - Python Pandas

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)

![Badge code size](https://img.shields.io/github/languages/code-size/fab-souza/7DaysOfCode-Python_Pandas)

| :placard: Vitrine.Dev |    |
| -------------  | --- |
| :sparkles: Nome        | **7 Days Of Code - Python Pandas**
| :label: Tecnologias | python
| :rocket: URL         | 
| :fire: Desafio     | [7 Days of Code - Python Pandas](https://7daysofcode.io/matricula/pandas)

![](https://user-images.githubusercontent.com/67301805/235231091-305c5353-564d-433b-a68b-e0bb2133546b.jpg#vitrinedev)

## Sobre o desafio 📚




## Minha prática 👩🏻‍💻

### Desafio 1: Importação dos dados

![01](https://user-images.githubusercontent.com/67301805/236515552-328963ef-a7ac-4239-8f8e-6ae3e68512f7.jpg)

- Unificar todos os dados dos empréstimos em um Dataset 

![image](https://user-images.githubusercontent.com/67301805/236516899-b6f8c069-3565-4fab-8f46-dd1128d36998.png)


- Mesclar com os dados do acervo

Para fazer união dos dois *dataset*, fiz alguns testes antes com os dados de 2020. Originalmente, ele possui 26.561 registros. Ao fazer a união através do *inner*, fiquei com 25.610 registros, quase 1.000 a menos.

Com a união através do *left*, o dataset ficou com 26.636 linhas, criando alguns dados.

Já através do *right*, o dataset passou 549.000 registros.

Diante o resultado destes testes, achei melhor fazer a união através do *inner* e perder alguns registros, do que acabar criando dados.

![image](https://user-images.githubusercontent.com/67301805/236517323-d0e171a2-dc27-439d-9463-2e41d0efeb44.png)

- Fazer a limpeza

A limpeza básica, refere-se a retirada de dados nulos e duplicados. Eu decidi manter os empréstimos que não foram devolvidos, porque futuramente eles podem sinalizar quais são os tipos de livros que estão mais propensos a não serem devolvidos. Já em relação aos dados duplicados, pensei em verificar se haviam dados repetidos no *id_emprestimo*, porque achei que cada empréstimo fosse único e se ele aparecesse mais de uma vez, seria um erro de registro, sistema, etc. 

Mas eu recordei da minha época de faculdade, em que peguei emprestado mais de um livro de uma vez. Por exemplo, no mesmo dia que precisava do livro de Cálculo I, eu também tinha que ler sobre circuitos elétricos e acabava pegando mais de um livro. 

No caso da instituição em que me graduei, cada aluno poderia pegar emprestado no máximo 3 livros de uma vez. Se precisasse retirar mais livros, tínhamos que devolver 1 dos 3 para pegar o outro, ou pedir para alguém fazer o empréstimo por você. Ou seja, quando retirava mais de um livro da biblioteca, ambos estariam registrados sob o mesmo *id_emprestimo*.

Porém, ao contar as aparições dos *ids*, vi que há empréstimos que aparecem mais do que 4 vezes: 

![image](https://user-images.githubusercontent.com/67301805/236517624-f902f0eb-9d3a-444d-b748-62e4e239c1bc.png)

Sem contar que achei muito estranho uma biblioteca permitir a retirada de 7 livros de uma só vez… 🤔

Portanto, vou supor que a biblioteca da UFRN também permite a retirada, de no máximo, 3 livros por empréstimo para cada aluno.

Diante o resultado da contagem, também fui verificar a variável *data_emprestimo* e ver quantas vezes cada data aparece.

![image](https://user-images.githubusercontent.com/67301805/236517804-5b6f18a5-8906-45cd-9dd3-df5fe749dc74.png)

Estranhamente, também temos datas que aparecem 7 vezes no dataset.  

Para tirar minha dúvida se realmente houve erro no sistema e um registro acabou sendo duplicado, fiz uma *query* selecionando um dos *ids* repetidos:

![image](https://user-images.githubusercontent.com/67301805/236517917-c8cdd10e-2c3c-474a-b8cd-9c1c0f10bc67.png)

E de fato, eles se tratam de um erro, pois todos os registros referem-se à retirada do mesmo livro. Fiz o mesmo para o próximo *id* e houve o mesmo erro que aconteceu com o *id* anterior, nos 3 *ids* seguintes, retiraram mais de um livro de uma só vez, mas ocorreu a duplicação do registro.
Diante estes erros, fiz um *drop_duplicate()*



### Desafio 2: Limpeza dos dados

![02](https://user-images.githubusercontent.com/67301805/236515560-9d6f3444-ed20-4ad7-a664-a88fdb9d4bd5.jpg)




### Desafio 3: Análise exploratória de dados e DateTime

![03](https://user-images.githubusercontent.com/67301805/236515558-983fef13-2c22-4a7a-92f4-a3ac7b7214ac.jpg)





### Desafio 4: Análise exploratória de dados e Variáveis

![04](https://user-images.githubusercontent.com/67301805/236515565-75209607-ed32-4899-a2e8-7ce7863965ca.jpg)


### Desafio 5: Análise exploratória de dados e Boxplot

![05](https://user-images.githubusercontent.com/67301805/236515568-af3baf59-6b27-4095-8403-f1a09c762bd6.jpg)


### Desafio 6: JSON, Excel e Pivot_table

![06](https://user-images.githubusercontent.com/67301805/236515569-49c276c0-6db8-4681-b67b-50c608fffd65.jpg)

### Desafio 7: Customização de tabelas

![07](https://user-images.githubusercontent.com/67301805/236515573-e132a360-850a-4e67-ae96-a0f5c420ab9c.jpg)







## Ferramentas utilizadas 🧰
<p> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> 
    <a href="https://pandas.pydata.org/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/2ae2a900d2f041da66e950e4d48052658d850630/icons/pandas/pandas-original.svg" alt="pandas" width="40" height="40"/> </a>
    <a href="https://seaborn.pydata.org/" target="_blank" rel="noreferrer"> <img src="https://seaborn.pydata.org/_images/logo-mark-lightbg.svg" alt="seaborn" width="40" height="40"/> </a>
    </p>
