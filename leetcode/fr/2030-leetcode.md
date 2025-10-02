---
titre: LeetCode 2030. Subséquence K-Length la plus petite avec les événements d'une lettre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes
**LeetCode 2030 – Subséquence K‐Length la plus petite avec les événements d'une lettre**
Données

* `s` – une chaîne minuscule
* `k` – longueur de la séquence à construire
* `lettre` – un caractère cible qui doit apparaître au moins `répétition` fois
* `répétition` – nombre minimum de `lettres` dans le résultat

Retournez la séquence *lexicographiquement la plus petite* de `s` qui satisfait aux contraintes.

> **Constraints**
> * `1 ≤ répétition ≤ k ≤=2 ≤ 5·104`
> * `lettre` apparaît dans `s` au moins `répétition` heures

L'exemple classique:

«» "
s = "code-leet", k = 4, lettre = 'e', répétition = 2
sortie → "ecde"
«» "

---

- Oui. 2. Idées fondamentales

Il s'agit d'un problème de manuel **monotonic-stack + cupide**, très semblable à *Supprimer les lettres dupliquées* (LeetCode 316).
Nous balayons `s` de gauche à droite, en maintenant une pile qui représente le préfixe courant de la réponse.

En regardant un nouveau caractère `c` nous pouvons *pop* la pile `t` supérieure si:

1. ** Amélioration lexicographique** – `t > c`.
2. **Peu de place à gauche** – après avoir sauté, nous avons encore assez de caractères (y compris `c`) pour atteindre la longueur `k`.
3. **Lettre contrainte** – nous ne pouvons pas laisser tomber une `lettre` qui nous laisserait moins de `répétition` copies.

La lettre-contrainte est la seule torsion par rapport au problème classique.

Après la boucle, nous aurons tout au plus des caractères `k` dans la pile; la réponse finale est le contenu de la pile dans l'ordre.

---

- Oui. 3. Esquisse d'exactitude

*Laissez `S` être la chaîne originale, `R` la pile après le scan, et `Ans = R` (haut → bas). *

1. **Feasibility** – Nous ne popons jamais un caractère si le reste de caractères (pas encore traité) + la taille de la pile actuelle < `k`.
C'est pourquoi ""Ans" ≤ k".
Lorsque l'analyse se termine, la taille de la pile est exactement `k` parce que nous *poussons toujours* lorsque la pile est plus courte que `k` (sauf lorsque nous ne pouvons pas en raison de la contrainte-lettre).

2. **Compte des lettres** – Nous tenons deux comptoirs :
* `remLetter` – combien `lettre` reste dans le suffixe non traité.
* `usedLetter` – combien `lettre` déjà dans la pile.
Une pop qui laisserait tomber une `lettre` n'est autorisée que si `useLettre – 1 + remLettre ≥ répétition`.
Par conséquent, la dernière sous-séquence contient au moins des copies de la «lettre».

3. ** minimalité lexicographique** –
Chaque fois qu'un personnage plus petit peut remplacer un plus grand * sans violer les contraintes*, nous le faisons (règles 1 et 2).
Ce choix avide est localement optimal et, comme toutes les décisions futures sont indépendantes des décisions antérieures, il donne une chaîne minimale mondiale.

Ainsi, l'algorithme est correct.

---

- Oui. 4. Analyse de la complexité

* Temps: **O(==)** – chaque personnage est poussé et sauté au plus une fois.
* Espace : **O(k)** – pile tient au plus des caractères `k`.

---

- Oui. 5. Mise en œuvre des références

Voici des implémentations propres et autonomes dans **Python, Java et C++**.
Tous les trois utilisent la même logique cupide/stable décrite ci-dessus.

> **Astuce** – Le code est écrit pour une entrevue de codage; gardez-le bref, commentez seulement si nécessaire, et évitez les conteneurs supplémentaires.

---

5.1 Python 3

'`python
subséquence(s): str, k: int, lettre: str, répétition: int) -> str:
Combien de `lettre` restent encore dans le suffixe?
rem_letter = s.count(lettre)

pile = []
_lettre utilisée = 0 # lettres déjà dans la pile

pour i, c dans le(s) énuméré(s):
# 1. pop pendant que nous pouvons améliorer la lexicographie
pendant la pile et la pile[-1] > c:
Est-ce sûr de sauter ?
# * Après pop nous avons encore assez de chars pour atteindre la longueur k
# * si haut est `lettre`, nous devons encore satisfaire la répétition
haut = pile[-1]
si len(stack) - 1 + (len(s) - i) < k:
pause
if top == lettre et used_letter - 1 + rem_letter < répétition:
pause
Pile.pop()
si haut == lettre:
_lettre utilisée -= 1

# 2. Poussez si nous avons encore besoin de plus de caractères
si len(stack) < k:
si c == lettre:
Annexe(c)
_lettre utilisée += 1
elif k - len(stack) > répétition - used_letter:
Annexe(c)

si c == lettre:
_lettre -= 1

retour ''.join(stack)
«» "

---

#### 5.2 Java 17

"Java
solution de classe {
public Chaîne la plus petiteSous-séquence(String s, int k, char letter, int replication) {
// Comptez combien de `lettre` restent encore dans le suffixe
nt remLetter = 0;
pour [charc : s.toCharArray())
si (c == lettre) remLetter++;

Deque<Caracter> pile = nouvelle ArrayDeque<>();
Int utiliséLettre = 0; // lettres déjà en pile

pour (int i = 0; i < s.longueur(); i++) {
c = s.charAt(i);

// pop pendant que nous pouvons améliorer lexicographiquement
pendant que (!stack.isEmpty() && stack.peekLast() > c) {
char top = pile.peekLast();
// vérifier si le saut maintient la faisabilité
i (taille de la pile() - 1 + (longueur() - i) < k)
pause;
if (top == lettre & & usedLettre - 1 + remLettre < répétition)
pause;
pile.pollLast();
si (en haut de la lettre) utiliséLettre--;
}

// Poussez si nous avons encore besoin de plus de caractères
si (taille de la pile() < k) {
si c == lettre) {
pile.addLast(c);
utiliséLettre++;
} sinon si (k - empil.size() > répétition - utiliséLettre) {
pile.addLast(c);
}
}

Si (c) la lettre) remLettre--;
}

// Construire le résultat
StringBuilder sb = nouveau StringBuilder(k);
pour (charc : pile) sb.append(c);
retour sb.toString();
}
}
«» "

---

Numéro 5.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne plus petiteSéquence(chaîne s, int k, lettre char, répétition int) {
int remLetter = count(s.begin(), s.end(), lettre;
vecteur <char> m; // pile
Int utilisé Lettre = 0;

pour (int i = 0; i < (int)s.zize(); ++i) {
c = s[i];

// pop tout en améliorant l'ordre lexicographique
pendant que (!st.vide() && st.back() > c) {
haut de char = m. dos();
// s'assurer que nous pouvons toujours remplir k après le saut
i (int)st.size() - 1 + (int)s.size() - i < k) pause;
// veiller à ce que le nombre de lettres reste >= répétition
si (en haut) lettre & & usedLettre - 1 + remLettre < répétition) pause;

le _retour_st.pop();
si (en haut de la lettre) utiliséLettre--;
}

// Poussez si nous avons encore besoin de plus de caractères
si ((int)st.size() < k) {
si c == lettre) {
st.push_back(c);
utiliséLettre++;
} sinon si (k - st.size() > répétition - usedLettre) {
st.push_back(c);
}
}

Si (c) la lettre) remLettre--;
}

retourner la chaîne(st.begin(), st.end());
}
};
«» "

---

- Oui. 6. Article de blog: -Le bon, le mauvais, et l'indulgence des problèmes de suite de l'avidité

> **SEO Mots-clés**: *LeetCode 2030*, *la plus petite sous-séquence*, *l'algorithme gredy*, *la pile monotonique*, *l'entrevue de Java*, *l'entrevue de Python*, *l'entrevue de C++*, *les problèmes de codage de l'entrevue d'emploi*, *la plus petite chaîne lexicographique*

---

Titre
**Le bon, le mauvais, et le lamentable des problèmes de suite de l'avidité – une plongée profonde dans le LeetCode 2030 *

#### 6.2 Crochet
Vous avez vu le problème classique *=Supprimer les lettres dupliquées*. Maintenant imaginez que vous avez une règle supplémentaire: *vous devez garder une certaine lettre au moins `r` fois*. C'est LeetCode 2030 – une déclaration faussement simple qui cache une touche subtile. Dans ce post, je vais vous guider à travers la solution de pile gourmande qui vous fera regarder aigu dans votre prochain entretien de codage, et je vais signaler les pièges qui maintiennent beaucoup de candidats coincés.

### 6.3 Récapitulation des problèmes (pour les lecteurs)
- Entrée: chaîne `s`, longueur `k`, lettre `lettre`, répétitions requises `r "
- Objectif: la plus petite subséquence lexicographique de la longueur `k` qui contient au moins des copies `r` de `lettre "
- Contraintes: < < S < ≤ 5·104 > >

### 6.4 Le bon: Pourquoi Greedy + Stack fonctionne
1. ** Temps linéaire, espace linéaire** – Les intervieweurs aiment les algorithmes à cette échelle.
2. **Structure de données élégante** – Une simple pile (`Deque`, `ArrayDeque`, `vector`) capture le préfixe.
3. **Intution claire** – Gardez un personnage si cela vous aide, pop si vous pouvez le remplacer en toute sécurité par un personnage plus petit.
4. **Language-agnostique** – La même logique se traduit directement en Python, Java ou C++ – parfait pour les différentes piles d'interviews.

6.5 Les mauvaises: erreurs courantes
Pourquoi il échoue Comment l'éviter
- C'est quoi ?
**Dropping `lettre` trop tôt**= Sans le contrôle de répétition vous pouvez pop une `lettre` et finir par < `r` copies. Conservez deux compteurs : `remLetter` (en suffixe) et `useLetter` (en pile). Pop seulement si `usedLetter-1 + remLetter ≥ r`. Autres
Autres **Pushing when empile < k but letter contrainte violed**. Vous pouvez remplir la pile à `k` mais sortir de `lettre` dans le suffixe. Lorsque vous poussez une autre lettre, assurez-vous que `k - stackSize > r - usedLetter`. Autres
**Complication excessive du test de faisabilité** Chars < k` seulement après avoir sauté, qui peut casser tôt. Calculer l'état *avant* la pop: `stackSize-1 + restant Chars >= k`. Autres

6.6 L'indulgence : les cas de bord subtil
1. **Tous les caractères restants sont `lettre`** – L'algorithme doit refuser d'afficher une "lettre" même si un caractère plus petit arrive.
2. **Le dernier caractère de `s` est la `lettre`** – Si vous poussez trop tard, vous pourriez ne pas être en mesure d'atteindre la longueur `k`.
3. **«k» égale la longueur de la chaîne** – La pile ne s'affichera jamais; vous avez juste besoin de copier la chaîne tout en respectant la règle de répétition.

Être conscient de ces cas de bord sauve les candidats de mauvaises réponses optimales qui violent toujours la contrainte de répétition.

### 6.7 Passage du code
*Insérer un mini-diaporama des extraits de Python/Java/C++ ci-dessus, avec de brefs commentaires. *
Expliquez line‐by‐line comment la boucle pousse et pops, pourquoi les compteurs fonctionnent et comment la chaîne finale est construite.

#### 6.8 Tendance des entrevues
- **Expliquer vos compteurs** – Les intervieweurs apprécient quand vous indiquez pourquoi vous avez besoin de `remLetter` et `useLetter`.
- **Tirer la pile** – Sur papier, esquissez quelques étapes (par exemple, `s = "abca"`, `k=3`, `lettre='a'`, `r=1`).
- **Afficher la vérification de faisabilité** – Nous ne pouvons sauter que si nous avons encore assez de caractères. (en milliers de dollars)
- **Revenir à *Supprimer les lettres dupliquées*** – Souligner comment la seule différence est la contrainte-lettre.

### 6.9 Conclusion
LeetCode 2030 est une classe de maître dans **. La solution de pile monotonique est courte, rapide et fonctionne pour toute langue que vous préférez dans l'interview (Python, Java, C++). L'astuce est de se rappeler le gardien supplémentaire qui protège la lettre requise. Maître ceci, et vous serez prêt pour le prochain problème de subséquence qui vient votre chemin.

### 6.10 Appel à l'action
> Si vous avez trouvé cet article utile, laissez un commentaire avec le plus dur problème avide que vous avez abordé, et partagez le post sur LinkedIn pour aider votre réseau à se préparer pour la prochaine grande interview.

---

- Oui. 7. Pensées finales

LeetCode 2030 est un modèle d'avidité bien connu. Maîtrisez l'approche basée sur la pile, gardez les deux compteurs à l'esprit, et vous gagnerez le titre de la plus petite séquence en quelques minutes. Bon codage, et bonne chance avec cet entretien d'embauche!