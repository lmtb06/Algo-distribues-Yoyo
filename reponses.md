# Réponses:
## 1.

Montrons cet invariant par récurrence :

- **Initialisation** : Au début de l'algorithme, d'après la définition des voisins entrants et sortants, si i < j alors j est voisin sortant de i et i est voisin entrant de j. L'invariant est donc vrai au début de la première ronde.

- **Hérédité** : Supposons l'invariant vrai au début d'une ronde r, montrons qu'il reste vrai au début de la ronde r+1 : 
    - Lors de la phase -Yo de la ronde r, si i envoie "no" à j alors i transfère j de ses voisins entrants vers ses voisins sortants, et j transfère i de ses voisins sortants vers ses voisins entrants. Donc l'invariant reste vérifié.
    - Si i envoie "yes" à j, les ensembles de voisins ne changent pas donc l'invariant reste vrai. 
    - Les seuls changements d'ensembles de voisins se font lors de la phase -Yo, donc l'invariant est bien vrai au début de la ronde r+1.

Par récurrence, l'invariant est donc vérifié au début de chaque ronde.

## 2.
- **Initialisation** : Au début de l'algorithme, le graphe ne contient pas de cycle. En effet, si le graphe contenait un cycle, il existerait un nœud i tel que i < i, ce qui est impossible. Donc l'invariant est vrai au début de la première ronde.

- **Hérédité** : Supposons l'invariant vrai au début d'une ronde r, montrons qu'il reste vrai au début de la ronde r+1 : 
    - L'orientation des arêtes ne change que lors de la phase -Yo, si j (voisin sortant) envoie "no" à i (voisin entrant), cela  ne se produit que si i n'a pas envoyé l'id minimum à j lors de la phase Yo-.
    - Si un nœud interne j reçoit "no" alors il envoie "no" à tous ses voisins entrants, dés lors qu'il y a un non, cela se propage à tous les voisins entrants à ce nœud et ainsi de suite. Changeant ainsi l'orientation de toutes les autres arêtes en partant de ce nœud jusqu'à une source.
    - La seule façon de créer un cycle est qu'il y ait deux chemin entre une source et un puit, et que l'un des deux chemin soit inversé. Cela ne peut pas se produire car les chemin ne sont inversé que si la source à l'origine du chemin n'a pas envoyé l'id minimum et comme c'est le même id qui est envoyé dans les deux chemin, cela ne peut pas se produire.

Par récurrence, l'invariant est donc vérifié au début de chaque ronde.

## 3.

- Montrons d'abord qu'une source peut devenir un nœud interne ou un puits après une ronde, mais pas l'inverse.
    - Lors de la phase -Yo, si une source i reçoit au moins un "no", alors un de ses voisins sortants j devient un voisin entrant. Donc i n'est plus une source, il devient un nœud interne ou un puits. 
    - Un nœud interne a à la fois des voisins entrants et des voisins sortants. Lors de la phase -Yo, il ne peut que transférer des voisins, il ne peut donc pas perdre tous ses voisins entrants ou tous ses voisins sortants, il reste un nœud interne.
    - Un puits n'a que des voisins entrants. Lors de la phase -Yo, il ne peut que transférer des voisins entrants en voisins sortants, il ne peut donc pas perdre tous ses voisins entrants. Il reste un puits ou devient un nœud interne, mais ne peut pas devenir une source.

- S'il y a au moins 2 sources au début d'une ronde, montrons qu'au moins une source devient un nœud interne ou un puits lors de cette ronde :
    - Chaque source envoie son identifiant à ses voisins sortants lors de la phase Yo-. 
    - Comme le graphe est connexe, il existe un chemin entre 2 sources quelconques. Sur ce chemin, il y a forcément un nœud j recevant les identifiants d'au moins 2 sources. 
    - Lors de la phase -Yo, le nœud j envoie "no" à toutes les sources dont il a reçu l'identifiant sauf une. Donc au moins une source recevra un "no" et deviendra un nœud interne ou un puits.

En combinant les deux points ci-dessus, on en déduit qu'à chaque ronde, au moins une source devient un nœud interne ou un puits, et aucun nouveau nœud ne devient une source. Donc le nombre de sources décroît strictement à chaque ronde.