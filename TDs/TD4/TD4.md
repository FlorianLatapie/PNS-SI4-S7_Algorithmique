# TD4

## Exercice 1

Nom : **Chemin le plus long**  
Instance : Un arbre arête-pondéré $T = (V, E)$ représenté sous forme de listes d’adjacence avec $p(uv)$ le poids (entier non-négatif) de chaque arête $uv$ de $E$, une somme racine $r$ de $V$ et un entier non-négatif $L$.  
Question : Le graphe admet-il un chemin de simple de $r$ à feuille de $T$ telle que la somme des poids des arêtes composant est au moins $L$ ?

Notons que la version du problème dans le cas général des graphes est NP-complet (chaîne hamiltonienne).

Prouver un algorithme de programmation dynamique polynomial dans le cas des arbres.

Quelle est sa complexité ?

### Réponse exercice 1

$f(v)=$ longueur du plus long chemin de $v$ vers une feuille

$v$ est une feuille $\Rightarrow f(v) = 0$  
$f(v) = \text{Max}(\{p(uv)+f(u), u\in V(v)\})$

Complexité : $O(n)$

## Exercice 2

Nom : **Ensemble Indépendant**  
Instance : Un graphe fini $G = (V, E)$ représenté sous forme de listes d’adjacence, un nombre entier non-négatif $k$  
Question : Le graphe admet-il un ensemble indépendant de taille $k$ ?

Prouver un algorithme de programmation dynamique polynomial dans le cas des arbres.

Quelle est sa complexité ?

### Réponse exercice 2

$v \in V \longmapsto (f(v), g(v))$

$f(v) =$ stable max du sous-arbre enraciné en $v$ inclus  
$g(v) =$ stable max du sous-arbre enraciné en $v$ exclu

$f(v) = 1 + \sum_{u \in V(v)} g(u)$  
$g(v) = \sum_{u \in V(v)} \text{Max}(f(u), g(u))$

Cas d'arrêt : feuille ($v$)  
f(v) = 1  
g(v) = 0

Complexité : $O(n)$

## Exercice 3

Nom : **Sac à dos**
Instance : Une liste d’objets $X$, une valeur $v(x)$ pour tout $x$ de $X$, un poids $p(x)$ pour tout $x$ de $X$, deux entiers non-négatifs $V$ et $P$.  
Question : existe-t-il un sous-ensemble $X’$ de $X$ tel que la somme des valeurs des éléments de $X’$ est au moins $V$ et la somme des poids des éléments de $X’$ est au plus $P$ ?  

Prouver un algorithme de programmation dynamique.

Quelle est sa complexité ?

### Réponse exercice 3

$X = \{x_1, x_2, ..., x_n\}$  
$v(x_i) \in \mathbb{N}$  
$p(x_i) \in \mathbb{N}$  
$V, P \in \mathbb{N}$

$R \subseteq X, \sum_{k \in R} v(k) \geq V$ et $\sum_{k \in R} p(k) \leq P$

Exemple :

|     |  0  |  1  |  2  |  3  |  4  |
|:---:|:---:|:---:|:---:|:---:|:---:|
|  0  |  0  |  0  |  0  |  0  |  0  |
|  1  |  0  |  0  |  3  |  3  |  3  |
|  2  |  0  |  1  |  3  |  4  |  4  |
|  3  |  0  |  3  |  4  |  6  |  7  |
|  4  |  0  |  3  |  4  |  6  |  7  |
|  5  |  0  |  3  |  5  |  6  |  8  |

|  obj  |  1  |  2  |  3  |  4  |  5  |
|:-----:|:---:|:---:|:---:|:---:|:---:|
|  val  |  3  |  1  |  3  |  1  |  2  |
| poids |  2  |  1  |  1  |  2  |  1  |
