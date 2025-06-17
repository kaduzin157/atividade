# atividade
#include <stdio.h> 

#include <stdlib.h>

#include <string.h>

#define MAX_ITEMS 50 #define MAX_CART_ITEMS 50

typedef struct { char descricao[30]; float valor; int id; } Item;

typedef struct { Item item; int qtd; } ItemCarrinho;

typedef struct { Item catalogo[MAX_ITEMS]; int totalItens; ItemCarrinho carrinhoCompras[MAX_CART_ITEMS]; int totalCarrinho; } Loja;

void inicializarLoja(Loja *loja) { loja->totalItens = 0; loja->totalCarrinho = 0; }

void adicionarItem(Loja *loja) { if (loja->totalItens >= MAX_ITEMS) { puts("Limite de itens no catálogo atingido.\n"); return; }

Item novoItem;
novoItem.id = loja->totalItens + 1;
printf("Digite a descrição do item: ");
scanf(" %29[^\n]", novoItem.descricao);
while (getchar() != '\n');

printf("Digite o valor do item: ");
scanf("%f", &novoItem.valor);
while (getchar() != '\n');

loja->catalogo[loja->totalItens++] = novoItem;
printf("Item cadastrado com sucesso!\n");
}

void listarItens(const Loja *loja) { if (loja->totalItens == 0) { puts("Nenhum item no catálogo!\n"); return; } puts("Itens cadastrados:\n"); for (int i = 0; i < loja->totalItens; i++) { printf("ID: %d\nDescrição: %s\nValor: R$ %.2f\n", loja->catalogo[i].id, loja->catalogo[i].descricao, loja->catalogo[i].valor); printf("--------------------------\n"); } }

void exibirMenu(Loja *loja) { int escolha; do { puts("----- BEM-VINDO AO MERCADO VIRTUAL -----\n"); puts("1. Cadastrar item"); puts("2. Listar itens"); puts("3. Adicionar item ao carrinho"); puts("4. Remover item do carrinho"); puts("5. Visualizar carrinho"); puts("6. Finalizar compra"); puts("7. Sair\n");

    printf("Escolha uma opção: ");
    scanf("%d", &escolha);

    switch (escolha) {
    case 1:
        adicionarItem(loja);
        break;
    case 2:
        listarItens(loja);
        break;
    // Implementar outras funções de acordo com o plano de refatoração
    case 7:
        printf("Saindo...\n");
        break;
    default:
        puts("Opção inválida!\n");
        break;
    }

    puts("\nPressione ENTER para continuar...");
    getchar();
    getchar();
} while (escolha != 7);
}

int main() { Loja loja; inicializarLoja(&loja); exibirMenu(&loja); return 0; }
