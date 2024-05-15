# Apoio Projeto \#2

Enunciado de apoio à entrega do *Checkpoint \#2*:

## Checkpoint \#2 - 📅 27 de maio, 2ª-feira, 16H

**Deliverable:**

- Inclusão dos ADTs (coleções) List e Map na estrutura do projeto; 
- Importação de atletas (LOAD_A) e medalhas (LOAD_M) para as coleções respetivas; 
- Implementação inicial de CLEAR e QUIT; 
- Implementação de SHOW_ALL, SHOW_YEAR e SHOW_AGE. 
- Documentação doxygen e respetiva geração da mesma na pasta “html”. 

**Submissão ZIP (conteúdo):**  Projeto VS Code (cópia do repositório).

## Versionamento de código

Todo o trabalho desenvolvido deve estar versionado no repositório do grupo.

## Inclusão dos ADTs na estrutura do projeto

Necessitará de copiar os ficheiros respetivos aos ADT List e Map para a sua estrutura do projeto VS Code.

Pode encontrá-los nos *templates* utilizados nas aulas, ou então centralmente em:

- <https://github.com/brunomnsilva/AbstractDataTypesInC>

Os ficheiros necessários são:

- ADT List: `list.h`, `listElem.h`, `listElem.c` e uma implementação (qualquer); mas sugere-se a implementação `listArrayList.c` (nas TP depois veremos porquê);

- ADT Map: `map.h`, `mapElem.h`, `mapElem.c` e uma implementação (qualquer) entre `mapArrayList.c` ou `mapLinkedList.c`.

Necessitará também de criar o módulo `stringWrap` de acordo com os slides [ADENDA - StringWrap](https://moodle.ips.pt/2324/pluginfile.php/138113/mod_label/intro/16_Colecoes_GuardarStrings_ADENDA.pdf) no Moodle.

### Parameterização dos ADT

De acordo com o enunciado, deverá parameterizar:

- o ADT List por forma a guardar elementos do tipo `Medal`;

- o ADT Map por forma a guardar tuplos onde `ValueElem` é do tipo `Athlete` e o `KeyElem` de um tipo que permita guardar uma string, i.e., `StringWrap` (id do atleta - a chave do dicionário); 

Não se esqueça de ajustar as funções `listElemPrint`, `mapKeyPrint`, `mapValuePrint` e `mapKeyCompare` de acordo.

### Makefile

Complemente o *makefile*.

## Estrutura base do programa

A partir da estrutura existente do *checkpoint #1*, adicione instâncias de ADT List e ADT Map ao seu programa, e.g.:

```cpp
#include <stdio.h>
#include "list.h"
#include "map.h"

int main() {

    PtList medals = listCreate();
    PtMap athletes = mapCreate();

    // Command line interpreter from checkpoint #1
    // while( ... ) { ... }

    // TODO: free ADT resources/memory

    return 0;
}
```

## Importação de atletas e medalhas

Sugere-se a criação de um módulo `import` (para evitar dependências circulares) que contenha as funções:

- `PtList importMedals()`, e;
- `PtMap importAthletes()`.

Adapte os exemplos fornecidos nas aulas TP para este objetivo:

- **[13] Introdução aos ADT do género coleção e utilização do ADT List** (ver Soluções)

- **[16] Utilização de  ADT Map** (ver Solução Exercício 2)

## Importação e implementação de CLEAR e QUIT

No seu interpretador de comandos complemente a resposta aos comandos `LOAD_A`, `LOAD_M` e `CLEAR`. A opção `QUIT` pode simplesmente sair do ciclo do interpretador e chegar às instruções assinaladas anteriormente com `// TODO: free ADT resources/memory`, onde deverá libertar a memória associada às instâncias existentes das coleções.

## Implementação de SHOW_ALL, SHOW_YEAR e SHOW_AGE. 

O propósito destas funções está explicado no enunciado. 

Sugere-se a existência de um módulo, e.g., `operations` para as conter; mas tem liberdade total para criar outra estrutura de módulos.

**Note que qualquer uma destas operações resultará na impressão de um conjunto de atletas.**

Poderá fazer uso de uma função "genérica" (e.g., módulo `athlete`) que imprima um array de atletas de forma paginada, e.g.,:

```cpp
void athletePrintArrayPaginated(Athlete *arr, int arrSize) {
    //...
}
```

### Como aceder a um conjunto de atletas e imprimi-lo?

Dado que os atletas estão guardados como "valores" do ADT Map, poderá obter essa informação com:

```cpp
Athlete *arr = mapValues(athletes); 
//terá de libertar este array, quando deixar de o necessitar

int athleteCount;
mapSize(athletes, &athleteCount);

athletePrintArrayPaginated(arr, athleteCount);
```

### SHOW_ALL

Esta operação irá envolver pegar num array de atletas, ordená-lo alfabeticamente e imprimi-lo de forma paginada.

Sugere-se uma função autónoma para ordenação.

### SHOW_YEAR e SHOW_AGE

Estas operações irão envolver "filtrar" um conjunto de atletas de acordo com um critério específico.

Se pensar bem nisto, quererá evitar repetição de código; se já tem funções para ordenar e imprimir um conjunto de atletas de forma paginada, necessita apenas de funções para "filtrar". O uso coordenado de todas estas funções irão resultar nas funcionalidades pretendidas.

A título sugestivo, pode ter uma função que faz a filtragem por ano de nascimento:

```cpp
/**
 * @brief Filters an array of athletes to include only those born in a specific year.
 *
 * This function takes an array of Athlete structures and filters it based on
 * a specified birth year. The resulting array contains only the athletes
 * whose birth year matches the specified year.
 *
 * @param arr [in] Pointer to the array of Athlete structures to be filtered.
 * @param arrSize [in] The size of the input array.
 * @param filterArrSize [out] Pointer to an integer where the size of the filtered array will be stored.
 * @return Pointer to a newly allocated array of Athlete structures containing the filtered athletes.
 *
 * @note The caller is responsible for freeing the memory allocated for the returned array.
 *
 * Example usage:
 * @code
 * int newSize;
 * Athlete *filteredArr = filterAthleteArrayByBirthYear(athletes, athleteCount, &newSize);
 * // Use filteredArr
 * free(filteredArr); // Remember to free the allocated memory
 * @endcode
 */
Athlete* athleteFilterArrayByBirthYear(Athlete *arr, int arrSize, int *filterArrSize);
```


## Documentação *doxygen*

Deve existir documentação:

- nos cabeçalhos de cada ficheiro; 
- em todas as funções definidas nos *header files*
- em todas as funções no `main.c`.
