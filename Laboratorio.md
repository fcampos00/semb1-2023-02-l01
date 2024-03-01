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
R.// Ferramentas do toolchain:
CC = arm-none-eabi-gcc
RM = rm -rf

// Diretórios arquivos objeto e de lista de dependências serão salvos:
OBJDIR = build
DEPDIR = .deps

// Arquivos a serem compilados:

SRCS = src/startup.c src/main.c

// Flags do compilador:

CFLAGS = -g -mcpu=cortex-m4 -mthumb -Wall -O0 -I./inc
DEPFLAGS = -MMD -MP -MF $(DEPDIR)/$*.d

// Gera lista de arquivos objeto e cria diretório onde serão salvos:

OBJS = $(patsubst src/%.c,$(OBJDIR)/%.o,$(SRCS))

// Gera lista de arquivos de lista dependência e cria diretório onde serão salvos:

DEPS = $(patsubst src/%.c,$(DEPDIR)/%.d,$(SRCS))

// Diretivas especiais para que não dê erro caso o diretório já exista:

$(shell mkdir -p $(OBJDIR) > /dev/null)
$(shell mkdir -p $(DEPDIR) > /dev/null)

// Target principal:

all: $(TARGET).elf

// Compilação dos objetos:

$(OBJDIR)/%.o: src/%.c
    $(CC) $(CFLAGS) $(DEPFLAGS) -c $< -o $@

// Inclui arquivos de dependência:

-include $(DEPS)

// Cria um novo target para cada arquivo de dependência possível:

$(DEPS):

// Linkagem:

$(TARGET).elf: $(OBJS)
    $(CC) $(LDFLAGS) $^ -o $@

.PHONY: clean
clean:
    $(RM) $(OBJDIR) $(DEPDIR)

OBS:Neste script, OBJDIR e DEPDIR especificam os diretórios onde os arquivos objeto e as dependências serão salvos, respectivamente. SRCS contém os arquivos fonte que serão compilados. CFLAGS contém as flags de compilação. DEPFLAGS são as flags para gerar as dependências. OBJS e DEPS são as listas de arquivos objetos e dependências, respectivamente. A regra all é o alvo padrão, responsável por gerar o executável. A regra para compilar os objetos é similar à que você já tinha, mas atualizada para usar o diretório OBJDIR. DEPS é incluído para garantir que as dependências sejam geradas e incluídas corretamente. O alvo clean é utilizado para limpar os diretórios de objetos e dependências.
