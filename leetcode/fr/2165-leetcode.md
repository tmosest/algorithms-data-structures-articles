---
titre: LeetCode 2165. Valeur la plus faible du nombre réaménagé -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La valeur la plus petite du nombre réarrangé** – Le bon, le mauvais et le mauvais
**Code de cap #2165.
**Mots clés:** plus petit changement de nombre, tri des chiffres, zéros de tête, nombre négatif, algorithme, complexité temporelle, complexité spatiale, prép d'entrevue

---

Aperçu du problème

Vous avez un entier signé `num` (intervalle `-1015 ... 1015`).
**Objectif:** Réorganiser les chiffres de `num` de sorte que l'entier résultant

1. a la valeur la plus faible possible, et
2. ne commence jamais par un zéro de tête.

Le signe du numéro est **fixé** – vous ne pouvez réorganiser que les chiffres absolus.

> **Exemples**
> `310 → 103`
> `-7605 → -7650`

---

Pourquoi ce problème est-il une médaille d'or pour les entrevues

C'est bien, c'est mal.
C'est pas vrai.
**Clarté** – un seul nombre, une seule règle** **Cas d'Edge** – zéros en tête, nombres négatifs, grande magnitude
**Breadth algorithmique** – tri, manipulation de chaînes, conversion d'entiers.
**Language Agnostique** – peut être résolu dans n'importe quelle langue. **Overflow** – éviter `int`, utiliser `long` / `long`" **Test** – plusieurs cas de coin (par exemple, `0`, `-1`, `1000`) Autres

---

Une perspective algorithmique

1. **Séparer le signe**
* Si `num < 0`, rappelez-vous le signe et travaillez avec sa valeur absolue.
* Si `num ≥ 0`, travailler directement.

2. **Convertissez-vous vers un tableau de caractères** – facilite l'échange.

3. **Stratégie de tri* *
* **Positive**: trier les chiffres dans l'ordre croissant* → le plus petit nombre non négatif.
* **Négatif** : trier les chiffres dans l'ordre *descendant* → le nombre *le plus négatif (c.-à-d. le plus petit) après avoir réappliqué le signe.

4. **Éviter les zéros de début (cas positif seulement)* *
* Si le tableau trié commence par `'0'`, trouvez le premier chiffre non zéro et échangez-le avec la première position.

5. **Réassembler* *
* Convertir le tableau de caractères trié en un nombre (`long`/`long`).

6. **Retour** le numéro signé.

---

Analyse de complexité

Complexe métrique
C'est pas vrai.
**Heure**="O(d log d)" – tri des chiffres `d` (`d ≤ 16`). Autres
**L'espace**="O(d)" – tableau de caractères temporaire. Autres

Parce que `d` est au plus 16, l'algorithme est effectivement temps constant pour toutes les fins pratiques.

---

Numéro de code

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.
Tous les trois sont prêts à copier-coller dans votre éditeur et à courir.

---

### Java

"Java
// 2165. Valeur la plus faible du nombre réaménagé
// Heure: O(d log d), Espace: O(d)

solution de classe {
publique longue plus petite Numéro(long num) {
// Poignée zéro immédiatement
Si (nombre) 0) retour 0;

booléen négatif = num < 0;
// Travailler avec une valeur absolue
num = Math.abs(num);

// Convertir en tableau char pour une manipulation facile
char[] chiffres = Long.toString(num).toCharArray();

si (négatif) {
// Ordre décroissant des nombres négatifs
Java.util. C'est ça. Arrays.sort(digits, java.util.Comparator.reverseOrder());
// Reconstruire le numéro avec signe négatif
retour -Long.parseLong(nouvelle chaîne(chiffres));
} autre {
// Ordre croissant des nombres positifs
Java.util. C'est ça. Tableaux.sort(chiffres);
// Éviter de diriger zéro
si (chiffres[0]] '0') {
int nonZeroIdx = -1;
pour (int i = 1; i < chiffres. longueur; i++) {
si (chiffres[i] != '0') {
nonZeroIdx = i;
pause;
}
}
si (non ZeroIdx != -1) {
char temp = chiffres[0];
chiffres[0] = chiffres[nonZeroIdx];
chiffres[nonZeroIdx] = température;
}
}
retour Long.parseLong(nouvelle chaîne(chiffres));
}
}
}
«» "

---

Python

'`python
# 2165. Valeur la plus faible du nombre réaménagé
♪ Temps: O(d log d), Espace: O(d)

Solution de classe:
def le plus petit Nombre(self, num: int) -> Int:
si num] 0:
retour 0

négatif = nombre < 0
chiffres = liste(str(abs(num))

si négatif:
nombres.sort(inverse=True)
retour -int('.join(chiffres))
Sinon:
nombres.sort()
si chiffres[0]] «0»:
# Trouver le premier non-zéro et l'échange
pour i dans la plage (1, len(chiffres)):
si chiffres[i] != «0»:
chiffres[0], chiffres[i] = chiffres[i], chiffres[0]
pause
retourner int('.join(chiffres))
«» "

---

C++

'`cpp
// 2165. Valeur la plus faible du nombre réaménagé
// Heure: O(d log d), Espace: O(d)

solution de classe {
public:
long long long plus petit Nombre(long num) {
Si (nombre) 0) retour 0;

bool négatif = num < 0;
num = llabs(num);

chaîne s = to_string(num);

si (négatif) {
tri(s.begin(), s.end(), plus grand<char>(); // descendant
retour -stoll(s);
} autre {
tri(s.degin(), s.end()); // Accent
si (s[0]] '0') {
// Trouver le premier chiffre non zéro et l'échange
pour (size_t i = 1; i < s.size(); ++i) {
si (s[i] != '0') {
échange(s)[0], s[i];
pause;
}
}
}
retour du ou des stoll(s);
}
}
};
«» "

---

Cas de bord et pièges communs

Qu'est-ce que regarder ?
- Oui.
- Oui. 0 ''' Tri des rendements `"0"` – aucun problème. Autres
Autres Tous les zéros ('1000') Trié ascendant → `"0001"`. D'abord l'échange non-zéro vers l'avant. Autres
Négatif avec zéro (`-1000`) Pas besoin de manipulation spéciale. Autres
Chiffres à un chiffre (`-7`, `9`) Autres
Nombres allant jusqu'à `10^15` correspondent à `long long`/`long`. Autres

---

Pourquoi cette solution remporte des entrevues

1. ** Séparation claire du signe** – maintient la logique simple.
2. **Single Pass Tri** – code minimal, aucune boucle imbriquée.
3. **Handles Leading Zeros Gracefully** – évite un bug commun.
4. **Time & Space Optimal** – convient aux contraintes sans suringénierie.
5. **Language-Neutral** – démontre une compréhension profonde des structures de données, pas seulement de la syntaxe.

---

À emporter : une seule ligne d'essence

> *Trier les chiffres absolus; inverser l'ordre pour les négatifs; échanger le premier chiffre non zéro vers l'avant pour les positifs afin d'éviter les zéros. *

C'est l'idée centrale qui régit les trois réalisations.

---

##= SEO Boost: Mots-clés pour le classement

- Numéro le plus petit réarrangement
- Solution de code 2165
- Triez les chiffres pour le plus petit nombre
- Numéro négatif la plus petite valeur
- Question de l'entretien avec l'algorithme
- Chiffres de tri de complexité

Inclure ceux-ci dans les titres, en-têtes, méta descriptions, et naturellement dans le corps de l'article pour une visibilité maximale.

---

La pensée finale

Lorsque les intervieweurs demandent au sujet de la réorganisation des chiffres, ils sont vraiment probant votre capacité à:

- Boîtes de bord de poignée,
- Choisissez la bonne structure de données (array vs string),
- Oui. Pensez au signe et à la magnitude,
- Gardez le code concis.

La maîtrise de ce problème simple mais subtil renforcera la confiance pour des énigmes à cordes plus complexes. Bon codage !