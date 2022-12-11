---
output:
  pdf_document: default
  html_document: default
---
# Algorithmes et complexité (2022-2023)

*Florian Bridoux, François Doré, Dorian Mazauric*.

## Partiel du 24 octobre 2022 (durée une heure, aucun document autorisé)

### Exercice 1

Écrire une machine de Turing déterministe à un seul ruban qui reconnait le langage des mots (à une lettre `a`) dont la longueur est une puissance de deux.  
Exemples de mots du langage: `a` ; `aa` ; `aaaa` ; `aaaaaaaa`  
Quelle est la complexité de votre machine de Turing dans le pire des cas ?

### Exercice 2

Écrire une machine de Turing déterministe à un seul ruban qui reconnaît le langage des mots sur l'alphabet $\{0,1\}$ qui contiennent autant de `0` que de `1`.  
Exemples de mots dulangage: `000111` ; `00100111` ; `1101010010` ; `1111010000`  
Quelle est la complexité de votre machine de Turing dans le pire des cas ?

### Exercice 3

Soit le problème suivant.

**Nom :** Double puzzle  
**Instance :** Deux rectangles de longueur $L$ et de largeur $I$ chacun ($L$ et $I$ étant deux entiers), un ensemble de pièces polygonales.  
**Question :** Existe-t-il une manière de remplir totalement les deux rectangles avec l'ensemble des pièces ?

Montrer que Problème de la table ronde est NP-difficile.  
Pour la réduction, vous utiliserez un des problèmes NP-difficiles listés en annexe.

### Exercice 4

Soit le problème suivant.

**Nom :** Problème de la table ronde  
**Instance :** Un ensemble de n personnes, un ensemble de paires de personnes qui sont amis.  
**Question :** Existe-t-il un placement de ces n personnes autour d'une table ronde de manière à ce que chaque personne ait deux amis comme voisins ?

Il est possible de voir l'ensemble des amitiés comme un graphe avec une arête entre deux personnes si ces dernières sont amis.

**Exemple :**  
Soient 5 personnes :
A, B, C, D et E avec les paires d'amitié suivantes :
{A,B}, {A,C}, {A,E}, {B,C), {B,E}, {C,D}, {E,D}.  
La réponse pour cette instance est oui.

En effet, le placement suivant A, C, D, E, B est valide car A est ami avec C, C est ami avec D, D est ami avec E, E est ami avec B et B est ami avec A.

Montrer que Problème de la table ronde est NP-difficile.  
Pour la réduction, vous utiliserez un des problèmes NP-difficiles listés en annexe
