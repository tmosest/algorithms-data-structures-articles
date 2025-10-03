---
titre: LeetCode 2214. Santé minimum pour battre le jeu -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La santé minimale pour battre le jeu – Solution 3-Langue + Blog pour les demandeurs d'emploi

Vous trouverez ci-dessous une application propre et prête à la production du problème LeetCode **2214. Santé minimum pour battre le jeu** en **Java, Python et C++**.
Après le code, un billet de blog de style *= bon, mauvais, laid=== explique l'astuce derrière la solution, les pièges communs, et comment vous pouvez transformer cette question d'entrevue en une vitrine pour les recruteurs.

---

- Oui. 1. Récapitulation des problèmes

> **Vous jouez à un jeu avec des niveaux séquentiels `n`. **
> `dommage[i]` = la santé que vous perdez au niveau `i`.
> Vous avez une armure qui peut être utilisée **une fois** pour annuler jusqu'à des dommages `armor` au niveau **any**.
> Votre santé doit rester **> 0** en tout temps.
> Retourner la santé minimale de départ nécessaire pour terminer tous les niveaux.

Contraintes
«» "
1 ≤ n ≤ 10^5
0 ≤ dommages[i], armure ≤ 10^5
«» "

---

- Oui. 2. Solution O(n) – Le sous-titrage «Greedy‐+»

1. **Défaut total** vous prendrez si vous n'utilisez jamais l'armure:
`sum = γ dommages[i] "
2. Le meilleur endroit pour utiliser l'armure est le niveau ** unique qui inflige le plus de dommages** (appelez-le `maxDamage`).
– Si `armor ≥ maxDamage` vous pouvez annuler complètement ce niveau.
– Si `armor < maxDamage` vous annulez seulement les points `armor`.
3. Santé minimale initiale = `sum – min(maxDamage, armure) + 1`.
Le +1 est nécessaire parce que la santé doit rester ** strictement positive**.

Pourquoi ça marche :
En annulant les dommages les plus importants, vous réduisez le plus le dommage total, et aucun autre placement de l'armure ne peut donner une réduction plus importante. Puisque vous ne vous souciez que de la somme des dommages, ce choix gourmand est optimal.

Complexités
- **Heure**: O(n) – un passage pour calculer la somme et max.
- **Espace**: O(1) – mémoire supplémentaire constante.

---

- Oui. 3. Mise en œuvre du code

#### 3.1 Java

"Java
le code de l'emballage;

solution de classe publique {
***
* Santé minimum pour battre le jeu - O(n) temps, O(1) espace.
* Tableau de dommages @param des valeurs de dommages par niveau
* @param armure maximum de dommages qui peuvent être annulés une fois
* @retour minimum santé de départ pour terminer tous les niveaux
*/
public long minimumSanté(int[] dommages, armure int) {
somme longue = 0;
Int maxDamage = 0;

pour (int dmg : dommages) {
somme += dmg;
si (dmg > maxDamage) maxDamage = dmg;
}

longue réduction = Math.min(maxDamage, armure);
somme de retour - réduction + 1;
}
}
«» "

3.2 Python

'`python
Solution de classe:
def minimumHealth(self, damage: list[int], armure: int) -> Int:
""Temps O(n), solution d'espace O(1).""
total = somme (dommage)
max_damage = max(damage, par défaut=0) # par défaut pour la liste vide (pas nécessaire ici)
réduction = min(max_dommage, armure)
total de retour - réduction + 1
«» "

### 3.3 C++

'`cpp
solution de classe {
public:
long minimumSanté(vecteur<int>& dommages, armure int) {
long total = 0;
Int maxDamage = 0;

pour (int dmg : dommages) {
total += dmg;
maxDamage = max(maxDamage, dmg);
}

longue réduction longue = min(static_cast<long long>(maxDamage), statique_cast<long long>(armor);
total de retour - réduction + 1;
}
};
«» "

> Les trois extraits compilent avec Java 17, Python 3.10+ et C++17 (GCC/Clang).

---

- Oui. 4. Article de blog: -Le bon, le mauvais, et l'acharnement de la santé minimum pour battre le jeu

> **Keyword Focus:** LeetCode, Minimum Health to Beat Game, algorithme d'entrevue, entretien de codage Java, entretien Python, entretien C++, conseils d'entrevue de codage, entretien d'emploi, conception d'algorithmes, solution O(n), succès d'entrevue.

---

Titre

**Le bon, le mauvais, et l'acharnement de LeetCode 2214 – Guide de la santé minimale pour battre le jeu**

---

Introduction

Si vous êtes en train de vous préparer pour des entretiens d'ingénierie de logiciels, vous allez courir sur LeetCode. À la surface, il ressemble à un cauchemar de programmation dynamique, mais avec la bonne idée, il se résume à un seul liner. Cet article divise le problème en trois parties – *Bon*, *Bad* et *Ugly* – pour vous aider à maîtriser la question et impressionner les recruteurs.

---

C'est vrai. Les bonnes

Autres Pourquoi ça compte ?
-- -- -- -- -- --
**Single-Pass O(n)**=Les intervieweurs adorent les solutions linéaires et spatiales. Autres
**L'utilisation de l'armure sur le niveau de dommages *maximum* est un choix propre et logique que tout codeur assaisonné peut voir immédiatement. Autres
**Réponse = somme (dommage) - min(maxDamage, armure) + 1`. Pas de boucles cachées ou de tables DP. Autres
**Language Agnostique** Allez, JavaScript – idéal pour les démos de portfolio. Autres
Autres ** Exécute en < 1 ms sur 105 entrées. Autres

**À emporter :** *Montrer au recruteur que vous pouvez repérer l'optimum gourmand. *

---

C'est vrai. Les mauvais

Piège commun
-- -- -- -- --
Oublier le `+1`= N'oubliez pas: la santé doit rester ** strictement positive**; sinon vous aviez commencé à zéro. Autres
En utilisant `long`/`long long` en Java/C++. Les sommes de dommages peuvent atteindre `10^5 * 10^5 = 10^10`; débordement en int 32-bits. Autres
Ignorer `armor = 0`" Votre formule fonctionne toujours, mais vérifier la logique pour éviter `-1` santé. Autres
Vous ne pouvez pas diviser l'armure sur deux niveaux – un seul appel. Autres

**À emporter :** *La conscience du cas d'Edge est la différence entre le bon et l'excellent. *

---

C'est vrai. L'Ugly

La complexité cachée Pourquoi les intervieweurs la détestent
-- -- -- -- -- -- -- -- -- --
Pensant en DP.Un DP 2-D au-dessus de l'armure utilisée ou non. Autres
Autres La suringénierie du placement de l'armure.La construction d'un arbre de segment ou d'une file d'attente prioritaire pour suivre les dommages maxi est inutile et rend la solution illisible. Autres
Erreurs hors-par-un. Le fait de manquer le `+1` ou d'utiliser `maxDamage - armure` au lieu de `min(maxDamage, armure)` conduit à WA. Autres

**À emporter :** *Éviter la suringénierie. Gardez-le maigre et expliquez pourquoi l'avidité est optimale. *

---

### Solution étape par étape

1. ** Calculer les dommages totaux**
'`python
Total = somme (dommage) # O(n)
«» "
2. **Trouver le plus grand dommage* *
'`python
max_dommage = max(dommage)
«» "
3. **Réduction du calcul**
'`python
réduction = min(max_dommage, armure)
«» "
4. **Réponse**
'`python
total de retour - réduction + 1
«» "

> **Proof d'optimalité:**
> Tout placement de l'armure réduit les dommages par au plus `armor`. La réduction *la plus importante* que vous pouvez atteindre est `min(max_dommage, armure)` parce que vous ne pouvez annuler les dommages qu'à un seul niveau. Aucune autre configuration ne peut donner une réduction plus grande, donc l'avidité est optimale.

---

- Oui. Comment faire pour clouer Dans une interview

1. **Parler le langage du problème** – mentionner -Damage array, -Armor utilisé une fois.
2. **Outline l'idée gourmande d'abord** – -I-ll annuler le plus grand succès – pour montrer votre intuition.
3. **Écrire le code en un seul passage** – mettre l'accent sur le temps O(n) et l'espace O(1).
4. ** Cas de limites d'essai** – par exemple, «armor = 0», «dommage = [0, 0]», «dommage[i] = 10^5».
5. **Exposer le +1** – une surveillance commune; recruteur aimera la clarté.

---

- Oui. Bonus : Ce que les recruteurs recherchent

Exemple de ce problème
C'est ce que j'ai dit.
**Efficacité algorithmique** Autres
**Connaissance de la réduction gourmande. Autres
**Lisibilité du code**= Effacer les noms de variables (`sum`, `maxDamage`, `reduction`). Autres
**Manipulation des caisses d'Edge** Autres
**La communication** Autres

> Délivrez cette question dans une repo de portfolio, une diapo ou une démo de codage en direct, et vous aurez une histoire d'entrevue solide qui met en valeur tous ces traits.

---

Clôture

LeetCode 2214 est un exemple de manuel d'un questionnement de point: un problème apparemment complexe qui s'effondre à une simple formule gourmande. Maîtrisez-le, expliquez la preuve, et vous éviterez non seulement les écueils *mauvais* mais transformerez aussi la suringénierie *meuglement* en une vitrine de pensée propre. Bonne chance pour votre prochain entretien de codage ! C'est ce qu'il a dit.

---



### TL;DR pour les demandeurs d'emploi

- **Problème:** Santé minimale de départ avec une armure unique.
- **Solution:** `réponse = -dommage – min(maxDamage, armure) + 1`.
- **Complexités:** temps O(n), espace O(1), arithmétique à temps constant.
- **Langues:** Java, Python, C++ (voir le code ci-dessus).
- **Conseil d'entrevue :** Concentrez-vous sur l'intuition gourmande, la clarté de la casse et évitez la suringénierie.

Bon codage et bonne chance sur vos entretiens!