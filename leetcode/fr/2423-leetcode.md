---
titre: LeetCode 2423. Supprimer la lettre pour égaliser la fréquence -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Code de Leet 2423 – Supprimer la lettre pour égaliser la fréquence
Les solutions C++** de Python et un post complet **blog** qui vous fera remarquer par les recruteurs.

---

- Oui. 1. Le problème (dans une phrase)

> Avec une chaîne minuscule `word`, pouvez-vous supprimer **exactement un** caractère de sorte que chaque caractère restant apparaît le même nombre de fois?

---

- Oui. 2. Brute-Force vs. Greedy – Le bon, le mauvais, le mauvais

Ce que vous faites Pourquoi ça compte
- Oui.
**Bon**. Compter les fréquences une fois, puis *simuler* enlever une lettre à la fois et vérifier les fréquences restantes. Exécute dans *O(262) = O(1)* temps (constamment parce que la taille de l'alphabet est fixe). Autres
Essaie toutes les suppressions possibles (temps O(n2)) et recompte après chaque suppression. Autres Fonctionne mais est inutile frais généraux; plus lentement sur les chaînes plus longues. Autres
Oubliez que la chaîne peut contenir **une seule lettre distincte** ou **deux** – cas de bord qui font votre code planter ou retourner de mauvais résultats. Autres Beaucoup d'intervieweurs s'interrogent sur les cas de bord; les manquer signifie que vous perdrez des points. Autres

---

- Oui. 3. L'algorithme de validation de la fréquence de l'avidité

1. **Compte de fréquence** – Construisez un tableau de 26 int ('freq[26]').
2. **Essayez d'enlever chaque caractère** – Pour chaque `i` tel que `freq[i] > 0`:
* Diminuer `freq[i]` de 1 (simuler la suppression).
* Vérifier si * toutes les fréquences non nulles sont égales*:
* Saisissez la première valeur non nulle comme la cible.
* Si toute autre valeur non nulle diffère → cette suppression **fails**.
* Restaurer `freq[i]` avant de passer.
3. **Retour** `true` si une suppression a réussi; sinon `faux`.

Parce que la taille de l'alphabet est constante, l'algorithme fonctionne dans **O(1)** temps et utilise **O(1)** mémoire supplémentaire.

---

- Oui. 4. Code – Trois langues

---

#### Java (style LeetCode)

"Java
solution de classe {
booléen public égal Fréquence (mot de frappe) {
int[] freq = nouveau int[26];
pour (int i = 0; i < word.longueur(); i++) {
freq[word.charAt(i) - 'a']++;
}

pour (int i = 0; i < 26; i++) {
Si (freq[i]) 0) poursuivre;

freq[i]-; // simulent l'enlèvement
cible int = 0;
booléen ok = vrai;

pour (int j = 0; j < 26; j++) {
si (freq[j]] 0) poursuivre;
si (cible) 0) cible = freq[j];
sinon si (freq[j] != cible) { ok = false; break; }
}

freq[i]++; // restaurer
si (ok) retourner vrai;
}
retourner faux;
}
}
«» "

> **Pourquoi il brille** – Simple, utilise seulement un tableau de taille fixe, et suit le raisonnement optimal O(1).

---

Python

'`python
Solution de classe:
def égal Fréquence(self, mot: str) -> C'est vrai.
freq = [0] * 26
pour ch en mot:
freq[ord(ch) - 97] += 1

pour i dans la fourchette(26):
si freq[i] == 0:
poursuivre

[i] 1 # simulent l'enlèvement
cible = Aucune
ok = Vrai

pour f en freq:
si f == 0:
poursuivre
si la cible est None:
cible = f
elif f != cible:
ok = Faux
pause

freq[i] += 1 # restaurer
si oui:
retour Vrai

Retour Faux
«» "

> ** Touches pyroniques** – la compréhension de la liste pourrait être utilisée, mais la lisibilité est primordiale ici.

---

C++

'`cpp
solution de classe {
public:
bool egalFrequence(mot chaîne) {
vecteur <int> freq(26, 0);
pour (char c : mot) freq[c - 'a']++;

pour (int i = 0; i < 26; ++i) {
Si (freq[i]) 0) poursuivre;

freq[i]-; // simulent l'enlèvement
cible int = -1;
bool ok = true;

pour (int f : freq) {
si (f) 0) poursuivre;
si (cible) -1) cible = f;
sinon si (f != cible) { ok = false; break; }
}

freq[i]++; // restaurer
si (ok) retourner vrai;
}
retourner faux;
}
};
«» "

> **Note C++** – Utilise `vector<int>` pour la simplicité; l'algorithme reste le même.

---

- Oui. 5. Récapitulation de la complexité

Langue Heure Espace
- C'est quoi ?
Java O(1) (262 itérations)
Python O(1)
(En milliers de dollars des États-Unis)

> Pourquoi le temps constant? La taille de l'alphabet est fixe (26 lettres), donc toutes les boucles sont limitées par cette constante.

---

- Oui. 6. Article de blog optimisé par le SEO

> **Titre**
> *Supprimer la lettre pour égaliser la fréquence – Maîtriser le problème LeetCode 2423 (Java, Python, C++)* *

---

C'est vrai. 1. Présentation

Lorsque les recruteurs recherchent des solutions *LeetCode*, le problème « Supprimer la lettre pour égaliser la fréquence » est une vitrine parfaite. Il combine le comptage des fréquences, la validation gourmande et la manipulation des cas de bord, qui sont tous des éléments essentiels des entrevues d'ingénierie logicielle. Ci-dessous, nous passerons par une solution concise et prête à la production en **Java**, **Python** et **C++**, puis nous plongerons dans le «Good, the Bad, and the Ugly» de résoudre ce défi.

---

C'est vrai. 2. Récapitulation des problèmes

*On vous donne une corde minuscule. Supprimez exactement un caractère pour que chaque caractère restant ait la même fréquence. Retour `true` si possible, sinon `faux`. *

---

C'est vrai. 3. Aperçu de base

> **Nombres de fréquence + suppression d'un caractère = contrôle à temps constant* *

Parce que l'alphabet est fixé, nous pouvons :
1. Comptez chaque lettre une fois.
2. Pour chaque lettre avec un nombre non nul, prétendons que nous avons supprimé un événement.
3. Vérifier si toutes les fréquences non nulles sont égales.

Si un renvoi satisfait à la condition d'égalité, la réponse est «vraie».

---

C'est vrai. 4. Pourquoi le contrôle de l'avidité est optimal

Raison de détail
C'est quoi ?
**O(1) Temps**=26 lettres → au plus 26×26 itérations. Autres
**O(1) Espace**= Seulement un tableau/vecteur de 26 éléments. Autres
**Pas de Re-Scanning**. Nous ne reconstruisons pas la corde; nous décrémentons et rétablissons les nombres. Autres
**Déterministe** Autres

---

C'est vrai. 5. Passage du code (Java)

1. Construire le tableau `freq`.
2. Bouclez chaque lettre.
3. `freq[i]--` → simuler la suppression.
4. Trouvez la première fréquence non nulle (`cible`).
5. Comparez le reste; si vous avez des différences → pause.
6. Restore `freq[i]++`.
7. Return `true` le cas échéant, sinon `faux`.

(extrait de code complet prévu à la section 4.)

---

C'est vrai. 6. Cas de bord que vous devez passer

Pourquoi ça compte ?
- C'est quoi ?
Autres **Toutes les lettres sont identiques** (par exemple, "aaaa""). Autres
Autres **Deux lettres avec des nombres différents** (par exemple, "aabbc""). Un cas d'Edge qui peut monter une simple boucle. Autres
Autres ** Longueur de la boucle 2**. Toujours `true` parce que vous pouvez toujours en retirer une pour laisser une seule lettre. Plus petite entrée; facile à manquer. Autres
**Déjà des fréquences égales** Certaines solutions renvoient par erreur `vrai` immédiatement. Autres

---

C'est vrai. 7. Pièges communs (Le "Bad" et "Ugly")

Piège
- Oui.
**O(n2) approche** – suppression de chaque caractère et recomptage. Utilisez la validation de fréquence gourmande ; pas besoin de reconstruire la chaîne. Autres
**N'ayant pas rétabli le compte** après une suppression d'essai. Toujours `freq[i]++` après la vérification. Autres
**Ignorer les fréquences zéro** – les traiter comme une fréquence valide. Sautez les zéros en comparant. Autres
**Missundercompréhension exacte d'une suppression** – permettant de ne rien faire. Assurez-vous que la boucle diminue toujours avant la vérification. Autres

---

C'est vrai. 8. À emporter pour les intervieweurs

> **=Je peux résoudre cela dans l'espace O(1) temps et O(1), gérer tous les cas de bord, et je peux expliquer clairement le raisonnement. *

Montrer la solution en trois langues démontre la polyvalence et une bonne compréhension des fondamentaux des structures de données.

---

C'est vrai. 9. Réflexions finales

Le problème de la lettre d'élimination pour égaliser la fréquence est trompeurment simple, mais est un grand test de litmus pour:

* Compter efficacement les fréquences.
* Penser en termes de *simulation* plutôt que de *reconstruction*.
* Manipulation des cas bord gracieusement.

La maîtrise de ce problème augmente non seulement votre score LeetCode, mais affûte également les compétences de base que les recruteurs recherchent chez un ingénieur logiciel.

---

10 ans. Mots clés & référencement Étiquettes

- LeetCode 2423
- Supprimer la lettre pour égaliser la fréquence
- Algorithme de comptage des fréquences
- Question d'entretien avec l'algorithme Greedy
- Solution d'entretien Java
- Entretien de codage Python
- C++ Solution LeetCode
- Entretien avec l'ingénieur logiciel
- Problème de codage des entretiens d'emploi
- Structures de données et algorithmes

---

Bon codage, et bonne chance avec votre prochaine interview! C'est ce qu'il a dit