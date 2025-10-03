---
titre: LeetCode 2190. Numéro le plus fréquent suivant la clé Dans un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. LeetCode 2190 – **Numéro le plus fréquent suivant la clé dans un tableau* *

Code de la langue
C'est quoi, ça ?
*Java**
solution de classe publique {
public int mostFrequent(int[] nums, int key) {
// HashMap pour garder les nombres de chaque valeur qui suit `key "
Carte<integer, integer> freq = nouveau HashMap<>();

// Traverser le tableau et compter seulement les nombres qui apparaissent après `key`
pour (int i = 0; i < nombres.longueur - 1; i++) {
si (nums[i] == clé) {
freq.merge(nums[i + 1], 1, entier::sum);
}
}

// Trouvez le nombre avec le nombre maximum
int best = -1;
int mieux Cnt = -1;
pour (Map.Entry<Integer, Integer> e : freq.entrySet() {
si (e.getValue() > bestCnt) {
bestCnt = e.getValue();
best = e.getKey();
}
}
retour meilleur; // garanti pour être unique
}
}
«» Autres
*Python**
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def mostFrequent(self, nums: List[int], clé: int) -> Int:
freq = compteur()
pour i dans la plage (len(nums) - 1):
si des nombres [i] == clé:
[nombres[i + 1]] += 1
# `most_common(1)` retourne une liste de l'élément le plus commun
retourner freq.most_common(1)[0][0]
«» Autres
*C++ *Cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int mostFrequent(vecteur<int>& nums, clé int) {
unordered_map<int, int> freq;
pour (size_t i = 0; i + 1 < nums.size(); ++i) {
si (nums[i] == clé) {
++freq[nums[i + 1]];
}
}
int best = -1, best Cnt = -1;
pour (const auto& kv : freq) {
si (kv.seconde > bestCnt) {
le meilleur Cnt = kv.seconde;
best = kv.first;
}
}
le meilleur retour; // garanti unique
}
};
«» Autres

> **Pourquoi une carte de hachage? **
> Le problème demande un nombre de fréquences de *valeurs qui suivent immédiatement* une clé particulière.
> Une carte de hachage (« O(1) » moyenne insert/lookup) nous donne le moyen le plus direct de maintenir un nombre de candidats.
> Avec seulement 1 000 éléments (par contraintes) et des valeurs limitées à 1 000, la carte reste minuscule, donc l'approche est à la fois temporelle et spatiale.

---

- Oui. 2. Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 2190

Titre
**Maîtrise du LeetCode 2190 : Le Bon, Le Mauvais et Le Méchant – Un Guide d'entrevue complet* *

Introduction

Si vous vous préparez à une entrevue d'ingénierie logicielle, vous rencontrerez souvent des problèmes de fréquence qui sonnent simples à première vue, mais qui peuvent vous faire trébucher si vous oubliez les cas de bord.
LeetCodeS *2190 – Numéro le plus fréquent La clé suivante dans un tableau* est un parfait exemple. Dans cet article, nous lisons:

- Passez par l'énoncé du problème et les contraintes.
- Présentez une solution propre et prête à la production dans **Java**, **Python** et **C++**.
- Mettre en évidence le *bon* (clair, efficace, facile à comprendre), le *mauvais* (pièges possibles) et le *ugly* (erreurs courantes, cas d'essai confus).
- Laissez-vous aller à l'action pour répondre à cette question et à des problèmes d'entrevue semblables.

---

Récapitulation du problème

> **Grâce** à un tableau entier indexé de 0 "nums" et à une "clé" entière garantie d'exister en "nums".
> **Tâche**: Pour chaque "cible" entière unique qui apparaît immédiatement après* une occurrence de "clé", compter combien de fois cela arrive. Retourner la « cible » avec le nombre maximal. La réponse sera toujours unique.

> **Constraints**

Paramètre Gamme
C'est quoi ?
2 – 1 000
1 – 1 000
"key" en "nums" Autres

> **Exemple**
> `nums = [1 100 200 1 100]`, `key = 1` → **Output**: `100` (il suit `1` deux fois).

---

Pourquoi cette approche est élégante

1. **Temps linéaire** – Un seul passage sur le tableau («O(n)») est tout ce dont nous avons besoin.
2. **L'espace supplémentaire continu** – La carte de hachage ne croît que jusqu'au nombre de valeurs distinctes qui suivent `key` (1 000).
3. **Clarité** – L'algorithme se lit comme un simple anglais: -Couvercle chaque suiveur; choisissez le plus fréquent. (en milliers de dollars)
4. **Agilité linguistique** – La même logique se traduit par Java, Python, C++ avec une plaque de chaudière minimale.

---

- Oui. Les mauvaises: les pièges communs à éviter

Piège Explication
- C'est quoi ?
**Passer le dernier élément**= Depuis que nous regardons `i + 1`, l'index final n'est jamais coché. "Itérer seulement à "nums.longueur - 1". Autres
**En supposant que la clé n'apparaît qu'une seule fois**=Si `key` se produit plusieurs fois, tous les abonnés doivent être comptés. Continuez à compter dans la boucle sans réinitialiser. Autres
**L'utilisation d'un tableau pour les comptages (taille 1000)** Utilisez une carte dynamique (`HashMap`, `unordered_map`, `Counter`). Autres
**Confuser la réponse avec la clé elle-même**= Si `key` apparaît deux fois dans une rangée, la clé elle-même peut être un suiveur valide. Traitez `key` comme tout autre suiveur; rien de spécial. Autres
**Retourner 0 ou -1 quand la carte est vide**Le problème garantit `key` existe, mais si `key` est à la fin, la carte serait vide. Gérez explicitement ce cas d'angle (bien qu'avec les contraintes cette situation ne se produise jamais). Autres

---

- Oui. L'Ugly: Trick Test Cases & Edge‐ Affaires

1. **Tous les éléments sont la clé* *
Texte
nombres = [5,5,5,5,5], clé = 5
«» "
*Réponse*: `5` (la clé se suit 4 fois).
*Pourquoi ça compte*: Certaines solutions naïves oublient que le suiveur peut égaler la clé.

2. **Clé à la fin**
Texte
nombres = [1,2,3,4], clé = 4
«» "
*Réponse*: Aucun suiveur n'existe – mais le problème garantit que la réponse est unique, donc cette entrée n'apparaît pas.
*À emporter*: Protégez toujours les «i+1» hors des frontières.

3. **Compte de grande fréquence**
Texte
nombres = [1,2,1,2,1,2,1,2], clé = 1
«» "
*Réponse*: "2" (compte = 4).
*Pourquoi ça compte*: Confirme que nous comptabilisons les événements, pas seulement des valeurs distinctes.

4. ** Candidats multiples ayant la même fréquence (contrairement à la garantie)* *
Bien que LeetCode assure l'unicité, le code d'écriture qui gère les liens gracieusement (par exemple en choisissant le plus petit ou le premier vu) montre la robustesse.

---

### Étape par étape (Java)

1. **Créer un `HashMap<entier,entier>`** – clé = suiveur, valeur = compte.
2. **Loop unique** – Pour `i = 0` à `len-2`:
- Si `nums[i] == clé`, incrément `freq[nums[i+1]]`.
3. **Trouver le maximum** – Iterate sur les entrées de la carte; suivre le plus grand nombre et le suiveur correspondant.
4. **Retour** – Ce suiveur est garanti unique.

**Code**
* (voir section 1 – Java)*

---

### Marche pas à pas (Python)

Collections de Python. Le compteur est trivial :

'`python
Importations provenant des collections Compteur

pour i, val dans l'énumération(nombres[:-1]): # éviter le dernier élément
if val == clé:
contre[nums[i+1]] += 1

compteur de retour.most_common(1)[0][0]
«» "

`most_common(1)` garantit l'élément supérieur; pas besoin de comparaison manuelle.

---

### Étape par étape (C++)

Utiliser `unordered_map<int,int>`:

'`cpp
unordered_map<int,int> freq;
pour (size_t i = 0; i + 1 < nums.size(); ++i) {
si (nums[i] == clé) freq[nums[ i+1]]++;
}
int best = -1, best Cnt = -1;
pour (auto &p : freq) {
si (p.second > bestCnt) { best Cnt = p.seconde; meilleur = p.première; }
}
le meilleur retour;
«» "

---

Analyse de complexité

Métrique Java/Python/C++
C'est-à-dire
**Heure**="O(n)" – un passage + "O(k)" pour trouver max (`k` = suiveurs distincts ≤ 1 000). Autres
**L'espace**="O(k)" – carte d'abonnés distincts. Autres

---

### Prise- Conseils pour les entrevues

1. ** Clarifier la question** – Demandez si les abonnés peuvent égaler la clé, confirmer les contraintes.
2. **Expliquez votre algorithme** – Mentionnez le temps linéaire, l'utilisation de la carte de hachage, pourquoi vous n'avez pas besoin de boucles imbriquées.
3. **Connaissance d'Edge** – Discutez des scénarios de la clé à la fin et de toutes les clés.
4. **Montrer la robustesse** – Même si la réponse est unique, montrez comment votre code se comporterait si des liens apparaissaient.
5. **Points forts spécifiques à la langue** – Dans Python, mettre en évidence `Counter`; dans C++, mettre l'accent `unordered_map`; dans Java, note `merge` ou `computer`.

---

La pensée finale

LeetCode 2190 est un micro-test de vos connaissances en structure de données et de votre capacité à raisonner sur la fréquence dans un domaine limité.
En maîtrisant ses aspects « bons, mauvais, laids », vous allez non seulement résoudre ce problème exact avec confiance, mais aussi construire un cadre qui s'applique à d'innombrables autres questions d'entrevue.

Bon codage – et que vos entretiens soient remplis de solutions *clear* et d'exécution *smooth*! C'est ce qu'il a dit.

---

### Mots-clés et référence

- **Entretien en génie logiciel**
- **LeetCode 2190**
- **algorithme de comptage des fréquences**
- **Codage de l'entrevue de Java**
- **Python solutions d'entretien**
- **C++ code d'entrevue**
- question d'entrevue sur la carte de l'hash**
- **algorithme du temps linéaire**
- **affaires de bord d'entrevue**

---

- Oui. À propos de l'auteur

> *Jane Doe* est une ingénieure principale du logiciel qui a aidé des équipes de fintech, de technologie de la santé et d'IA à naviguer dans les entrevues de codage. Elle écrit du contenu technique destiné aux développeurs de tous niveaux.

---

Références

- Problème de LeetCode 2190 : https://leetcode.com/problèmes/principaux nombres-suivant-key-in-an-array
- Les collections de Python. Counter`: https://docs.python.org/3/library/collections.html#collections.Counter
- Java `HashMap.merge`: Il s'agit d'un élément essentiel de la stratégie de Lisbonne.

---

> **Suivant de la série**: *LeetCode 2201 – Nombre minimum de Bit Flips consécutif K – autre torsion de fréquence-compte. Restez au courant !

---

> *© 2024 Jane Doe. Tous droits réservés. *

---

**Bonne entrevue!**

---

### Auteur Bio & Appel à l'action

> Vous voulez plus d'articles prêts à l'entrevue? Abonnez-vous à notre bulletin pour connaître les défis de codage hebdomadaires, les conseils d'entrevue simulés et les guides d'avancement de carrière.

---

- Oui. 3. Conclusion

La solution de hash-map dans les trois langues principales est la meilleure façon de s'attaquer au LeetCode 2190.
Comprendre le bien, éviter le mauvais, et se préparer pour les cas de test laid transforme une question apparemment simple en une vitrine de la résolution de problèmes – exactement ce que les intervieweurs veulent voir.

Bonne chance pour votre prochain entretien !