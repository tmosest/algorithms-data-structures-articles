---
Titre: LeetCode 2381. Lettres tournantes II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2381 – *Shifting Letters II* : une solution à pile complète (Java-Python)
> **Le bon, le mauvais, et le laid – et comment faire face à ce problème dans un entretien d'embauche* *

---

Récapitulation des problèmes (facile → moyenne)

> ** Lettres postales II**
> Compte tenu d'une chaîne inférieure `s` et d'un tableau 2-D `shifts`, chaque entrée `[start, fin, dir]` représente une mise à jour de portée:
> - `dir = 1` → déplacer chaque lettre dans `s[départ ... fin]` **avant** (`a → b`, `z → a`).
> - `dir = 0` → déplacer chaque lettre dans `s[départ ... fin]` ** retour** (`a → z`, `b → a`).
> Retourne la chaîne finale après toutes les opérations.

**Contrôles* *

C'est vrai.
C'est le cas.
"1 ≤ s.longueur ≤ 5·104". Autres
"direction "" {0,1} "s" ne contient que des lettres minuscules

---

Pourquoi Ce problème est un *Goldmine* pour les entrevues

1. **Mise à jour de la gamme + requête de points** – cas d'utilisation classique pour les tableaux de différence / préfixe des sommes.
2. ** Manipulation de la chaîne + arithmétique modulo** – teste la compréhension de bas niveau de l'ASCII/Unicode.
3. **Efficacité dans le temps** – Le « O(n · m) » naïf est trop lent; le « O(n+m) » optimal est attendu.
4. **Language-agnostic** – peut être résolu dans n'importe quel langage populaire; montre que vous connaissez les structures de données indépendamment de la syntaxe.

---

Intuition : de -Appliquer chaque quart -Appliquer tous les quarts à une fois

Imaginez que vous deviez traiter les mises à jour de 50 k sur une chaîne de 50 k – l'application de chaque shift un par un serait ~2,5 milliards de changements de caractère, bien trop lents.
L'astuce : **enregistrer l'effet net pour chaque indice en un seul passage**.

1. **Tableau de différence** – stocker la différence* entre les indices consécutifs.
2. **Préfixer la somme** – transformer le tableau de différence en décalage net réel pour chaque caractère.
3. **Appliquez le décalage net** – enroulez l'alphabet avec le module 26.

Il s'agit d'un problème de mise à jour du manuel *range, question de point*.

---

Algorithme pas à pas

Description du code Autres
- C'est quoi ?
Autres Créer un tableau `diff` de la taille `n+1` (tous les zéros). `int[] diff = nouvelle int[n+1];` Autres
Autres Pour chaque «[l, r, dir]»:
  • `shift = dir == 1 ? +1 : -1`
  • `diff[l] += Déplacement "
  • `diff[r+1] -= quart`= `diff[l] += quart; diff[r+1] -= quart;`=
Autres Calculer la somme du préfixe → `net[i]` (déplacement cumulatif jusqu'à l'index `i`).
Autres Pour chaque caractère `c` à la position `i`:
  `shiftVal = ((net[i] % 26) + 26) % 26` (assure la positivité)
«c» = (char)(a) + (c - «a» + posteVal) % 26)
Autres Rejoindre tous les caractères modifiés → chaîne finale. "return new StringBuilder(...).toString();" Autres

**Pourquoi modulo 26?**
Le déplacement vers l ' avant par `+k` ou vers l ' arrière par `-k` équivaut à `+k mod 26`.
Ajouter 26 avant `% 26` garantit que le résultat reste non négatif.

---

Mise en œuvre du code

Voici des solutions idiomatiques propres pour **Java**, **Python** et **C++**.
Tous fonctionnent dans **O(n + m)** temps et **O(n)** espace supplémentaire.

> **Conseil** – Dans les entrevues, demandez si vous avez besoin de gérer un nombre extrêmement élevé de postes (p. ex. > 106). Il suffit d'utiliser un accumulateur "long" pour éviter les débordements.

---

### Java (Java 17+)

"Java
solution de classe {
public Chaîne de changementLettres(String s, int[][] postes) {
int n = s.longueur();
int[] diff = nouveau int[n + 1]; tableau de différence //

// 1. Appliquer toutes les mises à jour de la gamme
pour (int[] op : postes) {
int l = op[0], r = op[1];
int dir = op[2];
int delta = dir == 1 ? 1 : -1; // +1 pour l'avant, -1 pour l'arrière
diff[l] += delta;
[r + 1] -= delta;
}

// 2. Préfixer la somme + appliquer des quarts à chaque caractère
StringBuilder sb = nouveau StringBuilder(n);
Int cur = 0;
pour (int i = 0; i < n; i++) {
cur += diff[i];
changement de cap = ((cur % 26) + 26) % 26; // assurer [0,25]
base de char = s.charAt(i);
Char newChar = (char) ('a' + (base - 'a' + poste) % 26);
sb.append(nouveauChar);
}
retour sb.toString();
}
}
«» "

---

Python 3

'`python
Solution de classe:
def deplacementLetters(self, s: str, deplacements: List[List[int]]) -> str:
n = len(s)
diff = [0] * (n + 1)

# Mises à jour de la gamme
pour l, r, dir en équipes:
delta = 1 si dir autre -1
diff[l] += delta
[r + 1] -= delta

# Préfixer la somme + appliquer les quarts
pour = 0
res = []
pour i, ch dans le(s) énuméré(s):
pour += diff[i]
shift = cur % 26 # Python gère bien les négatifs
new_ch = chr((ord(ch) - 97 + poste) % 26 + 97)
res.append(new_ch)
retourner "".join(res)
«» "

---

### C++ (C++17)

'`cpp
solution de classe {
public:
changement de chaîneLettres(chaîne s, vecteur<vector<int>>&shifts) {
int n = s.size();
vecteur<int> diff(n + 1, 0);

// 1. Mises à jour de la gamme
pour (auto &op : équipes) {
int l = op[0], r = op[1], dir = op[2];
int delta = dir ? 1 : -1; // +1 en avant, -1 en arrière
diff[l] += delta;
[r + 1] -= delta;
}

// 2. Préfixe somme + appliquer
le résultat de la chaîne;
le nom de l'autorité compétente;
Int cur = 0;
pour (int i = 0; i < n; ++i) {
cur += diff[i];
int shift = ((cur % 26) + 26) % 26; // normalisé à [0,25]
Char newChar = 'a' + (s[i] - 'a' + poste) % 26;
result.push_back(newChar);
}
le résultat du retour;
}
};
«» "

---

Analyse de complexité

Heure Espace supplémentaire
C'est quoi ?
**Toutes les 3 solutions**=1 `O(n + m)` (perçage linéaire sur chaîne + mises à jour)=1 `O(n)` (tableau de différence + tampon de résultat)=1
**Magnitude de déplacement du plus mauvais cas**

**Pourquoi `O(n+m)` suffit-il? **
- Chaque mise à jour touche deux positions dans `diff` → `O(m)`.
- Un balayage sur `s` pour construire des montants préfixes et des caractères mutés → `O(n)`.

---

Une plongée profonde

Aspect du bien
- C'est quoi ?
**Concept**=Supprimer la séparation entre *mise à jour* et *query* → tableau de différence. Les élèves oublient souvent d'ajouter la sentinelle `+1` (`diff[r+1] -= delta`). Le fait de ne pas normaliser les valeurs modulo négatives peut produire des sous-flux "char" (par exemple, "-1 % 26 = -1" dans certaines langues). Autres
**Mise en œuvre**=Sum préfixe unique + simple `StringBuilder` / `StringBuilder`.= L'utilisation de `ArrayList<Intégre>` ou `int[]` de mauvaise taille peut causer `ArrayIndexOutOfBoundsException`.= Le sur-optimisation avec des astuces bitwise (`+26) % 26`) peut nuire à la lisibilité. Autres
**Cas d'Edge**Le Modulo 26 assure l'enroulement de tout poste. Dans Python, oublier de convertir "shift % 26" en positif peut encore fonctionner, mais la clarté est perdue. Autres
**La lisibilité est claire. Utiliser `cur` comme un total courant est très bien; éviter de confondre les noms de variables comme `sum` (mot clé réservé dans C++). Autres
**Tests**=Créer des tests avec des déplacements alternés vers l'avant et vers l'arrière pour assurer l'enroulement. Cochez `s="az"`, selfs=[[0,1]] → `"yz"`. Autres

---

Liste de contrôle de l'entrevue

Question Explication
- C'est quoi ?
Vous connaissez la technique du tableau de différence ? Afficher vous pouvez transformer un problème de mise à jour de gamme en une solution linéaire. Autres
Pourquoi utiliser le modulo 26 ? Démontre la compréhension des alphabets cycliques. Autres
Et le débordement ? Les montants de déplacement peuvent-ils être énormes? Discutez en utilisant `long` ou `BigInteger` si nécessaire. Autres
Comment modifier cela pour une seule direction de déplacement ? Parler de sommes partielles par rapport à des sommes cumulatives. Autres
Et si nous devions interroger la chaîne après chaque quart de travail ? Range update, point request vs. prefix sum; mentionnez l'arborescence Fenwick pour les mises à jour dynamiques. Autres

---

Bonus : Étendre l'idée

- **Généraliser les alphabets arbitraires** – remplacer "26" par "ALPHA".
- **Cas de test multiples** – envelopper toute la logique dans une boucle et réutiliser le tableau `diff`.
- **Streaming input** – dans une vraie interview, vous pouvez diffuser la chaîne et appliquer la somme du préfixe à la volée pour garder l'utilisation de la mémoire minimale.

---

## Le départ

- **Good**: Le tableau des différences est *intuitif*, *fast* et *langue-agnostique*.
- **Bad**: Une solution "O(n·m)" naïve est tentante mais vous fera coller sur les limites de temps.
- **Ugly**: Oublier de normaliser les valeurs de modulo négatives est un piège commun qui plante votre code en Java/C++.

Maîtrisez ce modèle, et vous gagnerez des points pour **réflexion efficace** et **implémentation propre** – deux qualités que tout embaucheur aime.

---

Comment l'utiliser dans votre prochaine entrevue

1. ** Expliquez le problème** dans vos propres mots (ordre de mise à jour + requête point).
2. **Afficher l'astuce de la différence** sur un tableau blanc avant le codage.
3. **Demander des éclaircissements** (par exemple, la chaîne est-elle garantie d'être petite? – montre une écoute active.
4. **Écrire le code propre** avec les commentaires (comme ci-dessus).
5. **Discuse la complexité** explicitement.
6. **Enveloppez** avec un exemple de test rapide pour démontrer l'exactitude.

---

Mot final

LeetCode 2381 est plus qu'un puzzle de changement de chaîne – c'est un micro-leçon dans la manipulation efficace des données**.
Implémentez-le en Java, Python et C++, présentez clairement l'algorithme, et vous serez prêt à impressionner les gestionnaires de recrutement chez les géants de la technologie, les startups, ou votre prochaine interview de codage.

> **Rappelez-vous :** La clé est *=Enregistrez les différences, puis additionnez-les*. Une fois que vous internalisez cela, le même état d'esprit résout un vaste éventail de questions d'entrevue (mises à jour de gamme, problèmes d'intervalle, sommes cumulatives, etc.).

Bon codage – et que votre prochaine interview se déroule en douceur !