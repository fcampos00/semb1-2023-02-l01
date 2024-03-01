# Questionário Sistemas Embarcados I
# Felipe 11921ETE007

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
R.A compilação cruzada é o processo de compilar um programa em um ambiente de desenvolvimento diferente do ambiente do qual ele será executado.Isso geralmente é feito quando o código-fonte é desenvolvido em uma plataforma,como um computador pessoal,mas o programa final precisa ser executado em uma plataforma diferente,como no caso um sistema embarcado.Sua importância se dá pelo fato de permitir que desenvolvedores criem softwares para uma ampla variedade de plataformas,maximizando a eficiência e a portabilidade do código.
## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
R.É um conjunto de instruções que são executadas automaticamente quando um computador ou dispositivo é ligado,em que ele é responsável por carregar o sistema operacional e outros programas essenciais para o funcionamento do sistema.Sua finalidade é garantir que o sistema operacional seja carregado corretamente e que todos os programas necessários estejam disponíveis para uso,além de também ser usado para configurar o sistema operacional e personalizar o ambiente de trabalho.Porém,além desses benefícios que um código de inicialização possui,ele pode ter algumas desvantagens,tais como deixar o processo de inicialização mais lento,possibilidade de causar problemas de compatibilidade e difícil configuração,portanto deve-se verificar a compatibilidade dos programas e fazer um backup do código de inicialização sempre que for utilizá-lo.
## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
R.O Makefile é basicamente um arquivo de texto que define as instruções para construir um programa ou software,em que ele serve como um guia para o utilitário make,que automatiza o processo de compilação,linkedição e outras tarefas necessárias para gerar o programa final.Ele torna o processo de desenvolvimento mais eficiente e organizado,pois centraliza todas as informações necessárias para construir o programa em um único lugar,o que em um trabalho em equipe gerará mais facilidade,já que todos poderão construir o programa. 
#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
R.O utilitário make lê o Makefile e segue as instruções nele contidas para construir o programa,e o processo consiste nas etapas de análise do Makefile(o make lê o Makefile e identifica os targets[alvos] e suas dependências),verificação de dependências(o make verifica se os arquivos que compõem o target foram modificados desde a última compilação),execução de regras(caso os arquivos foram modificados,o make executa as regras associadas ao target) e atualização de timestamps(o make atualiza os timestamps dos arquivos que foram modificados).
#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
R.A sintaxe para criar um novo target no Makefile é: target: dependências
                                                         regras
Onde o target representa o nome do target,dependências representa uma lista de arquivos que o target depende e regras representa uma lista de comandos que serão executados para construir o target.
#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
R.As dependências de um target são definidas no Makefile após o nome do target,separadas por dois pontos(:).As dependências podem ser arquivos ou outros targets,e são utilizadas pelo make para determinar quais arquivos precisam ser recompilados quando um arquivo é modificado.Se um arquivo depende de outro arquivo que foi modificado,o make recompilará o arquivo dependente.
#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
R.As regras do Makefile são as instruções que o make segue para construir um target,e elas podem ser subdivididas em explícitas(definidas explicitamente no Makefile pelo desenvolvedor,em que definem quais comandos serão executados para construir o target) e implícitas(predefinidas pelo make para alguns tipos de arquivos,em que definem automaticamente os comandos para compilar e linkar de acordo com o tipo de arquivo).
## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
R.O conjunto de instruções Thumb é um conjunto de instruções de 16 bits para a arquitetura ARM,e oferece várias vantagens como o tamanho reduzido(instruções Thumb são menores que as isntruções ARM de 32 bits,o que reduz o tamanho do código e a quantidade de memória necessária),eficiência energética(instruções Thumb geralmente consomem menos energia do que as instruções ARM de 32 bits,o que é importante para sistemas embarcados com bateria) e desempenho aprimorado(em alguns casos,instruções Thumb podem ser executadas mais rapidamente do que as instruções ARM de 32 bits).
### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?

### (f) Qual a finalidade do **LR** (***Link Register***)?

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?

### (h) O que é a tabela de vetores de interrupção?

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 


## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
