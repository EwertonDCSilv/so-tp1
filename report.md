RELATÓRIO

1. Termo de compromisso

Os membros do grupo afirmam que todo o código desenvolvido para este
trabalho é de autoria própria.  Exceto pelo material listado no item 3
deste relatório, os membros do grupo afirmam não ter copiado
material da Internet nem obtiveram código de terceiros.

2. Membros do grupo e alocação de esforço

Preencha as linhas abaixo com o nome e o e-mail dos integrantes do
grupo.  Substitua XX pela contribuição de cada membro do grupo no
desenvolvimento do trabalho.

Ewerton Silva Santos <ewerton_dc@hotmail.com> 50%
Rafael Oliveira Prado Nascimento <rafaelnascimento@dcc.ufmg.br> 50%


3. Referências bibliográficas

    1 The GNU C Library Reference Manual, Sandra Loosemore, Richard M. Stallman, Roland McGrath, Andrew Oram, Ulrich Drepper. Version 2.33.
        Link: <https://www.gnu.org/software/libc/manual/pdf/libc.pdf>
        Capítulos:
        . Capítulo 13 - Low-Level Input/Output
        . Capítulo 15 - File System Interface
        . Capítulo 15 - Pipes and FIFOs
        . Capítulo 26 - Process
        
    2 Modern Operating Systems, Andrew S. Tanenbaum and Herbert Bos. 4th Edition.
        Capítulos:
        . Capitulo 2 Processos e threads
        
    3 Fundamentos de Sistemas Operacionais, Silberschatz, Galvin e Gagne. 9th Edition.
        Capítulos:
        . Capítulo 3 - Processos

4. Estruturas de dados

Não foram utilizadas estruturas de dados complexas, apenas as já implementadas no código **sh.c** e as fornecidas nativamente pela linguagem, tendo em vista a simplicidade do problema e facilidade de utilizar os recursos já disponíveis. \
Para o executor simples (**case ‘’**) fora utilizada apenas uma string para obter o nome do programa a ser executado como filho, em seguida a função **execvp** é chamada, tendo como parâmetros o programa a ser executado e os argumentos recebidos. A função **execvp** o ao conjunto de funções **exec**, criando um processo filho que pode executar programadas distintas do pai.\
	Para o **case “>”** foi utilizada uma lista para abrir o arquivo de saída, utilizando a função **open** para abrir e dar permissão de escrita ao arquivo de saída, em seguida foi utilizada a função **close** para fechar o arquivo de saída, na sequência foi utilizada a função **dup** para criar cópia para o descritor de arquivo e mais uma vez a função **close** para fechar a lista **p[1]**(escrita), em seguida foi executada a função **runcmd** para executar o comando cmd. Para o **case “<”** assim como no caso anterior, foram utilizadas as mesmas funções, mas para o arquivo de entrada, no índice **p[0]**(leitura).\
	Para o **case “|”** foi utilizado a função pipe, para criar um canal de comunicação entre processos, recebendo um vetor que guarda o file description, sendo 0 posição de leitura e 1 posição de escrita. Em seguida é utilizada a função **fork**, para criar um processo filho e armazenar na variável child, sendo que se a variável child for <0, o processo é invalido e não entra na estrutura Switch. \
No Switch, caso o valor da variável child seja 0, corresponde a um processo filho, onde é utilizada a função **close** para fechar o arquivo de saída, em seguida é chamada a função **copyClose** que recebe o **descriptor[1]** e **descriptor[0]** como parâmetro, fechando os descritores de entrada e saída, por fim o comando a esquerda é executado. Caso contrário é um processo pai, que fecha o arquivo de entrada e também chama a função **copyClose** que recebe o **descriptor[0]** e **descriptor[1]** como parâmetro, por fim o comando a direita é executado. A função **copyClose**, tem como objetivo, basicamente simplificar o fechamento e a cópia dos arquivos de descrição, na qual o primeiro parâmetro é duplicado usando a função **dup**.\

