---
titre: LeetCode 1897. Redistribuer les caractères pour rendre toutes les cordes égales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 1897
** Exposé des problèmes* *
Vous êtes donné un tableau de chaînes `words`. Dans une opération, vous pouvez choisir deux indices différents `i` et `j` (avec `words[i]` non-vide) et déplacer **any** caractère unique de `words[i]` à **any** position in `words[j]`.
Return **true** s'il est possible de rendre chaque chaîne identique en `words` après un certain nombre de telles opérations, sinon retourner **false**.

---

- Oui. 2. Intuition

Si nous pouvons réorganiser arbitrairement les caractères entre les chaînes, la chose *seulement* qui compte est :

1. ** Longueur totale** – Chaque chaîne finale doit avoir la même longueur, sinon elle est impossible.
2. ** Fréquences des caractères** – Pour chaque lettre `a...z`, le nombre total de cette lettre doit être divisible par `mots.longueur`. Sinon, les caractères restants ne peuvent jamais être partagés uniformément entre toutes les chaînes.

L'opération est essentiellement un *redistribution* de caractères; l'ordre relatif des caractères à l'intérieur d'une chaîne n'affecte pas la faisabilité.

---

- Oui. 3. Algorithme (Hash-Table / Compteur de répartition)

1. Si "mots.longueur". 1' → trivialement vrai.
2. Calculer le total Len = Mots-clés[i]
- Si 'totalLen % words.longueur != 0`, retourner `faux`.
3. Compter les fréquences de chaque lettre dans un tableau de 26 éléments «cnt[26]».
4. Pour chaque "cnt[c] "
- Si "cnt[c] % words.longueur != 0`, retourner `faux`.
5. Tous les chèques passés → retourner `true`.

Pourquoi ça marche ?

**Nécessité** –
*Length*: Après tous les mouvements, chaque chaîne aura la longueur `totalLen / words.length`.
*Lettre compte*: Chaque chaîne contiendra exactement `cnt[c] / words.length` de la lettre `c`. Si un `cnt[c]` n'est pas divisible, la division entière laisserait un reste qui ne peut pas être distribué.

- **Suffisance** –
Nous pouvons toujours déplacer les caractères excédentaires des chaînes plus longues vers des chaînes plus courtes. Parce que nous pouvons insérer un personnage n'importe où, nous pouvons réorganiser les caractères arbitrairement. Par conséquent, si les deux conditions ci-dessus tiennent, il existe une séquence constructive de mouvements (la preuve est une simple redistribution gourmande).

---

- Oui. 4. Complexités

Mesure Complexité
C'est pas vrai.
**Heure**="O(N * M)" où `N = words.length`, `M` = longueur moyenne de la chaîne (au plus 100)="
**Espace** – seulement un tableau fixe de 26 éléments indépendamment de la taille d'entrée

---

- Oui. 5. Mise en œuvre du code

#### 5.1 Java

"Java
solution de classe {
public booléen makeEqual(String[] mots) {
// 1. Une seule chaîne → déjà égale
si (mots.longueur) 1) retour vrai;

// 2. La longueur totale doit être divisible par le nombre de chaînes
= 0;
pour (String w : mots) totalLen += w.longueur();
si (totalLen % mots. longueur != 0) retourner faux;

// 3. Fréquences de comptage
int[] freq = nouveau int[26];
pour (Pièce w : mots) {
pour (char ch : w.toCharArray()) freq[ch - 'a']++;
}

// 4. Chaque fréquence doit être divisible par des mots. longueur
pour (int f : freq) {
si (f % mots. longueur != 0) retourner faux;
}
retour vrai;
}
}
«» "

5.2 Python

'`python
Solution de classe:
def makeEqual(self, mots: List[str]) -> bool:
n = len(mots)
si n] 1 :
retour Vrai

total_len = somme(len(w) pour w en mots)
si total_len % n:
Retour Faux

# Compteur pour 26 lettres minuscules
freq = [0] * 26
pour w en mots:
pour ch in w:
freq[ord(ch) - 97] += 1

retourner tous(f % n == 0 pour f in freq)
«» "

C++

'`cpp
solution de classe {
public:
bool makeEqual(vector<string>& words) {
int n = mots.size();
si (n) 1) retour vrai;

= 0;
pour (const auto& w : mots) totalLen += w.size();
si (totalLen % n) retourner faux;

tableau <int, 26> freq{};
pour (const auto& w : mots)
pour (char ch : w) freq[ch - 'a']++;

pour (int f : freq)
si (f % n) retourner faux;
retour vrai;
}
};
«» "

Les trois solutions sont **O(1) espace supplémentaire** et **O(N·M)** temps, satisfaisant les contraintes du problème.

---

- Oui. 6. Article du blog – Redistribuer les caractères pour rendre toutes les cordes égales : le bon, le mauvais et le mauvais

> **SEO Mots-clés**: LeetCode 1897, Redistributer Caracters to Make All Strings Equal, problème d'entrevue, solution Java, solution Python, solution C++, table de hachage, comptage de caractères, interview algorithmique, prép d'entrevue de codage

---

Introduction

Lorsqu'on se prépare à une entrevue de codage, on apprend rapidement que **le style de résolution des problèmes** est souvent plus important que les spécificités linguistiques. LeetCode="s "Redistribuer les caractères pour rendre toutes les chaînes égales" (Problem 1897) est un exemple de manuel : la solution repose sur une simple invariante plutôt que sur des structures de données intelligentes. Dans cet article, nous disséquons les aspects *good*, *bad* et *ugly* de ce problème, explorons la solution la plus efficace et montrons comment intégrer votre maîtrise dans un portefeuille prêt à l'emploi.

---

#### Le bon: Invariants simples, code propre
- **Scan linéaire**: Seulement deux passes sur les données — l'une pour la longueur totale, l'autre pour le nombre de caractères.
- **Espace continu**: tableau de 26 éléments pour les lettres minuscules, pas de conteneurs dynamiques.
- **applicabilité universelle** : Fonctionne pour Java, Python, C++ ou n'importe quelle langue avec support de tableau.

#### Les mauvaises: Cas de bord et idées fausses
- **Ficelles vides**: Le problème garantit `words[i].longueur >= 1`, mais une implémentation naïve peut encore se déplacer sur une chaîne vide lors du comptage.
- **Pièges de séparation**: Oublier de vérifier `total Len % words.length` est un piège commun; il conduit à corriger les sorties sur de nombreux tests mais échoue sur ceux cachés.
- **Présomption d'ordonnance**: Certains participants pensent qu'ils doivent conserver l'ordre original des caractères; l'opération vous permet en fait d'insérer n'importe où, rendant l'ordre non pertinent.

C'est vrai. L'Ugly : sur-ingénierie et jeux de performance
- **Utiliser des cartes de hachage**: Un `HashMap<Caracter, Integer>` en Java ou `unordered_map` en C++ fonctionne, mais introduit des frais généraux inutiles.
- ** Solutions récursives** : Essayer de simuler les opérations entraîne récursivement un dépassement exponentiel du temps et de la pile.
- ** Contraintes de manœuvre** : Pour les chaînes jusqu'à 100 caractères et jusqu'à 100 chaînes, la solution O(N·M) est triviale; sur-optimisation avec des tableaux suffixes ou des arbres de segments est un gaspillage d'effort.

---

### L'idée de base – Une promenade

Laissez passer une course à sec** avec "mots = ["abc", "aabc", "bc"]".

1. ** Longueur totale** = 3 + 4 + 2 = 9.
"9 % 3 == 0 ' → **Longueur possible** = 3.
2. **Comptes des caractères**
- "a" : 3
- "b" : 2
- "c" : 2
Chaque dénombrement est divisible par 3 → **distribution réalisable**.
3. **Résultat**: vrai.

---

Code affiché

C'est vrai. Java (rapide, sans danger de type)
(Voir rubrique 5.1 ci-dessus)

#### Python (concise, lisible)
(Voir rubrique 5.2 ci-dessus)

#### C++ (orienté vers la performance)
(Voir rubrique 5.3 ci-dessus)

Chaque extrait suit exactement la même logique, ne différant que dans la syntaxe. N'hésitez pas à copier-coller dans votre IDE préféré.

---

### Pourquoi ce problème est d'interview Gold

- **Montre que vous comprenez les invariants**: Les candidats qui comprennent que l'opération est une *répartition* plutôt qu'une *réorganisation* ont tendance à impressionner les intervieweurs.
- ** Démontre un codage propre**: L'utilisation d'un tableau de taille fixe au lieu d'une carte reflète l'optimisation réfléchie de l'espace.
- **Adaptable** : La solution peut être étendue à des problèmes similaires (p. ex., faire en sorte que toutes les chaînes soient égales avec les swaps ou les nombres redistribués).

---

- Oui. Comment utiliser cet article pour trouver un emploi

1. **Blogue sur Moyen / Dev.to**
Poster cet article, l'étiqueter avec `leetcode`, `coding-interview`, `algorithm`, `java`, `python`, `cpp`. Les mots-clés SEO ci-dessus aideront les recruteurs à rechercher des solutions LeetCode vous trouvent.
2. **Ajouter à GitHub**
Créer un repo `leetcode-1897` contenant les trois fichiers de code, un README avec l'instruction de problème, et le lien de blog.
3. **Le levier lié En**
Partagez l'article avec une brève légende: **Solved LeetCode 1897 en 5 minutes avec une solution O(1) propre. Consultez mon blog pour la visite complète!
4. **Appliquer aux entreprises**
Rechercher les rôles de « Java backend », « Python data engineer » ou « C++ systems engineer » qui mentionnent LeetCode dans la description de travail. Joindre un lien vers votre blog ou GitHub repo dans votre CV ou lettre de motivation.

---

Dernier départ

Le problème *Redistribuer des caractères pour rendre toutes les chaînes égales* est un bel exemple de la façon dont un invariant simple peut s'effondrer une opération apparemment complexe mise en un contrôle trivial. Maîtrisez-le, écrivez un code propre, partagez-le, et laissez les recruteurs voir la clarté de votre processus de pensée. Bonne chance pour votre voyage d'entrevue !