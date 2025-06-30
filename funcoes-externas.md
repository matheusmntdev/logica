Funções em Arquivos Separados em C
==================================

Organizar funções em arquivos separados em C é uma prática essencial para criar programas modulares e fáceis de manter. Este guia explica passo a passo como fazer isso, com exemplos completos e dicas para iniciantes. Vamos criar um projeto simples, compilar e executar, tudo de forma clara e sem interrupções.

Por que Separar Funções em Arquivos?
------------------------------------

Separar funções em arquivos diferentes:

* Torna o código mais organizado.
* Facilita a reutilização de funções em outros projetos.
* Permite trabalhar em equipe, com cada pessoa editando partes específicas.

Em C, usamos:

* **Arquivos de cabeçalho** (`.h`): Para declarar os protótipos das funções.
* **Arquivos de implementação** (`.c`): Para definir o código das funções.
* **Arquivo principal** (`main.c`): Para usar as funções.

Estrutura do Projeto
--------------------

Um projeto típico com funções separadas tem esta organização:

    meu_projeto/
    ├── funcoes.h    // Declarações das funções
    ├── funcoes.c    // Implementações das funções
    ├── main.c       // Programa principal

Vamos criar cada arquivo com exemplos práticos.

1\. Arquivo de Cabeçalho (`funcoes.h`)
--------------------------------------

O arquivo `.h` contém os **protótipos** das funções (assinaturas) e usa **include guards** para evitar múltiplas inclusões.

**Conteúdo de `funcoes.h`:**

    #ifndef FUNCOES_H
    #define FUNCOES_H
    
    // Protótipos das funções
    int somar(int a, int b);
    int ehPar(int num);
    void imprimirMensagem();
    
    #endif

\- `#ifndef`, `#define`, `#endif`: Garantem que o arquivo não seja incluído mais de uma vez, evitando erros.

2\. Arquivo de Implementação (`funcoes.c`)
------------------------------------------

O arquivo `.c` contém o código das funções declaradas no `.h`. Ele inclui o arquivo de cabeçalho para garantir consistência.

**Conteúdo de `funcoes.c`:**

    #include "funcoes.h"
    #include <stdio.h>
    
    int somar(int a, int b) {
        return a + b;
    }
    
    int ehPar(int num) {
        return (num % 2 == 0) ? 1 : 0;
    }
    
    void imprimirMensagem() {
        printf("Olá, este é um exemplo!\n");
    }

\- `#include "funcoes.h"`: Inclui o arquivo local com as declarações.

3\. Arquivo Principal (`main.c`)
--------------------------------

O arquivo `main.c` usa as funções definidas em `funcoes.c`, incluindo o arquivo `.h` para acessar os protótipos.

**Conteúdo de `main.c`:**

    #include <stdio.h>
    #include "funcoes.h"
    
    int main() {
        int a = 5, b = 3;
        printf("Soma de %d e %d: %d\n", a, b, somar(a, b));
    
        int num = 8;
        if (ehPar(num)) {
            printf("%d é par\n", num);
        } else {
            printf("%d é ímpar\n", num);
        }
    
        imprimirMensagem();
    
        return 0;
    }

4\. Compilar e Executar
-----------------------

Para compilar um programa com múltiplos arquivos, use o comando abaixo no terminal (com `gcc`, por exemplo):

**Compilar:**

    gcc -o programa main.c funcoes.c

\- `-o programa`: Nome do executável.

\- `main.c funcoes.c`: Lista todos os arquivos `.c` a serem compilados.

**Executar:**

    ./programa

**Saída esperada:**

    Soma de 5 e 3: 8
    8 é par
    Olá, este é um exemplo!

Detalhes Importantes
--------------------

* **Diferença entre `#include < >` e `#include " "`**:
  * `<stdio.h>`: Biblioteca padrão.
  * `"funcoes.h"`: Arquivo local no mesmo diretório.
* **Include Guards**: Evitam erros como "redefinition" se o `.h` for incluído várias vezes.
* **Modularidade**: Cada arquivo `.c` pode ter sua própria lógica, e o `.h` serve como uma "interface".

Exemplo Adicional
-----------------

Vamos criar um exemplo com uma função que calcula o fatorial de um número.

**`fatorial.h`:**

    #ifndef FATORIAL_H
    #define FATORIAL_H
    
    int fatorial(int n);
    
    #endif

**`fatorial.c`:**

    #include "fatorial.h"
    
    int fatorial(int n) {
        if (n <= 1) return 1;
        return n * fatorial(n - 1);
    }

**`main.c`:**

    #include <stdio.h>
    #include "fatorial.h"
    
    int main() {
        int num = 5;
        printf("Fatorial de %d é %d\n", num, fatorial(num));
        return 0;
    }

**Compilar e executar:**

    gcc -o fatorial main.c fatorial.c
    ./fatorial

**Saída:**

    Fatorial de 5 é 120

Dicas para Iniciantes
---------------------

1. **Mantenha os arquivos no mesmo diretório**: Simplifica a compilação.
2. **Use nomes claros**: Ex.: `matematica.h`, `utilidades.c`.
3. **Teste cada função**: Compile e verifique erros após adicionar cada parte.
4. **Evite código no `.h`**: Coloque apenas protótipos, nunca implementações.

Resolução de Problemas Comuns
-----------------------------

* **"undefined reference to..."**: Você esqueceu de incluir um arquivo `.c` na compilação (ex.: `gcc -o programa main.c` em vez de `gcc -o programa main.c funcoes.c`).
* **"cannot find funcoes.h"**: Verifique se o arquivo `.h` está no mesmo diretório ou ajuste o caminho no `#include`.
* **Erros de redefinição**: Confirme que usou **include guards** no `.h`.
