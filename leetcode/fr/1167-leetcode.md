---
titre: LeetCode 1167. Coût minimum pour connecter des bâtonnets -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Coût minimum pour connecter des bâtons – LeetCode 1167
> **Les solutions Java + Python + C++, l'explication prête à l'interview et un billet de blog SEO optimisé* *

---

- Oui. 1. Le problème en coque

> **Grâce à un tableau de « bâtons » d'entiers positifs, choisir plusieurs fois deux bâtons, les connecter et payer un coût égal à la somme de leurs longueurs. Après connexion vous obtenez un nouveau bâton dont la longueur est cette somme. Continuer jusqu'à ce qu'un seul bâton reste. Retournez le coût total minimum. **

La taille d'entrée peut être aussi grande que les bâtons `104`, chacun jusqu'à `104` de longueur.

---

- Oui. 2. Pourquoi l'approche Greedy + Min-Heap fonctionne

Le problème est un modèle classique **Huffman-codage**.
A chaque étape, vous voulez combiner les deux bâtons *les plus petits* – tout autre choix rendra le coût strictement plus grand.
Une min‐heap garantit l'extraction O(log n) des deux plus petits éléments et l'insertion O(log n) du nouveau bâton.

> **Insight clé**:
> *Greedy + Min-Heap = Optimal*.

---

- Oui. 3. Complexité temporelle et spatiale

Algorithme
-- -- -- -- -- --
**Heure**="O(n log n)" – construction du tas + "n-1" opérations d'extraction et d'insertion Autres
**Espace** – magasins en tas tous les bâtons actuels

Cas de bord: quand `sticks.longueur == 1` la réponse est `0` – aucun travail nécessaire.

---

- Oui. 4. Le Code – Trois langues

> **Important** – toutes les solutions utilisent un **min-heap** et fonctionnent dans le temps `O(n log n)` optimal.
> Ils évitent également les débordements entiers en utilisant 64 bits (`long` en Java, `long` en C++, Python=s arbitraire-size int).

#### 4.1 Java

"Java
Importer java.util. Priorité Demande;

solution de classe publique {
public int connectSticks(int[] sticks) {
// Utilisez longtemps pour éviter les débordements; le résultat final s'inscrit dans l'int.
long total = 0;
Priorité Queue<integer> pq = nouvelle prioritéQueue<>();
pour (int stick : sticks) pq.add(stick);

pendant que (pq.size() > 1) {
somme longue = (long) pq.poll() + pq.poll();
total += somme;
pq.add(int) somme; // somme ne dépassera jamais 2^31-1 dans les contraintes données
}
retour (int) total;
}
}
«» "

> **Pourquoi c'est propre**
> - Une file d'attente prioritaire
> - Aucune méthode d'aide, boucle concise
> - Poignées débordent en toute sécurité

4.2 Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def connectSticks(self, sticks: List[int]) -> Int:
heapq.heapify(sticles) # O(n)
Total = 0
pendant que lent(s) > 1 :
a = heapq.heappop(sticks) # plus petit
b = heapq.heappop(sticks) # deuxième plus petite
s = a + b
Total += s
heapq.heappush(piles, s)
retour total
«» "

> ** Touches pyroniques* *
> - `heapq.heapify` construit le tas dans le temps linéaire
> - La liste est mutée en place – aucun tableau supplémentaire

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int connectSticks(vector<int>& sticks) {
// Min‐heap via priority_queue avec un comparateur plus important
priorité_queue<int, vecteur<int>, plus grande<int>> pq(sticks.begin(), sticks.end());
long total = 0;
pendant que (pq.size() > 1) {
long a = pq.top(); pq.pop();
long long b = pq.top(); pq.pop();
long long s = a + b;
total += s;
pq.push(static_cast<int>(s));
}
retourner static_cast<int>(total);
}
};
«» "

> **C++ style**
> - `plus grand<int>` donne un peu de poids
> - `static_cast<int>` garantit le type retourné

---

- Oui. 5. Bon, mauvais, et humble

C'est bien, c'est mal.
C'est pas vrai.
**Algorithme**= Greedy + Min-Heap (optimal)== O(n2) naïve fusion par paire (quadratique)== Mélange de heap + force brute, conduisant à un code messy==
**Mise en oeuvre**=Clean, concision, utilise le langage-idiomatique heap==Loops imbriquées, difficiles à lire==Modifications en place sans commentaires, gestion sans erreur==
**Edge-Cases**=Poignées simple bâton, grandes entrées, débordement==Fails sur l'entrée vide, ou sur le débordement `int`

- Oui. Pourquoi la version "Ugly" est un désastre

- Oui. Il utilise une astuce à deux listes («vals» et «sommes») sans expliquer pourquoi elle fonctionne.
- La méthode `removeLowest` est appelée `O(n)` à l'intérieur d'une boucle qui exécute `n-1` times → performance globale `O(n2)`.
- Oui. Aucune sécurité de type – potentiel `ArrayIndexOutOfBounds` si la liste est vidée prématurément.
- Difficile à déboguer; aucun essai unitaire n'est inclus.

---

- Oui. 6. Aperçu du site Web du SEO

Section du mot-clé Densité
C'est le cas.
**Titre** 1167 Solution en Java, Python, C++
**Moyen de description**=155-char résumé avec le coût minimum pour connecter des bâtons, LeetCode 1167, algorithme gourmand, min-heap
**En-tête H1**
**Intro**, 3-4 phrases contenant le coût minimum pour connecter des bâtonnets, le code 1167, le code Huffman
Utiliser le libellé officiel; ajouter les contraintes Afficher la compréhension
*Approach**==Greedy + Min-Heap===Huffman coding pattern==== Explication de base
**Complexité**
**Code**=Java, Python, sections C++, chacune avec syntaxe en surbrillance== Valeur pratique==
**Cas d'escroquerie**
Sous-rubriques avec des points de balle
**Conclusion**="Master LeetCode 1167 en minutes="Ajouter à votre portfolio="Appel à l'action="
**Tags**=LeetCode=, coût minimum pour connecter des bâtonnets==, algorithme de traitement==, lien interne==

> **Astuce**: Inclure des liens internes à vos autres billets de blog sur le code Huffman, la file d'attente prioritaire en C++, etc. Cela maintient les lecteurs sur votre site et stimule le référencement.

---

- Oui. 7. Pensées finales

- La solution **greedy + min-heap** est la *uniquement* qui s'échelonne jusqu'aux limites d'entrée maximales.
- Gardez votre code **readable** – noms de variables clairs, commentaires où l'algorithme n'est pas évident, et formatage cohérent.
- Oui. Essai contre les cas de bord: `[1]`, `[1, 2]`, `[10000] * 10000`.

> ** Prêt à accepter votre prochaine entrevue de codage? * *
> Ajoutez cette solution propre et rapide à votre portefeuille et partagez votre expérience sur LinkedIn – les recruteurs adorent voir le monde réel maîtriser LeetCode!