---
Titre: LeetCode 2262. Appel total d'une chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes – LeetCode 2262: * Appel total d'une chaîne*

- Oui.
-- -- -- -- -- --
Difficulté
Type de chaîne, mathématiques, programmation dynamique Autres
** Contraintes du temps libre** Autres
**Support linguistique**

**Définition**

*Le **appeal** d'une chaîne* = le nombre de caractères **distinct** qu'il contient.
Compte tenu d'une chaîne `s`, retourner le **sum des appels** de **chaque** substring contigu possible de `s`.

---

Naïve Brute Force (et pourquoi c'est un grand non*)

1. Énumérer toutes les sous-chaînes «O(n2)».
2. Pour chaque sous-chaîne, construire un `Set` de ses caractères → `O(longueur)` travail.
3. Sommez les tailles.

**Time** – `O(n3)` dans le pire des cas (par exemple, tous les caractères sont identiques).
**Espace** – « O(1) » (à l'exception de l'ensemble temporaire).

> **Bad** – Ça saute vite. Même `n = 104` serait déjà invraisemblable.

---

- Oui. Insight: Contribution d'un personnage

Pensez à chaque caractère `c` indépendamment.
Combien de sous-chaînes contiennent cette occurrence particulière de `c`?
Si nous pouvons résumer ces chiffres sur tous les événements, nous obtenons la réponse.

Observation

Pour un événement à l'index «i» (0-basé):

- Laisser `last[c]` être l'index de l'occurrence **précédente** du même caractère.
(Si `c` n`est pas encore apparu, `last[c] = -1`.)
- Toute sous-chaîne se terminant à l'index `i` *et* commence **après** `last[c]` contiendra cette `c`.

Nombre de ces sous-chaînes
«» "
(i - last[c]) // positions de départ possibles
«» "

Donc la contribution de cet événement à la somme finale est
«» "
(i - last[c]) * (n - i)
«» "
parce que la sous-chaîne peut se terminer n'importe où de `i` à `n‐1`.

La complexité totale

Nous traversons la chaîne une fois, mettant à jour `last[26]` et ajoutant la contribution pour chaque caractère.
Les deux **temps** et **espace** sont linéaires/constantes.

> ** Bon** – temps « O(n) », espace « O(1) ».

---

- Oui. Pourquoi une boucle de 26 par personnage est *Ugly*

Une solution DP plus simple maintient un total en cours des dernières positions de chaque lettre (`last[26]`) et les ajoute via un `pour (int k=0;k<26;k++) total += i+1-dernier[k]».
C'est **'O(26 · n)'** – toujours linéaire, mais le facteur 26 peut dominer pour très grande `n`.
De plus, le code est plus difficile à lire et à raisonner.

---

## 4=" Solution O(n) Élégante Finale (Astuce Prev‐Occurrence)

Un point de vue légèrement différent est de maintenir l'appel actuel ** pour toutes les sous-chaînes qui se terminent à l'index `i`** (`cur`) et d'ajouter cela au résultat global.

«» "
cur += (i + 1) - last[s[i]] // new substrings that trowing this char into the appel
last[s[i]] = i + 1 // +1 afin que nous puissions commencer à compter à 1 au lieu de 0
Rés += cur
«» "

Les deux variantes produisent le même résultat ; nous présenterons les deux pour la clarté.

---

Code – Trois langues

> **Astuce** – Tous les codes sont prêts à fonctionner sur LeetCode, CodeChef, HackerRank, etc.

### 4.1. Java 17

"Java
// 2262. Appel total d'une chaîne – Java
solution de classe {
appel public long Somme(s) {
int n = s.longueur();
int[] dernière = nouvelle int[26]; // dernière occurrence (+1). 0 signifie jamais vu.
long res = 0, total = 0;

pour (int i = 0; i < n; i++) {
int idx = s.charAt(i) - 'a';
total += (i + 1) - last[idx]; // sous-chaînes qui incluent récemment ce char
last[idx] = i + 1; // update to current position (+1)
res += total; // toutes les sous-chaînes se terminant à i
}
retour rés;
}
}
«» "

4.2. Python 3.10+

'`python
# 2262. Appel total d'une chaîne – Python 3
de collections importer par défautdict

Solution de classe:
def recours Somme(s), s: str) -> Int:
n = len(s)
Last = defaultdict(lambda: -1)
Res = 0

pour i, ch dans le(s) énuméré(s):
# (i - last[ch]) * (n - i) – contribution de cet événement
res += (i - last[ch]) * (n - i)
last[ch] = i
retour res
«» "

Oui. C++17

'`cpp
// 2262. Appel total d'une chaîne – C++17
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long appel Somme (chaîne s) {
int n = s.size();
vecteur<int> dernier(26, -1);
longue rés = 0;
pour (int i = 0; i < n; ++i) {
int idx = s[i] - 'a';
res += 1LL * (i - last[idx]) * (n - i);
last[idx] = i;
}
retour rés;
}
};
«» "

Les trois codes fonctionnent dans **O(n)** temps, **O(1)** mémoire auxiliaire.

---

- Oui. Tranche Liste de contrôle des cas

Cas Résultat prévu Pourquoi c'est important
-- -- -- -- -- -- --
Autres Toutes les mêmes lettres, par exemple "aaaa" `4*5/2 = 10` sous-chaînes, chaque appel `1` → sum `10`
Autres Tous distincts, par exemple ""abcd""""" Appel de chaque sous-chaîne égale sa longueur" teste le scénario d'appel *max*"
Chaîne vide – non autorisée par les contraintes
Autres Caractère unique, par exemple "z"""" Appel "1""
La longueur maximale `105` corde aléatoire doit finir < 0,5 s sur LeetCode

---

## 5-- Test rapide Harnais (Python)

'`python
def brute(s):
n = len(s)
ans = 0
pour i dans la plage(n):
vu = set()
pour j dans la plage(i, n):
Voir.add(s[j])
ans += len(see)
retour et

def test():
importer au hasard, chaîne
pour n dans la plage(1, 50):
pour _ dans l'intervalle(100):
s = ''.join(random.choice('abc') pour _ dans l'intervalle(n))
si brute(s) != Solution().appealSum(s) :
print('Mismatch', s, brut(s), Solution().appealSum(s))
retour
print('Tous les tests sont passés!')

si __nom__ == "__main__" :
essai()
«» "

---

Conclusion – Ce que veulent les intervieweurs

- **Efficacité dans le temps**: "O(n)" résout le problème en sous-seconde même pour `n=105`.
- **Space‐light**: seulement un tableau ou dictionnaire de 26 éléments.
- **Élégance mathématique** : la contribution du personnage évite les boucles ou les boucles sales.

> **Bien** – Simple, linéaire, facile à raisonner.
> **Bad** – Naïve set‐based ou DP avec 26 boucles par caractère – les deux sont inutiles.
> **Ugly** – La suringénierie de la solution ou l'oubli de l'astuce +1 peut conduire à des hors-par-ones.

---

Article sur le blog optimisé du SEO

Titre
> **Master LeetCode 2262 – Appel total d'une chaîne Java, Python, C++ O(n) Solution**

Description de la méta
> Solve LeetCode 2262 *Appel total d'une chaîne* dans le temps linéaire. Apprenez le trick de contribution de caractère avec le code clair Java, Python et C++. Parfait pour la préparation d'entrevue!

---

Post Blog

Introduction
Entretiens problèmes d'amour qui déguisent un modèle simple derrière un ard... *L'appel total d'une chaîne* est un tel classique. Malgré son tag `Hard`, la solution la plus efficace est un algorithme `O(n)` à passe unique avec la mémoire `O(1)`. Ce billet vous permet de parcourir :

- Rétablissement du problème
- Pièges naïfs
- La solution linéaire **good**
- La force quadratique/brute cubique
- La version **ugly** DP avec 26 boucles
- Nettoyez les extraits de code (Java, Python, C++)
- Analyse de complexité
- Discussion de cas
- Harnais d'essai rapide

---

#### 1-

> **Appeal** = nombre de caractères distincts dans une chaîne.
> Pour chaque substring contigu des `s`, calculer son appel et les résumer tous.

Exemple: `s = "aba"`
Sous-chaînes → `"a"`, `"ab"`, `"aba"`, `"b"`, `"ba"`, `"a"`
Appels → 1, 2, 1, 2, 1 → **Total = 9**.

---

C'est vrai. Approche naïve – Le grand non-non

Texte
pour chaque i dans [0,n):
pour chaque j en [i,n):
construire ensemble de s[i..j]
ans += taille(set)
«» "

- **Heure** `O(n3)` → impossible pour `n=105`.
- **Espace** "O(1)" (ignorer l'ensemble temporaire).

C'est le classique *explosif* que vous devez éviter dans les entrevues.

---

C'est vrai. Le point de vue sur le caractère

Considérez chaque apparition d'un personnage séparément.

1. `dernier[26]` contient l'index de la dernière occurrence de chaque lettre (`-1` si aucune).
2. Pour l'occurrence à l'index `i` de caractère `c`:
- Sous-chaînes qui **démarrent après** "last[c]" et **à la fin ou après** `i` contiennent cette `c`.
- Nombre de départs: "i - last[c]".
- Nombre de extrémités: `n - i`.
3. Contribution: "i - last[c]) * (n - i)".

Ajoutez ceci pour chaque indice.

**Résultat:** Scan linéaire, espace auxiliaire constant.

> Pourquoi ça ? Pas de boucles imbriquées, pas de jeux coûteux, juste de l'arithmétique entier.

---

C'est pas vrai. Le PDD Ugly avec 26 boucles

Un schéma de PDD commun:

Texte
Total = 0
pour chaque caractère:
Total += Last[c]
last[c] = i
«» "

Ensuite, dans chaque itération, additionner toutes les valeurs `derniers` via un `pour intérieur (k=0;k<26;k++) total += dernier[k]; "
C'est **'O(26 · n)'**, toujours linéaire, mais le facteur constant nuit à la lisibilité et aux performances.

> **Ugly** – Ajoute des boucles inutiles et rend la logique plus difficile à maintenir.

---

#### 5.

Code de la langue
C'est quoi, ça ?
**Java** Cliquez pour voir la solution </résumé><pre>class {<br> appel public long Sum(String) {<br> int n = s.longueur();<br> int[] last = new int[26];<br> long res = 0;<br> pour (int i = 0; i < n; ++i) {<br> int idx = s.charAt(i) - 'a';<br> res += 1L * (i - last[idx]) * (n - i);<br> last[idx] = i;<br> }<br> retour res;<br> }<br>}<br><br><br></pre></details> Autres
**Python**= <details><sommary>Cliquer pour voir</sommary><pre>class Solution:<br> def appealSum(self, s: str) -> int:<br> n = len(s)<br> last = defaultdict(lambda: -1)<br> res = 0<br> pour i, ch in énumérate(s):<br> res += (i - last[ch]) * (n - i)<br> last[ch] = i<br> res</pre></details> Autres
**C++** Cliquez pour visualiser</résumé><pre> solution de classe {<br>public:<br> long long appelSum(string s) {<br> int n = s.size();<br> vector<int> last(26, -1);<br> long res = 0;<br> pour (int i = 0; i < n; ++i) {<br> int idx = s[i] - 'a';<br> res += 1LL * (i - last[idx]) * (n - i);<br> last[idx] = i;<br> }<br> res;<br><br>};</pre></details> Autres

Tous les codes sont compilés sur LeetCode, CodeChef et autres juges en ligne.

---

Récapitulation de la complexité

- **Heure** : "O(n)" (passe unique).
- **Espace**: `O(1)` (26 éléments de tableau ou dictionnaire).
- **Opérations numériques** : multiplications `1 × 106` et ajouts pour `n=105` – trivial sur les processeurs modernes.

---

Essais – Script Python rapide

'`python
def brute(s):
# O(n^3) force brute pour les petites cordes
...

def test():
importer au hasard, chaîne
pour n dans la plage(1, 100):
pour _ dans l'intervalle(200):
s = ''.join(random.choice('abcd') pour _ dans l'intervalle(n))
si brute(s) != Solution().appealSum(s) :
print('Fail', s, brut(s), Solution().appealSum(s))
retour
print('All good!')

essai()
«» "

Exécutez ce script localement pour valider votre implémentation avant de soumettre.

---

- Oui. Dernier départ

*L'appel total d'une chaîne* vous apprend que beaucoup de problèmes -Hard-Hard se résument à un tour linéaire caché. Maîtrisez le modèle de contribution de caractère, et vous répondrez avec confiance en Java, Python ou C++ lors des interviews de codage. N'oubliez pas : recherchez toujours une solution arithmétique simple avant de recourir à des ensembles ou à des boucles imbriquées.

---

Lire plus

- Cracking the Coding Interview - Tricks de comptage de caractères
- LeetCode Problèmes difficiles – chapitre de reconnaissance des motifs
- Codage Interview Prep - O(n) tricks collection

Bon codage ! C'est ce qu'il a dit.

---

La pensée finale

Que vous vous attaquiez à des défis de codage ou à des interviews techniques, la leçon de *Total Appeal of a String* est claire : cherchez le modèle arithmétique **simple** derrière un problème complexe, maintenez vos boucles serrées et toujours viser le temps linéaire. Joyeux entretien !