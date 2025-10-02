---
titre: LeetCode 3407. Sous-chaîne du modèle de correspondance -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3407 – Sous-chaîne Modèle de correspondance
** Problème* *
> On vous donne une chaîne `s` et une chaîne `p`.
> `p` contient exactement un caractère `*`. Le `*' peut être remplacé par n'importe quel
> (éventuellement vide) séquence de caractères.
> Retour `true` si `p` peut être fait un *sous-chaîne* de `s`, sinon retourner `faux`.

**Exemples**
Résultats
- C'est quoi ?
`leetcode`="ee*e`="true`=" `*` → `tcod` → `eetcode` Autres
Pas de sous-chaîne correspondant
"luck" "u" "true" "*" → "{}" → "u" (ou "uc", "uck") Autres

**Contrôles* *

"1 ≤ longueur ≤ 50"
- "1 ≤ p.longueur ≤ 50"
- "s" ne contient que des lettres anglaises minuscules
- `p` contient seulement des lettres anglaises minuscules et exactement une `* "

---

Trois solutions de foudre

L'astuce est simple :
Divisez le motif dans la partie avant `*` (`préfixe`) et la partie après `*` (`suffix`).
Si `préfix` et `suffix` apparaissent dans `s` **dans cet ordre** (avec le suffixe commençant après la fin du préfixe), alors le motif correspond à une sous-chaîne de `s`.

- Oui. 1. Java (temps O(n), espace O(1))

"Java
solution de classe {
public booléen hasMatch(String s, String p) {
= p.indexOf('*'); // position de '* '
Préfixe de chaîne = p.substring(0, étoile);
suffixe de chaîne = p.substring(étoile + 1);

// Trouver la première occurrence de préfixe
int start = s.indexOf(préfix);
Si (démarrer) -1) retourner faux;

// Trouver le suffixe à partir de la fin du préfixe
Int fin = s.index de(suffix, début + préfix.longueur());
retour fin != -1;
}
}
«» "

- Oui. 2. Python (3 lignes, temps O(n), espace O(1))

'`python
Solution de classe:
def hasMatch(self, s: str, p: str) -> C'est vrai.
avant, après = p.split('*')
i = s.find(pre)
retour i != -1 et s.find(post, i + len(pre)) != -1
«» "

- Oui. 3. C++ (temps O(n), espace O(1))

'`cpp
solution de classe {
public:
bool hasMatch(chaîne s, chaîne p) {
taille_t étoile = p.find('*');
chaîne pre = p.substr(0, étoile);
string post = p.substr(étoile + 1);

taille_t i = s.find(pre);
si (i == chaîne::npos) retourner faux;

taille_t j = s.find(post, i + pre.longueur());
retourner j != chaîne::npos;
}
};
«» "

> **Pourquoi ça marche* *
> `indexOf` / `find` scans `s` seulement une fois pour chaque partie, de sorte que la complexité globale est linéaire dans `=s="`.
> Nous n'avons jamais besoin d'une table de programmation dynamique ou d'un rétrotraçage – le motif n'a qu'une seule carte.

---

Article du blog : Le bon, le mauvais, et l'acharnement de Substring Pattern

Introduction
Le **Substring Matching Pattern** (LeetCode 3407) est un problème fallacieux qui teste votre capacité à penser à la manipulation de chaînes et à l'efficacité algorithmique. En tant que candidat à l'entrevue, montrer une solution propre et efficace ici peut impressionner les gestionnaires d'embauche à la recherche de *concise* et *correct* code. Dans cet article, nous allons parcourir les aspects *bon*, *mauvais* et *doucement* du problème, présenter trois solutions idiomatiques (Java, Python, C++) et vous donner une référence prête à passer pour vous aider à poser ce rôle de rêve.

> **SEO Mots-clés**: LeetCode 3407, Substring Matching Pattern, interview coding, Java solution, Python solution, C++ solution, job interview prep, algorithme, string matching, wildcard pattern.

---

Les bons

Aspect Ce que nous aimons
C'est pas vrai.
Un seul `*` fait le problème linéaire-temps; nous n'avons pas besoin de DP ou de backtracking. Autres
**Readable Split**= Le fractionnement `p` en `préfixe` et `suffix` est intuitif et élimine la confusion dans les cas de bord. Autres
**Construire la recherche**= `String.indexOf`, `str.find`, et `std::string::find` font le levage lourd dans l'espace constant. Autres
**Complexité claire**="Temps d'O(="s)", espace auxiliaire d'O(1), parfait pour les contraintes d'entretien. Autres
La même logique s'applique à Java, Python et C++, ce qui facilite l'adaptation. Autres

---

- Oui. Les mauvais

Pourquoi il peut vous faire monter
C'est ce qu'on dit.
**Substring Overlap**= Si le préfixe et le suffixe se chevauchent, le naïf `indexOf` peut sauter les correspondances valides. L'algorithme ci-dessus gère cela parce que la recherche suffixe commence **après** le préfixe se termine. Autres
**Empty Prefix/Suffix**= Lorsque le motif commence ou se termine par `*`, l'une des pièces est vide. Notre code fonctionne toujours parce que `indexOf("")` retourne `0`, permettant des correspondances n'importe où. Autres
Bien que les contraintes soient minuscules, un intervieweur peut tester le cas le plus défavorable ("S" = 50,"p" = 50"). La solution fonctionne toujours en microsecondes. Autres

---

- Oui. L'Ugly

La partie "puisse" est ce que beaucoup de débutants trébuchent:

1. ** Erreurs hors‐par‐un**
Le démarrage de la recherche suffixe à `start + prefix.length()` est critique. Commencer par `start` peut accepter incorrectement les chevauchements qui violent la contrainte de commande.

2. **Causes d ' exclusion avec "*" à la fin**
Oublier que `""` est une sous-chaîne valide peut causer de faux négatifs lorsque `p = "*abc"` ou `p = "abc*"`. Notre implémentation s'en charge automatiquement.

3. **Plusieurs cartes sauvages**
Certains intervieweurs ont modifié le problème pour permettre plus d'un "*". La solution présentée casse alors; vous auriez besoin d'une approche DP ou régex plus sophistiquée.

---

Pourquoi ça compte pour votre travail de chasse

- **Démontre la clarté algorithmique** – Vous avez résolu un vrai problème d'interview avec une solution O(n) propre.
- **Showcases Cross-Language Proficiency** – Savoir traduire la même logique en Java, Python et C++ indique la polyvalence.
- **Points saillants Attention au détail** – La manipulation des préfixes/suffixes vides et des bogues off-by-one vous montre que vous êtes complet.
- **SEO‐Ready Portfolio** – Publier cet article (avec les extraits de code) sur GitHub ou un blog personnel donne aux recruteurs une référence rapide et stimule votre visibilité en ligne.

---

Référence rapide

Code de la langue
C'est quoi, ça ?
{<br> public boolean hasMatch(String s, String p) {<br> int star = p.indexOf('*);<br> String pre = p.substring(0, star);<br> Le nombre de chaînes = p.substring(étoile + 1);<br> int i = s.indexOf(pre);<br> si (i== -1) retourner faux;<br> retourner s.index De(post, i + pre.longueur()) != -1;<br> }<br>}`` Autres
**Python**="python<br>class Solution:<br> def hasMatch(self, s: str, p: str) -> bool:<br> pre, post = p.split('*')<br> i = s.find(pre)<br> retour i != -1 et s.find(post, i + len(pre)) != -1'''
{<br>public:<br> bool hasMatch(string s, string p) {<br> size_t star = p.find('*');<br> string pre = p.substr(0, star);<br> string post = p.substr(star + 1);<br> size_t i = s.find(pre);<br> if (i) string::npos) retourner false;<br> retourner s.find(post, i + pre.long()) != string::npos;<br> }<br>;``` Autres

---

Les pensées finales

Substring Matching Pattern est un problème *gateway* dans de nombreuses entrevues de codage.
En maîtrisant la stratégie de séparation **préfixe-suffixe** et en évitant les pièges communs, vous pouvez résoudre ce problème avec confiance et impressionner les intervieweurs avec un code propre et prêt à la production.

> ** Prêt au code?** Prenez votre IDE, copiez les extraits ci-dessus, et essayez quelques tests personnalisés!
> **Vous voulez booster votre CV?** Écrivez un court billet de blog ou un GitHub Gist, marquez-le avec `#LeetCode3407`, et laissez les recruteurs vous découvrir.

Bon codage, et bonne chance pour la prochaine interview! C'est ce qu'il a dit