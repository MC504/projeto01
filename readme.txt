Esse projeto possu� 3 m�dulos que trabalham com uma matriz 9x9 representando um tabuleiro de Sudoku.

No primeiro m�dulo foi implementado um verificador que diz se a matriz est� valida ou se possui erros e nesse caso, apontando os mesmos. Assim criamos 3 fun��es que analisam 
independentemente as linhas, colunas e submatrizes da matriz principal, verificando se a regra do jogo est� v�lida. Visto que as 3 fun��es fazem uma an�lise independente,
conclu�mos que elas poderiam ser executadas separadamente. Criamos 9 threads para executar cada fun��o. Dessa forma a valida��o da 
Linha 1, Coluna1 e submatriz 1 s�o executadas paralelamente em threads diferentes, em uma pr�xima intera��o j� � come�ada a verifica��o da Linha2, Coluna2 e submatriz2
mesmo ainda n�o tendo necessariamente terminada a valida��o do grupo 1. Assim, no total executamos 27 threads paralelizando as valida��es.
Essa � uma abordagem interessante pois podemos validar diversas partes da matriz que dependem de diferentes regras de valida��o de forma concorrente, sem utilizar um n�mero
absurdo de threads e agilizando o processamento.

O segundo m�dulo foi implementado para, dado um tabuleiro de Sudoku 9x9 com X's, disponibilizar as op��es v�lidas para cada campo contendo um X. Uma fun��o foi criada para detectar essas op��es, chamada "findClues". Como o objetivo � analisar cada c�lula da matriz, executamos 81 threads paralelizando as buscas pelas op��es. A fun��o verifica se existe um X, e caso exista, preenche a sa�da com todas as op��es, iterando nas linhas, colunas e submatrizes de modo a retirar op��es invalidas substituindo pelo caracter N. Na impress�o, removemos todas as refer�ncias do caracter N, restando apenas as op��es v�lidas para cada uma das c�lulas. A escolha das 81 threads teve como objetivo otimizar a identifica��o das op��es em cada uma das c�lulas da matriz completa em paralelo, sem que haja problemas de concorr�ncia. Considerando que as c�lulas que n�o est�o marcadas com X tem seu processamento bem r�pido, isso ameniza o fato de termos uma alta quantidade de threads simult�neas.

O terceiro m�dulo n�o foi terminado, apesar de boa parte do c�digo estar feita. O objetivo do modulo sudoku.c �, a partir de uma entrada com alguns n�meros faltantes de um
tabuleiro 9x9 de Sudoku (representados pelo caracter 'X'), ele retornar para o usu�rio o Sudoku resolvido. O algoritmo pensado foi utilizar o segundo m�dulo para encontrar
todas as poss�veis dicas e, para cada elemento faltante que s� tivesse uma dica, considerar que esse elemento � o certo. Para avaliar quais elementos j� est�o certos, uma
matriz 9x9 foi feita e caso o elemento daquela posi��o esteja com valor 0, ainda n�o est� correto, caso esteja com 1, j� est� correto. Enquanto os 81 elementos n�o estiverem
corretos, o programa rodaria novamente o algoritmo do segundo m�dulo e, cada vez retornaria menos possibilidades, j� que no passo anterior assumimos que os que s� tem uma
dica est�o corretos e marcamos isso na matriz de valores corretos do Sudoku. Isso aconteceria at� que todos os valores estivessem corretos. � poss�vel talvez que o Sudoku 
n�o tenha solu��o e, nesse caso, em algum momento o n�mero de dicas seria nulo, nos mostrando que o Sudoku n�o pode ser resolvido. As threads a princ�pio rodariam em paralelo
como no segundo m�dulo, fazendo com que o programa calcule de maneira mais r�pida as dicas.
