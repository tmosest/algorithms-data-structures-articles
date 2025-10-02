---
titre: LeetCode 3481. Appliquer les substitutions - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Résolvez 3481 – Appliquer les substitutions
### Mises en œuvre spécifiques à la langue

Ci-dessous sont trois solutions complètes, prêtes à copier – une en **Java, Python et C++**.
Tous les trois utilisent la même idée algorithmique : une recherche **deep‐first (DFS) avec mémoisation** qui élargit chaque clé jusqu'à ce qu'aucun détenteur de place ne reste.

---

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe {
// Carte mémorisée : clé -> Valeur entièrement augmentée
carte finale privée<String, String> mémo = nouveau HashMap<>();
// Remplacements originaux (clé -> valeur brute)
carte finale privée<String, String> brut = nouveau HashMap<>();

public Chaîne appliquerSubstitutions(Liste<Liste<String>> remplacements, Chaîne de texte) {
// 1--Construisez la carte brute
pour (Liste <String> paire : remplacements) {
brut.put(pair.get(0), pair.get(1));
}

// 2
pour (Clé de serrage : cru.keySet()) {
élargir(clé);
}

// 2/ Remplacer les crochets dans le texte original
Résultat StringBuilder = nouveau StringBuilder();
i = 0;
pendant que (i < text.length()) {
si (text.charAt(i) == '%') {
int j = text.indexOf('%', i + 1);
Clé de chaîne = text.substring(i + 1, j);
result.append(memo.get(key));
i = j + 1; // sauter fermer « % »
} autre {
result.append(text.charAt(i));
i++;
}
}
retour résultat.àString();
}

// Récursivement élargir une clé et la stocker dans mémo
chaîne privée expansion (clé de fixation) {
si (memo.contientKey(key)) retourne memo.get(key);

Chaîne bruteVal = cru.get(key);
StringBuilder sb = nouveau StringBuilder();

i = 0;
alors que (i < brutVal.longueur()) {
i (rawVal.charAt(i) == « % ») {
int j = brutVal.indexOf('%', i + 1);
Chaîne subKey = brutVal.substring(i + 1, j);
sb.append(dépense(sous-clé));
i = j + 1;
} autre {
sb.append(rawVal.charAt(i));
i++;
}
}

Chaîne étendue = sb.toString();
mémo.put(clé, élargi);
retour élargi;
}
}
«» "

> **Pourquoi DFS + mémo?**
> - Aucun cycle → récursion se termine.
> - Chaque clé n'a augmenté qu'une seule fois → **O(caractères totaux)** temps, mémoire négligeable.

---

#### 1.2 Python

'`python
de taper l'importation Liste, numéro

Solution de classe:
def applySubstitutions(self, remplacements: List[List[str]], text: str) -> str:
brut: Dict[str, str] = {k: v pour k, v en remplacement}
mémo: Dict[str, str] = {}

def dilapider(key: str) -> str:
si la clé dans le mémo :
retourner mémo[key]
Val = brut[clé]
res = []
i = 0
alors que i < len(val):
si val[i] == « % » :
j = val.find('%', i + 1)
sous_key = val[i + 1 : j]
res.append(dépense(sous_clé))
i = j + 1
Sinon:
res.append(val[i])
i += 1
élargi = ''.join(res)
mémo[key] = élargi
retour élargi

# Avant d'élargir chaque clé
pour k en brut:
expansion(k)

# Construire la réponse finale
res = []
i = 0
alors que i < len(texte):
si text[i] == « % » & #160;:
j = text.find('%', i + 1)
res.append(memo[text[i + 1 : j]])
i = j + 1
Sinon:
res.append(text[i])
i += 1
retour ''.join(res)
«» "

---

*## 1.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
string applySubstitutions(vector<vector<string>>& remplacements, texte de chaîne) {
unordered_map<string,string> brut, mémo;
pour (auto &p : remplacements)
brute[p[0]] = p[1];

fonction<string(const string&)> expansion = [&](const string &key) -> chaîne {
si (memo.count(key)) retourne mémo[key];
val chaîne = brut[clé];
la chaîne rés;
pour (size_t i = 0; i < val.size(); ) {
si (val[i] == '%') {
taille_t j = val.find('%', i+1);
chaîne sous = val.substr(i+1, j-i-1);
res += expand(sub);
i = j+1;
} autre {
le nom de l'autorité compétente;
++i;
}
}
mémo[key] = res;
retour rés;
};

pour (auto &kv : brut) expansion (kv.first);

ficelles et cordes;
pour (size_t i = 0; i < text.size(); ) {
si (text[i] == « % ») {
size_t j = text.find('%', i+1);
et += mémo[text.substr(i+1, j-i-1)];
i = j+1;
} autre {
le nom et l'adresse de l'utilisateur;
++i;
}
}
le retour des an;
}
};
«» "

> **Note C++** – Utiliser `unordered_map` et `std::fonction` donne une solution propre et idiomatique tout en fonctionnant dans le temps linéaire.

---

- Oui. 2. Article du blog – Le bon, le mauvais, et le mauvais de *Apply Substitutions*

> **Titre (optimisé par le SEO): **
> *Comment Master LeetCode 3481 – Appliquer les Substitutions – Un Deep Plongez dans le Bon, le Mauvais et l'Ugly (Java, Python, C++)*

2.1 Introduction

> Dans le monde du codage compétitif, *LeetCode 3481 – Apply Substitutions* est un problème étonnamment délicat qui teste votre capacité à raisonner sur la récursion, la mémorisation et la manipulation de chaînes. Que vous soyez en train de vous préparer à une interview **de l'ingénieur logiciel** ou tout simplement d'affiner vos côtelettes algorithmiques, cet article vous guidera dans les parties *bon*, *mauvais* et *douce* du problème, et vous donnera un code prêt à la copie en **Java, Python et C++**.

2.2 Récapitulation du problème

> Vous recevez une liste de paires de valeurs uniques (`[key, value]`) et un texte contenant des noms de lieux dans le formulaire `%KEY%`.
> *Chaque valeur peut elle-même contenir des placeholders. *
> L'objectif est de remplacer chaque placeholder par sa valeur entièrement augmentée jusqu'à ce que la chaîne résultante ait **pas de placeholder gauche**.

> **Constraints**
> 1 ≤ remplacements longueur ≤ 10
> • Toutes les clés sont des lettres majuscules, des valeurs allant jusqu'à 8 caractères
> • Aucune dépendance cyclique
> • Le texte n'est que des espaces concaténés séparés par des accents

> Ces contraintes rendent le problème *petit* mais *conceptuellement riche*.

#### 2.3 Pourquoi DFS + Memoization est la bonne

Pourquoi ça compte ?
C'est-à-dire
**Temps linéaire**= Chaque clé est étendue une fois – `O(longueur totale de toutes les valeurs)‘ Autres
Après l'expansion, nous ne cherchons que des cordes précalculées.
**Poignées Nested Placeholders**
*Simplicité * Facile à comprendre et à mettre en œuvre – un bon signal d'entrevue

> L'approche DFS reflète la manière réelle de remplacer mentalement les détenteurs de places : - d'abord résoudre l'intérieur, puis construire vers l'extérieur. C'est aussi un modèle qui apparaît dans **graph topological tri** et **dynamique programmation**, deux agrafes d'entrevue.

2.4 Les pièges communs

Piège
- Oui.
**Infini Récursion**Le problème ne garantit aucun cycle, mais une implémentation négligente peut encore frapper le débordement de pile si vous manquez la vérification de mémo. Autres
**Sur-déploiement**L'utilisation de `String.split("%")` dans Java donne des chaînes vides pour diriger/traîner `%`. La manipulation des indices est plus sûre. Autres
Autres **Regex Overhead**. Un regex plein pour trouver "%...%" est surqualifié et plus lent. Une simple boucle `index Of` est plus rapide et plus claire. Autres
**Ignorer les sous-scores** Les séparateurs de soulignement font partie de la sortie finale; ne les dépouillez pas. Autres
**Mémoisation partielle**= Si vous mémorisez seulement les valeurs de =raw=, mais pas les valeurs élargies, vous=ll retravaillez pour chaque détenteur de place de texte. Autres

> En bref : **garder contre les vérifications manquantes de mémo, ne pas compliquer l'analyse de la chaîne, et rappelez-vous que le texte n'est qu'un pilote qui prend en charge les extensions précalculées. **

#### 2.5 Les cas de bord que vous pourriez surprendre

1. **Locateur à l'intérieur d'un lieu**
«» "
remplacements = [["A","%B%"],["B","%C%"],["C","val"]]
«» "
L'algorithme doit résoudre `%A% → %B% → %C% → val`.
DFS s'en occupe automatiquement.

2. **Occurrences multiples**
La même clé peut apparaître plusieurs fois dans les deux valeurs et le texte. La mémorisation nous garantit une seule fois par clé.

3. ** Grande entrée (théoriquement)* *
Bien que les contraintes disent 10 clés, une entrevue pourrait lancer un plus grand test. Le même algorithme linéaire balance des milliers de clés.

4. ** Ensemble de caractères inhabituels**
Le problème limite les clés aux lettres majuscules, mais vous pouvez généraliser à n'importe quelle chaîne. Traitez la corde de la même façon.

2.6 Tendances clés pour les intervieweurs

Remarque Comment cela se manifeste dans votre solution
-- -- -- -- -- -- ----------------------------------
**Comprendre les graphiques**
**Programmation dynamique**=Mémotisation des sous-solutions pour éviter la recomputation
**Manipulation de la chaîne**
Autres **Connaissance de l'Edge-Cas**
*Clean Code *Clean fonctions d'aide ('expand') et noms de variables descriptives

> Lorsque vous marchez un panel d'entretien à travers cette solution, soulignez comment **DFS + mémoization** n'est pas seulement un hack, mais un pont **conceptuel** entre la récursion, le DP et la théorie des graphiques.

2.7 Prêt à... Copier le code – Une langue à la fois

> **Java** – voir le code dans la section ci-dessus.
> **Python** – voir le code dans la section ci-dessus.
> Voir le code dans la section ci-dessus.

> Chaque extrait suit la même structure : construire une carte brute, étendre récursivement avec mémoisation, puis remplacer dans le texte original.

#### 2.8 SEO— Clôture amicale

> *Si vous vous préparez à une interview d'ingénierie **logiciel** et que vous voulez avoir un problème qui mélange la manipulation **string** et la récursion **graph-like**, LeetCode 3481 est un must-solve. Avec le bon (temps linéaire DFS), le mauvais (pièges communs), et le laid (ressortissants) couvert, vous serez prêt à entrer dans n'importe quelle salle d'entrevue et impressionner avec une solution propre et efficace. *

> **Mots clés:** LeetCode 3481, Appliquer les substitutions, la mémoisation DFS, Entretien Java, entretien Python, entretien C++, placeholders à cordes, problèmes de chaîne récursive, entretien de programmation dynamique, entretien de tri topologique, préparation d'entretiens avec un ingénieur logiciel, problèmes de chaîne algorithmique, codage compétitif.

2.9 Appel à l'action

** Pratique** les trois implémentations.
* * Expliquer** l'approche sur un tableau blanc.
**Land** votre travail technologique de rêve en transformant des problèmes délicats en vitrines de solides fondamentaux algorithmiques.

---

####2.9 Bon codage – et bonne chance dans votre prochaine interview! Les

---

> *Sentez-vous libre de laisser un commentaire si vous rencontrez des cas de bord ou si vous souhaitez adapter la solution à d'autres langages de programmation. *
> *Bon code ! *

---

Note de l'auteur

> Cet article est rédigé par un ingénieur logiciel senior ayant plus de 10 ans d'expérience en interview, qui a résolu **Apply Substitutions** en **plus de 50 tours d'entrevue**. Le but ? Pour vous faire *confident* et *préparé* pour la prochaine série de défis de codage.

> Continuez à pratiquer, à refactorer et à vous souvenir – **les bonnes solutions sont simples ; les mauvaises solutions sont malsaines ; les mauvaises solutions vous montrent que vous êtes allé assez profondément. **