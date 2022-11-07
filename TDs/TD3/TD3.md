# TD3

Nom : **Somme de Sous-Ensembles**  
Instance : un ensemble fini $E$, une taille $s(e) \in N$ pour chaque $e \in E$ et une capacité $C \in N$.  
Question : existe-t-il un sous-ensemble $E' \subseteq E$ tel que la somme des éléments de $E' = C$ ?

## Exercice 1

Montrer que Somme de Sous-Ensembles est dans NP en décrivant une machine de Turing non-déterministe.

### Réponse exercice 1

- Machine de Turing non déterministe.  
  On fait une machine de Turing à 3 états on prend l'élément et on ne prend pas l'élément, ainsi que l'état initial.
  À chaque élément de e on fait respectivement les deux choix. Si sur le deuxième on a 0 la réponse est oui.

  ```mermaid
  graph LR
    a(( )) --> | je choisis e | b(( ))
    a(( )) --> | je ne choisis pas e | c(( ))
  ```

- Algorithme de vérification d'une solution en temps polynomial.  
  Somme des éléments en entrée d'une taille $n$, complexité en temps $O(n)$

Le problème est donc NP

---

Soient les problèmes suivants.

Nom : **Chaîne Hamiltionienne**  
Instance : Un graphe fini $G = (V, E)$ représenté sous forme de listes d’adjacence.  
Question : Le graphe admet-il une chaîne Hamiltonienne (c’est-à-dire qui passe une et une seule fois par tous les sommets) ?

Nom : **Cycle Hamiltonien**  
Instance : Un graphe fini $G = (V, E)$ représenté sous forme de listes d’adjacence.  
Question : Le graphe admet-il un cycle Hamiltonien (c’est-à-dire qui passe une et une seule fois par tous les sommets) ?

Nom : **Chemin Hamiltionien**  
Instance : Un graphe orienté fini $G = (V, E)$ représenté sous forme de listes d’adjacence.  
Question : Le graphe admet-il un chemin Hamiltonien (c’est-à-dire qui passe une et une seule fois par tous les sommets) ?

Nom : **Circuit Hamiltonien**  
Instance : Un graphe orienté fini $G = (V, E)$ représenté sous forme de listes d’adjacence.  
Question : Le graphe admet-il un circuit Hamiltonien (c’est-à-dire qui passe une et une seule fois par tous les sommets) ?

## Exercice 2

1. Chemin Hamiltionien $\propto$ circuit Hamiltonien
2. Cycle Hamiltonien $\propto$ circuit Hamiltonien
3. Chaîne Hamiltionienne $\propto$ chemin Hamiltionien
4. Cycle Hamiltonien $\propto$ chaîne Hamiltionienne
5. Circuit Hamiltonien $\propto$ chemin Hamiltionien
6. Circuit Hamiltonien $\propto$ cycle Hamiltonien
7. Chemin Hamiltionien $\propto$ chaîne Hamiltionienne

## Méthodologie pour "Q NP-Complet ?"

$P \propto Q$, $P$ NP-Complet  
$\Rightarrow$ si P est vrai alors Q est vrai  
$\Rightarrow$ si P est faux alors Q est faux  
$\Rightarrow$ Réduction en temps polynomial

### Réponses exercice 2

1. **Chemin Hamiltionien $\propto$ circuit Hamiltonien**  
    Pour tout $G = (V, E) \xrightarrow[\text{Transformation polynomiale}]{} G' = (V', E')$

    $V' = V \cup \{x_0\}$  
    $E' = E \cup \{(x_0, v), (v, x_0), v \in V\}$

    $\Rightarrow$ On suppose qu'il existe un chemin Hamiltonien dans $G$  
    Soit $(v_0, v_1, \dots, v_n)$ avec $n = |V|$ ce chemin.  
    Construisons un circuit dans $G' : (x_0, v_0, v_1, \dots, v_n, x)$ car $(x_0, v_0)$ et $(v_n, x_0)$ sont des arcs de $E$

    $\Leftarrow$ S'il existe un circuit Hamiltonien de $G'$, alors en enelvant l'arc $x_0$ de ce circuit, on obtient un chemin Hamiltionien dans G.

    On a montré qu'il existe un chemin Hamiltionien dans $G$ si et seulement s'il existe un circuit hamiltonien dans $G$.

    Donc chemin Hamiltionien $\propto$ circuit Hamiltonien

2. **Cycle Hamiltonien $\propto$ circuit Hamiltonien**  
    Pour tout $G = (V, E)$

    $V' = V$  
    $E' = E \cup \{(v_0, v_1), \exists v_0, v_1 \in V, (v_1, v_0) \in E\}$

    $\Rightarrow$ On suppose qu'il existe un cycle Hamiltonien dans $G$ alors on a un circuit Hamiltonien dans $G'$ car les arcs du cycle dans $G$ sont symétriques.

    $\Leftarrow$ On suppose qu'il existe un cycle Hamiltonien dans $G'$ alors on a un circuit Hamiltonien dans $G$

    Donc cycle Hamiltonien $\propto$ circuit Hamiltonien

3. **Chaîne Hamiltionienne $\propto$ chemin Hamiltionien**  
    Même transformation que dans la question 2  
    Donc chaîne Hamiltionienne $\propto$ chemin Hamiltionien

4. **Cycle Hamiltonien $\propto$ chaîne Hamiltionienne**  
    Pour tout $G = (V, E)$  
    $V' = V \cup \{x', y, y'\}$  
    $E' = E \cup \{(y, v), v \in N_g(x)\} \cup \{x,x'\} \cup \{y, y'\}$

    $\Rightarrow$ Soit $(x, v_1, \dots, v_{n-1})$ un Cycle Hamiltonien dans $G$ $n = |V|$

    Considérons la chaine suivante : $(x', x, v_1, \dots, v_{n-1}, y, y')$  
    Cette chaine est hamiltonienne car :
    - $\{x', x\} \in E'$
    - $\{x, v_1\} \in E'$
    - $\{v_i, v_{i+1}\} \in E'$ pout $i$ de $1$ à $n-2$
    - $\{v_{n-1}, y\} \in E'$ car les voisins de $x$ sont les voisins de $y$
    - $\{y, y'\} \in E'$

    $\Leftarrow$ S'il existe une chaine Hamiltonienne dans $G'$, dont les deux extrémités sont $x'$ et $y'$.  
    Soit $(x', x, v_1, \dots, v_{n-1}, y, y')$ une chaine hamiltonienne  
    Comme $\{y, v_{n-1}\} \in E'$  
    Donc $\{x, v_{n-1}\} \in E$  
    Finalement $(x, v_1, \dots, v_{n-1})$ est un Cycle Hamiltonien de $G$

5. **Circuit Hamiltonien $\propto$ chemin Hamiltonien**  
    Pour tout $G = (V, E)$  
    $V' = V \cup \{y, z\}$  
    $E' = E \cup \{(y, v), v \in N_{G,S}(x)\} \cup \{x, z\}$  
    $\Rightarrow$ Soit $(x, v_1, \dots, v_{n-1})$ un circuit Hamiltonien de $G$  
    Le chemin $(y, v_1, \dots, v_{n-1}, x, z)$ est hamiltonien car :
    - $(y, v_1) \in E'$ car $(x, v_1) \in E'$ par hypothèse
    - $(x, z) \in E'$  

    $\Leftarrow$ Soit $(y, v_1, \dots, v_{n-1}, x, z)$ un chemin hamiltonien  
    On montre que $(x, v_1, \dots, v_{n-1}, x)$ est un circuit Hamiltonien de car $(x, v_1) \in E'$ par construction de $G'$  
    (les voisins sortant de $y$ sont les voisins sortants de $x$)

6. **Circuit Hamiltonien $\propto$ cycle Hamiltonien**  

    Non valide :

    ```mermaid
    graph LR
        a(( )) --> b(( ))
        a(( )) --> c
        c(( )) --> b
    ```

    Valide :

    ```mermaid
    graph LR 
        a(( )) --- b(( ))
        a(( )) --- c
        c(( )) --- b
    ```

    Si on a un circuit alors il y a forcément un cycle :

    ![image](./r%C3%A9ponse%202.6.jpg)

    Transformation d'un graphe dirigé en un graphe non dirigé :

    - On transforme chaque noeud du problème initial en 3 noeuds : un qui gère les entrées, un qui gère les sorties et un dernier au milieu reliant les deux précédents. Ce dernier noeud permet de bien vérifier une entrée puis une sortie.
    - La transformation est polynomiale.

7. **Circuit Hamiltonien $\propto$ chemin Hamiltonien**  
    Deux possibilités :
    - Faire la même transformation que dans la question 6
    - Utiliser la transitivité :  
        Chemin Hamiltonien $\propto$ Circuit Hamiltonien $\propto$ Cycle Hamiltonien $\propto$ Chaîne Hamiltonienne

---

Pour la suite, nous pourrons utiliser la NP-difficulté des problèmes suivants : chemin Hamiltionien, circuit Hamiltonien, cycle Hamiltonien, chaîne Hamiltionienne, Clique, Partition, 3-Dimensional Matching, X3-SAT.

Nom : **Clique**  
Instance : un graphe fini $G(V, E)$, et un entier positif $C \leq |V|$  
Question : le graphe admet-il une clique (sous-graphe complet) de cardinalité au moins C ?

Nom : **Partition**  
Instance : un ensemble fini d'entiers non-négatifs $A$.  
Question : existe-t-il une partition de $A$ en deux ensembles $A'$ et $A''$, telle que la somme des éléments de $A'$ soit égale à la somme des éléments de $A''$ ?

Nom : **3-Dimensional Matching**  
Instance : un ensemble $M$ de triplets $(w, x, y)$, avec $w$, $x$ et $y$ des éléments de trois ensembles $W$, $X$, $Y$ de même cardinalité $q$.  
Question : $M$ contient-il un couplage (un sous-ensemble de triplets contenant tous les éléments une fois et une seule) ?

Nom : **X3-SAT**  
Instance : une formule logique sous forme normale conjonctive, composée de clauses de degré exactement 3.  
Question : est-ce que la formule est satisfiable ?

---

**Définition (Sous-graphe) :**  
Le sous-graphe de $G = (V,E)$ engendré par un sous-ensemble des sommets $S$ de $V$ est le graphe $G_S$ dont les sommets sont les sommets de $S$ et les arêtes sont celles de $G$ dont les deux extrémités sont dans $S$.

**Définition (Graphe partiel) :**  
Le graphe partiel de $G = (V,E)$ engendré par un sous-ensemble $A$ de l’ensemble des arêtes de $G$ est le graphe obtenu de $G$ en retirant les arêtes de $E \backslash A$.

**Définition (Sous-graphe partiel) :**  
Le sous-graphe partiel de $G$ est le sous-graphe d’un graphe partiel de $G$.

---

## Exercice 3

Montrer que le problème Isomorphisme de sous-graphes est NP-difficile.

Nom : **Isomorphisme de sous-graphes**  
Instance : deux graphes finis $G_1$ et $G_2$  
Question : $G_1$ contient-il un sous-graphe isomorphe à $G_2$ ?

### Réponse exercice 3

Clique $\propto$ Isomorphisme de Sous-Graphes (ISG)

$$
\begin{align*}
G = <V,E> &\Rightarrow{} G_1<V_1, E_1> \\
C \in \mathbb{N} &\phantom{\Rightarrow{}} G_2<V_2, E_2> \\
\phantom{} &\phantom{\Rightarrow{}} G = G_1 \\
\phantom{} &\phantom{\Rightarrow{}} G_2 = \text{graphe complet à C sommets} \\
\end{align*}
$$

---

## Exercice 4

Montrer que le problème Isomorphisme de sous-graphes partiels est NP-difficile.

Nom : **Isomorphisme de sous-graphes partiels**  
Instance : deux graphes finis $G_1$ et $G_2$  
Question : $G_1$ contient-il un sous-graphe partiel isomorphe à $G_2$ ?

### Réponse exercice 4

Cycle Hamiltonien $\propto$ Isomorphisme de sous-graphes partiels (ISGP) (ou clique $\propto$ ISGP même demo que 3)

$$
\begin{align*}
G = <V,E> &\Rightarrow{} G_1 = G \\
\phantom{} &\phantom{\Rightarrow{}} G_2 = \text{cycle à |V| sommets}\\
\end{align*}
$$

---

## Exercice 5

Montrer que le problème Arbre couvrant de degré borné est NP-difficile.

Nom : **Arbre couvrant de degré borné**  
Instance : $G$ et un entier $k$  
Question : Existe-t-il un arbre couvrant de degré au plus k ?

### Réponse exercice 5

Chaine Hamiltonienne $\propto$ Arbre

$$
\begin{align*}
G = <V,E> &\Rightarrow{} G' = G \\
\phantom{} &\phantom{\Rightarrow{}} k = 2 \\
\end{align*}
$$

---

## Exercice 6

Montrer que le problème Ordonnancement de tâches est NP-difficile.

Nom : **Ordonnancement de tâches**  
Instance : Soient $k$ tâches de durées respectives $t_1, \dots, t_k$ (durées entières), $T$ le temps total d’exécution autorisé et $n$ le nombre de processeurs.  
Question : Est-il possible d’exécuter les $k$ tâches sur une machine à $n$ processeurs en moins de $T$ unités de temps ?

### Réponse exercice 6

Partition $\propto$ Ordonnancement de tâches

$$
\begin{align*}
A' \subseteq A &\Rightarrow{} n = 2\\
\sum_{a \in A'} a = \sum_{a \in A \backslash A'} a &\phantom{\Rightarrow{}} k = card(A)\\
\phantom{} &\phantom{\Rightarrow{}} T = \frac{1}{2} \sum_{a \in A} a\\

\end{align*}
$$

$\Rightarrow{}$ Soit $A \subseteq A$ tel que $\sum_{a \in A} a = \sum_{a \in A \backslash A'} a$  
On construit une instance d'orderonnancement de tâches de la manière suivante :

- Les tâches correspondantes aux éléments de $A'$ sont sur le cœur 1
- Les tâches correspondantes aux éléments de $A \backslash A'$ sont sur le cœur 2

---

## Exercice 7

Montrer que le problème Plus petit ensemble de tests est NP-difficile.

Nom : **Plus petit ensemble de tests**  
Instance : $P$ un ensemble de pannes possibles, $C$ une famille de sous-ensembles de $P$ représentant des tests, $J$ un entier  
Question : Existe-t-il un sous-famille de tests $C'$ de cardinalité au plus $J$ telle que pour toute
paire $p_i$, $p_j$ de pannes, il existe $c \in C'$ un test tel que $|\{p_i, p_j\} \cap c | = 1$. En d’autres termes, existe-t-il un test qui permette de distinguer la panne $p_i$ de la panne $p_j$ (pour tout $i$ et $j$).

---

## Exercice 8

Montrer que le problème Score est NP-difficile.

Nom : **Score**  
Instance : $G = (V, E)$ un graphe arête-pondéré non orienté dont les poids des arêtes sont des entiers non négatifs, $u$ et $v$ deux sommets et $S$ un entier.  
Question : Existe-t-il une chaîne simple de $u$ à $v$ de poids supérieur ou égal à $S$ ?

### Réponse exercice 8

Chaine Hamiltonienne $\propto$ Score

$f : G(V,E) \rightarrow G'(V',E'), u, v \in V', S \in \mathbb{N}$

![image](./r%C3%A9ponse%208.jpg)

$G'$ est composé de $G$ avec chacune des arrêtes de $G$ avec un poids de $1$.  
On rajoute $2$ sommets à $G'$, $u$ et $v$, relisés à tous les sommets de $V$ avec un poids de $1$.  
On prend $S = |V| - 1 + 2 = |V| + 1$.

$$
\begin{align*}
\text{Chaine Hamiltonienne} &\Leftrightarrow \exists \text{ chemin Hamiltonien } (v1, \dots, v_n) \text{ dans } G \\
&\Leftrightarrow \exists \text{ chemin } (u, v1, \dots, v_n, v) \text{ dans  G' avec un poids } S = |V| + 1 \\
&\Leftrightarrow \text{Score } (G', u, v, S) \\
\end{align*}
$$

---

## Exercice 9

Montrer que le problème 3-Partition est NP-difficile.

Nom : **3-Partition**  
Instance : A un ensemble fini d’entiers non-négatifs  
Question : Existe-t-il une partition de $A$ en $A1$, $A2$ et $A3$ en trois ensembles de somme égale ?

### Réponse exercice 9

Partition $\propto$ 3-Partition

$$
\begin{align*}
f : &A &\rightarrow & B\\
&\{t_1, \dots, t_k\} &&B = A \cup \{s\} \text{ avec s} = \frac{1}{2}\sum_{a \in A}a\\
\end{align*}
$$

$$
\begin{align*}
\text{Partition (A)} &\Leftrightarrow \exists \text{A', A'' une partition de A telle que }\sum_{a \in A'}a = \sum_{a \in A''}\\
&\Rightarrow \exists B' = A', B'' = A'', B''' = \{s\}, \sum_{b \in B'}b = \sum_{b \in B''}b = \sum_{b \in B'''}b\\
&\Rightarrow \text{3-Partition (B)}\\
\end{align*}
$$

$$
\begin{align*}
\text{3-Partition (B)} &\Rightarrow \text{B', B'' et B'''} = \{s\} \text{ car }\sum_{b \in B} = 3S\\
&\Rightarrow \text{B', B'' est une partition équilibrée de B\textbackslash\{s\} = A}\\
&\Rightarrow \text{A' = B' et A'' = B'' est une partition de A } (\sum_{a \in A'}a = \sum_{a \in A''})\\
&\Rightarrow \text{Partition (A)}\\
\end{align*}
$$

---

## Exercice 10

Montrer que le problème Somme de sous-ensembles est NP-difficile (en utilisant X3-SAT dans la réduction).

Nom : **Somme de sous-ensembles**  
Instance : Un ensemble A d’entiers non négatifs et un entier $C$  
Question : Existe-t-il un sous-ensemble de A qui somme à $C$ ?  

### Réponse exercice 10

X3-SAT $\propto$ Somme de sous-ensembles

$f : \mu : ((\lambda_1 \lor \lnot \lambda_2 \lor \lnot \lambda_3) \land \dots ) \rightarrow \exists A \in \mathbb{N}^*, C \in \mathbb{N}$

$|\mu| = m$  
$|\lambda| = n$

$ \mu_1 = \lambda_1 \lor \lnot \lambda_2$

<!-- align left -->
$$
\begin{aligned}
\lambda_1 &\rightarrow a_1 = 2^1 + 2^{n+1} \\
\lnot \lambda_1 &\rightarrow \lnot a_1 = 2^1 \\
\lambda_2 &\rightarrow a_2 = 2^2 + 2^{n+2} \\
\lnot \lambda_2 &\rightarrow \lnot a_2 = 2^2 + 2^{n+1} \\
\end{aligned}
$$

$c = \sum_{i=1}^n 2^i + \sum_{i=1}^m 2^{n+2i}$
