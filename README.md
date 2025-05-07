#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

typedef struct no {
    int info;
    struct no* prox;
} No;

typedef No* Lista;

Lista inicializar() {
    return NULL;
}

bool lista_vazia(Lista l) {
    return l == NULL;
}

Lista inserir_inicio(Lista l, int valor) {
    No* novo = (No*) malloc(sizeof(No));
    novo->info = valor;
    novo->prox = l;
    return novo;
}

Lista inserir_fim(Lista l, int valor) {
    No* novo = (No*) malloc(sizeof(No));
    novo->info = valor;
    novo->prox = NULL;
    
    if (l == NULL) return novo;

    No* aux = l;
    while (aux->prox != NULL)
        aux = aux->prox;

    aux->prox = novo;
    return l;
}

Lista remover_elemento(Lista l, int valor) {
    No* atual = l;
    No* anterior = NULL;

    while (atual != NULL) {
        if (atual->info == valor) {
            No* temp = atual;
            if (anterior == NULL) {
                l = atual->prox;
                atual = l;
            } else {
                anterior->prox = atual->prox;
                atual = anterior->prox;
            }
            free(temp);
        } else {
            anterior = atual;
            atual = atual->prox;
        }
    }

    return l;
}

int tamanho(Lista l) {
    int cont = 0;
    while (l != NULL) {
        cont++;
        l = l->prox;
    }
    return cont;
}

float media(Lista l) {
    int soma = 0, cont = 0;
    while (l != NULL) {
        soma += l->info;
        cont++;
        l = l->prox;
    }
    if (cont == 0) return 0;
    return (float)soma / cont;
}

int maior(Lista l) {
    if (l == NULL) return -1;

    int max = l->info;
    l = l->prox;
    while (l != NULL) {
        if (l->info > max)
            max = l->info;
        l = l->prox;
    }
    return max;
}

int menor(Lista l) {
    if (l == NULL) return -1;

    int min = l->info;
    l = l->prox;
    while (l != NULL) {
        if (l->info < min)
            min = l->info;
        l = l->prox;
    }
    return min;
}

bool busca(Lista l, int valor) {
    while (l != NULL) {
        if (l->info == valor)
            return true;
        l = l->prox;
    }
    return false;
}

void imprimir(Lista l) {
    while (l != NULL) {
        printf("%d -> ", l->info);
        l = l->prox;
    }
    printf("NULL\n");
}


//testando se deu certo
int main() {
    Lista minhaLista = inicializar();

    minhaLista = inserir_inicio(minhaLista, 10);
    minhaLista = inserir_fim(minhaLista, 20);
    minhaLista = inserir_inicio(minhaLista, 5);
    minhaLista = inserir_fim(minhaLista, 10);

    printf("Lista atual: ");
    imprimir(minhaLista);

    printf("Tamanho: %d\n", tamanho(minhaLista));
    printf("Média: %.2f\n", media(minhaLista));
    printf("Maior: %d\n", maior(minhaLista));
    printf("Menor: %d\n", menor(minhaLista));
    printf("Busca 20: %s\n", busca(minhaLista, 20) ? "Sim" : "Não");

    minhaLista = remover_elemento(minhaLista, 10);
    printf("Após remover 10: ");
    imprimir(minhaLista);

    printf("Lista vazia? %s\n", lista_vazia(minhaLista) ? "Sim" : "Não");

    return 0;
}
