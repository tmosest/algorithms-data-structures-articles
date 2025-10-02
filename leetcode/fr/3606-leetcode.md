---
titre: LeetCode 3606. Validateur de code de coupon - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3606. ** Validateur de code de coupon** – Solution à pile complète (Java, Python, C++)
> *=Code propre== Débutant-Amis==Traitement personnalisé==

---

### TL;DR
La complexité temporelle La complexité spatiale Autres
Il s'agit d'un projet pilote.
**O(n log n)**
**O(n log n)**
* * * * * * * * * * * * * * * * * * * * * *

La solution est une simple routine de filtre à l'époque.
- **Filter** : ne conserver que les coupons actifs, non vides, ayant un code alphanum-underscore valide et appartenant à l'une des quatre catégories d'entreprises.
- **Trier** : utiliser une carte de priorité pour les quatre catégories puis l'ordre lexicographique du code.

Les trois implémentations sont < 40 lignes de code propre et prêt à la production.



---

- Oui. 1. Mise en œuvre Java

"Java
Importation de java.util.*;

solution de classe publique {

// Ordre des secteurs d'activité – nombre inférieur = priorité plus élevée
Carte statique privée<String, entier> COMMANDE = Carte
"électronique", 0,
"l'épicerie", 1,
"pharmacie", 2,
"restaurant", 3
);

liste publique<String> validerCoupons(code String[],
Chaîne[] entreprise Ligne,
booléen[] estactif {

Liste <Coupon> valide = nouvelle liste de distribution<>();

pour (int i = 0; i < code.longueur; i++) {
// --- 1 Contrôles de base ------------------------------------------------
si (code[i] == null="code[i].isEmpty() continue;
si (!code[i].matches("[a-zA-Z0-9_]+") continue;
si (!ORDER.contientKey(businessLine[i])) continue;
si (!estActive[i]) continue;

// --- 2 Stockez un objet coupon léger -----------
valid.add(nouveau Coupon(code[i], businessLine[i]);
}

// --- 3 Tri selon la priorité commerciale puis ordre lexicographique
valid.sort(Comparateur
.comparerInt(Coupon c) -> COMMANDE.get(c.businessLine))
.thenComparing(c -> c.code) ;

// --- 4 Extrait juste les codes pour la réponse finale -----------------
Liste du résultat <String> = nouvelle liste de distribution<>(valid.size());
pour (Coupon c : valide) result.add(c.code);
le résultat du retour;
}

// Conteneur léger – pas de getters / setters pour la brièveté
classe statique privée Coupon {
finale Code chaîne;
Final String business Ligne;
Coupon(code de la chaîne, ligne d'affaires) {
code = code;
ce.businessLigne = entreprise Ligne;
}
}
}
«» "

---

- Oui. 2. Mise en œuvre de Python

'`python
importations
de taper l'importation Liste

Solution de classe:
# Ordre de priorité pour les quatre catégories d'entreprises
ORDONNANCE = {"électronique": 0, "épicerie": 1,
"pharmacie": 2, "restaurant": 3}

def valide Coupons(s)
code: Liste[str],
BusinessLine: Liste[str],
isActive: List[bool]) -> List[str]:

# Regex pour alphanumérique + souligné
modèle = re.compile(r'^[A-Za-z0-9_]+$')

N° 1 Filtrer les coupons valides
valide = [
(c, bl) pour c, bl, agir en zip(code, businessLine, estActive)
si acte et c et pattern.match(c) et bl en soi. ORDRE
- Oui.

N° 2 Tri: d'abord par priorité d'affaires, puis par lexicographie
valid.sort(key=lambda x: (self.ORDER[x[1]], x[0])

N° 3 Ne retourner que les codes
retour [c pour c, _ valide]
«» "

---

- Oui. 3. Mise en œuvre C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<string> validerCoupons(vecteur<string> code,
vecteur <string> entreprises Ligne,
vecteur<bool> estactif) {
Carte des priorités des entreprises
non ordonné_map<string, int> ordre = {
{"électronique", 0},
{"épicerie", 1},
{"pharmacy", 2},
"Restaurant", 3
};

// / / / / / Aide régex: alphanumérique + souligné
le modèle regex(R"([A-Za-z0-9_]+)";

// Stocker les coupons valides en paires (code, businessLine)
vector<pair<string, string>> valable;
pour (size_t i = 0; i < code.size(); ++i) {
si (!estActive[i]) continue;
si (code[i].vide()=" !regex_match(code[i], pattern) continue;
si (!order.count(businessLine[i])) continue;
valid.emplace_back(code[i], businessLine[i]);
}

Tri personnalisé : priorité puis lexicographie
tri(valid.begin(), valid.end(),
[&](const auto &a, const auto &b) {
int p = ordre[a.seconde] - ordre[b.seconde];
Si (p != 0) retour p < 0;
retour a. premier < b. premier;
});

// Extraire les codes triés
vecteur <string> résultat;
result.reserve(valid.size());
pour (const auto &p : valide) result.push_back(p.first);
le résultat du retour;
}
};
«» "

---

- Oui. 4. Article de blog: -Validateur de code de coupon – Le bon, le mauvais, et le mauvais

> **SEO Focus:** Validateur de code de coupon, LeetCode 3606, solution Java/Python/C++, question d'entretien, code propre, tri personnalisé, entretien d'emploi

---

4.1 Introduction

Quand j'ai vu pour la première fois *Coupon Code Validator* (LeetCode 3606), le problème a semblé presque trop facile pour une entrevue de 2 minutes : (en milliers de dollars)
Mais il y a des pièges subtils, des cordes vides, des personnages bizarres, des catégories professionnelles invalides, qui peuvent même voyager avec des ingénieurs chevronnés.

Dans cet article, je vais passer par le **bon** (ce que le problème enseigne), le **mauvais** (pièges communs), et le **ugly** (cas de bord cachés). Je terminerai avec une solution propre et prête à la production en **Java, Python et C++** que vous pourrez déposer dans votre CV ou vos notes d'entrevue.

---

4.2 Récapitulation des problèmes

> **Input**
> Trois tableaux de longueur *n* (`code`, `businessLine`, `isActive`).

> **Règles pour un coupon valide* *
> 1. Le `code` n'est pas vide et ne contient que des lettres, des chiffres ou des points forts (`_`).
> 2. `businessLine` , {...
> 3. " est actif " == " vrai " .

> ** Sortie**
> Liste triée des codes coupons valides, d'abord par priorité d'entreprise
> ("électronique → épicerie → pharmacie → restaurant"), puis lexicographiquement.

> **Constraints**
> 1 ≤ n ≤ 100, chaque longueur de chaîne ≤ 100.
> Toutes les entrées sont imprimables ASCII.

---

### 4.3 Les bonnes – Pourquoi Ce problème est précieux

1. **Spécifications claires** – Les règles sont sans ambiguïté, donc les tests de problèmes *la compréhension de lecture*.
2. **Simple Structures de données** – Listes/arrays et une petite carte de recherche.
Idéal pour pratiquer la manipulation *collection*.
3. **Traitement personnalisé** – Introduit l'idée d'une carte *prioritaire* plus une clé *secondaire*.
4. **Regex Basics** – Valider un code de coupon avec un seul regex (`[A-Za-z0-9_]+`) est un moyen rapide de montrer la connaissance de la correspondance des motifs.
5. **Temps‐Espace échange** – La solution O(n2) naïve serait plus lente; la solution O(n log n) optimale est simple.

---

4.4 Les mauvaises – Pièges communs

Pourquoi ça arrive
- Oui.
En Java ou en C++, l'égalité des chaînes est basée sur la référence. Utiliser `.equals()` ou `==` après avoir stocké dans un `non-ordonné_map`. Autres
**Ignorer les valeurs `null`**.Le `code[i]` ou `businessLine[i]` peut être `null` dans les tests Java. Ajouter "si (code[i]] == null" code[i].isEmpty() continue;"
**Omettre les limites du regex**=Le `matches("[A-Za-z0-9_]+")' peut correspondre à des sous-chaînes. Prépendre `^` et ajouter `$` → `^[A-Za-z0-9_]+$`. Autres
La valeur de la carte de priorité est mal utilisée (p. ex. `-ORDER.get()` vs `ORDER.get()`). ORDER.get(c.businessLine)» Autres
**Dupliquer les lignes d'affaires**= Si le même code apparaît deux fois, le genre peut encore les commander correctement, mais certaines personnes oublient de préserver l'ordre des doublons. Conservez un objet léger (`Coupon`) au lieu d`une paire `String[]`.
**Sur-ingénierie**= Écrire une classe complète avec getts/setters pour une fonction aussi minuscule. Utilisez une classe intérieure minimale ou un tuple; conservez le code lisible. Autres

---

4.5 Les horribles cas de bords cachés

Surmonter l'impact Comment surveiller
- C'est quoi ?
"code" = "_" Valable par regex mais sémantiquement étrange. Le régex l'accepte toujours – la spec dit seulement alphanum ou souligne, donc il est très bien. Autres
Le tri fonctionne toujours; aucun duplicata n'est supprimé. Si vous voulez unicité, vous pouvez ajouter un `Set` avant l'extraction finale. Autres
Autres Très long `code` (100 chars)=Peut frapper la profondeur de récursion ou les limites de tampon dans les langues avec de petites piles. Aucun effet ici parce que n ≤ 100; mais toujours utiliser `StringBuilder`/`vector` pré-allocation dans Java/C++. Autres
En mélangeant `True`/`true` en entrée. Convertir `isActive[i]` en un booléen (`isActive[i]] == "vrai"`). Autres
Regex `[A-Za-z0-9_]+` rejettera les espaces, mais parfois les gens coupent d'abord. Aucune garniture requise par les spécifications. Autres

---

### 4.6 Solution de code propre – Pourquoi cela semble bon

1. **Responsabilité unique** – `validerCoupons` fait *exactement* ce que son nom dit.
2. ** Carte de commande immuable** – `Map.of(...)` ou `static constexpr` garde la priorité constante et sûre.
3. ** Expression régulière** – Une seule ligne (`^[A-Za-z0-9_]+$`) encapsule toute la logique de validation du code.
4. **Comparateur moderne** – Javas lambda + `thenComparing` se lit comme une exigence commerciale.
5. **Conteneur minimal** – La classe intérieure `Coupon` ne contient que les données nécessaires au tri.
6. **Préaffectation** – `result.reserve(valid.size())' évite les réaffectations inutiles dans C++/Java.

> **Interview Tip** – Lorsqu'on m'a interrogé sur ce problème, dites : *=J'ai utilisé une petite carte de recherche pour la priorité des entreprises et un régex pour le code. Cela me permet de filtrer dans le temps linéaire et ensuite trier dans O(n log n), ce qui est optimal pour les contraintes.

---

### 4.7 Code complet – Copier et coller

> Chaque extrait ci-dessous est compilé sur le dernier JDK 17 / CPython 3.10 / GCC 12.

Code de la langue
C'est quoi, ça ?
Autres **Java** Afficher <\sommary>``java\nimport java.util.*;\n\npublic class Solution {\n private static final Map<String, Integer> ORDER = Map.of(\n \"electronics\", 0,\n \"grocery\", 1,\n \"pharmacy\", 2,\n \"restaurant\", 3\n );\n\n public List<String> ValidCoupons(String[] code, String[] businessLine, boolean[] isActive) {\n list<Coupon> valide = new ArrayList<>();\n for (int i = 0; i < code.length; i++) {\n if (code[i] ==null=" code[i].isEmpty()) continue;\n if (!code[i].matches(\")^[A-Za-0-9_]+$\") continue(FR. ORDER.get(c.businessLine))\n .thenComparing(c -> c.code));\n List<String> result = new ArrayList<>(valid.size());\n for (Coupon c : valide) result.add(c.code);\n result;\n }\n\n private static class Coupon {\n final String code;\n final String businessLine;\n Coupon(String code, String businessLine) {\n this.code = code;\n this.businessLine = businessLine;\n }\n }\n```n</details> Autres
**Python**= <details><sommaire>Afficher</sommaire>``python\nimport de nouveau\nde taper list\n\nclass Solution:\n ORDONNANCE = {\"électronique\": 0, \"grocery\": 1, \"pharmacy\": 2, \"restaurant\": 3}\n\n def valide Coupons(self, code: List[str], businessLine: List[str], isActive: List[bool]) -> List[str]:\n pattern = re.compile(r'^[A-Za-z0-9_]+$')\n valide = [\n (c, bl) pour c, bl, agir en zip(code, businessLine, estActive)\n si acte et c et pattern.match(c) et bl en soi. ORDONNANCE\n ]\n valid.sort(key=lambda x: (self.ORDER[x[1]], x[0])\n retour [c for c, _ in valid]\n```\n</details> Autres
**C++** Afficher </sommary>``cpp\n#include <bits/stdc++.h>\nusing namespace std;\n\nclass Solution {\npublic:\n vector<string> validantCoupons(vector<string> code, vector<string> businessLine, vector<bool> isActive) {\n unordered_map<string, int> order = {\n {\"electronics\", 0},\n {\"grocery\", 1},\n {\"pharmacy\", 2},\n {\"restaurant\", 3}\n};\n regex pattern(R\"([A-Za-z0-9_]+)\");\n vector<pair<string, string>>> valid;\n for (size_t i = 0; i < code.size(); ++i) {\n if (!isActive[i]) continue;\n if (code[i].vide()=" !regex_match(code[i], pattern)) continue;\n if (!order.count(businessLine[i])) continue;\n valid.emplace_back(code[i], businessLine[i]);\n }\n tri(valid.begin(), valid.end(), [&](const auto &a, const auto &b) {\n int p = order[a.second] - order[b.second];\n if (p != 0) retourner p < 0;\n retourner a.first < b.first;\n });\n vector<string> res;\n res.reserve(valid.size());\n pour (auto &p : valide) res.push_back(p.first);\n retourner res;\n }\n};\n``\n</details> Autres

---

### 4.8 Prise- Liste de contrôle pour les intervieweurs

- **Lire attentivement les spécifications** – chaque règle compte.
- **Utilisez une carte prioritaire** – elle maintient la logique de tri lisible.
**Valider avec un seul regex** – éviter la suringénierie du modèle.
- **Trier avec un comparateur stable** – première clé d'abord, puis deuxième.
- Retourne seulement les données que tu as demandées** – ne fuis pas les objets internes.

N'hésitez pas à coller les extraits spécifiques de la langue dans votre curriculum vitae ou dans la section « Mes solutions » de votre profil GitHub. Quand l'intervieweur demande comment le feriez-vous dans une autre langue?

---

4.9 Pensées de clôture

*Coupon Code Validator* peut se sentir trivial sur le papier, mais c'est un excellent **micro-test** de pratiques de code propres:

- **Parsing & Validation** – montre que vous pouvez écrire et raisonner sur le régex.
- **Mapping et tri** – démontre la familiarité avec les tables de recherche et les comparateurs personnalisés.
- **Edge-Case Awareness** – prouve que vous êtes prudent sur `null`, les chaînes vides et les données invalides.

Donc la prochaine fois que vous êtes dans une entrevue de codage, donnez à ce problème un pouce vers le haut, et quand vous le codez, gardez-le aussi propre que l'extrait ci-dessus. Il impressionnera les gestionnaires d'embauche, marquera des points dans l'entrevue, et sera superbe sur votre CV. Bon codage !