# Cours algorithmique et complexité

---

- mail du prof : dorian.mazauric@inria.fr
- mail prof de td : bridoux@i3s.unice.fr

---

## 19/09/2022

## Machine de Turing

Une Machine de Turing est un modèle mathématique de calcul. Elle est composée d'une bande infinie de cellules, d'une tête de
lecture et d'un état. La tête de lecture peut lire, écrire et se déplacer sur la bande. La machine de Turing est définie
par un programme qui décrit les actions à effectuer en fonction de l'état et du symbole lu.

Machine de Turing (1936) - Modèle de calcul

Composition d'une machine de Turing :

- Une ou plusieurs bandes/ruban
- Une unité de contrôle
- Chaque bande est divisée en cases
- Chaque case contient un symbole d'un alphabet fini
- Tetes de lecture/écriture permet de lire/écrire dans une case

## Machine de Turing à $K$ rubans

- $Q$ : ensemble fini d'états de la machine
- $T$ : alphabet de la machine, ensemble fini de symboles que l'on peut utiliser sur les bandes
- $I$ : sous-ensemble de l'ensemble de données
- $\delta$ : fonction de transition $Q \times T^X \to Q \times (T \times \{G,D,S\})^K$
- $B$ : symbole blanc
- $q_0$ : état initial
- $q_f$ : état final

Exemple de machine de Turing à 2 rubans : palindromes

ruban 1 : ... | K | A | Y | A | K | ...

ruban 2 : ... | B | B | B | B | B | ...$

---

## 26/09/2022

Temps de calcul d'une machine de Turing (MT), est une fonction de $T(n)$ avec n la taille des données

$T(n)$ nombre maximum de transitions pour une donnée de taille n

## Théorème

Si le langage $L$ est accepté par une machine de Turing $T$ à $k$ bandes alors il existe une machine de Turing $T'$ à 1
bande qui reconnaît le même langage $L$.

### Théorème de l'accélération

Si $L$ est accepté par une machine de Turing à bande ( $k>1$ ) en un temps $T(n)$ (avec $\lim\limits_{x \to \infty} \frac{T(n)}{n} = +\infty$ ) alors pour toute constante réelle $c>0$, il existe une machine de Turing à $k$ bandes acceptant $L$
en un temps $c T(n)$

### Preuve

1. Nous encodons de la manière suivante les cases de MT $\longrightarrow$ 1 case de MT
2. Ce codage permet plusieurs transitions à la fois.
   En effet, une lecture donne l'information de `n` cases de MT.
   Donc, on peut effectuer tout le travail de ces `n` lectures.
   Chaque phase de base de `MT' >= m` transitions de `MT`
   Pour MT', on va lire 3 cases voisines ( $3^m$ cases dans MT)  
   $T'(n) < 2n + \frac{8T(n)}{m}$  
   Il faut choisir `m` pour que $T'(n) \leq c T(n)$  
   $m > \frac{16}{c}$  
   $\Rightarrow \frac{8T(n)}{m} < \frac{c}{2}n < c T(n) - 2n$  
   pour `n` suffisamment grand.

---

## 03/10/2022

## Manière de formaliser un problème

- Nom du problème
- Données du problème (codage inclus)
- Une question qui a deux réponses possibles OUI ou NON

### Exemple

- Nom : Sac a dos (Knapsack)
- Données :
  - ensemble fini d'objets $E$
  - une fonction entière $v$ qui associe une valeur à chaque objet
  - une fonction entière $p$ qui associe un poids à chaque objet
  - un poids total $P$
  - une valeur totale minimale $V$
- Question : pouvons-nous choisir des objets de manière à ne pas dépasser le poids total $P$ et à avoir une valeur
  totale au moins $V$ ?

*Réduction polynomiale :*

$P_1$ et $P_2$ deux problèmes (de décision)
$P_1$ peut être réduit à $P_2$ s'il existe une transformation associant à chaque instance $I_1$ de $P_1$ une instance
$f(I_1$) de $P_2$ telle que :
la réponse à $I_1$ est OUI si et seulement si la réponse à $f(I_1)$ est OUI

$P_1$ : Chaine hamiltonienne
Graphe G = (V,E) (liste d'adjacence)
Est-ce qu'il existe une chaine qui permet de passer une fois et une seule par chaque sommet de G ?

$P_2$ : Cycle hamiltonien
Graphe G = (V,E) (liste d'adjacence)
Est-ce qu'il existe un cycle qui permet de passer une fois et une seule par chaque sommet de G ?

Nous montrons que G admet une chaine hamiltonienne si et seulement si G' admet un cycle hamiltonien

$\Leftarrow$ : considérons un cycle hamiltonien de $G$ : "moins $x_0$" alors on obtient une chaine hamiltonienne de $G$

$\Rightarrow$ : Si G admet une chaine hamiltonienne, alors on ajoute 2 arêtes des extrémités de la chaine vers $x_0$
et on obtient un cycle hamiltonien dans $G'$ avec $x_0$

Finalement, $p_1$ $\leq$ $p_2$

---

## Classique en DS

TD2 : exo4 variante ${a_k, b_k}$  
et vérifier la parité d'un nombre

---

## 10/10/2022

## P et NP

**Définition** : P est la classe des problèmes qu'il est possible de résoudre en temps *polynomial* avec une machine de
Turing *déterministe*.

Cette machine est non déterministe :

```mermaid
graph LR
    a((q)) --> | a/a/D | b(( ))
    a((q)) --> | a/b/G | c(( ))
```

Plusieurs transitions à partir d'un même état.

**Définition** : NP (Nondeterministic Polynomial) non déterministe polynomial est la classe de problèmes qu'il est
possible de résoudre en un temps polynomial avec une machine de Turing non déterministe.

Exemple :

- Partition
- Entrée : un ensemble A non négatif (écrit en base $k => 2$)
- Question : Est-ce qu'il existe un sous ensemble $A_1 <= A$ tel que $\sum_{a \in A_1} a = \sum_{a' \in A \backslash
  A_1} a'$

```mermaid
graph LR
    a(( )) --> b((Choisir a))
    a(( )) --> c((Ne pas<br/>choisir A))
```

Un problème $\Pi$ est NP-complet si et seulement si (classe les plus difficiles de NP) :

- $\Pi$ est dans NP  
  Comment ?
  - Machine de Turing non déterministe
  - On peut vérifier une solution en un temps polynomial

- Tout problème $\Pi'$ dans NP peut être réduit polynomialement à $\Pi$
  Comment ?
  - On trouve un problème $\Pi'$ qui est NP-Complet et tel qu'il existe $\Pi' \propto \Pi$

---

## 17/10/2022

Problème Partition :
Partition est NP-Complet

- Partition est dans NP :
On peut vérifier une solution en temps polynomial.

##  3DM

- 3DM
- Entrée :  
  $X = \{x_1, x_2, ..., x_t\}$, $t = |X| = |Y| = |Z|$  
  $Y = \{y_1, y_2, ..., y_t\}$  
  $Z = \{z_1, z_2, ..., z_t\}$

  $M$ un ensemble de triplets dans $X \times Y \times Z$  
  Un triplet (x,y,z) avec $x \in X$, $y \in Y$, $z \in Z$
- Question : Existe-t-il $M' \subseteq M$ tel que $|M'| = t$ et $U_{i=1}^{t} \{n_i\} = X \times Y \times Z$ avec $M = \{n_1, n_2, ..., n_t\}$

3DM $\propto$ Partition

N'importe quelle instance et 3DM

$X, Y, Z$  
$M$  
$k = |M|$

$\xrightarrow[\text{Transformation polynomiale}]{}$

Chaque $a_i \in A$ sera donc composé de $3tp$ chiffres binaires
$p = \lceil log_2(k + 1) \rceil$  
$|A| = k+2$

Exemple :

$x_1, y_1, z_1$

| 001   | 000   | 000   | 000   | 001   | 000   | 000   | 000   | 001   | $(3tp)$ |
|-------|-------|-------|-------|-------|-------|-------|-------|-------|---------|
| $x_1$ | $x_2$ | $x_3$ | $y_1$ | $y_2$ | $y_3$ | $z_1$ | $z_2$ | $z_3$ |         |

$B = 001001001\dots$ (taille $3tp$)  
$a_{k+1} = 2S - B$  
$a_{k+2} = S + B$

---

## 07/11/2022

## Vertex Cover

**Definition :**  
Un Vertex Cover d'un graphe $G = (V,E)$ est un sous-ensemble $V \subseteq V$ qui inclut au moins une extrémité de chaque arête de $G$ : $V' \subseteq V$ tel que $\forall \{u,v\} \in E$, on a $\{u,v\} \cap V' \neq \emptyset$

- Vertex cover
- Entrées : Un graphe $G = (V,E)$ (représenté par sa liste d'adjacence), un entier $k \in \mathbb{N}$
- Question : Existe-t-il un Vertex Cover de taille au plus $k$ ?

Comment montrer que Vertex Cover est NP-Complet ?

- Vertex Cover est dans NP, car il est possible de vérifier, en temps polynomial la validité d'une solution
- NP-Difficulté ? En faisant une réduction polynomiale : 3-Sat $\propto$ Vertex Cover

## 3-Sat

Exemple :
$$
\begin{align*}
\phi = &\phantom{}&(x_1 \lor \lnot  x_2 \lor \lnot x_3)  \\
&\land &(\lnot x_1 \lor \lnot  x_3 \lor \lnot  x_4) \\
&\land &(\lnot x_2 \lor x_3 \lor \lnot x_4) \\
&\land &(x_2 \lor x_4 \lor \lnot x_5)  \\
&\land &(\lnot x_3 \lor \lnot x_4 \lor x_5)
\end{align*}
$$

// TODO : mettre le schéma

$n$ variables et $p$ clauses

$\exists$ une solution pour 3-SAT $\iff$ $\exists$ un vertex cover de $G$ de taille $n + 2p$

$2p$ clauses, car au moins besoin d'utiliser 2 sommets dans chaque triangle

**Preuve :**

- $\Rightarrow$ S'il existe une affectation qui rend vrai 3-SAT, alors il existe un Vertex Cover de taille $n + 2p$.
- $\Leftarrow$ S'il existe un Vertex Cover $V'$ de taille $|n + 2p|$, alors nécessairement il y a $n$ sommets de $V_1$ qui sont dans $V'$ et $2p$ sommets de $V_2$ qui sont dans $V'$.  
  Donc $\exists$ une affectation qui rend vrai $\phi$ en prenant les sommets de $V_2$ qui ne sont pas dans $V'$.

## 14/11/2022

### Résumé du contrôle

La moyenne du contrôle avant l'harmonisation est de 8/20 avec un écart type de 5 (C'est très grand). 15/78 personnes (19,2%) de la promo ont eu plus de 15/20. Une personne a eu 20/20 sans harmoniser.

Ceux qui ont compris l'idée sur les exercices de reduction auront une "bonne note" pour cette partie. De plus, 3/4 exercices ont étés notés.  
Comprendre l'idée de l'exercice : le problème qu'on sait, on le met à droite.

Afin de parer à cela, les notes ont étés harmonisés. La moyenne harmonisée est donc de 10,5/20.

Avant comme après harmonisation, les notes vont de 0 à 20.

Résumé des informations :

| Notes | # de personnes | % de la promo |
|-------|----------------|---------------|
| 0-5   | 7              | 8,97%         |
| 5-10  | 30             | 38,46%        |
| 10-15 | 26             | 33,33%        |
| 15-20 | ? (calculé 15) | 6,41%         |
| 18-20 | (10-4 =) 6     | 7,69%         |
| 20    | 4              | 5,13%         |

Résumé du résumé :

| Notes | # de personnes | % de la promo |
|-------|----------------|---------------|
| 0-5   | 7              | 8,97%         |
| 5-10  | 30             | 38,46%        |
| 10-15 | 26             | 33,33%        |
| 15-20 | 15             | 19,23%        |

Pas de nouvelles notes prévues avant le partiel final.

## Programmation dynamique

![image](assets/2022.14.11_1.jpg)

Min Vertex Cover = Version minimisation de Vertex Cover  
$\rightarrow$ Trouver un plus petit ensemble de sommets qui est Vertex Cover du graphe.  
$N_T (v) = \{v_1, v_2, \dots, v_d\}$

![image](assets/2022.14.11_2.jpg)
![image](assets/2022.14.11_3.jpg)

Pour tout $v \in V$, on calcule :  
$f(v) =$ la taille du plus petit ensemble couvrant de $v$ avec la contrainte que $v$ est dans l'ensemble.
$g(v) =$ la taille du plus petit ensemble couvrant de $v$ avec la contrainte que $v$ n'est pas dans l'ensemble.

Soit $v \in V$ et les enfants de $v$ notés par l'ensemble $N_T (v)  = \{v_1, v_2, \dots, v_d\}$

Soient $(f(v_1), g(v_1)), (f(v_2), g(v_2)), \dots, (f(v_d), g(v_d))$ connus.  
$f(v) = 1 + \sum_{i=1}^d min(f(v_i), g(v_i))$  
$g(v) = \sum_{i=0}^d f(v_i)$

$f(v) = 1$  
$g(v) = 0$

## 21/11/2022

### Approximation

Un problème de minimisation P admet une approximation en temps polynomial à un facteur constant $k$ ( $k$ un réel plus grand que 1) s'il existe un algorithme $A$ de complexité polynomiale telle que $\forall$ instance de $P$, alors $A$ retourne une solution $S$ avec $|S| \leq k |S^\star|$ ( $S^\star$ une solution optimale).

Problème :  
Vertex cover (approximation)
On va prouver une 2-approximation en temps polynomial. (k=2)

$G = (V, E)$

**Principe de l'algorithme :** calculer un couplage maximal (par inclusion)

**Definition :**  
**Couplage** étant donné un graphe $G = (V, E)$, un couplage est un ensemble d'arêtes $E' \subseteq E$ deux à deux disjointes. (Autrement dit ; tout sommet de $V$ est une extrémité d'au plus 1 arrête de $E'$)

$E = \{e_1, e_2, \dots, e_n\}$

Comment trouver un couplage maximal ?

- On prend les arêtes les plus dans l'ordre et on ajoute une arête au couplage si et seulement si cet ajout permet à $C$ de rester un couplage.

On construit un Vertex Cover en prenant les 2 extrémités de chaque arête du couplage maximal calculé

On note cet ensemble $V' \subseteq V$.  
On montre que $V'$ est un Vertex Cover.  
En effet, comme $C$ est un couplage maximal, alors chaque arête $e \in E$ a (au moins) une extrémité dans $V'$. Par construction de $V'$

Montrons que $|V'| \leq 2|V^\star|$ avec $V^\star$ un vertex de plus petite cardinalité.  
Pour chaque arête de $C$, nécessairement une des deux extrémités (ou moins) doit être dans tout Vertex Cover.  
Donc, alors le pire des cas, prendre une extrémité suffit.  
Donc notre algorithme est une 2-approximation polynomiale

Complexité : $C(n,m) = O(m^2)$

## 28/11/2022

Décomposition de $G$ en arbre (décomposition arborescente) est un arbre $T(N,A)$ avec $N = \{N_1, N_2, \dots, N_p\}$, $N \subseteq V$ pour tout $1 \dots p$ tel que :

- Les sous-ensembles couvrant les sommets de $G$ : $\underset{i = 1 \dots p}{\cup} N_i = V$
- Pour toute arête $vw \in E$, il existe un nœud $N_i$ tel que $v,w \in N_i$ (pour i donné)
- Pour tout sommet $v \in V$, les noeuds $N_i$ et $N_j$ contenant $v$ forment un sous-arbre de $T$.

**Definition :**  
Graphe connexe : $G=(V,E)$ est connexe si pour tout $u, v \in V$, alors il existe un chemin être $u$ et $v$ dans $G$

La largeur arborescente de $T = -1 + \underset{i = 1 \dots p}{\max} |N_i| = 2$

$v \space c (T_M, C \subseteq N_i)$ pour tous les sous-ensembles $C$ de $N$  
= Vertex Cover min de $T_{N_i}$ avec la contrainte que les sommets de $C$ sont dans le Vertex Cover. (les sommets qui ne sont pas dans $C$ ne sont pas dans le Vertex Cover)

## 05/12/2022

### Infos sur l'oral de l'aprem

Objectif : apporter des points  
5 minutes de préparation, 1.30 min d'oral  
Si c'est une machine de turing on demande que les grandes lignes, pas besoin de détails.  
Montrer dans les grandes lignes qu'on a compris  
Si on a pas compris comment faire une reduction c'est mort

### Rappels

le non déterminisme c'est qu'a un état on peut avoir plusieurs transitions possibles

p est contenu dans np

montrer que c'est dans np et np-difficile (ca a l'aide d'une réduction polynomiale)

montrer que le problème à droite est au moins aussi difficile qu'un problème a gauche qu'on connait  
ca démontre qu'un problème np diffile est aussi dur que nous

comment on montre qu'un problème est np difficile, on le montre avec une transformation polynomiale  

pour prouver que c'est np :  
1/2 : avec une machine de turing non déterministe  
2/2 : une vérifier que c'est possible en temps polynomial (pas prouver, vérifier : dire que c'est possible)  

### Comme en TD : problème du plus long chemin

On va montrer que le plus long chemin n'est pas approximable en temps polynomial
