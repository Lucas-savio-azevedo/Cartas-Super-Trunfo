#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

#define NUM_CARTAS 4
#define NUM_ATRIBUTOS 3

typedef struct {
    char nome[30];
    int forca;
    int velocidade;
    int inteligencia;
} Carta;

// Função para exibir uma carta
void exibirCarta(Carta c) {
    printf("Nome: %s\n", c.nome);
    printf("1. Força: %d\n", c.forca);
    printf("2. Velocidade: %d\n", c.velocidade);
    printf("3. Inteligência: %d\n", c.inteligencia);
}

// Função para escolher atributo
int escolherAtributo() {
    int escolha;
    printf("\nEscolha o atributo para disputar (1-Força, 2-Velocidade, 3-Inteligência): ");
    scanf("%d", &escolha);
    return escolha;
}

// Função para obter valor de atributo baseado na escolha
int obterValorAtributo(Carta c, int atributo) {
    switch (atributo) {
        case 1: return c.forca;
        case 2: return c.velocidade;
        case 3: return c.inteligencia;
        default: return 0;
    }
}

int main() {
    srand(time(NULL));

    // Definindo baralho de cartas
    Carta baralho[NUM_CARTAS] = {
        {"Dragão", 90, 70, 60},
        {"Fênix", 60, 95, 85},
        {"Minotauro", 85, 65, 50},
        {"Grifo", 70, 80, 75}
    };

    // Sorteando carta do jogador e do computador
    int indiceJogador = rand() % NUM_CARTAS;
    int indiceComputador;

    do {
        indiceComputador = rand() % NUM_CARTAS;
    } while (indiceComputador == indiceJogador);

    Carta cartaJogador = baralho[indiceJogador];
    Carta cartaComputador = baralho[indiceComputador];

    printf("Sua carta:\n");
    exibirCarta(cartaJogador);

    // Jogador escolhe atributo
    int atributoEscolhido = escolherAtributo();

    printf("\nCarta do computador:\n");
    exibirCarta(cartaComputador);

    // Obtendo valores escolhidos
    int valorJogador = obterValorAtributo(cartaJogador, atributoEscolhido);
    int valorComputador = obterValorAtributo(cartaComputador, atributoEscolhido);

    printf("\nResultado:\n");
    printf("Seu valor: %d\n", valorJogador);
    printf("Valor do computador: %d\n", valorComputador);

    // Definindo vencedor
    if (valorJogador > valorComputador) {
        printf("\nVocê venceu esta rodada!\n");
    } else if (valorJogador < valorComputador) {
        printf("\nComputador venceu esta rodada.\n");
    } else {
        printf("\nEmpate!\n");
    }

    return 0;
}
