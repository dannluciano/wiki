# Busca binária em resposta

A **busca binária tradicional** é um algoritmo de pesquisa em vetores usando o paradigma divisão e conquista, para funcionar o vetor precisa estar ordenado (crescente ou decrescente), se você não conhece recomendo pesquisar sobre para entender melhor oque será explicado.

A **busca binária em resposta** consegue resolver problemas além de uma simples pesquisa, ela trabalha diretamente no valor do resultado, o algoritmo vai "chutando" até achar a resposta para o seu problema, um exemplo comum é achar a raiz quadrada de um número.

Vamos resolver o problema __“Aggressive cows”__ para entender.

**link do problema:** [AGGRCOW](https://www.spoj.com/problems/AGGRCOW/)

# Problema:
O fazendeiro John construiu um estábulo bem longo, com N (2 <= N <= 100,000) baias. As baias estão alocadas nas seguintes posições x1,...,xN (0 <= xi <= 1,000,000,000).
As vacas dele C (2 <= C <= N) não gostam desse layout e ficaram agressivas uma com a outra quando colocadas em um estábulo. Para impedir que as vacas se machuquem, John quer atribuir as vacas às baias, de modo que a distância mínima entre duas delas seja a maior possível. Qual é a maior distância mínima?
## Entrada
t - o número de casos de teste e, a seguir, t casos de teste.
* Linha 1: Dois números inteiros separados por espaço: N e C
* Linhas 2..N + 1: A linha i + 1 contém um local de paralisação inteiro, xi
## Resultado
Para cada caso de teste, imprima um número inteiro: a maior distância mínima.
### Caso de entrada:
>1
>5 3
>1 2 8 4 9

### Saida:
>3

**Abaixo está o código feito em c++ comentado.**
```
#include <bits/stdc++.h>
using namespace std;
int main() {
  
  int a;
 
  cin >> a; //recebendo o número de casos de teste
 
  for(int i = 0; i < a; i++){
    int n, c;
    cin >> n >> c; //recebendo N e C

    int baias[n + 1];

    for(int j = 1; j <= n; j++){
      cin >> baias[j];
    }
 
    sort(baias + 1, baias + n); //ordenando as posições das baias
 
```
Até agora só **coletei os dados** da questão e ordenei as baias em ordem **não** decrescente, nada demais.

```
    int left = 1;//left começa com 1 que é o valor mínimo de distância entre duas baias.

    int right = baias[n];//right é inicializado com o valor da baia mais a direita.
```
Essas duas **variáveis** “left” e “right” serão o “raio” de busca, já que o **menor** valor possível de distância entre duas vacas tem que ser 1 e o **máximo** é a distância da última baia (poderia ser baias[n] - baias[1]), resumindo, a resposta está entre essas duas variáveis.
```
    int fm = -1;

    while(left <= right){
      int meio = (left + right) / 2;//a variável “meio” vai chutar algum valor da metade de left + right

      int dis = 0;//a variável "dis" vai fazer a contagem e a divisão das vacas

      int longe = 1;//essa variável vai ser a responsável para dizer quantas vacas conseguiram bater a meta do “meio”
 
      //a variável "j" começa com 2 pois a primeira vaca já foi colocada na primeira baia
      for(int j = 2; j <= n; j++){
        //vai verificar se a distância é maior ou igual ao valor pela variável "meio" para colocar uma vaca.
        if(dis >= meio){
          dis = 0;
          longe++;
        }
        dis += baias[j] - baias[j - 1];
      }
```
A variável “dis” calcula a **distância da baia anterior até baia atual**, caso seja possível ter uma vaca na baia atual, **zera** a distancia, se não, vai para a próxima baia.
```
      //é preciso verificar se a última posição pode ser colocada mais uma vaca
      if(dis >= meio){
          dis = 0;
          longe++;
      }
      
      //caso todas as vacas tenham sido colocadas a pelo menos ao que foi "chutado" pelo "meio", vamos tentar aumentar ainda mais a distância entre elas.
      if(longe >= c){
        left = meio + 1;
        fm = meio;//guardei o valor do valor chutado pois é uma possivel melhor resposta
      }else{
        right = meio - 1;//o valor "chutado" foi muito alto, temos que tentar um valor menor
      }
    }
    cout << fm << endl;//imprimindo a resposta
  }
}
```

Obs: **Preste atenção** como está implementado a busca binária pois é fácil dar algum erro ou não entregar o resultado que foi proposto.

#### Referencias:
https://noic.com.br/materiais-informatica/curso/techniques-01/
https://www.topcoder.com/community/competitive-programming/tutorials/binary-search

#### Escrito por: [Walex henrique](https://github.com/walexhenrique)
**Lembrando que sou iniciante em programação.**

#### Algumas questões para treino:

https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/  https://leetcode.com/problems/heaters/
https://leetcode.com/problems/sqrtx/

**Tente usar busca binária em resposta.**