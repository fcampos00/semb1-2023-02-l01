# Atividades de Laboratório - Sistemas Embarcados I
# Felipe Andrade Campos-11921ETE007

## 1. O arquivo **stm32f411-blackpill/src/startup.c** implementa parcialmente a tabela de vetores de interrupção do microcontrolador STM32F411. Utilizando a tabela disponibilizada no manual de referência (***RM0383 Reference manual***) implemente **toda** a tabela de vetores de interrupção do microcontrolador STM32F411.
R.#include <stdint.h>

// Definição do endereço inicial da pilha
#define SRAM_START 0x20000000U /* Início da SRAM Cortex-M */
#define SRAM_SIZE (128U * 1024U) /* Tamanho SRAM STM32F411 128K */
#define SRAM_END ((SRAM_START) + (SRAM_SIZE)) /* Final da SRAM STM32F411 */
#define STACK_START SRAM_END /* Início da stack */

// Definição do tipo de função para os vetores de interrupção
typedef void (*InterruptHandler)(void);

// Protótipos das funções de exceção
void onReset(void);
void onNMI(void) __attribute__((weak, alias("defaultHandler")));
void onHardFault(void) __attribute__((weak, alias("defaultHandler")));
// Implemente outras funções de manipuladores de interrupção conforme necessário

// Vetor de tabela de exceção
__attribute__((section(".isr_vector"))) InterruptHandler __isr_vectors[] = {
    (InterruptHandler)((uint32_t)STACK_START), // Endereço de inicialização de pilha
    onReset, 
    onNMI, 
    onHardFault, 
    // Vetores de interrupção específicos do STM32F411
    // Coloque aqui os demais manipuladores de interrupção
};

// Função de Reset
void onReset(void) {
    // Lógica para tratamento de reset
}

// Manipulador de interrupção padrão
void defaultHandler(void) {
    while (1) {}
}
## 2. Siga o roteiro disponibilizado no [laboratório 02](https://github.com/daniel-p-carvalho/ufu-semb1-lab-02.git) e implemente no arquivo **stm32f411-blackpill/Makefile** um script para automatizar o processo de compilação. Este script deverá ser capaz de gerar os arquivos objetos realocáveis e gerenciar automaticamente as dependências dos arquivos fonte do projeto.
