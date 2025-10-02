---
titre: LeetCode 1945. Somme des chiffres des chaînes après conversion -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – 3 langues

Ci-dessous vous trouverez **compact, prêt à la production** pour LeetCode 1945 en **Java, Python et C++**.
Les trois implémentations suivent la même idée :

1. Convertir chaque lettre en son index alphabétique (`a=1 ... z=26`).
2. Concaténez ces indices en une grande chaîne décimale.
3. Remplacer la chaîne par la somme de ses chiffres, **k** fois.

> **Note** – Le premier chiffre-somme est *après* la conversion.
> Donc on fait la boucle **k** fois.

---

#### 1.1 Java

"Java
// Java 17
solution de classe {
Int public getLucky(String s, int k) {
// Construisez la grande chaîne décimale
StringBuilder sb = nouveau StringBuilder();
pour [charc : s.toCharArray()) {
sb.append(c - 'a' + 1); // 1-based alphabet position
}

Chaîne cur = sb.toString();

// Répétez le chiffre k fois
pour (int i = 0; i < k; i++) {
= 0;
pour (char d : cur.toCharArray()) {
somme += d - '0';
}
cur = entier.toString(sum);
}
retour Integer.parseInt(cur); // réponse finale
}
}
«» "

---

#### 1.2 Python

'`python
# Python 3
Solution de classe:
def getLucky(self, s: str, k: int) -> Int:
# Convertissez chaque char en sa valeur numérique et concaténez
num = ''.join(str(ord(c) - 96) pour c in s)

# k tours de chiffres
pour _ dans la plage(k):
num = str(sum(int(d) pour d en num))
retour int(num)
«» "

---

*## 1.3 C++

'`cpp
// C++17
solution de classe {
public:
Int getLucky(chaîne s, int k) {
le nombre de cordes;
pour (charc : s)
num += to_string(c - 'a' + 1); //

pour (int i = 0; i < k; ++i) {
= 0;
pour (char d : num)
somme += d - '0';
num = to_string(sum);
}
retour stoi(num);
}
};
«» "

---

> **Pourquoi ça marche* *
> La chaîne construite à l'étape 1 contient la représentation décimale de la
> indices concaténés.
> Le résumé de ses chiffres est exactement l'opération décrite dans l'énoncé,
> et le répéter *k* fois donne le nombre de chance requis.

---

- Oui. 2. Article du blog
**Titre:** *LeetCode 1945 – Somme des chiffres de cordes après conversion – Un emploi‐Interview Guide prêt (Java / Python / C++)*

> **Meta‐Description**: Master LeetCode 1945 avec des solutions propres et efficaces en Java, Python et C++. Apprenez l'algorithme, les cas de bord et les conseils d'entrevue pour impressionner les gestionnaires d'embauche.

---

2.1 Aperçu du problème

Code Leet 1945 vous demande :

1. Convertissez une chaîne inférieure `s` en un grand entier en remplaçant chaque lettre par sa position dans l'alphabet (`a=1, ..., z=26`).
2. Remplacer cet entier par la somme de ses chiffres.
3. Répétez l'étape de la somme numérique **k** fois.
4. Retourne l'entier résultant.

*Exemples*
- "s="iiii", k=1` → 36
- `s="leetcode", k=2` → 6
- `s="zbax", k=2` → 8

Les contraintes (‘''' ≤ 100, k ≤ 10') permettent une simulation simple, mais une observation intelligente peut réduire le code à quelques lignes.

---

2.2 Principales observations (Le bien)

- **La cartographie de l'alphabète est banale:** "c - "a" + 1" donne un indice basé sur 1 en O(1).
- **Le nombre concaténé peut être énorme (jusqu'à 200 chiffres),** mais nous n'avons jamais besoin* de le stocker comme un type entier – tout comme une chaîne.
- **La somme des chiffres de la chaîne concaténée équivaut à la somme des chiffres de chaque caractère de la représentation numérique** (les nombres à 1 chiffre conservent leur valeur, les nombres à 2 chiffres s'élèvent à "tens + unités").
Cela vous permet d'éviter de construire une longue chaîne si vous voulez une solution micro-optimisée.
- **`k` est minuscule (=10),** donc les chiffres répétés sont bon marché.

---

2.3 Algorithme (Le "Bad")

1. **Construisez la corde concaténée. **
`num = ''.join(str(ord(c) - 96) pour c in s)` (Python)
ou `num += to_string(c - 'a' + 1)' (C++/Java).

2. **Loop `k` fois.**
Dans chaque itération:
- Calculer "somme = somme(int(d) pour d en nombre)".
Remplacer `num` par `str(sum)`.

3. **Retourner le total final. **
`return int(num)` / `return Integer.parseInt(num)` / `return stoi(num)`.

> **Pourquoi il pourrait sembler faux** – Si vous pensez que « convertir → transformer » compte comme l'une des transformations *k*, vous allez exécuter la boucle une fois trop et obtenir de mauvaises réponses sur des tests cachés.

---

2.4 Cas de bord & Erreurs

Ce qui se passe
- C'est quoi ?
Autres **Lettre à deux chiffres (`j–z`).**="to_string(10)` → `"10"`. La somme des chiffres = `1+0`. Autres
**k = 1.**= Vous devez *seulement* effectuer le premier chiffre-somme après la conversion. Autres Assurez-vous que la boucle fonctionne exactement `k` fois, pas `k‐1`. Autres
Autres **Très long `s` (100 chars).**= La chaîne concaténée peut être longue de 200 chiffres – encore fine dans une chaîne, mais attention au débordement entier si vous utilisez `long`.== Gardez tout comme `string` ou utilisez `int` pour les sommes intermédiaires. Autres
**Laisser des zéros?** La concaténation ne produit jamais de zéros de tête parce que les indices alphabétiques sont basés sur 1. Pas besoin de manipulation spéciale. Autres

---

2.4 Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Convertir la chaîne → chaîne concaténée **O(=======)**** (longueur ≤ 200)
Nombre de chiffres répétés (`k` ≤ 10)

Dans la pratique, tant **temps que mémoire** sont négligeables pour les limites données.

---

2.5 Faits saillants de la mise en oeuvre – 3 langues

- **Java:** Utilise `StringBuilder` pour la concaténation, une simple boucle `pour chaque` pour le chiffre-sum, et `Integer.parseInt()` pour le résultat final.
- **Python:** Liste-compréhensions et expressions génératrices maintiennent le code court et lisible.
- **C++:** `to_string` et `stoi` rendent le code aussi concis que les versions Java/Python.

Toutes les solutions sont ** entièrement commentées** et **idiomatic** pour leurs langues respectives, ce qui est un plus énorme dans une interview d'embauche.

---

2.6 Pièges communs (Le "Ugly" revisité)

Erreurs Symptômes Correction
- C'est quoi ?
Autres **Considérer la conversion comme une transformation. Rappelez-vous que la boucle commence *après* la conversion. Autres
**Utiliser `long` pour stocker le nombre concaténé. Autres
**Off‐by‐one dans la cartographie alphabetique (« c - « a »)**. Toujours ajouter `+1` pour obtenir 1-based index. Autres
**Ignorer le boîtier à 2 chiffres ('10–26'). Somme des dizaines et des unités ( 'val / 10 + valeur % 10'). Autres

---

2.7 Conseils d'entrevue – Comment tourner Cela dans un travail

1. ** Expliquez l'idée d'abord. **
Il construit la représentation décimale, puis additionne les chiffres k fois. (en milliers de dollars)
Cela vous montre que vous n'êtes pas juste en écriture aveugle.

2. **Montrer l'astuce optimisée. **
*=Au lieu de construire un numéro à 200 chiffres, je peux présumer les contributions numériques de chaque lettre.
Même si vous ne l'implémentez pas, l'intervieweur remarquera votre sensibilisation.

3. **Écrire le code propre, commenté. **
Utilisez des noms de variables significatifs (`cur`, `sumDigits`, `sb`) et gardez la logique dans une seule boucle autonome.

4. **Discuss cas bord. **
Mention `k=1`, indices à deux chiffres, et pourquoi l'approche de chaîne est sûre.

5. **Talk performance.**
La complexité du temps est O(=S) + k·len(num), l'espace est O(=S). (en milliers de dollars)
Même si les contraintes sont petites, montrer que vous pouvez analyser la complexité impressionnera les ingénieurs seniors.

6. ** Facultatif: Essais unitaires.**
Ajouter quelques affirmations pour les exemples et les cas aléatoires. (en milliers de dollars)
Un gestionnaire d'embauche aime les candidats qui pensent aux tests.

---

### 2.8 Liste de contrôle du référencement (Le bon)

Élément du référencement Comment il est couvert
C'est ce qu'on dit.
**Titre**Contient le code Leet 1945, le nom des chiffres, le code Java / Python / C++
**Moyen-Description**
**En-têtes (h1‐h4)**= Structurel, riche en mots clés (`Aperçu du problème`, `Algorithme`, etc.) Autres
**Blocks de code**= Classé avec des balises de langage (`java`, `python`, `cpp`) Autres
** Listes de bulles**
**Lien interne**.Pas nécessaire ici, mais un vrai blog serait lié à des articles liés LeetCode.
**Alt‐texte (si images)** Autres
**L'URL canonique**

---

2.9 Conclusion

LeetCode 1945 est trompeurment simple, mais il enseigne quelques leçons précieuses:

- **Caractères de carte rapidement** (`c - 'a' + 1`).
- **Conservez les nombres lourds comme des chaînes** pour éviter les débordements.
- **Couvercle des opérations correctement** – la conversion n'est *pas* une transformation.
- **N'itérer que le nombre de fois requis** (k ≤ 10).

Avec les extraits Java, Python et C++ ci-dessus, vous pouvez écrire la solution à la main dans n'importe quelle interview, expliquer chaque étape avec confiance, et montrer que vous êtes un ingénieur logiciel bien arrondi prêt pour votre prochain rôle.

Bonne chance, et le codage heureux!