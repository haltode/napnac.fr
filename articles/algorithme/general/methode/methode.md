Méthode de résolution
=====================
algo/general

Publié le : 13/07/2016  
*Modifié le : 13/07/2016*

## Introduction

Je ne le répèterai jamais assez, mais [France-IOI](http://www.france-ioi.org/) est la référence francophone en algorithmique, et une des choses qui distingue fortement cette plateforme est la méthode de résolution qu'elle cherche à transmettre au travers de ses exercices. Cet article a pour but de présenter cette méthode qui peut être terriblement efficace si correctement maitrisée. De plus, elle ne s'applique pas uniquement pour des concours ou des exercices, mais de manière générale lorsqu'on cherche un algorithme pour résoudre un problème donné.

Cependant, cette méthode peut paraître longue et fastidieuse au début, et nécessite de l'[entraînement](/algo/general/entrainement.html) ainsi que de la rigueur pour être utilisée efficacement. La vitesse viendra avec la pratique et non en bâclant les étapes de cette méthode. Il peut être frustrant au début de résoudre lentement un problème, mais cela vous sera très utile dans le futur et vous serez capable de réaliser les différentes étapes de cette méthode bien plus rapidement grâce à votre expérience.

Pour commencer, il vous faut uniquement une feuille et un crayon.

## Enoncé

### Lecture

Que ce soit un concours de programmation ou un problème que vous cherchez à résoudre, la première étape est de **lire attentivement l'énoncé**, et de ne surtout pas se précipiter. Cela peut paraitre évidant, mais c'est une erreur commune de se tromper dans la lecture du sujet, alors qu'il est facile d'éviter ceci. Relisez plusieurs fois ce dernier jusqu'à l'avoir en tête, et essayer de vous concentrer sur le sujet et non sur l'algorithme pour l'instant. Il est fréquent de commencer à lire le sujet et d'avoir une idée d'algorithme en tête qu'on cherche à développer, mais cette dernière n'est quasiment jamais la bonne car on n'a pas toutes les informations à propos de l'énoncé. **Ne cherchez pas de solutions au problème pour l'instant**, votre premier objectif est de comprendre parfaitement le sujet et de n'avoir aucuns doutes dessus. Commencer à chercher aussi tôt ne ferra que vous perturber, vous emmêler ou encore pire, vous induire en erreur.

### Reformulation

Une fois le sujet correctement lu et appréhendé, il est crucial de le **reformuler en quelques phrases** (deux ou trois en général suffisent, il ne s'agit pas de réécrire le problème ici). Ceci vous permet dans un premier temps de vérifier votre compréhension vis-à-vis de l'énoncé, mais aussi de le décrire efficacement et de manière concise. Supprimez tous les détails inutiles, et concentrez-vous sur ce qu'on vous demande concrètement de faire. Vous pouvez vous aider en écrivant deux phrases types, "On nous donne..." et "On nous demande...", puis si nécessaire notez les points importants à ne pas oublier ou spécifiques au sujet. Attention cependant, car **l'étape de reformulation ne doit pas dériver du sujet** (en le simplifiant ou en le généralisant par exemple), elle doit le décrire parfaitement comme si vous expliquiez l'énoncé à une personne.

Il est très courant dans un concours de programmation d'avoir une histoire qui accompagne le sujet, et l'étape de reformulation permet d'écarter cette dernière en explicitant le problème de manière crue et non imagée. Il faut arriver à se **détacher le plus possible de l'histoire** et de décrire le problème d'un point de vue purement algorithmique.

Voici un exemple de sujet très simple, ainsi qu'une reformulation de ce dernier :

> Alice et Bob sont de très bons amis, cependant les deux voyagent beaucoup et ils aimeraient se rencontrer afin de discuter de leurs dernières aventures. A force de voyager, Alice et Bob n'ont plus énormément d'argent, et Alice n'a pas de quoi payer pour rencontrer Bob. Ce dernier décide donc de la rejoindre, et se renseigne sur les différents moyens de transports ainsi que leurs coûts. Son but est de voyager à prix minime, pour économiser dans de futurs voyages. Après une recherche sur son navigateur favori, Bob se retrouve avec les informations suivantes :  
> 
> | Départ   | Arrivée  | Coût | Transport |
> | ------   | -------  | ---- | --------- |
> | Shanghai | Pékin    | 100€ | train     |
> | New-York | Londres  | 700€ | avion     |
> | Paris    | Shanghai | 700€ | avion     |
> | New-York | Pékin    | 800€ | avion     |
> | Moscou   | Shanghai | 450€ | avion     |
> | Pékin    | Moscou   | 300€ | train     |
> | Le Caire | Paris    | 500€ | avion     |
> | Moscou   | New-York | 700€ | avion     |
> | Paris    | Londres  | 200€ | train     |
> | Moscou   | Paris    | 300€ | train     |
> 
> Sachant que Bob est actuellement à Pékin et qu'Alice se trouve à Londres, combien Bob devra-t-il dépenser au minimum afin de rencontrer Alice ?

Un exemple de reformulation utile de ce sujet :

> On nous un graphe orienté pondéré positivement.  
> On nous demande le plus court chemin entre deux nœuds de ce graphe.

Plus d'histoire, plus d'Alice et Bob, on garde uniquement le strict minimum, sans pour autant perdre des informations. Ici, l'entrée donnée par le sujet est un graphe implicite où chaque ville est un nœud et chaque trajet un arc. Le graphe est orienté car on a une case "Départ" et "Arrivée" ce qui semble indiquer une direction à suivre. L'information du transport (avion ou train) est en réalité inutile à notre problème puisqu'on ne cherche qu'à minimiser le coût, on l'omet donc de notre description. La pondération du graphe simule le coût du trajet, or ce coût est toujours positif donc on le précise. Pour ce qui est de la sortie, on nous demande effectivement un plus court chemin reliant le nœud de départ (où se trouve Bob sur le graphe) et un nœud d'arrivée (où se trouve Alice).

Une fois le sujet reformulé, il peut être intéressant de **relire une dernière fois l'énoncé** pour s'assurer de la véracité de la reformulation. En effet, cette dernière sera l'élément central de notre réflexion, donc il faut être certain qu'elle est correcte car on basera toute notre méthode de recherche de l'algorithme dessus.

Encore une fois, on est actuellement dans la compréhension du sujet et non dans la résolution. Ne vous lancez pas à tête baissée dans une idée d'algorithme tout de suite, attendez pour vérifier votre réflexion.

### Dimensions et contraintes

Enfin, dernière sous étape qui concerne l'énoncé, il faut noter sur votre feuille les **dimensions** et les **contraintes** du sujet.

Une **dimension** est une donnée qu'on fournit dans l'énoncé du problème. Par exemple dans le cas du problème d'Alice et Bob, on pourra avoir une liste de dimensions comme :

> Soit $N$ le nombre de villes où peuvent voyager Alice et Bob, $1 <= N <= 200$  
> Soit $M$ le prix d'un trajet, $1 <= M <= 3000$€  
> Soit $K$ le coût total du trajet de Bob pour rejoindre Alice, $1 <= K <= 100000$€

On distingue plusieurs types de dimensions :

- **dimension d'entrée** : une valeur qui va concerner directement l'entrée de votre programme (ex: $N$ ou $M$)
- **dimension de sortie** : une valeur qui va concerner directement la sortie de votre programme (ex: $K$)
- **dimension implicite** : une valeur implicite de l'énoncé qui peut être intéressante de noter (ex: )

TODO : exemple dimension implicite

Pour chaque dimension il est utile de mettre la borne minimale et maximale, qui sont la plupart du temps données par le sujet ou qu'on peut simplement trouver avec quelques calculs.

Une **contrainte** est une limite imposée par l'énoncé, concernant généralement le temps ou la mémoire qu'on accorde à votre programme. Ces dernières sont explicites, par exemple :

> Temps : 1s sur une machine à 1Ghz  
> Mémoire : 32000 Ko

Lister les dimensions et les contraintes vous permet de vérifier rapidement si votre algorithme est assez efficace. En effet, avec ces informations il suffit de calculer la complexité d'un algorithme pour se rendre compte instantanément s'il respecte ou non le sujet.

*Attention à ne pas mettre les dimensions ou les contraintes dans la reformulation, ce sont deux sous-étapes bien distinctes.*

## Exemple

Deuxième étape de la méthode de résolution : **résoudre des exemples à la main**. C'est à mi-chemin entre compréhension du sujet et début de réflexion, mais cette étape est cruciale et bien souvent trop peu réalisée.

### Représentation graphique du problème

Avant de se lancer dans la résolution d'exemples, on peut commencer par chercher une bonne représentation de notre problème. Visualiser ce dernier nous permettra de trouver une solution bien plus facilement, mais encore une fois, il y a de nombreuses façons de représenter une même chose mais peu sont réellement efficaces et utiles.

Une bonne visualisation indique des informations indispensables, il ne faut surtout pas surcharger la figure car elle doit rester claire et précise. Cette représentation peut prendre différentes formes selon le sujet et le contexte : graphe, arbre, tableau, graphique 2D, etc.

### Résoudre des exemples à la main

Maintenant que vous avez le sujet bien en tête, reformulé, et correctement représenté sur votre feuille, il faut réaliser plusieurs exemples de résolution.


## Algorithme

## Pseudo-code

## Vérifier le pseudo-code

## Coder l'algorithme

## Tester le code

## Débuguer le programme

## Conclusion