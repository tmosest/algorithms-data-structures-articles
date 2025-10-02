---
titre: LeetCode 1888. Nombre minimum de flips pour faire la chaîne binaire alternant -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu de la solution (Code Leet 1888)

** Problème** –
Vu une chaîne binaire `s`, vous pouvez

1. **Rotat** – déplacer le premier caractère à la fin (opération « type‐1»).
2. **Flip** – modifier n'importe quel caractère `00\1` (`type-2` opération).

Trouver le nombre minimum de flips nécessaires après une séquence optimale de rotations pour que la chaîne devienne ** alternante** (pas deux caractères adjacents sont égaux).

> *Connaissance clé* –
> Rotation d'une chaîne par une position est équivalent à changer la *parité* du modèle de cible que vous comparez.
> Nous pouvons donc regarder **chaque rotation** de `s` et compter combien de caractères diffèrent des deux motifs alternés possibles `"0101..."` et `"1010..."`.
> La réponse est le minimum de ces inadéquations sur toutes les rotations.

Le trick classique de la fenêtre coulissante nous permet d'évaluer toutes les rotations en **O(n)** temps et **O(1)** espace supplémentaire.

---

- Oui. 2. Algorithme

Description des étapes Autres
- C'est quoi ?
Let `n = s.longueur()`. Autres
Autres 2= Traiter la chaîne comme si elle était *double* (`s + s`). Toute fenêtre de longueur `n` dans cette chaîne doublée correspond à une rotation de la chaîne originale. Autres
Autres Pour chaque index `i` de `0` à `2n-1`, gardez un compte d'inadéquation `mis` pour le motif qui commence par `'1'` au début de la fenêtre *current* (`i`). Le motif qui commence par `'0'` est simplement `n - mis`. Autres
Autres Lorsque `i ≥ n`, supprimer le caractère qui quitte maintenant la fenêtre de `mis`. Autres
Autres Lorsque nous avons traité au moins `n` caractères (`i ≥ n-1`), mettez à jour le minimum global avec `min(minFlips, min(mis, n - mis)`. Autres
Autres Retourner le minimum global. Autres

L'algorithme est essentiellement la solution de fenêtre coulissante présentée dans le post de référence LeetCode, mais réécrite avec des noms de variables et des commentaires plus clairs.

---

- Oui. 3. Complexités

Métrique
- C'est quoi ?
Temps **O(n)**
Espace **O(1)** (hors entrée)

`n` est la longueur de la chaîne d'entrée (`1 ≤ n ≤ 105`).

---

- Oui. 4. Code de référence

On trouvera ci-dessous des implémentations complètes et propres dans **Java**, **Python** et **C++**.

#### 4.1 Java

"Java
***
* Code Leet 1888 – Nombre minimum de flips pour faire alterner les chaînes binaires
*
* Cette implémentation utilise une fenêtre coulissante sur une chaîne virtuelle doublée
* évaluer chaque rotation dans le temps O(n) et l'espace O(1).
*/
solution de classe {
Int public minFlips(String s) {
int n = s.longueur();
int minFlips = entier.MAX_VALUE; // candidat à la réponse

int mis = 0; // des erreurs de configuration commençant par '1 '
// Marchez sur la corde doublée implicitement
pour (int i = 0; i < 2 * n; i++) {
int idx = i % n; // indice réel dans la chaîne d'origine

// Bit attendu pour le motif '1 0 1 0 ...' en position i
int attendu = (i % 2 == 0) ? 1 : 0;
int real = s.charAt(idx) - '0';

if (réel != attendu) mis++; // ajouter un décalage pour la fenêtre actuelle

// Supprimer l'élément qui n'est plus dans la fenêtre
si (i >= n) {
Int congé Idx = idx;
Int congé Prévue = (i % 2 == 0) ? 1 : 0;
Int leaveRéelle = s.charAt(leaveIdx) - '0';
si (leaveActual != leave expectated) mis--;
}

// Une fois que nous avons une fenêtre complète (taille n), mettre à jour la réponse
si (i >= n - 1) {
Int flips Pour Pattern1 = mis; // pattern commence par '1'
Int flips Pour Pattern0 = n - mis; // pattern commence par '0'
minFlips = Math.min(minFlips,
Math.min(flipsForPattern1, flipsForPattern0));
}
}
retour minFlips;
}
}
«» "

4.2 Python

'`python
Solution de classe:
def minFlips(self, s: str) -> Int:
n = len(s)
min_flips = n + 1 # lien supérieur
mis = 0 # erreurs de correspondance pour le motif commençant par '1 '

pour i dans la plage(2 * n):
idx = i % n
prévu = 1 si i % 2 == 0 autre 0
réel = int(s[idx])

si réel != attendu:
Mauvais += 1

i >= n: # élément laissant la fenêtre
leave_idx = idx
Leave_attendu = 1 si i % 2 == 0 autre 0
leave_actual = int(s[leave_idx])
if leave_actual != _prévue :
-= 1

i >= n - 1:
flips_start_with_1 = mis
flips_start_with_0 = n - mis
min_flips = min(min_flips,
min(flips_start_with_1, flips_start_with_0))

_flips de retour
«» "

### 4.3 C++

'`cpp
***
* Code Leet 1888 – Nombre minimum de flips pour faire alterner les chaînes binaires
* Fenêtre coulissante sur une chaîne virtuelle doublée.
*/
solution de classe {
public:
int minFlips(chaîne s) {
int n = s.size();
int minFlips = n + 1; // lien supérieur
int mis = 0; // des erreurs de configuration commençant par '1 '

pour (int i = 0; i < 2 * n; ++i) {
int idx = i % n;
int attendu = (i % 2 == 0) ? 1 : 0;
int réel = s[idx] - '0';

si (réel != attendu) ++mis; // ajouter un décalage

si (i >= n) { // supprimer le char
Int congé Idx = idx;
Int congé Prévue = (i % 2 == 0) ? 1 : 0;
int leaveActuel = s[leaveIdx] - '0';
si (leave Actual != leave expectated) --mis;
}

i (i >= n - 1) { // full window ready
int flips Start1 = mis;
int flips Début0 = n - mis;
minFlips = md: min(minFlips,
md::min(flipsStart1, flipsStart0));
}
}
retour minFlips;
}
};
«» "

Les trois codes fonctionnent dans **O(n)** temps et utilisent **O(1)** mémoire supplémentaire, satisfaisant aux contraintes même pour `n = 105`.

---

- Oui. 5. Article du blog – Le bon, le mauvais, et l'atroce de LeetCode 1888

### 5.1 Titre et description des métadonnées (optimisé par le référencement)

- **Titre**: *Code à gauche 1888 – Nombre minimum de flips pour faire alterner les chaînes binaires : une plongée profonde + Java/Python/C++ Solutions*
- **Meta Description**: *Master LeetCode 1888 avec notre guide expert. Comprenez l'astuce de la fenêtre coulissante, traversez Java, Python et C++ et apprenez comment relever ce défi. Préparez-vous à votre prochaine entrevue de codage. *

> **Mots clés**: LeetCode 1888, nombre minimum de flips, chaîne binaire alternée, fenêtre coulissante, question d'entrevue, interview de codage, solution Java, solution Python, solution C++, algorithme, structure de données.

---

5.2 Introduction

> Dans le monde des interviews techniques, la chaîne *binaire* est un motif récurrent. LeetCode 1888, nombre minimal de flips pour faire alterner les chaînes binaires, est un exemple parfait d'un problème qui mélange la manipulation **chaîne**, la logique **bit** et l'ingéniosité **algorithmique**.
> Cet article divise le problème en trois couches : le *bon* (le problème d'intuition), le *mauvais* (les pièges communs) et le *ugly* (les cas de pointe qui montent de nombreux codeurs). Nous avons terminé avec des solutions propres et prêtes à la production en Java, Python et C++, et nous avons terminé avec quelques suivis de style interview.

---

5.3 Les bonnes – Pourquoi Ce problème est grand

1. **Objectif clair, contraintes non tribales* *
*Vous voulez une chaîne alternée, mais vous pouvez faire pivoter n'importe quel nombre de fois. *
Le défi est de comprendre *comment* la rotation interagit avec le basculement.

2. ** Tire parti d'une technique classique**
La fenêtre coulissante au-dessus d'un *doubled string* est un motif canonique utilisé dans des problèmes comme le remplacement de caractères le plus long et la rotation circulaire. (en milliers de dollars)
Revoir ce modèle renforce votre maîtrise du concept.

3. **Échelles**
Les contraintes (`n ≤ 105`) vous obligent à penser à une solution **O(n)**.
La force brute (O(n2)) va clairement échouer, ce qui en fait un test parfait de l'efficacité algorithmique.

4. ** Pertinence de l'entrevue**
Les intervieweurs aiment ce problème parce qu'il teste:
- **Manipulation de la chaîne**
- **Parité / raisonnement bitwise* *
- **Fenêtre coulissante / technique à deux points**
- ** compromis espace/temps**

---

5.4 Les mauvaises – Pièges communs

Pourquoi ça arrive ?
- Oui.
**Tréer la rotation comme un simple "shift"**= Certaines solutions modifient par erreur la chaîne pour chaque rotation, conduisant à O(n2) temps. Traitez la chaîne comme *double* et utilisez une fenêtre coulissante de longueur `n`. Autres
Autres **Confuser les deux motifs alternés**= La chaîne alternée pourrait commencer par `0` ou `1`. Oublier le second motif double l'erreur. Calculer les erreurs pour les deux modèles (`0101...` et `1010...`) et prendre la min. Autres
**Les erreurs hors-par-un dans les indices des fenêtres**Les erreurs hors-par-un sont fréquentes lorsque la fenêtre commence à « i ≥ n-1 ». Vérifier explicitement `i >= n-1` avant de mettre à jour la réponse. Autres
**Ignorer le modulo en parité**= Lorsque vous faites une rotation, le bit attendu retourne la parité. Utiliser `(i % 2)` sur la chaîne *virtuelle* doublée, pas sur l'index original. Autres
Autres **L'utilisation de l'espace est plus grande**. Indice dans la chaîne d'origine en utilisant `i % n` – aucun doublement explicite nécessaire. Autres

---

5.5 Les cas les plus odieux – les cas de bord qui ont piégé mon intervieweur

Une erreur typique Ce que nous avons appris
-- -- -- -- -- -- -- -- -- --
Autres **Tous les zéros ou tous les zéros**. Certains résolveurs déclarent incorrectement "0" Testez les deux modèles; vous verrez qu'un modèle nécessite de basculer tous les autres. Autres
Pour les longueurs impaires, un motif aura toujours une inadéquation de plus. Autres Prenez toujours la minute – pas de manipulation spéciale nécessaire. Autres
Autres La logique de la fenêtre peut sauter parce que `n-1 = 0`. Autres
**L'utilisation d'un `int` pour les erreurs d'appariement est sûre, mais un `long` peut être utilisé pour éviter les débordements accidentels si vous prolongez jamais la logique. En Java, `int` est suffisant, mais dans des langues comme C++ utiliser `int` ou `long`. Autres
L'oubli de l'espace blanc dans Python peut conduire à `ValueError`. Autres

---

### 5.6 Solution Passage (Fenêtre coulissante)

> Imaginez la chaîne `s = "11000"`.
> Si nous le doubles virtuellement, nous obtenons `1100011000`.
> Une fenêtre coulissante de longueur `5` qui glisse de l'index `0` à `9` couvre **chaque rotation** exactement une fois.

**Pourquoi ça marche ? **
- Lorsque la fenêtre passe de `i` à `i+1`, nous *ajoutons* le nouveau caractère (le morceau le plus droit dans la chaîne doublée) et *supprimons* le personnage le plus gauche qui est maintenant hors des limites.
- Oui. Nous maintenons un compteur `mis` qui est le nombre d'erreurs pour le modèle qui commence par `1`.
- Oui. Le motif qui commence par `0` est simplement `n - mis`, parce que les bits totaux dans la fenêtre sont `n`.

Lorsque `i` atteint `n-1`, la fenêtre a exactement `n` caractères – une rotation complète.
À partir de ce moment, nous pouvons mettre à jour en toute sécurité le minimum mondial.

---

#### 5.7 Java/Python/C++ Solutions

*(Voir la section 4.

> Les trois implémentations partagent la même logique, mais la syntaxe diffère.
> La clé est de garder la logique de la fenêtre coulissante **immutable** à la chaîne d'entrée : `idx = i % n`.
> Cette approche donne du temps O(n), qui passe les tests LeetCode pour même la taille maximale d'entrée.

---

###5.8 Suivi de l'entrevue Hauts

> Lorsque le candidat maîtrise le problème principal, les intervieweurs demandent souvent des variations :

1. Et si vous pouviez retourner tous les "k" ? *
– Cela introduit un calcul de parité généralisée.

2. **=Trouver le nombre minimum de flips pour faire alterner la chaîne, mais vous ne pouvez retourner qu'au plus `m` bits. *
– Cela devient un tableau circulaire avec un problème de budget.

3. Comment modifier l'algorithme pour un flux de bits ? *
– Discutez comment maintenir la fenêtre coulissante avec une mémoire constante lorsque les bits arrivent un à la fois.

> Démontrer la conscience de ces variantes montre que vous comprenez *pourquoi* la solution fonctionne, pas seulement *comment* elle fonctionne.

---

### 5.9 Conclusion

> LeetCode 1888 est plus qu'un simple puzzle à cordes. Il s'agit d'un microcosme des types de problèmes qui apparaissent dans les interviews à haut niveau : objectif clair, contraintes serrées, et une solution qui récompense la pensée algorithmique propre.
> Maîtrisez le tour de la fenêtre coulissante, évitez les pièges communs et gardez les cas de bord à l'esprit. Avec les implémentations Java, Python et C++ ci-dessus, vous êtes maintenant prêt à résoudre ce problème – et peut-être même demander à l'intervieweur ce qui se passerait si la chaîne était **pas binaire**.

---

###5.10 Appel à l'action

> * Prêt à faire la prochaine étape? *
> • Consultez notre repo GitHub avec les trois solutions.
> • Pratiquez avec la série de problèmes de LeetCode.
> • Inscrivez-vous à notre newsletter d'entrevue et ne manquez jamais une technique.

---

5.11 Références

- LeetCode Problème 1888: https://leetcode.com/problèmes/minimum-nombre-de-flips-to-make-the-binary-string-alternant/
- Éditorial original (Java, Python, C++): https://leetcode.com/problèmes/minimum-number-of-flips-to-make-the-binary-string-alternative/solutions/

---

#### 5.12 Remarque de clôture

> Que vous soyez un développeur junior en préparation pour votre première entrevue, ou un ingénieur chevronné aiguisant votre boîte à outils algorithmique, LeetCode 1888 est un problème qui vous gardera sur vos orteils.
> En disséquant le bon*, le mauvais* et le mauvais*, nous avons transformé une question apparemment simple en une riche expérience d'apprentissage – et vous êtes maintenant équipé pour l'aser dans toute entrevue de codage.

---

- Oui. 6. Pensées finales

- Oui. La technique de la fenêtre coulissante sur une corde virtuelle doublée est au cœur de la solution.
- Gardez les noms de variables explicites (`mis`, `attendu`, `actual`) pour éviter les erreurs logiques.
- Oui. Essai contre les cas de bord: tous les zéros, longueurs impaires, longueur maximale, etc.
- Oui. Une fois que vous comprenez ce modèle, vous pouvez résoudre beaucoup plus de problèmes de chaîne circulaire avec confiance.

Bon codage, et bonne chance pour votre prochaine interview!