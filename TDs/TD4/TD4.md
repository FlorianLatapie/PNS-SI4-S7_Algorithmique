# TD4

## Exercice 1

Nom : **Chemin le plus long**  
Instance : Un arbre arête-pondéré $T = (V, E)$ eprésenté sous forme de listes d’adjacence avec $p(uv)$ le poids (entier non-négatif) de chaque arête $uv$ de $E$, une somme racine $r$ de $V$ et un entier non-négatif $L$.  
Question : Le grapch admet-il un chemin de simple de $r$ à feuille de $T$ telle que la somme des poids des arêtes composant est au moins $L$ ?

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

$f(v) = $ stable max du sous-arbre enraciné en $v$ inclus  
$g(v) = $ stable max du sous-arbre enraciné en $v$ exclu

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
