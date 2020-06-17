# matriz-ajacente-grafo
//busca bfs e dfs em uma matriz adjacente
#include<stdio.h>
#include<stdlib.h>
#define TAM 4


struct tVertice {
	char rotulo;
	int visitado; // 0 / 1
	int aresta;
};

// Declarações
void inicializar(struct tVertice grafo[TAM][TAM]);
void incluir(struct tVertice grafo[TAM][TAM]);
void bfs(struct tVertice grafo[TAM][TAM]);
void dfs(struct tVertice grafo[TAM][TAM]);


int main() {
	struct tVertice grafo[TAM][TAM];
	int coluna, linha;

	inicializar(grafo);
	incluir(grafo);


	for(coluna = 0; coluna < TAM; coluna++) {
		for(linha = 0; linha < TAM; linha++) {
			printf("%d ", grafo[linha][coluna].aresta);
		}
		printf("\n");
	}

	printf("\n\n");

	bfs(grafo);
	printf("\n");

	inicializar(grafo);
	incluir(grafo);
	dfs(grafo);

	return 0;
}


void inicializar(struct tVertice grafo[TAM][TAM]) {
	int linha, coluna;

// coloca 0 em todas as arestas;
	for(coluna = 0; coluna < TAM; coluna++) {
		for(linha = 0; linha < TAM; linha++) {
			grafo[coluna][linha].aresta = 0;
			grafo[coluna][linha].visitado = 0;
		}
	}
}

void incluir(struct tVertice grafo[TAM][TAM]) {
	int i;

// Incluindo arestas pré-determinadas
	grafo[1][0].aresta = 1;
	grafo[2][0].aresta = 1;
	grafo[2][1].aresta = 1;
	grafo[3][2].aresta = 1;

// atribui a letra A,B,C,D usando a tabela ASCII
	for(i = 0; i < TAM; i++) {
		grafo[i][i].rotulo = 97+i;
	}

}

void bfs(struct tVertice grafo[TAM][TAM]) {
	int coluna = 3, linha = 0, i = 1;

	// vetor para guardar a ordem de vertice no encaminhamento BFS
	struct tVertice fila[TAM];

	fila[0] = grafo[0][0]; // vertice de origem "A"
	grafo[0][0].visitado = 1;

	//debug do codigo
	for(linha = 0; linha < TAM; linha++) {
		for(coluna = TAM-1; coluna >= 0; coluna--) {
			//printf("Coluna[%d], Linha[%d]\n", coluna, linha);
			if(grafo[coluna][linha].aresta == 1) {
				//printf("tem ligacao\n");
				if(grafo[coluna][coluna].visitado == 0) {
					//printf("Nao foi visitado\n");
					fila[i] = grafo[coluna][coluna];
					i++;
					grafo[coluna][coluna].visitado = 1;
					//printf("%c foi visitado\n", grafo[coluna][coluna].rotulo);
				} else {
					//printf("%c foi visitado\n", grafo[coluna][coluna].rotulo);
				}
			} else {
				//printf("Nao tem ligacao\n");
			}
		}
	}

	printf("BFS\n");
	for(i = 0; i < TAM; i++) {
		printf("%c ", fila[i].rotulo);
	}

}

void dfs(struct tVertice grafo[TAM][TAM]) {
	int coluna = 3, linha = 0, i = 1, aux = 0, aux2 = 0;

	// vetor para guardar a ordem de vertice no encaminhamento BFS
	struct tVertice fila[TAM];

	fila[0] = grafo[0][0]; // Vertice de origem "A"
	grafo[0][0].visitado = 1;

	//debug do codigo
	while(aux2 < TAM){ // 4 é quantida de ligações que o vertice de origem pode fazer 
	
		for(linha = 0; linha < TAM; linha++, aux++) {
			aux = 0;
			for(coluna = TAM-1; coluna >= 0 && aux == 0; coluna--) {
			//	printf("Coluna[%d], Linha[%d]\n", coluna, linha);
				if(grafo[coluna][linha].aresta == 1) {
				//	printf("tem ligacao\n");
					if(grafo[coluna][coluna].visitado == 0) {
						//printf("Nao foi visitado\n");
						fila[i] = grafo[coluna][coluna];
						i++;
						grafo[coluna][coluna].visitado = 1;
						aux = 1;
						//printf("%c foi visitado\n", grafo[coluna][coluna].rotulo);
					} else {
						//printf("%c foi visitado\n", grafo[coluna][coluna].rotulo);
					}
				} else {
					//printf("Nao tem ligacao\n");
				}
			}
		}
		if(linha == TAM && coluna == TAM){
			aux = 0;
		}
		aux2++;
	}


	printf("DFS\n");
	for(i = 0; i < TAM; i++) {
		printf("%c ", fila[i].rotulo);
	}

}
