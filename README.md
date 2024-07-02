# Projecto Final Recurso 2024

**UNIVERSIDADE LUSÓFONA DE HUMANIDADES E TECNOLOGIAS**

*Linguagens de Programação I*

# Projecto Final 2024 - Mortal Pandora C_ombat
![image](https://github.com/LP1ULHT/2024ProjectoFinal/assets/98768479/0f0cd02f-d91b-4551-bd2e-bfa1e9bee2ad)



>Na resolução deste projecto deve ser utilizada a Linguagem de Programação C. Para além da correta implementação dos requisitos, tenha em conta os seguintes aspetos:
>- O código apresentado deve ser bem indentado. 
>- O código deve compilar sem erros ou *warnings* utilizando o *gcc* com as seguintes flags:
>- `-g -Wvla -Wall -Wpedantic -Wextra -Wdeclaration-after-statement`
>- Tenha em atenção os nomes dados das variáveis, para que sejam indicadores daquilo que as mesmas vão conter.
>- Não é permitida a utilização de variáveis globais ou estáticas
>- O programa não deve ter *memory leaks*.
>- É obrigatório o uso de listas ligadas.
>- O trabalho deve ser desenvolvido e submetido de forma individual.

**O não cumprimento dos aspetos supracitados incorre uma penalização de 50% da nota.**

>Este exercício deverá ser submetido na plataforma Pandora até às 23h59 de dia 24 Julho e será contabilizado para a nota final da unidade curricular de acordo com os critérios disponibilizados na página da disciplina, concretamente nos slides da primeira aula.

>Todos os trabalhos serão comparados utilizando um sistema de deteção de plágio.
>Todos os trabalhos serão revistos e submetidos a avaliação oral


## Descrição do problema
Neste projeto, vamos implementar um jogo de luta simples em linguagem C, onde um jogador humano contra jogaor computador lutam num épico cenário de porrada da grossa. 
Cada jogador terá a oportunidade de escolher um conjunto de ataques em cada rodada, mas também terá de gerir a sua estamina. 

Além disso, dependendo de sua estamina, o jogador pode activar um *combo*, que é um ataque que causa um número significativo de danos e consome mais estamina.

Como ataque especial, quando um jogador estiver a perder, é possivel andar no tempo para trás, onde retrocedemos o jogo um certo número de ataques.

## Requisitos do jogo

---
### Core
---

**Requisito 1.**
Cada jogador começa com **837** pontos de vida e **791** pontos de estamina. Um jogador nunca pode ter mais do que **999** pontos de vida e **1003** pontos de estamina.

**Requisito 2**
O jogador vence quando o seu oponente tem pontos de vida nulos ou negativos. Neste caso, o jogo termina.

**Requisito 3**
OS jogadores podem empatar quando obtêm ao mesmo tempo pontos de vida nulos ou negativos. Neste caso, o jogo termina.

**Requisito 4**
O número de jogadores é sempre 2. Sendo um jogador humano inserindo dados pelo teclado ou ficheiro.

**Requisito 4.1**
O segundo jogador é o computador, que usa a geração de números aleatórios para fazer sua jogada.

**Requisito 4.2**
O segundo jogador computador faz sempre 5 ataques.

**Requisito 4.3**
O número aleatório é gerado com a função srand usando uma seed (número inteiro) fornecida no início como argumento do programa.

Exemplo para chamar o programa com seed com valor 3:
        *./main 3*

Mais informação sobre a função em:
https://linux.die.net/man/3/srand


**Requisito 4.4**
Se o primeiro numero é entre 1 e 11, gera mais 5 numeros aleatórios (entre 1 e 11) para fazer 5 ataques de acordo com a seguinte tabela.

| **Numero Gerado** | **Nome do Ataque** | **Letra** | 
| --- | --- | --- |
|1| Zarabatana | Z |
|2| Pontapé | P | 
|3| Agarrar | A | 
|4| Estalada | E |
|5| Tombeta | T |
|6| Rasteira | R |
|7| Cotovelada | C |
|8| Bicada | B | 
|9| Onda de Choque | O |
|10| Murro | M |
|11| Defender | D |

**Requisito 4.5**
Se o primeiro numero é entre 12 e 15, o jogador joga um combo de acordo com seguinte tabela,
| Numero | Nome do Combo | Sequência de Letras |
| --- | --- | --- |
|12| Arrozão | ARROZAO |
|13| Dad Bad | DADBAD |
|14| Bife Wellington | STTEACC |
|15| Furacão Thiago | TATAPAAA |

**Requisito 4.6**
Se o primeiro numero é 16, gera mais um numero aleatorio entre 1 e 17. 
O jogador 2 chama então o combo especial TARZANTABORDAX, onde X é o segundo numero aleatório gerado.


**Requisito 5**
Um jogador pode realizar até **5** ataques em cada jogada (não pode escrever mais de **5** caracteres).

**Requisito 6**
Um jogador pode realizar apenas 1 combo em cada jogada (neste caso, escreve mais de **5** caracteres).

**Requisito 7**
Não se pode combinar ataques com combos.

**Requisito 8**
Cada jogador faz uma jogada por vez, alternando suas tentativas.

---
### Ataque e Combos
---

**Requisito 9**
Existem os seguintes ataques correspondentes a uma letra conforme a seguinte tabela:


| **Nome do Ataque** | **Letra** |
| --- | --- |
| Zarabatana | Z |
| Pontapé | P | 
| Agarrar | A | 
| Estalada | E |
| Tombeta | T |
| Rasteira | R |
| Cotovelada | C |
| Bicada | B | 
| Onda de Choque | O |
| Murro | M |
| Defender | D |
| Descansa | |

**Requisito 10**
O jogo rege sob efeito "Pedra, Papel, Tesoura", isto é, um ataque tem um determinado efeito de acordo com ataque do outro jogador. Os efeitos sao descritos na seguinte tabela.
![Screenshot 2024-05-16 001812](https://github.com/LP1ULHT/2024ProjectoFinal/assets/1611372/aa6eab03-e46b-488c-89d6-07e86430d2b6)


**Requisito 11**
Se valor é positivo jogador1 tira esse valor positivo em pontos à vida do jogador 2
Se valor é negativo jogador2 tira esse valor positivo em pontos à vida do jogador 1

        
**Requisito 12**
Cada ataque efectuado pelo jogador faz perder 23 pontos de estamina (com exceção do *Defender* e *Descansar*). O valor mínimo da estamina é zero. O jogador pode continuar a realizar ataques mesmo com estamina a zero. 

**Requisito 13**
À medida que a estamina diminui, o jogador perde mais vida ao sofrer ataques do oponente, de acordo com a seguinte lógica:

 - **Estamina > 750** - Perde vida que é descrita na tabela do Requisito 10
 
 - **Estamina > 500** - Perde **dobro** da vida que é descrita na tabela do Requisito 10
 
 - **Estamina > 250** - Perde **triplo** da vida que é descrita na tabela do Requisito 10 

 - **Estamina < 250** - Perde **quadruplo** vida que é descrita na tabela do Requisito 10 

*Combos não são afetados pelo fator multiplicativo.*

**Requisito 14**
Quando um jogador utilizar o ataque *Defender*, ele **sobe 7 pontos** de estamina e recupera **13** pontos de vida. A recuperação de vida também é afetada pelo fator multiplicativo.
- Exemplo: Se o jogador estiver com estamina abaixo de 250, recupera então 28 pontos de vida.

**Requisito 15**
Caso haja uma quantidade diferente de ataques entre os jogadores, os ataques não explicitados devem ser considerados como *Descansar*. 
Quando acontece *Descansar*  o jogador recupera 25 de estamina. 
Não existe letra explicíta para efectuar o *Descansar*

- Exemplo 1: o jogador1 usa *"AAO"* e o jogador2 usa *"ZZ"*. Como o jogador1 usou mais ataques que o jogador2, deve-se considerar que a *Onda de Choque* do jogador1 foi respondida com um *Descansar* pelo jogador2. No total serão realizados 3 ataques no turno.

- Exemplo 2: jogador1 usa *"DADBAD"* (um combo) e jogador2 usa *"MZZZ"*. O jogador1 usou um combo (e não pode usá-lo com outros ataques) e o jogador2 usou quatro ataques.
Deve-se descartar todos os ataques do jogador2. Considerar que o combo DADBAD do jogador1 foi respondida por um *Descansar* do jogador2.

- Exemplo 3: Se os dois jogadores usarem um combo, o resultado é que o efeito do combo ocorrer para os dois jogadores. Se o jogador1 usar o *"DADBAD"* e o jogador2 usar o *"DADBAD"*, ambos os jogadores vão perder 400 de estamina e 400 pontos de vida.

- Exemplo 4: Se jogador1 ataca com "AA" e jogador2 joga com "BB", não existe diferença entre o número ataques, logo não acontece descansar.

---


**Requisito 16**
O jogador pode ativar combos durante o jogo, quando certas sequências de letras forem escritas. 
Um ataque combo faz o jogador gastar estamina. 

As combinações e os pontos que reduzem a vida/estamina do oponente são mostrados abaixo:

| Nome do Combo | Sequência de Letras | Pontos Vida Tirado ao oponente | Estamina Perdida |
| --- | --- | --- | --- |
| Arrozão | ARROZAO | 500 | 500 |
| Dad Bad | DADBAD | 400 | 400 |
| Bife Wellington | STTEACC | 300 | 300 |
| Furacão Thiago | TATAPAAA | 200 | 200 |

**Requisito 16.1**
Um jogador só pode fazer um combo quando tem mais do que 750 de estamina. Se não tem estaminha suficiente, o combo se escrito é ignorado e se escreve a mensagem *Estamina Insuficiente* 

**Requisito 16.2**
Existe um combo especial chamado *Lucio Tarzan Reversal*, que é ativado quando as letras *"TARZANTABORDA"* são escritas. Este combo permite que o jogador retroceda no tempo, revertendo o jogo para X ataques anteriores, onde X é o número especificado pelo jogador.

- Exemplo: Se o jogador quiser retroceder 3 ataques, ele escreve "TARZANTABORDA3".

*O conceito por trás disso é apagar os X últimos elementos da lista ligada, forçando cada elemento da lista a conter o valor da vida e da estamina do jogador.*

**Requisito 16.3**
Se o valor X de ataques é superior ao numero maximo que jogadas ocorridas, o jogo volta para o início.

**Requisito 16.4**
O jogador só pode fazer o combo especial *"TARZANTABORDA"* quando a estamina for maior que 500 e menor que 900.

### Implementação
---

**Requisito 18**
O histórico de ataques realizados, pontos de vida e pontos de estamina de cada jogador é obrigatoriamente guardado numa lista ligada.

**Requisito 19**
Antes de um jogador fazer sua jogada, os últimos **17** ataques realizados pelo jogador são impressos no ecrã.

**Requisito 20**
Antes de um jogador fazer sua jogada, os pontos de sua vida e estamina são impressos.

**Requisito 21**
Se o utilizador escrever algo inválido ou fora destes requisitos, deve escrever "Entrada invalida" e termina o jogo!

**Requisito 22.**
Pode se inserir as jogadas por um ficheiro. Ver exemplo no fim do enunciado.

**Requisito 23**
Cada linha do ficheiro representa uma jogada tal como descrito no requisito 5, 6, 8 e 16.

**Requisito 24**
Cada linha corresponde a uma jogada de **5** ataques ou um combo do jogador.
Se a linha contem um ataque ou letra invalido o programa termina.
Se a linha contem um combo com estamina suficiente, a linha é ignorada, e a **próxima linha é lida como os input corretos do jogador**.

**Requisito 25**
O jogo contém os seguintes códigos secretos que, quando escritos, produzem os seguintes efeitos:

- Modo-Jesus - Reinício do jogo, ambos os jogadores voltam a ter estamina a 791 e vida a 837 e no histórico não consta nenhum golpe.

- Alt-F4*X* - Jogador 1 - Restaura a estamina a X pontos. X deve ser um número positivo.

- Kebab*X* - Jogador 2 - Restaura a estamina a X pontos. X deve ser um número positivo.

- Hiroshima*X* - Jogador 1 - Restaura a vida a X pontos. X deve ser um número positivo.

- Nood-Mode*X* - Jogador 2 - Restaura a vida a X pontos. X deve ser um número positivo.

---
### Exemplos

Usar como referencia exemplos dado em https://github.com/LP1ULHT/2024ProjectoFinal

## FAQ ##
Ver https://github.com/LP1ULHT/2024ProjectoFinal

