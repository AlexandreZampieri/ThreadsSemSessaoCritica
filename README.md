Escrita Concorrente em Arquivo com Threads (C#)

Este projeto foi desenvolvido para demonstrar um problema comum em programação concorrente, quando várias threads acessam o mesmo recurso ao mesmo tempo.

O programa cria 20 threads, e cada uma delas escreve 500 linhas em um arquivo de texto, totalizando 10.000 linhas.

O objetivo é comparar dois cenários:

Escrita sem controle de concorrência Escrita com seção crítica usando lock Funcionamento do Programa

Cada thread executa a mesma função:

Gera uma linha de texto contendo o ID da thread Escreve essa linha em um arquivo Repete esse processo 500 vezes

Como são 20 threads, o total esperado no arquivo é:

20 threads × 500 linhas = 10000 linhas

--Sem Seção Crítica

Na primeira versão do código, as threads escrevem no arquivo ao mesmo tempo, sem nenhum tipo de proteção.

Trecho do código:

writer.WriteLine(linha);

Como o StreamWriter não é thread-safe, várias threads tentando escrever ao mesmo tempo podem causar problemas.

Durante a execução apareceu o erro:

Probable I/O race condition detected while copying memory. The I/O package is not thread safe by default.

Esse erro acontece porque o sistema detecta que várias threads estão acessando o mesmo recurso simultaneamente, causando uma condição de corrida (race condition).

Tive de utilizar um tratamento de exceção (try-catch) para tornar o erro visível.

Isso pode resultar em:

-Linhas faltando; 
-Linhas misturadas; 
-Erros durante a execução.
