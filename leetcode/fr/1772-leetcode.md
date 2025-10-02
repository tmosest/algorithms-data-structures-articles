---
titre: LeetCode 1772. Trier par Popularité -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 1772 – Caractéristiques de la caisse par popularité
> **Le bon, le mauvais et le laid** de résoudre un problème de fréquence de niveau moyen

> **Mots-clés**: LeetCode 1772, Tri Caractéristiques par Popularité, Java, Python, C++, interview, algorithme, carte de hachage, stable tri, complexité, conseils d'entretien d'emploi

---

Aperçu rapide

Langue Heure Espace Remarques
C'est pas vrai.
*Java*** O(F + R + F log F)* O(F + R)* Utilise `HashMap` + `Arrays.sort` avec un comparateur personnalisé. Autres
**Python**=O(F + R + F log F)=O(F + R)=Utiliser les collections. Compteur` + `trié`. Autres
O(F + R + F log F)= O(F + R)= Utilise `unordered_map` + `sort` avec un lambda. Autres

> **F** – nombre de caractéristiques ( ' , 104 ')
> **R** – nombre de réponses ( < < 102 > > , chacune jusqu ' à 103 caractères)

---

Récapitulation des problèmes

Vous avez reçu :

- "caractéristiques" : une série de "mots uniques" (longueur ≤ 10).
- `réponses`: une série de phrases, chaque mot séparé par un seul espace.

**Popularité** d'une fonctionnalité = nombre de réponses qui contiennent la fonctionnalité ** au moins une fois**.

Triez le tableau des « caractéristiques » dans l'ordre de popularité **non croissant**.
Si deux caractéristiques s'attachent, gardez la commande originale (stable tri).

---

Ce qui fait ce problème

1. **Déduplication par réponse** – une seule réponse peut mentionner une fonctionnalité plusieurs fois, mais elle ne doit compter qu'une seule fois.
2. **Ordre stable** – vous ne pouvez pas simplement trier par fréquence; les liens doivent respecter l'index original.
3. ** Grande taille d'entrée** – jusqu'à 104 fonctionnalités, donc une approche O(F2) serait temps-out.

---

Une idée de solution

1. **Carte de fréquence** – stocker un nombre pour chaque fonction.
Utilisez un `HashMap<String,Integer>` (Java), `unordered_map<string,int>` (C++), ou `Counter` (Python).

2. **Procéder à chaque réponse**
* Se diviser en mots.
* Mettez les mots dans un `HashSet` / `unordered_set` / `set` pour ne garder que des mots uniques.
* Pour chaque mot unique qui existe dans le jeu de fonctionnalités, augmenter sa fréquence.

3. **Trier**
* En Java: `Arrays.sort(caractères, comparateur)` – comparateur regarde la fréquence de la carte.
* Dans Python: `sorted(features, key=lambda f: (-freq[f], index_map[f])`.
* Dans C++: `std::sort(features.begin(), features.end(), comp)` avec une lambda qui utilise la carte.

Le comparateur conserve automatiquement l'index d'origine pour les liaisons parce que le tableau `caractéristiques` est trié **en place**, et l'ordre d'origine est conservé lorsque les fréquences sont égales (comportement stable du type Java/Python `trié` et C++ `sort` avec une clé stable).

---

Code

- Oui. Java (Java 17)

"Java
Importation de java.util.*;

solution de classe {
public Chaîne[] triCaractéristiques(Caractéristiques de la chaîne[], Réponses de la chaîne[]) {
// 1. Carte des fréquences
Carte<String, entier> freq = nouveau HashMap<>();
pour (String f : caractéristiques) {
(f, 0);
}

// 2. Nombre de comparutions
pour (Réponse en attente : réponses) {
Chaîne[] mots = response.split(");
Set<String> vu = nouveau HashSet<>(Arrays.asList(words));
pour (Score w : vu) {
si (freq.contientKey(w)) {
freq.put(w, freq.get(w) + 1);
}
}
}

// 3. Tri stable par fréquence (descendant)
// Arrays.sort de Java est stable uniquement pour les objets,
// mais en utilisant un comparateur qui maintient l'ordre original fonctionne.
Integer[] idx = nouveau Integer[caractères.longueur];
pour (int i = 0; i < features.longueur; i++) idx[i] = i;

Tableaux.sort(idx, (i, j) -> {
int fi = freq.get(caractéristiques[i]);
int fj = freq.get(caractéristiques[j]);
si (fi != fj) retourner Integer.compare(fj, fi); //
retour Integer.compare(i, j); // ordre original
});

// Construire le résultat
Résultat de la chaîne[] = nouvelle chaîne[caractères.longueur];
pour (int i = 0; i < caractéristiques.longueur; i++) {
résultat[i] = caractéristiques[idx[i]];
}
le résultat du retour;
}
}
«» "

> **Pourquoi cette version Java? * *
> *Utilise `Integer[]` pour une commande stable parce que `Arrays.sort` sur primitive `int[]` n'est pas stable. *
> *Le tableau d'index conserve les indices d'origine pour la rupture d'attache. *

---

### Python 3 (≥ 3.7)

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def sortCaractéristiques(self, features: List[str], responses: List[str]) -> List[str]:
# Carte de fréquence
freq = Counter({f: 0 pour f dans les fonctions})

Nombre d'apparitions par réponse
pour resp en réponse:
mots = resp.split()
pour w dans set(words):
si w en freq:
freq[w] += 1

# Carte d'index originale pour la rupture de cravate
idx = {f: i pour i, f dans le dénombrement (caractéristiques)}

# Tri : d'abord par -freq (desc), puis par index original (asc)
retour trié(caractères, clé=lambda f: (-freq[f], idx[f]))
«» "

> **Pourquoi Python?**
> *Construire dans `Counter` + `sorted` rend le code concis.
> *La lambda donne O(F log F) tri, ce qui est optimal. *

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<string> triCaractéristiques(vecteur<string>& caractéristiques, vector<string>& réponses) {
// Carte des fréquences
non ordonné_map<string, int> freq;
pour (const string& f : features) freq[f] = 0;

// Nombre d'apparitions par réponse
pour (const string & resp : réponses) {
unordered_set<string> vu;
mot chaîne;
istringstream iss(resp);
pendant que (ais >> mot) vu.insert(mot);
pour (cont string& w : vu)
si (freq.find(w) != freq.end()) freq[w] += 1;
}

// Carte originale de l'index
unordered_map<string, int> idx;
pour (int i = 0; i < (int)features.size(); ++i) idx[features[i]] = i;

// Tri avec lambda
tri(features.begin(), features.end(),
[&](chaîne de const&a, chaîne de const&b) {
si (freq[a] != freq[b]) retourne freq[a] > freq[b]; //
retourner idx[a] < idx[b]; // original
});

les fonctions de retour;
}
};
«» "

> **Notes C++**
> *Utilise `istringstream` pour l'extraction de mots et `unordered_set` pour la duplication.
> *Lambda capture les cartes de fréquence et d'index par référence. *

---

Analyse de complexité

Étape Java Python C++
- C'est quoi ?
Construisez la carte freq
Réponses au processus **O(mots totaux)** ≤ O(R × maxLen)
Dédoublement par réponse
Classer **O(F log F)**
**(F + R + F log F)
**L'espace**

> **Pourquoi ne pas utiliser une file d'attente prioritaire* *
> Un min‐heap donnerait aussi O(F log F), mais le type simple stable est plus facile à raisonner et moins sensible aux erreurs dans les paramètres d'entrevue.

---

Pièges communs

Pourquoi ça fait mal ?
- C'est quoi ?
**Compiler des duplicata à travers une réponse**.Si vous venez de diviser et de boucler, vous aurez deux mots à compter qui apparaissent deux fois dans la même phrase. Dupliquer avec un jeu avant d'augmenter. Autres
**Traitement non-stable**="Arrays.sort" sur `int[]` n'est pas stable, de sorte que les ruptures d'attaches peuvent mal mélanger les caractéristiques.=" Utilisez un tableau d'index ou un tableau d'objets pour préserver l'ordre. Autres
**Splitting sur les espaces aveuglément**.Les peines peuvent contenir plusieurs espaces ou des espaces de guidage/traînement. Utiliser `split()` (Python), `istringstream` (C++) ou `String.split(")` (Java). Tous ignorent les espaces consécutifs par défaut. Autres
**Les réponses les plus importantes**=La division de chaque réponse par `String.split()` est O(longueur de la phrase). Acceptable parce que R est petit (''' 102'). Autres
**Contrôles en cas d'accident dans une_carte non ordonnée** Dénombrement du seau de réserve : `unordered_map<string,int> freq; freq.reserve(features.size()*2);`"

---

Conseils d'entrevue

Thème Ce que cherchent les intervieweurs.
Il y a un problème.
**Structures de données**= Utilisation de cartes de hachage / ensembles de hachage pour les recherches O(1). Les trois codes construisent une carte de hachage pour la fréquence et un jeu de hachage pour la déduplication. Autres
**La pensée algorithmique**=Décomposer le problème en comptage + tri.=La séparation claire des étapes dans l'explication. Autres
**Manipulation de cas d'Edge** Le code compte pour tous; `set()`/`unordered_set` garantit un double comptage. Autres
**Connaissance au rendement**La complexité O(F log F) est optimale compte tenu des contraintes. L'analyse du temps et de l'espace est fournie. Autres
**Caractéristiques linguistiques**= Utilisation de bibliothèques intégrées (`Counter`, `unordered_map`, `std::sort`). Montre la familiarité avec les outils standard. Autres

> **Afficher votre processus de pensée* *
> Quand vous êtes demandé de mettre en œuvre ceci, marchez à travers le raisonnement: Pourquoi la duplication ? Pourquoi avons-nous besoin d'un tri stable ? Comment garder une trace des indices ? Ce récit impressionne beaucoup plus les intervieweurs que le code final.

---

Les bons

- **Simplicité** – le comptage des fréquences + le tri est simple une fois que vous comprenez les contraintes.
- **Language-agnostic** – la même logique fonctionne en Java, Python, C++ et bien d'autres langues.
- **Stable tri** – les fonctions de tri intégrées préservent naturellement l'ordre d'origine des liens, donc vous n'avez pas besoin d'un passage séparé.

---

Les mauvais

- **Grande taille d'entrée** – tri naïf O(F2) (par exemple, tri de bulles) sera TLE.
- **Coût de la duplication** – créer un `HashSet` par réponse peut être coûteux si les réponses sont longues, mais ici le nombre de réponses est faible, donc il est très bien.
- **Mémoire au-dessus** – stocker tous les mots de toutes les réponses dans un ensemble pourrait doubler l'utilisation de la mémoire si ce n'est prudent; nous ne conservons un ensemble par réponse pour garder l'empreinte de mémoire faible.

---

Les affreux

- **Utiliser un tri non-stable avec un simple comparateur* *
*En Java, `Arrays.sort` sur les types primitifs est **pas** stable, vous devez donc gérer les indices vous-même (comme dans le code ci-dessus). *

- **Musiciper au moins une fois* *
*De nombreux candidats comptent les mentions totales, et non les réponses uniques. *
*Cela conduit à de mauvaises réponses sur les cas de test comme:*
Texte
caractéristiques = ["alpha", "bêta"]
réponses = ["alpha alpha beta", "bêta beta"]
«» "
*Valeur correcte: alpha = 1, bêta = 2.*

- **Séparateurs codés à la main**
*En supposant qu'un seul espace peut causer des accidents si l'entrée contient des onglets ou plusieurs espaces. *
*Robust fractionnement avec le régex ou l'extraction du flux est plus sûr. *

---

# # # # Take- Messages d'accueil

1. **Fréquence + déduplication** est un modèle d'entrevue courant.
2. **Conservez les indices d'origine** à portée de main pour les types de rupture ou de stabilité.
3. **Utilisez les bibliothèques standard** pour garder le code propre et réduire les bogues.
4. **Analyze complexité tôt** – O(F log F) est le coût minimal pour le tri des « caractéristiques ».

---

Prêt à passer votre prochaine interview

- **Pratique** le problème sur LeetCode; c'est un terrain d'entraînement parfait *fréquence-compte*.
- **Expliquer** l'approche à haute voix; les intervieweurs aiment entendre votre raisonnement.
- **Mention** les cas de bord ( phrases vides, duplicata) – montre l'attention au détail.
- **Parlez des performances** – pourquoi vous avez choisi le tri O(F log F) et pas quelque chose de plus lent.

> **Conseil pro**: En codant, conservez une liste de contrôle mentale :
> 1. Dupliquer par réponse?
> 2. Est-ce que le tri est stable ou est-ce que nous coupons manuellement?
> 3. Avons-nous traité tous les mots qui pourraient ne pas être dans les "caractéristiques"?

Une fois que vous pouvez répondre avec confiance, vous impressionnerez les gestionnaires d'embauche à la recherche de code propre, efficace et fiable.

---

Les pensées finales

LeetCode 1772 peut ressembler à "medium" sur papier, mais il cache des détails subtils qui sont du matériel d'entretien doré. La maîtrise de ce problème démontre :

- **Connaissance forte des structures de données** (cartes hash, ensembles).
- **Une clarté algorithmique** (déduplication, tri stable).
- **Connaissance de la qualité du code** (lecture, manipulation des cas de bord).

Montrez-le dans votre portfolio ou GitHub – c'est une victoire rapide pour votre prochain entretien de codage! Joyeux codage.