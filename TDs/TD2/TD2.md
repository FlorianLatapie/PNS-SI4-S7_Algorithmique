# TD2

## Exercice 1

Décrire de manière détaillée une machine de Turing déterministe à un seul ruban qui
reconnaît le langage des mots composés d’un nombre en binaire qui contient exactement un
0 et qui n’est ni en première ni en dernière position.
Exemples de mots du langage : 11011111 ; 101111111 ; 11111101 ; 101

```mermaid
graph TB
    q0((q0)) --> | 1/1/D | q1((q1))
    q1((q1)) --> | 1/1/D | q1((q1))
    q1((q1)) --> | 0/0/D | q2((q2))
    q2((q2)) --> | 1/1/D | q3((q3))
    q3((q3)) --> | 1/1/D | q3((q3))
    q3((q3)) --> | B/B/S | qf((qf))

    %% etat poubelle
    q0((q0)) --> | 0/0/S<br/>B/B/S | poubelle((poubelle))
    q1((q1)) --> | B/B/S | poubelle((poubelle))
    q2((q2)) --> | 0/0/S<br/>B/B/S | poubelle((poubelle))
    q3((q3)) --> | 0/0/S | poubelle((poubelle))
```

Sans l'état poubelle

```mermaid
graph LR
    q0((q0)) --> | 1/1/D | q1((q1))
    q1((q1)) --> | 1/1/D | q1((q1))
    q1((q1)) --> | 0/0/D | q2((q2))
    q2((q2)) --> | 1/1/D | q3((q3))
    q3((q3)) --> | 1/1/D | q3((q3))
    q3((q3)) --> | B/B/S | qf((qf))
```

## Exercice 2

Décrire de manière détaillée une machine de Turing déterministe à deux rubans qui reconnaît
le langage des mots composés d’un nombre en binaire répété deux fois.
Exemples de mots du langage : 011011 ; 1111 ; 101011101011 ; 000111000111

```mermaid
graph LR
    q0((q0)) --> | 1/1/D<br/>0/0/D | q0((q0))
    q0((q0)) --> | b/b/D | q1((q1))
    q1((q1)) --> | 0/0/G<br/>0/1/G<br/>1/0/G<br/>1/1/G | q2((q2))
    q2((q2)) --> | 0/0/G/S<br/>0/1/G/S<br/>1/0/G/S<br/>1/1/G/S | q1((q1))
    q2((q2)) --> | b/b/D | q3((q3))
    q3((q3)) --> | 1/1/D<br/>0/0/D | q3((q3))
    q3((q3)) --> | 0/b/D<br/>1/b/D | qf((qf))
```

Même question avec une machine de Turing déterministe à un seul ruban.

```mermaid
graph TB
    q0((q0)) --> | 0/x/D<br/>1/y/D | q1((q1))
    q0((q0)) --> | x/x/D<br/>y/y/D | q4((q4))

    q1((q1)) --> | 0/0/D<br/>1/1/D | q1((q1))
    q1((q1)) --> | b/b/G<br/>x/x/G<br/>y/y/G | q2((q2))

    q2((q2)) --> | 0/x/G<br/>1/y/G | q3((q3))

    q3((q3)) --> | 0/0/G<br/>1/1/G | q3((q3))
    q3((q3)) --> | x/x/D<br/>y/y/D | q0((q0))

    q4((q4)) --> | y/1/G | q5((q5))
    q4((q4)) --> | x/0/G | q9((q9))

    q5((q5)) --> | x/x/G<br/>y/y/G | q5((q5))
    q5((q5)) --> | b/b/D<br/>1/1/D<br/>0/0/D | q6((q6))

    q6((q6)) --> | y/1/D | q7((q7))

    q7((q7)) --> | x/x/D<br/>y/y/D | q7((q7))
    q7((q7)) --> | 0/0/D<br/>1/1/D | q8((q8))

    q8((q8)) --> | 0/0/D<br/>1/1/D | q8((q8))
    q8((q8)) --> | x/x/S<br/>y/y/S | q4((q4))
    q8((q8)) --> | 0/0/D<br/>1/1/D | qf((qf))

    q9((q9)) --> | x/x/G<br/>y/y/G | q9((q9))
    q9((q9)) --> | b/b/D<br/>1/1/D<br/>0/0/D | q10((q10))

    q10((q10)) --> | x/0/D | q7((q7))
```

## Exercice 3

Nous considérons le problème du calcul de la longueur en binaire d’un mot sur l’alphabet {a, b}
donné en entrée.

- Décrire une machine de Turing à deux rubans qui effectue le calcul et évaluer sa
  complexité.
- Même question avec un seul ruban.
- Comment améliorer la complexité de votre machine précédente (à un seul ruban) afin
  d’obtenir une complexité de O(n log n) ?
- En déduire une machine à deux rubans de complexité linéaire ?

```mermaid
graph LR
    q0((q0)) --> | a/a/D | q0((q0))
    q0((q0)) --> | B/B/G | q1((q1))
    q1((q1)) --> | X/X/G<br/>0/0/G<br/>1/1/G | q1((q1))
    q1((q1)) --> | B/0/D | q2((q2))
    q1((q1)) --> | a/X/G | q3((q3))
    q2((q2)) --> | X/X/D<br/>0/0/D<br/>1/1/D | q2((q2))
    q2((q2)) --> | B/B/S | qf((qf))
    q2((q2)) --> | a/a/D | q0((q0))
    q3((q3)) --> | X/X/G<br/>0/0/G<br/>1/1/G | q3((q3))
    q3((q3)) --> | a/a/G | q1((q1))
    q3((q3)) --> | B/1/G | q2((q2))
```

## Exercice 4

Décrire de manière détaillée une machine de Turing déterministe à deux rubans qui reconnaît
le langage des mots $\{0^k1^k : k > 0\}$. Quelle est la complexité de votre machine ?
Premiers mots du langage : 01 ; 0011 ; 000111

```mermaid
graph LR
    q0((q0)) --> | 0,B/0,0/DD | q0((q0))
    q0((q0)) --> | 1,B/1,B/S,G | q1((q1))
    q1((q1)) --> | 1,0/1,0/D,G | q1((q1))
    q1((q1)) --> | B,B/B,B/S,S | qf((qf))
```

## Exercice 5

Décrire de manière détaillée une machine de Turing déterministe à deux rubans qui reconnaît
le langage des mots (à une lettre a)  dont la longueur est un carré parfait.
Premiers mots du langage : a ; aaaa ; aaaaaaaaa ; aaaaaaaaaaaaaaaa

```mermaid
graph LR
    q0((q0)) --> | a,B/A,X/D,D | q1((q1))
    q1((q1)) --> | a,x/a,X/S,D | q1((q1))
    q1((q1)) --> | B,B/B,B/S,S | qf1((qf1))
    q1((q1)) --> | a,B/a,X/S,D | q2((q2))
    q2((q2)) --> | a,B/a,X/D,G | q3((q3))
    q3((q3)) --> | a,X/a,X/D,G | q3((q3))
    q3((q3)) --> | a,B/a,B/S,D | q1((q1))
    q3((q3)) --> | B,B/B,B/S,S | qf1((qf1))
```

## Exercice 6

Décrire de manière détaillée une machine de Turing déterministe qui fait l’addition de deux
nombres binaires. Le nombre de rubans est trois. Vous pourrez également écrire une machine
de Turing avec deux rubans et ensuite un ruban.

```mermaid
graph TB
    q0((q0)) --> | 0,B,B/B,0,B/D,D,S<br/>1,B,B/B,1,B/D,D,S | q0((q0))
    q0((q0)) --> | +,B,B/B,B,B/D,S,S | q1((q1))

    q1((q1)) --> | 0,B,B/B,B,0/D,S,D<br/>1,B,B/B,B,1/D,S,D | q1((q1))
    q1((q1)) --> | B,B,B/B,B,B/S,G,G | q2((q2))
    
    q2((q2)) --> | B,0,0/0,0,0/G,G,G<br/>B,1,0/1,1,0/G,G,G<br/>B,0,1/1,0,1/G,G,G<br/>B,B,0/0,B,0/G,G,G<br/>B,0,B/0,0,B/G,G,G<br/>B,B,1/1,B,1/G,G,G<br/>B,B,1/1,B,1/G,G,G<br/>B,1,B/1,1,B/G,G,G | q2((q2))
    q2((q2)) --> | B,1,1/0,1,1/G,G,G | q3((q3))
    q2((q2)) --> | B,B,B/B,B,B/S,S,S | qf((qf))

    q3((q3)) --> | B,0,1/0,0,1/G,G,G<br/>B,1,0/0,1,0/G,G,G<br/>B,1,1/1,1,1/G,G,G<br/>B,B,1/0,B,1/G,G,G<br/>B,1,B/0,1,B/G,G,G | q3((q3))
    q3((q3)) --> | B,0,0/1,0,0/G,G,G<br/>B,B,0/1,B,0/G,G,G<br/>B,0,B/1,0,B/G,G,G<br/>B,B,B/1,B,B/G,G,G | q2((q2))
```

## Exercice 7

Décrire de manière détaillée une machine de Turing déterministe à un seul ruban qui trie les
lettres d’un mot écrit sur l’alphabet {x, y}.
Exemple : si le mot est xyxxy alors le résultat sera xxxyy

Même question avec l’alphabet {x,y,z}.
