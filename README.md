#include <stdio.h>  // Biblioteca padrão para entrada e saída (ex: printf, scanf)

#define MAX 100  // Define o número máximo de cadastros permitidos

// Estrutura que representa um carro com marca, modelo e placa   
struct carro {
    char marca[50];  
    char modelo[50];  
    char placa[8];    
};

struct carro carros[MAX];
int qtd = 0;

// Cadastrar novo carro
void cadastrar() {
    if (qtd >= MAX) {
        printf("\nLimite de carros atingido (%d cadastros)!\n", MAX);
        return;
    }

    printf("\n--- NOVO CADASTRO ---\n");

    printf("Marca: ");
    scanf(" %49[^\n]", carros[qtd].marca);

    printf("Modelo: ");
    scanf(" %49[^\n]", carros[qtd].modelo);

    printf("Placa: ");
    scanf(" %7[^\n]", carros[qtd].placa);

    qtd++;

    printf("\nCadastro realizado com sucesso!\n");
}

// Busca por código (indice + 1)
int buscarPorCodigo(int codigo) {
    if (codigo < 1 || codigo > qtd) {
        return -1;
    }
    return codigo - 1;
}

// Editar carro
void editar() {
    int codigo, index;

    printf("\n--- EDITAR CADASTRO ---\n");
    printf("Digite o codigo do carro: ");
    scanf("%d", &codigo);

    index = buscarPorCodigo(codigo);

    if (index == -1) {
        printf("\nCarro não encontrado!\n");
        return;
    }

    printf("\nEDITANDO CADASTRO:\n");
    printf("Marca atual: %s\n", carros[index].marca);
    printf("Modelo atual: %s\n", carros[index].modelo);
    printf("Placa atual: %s\n\n", carros[index].placa);

    printf("Novo modelo: ");
    scanf(" %49[^\n]", carros[index].modelo);

    printf("Nova placa: ");
    scanf(" %7s", carros[index].placa);

    printf("\nCadastro atualizado com sucesso!\n");
}

// Excluir carro
void excluir() {
    int codigo, index;
    char confirmacao;

    printf("\n--- EXCLUIR CADASTRO ---\n");
    printf("Digite o código do carro: ");
    scanf("%d", &codigo);

    index = buscarPorCodigo(codigo);

    if (index == -1) {
        printf("\nCarro não encontrado!\n");
        return;
    }

    printf("\nCONFIRMAR EXCLUSÃO:\n");
    printf("Marca: %s\n", carros[index].marca);
    printf("Modelo: %s\n", carros[index].modelo);
    printf("Placa: %s\n", carros[index].placa);

    printf("\nTem certeza que deseja excluir? (s/n): ");
    scanf(" %c", &confirmacao);

    if (confirmacao == 's' || confirmacao == 'S') {
        for (int i = index; i < qtd - 1; i++) {
            carros[i] = carros[i + 1];
        }
        qtd--;
        printf("\nCadastro excluído com sucesso!\n");
    } else {
        printf("\nOperação cancelada.\n");
    }
}

// Listar carros
void listar() {
    printf("\n--- CARROS CADASTRADOS ---\n");
    printf("Total: %d\n\n", qtd);

    if (qtd == 0) {
        printf("Nenhum carro cadastrado.\n");
        return;
    }

    printf("CÓDIGO  %-20s %-20s %-8s\n", "MARCA", "MODELO", "PLACA");
    printf("------------------------------------------------------------\n");

    for (int i = 0; i < qtd; i++) {
        printf("%-8d%-20s%-20s%-8s\n",
               i + 1,
               carros[i].marca,
               carros[i].modelo,
               carros[i].placa);
    }
}

// Main
int main() {
    int op;

    printf("\n----------------------------------------");
    printf("\n    SISTEMA DE CADASTRO DE CARROS");
    printf("\n----------------------------------------\n");

    do {
        printf("\n----------- MENU PRINCIPAL -----------\n");
        printf("1. Cadastrar novo carro\n");
        printf("2. Listar todos os carros\n");
        printf("3. Editar cadastro existente\n");
        printf("4. Excluir cadastro\n");
        printf("0. Sair do sistema\n");
        printf("--------------------------------------\n");
        printf("Opcao: ");
        scanf("%d", &op);
        while(getchar() != '\n');

        switch (op) {
            case 1: cadastrar(); break;
            case 2: listar(); break;
            case 3: editar(); break;
            case 4: excluir(); break;
            case 0: printf("\nEncerrando sistema...\n"); break;
            default: printf("\nOpção inválida! Tente novamente.\n");
        }

    } while (op != 0);

    printf("\nObrigado por utilizar o sistema!\n");
    return 0; // finalizar o programa
}
