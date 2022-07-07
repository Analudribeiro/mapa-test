# mapa-test
testando árvore binaria 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

//defines
#define E 0
#define D 1
#define R -1
//sera no
typedef struct NO {
	int dado;
	struct NO *esq;
	struct NO *dir;
	struct NO *pai;
} NO;
//arvore
typedef struct ARVORE{
	NO *raiz;
}ARVORE;

ARVORE a;

//Protótipos das funções
void inicializaArvore(ARVORE arv);
void inicializaNo(NO* n, int val);
void insereNoArvoreOrdenada(int valor);
void preOrdem(NO* raiz);
void emOrdem(NO* raiz);
void posOrdem(NO* raiz);

void inicializaArvore(ARVORE arv)
{
	arv.raiz = NULL;
}

void inicializaNo(NO* n, int val){
	if(!n)
	{
		printf("Falha de alocacao.\n");
		return;
	}
	n->pai = NULL;
	n->esq = NULL;
	n->dir = NULL;
	n->dado = val;
}
//nota : valores menores  vão à esquerda
//nota :valores maiores ou iguais vão à direita
void insereNoArvoreOrdenada(int valor)
{
	NO* corrente = a.raiz;
	NO* pai;

	NO* novoNo = (NO*) malloc(sizeof(NO));
	inicializaNo(novoNo, valor);
	printf("Inserindo no %d. \n", novoNo->dado);
	
	if(corrente == NULL)
	{
		a.raiz = novoNo;
		printf("No inserido na raiz. \n");
		return;
	}
	
	while(corrente){
		pai = corrente;
		if(novoNo->dado < corrente->dado){
			corrente = corrente->esq;
			if(!corrente){
				printf("No inserido à esquerda do no %d. \n", pai->dado);
				pai->esq = novoNo;
				return;
			}
		}
		else{
			corrente = corrente->dir;
			if(!corrente){
				printf("No inserido à direita do no %d. \n", pai->dado);
				pai->dir = novoNo;
				return;
			}
		}
	}
}

void preOrdem(NO* raiz){
	if(raiz){
		printf("%d \t", raiz->dado);
		preOrdem(raiz->esq);
		preOrdem(raiz->dir);
	}
}

void emOrdem(NO* raiz){
	if(raiz){
		emOrdem(raiz->esq);
		printf("%d \t", raiz->dado);
		emOrdem(raiz->dir);
	}
}

void posOrdem(NO* raiz){
	if(raiz){
		posOrdem(raiz->esq);
		posOrdem(raiz->dir);
		printf("%d \t", raiz->dado);
	}
}

int main()
{
	inicializaArvore(a);
	
	printf("\n ------------------------------\n");
	printf("\n         Inicialização         \n");
	printf("\n ------------------------------\n");
	
	insereNoArvoreOrdenada(2);
	insereNoArvoreOrdenada(1);
	insereNoArvoreOrdenada(1);
	insereNoArvoreOrdenada(4);
	insereNoArvoreOrdenada(1);
	insereNoArvoreOrdenada(8);
	insereNoArvoreOrdenada(6);
    insereNoArvoreOrdenada(5);
    insereNoArvoreOrdenada(5);
	
	printf("\nBusca em ordem: \n");
	emOrdem(a.raiz);
	
	printf("\nBusca pre ordem: \n");
	preOrdem(a.raiz);
	
	printf("\nBusca pos ordem: \n");
	posOrdem(a.raiz);
}

