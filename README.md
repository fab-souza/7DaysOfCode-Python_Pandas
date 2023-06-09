# 7 Days Of Code - Python Pandas

![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=FINALIZADO&color=GREEN&style=for-the-badge)

![Badge code size](https://img.shields.io/github/languages/code-size/fab-souza/7DaysOfCode-Python_Pandas)

| :placard: Vitrine.Dev |    |
| -------------  | --- |
| :sparkles: Nome        | **7 Days Of Code - Python Pandas**
| :label: Tecnologias | python
| :rocket: URL         | 
| :fire: Desafio     | [7 Days of Code - Python Pandas](https://7daysofcode.io/matricula/pandas)

![](https://user-images.githubusercontent.com/67301805/235231091-305c5353-564d-433b-a68b-e0bb2133546b.jpg#vitrinedev)

## Sobre o desafio 📚

Para quem não sabe, a [Alura](https://www.alura.com.br/) criou o #7DaysOfCode para as pessoas exercitarem seus conhecimentos em programação, ao oferecer sete desafios em diversas áreas. 

Este desafio sobre Python Pandas foi criado pelo [Francisco Foz](https://br.linkedin.com/in/francisco-tadeu-foz), cujo objetivo é explorar os dados de empréstimos dos acervos do sistema de bibliotecas da UFRN.


## Minha prática 👩🏻‍💻

### Desafio 1: Importação dos dados

![01](https://user-images.githubusercontent.com/67301805/236515552-328963ef-a7ac-4239-8f8e-6ae3e68512f7.jpg)

- Unificar todos os dados dos empréstimos em um Dataset ✅ 

![image](https://user-images.githubusercontent.com/67301805/236516899-b6f8c069-3565-4fab-8f46-dd1128d36998.png)


- Mesclar com os dados do acervo ✅

Para fazer união dos dois *dataset*, fiz alguns testes antes com os dados de 2020. Originalmente, ele possui 26.561 registros. Ao fazer a união através do *inner*, fiquei com 25.610 registros, quase 1.000 a menos.

Com a união através do *left*, o dataset ficou com 26.636 linhas, criando alguns dados.

Já através do *right*, o dataset passou 549.000 registros.

Diante o resultado destes testes, achei melhor fazer a união através do *inner* e perder alguns registros, do que acabar criando dados.

![image](https://user-images.githubusercontent.com/67301805/236517323-d0e171a2-dc27-439d-9463-2e41d0efeb44.png)

- Fazer a limpeza ✅

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

E de fato, eles se tratam de um erro, pois todos os registros referem-se à retirada do mesmo livro. Fiz o mesmo para o próximo *id* e houve o mesmo erro que aconteceu com o *id* anterior.

Diante estes erros, fiz um *drop_duplicate()*.

---

### Desafio 2: Limpeza dos dados

![02](https://user-images.githubusercontent.com/67301805/236515560-9d6f3444-ed20-4ad7-a664-a88fdb9d4bd5.jpg)

- Atribuir CDU ✅

Ao invés de fazer o mapeamento do CDU através de uma lógica condicional, eu preferi utilizar a função *pd.cut()*, que aprendi no 1º curso de estatística da Alura. A diferença é que precisei definir, previamente, os *bins* e *labels* antes de utilizar a função. Os *bins* são os valores na lista *cdu* que limitam os valores para os *labels*, que são as áreas de conhecimento.

![CDU](https://user-images.githubusercontent.com/67301805/236575170-3aa6f0a1-aebe-41a4-a378-62d55c65ead9.png)

Para ter certeza que a classificação foi feita corretamente, fiz um *query()* selecionando alguns valores:

![image](https://user-images.githubusercontent.com/67301805/236575345-8c37713f-5a61-48fa-8e8e-eab5514b672a.png)

- Excluir coluna ✅

Segundo o Desafio, não iria precisar da coluna *registro_sistema* em nenhum momento, por isso era melhor excluí-la.

![image](https://user-images.githubusercontent.com/67301805/236519367-5de074db-2c76-4383-8c7e-eca4c9e690e4.png)

- Mudar tipo de variável ✅

Eu já havia realizado um pequeno tratamento nos dados, no dia anterior. Por exemplo além de mudar a variável *matricula_ou_siape* para o tipo *string*, eu também passei as variáveis referentes a datas para o tipo *datetime*, pois imaginei que, em algum momento, teria que fazer alguma análise referente ao tempo.

---

### Desafio 3: Análise exploratória de dados e DateTime

![03](https://user-images.githubusercontent.com/67301805/236515558-983fef13-2c22-4a7a-92f4-a3ac7b7214ac.jpg)

- Analisar os empréstimos ✅

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

        Voltando à análise da quantidade de empréstimos que foram feitos, há uma outra forma de obter este valor. Para ver os itens únicos presentes em uma variável, eu uso o *.unique()*, que devolve um *array* com este valores. Ao aplicar a função *len()* no *array*, ela me devolve o número de itens, que no caso é de 1955945 empréstimos.

    - Exemplar mais emprestado:
    
        Neste caso, utilizei o *value_counts()* na variável *código de barra*. Ao fazer um *query()* dos três primeiros itens, vi que o segundo exemplar mais emprestado é sobre Ciências Sociais, enquanto o primeiro e terceiro mais emprestado são de Ciências Aplicadas.

        ![image](https://user-images.githubusercontent.com/67301805/236522989-07fd4290-9065-4838-9769-c132d895a367.png)
        ![image](https://user-images.githubusercontent.com/67301805/236523094-4d2794aa-e023-4e38-84af-d35faa771949.png)

- Verificar os empréstimos ao longo do tempo ✅

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

- Verificar os empréstimos ao longo dos anos ✅

Para saber como os empréstimos estão distribuídos ao longo dos anos, peguei a variável *data_empréstimo*, apliquei o *dt.year*, para que ele me devolvesse apenas os anos das datas de empréstimo, e transformei o resultado em um DataFrame. Nele, é possível observar que o ano de 2020 teve a melhor quantidade de empréstimo, mas devo ressaltar que quando fiz a importação dos dados, só tive acesso ao começo daquele ano. Sem contar que, foi um período de pandemia, isolamento social e, provavelmente, sem acesso à biblioteca. Os anos que tiveram mais empréstimos foram 2013, 2012 e 2014, respectivamente, e plotei um gráfico para facilitar a visualização.

![image](https://user-images.githubusercontent.com/67301805/236523935-37a238ba-dddb-4b32-9b3d-86ec424de654.png)

O grande volume de empréstimo pode ter ocorrido por alguns motivos:

   - a instituição começou a oferecer mais cursos, ou ampliou a quantidade de salas/alunos por curso, que acabou ampliando o número de pessoas atendidas pela biblioteca;
   - ampliação do acervo, permitindo que mais alunos efetuassem o empréstimo.

Em 2015 e 2016, houve uma redução pela procura dos livros, que voltou a aumentar um pouco em 2017, mas não houve melhora nos anos seguintes. A redução no volume de empréstimos pode ser um reflexo de como estava a economia do país naquela época, por exemplo, em 2015 eu estava estudando em uma instituição pública, que passou por greves naquele ano, que bagunçou a grade curricular até 2016. Isso desestimulou alunos, que acabaram trancando a faculdade. Sem contar os casos em que o aluno parou de estudar, porque a situação financeira não estava favorável. 

Outro ponto que pode ter contribuído para a redução, é a maior circulação de material digital (não oficial) entre os alunos. 

- Qual mês possui menor número de empréstimo? Os meses mais movimentados da biblioteca são em março e setembro? ✅

Para saber como os empréstimos estão distribuídos ao longo dos meses, fiz algo semelhante ao que já tinha feito, porém mudei apenas o final do *.dt* para *.dt.month*. Também transformei em um *DataFrame* e plotei um gráfico.

![image](https://user-images.githubusercontent.com/67301805/236524225-9662f8c4-d38f-4c3d-b5a1-219bc3ddd210.png)

E de fato, os meses com menor procura são durante as férias de verão e inverno, janeiro-dezembro e junho-julho, respectivamente. Já os meses com maior procura são março e agosto, diferente da suspeita interna, setembro não é um dos 2 meses com maior procura.

- Qual horário possui maior movimento? ✅

Para finalizar com a distribuição ao longo das horas, mudei o *.dt* para *.dt.hour*, transformei o resultado em um *DataFrame* e plotei o gráfico.

![image](https://user-images.githubusercontent.com/67301805/236524390-79fb5b23-4ad4-4d2e-9be4-87b6300cd898.png)

Na parte da manhã, 10 e 11 horas possuem o maior movimento, na parte da tarde das 16 às 18 horas há um grande movimento na biblioteca, enquanto na parte da noite às 20 horas é o horário mais movimentado. Em contrapartida, os horários com menor movimento são às 6, às 22, 23 e à meia-noite. 

Diante estes números, eu suspenderia o atendimento ao usuário às 6 da manhã, às 23h e a meia-noite, porque de 2010 até 2020 (mesmo que parcial) estes 3 horários tiveram um total de 82 empréstimos, que quando comparados com os mais de 2 milhões de registros que estamos analisando, não chega a atingir 0,01% do total. Ou seja, são os melhores horários para se dedicar a outras atividades. Enquanto às 10 e 11h da manhã e das 16 às 19h, o ideal seria focar no atendimento ao público.

---

### Desafio 4: Análise exploratória de dados e Variáveis

![04](https://user-images.githubusercontent.com/67301805/236515565-75209607-ed32-4899-a2e8-7ce7863965ca.jpg)

- Tipo de vínculo ✅

Para saber os valores únicos e quantas vezes eles aparecem na variável, eu utilizei o *value_counts()*, que me devolveu uma *Series* mostrando que os alunos de graduação são os maiores consumidores das bibliotecas, seguidos pelos alunos de pós-graduação e docentes. O que faz total sentido, já que estamos analisando dados de uma universidade, ter pessoas que fazem parte do meio acadêmico como maiores consumidores é compreensível.

![image](https://user-images.githubusercontent.com/67301805/236525687-5a95d499-0a16-4c5e-aa0e-4b5bb48c4bd2.png)

Para facilitar a compreensão do tamanho que estes públicos ocupam, também fiz um *value_counts()* na forma de porcentagem. Alunos de graduação representam mais do que 75% dos usuários, alunos de pós-graduação são quase 15%, enquanto docentes são quase 3,5% do público atendido.

![image](https://user-images.githubusercontent.com/67301805/236525780-c0fb3e3e-ce06-4bea-81fb-dd75ad711bda.png)

Depois, uni as duas *Series* em um *Dataframe* através de uma função que criei.

![image](https://user-images.githubusercontent.com/67301805/236525924-468059d3-5447-4850-9c76-4c816b943d64.png)

O ponto que me chamou atenção, foi ver que servidores técnico/administrativo e alunos do ensino médio/técnico efetuam mais empréstimos do que docentes e usuários externos.  Investir nos públicos externos pode fazer com que eles frequentem mais as instalações da universidade e quem sabe, futuramente, retornem como estudantes de graduação, pós-graduação ou docentes. Ou seja, trazer a comunidade para a academia.

- Coleção ✅

Considerando que repetiria as mesmas etapas para analisar as demais variáveis categóricas, eu criei funções que me devolveriam as *Series* e tabela. No caso das *Coleções*, mais do que 99% dela é composta pelo *Acervo circulante*, mas o público também tem acesso a *Multimeios* (que podem ser partituras, VHS, CDs, DVDs, etc. Fonte: [UFU](https://bibliotecas.ufu.br/servicos/multimeios)), *Monografias*, *Dissertações* e demais publicações.

![image](https://user-images.githubusercontent.com/67301805/236526211-66b42903-adda-473b-8456-7bdf58a949bc.png)

Para entender como público consome as coleções disponíveis na biblioteca, fiz um *crosstab()* entre estas duas variáveis. Considerando o volume que o *Acervo circulante* representa, não é de se espantar que ela seja a mais consumida por todos os públicos da biblioteca.

![image](https://user-images.githubusercontent.com/67301805/236526306-9568261e-aee2-4348-9b55-79ce9a08626b.png)

- Biblioteca ✅

Já na variável *biblioteca*, temos 22 bibliotecas registradas, a que mais aparece é a *Biblioteca Central Zila Mamede*, representando mais do que 68% dos empréstimos, enquanto a *Biblioteca Setorial do Núcleo de Ensino Superior do Agreste* é a menor. Essa diferença pode ocorrer por motivos como:

    - A primeira biblioteca ser mais antiga e ter um acervo maior;
    
    - A biblioteca Central pode estar próxima a um campus que oferece mais cursos, enquanto a segunda atende alunos e docentes de alguns cursos;
    
    - A biblioteca do núcleo de Ensino pode ter uma localização mais afastada, enquanto a biblioteca Central ocupa um ponto com maior fluxo de pessoas.

![image](https://user-images.githubusercontent.com/67301805/236526490-47ca8c37-deb2-42ac-8ad3-7c0aaca39ec7.png)

Ao fazer um *crosstab* entre os usuários e as bibliotecas, com exceção da biblioteca Central Zila Mamede, ficou difícil identificar a distribuição do público. Por isso, também fiz um *crosstab* com as porcentagens. 

![image](https://user-images.githubusercontent.com/67301805/236527039-42c30129-7f2f-4ef3-a4c1-34a7734f72fa.png)

Nela ficou mais fácil identificar alguns pontos, por exemplo, os alunos de graduação, depois da biblioteca Central, que representa 55,07% do total de empréstimos, utilizam bastante as bibliotecas voltadas a Ciências da Saúde, a biblioteca Setorial do Centro Ciências da Saúde e a biblioteca Setorial da Faculdade de Ciências da Saúde do Trairi, representando 5,01% e 3,32% respectivamente. Estas porcentagem podem promover uma pesquisa mais aprofundada, ao buscar entender o que faz os alunos procurarem estes locais:

    - Melhores instalações?
    
    - Material mais atualizado/novo?
    
    - Acesso mais rápido/fácil?
    
    - Há cursos de medicina por perto?
    
Já para os alunos de pós-graduação, novamente, depois da biblioteca Central com seus 10,46%, há uma maior procura pela biblioteca Setorial do Centro de Ciências Humanas, Letras e Artes, seguida pela biblioteca Setorial Prof. Alberto Moreira Campos - Departamento de Odontologia, representando 0,92% e 0,65% respectivamente. Por se tratarem de 2 áreas distintas, as campanhas voltadas para este público podem ser divididas por áreas, por exemplo promover eventos de humanas, exatas ou biológicas nas datas comemorativas de cada uma.


- CDU ✅

Em relação ao CDU, vemos que as bibliotecas efetuaram mais empréstimos de materiais sobre *Ciências aplicadas*, seguida por *Ciências sociais* e depois por *Matemática e ciências naturais*, representando 68,78%, 17,83% e 3,32% respectivamente. 

![image](https://user-images.githubusercontent.com/67301805/236527184-960a1bb2-61c0-4efb-9725-aeb4c8515fc4.png)

Ao analisar o *crosstab* dos usuários com o CDU, é possível observar que estas três áreas são as mais procuradas pelos alunos de graduação, pós-graduação, médio/técnico, docentes e servidores. Enquanto os docentes externos buscam mais materiais de *Ciências sociais* do que *Ciências aplicadas* e com esta informação podemos levantar algumas hipóteses, por exemplo:

    - As bibliotecas da UFRN possuem materiais melhores do que as outras instituições;
    
    - Os docentes externos procuram a UFRN, porque elas têm um acesso mais fácil para eles, seja por questões ligadas à localização, acesso ou horário de atendimento.



---

### Desafio 5: Análise exploratória de dados e Boxplot

![05](https://user-images.githubusercontent.com/67301805/236515568-af3baf59-6b27-4095-8403-f1a09c762bd6.jpg)

- Analisar separadamente os alunos de graduação e pós-graduação ✅

Para fazer esta separação, utilizei um *query()* e criei um *DataFrame* para cada público.

- Verificar quais coleções possuem maior frequência de empréstimo nos dois públicos ✅

Eu já tinha feito uma rápida análise sobre isso no desafio anterior, quando fiz o *crosstab()* entre os usuários e as coleções. Neste caso, fiz um *value_counts()* das coleções em cada *dataset*. Vemos que em ambos os casos, os materiais que mais foram emprestados pertencem ao *Acervo circulante*.

![image](https://user-images.githubusercontent.com/67301805/236532904-9930d383-7ada-4a3f-8201-82a5e19dcb57.png)
![image](https://user-images.githubusercontent.com/67301805/236532995-b25d5593-fe53-453f-b391-010ce8d4a5a8.png)

- Verificar a distribuição dos empréstimos, mensais por ano, nos dois públicos ✅

Inicialmente, eu fiquei na dúvida sobre o que esta parte do desafio estava propondo. Eu havia entendido que deveria fazer um box-plot para cada, ou seja, os empréstimos estariam no eixo *y*, enquanto os meses estariam dispostos ao longo do eixo *x*. 

No terceiro desafio, manipulei as datas com o *dt.year* e *dt.month* para devolverem os anos e meses que os empréstimos ocorreram. Neste caso, utilizei estes atributos para criarem novas colunas no *dataset* de cada público, o *Ano* e *Mes*.

![image](https://user-images.githubusercontent.com/67301805/236533277-8400fe4f-24ca-4443-9328-f8ff0a5f35f7.png)

Lembrando que cada linha do *dataset* representa o empréstimo de um único livro, por isso fiz um *value_counts()* das duas colunas que acabei de criar e transformei o resultado em um *DataFrame*

![image](https://user-images.githubusercontent.com/67301805/236533508-06508d0c-6780-4c9d-9c21-beb4c127c7d8.png)

- Plotar um box-plot para cada ano nos dois públicos ✅

Na hora de fazer o *box-plot*, entendi que não daria certo fazer um para cada ano e que o correto seria colocar os **Anos** no eixo *x*.

![image](https://user-images.githubusercontent.com/67301805/236533618-9388de29-b537-4493-a785-462f8ceb7e19.png)

- O que ocorreu ao longo do tempo? ✅

No *box-plot* dos alunos de graduação, é possível identificar uma similaridade com o gráfico de linha feito no Desafio 3, já que estamos analisando o maior público, consumindo a maior categoria presente nas bibliotecas. Ou seja, até 2013 os empréstimos estavam em uma crescente. 2014 e 2015 foram anos de baixa, houve uma recuperação nos dois anos seguintes, até que em 2018 o volume de empréstimos teve nova queda.

![image](https://user-images.githubusercontent.com/67301805/236533777-705fa7f0-339a-4d92-a174-a4a9ef819b9a.png)

Já para os alunos de pós-graduação, temos um cenário que difere um pouco do público anterior. Há a crescente de 2010 até 2013, porém entre 2013 à 2017 os valores mínimos e medianas estão próximos uns dos outros, sem a queda dos empréstimos em 2014 e 2015, que observamos anteriormente. Este público começou a reduzir o número de empréstimos em 2018, que seguiu em queda até 2020. 

![image](https://user-images.githubusercontent.com/67301805/236533863-7cf135aa-ad8f-410e-bd51-8625b64e047c.png)

Fica como sugestão para a diretoria da biblioteca:

 * rever o que foi feito entre 2010 e 2013, pois houve aumento do número de empréstimos nestes anos.

 * Verificar se houve grandes mudanças no número de alunos, principalmente os alunos de graduação, já que em 2014 e 2015 ocorreram queda no número total de empréstimos, mas isso não ocorreu com os alunos de pós-graduação. 
    
 * Rever as campanhas que foram promovidas, para os alunos de pós-graduação, entre 2013 à 2017, pois podemos inferir que elas foram consistentes, já que elas mantiveram as medianas do número de empréstimos próximos e atingiram os maiores valores máximos.

---

### Desafio 6: JSON, Excel e Pivot_table

![06](https://user-images.githubusercontent.com/67301805/236515569-49c276c0-6db8-4681-b67b-50c608fffd65.jpg)

- Extrair dados de arquivos Excel e JSON ✅

Para fazer a leitura do arquivo Excel, utilizei o *pd.read_excel*. Retirei a primeira linha, porque ela não era referente a variáveis e alterei os nomes das colunas, para ficarem iguais às variáveis presente no dataset sobre os empréstimos. 

Já para ler o arquivo JSON, utilizei o *pd.read_json*, que me devolveu um dataset com duas linhas, a primeira referente aos alunos de graduação e a segunda, dos alunos de pós-graduação.

![image](https://user-images.githubusercontent.com/67301805/236535034-22579cbf-ec52-406b-83d0-159e8c01b103.png)

O público alvo desta análise são os alunos de graduação, então peguei somente as informações da primeira linha.

![image](https://user-images.githubusercontent.com/67301805/236535156-1deaec19-2d1c-4e32-a914-5fe551cec8d3.png)

Antes de fazer o agrupamento dos arquivos, vi que as matrículas extraídas do arquivo Excel e JSON não estavam no mesmo padrão. No Excel, elas estavam como *string*, enquanto no JSON elas estavam como *int64*. Eu não poderia fazer somente a mudança para *string*, porque as matrículas no Excel terminam com um *.0*. A resolução que encontrei foi fazer duas alterações: 

*int* -> *float* -> *string*

![image](https://user-images.githubusercontent.com/67301805/236535250-2d6c3d1d-1f87-48af-981f-cdc7734e67f7.png)

- Agrupar os arquivos em um ✅

Os dados extraídos do Excel resultaram em dataset com 10.000 linhas, enquanto os dados do arquivo JSON resultou em 62.802 linhas, uni ambos através de um *pd.concat*.

![image](https://user-images.githubusercontent.com/67301805/236535445-e586a10d-f58b-45b4-b66f-a89d2ad03680.png)

- Calcular a quantidade de empréstimos feitos entre 2015 e 2020, pelos cursos: ✅

    - Biblioteconomia
    - Ciências sociais
    - Comunicação social
    - Direito
    - Filosofia
    - Pedagogia

Antes de separar apenas os cursos solicitados, importei o dataset dos empréstimos, que estava trabalhando até então e fui fazendo recortes. Primeiro selecionando apenas os alunos de graduação, depois os empréstimos depois de 2015 e fiz o *reset* dos índices.

![image](https://user-images.githubusercontent.com/67301805/236535715-15e9578c-a17c-4a46-86ae-e6fbd52a89f4.png)

Antes de selecionar os cursos, fiz um *value_counts()*, para ter certeza de que eles estão presentes no dataset. Com a presença de todos confirmada, fiz um *.query()* para selecioná-los e criar um novo dataset.

![image](https://user-images.githubusercontent.com/67301805/236535799-0f35b4a9-2872-48b9-93de-d98c3a892a29.png)

Antes de fazer a união dos dois datasets, percebi que só precisaria de algumas variáveis do dataset dos empréstimos, a data do empréstimo e do número de matrícula do aluno. Então, fiz um *.loc* selecionando as duas variáveis e fiz a junção dos datasets com o *.merge*:

![image](https://user-images.githubusercontent.com/67301805/236535996-4c90569a-5d1a-4d20-97c2-708491babdd6.png)

Considerando que somente os anos que os empréstimos ocorreram importa nesta análise, utilizei o *dt.year* na variável referente às datas de empréstimo para retirar as demais informações que não são sobre o ano.

Com a data alterada, fiz um *.iloc* no dataset, selecionando apenas as colunas do empréstimo e curso. Ao fazer um *value_counts()* neste resultado, vemos quantas vezes os anos e cursos apareceram no dataset.

![image](https://user-images.githubusercontent.com/67301805/236536166-f3e8c4a3-e678-481d-9839-50992cfb8157.png)

- Gerar uma tabela com os cursos como índice, as colunas são os anos analisados (2015 a 2020) preenchidas com as quantidades de empréstimos e, ao final, acrescentar uma linha e coluna fazendo os somatórios ✅

Eu nunca havia trabalhado com o *pivot_table* antes, quando li o desafio, pensei em resolver a atividade com um *crosstab*, porém gostei de aprender uma nova opção para chegar em um resultado similar.

![image](https://user-images.githubusercontent.com/67301805/236536354-c369d6ec-261c-47ed-80c1-f946dcfd027d.png)

---

### Desafio 7: Customização de tabelas

![07](https://user-images.githubusercontent.com/67301805/236515573-e132a360-850a-4e67-ae96-a0f5c420ab9c.jpg)

- Fazer a diferença percentual de empréstimos realizados (2017, 2018, 2019 e 2022) para cada curso ✅

Fiz a importação dos arquivos Excel e JSON novamente, porém não há registro de alunos de pós graduação no primeiro arquivo, então não vi necessidade de unir os dois, como fiz no começo do desafio anterior.

Para fazer a seleção dos anos, importei o arquivo *parquet* e fui fazendo *query*. Primeiro, com o tipo de aluno, depois com os anos (> 2017 e < 2020).

![image](https://user-images.githubusercontent.com/67301805/236567265-731f6a21-b4dc-4586-9465-df1f43032f61.png)

Da junção dos datasets até o plot da tabela Pivot, basicamente, segui o mesmo processo que fiz no desafio anterior e não vi necessidade de detalhar novamente o que fiz. A tabela ficou da seguinte forma:

![image](https://user-images.githubusercontent.com/67301805/236567349-88af234c-bbf5-44a5-bd5a-58beca32133b.png)

- Criar uma tabela com os valores encontrados ✅

Foi feita uma previsão de quantos empréstimos seriam realizados em 2022, que foi disponibilizado através de um link, e o transformei em um *DataFrame*. 

![image](https://user-images.githubusercontent.com/67301805/236567444-fa26d587-4778-4790-a118-ae1f18e9c116.png)

Ao tentar unir os valores da previsão com a tabela Pivot, eu não obtive sucesso e passei muito mais tempo do que gostaria tentando resolver essa questão. A solução que encontrei foi refazer a tabela Pivot, pois eu tinha acesso a tabela que deu origem ao *pivot table* e a tabela com os novos dados.

![image](https://user-images.githubusercontent.com/67301805/236567548-49cb1130-8ba6-46d5-b736-3d5f96a5a4e1.png)
![image](https://user-images.githubusercontent.com/67301805/236567583-c7d17502-7fa7-4fa4-b2d9-01af0f02401d.png)

Eu só precisava adicionar mais uma coluna no dataset de previsão, referente ao ano, e depois unir os dois com um *.concat*. Assim, obtive a tabela com os anos de 2017, 2018, 2019 e 2022.

![image](https://user-images.githubusercontent.com/67301805/236567661-a46617d2-23bc-4081-b622-70e3c4525392.png)

Para calcular a diferença percentual, fiz uma função para calcular estes valores, semelhante a *Regra de três*, porém também fazendo uma subtração de 100, para se chegar no percentual, e devolver o valor com duas casas decimais.

![image](https://user-images.githubusercontent.com/67301805/236567718-68884139-c353-45cd-bdf5-89fe664dab5f.png)

Transformei o resultado da função em três variáveis e as transformei em um *DataFrame*.

![image](https://user-images.githubusercontent.com/67301805/236567797-4de043ad-7dc0-44df-b0c1-f529d820ef44.png)


- Exportar como HTML 

A exportação precisava atender alguns requisitos:

	- Não conter numeração no índice;
	- Os nomes dos cursos tenham apenas a primeira letra maiúscula;
	- Os números percentuais estejam indicados pelo símbolo “%”;
	- Cor dos números: Positivos = Verde; Negativos = Vermelho

Para a primeira, como eu já sabia desta condição, quando fui fazer o *Dataframe* com as diferenças percentuais, atribuí nomes em forma de *string* para as colunas.

![image](https://user-images.githubusercontent.com/67301805/236568235-d4736b15-6ba7-441e-9ced-53acaed8ae35.png)

Para fazer o segundo tratamento, utilizei o método *capitalize()*.

![image](https://user-images.githubusercontent.com/67301805/236568379-039a9b50-23d1-41a8-859d-a1b0cd87f6d6.png)

Para os dois últimos itens, eles me custaram muito mais tempo do que planejei 😕

Inicialmente, havia entendido que precisava fazer as alteração no *DataFrame* e que elas precisavam ser feitas antes da exportação. 

Resultado: passei horas tentando atribuir as cores vermelho e verde para as colunas numéricas, sem alterar a coluna *Curso*, mas sem sucesso… 😥

A exaustão foi tamanha, que nem consegui formular uma solução para a adição do símbolo de “%” ao final dos números… 😵‍💫

O projeto já estava com mais de um dia de atraso, eu não estava tendo progressão nas soluções que tentava implementar e decidi fazer a exportação da tabela como ela estava, que resultou no seguinte HTML.

![image](https://user-images.githubusercontent.com/67301805/236568683-d7aaa310-12de-4d45-96bc-46cc5477dec7.png)

Ao verificar a correção, vi que as duas últimas configurações eram para serem feitas durante a exportação, algo que não imaginei como solução.

## Conclusão 🏁

Eu gostei bastante de ter realizado estes desafios, sempre é muito bom pôr em prática o que já aprendemos e acabar descobrindo coisas novas ao longo do caminho.
Infelizmente, eu não consegui entregar os desafios dentro de sete dias e sem as condições finais, mas acredito que o saldo final foi positivo, ainda tenho muito o que explorar na estilização de *DataFrame* e farei isso como lição de casa.

---

Muito obrigada por chegar até aqui e até a próxima 🤗

## Ferramentas utilizadas 🧰
<p> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> 
    <a href="https://pandas.pydata.org/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/2ae2a900d2f041da66e950e4d48052658d850630/icons/pandas/pandas-original.svg" alt="pandas" width="40" height="40"/> </a>
    <a href="https://matplotlib.org/" target="_blank" rel="noreferrer"> <img src="https://matplotlib.org/_static/images/documentation.svg" alt="matplotlib" width="40" height="40"/> </a>
    <a href="https://seaborn.pydata.org/" target="_blank" rel="noreferrer"> <img src="https://seaborn.pydata.org/_images/logo-mark-lightbg.svg" alt="seaborn" width="40" height="40"/> </a>
    </p>

<br><hr> 
[🔼 back to Top](https://github.com/fab-souza/7DaysOfCode-Python_Pandas#7-days-of-code---python-pandas)
