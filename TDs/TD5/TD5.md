# TD5

## Exercice 1

Nom : **Ordonnancement de tâches**  
Instance : Soient k tâches de durées respectives $t_1, ..., t_k$ (durées entières), $T$ le temps total d’exécution autorisé et n le nombre de processeurs.  
Question : Est-il possible d’exécuter les k tâches sur une machine à n processeurs en moins de $T$ unités de temps ?

Prouver un algorithme polynomial qui est une 2-approximation de la version minimisation du problème Ordonnancement de tâches.  
La version minimisation consiste à minimiser la durée totale d’exécution ($T$ n’est donc plus dans l’entrée du problème).

### Réponse exercice 1

Preuve par un algorithme

```py
def ord(t, n): # t = tableau d'entiers
    lst = [0] * n
    for i in range(len(t)):
        plus_petit = 0
        for j in range(n):
            if lst[j] < lst[plus_petit]:
                plus_petit = j
        lst[plus_petit] += t[i]
    return max(lst)
```

À chaque tour de boucle :

```py
max(lst) <= min(lst) + max(t)
```

- Au tour 0 : $\forall i \in [0, n-1], lst[i] = 0$  
  $\Rightarrow$ vrai 
- On suppose que c'est vrai au tour $l$  
  $max(lst) \leq min(lst) + max(l)$  
  lst' est lst après un tour de boucle
- $1^{er}$ cas : $max(lst') = max(lst)$  
  donc $max(lst') \leq min(lst) + max(t) \leq min(lst') + max(t)$
- $2^{nd}$ cas : $max(lst') > max(lst)$  
  Donc $max(lst') \geq min(lst)$  
  $max(lst') \leq min(lst) + t[i] \leq min(lst') + max(t) \leq min(lst') + max(t)$

Finalement on a : 
$max(lst) \leq min(lst) + max(t)$  
or $\frac{1}{n} \sum_{i \in [1,k]} t_i \leq T_\text{min}$ et $min(t_i) \leq \frac{1}{n} \sum_{i \in [1,k]} t_i$  
donc $min(t_i) \leq T_\text{min}$ (1)  
de plus $max(lst) \leq T_\text{min}$ (2)  
D'après (1) et (2) on obtient :  
$max(lst) \leq 2 \times T_\text{min}$

## Exercice 2 (niveau de difficulté qu'on pourrait avoir à l'exam)

Soit $p$ une constante dans [0, 100].

Nom : **Plus long chemin**  
Instance : Un graphe fini arête-pondéré $G = (V, E)$ représenté sous forme de listes d’adjacence, un nombre entier non-négatif $L$, deux sommets $u$ et $v$ (les poids sont des réels positifs)  
Question : Le graphe admet-il un chemin simple qui passe par au p % de sommets et de poids total au moins L entre u et v ?

Montrer que Plus long chemin est NP-difficile ?

Considérons la version maximisation du problème Plus long chemin, c’est-à-dire qui maximise le poids total du chemin.

Pour tout entier $k$, prouver qu’il n’existe pas d’algorithme polynomial qui trouve une solution approchée, à un facteur d’approximation $k$, à moins que $P=NP$

### Réponse exercice 2

Chaine Hamiltonienne $\xrightarrow[\text{Transformation polynomiale}]{}$ plus long chemin

Chaine Hamiltonienne $\propto$ plus long chemin (notation officielle du prof donc c'est forcément le bon sens)

Pour toute instance :

On va ajouter deux points $u$ et $v$ et les connecter à tous les autres points du graphe.

Ce qui nous donne : $G' = (V', E')$ avec  
$V' = V \cup \{u, v\}$ et  
$E' = E \cup \{u_x, x \in V\} \cup \{x_v, x \in V\}$

On a donc : $w(e) = 1 \forall e \in E'$

Chaine Hamiltonienne si et seulement s'il existe un chemin simple de $u$ à $v$ de $G'$ de poids total $L$.

**Plus long chemin (version maximisation)** :

- **Entrées :**  
  $G = (V, E)$  
  $u,v \in V$  
  $w(e) \forall e \in E$
- **Question :**  
  trouver un chemin simple entre $u$ et $v$ dans $G$ qui minimise le poids total (somme des poids des arêtes du chemin)

Montrons qu'il n'existe pas d'algorithme d'approximation à un facteur 2 près en temps polynomial à moins que P=NP.

$n = |V|$  
$n' = |V'|$  

$n' + 2 = 3n$  
$n' = 3n - 2$  

**Poids chemin noir** : $3n - 1$ (chemin ajouté entre $u$ et $v$ donc il y a 3n sommets et donc $3n - 1$ arêtes)  
**Poids chaine hamiltonienne** : toutes les arêtes du graphe d'origine ont un poids de 8 : $8 \times (n - 1) = 8n - 8$

$|V \cup V'| = 4n - 2$  
25% de $4n - 2 = n + \frac{1}{2}$  
$\Rightarrow$ tout chemin simple doit passer par au moins $n$ sommets

Supposons qu'un tel algorithme $A$ existe.

- **Soit $A$ retourne le chemin noir** (chemin extérieur)  
  Comme "un chemin bleu" (chemin intérieur) a un poids strictement plus grand que $k$ fois le poids du "chemin noir" alors il n'y a pas de chemin hamiltonien dans $G$
- **Soit $A$ retourne un chemin bleu** (chemin intérieur) et donc il existe une chaine dans hamiltonienne dans G.

Donc A permet de décider en temps polynomial si un graphe $G$ quelconque admet une chaine hamiltonienne ou non."
$\Rightarrow$ Une contradiction à moins que P $\neq$ NP (car chaine hamiltonienne est NP-Complet)

## Exercice 3

Nom : **Plus court chemin**  
Instance : Un graphe fini $G = (V, E)$ représenté sous forme de listes d’adjacence, un nombre entier non-négatif $L$, deux sommets $u$ et $v$.  
Question : Le graphe admet-il un chemin simple entre $u$ et $v$ de longueur au plus $L$ ?

Écrire et prouver un algorithme polynomial pour le problème Plus court chemin.  
Quelle est sa complexité ?

### Réponse exercice 3

```python	
def parcoursLargeur(...):
  compteur = 1 
  en_cours = [u]
  tant que visités != n:
    pour chaque sommet s dans en_cours:
      pour chaque sommet voisin v de s:
        si v non visité:
          ajouter v à en_cours
        visités.add(u)
    compteur ++
```

Solution de Quentin "le GOAT" Dubois :

```python
def parcoursLargeur(Graphe G, Sommet u, Sommet v):
  compteur = 1
  en_cours = [u]
  marquer(u)
  tant que file est non vide:
    s = en_cours.enlever()
    pour chaque voisin t de u dans G:
      si t non marqué:
        si t == v:
          return compteur + 1
        en_cours.ajouter(t)
        marquer(t)
    compteur ++
```

Complexité : $O(|V| + |E|)$

Cf. [Wikipédia : Parcours en largeur](https://fr.wikipedia.org/wiki/Algorithme_de_parcours_en_largeur)

## Exercice 4

Même question que 3 avec un graphe arête-pondéré.

### Réponse exercice 4

```python
def f(x):
  pour chaque voisin de x tel que p(v) = non visité 
  alors s(v) = en cours
    f(v)
  s(x) = visité
```

cf [Wikipedia : Algorithme de Dijkstra](https://fr.wikipedia.org/wiki/Algorithme_de_Dijkstra)

## Exercice 5

Utiliser l'algorithme de l'exercice 3 afin de prouver un algorithme polynomial pour sortir de tout labyrinthine.
