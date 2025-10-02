---
titre: LeetCode 810. Craie XOR Jeu -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Cracking LeetCode 810 – Jeu de tableau XOR
Les bons, les mauvais et les méchants
*(Guide SEO optimisé pour vous aider à décrocher votre prochain rôle d'ingénierie logicielle)*

---

### TL;DR

- **Problème**: Deux joueurs alternent l'effacement d'un nombre d'un tableau.
Si un mouvement rend le XOR des nombres restants égal à 0, ce joueur perd.
Si un joueur commence un tour avec XOR = 0, il gagne immédiatement.
- **Réponse**:
Texte
Alice gagne (XOR total) 0) OU (la longueur de l'arrachage est égale)
«» "
- **Pourquoi ça marche**: arguments de parité théorétique de jeu + propriété XOR.
- **Complexité**: temps «O(n)», espace «O(1)».
- **Pourquoi tu devrais le savoir**: Démontre une pensée rapide, une intuition mathématique et un code concis – le point de conversation parfait pour l'entrevue.

---

- Oui. 1. Récapitulation des problèmes

> **LeetCode 810 – Jeu XOR de Chalkboard* *
> Avec un tableau «nums», Alice et Bob retirent alternativement un seul élément.
> - Si une suppression provoque la XOR des éléments restants à devenir **0**, le joueur qui a effectué cette suppression **perde**.
> - Si un joueur commence un tour avec le XOR de tous les éléments restants égaux à **0**, ils **win immédiatement**.
> Retour `vrai` si Alice peut forcer une victoire, en supposant un jeu optimal des deux côtés.

**Contrôles* *

- Oui.
-- -- -- -- -- --
"1 ≤ longueur des nums ≤ 1000"

---

- Oui. 2. Aperçu intuitif

> Le jeu est régi par **parity** et le **initial XOR**.

1. **XOR initial = 0**
Alice commence son tour avec XOR = 0 → elle gagne instantanément.
2. **La longueur est égale**
Même longueur → après tout mouvement, le nombre d'éléments restants est étrange.
Parce que le XOR avant le mouvement est non-zéro (autrement, le cas 1 aurait déjà gagné), la seule façon pour un joueur d'éviter de perdre est de forcer l'adversaire à une position avec un nombre pair d'éléments et XOR 0, qui est une position perdante pour l'adversaire.
3. **Longueur est impair et initial XOR 0**
Chaque mouvement laisse un nombre pair d'éléments.
L'adversaire peut toujours refléter la stratégie Alice et forcer une victoire.
Alice perd donc.

> La règle concise : **Alice gagne si le XOR de tous les nombres est zéro ou si la longueur du tableau est égale. **

---

- Oui. 3. Esquisse de preuve officielle

Laissez `S` être le XOR de tous les nombres actuels, et `n` être le nombre d'éléments restants.

- **Cas de base**: Si "S" 0` au début d'un tour, le joueur pour bouger gagne.
- **Étape inductive**:
- Si `n` est **even**, le lecteur peut supprimer un élément `x` tel que `S ^ x != 0'.
Après la suppression, `n-1` est étrange, et l'adversaire fait face à une position qui est **perdant** par l'hypothèse d'induction.
- Si `n` est **odd** et `S != 0`, tout retrait donne même `n-1`.
L'adversaire peut alors gagner par la stratégie d'équilibre ci-dessus.
- Oui. Par conséquent, les seules conditions gagnantes sont `S == 0` ou `n` même.

---

- Oui. 4. Exécution

### Java

"Java
solution de classe {
xor de booléen publicGame(int[] nums) {
Total Xor = 0;
pour (int val : nombres) total Xor ^= valeur;
// Alice gagne si le XOR total est zéro ou la longueur est égale
retour total (longueur numérique % 2) 0);
}
}
«» "

Python

'`python
Solution de classe:
def xor Jeu(self, nombres: List[int]) -> bool:
_xor total = 0
pour v en chiffres:
Total_xor ^= v
# Alice gagne si le XOR total est zéro ou la longueur est égale
retourner total_xor == 0 ou len(nums) % 2 == 0
«» "

C++

'`cpp
solution de classe {
public:
bool xorGame(vecteur<int>& nums) {
Total Xor = 0;
pour (int v : nombres) total Xor ^= v;
// Alice gagne si le XOR total est zéro ou la longueur est égale
retour totalXor == 0=0 (nums.size() % 2=0);
}
};
«» "

Les trois extraits se déroulent dans **O(n)** temps et **O(1)** mémoire supplémentaire.

---

- Oui. 5. Les bonnes

Explication
C'est quoi ?
Une seule analyse linéaire; aucune récursion ou DP nécessaire. Autres
**Clarté**La condition reflète directement le théorème; facile à raisonner. Autres
**L'impact de l'interview**Shows vous pouvez réduire un jeu apparemment complexe à un simple contrôle de parité. Autres
**Les arguments XOR + parité apparaissent dans de nombreux problèmes d'entrevue de style Nim. Autres

---

- Oui. 6. Les mauvais (Pitfalls à éviter)

Erreurs courantes
-- -- -- -- -- --
**En supposant que XOR est un jeu d'enfant**
**Ignorer la longueur du tableau** Autres
**PDD récursif** Autres
Erreurs hors-par-un** Autres

---

- Oui. 7. L'Ugly

Cas de bord et éclaircissements Autres
Il n'y a pas de lien entre les deux.
**Réseau d'empattement**. Autres
**Tous les zéros**=XOR = 0 → Alice gagne immédiatement, même si la longueur est étrange. Autres
**Les plus grands nombres**= XOR fonctionne jusqu'à "2^16" en toute sécurité; utiliser des ints 32 bits. Autres
**Mise en échec de la règle**=Enlèvement d'un élément qui fait perdre XOR = 0 – rappelez-vous que c'est le *joueur qui fait ce mouvement* qui perd, pas celui qui commence avec XOR = 0.=

---

- Oui. 8. Points d'entrevue prêts à parler

1. ** Expliquez l'argument de parité** – pourquoi même la longueur garantit une victoire.
2. **Afficher la case de base** – commencer XOR = 0 donne une victoire instantanée.
3. **Mention le théorème** – la condition de réussite concise.
4. **Démonstration du code** – gardez-le un seul liner.
5. ** Temps et espace** – mettre l'accent sur l'optimisation.

J'ai résolu le LeetCode 810 en un seul passage en observant que le XOR de tous les nombres étant zéro ou le tableau ayant une longueur égale est le critère exact pour gagner Alice. Cela démontre ma capacité à distiller des problèmes complexes de jeu-théorique en solutions élégantes, O(n).

---

- Oui. 9. Mots clés du référencement (pour le classement de blog)

- Jeu XOR Chalkboard
- Solution LeetCode 810
- Théorie du jeu XOR
- Jeu de stratégie optimal
- Question d'entretien de la théorie du jeu
- Problèmes d'entrevue Bitwise XOR
- Même la longueur de la victoire condition
- Python Java C++ Jeu XOR
- Défis de codage des entrevues

---

## 10. A emporter

Le XOR de Chalkboard Le jeu est un exemple de la façon dont **simple math** peut transformer un jeu apparemment complexe en un puzzle logique de taille **. En se concentrant sur les propriétés XOR et la parité des tableaux, vous pouvez fournir une solution qui est:

- **Fast** ('O(n)')
- **Efficacité de la mémoire** ('O(1)')
- **Amis à l'interview** – parfait pour montrer la pensée analytique.

Utilisez ceci comme tremplin pour d'autres problèmes de style Nim, et vous impressionnerez les intervieweurs avec élégance et rapidité. Bonne chance pour le prochain rôle ! C'est ce qu'il a dit