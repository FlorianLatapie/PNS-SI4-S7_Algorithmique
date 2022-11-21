# TD5

## Exercice 1

Nom : **Ordonnancement de tâches**  
Instance : Soient k tâches de durées respectives $t_1, ..., t_k$ (durées entières), $T$ le temps total d’exécution autorisé et n le nombre de processeurs.  
Question : Est-il possible d’exécuter les k tâches sur une machine à n processeurs en moins de $T$ unités de temps ?

Prouver un algorithme polynomial qui est une 2-approximation de la version minimisation du problème Ordonnancement de tâches.  
La version minimisation consiste à minimiser la durée totale d’exécution ($T$ n’est donc plus dans l’entrée du problème).

## Exercice 2

Nom : **Plus long chemin**  
Instance : Un graphe fini arête-pondéré $G = (V, E)$ représenté sous forme de listes d’adjacence, un nombre entier non-négatif $L$, deux sommets $u$ et $v$ (les poids sont des réels positifs)  
Question : Le graphe admet-il un chemin simple de poids total au moins L entre $u$ et $v$ ?

Montrer que Plus long chemin est NP-difficile ?

Considérons la version minimisation du problème Plus long chemin.  
Pour tout entier k, prouver qu’il n’existe pas d’algorithme polynomial qui trouve une solution approchée, à un facteur d’approximation k, à moins que P=NP.

## Exercice 3

Nom : **Plus court chemin**
Instance : Un graphe fini $G = (V, E)$ représenté sous forme de listes d’adjacence, un nombre entier non-négatif $L$, deux sommets $u$ et $v$.
Question : Le graphe admet-il un chemin simple entre $u$ et $v$ de longueur au plus $L$ ?

Écrire et prouver un algorithme polynomial pour le problème Plus court chemin.  
Quelle est sa complexité ?

## Exercice 4

Même question que 3 avec un graphe arête-pondéré.
