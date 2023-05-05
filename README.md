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

- Atribuir CDU

Ao invés de fazer o mapeamento do CDU através de uma lógica condicional, eu preferi utilizar a função *pd.cut()*, que aprendi no 1º curso de estatística da Alura. A diferença é que precisei definir, previamente, os *bins* e *labels* antes de utilizar a função. Os *bins* são os valores na lista *cdu* que limitam os valores para os *labels*, que são as áreas de conhecimento.

Para ter certeza que a classificação foi feita corretamente, fiz um *query()* selecionando alguns valores:

![image](https://user-images.githubusercontent.com/67301805/236519212-70ef2d2f-1329-4f3e-9fc2-683e78e921ba.png)

- Excluir coluna

Segundo o Desafio, não iria precisar da coluna *registro_sistema* em nenhum momento, por isso era melhor excluí-la.

![image](https://user-images.githubusercontent.com/67301805/236519367-5de074db-2c76-4383-8c7e-eca4c9e690e4.png)

- Mudar tipo de variável

Eu já havia realizado um pequeno tratamento nos dados, no dia anterior. Por exemplo além de mudar a variável *matricula_ou_siape* para o tipo *string*, eu também passei as variáveis referentes a datas para o tipo *datetime*, pois imaginei que, em algum momento, teria que fazer alguma análise referente ao tempo.



### Desafio 3: Análise exploratória de dados e DateTime

![03](https://user-images.githubusercontent.com/67301805/236515558-983fef13-2c22-4a7a-92f4-a3ac7b7214ac.jpg)

- Analisar os empréstimos

    - A quantidade que ocorreu no período:
    
        Para ver quantos empréstimos ocorreram, fiz um *value_counts()* dos *id_emprestimo*. Sei que seu principal objetivo é apresentar quantas vezes os itens aparecem ao longo do dataset, porém, ao final, ele também mostra o total de valores únicos.
        
        ![len](https://user-images.githubusercontent.com/67301805/236521550-5fdafa15-4ddf-46df-9912-2e26c1bc1038.jpg)

        Entretanto, um ponto chamou minha atenção. Ao analisar o *id* que mais apareceu, no começo, imaginei que a regra de empréstimo desta biblioteca fosse diferente da instituição em que estudei, porque pensei que um aluno pegou 6 livros de uma só vez. 

        ![id](https://user-images.githubusercontent.com/67301805/236521214-af36e87d-4fca-4a2b-80b5-d8f83c2a2f13.jpg)

        Depois, pensei que tivesse ocorrido um erro no sistema, porque o *id dos exemplares* se repetiam. Ou seja, o aluno retirou 3 livros, só que, por algum motivo, o sistema acabou duplicando o empréstimo.

        ![rep](https://user-images.githubusercontent.com/67301805/236521833-332e4297-e48e-45ab-b04d-1c729bdaf349.jpg)

        No entanto, as datas do empréstimo são diferentes, apenas o ano, para ser mais exata. Há um intervalo de 1 ano entre a data dos empréstimos e devolução, por isso estes registros não foram excluídos quando fiz a retirada de dados duplicados. 

        ![data](https://user-images.githubusercontent.com/67301805/236522335-78cb88ed-6ddc-40d1-8949-8c26f611be8e.jpg)

        Achei estranho ter dois empréstimos, feitos em anos diferentes, terem o mesmo *ID*. Se eu estivesse trabalhando (de forma remunerada) e me deparasse com uma situação como esta, eu definitivamente, pediria ajuda/concelho para os demais membros da equipe, porque acredito que a repetição de *ID dos empréstimos* seja algo que não devesse ocorrer.

        Voltando à análise da quantidade de empréstimos que foram feitos, há uma outra forma de obter este valor. Para ver os itens único presentes em uma variável, eu uso o *.unique()*, que devolve um *array* com este valores. Ao aplicar a função *len()* no *array*, ela me devolve o número de itens, que no caso é de 1955945 empréstimos.

    - Exemplar mais emprestado:
    
        Neste caso, utilizei o *value_counts()* na variável *código de barra*. Ao fazer um *query()* dos três primeiros itens, vi que o segundo exemplar mais emprestado é sobre Ciências Sociais, enquanto o primeiro e terceiro mais emprestado são de Ciências Aplicadas.

        ![image](https://user-images.githubusercontent.com/67301805/236522989-07fd4290-9065-4838-9769-c132d895a367.png)
        ![image](https://user-images.githubusercontent.com/67301805/236523094-4d2794aa-e023-4e38-84af-d35faa771949.png)

- Verificar os empréstimos ao longo do tempo (gráfico de linha)

As datas no *dataset* são compostas pelo dia e hora do empréstimo e antes de fazer a análise, precisei separar estas duas informações. Segundo a interpretação que tive do Desafio, eu teria que fazer o somatório de quantos empréstimos que ocorreram no dia, antes de plotar o gráfico.

Então, peguei a variável *data_emprestimo* e fiquei apenas com os dias, ao usar o *dt.date*

![image](https://user-images.githubusercontent.com/67301805/236523293-2f085d0f-aba5-4ccd-966e-41d0c989423f.png)

Para saber quantas vezes aquela data aparece, fiz um *value_counts()* em cima do resultado anterior.

![image](https://user-images.githubusercontent.com/67301805/236523410-629da477-7bcc-4b88-ba49-47bb0d0fff1d.png)

Para ter uma ideia inicial de como estavam os empréstimos, fiz um gráfico com o *Matplotlib*:

![image](https://user-images.githubusercontent.com/67301805/236523514-b3acbe96-bbaa-4702-bd7d-cc4e370b3b75.png)

Para conseguir plotar um gráfico mais elaborado, peguei o resultado anterior e transformei em um *DataFrame* para facilitar o plot do gráfico com o *Seaborn*.

![image](https://user-images.githubusercontent.com/67301805/236523682-35f00235-0dbf-45a2-9563-b6066b92ed71.png)

Neste gráfico é possível observar melhor que nos períodos de férias (janeiro, julho e dezembro) a quantidade de empréstimo é menor, enquanto houve uma maior busca pelos livros um pouco depois das férias.

- Verificar os empréstimos ao longo dos anos

Para saber como os empréstimos estão distribuídos ao longo dos anos, peguei a variável *data_empréstimo*, apliquei o *dt.year*, para que ele me devolvesse apenas os anos das datas de empréstimo, e transformei o resultado em um DataFrame. Nele, é possível observar que o ano de 2020 teve a melhor quantidade de empréstimo, mas devo ressaltar que quando fiz a importação dos dados, só tive acesso ao começo daquele ano. Sem contar que, foi um período de pandemia, isolamento social e, provavelmente, sem acesso à biblioteca. Os anos que tiveram mais empréstimos foram 2013, 2012 e 2014, respectivamente, e plotei um gráfico para facilitar a visualização.

![image](https://user-images.githubusercontent.com/67301805/236523935-37a238ba-dddb-4b32-9b3d-86ec424de654.png)

O grande volume de empréstimo pode ter ocorrido por alguns motivos:

   - a instituição começou a oferecer mais cursos, ou ampliou a quantidade de salas/alunos por curso, que acabou ampliando o número de pessoas atendidas pela biblioteca;
   - ampliação do acervo, permitindo que mais alunos efetuassem o empréstimo.

Em 2015 e 2016, houve uma redução pela procura dos livros, que voltou a aumentar um pouco em 2017, mas não houve melhora nos anos seguintes. A redução no volume de empréstimos pode ser um reflexo de como estava a economia do país naquela época, por exemplo, em 2015 eu estava estudando em uma instituição pública, que passou por greves naquele ano, que bagunçou a grade curricular até 2016. Isso desestimulou alunos, que acabaram trancando a faculdade. Sem contar os casos em que o aluno parou de estudar, porque a situação financeira não estava favorável. 

Outro ponto que pode ter contribuído para a redução, é a maior circulação de material digital (não oficial) entre os alunos. 

- Qual mês possui menor número de empréstimo? Os meses mais movimentados da biblioteca são em março e setembro?

Para saber como os empréstimos estão distribuídos ao longo dos meses, fiz algo semelhante ao que já tinha feito, porém mudei apenas o final do *.dt* para *.dt.month*. Também transformei em um *DataFrame* e plotei um gráfico.

![image](https://user-images.githubusercontent.com/67301805/236524225-9662f8c4-d38f-4c3d-b5a1-219bc3ddd210.png)

E de fato, os meses com menor procura são durante as férias de verão e inverno, janeiro-dezembro e junho-julho, respectivamente. Já os meses com maior procura são março e agosto, diferente da suspeita interna, setembro não é um dos 2 meses com maior procura.

- Qual horário possui maior movimento?

Para finalizar com a distribuição ao longo das horas, mudei o *.dt* para *.dt.hour*, transformei o resultado em um *DataFrame* e plotei o gráfico.

![image](https://user-images.githubusercontent.com/67301805/236524390-79fb5b23-4ad4-4d2e-9be4-87b6300cd898.png)

Na parte da manhã, 10 e 11 horas possuem o maior movimento, na parte da tarde das 16 às 18 horas há um grande movimento na biblioteca, enquanto na parte da noite às 20 horas é o horário mais movimentado. Em contrapartida, os horários com menor movimento são às 6, às 22, 23 e à meia-noite. 

Diante estes números, eu suspenderia o atendimento ao usuário às 6 da manhã, às 23h e a meia-noite, porque de 2010 até 2020 (mesmo que parcial) estes 3 horários tiveram um total de 82 empréstimos, que quando comparados com os mais de 2 milhões de registros que estamos analisando, não chega a atingir 0,01% do total. Ou seja, são os melhores horários para se dedicar a outras atividades. Enquanto às 10 e 11h da manhã e das 16 às 19h, o ideal seria focar no atendimento ao público.



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
