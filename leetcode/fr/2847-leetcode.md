---
titre: LeetCode 2847. Plus petit nombre avec le produit à chiffres donnés - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de la solution

Ci-dessous vous trouverez **trois implémentations complètes et exécutables** pour le problème LeetCode **2847 – Plus petit nombre avec un produit à chiffres donnés**.
Les trois solutions utilisent la même logique gourmande :

1. Facteurz l'entrée `n` uniquement avec les premiers `2, 3, 5, 7`.
2. Si un facteur demeure, la réponse est `-1`.
3. Combiner les facteurs principaux en les plus petits chiffres possibles (9 → 32, 8 → 23, 6 → 2·3, 4 → 22).
4. Construisez la réponse dans l'ordre ascendant des chiffres.

Texte
Complexités
- Oui.
Temps : O(log n) (le pire cas que nous divisons par 2, 3, 5 ou 7 quelques dizaines de fois)
Espace : O(1) (supérieur à la chaîne de sortie)
«» "

> **Astuce** – Lors de l'écriture du code d'entrevue, gardez toujours la logique dans une fonction d'aide séparée ; ceci garde le code lisible et facile à tester.

---

## 1.1 Java (Signature du code leet)

"Java
solution de classe {
public Chaîne la plus petiteNombre(long n) {
// cas particuliers
si (n) 1) retourner "1";
si (n < 10) retourner String.valueOf(n);

Int[] prime = {2, 3, 5, 7};
int[] cnt = nouvelle int[10]; // cnt[d] = combien de fois le chiffre d apparaîtra

// facteur n par prime 2,3,5,7
pour (int p : prime) {
pendant que (n % p == 0) {
n /= p;
cnt[p]++;
}
}

Si (n != 1) retourner "-1" // facteur restant > 7 → impossible

// Fusionner en chiffres plus grands
cnt[9] = cnt[3] / 2; // 3*3 = 9
cnt[3] %= 2;

cnt[8] = cnt[2] / 3; // 2*2*2 = 8
cnt[2] %= 3;

si (cnt[3] > 0 && cnt[2] > 0) { // 3*2 = 6
cnt[3] = 0;
cnt[2] = 1; // laisser un '2 '
cnt[6] = 1;
}

cnt[4] = cnt[2] / 2; // 2*2 = 4
cnt[2] %= 2;

// construire la réponse dans l'ordre ascendant des chiffres
StringBuilder sb = nouveau StringBuilder();
pour (int d = 1; d <= 9; d++) {
pour (int i = 0; i < cnt[d]; i++) sb.append(char)('0' + d));
}
retour sb.toString();
}
}
«» "

---

## 1.2 Python 3

'`python
Solution de classe:
def le plus petit Nombre(self, n: int) -> str:
si n] 1: # Cas particulier
retour "1"
si n < 10: # un seul chiffre est déjà la réponse
retour str(n)

prime = [2, 3, 5, 7]
cnt = [0] * 10 # cnt[d] = combien de fois le chiffre d apparaîtra

Facteur n
pour p en prime:
alors que n % p == 0 & #160;:
n //= p
cnt[p] += 1

si n != 1: # facteur restant > 7 → impossible
retour "-1"

# fusionner en chiffres plus grands
cnt[9] = cnt[3] // 2 # 3*3
cnt[3] %= 2

cnt[8] = cnt[2] // 3 # 2*2*2
cnt[2] %= 3

si cnt[3] > 0 et cnt[2] > 0: # 3*2
cnt[6] = 1
cnt[3] = 0
cnt[2] = 1

cnt[4] = cnt[2] // 2 # 2*2
cnt[2] %= 2

# construire la réponse en ordre ascendant
res = []
pour d dans la plage (1, 10):
res.append(str(d) * cnt[d])
retourner "".join(res)
«» "

---

## 1,3 C++ (GNU C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne la plus petite Nombre(long n) {
si (n) 1) retourner "1";
si (n < 10) retourner à_string(n);

vecteur<int> prime = {2, 3, 5, 7};
vector<int> cnt(10, 0); // cnt[d] = fois le chiffre d apparaîtra

pour (int p : prime) {
pendant que (n % p == 0) {
n /= p;
++cnt[p];
}
}
Si (n != 1) retourner "-1";

cnt[9] = cnt[3] / 2; // 3*3
cnt[3] %= 2;

cnt[8] = cnt[2] / 3; // 2*2*2
cnt[2] %= 3;

Si (cnt[3] && cnt[2]) { // 3*2
cnt[6] = 1;
cnt[3] = 0;
cnt[2] = 1;
}

cnt[4] = cnt[2] / 2; // 2*2
cnt[2] %= 2;

la chaîne rés;
pour (int d = 1; d <= 9; ++d) {
l'annexe(cnt[d], char('0' + d));
}
retour rés;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et le mal de résoudre le LeetCode 2847

> **Mots clés**: *Code Leet 2847*, *Numéro le plus petit avec le produit à chiffres donnés*, *solution de Java*, *solution de Python*, *solution de C++*, *codage d'entrevue*, *algorithme*, * factorisation en douceur*, *conseils d'entrevue de codage*, *embauche technologique*

---

Présentation

Chaque ingénieur logiciel a un problème de LeetCode qui ressemble à un *mini-code-wars* : vous êtes en train de fixer un nombre, vous devez le séparer, et vous devez le faire dans la chaîne la plus courte possible**. C'est **2847 – Le plus petit nombre avec le produit à chiffres donnés**.

Il s'agit d'un problème moyen sur LeetCode, mais dans une interview il peut **faire ou casser** la confiance du candidat. Laissez-nous disséquer pourquoi ce problème est une grande vitrine, ce que les recruteurs cherchent d'écueils, et comment vous pouvez ** le transformer en une vedette d'interview prête pour le portefeuille**.

---

Pourquoi Ce problème est une médaille d'or pour les candidats

1. **Déclaration de problème claire** – Vous êtes donné un seul entier `n`. Si vous pouvez exprimer le produit de ses chiffres comme `n`, affichez le nombre *le plus petit* qui le fait.
2. **Petit domaine d'entrée** – Tous les facteurs principaux supérieurs à 7 ruinent la solution. Cette contrainte vous donne un ensemble **finite de "utile" premiers** (`2, 3, 5, 7') à s'inquiéter.
3. **Greedy + factorisation** – La solution optimale est presque insignifiante lorsque vous voyez le motif: 9 = 32, 8 = 23, 6 = 2·3, 4 = 22. Si vous fusionnez les principaux facteurs dans le bon ordre, vous obtenez la plus petite chaîne instantanément.
4. ** Logique linguistique-agnostique** – Que vous codez en Java, Python ou C++, l'idée centrale reste identique. C'est super pour les candidats qui *aiment* une langue mais doivent répondre dans une autre pendant une entrevue.

> **Conseil pro**: Dans une entrevue, ** expliquer votre plan avant d'écrire le code**. Les recruteurs adorent vous voir réfléchir avant de taper.

---

- Oui. Les mauvaises – pièges communs

Pourquoi c'est un problème Comment l'éviter
-- -- -- -- -- -- -- -- -- -- --
**Leaving `n` < 10** – retour `String.valueOf(n)` en Java ou `str(n)` en Python. Il semble trivial, mais vous devez également gérer `n = 1` qui est *not* couvert par la règle -"simple" chiffre. Traiter "n". 1' comme cas séparé *avant* la logique générale. Autres
Autres ** Complètement gourmand de 9 à 2** sans vérifier les facteurs impossibles. Vous pouvez diviser par 9, 8, ..., mais si un facteur restant > 7 reste, vous obtiendrez silencieusement un mauvais nombre. Autres Après factorisation, **check `n != 1'**; si vrai, sortie `-1'. Autres
**Ne fusionnez pas les facteurs principaux**** Si vous affichez simplement les premiers 2,3,5,7 dans l'ordre décroissant, la chaîne peut être plus longue que nécessaire (p. ex. 222 → 222,2 vs 8,8). Fusionner `23` → 8, `32` → 9, `2·3` → 6, `22` → 4. C'est l'étape *greedy fusion*. Autres
**Construire le résultat dans un mauvais ordre** Ajouter des chiffres dans l'ordre **ascendant** après fusion. Dans C++/Java `append(cnt[d], chiffre)` ou dans Python `"digital"*cnt[d]`. Autres

---

- Oui. Les maux de tête de l'Edge-Case

1. ** Nombres énormes** (`n` jusqu`à `1018`) – Vous pourriez penser que la récursion ou les boucles pourraient déborder. Utiliser **`long`/`long`** et diviser étape par étape.
2. ** factorisation de prime** – Bien que Python="s `//=` soit bon marché, Java="s modulo sur `long` peut sembler intimidant. N'oubliez pas : vous divisez seulement par 2, 3, 5 ou 7 – ce qui est au plus ~60 itérations.
3. **La fuite de mémoire en Java** – Un `StringBuilder` est essentiel. Évitez de concaténer les cordes dans une boucle; il s'agit de O(n2).
4. **C++ `string::append` nuances** – `res.append(cnt[d], char('0'+d));` peut prêter à confusion pour les nouveaux venus. Le premier argument est le compte **repas**.

---

- Oui. Comment briller dans une entrevue

1. ** Indiquez votre approche* *
Le facteur de nombre en utilisant les premiers 2, 3, 5, 7. S'il reste quelque chose, c'est impossible. Ensuite, je fusionnerai avidement des paires de 3s en 9s, des triples de 2s en 8s, et ainsi de suite. (en milliers de dollars)

2. **Expliquer la fusion gourmande**
Parce que 9 est le plus grand chiffre, et 9=32, en utilisant 9 réduit le nombre de chiffres. De même 8=23 et 6=2·3, 4=22. Cela garantit le plus petit résultat lexicographiquement. (en milliers de dollars)

3. **Montrer le code étape par étape**
*Ne laissez pas tomber l'extrait final. Passez par la boucle de factorisation, la section fusion et la construction de la chaîne. Les recruteurs adorent l'explication.

4. **Cas d ' angle à main**
* `n == 1` → .
* `n < 10` → `str(n)` ou `to_string(n)`.
* Facteur restant > 7 → `-1`.

5. **Test complet**
Exécutez les cas suivants :
Texte
1 → "1"
10 → "-1" (10 = 2·5 → OK, mais 10<10 est un seul chiffre)
20 → "45" (20 = 22·5 → 4·5)
256 → "288" (256 = 28 → 8·8)
1000000000000000000 → "-1"
«» "
Dans les entrevues, les candidats passent souvent le test de grand nombre; assurez-vous de ne pas.

---

## Conclusion – Transformer 2847 en victoire d'embauche

*LeetCode 2847* est une étude de microcas** sur la factorisation, la manipulation et la manipulation des cordes. Il est assez petit pour être résolu en moins de 5 minutes, mais il teste votre:

* ** intuition mathématique** – Reconnaître que 9 = 32, 8 = 23, etc.
* ** Clarté algorithmique** – écriture propre, code agnostique de langue.
* **Connaissance de cas** – Manipulation de `1`, de chiffres simples et d'entrées impossibles.

Quand vous entrez dans un entretien technique, *mention la stratégie gourmande* d'abord. Montrez que vous pouvez expliquer pourquoi la fusion des facteurs principaux donne la plus petite chaîne lexicographique. Puis écrivez votre code dans le style convivial d'entrevue ci-dessus.

> **Rappelez-vous**: Le *bon* est l'élégante logique gourmande; le *mauvais* est la tentation de sur-penser ou d'oublier le cas `-1`; le *ugly* est les petits bogues d'implémentation qui apparaissent seulement dans les cas de bord. Maîtrisez-les, et vous passerez rapidement de "medium" à "must-hire".

Bon codage, et bonne chance pour votre prochain entretien technique! C'est ce qu'il a dit.

---

> **Vous souhaitez d'autres solutions prêtes à l'entrevue? * *
Autres [My GitHub LeetCode Repository](https://github.com/votre-github) – Java, Python, C++ – prêt pour copier-coller.
> Inscrivez-vous à mon bulletin d'information pour connaître les pannes d'algorithmes hebdomadaires et les conseils de préparation d'entrevues!