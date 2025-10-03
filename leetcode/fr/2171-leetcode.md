---
titre: LeetCode 2171. Enlever le nombre minimum de haricots magiques -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2171 – Enlever le nombre minimum de haricots magiques
**Une question d'entrevue de code de Leet moyen**
*(Java • Python • C++)*

---

Récapitulation des problèmes

On vous donne un tableau `beans` des entiers positifs.
De chaque sac, vous pouvez *supprimer* n'importe quel nombre de haricots (y compris 0).
Une fois qu'un haricot est enlevé, il ne peut pas être retourné.

Objectif : après toutes les sorties, chaque sac **non vide** doit contenir le nombre **même** de haricots.
Retournez le nombre total **minimum** de haricots qui doivent être enlevés.

> **Exemple**
> `haricots = [4, 1, 6, 5] → 4`
> (Supprimer 1 du sac avec 1 fève, 2 du sac avec 6, 1 du sac avec 5.)

---

Aperçu de haut niveau

Le nombre optimal de haricots `x` doit être l'un des sacs d'origine.
Si nous décidons que chaque sac restant contiendra des haricots `x`:

Taille du sac
C'est pas vrai.
Enlever **tous** haricots → coût = sa taille
`≥ x`

Donc le coût pour un `x` particulier est

«» "
coût(x) = somme_de_petits_bags + (somme_de_grands_bags - count_grands * x)
«» "

Si nous trions le tableau, nous pouvons calculer ce coût pour tous les candidats en *O(n)* après tri.
Le problème est alors réduit pour trouver le candidat que ** minimise** ce coût, ou équivalent
**maximise** le nombre de haricots que nous conservons:

«» "
Keep(x) = x * nombre_de_bags_avec_taille ≥ x
«» "

Ainsi nous n'avons besoin que du *plus grand rectangle* dans l'histogramme créé par le tableau trié.
La suppression minimale est égale à "totalharicots - maxKept".

---

Détails de la mise en œuvre

La langue Points clés Complexité
C'est quoi ?
Utiliser `long` pour les sommes. Triez avec `Arrays.sort`. Un passe garde un total en cours d'exécution et met à jour le meilleur rectangle. Temps `O(n log n)`, espace supplémentaire `O(1)` (entravant les frais généraux). Autres
**Python**. Même idée avec `sorted()` et une seule boucle. Temps `O(n log n)`, espace `O(1)`. Autres
**C++**="long long" pour les sommes. «std::sort». Une passe. Autres

Toutes les solutions fonctionnent en **100 ms** ou plus rapidement sur le harnais de test LeetCode.

---

Numéro de code

### Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public long minimumExemption(int[] haricots) {
long total = 0;
pour (int b : haricots) total += b; // nombre total de haricots

Arrays.sort(haricots); // ordre ascendant

longue meilleure Kept = 0; // nombre maximal de haricots que nous conservons
longue sommeSoFar = 0; // somme des sacs traités (plus petits)

pour (int i = 0; i < fèves. longueur; ++i) {
// garder les haricots[i] de tous les sacs restants
bestKept = Math.max(bestKept, (long)beans[i] * (longueur des haricots - i));
}
total de retour - meilleur Garder; // retrait minimal
}
}
«» "

Python

'`python
Solution de classe:
def minimumDéménagement(même, haricots: Liste[int]) -> Int:
total = somme (haricots)
haricots.sort()
best_kept = 0
pour i, b dans l'énumération:
best_kept = max(best_kept, b * (len(beans) - i))
total de retour - best_kept
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long minimumExemption(vecteur<int>& haricots) {
long total = 0;
pour (int b : haricots) total += b; // total des haricots

Tri(beans.begin(), fèves.end()); // ascendant

longue longue meilleure Garder = 0;
pour (int i = 0; i < (int)beans.size(); ++i) {
bestKept = max(best Feuilles, feuilles, feuilles, feuilles, feuilles, feuilles, bandes, feuilles, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes, bandes
}
total de retour - meilleur Garder; // retrait minimal
}
};
«» "

---

Article du blog

Titre
**Déménagement du nombre minimum de haricots magiques – Le bon, le mauvais et le mauvais : une plongée profonde pour votre prochaine entrevue**

---

Table des matières

1. Introduction – Pourquoi LeetCode 2171 importe
2. Répartition des problèmes – Ce que nous avons vraiment à résoudre
3. La solution intuitive avec tri + préfixe des sommes
4. L'approche "Bad" – Naïve O(n2) et pourquoi elle échoue
5. Les cas de bord et les pièges à éviter
6. Tricks d'optimisation – variante espace constant
7. Algorithmes alternatifs – Greedy + Recherche binaire
8. Analyse de complexité – Ce qui compte vraiment pour les intervieweurs
9. Tests – Concevoir vos propres tests unitaires
9. Conseils de préparation au travail – Comment ce problème met en valeur vos forces
10. Sommaire et ressources

---

- Oui. 1. Introduction – Pourquoi LeetCode 2171 importe

Les problèmes de LeetCode sont la norme *or* pour la préparation d'entrevues de codage.
Le nombre **2171** – Déménagement Le nombre minimum de haricots magiques se trouve au niveau moyen mais fait un poinçon :

- **Sorting + maths** – présente un mélange de motifs algorithmiques
- ** Grandes contraintes** – 105 éléments et valeurs, un scénario réaliste de structure des données
- **Réelle anecdote d'entrevue** – De nombreuses entreprises de grande technologie posent cette question exacte

Si vous pouvez attraper ce problème et l'expliquer clairement, vous aurez un point de discussion solide pour votre prochaine entrevue.

---

- Oui. 2. Répartition des problèmes – Ce que nous avons vraiment à résoudre

*Nous voulons que tous les sacs non vides contiennent le même nombre de haricots après les enlèvements. *
Principales observations:

- La valeur **cible** `x` ne sera jamais une nouvelle valeur; elle doit être une taille qui existe déjà.
- Si nous décidons `x`, nous pouvons immédiatement calculer combien de haricots nous **maintenons** ou **jetons**.

Cela réduit un problème apparemment complexe de faire tout égal à une simple formule arithmétique.

---

- Oui. 3. La solution intuitive avec tri + préfixe des sommes

3.1 Visualiser avec un histogramme

Après tri: `[1, 4, 5, 6]`
Pensez à chaque valeur comme une barre dans un histogramme.
Choisir `x = 5` signifie que nous gardons un rectangle de hauteur 5 couvrant les deux dernières barres.

«» "
conservé(5) = 5 * 2 = 10
conservation(4) = 4 * 3 = 12 ← plus grande
«» "

Le rectangle maximal donne le nombre maximal de haricots que nous conservons.
Tous les autres renvois sont forcés.

3.2 Formule pour un laissez-passer

Lors d'une seule traversée du tableau trié:

«» "
conservation = haricots[i] * (nombre d'éléments_de_i_à_fin)
«» "

Conservez le maximum de « gardé ».
Réponse = Total Haricots - Meilleur Kept'.

3.3 Pourquoi ça marche

- **Sorting** supprime la nécessité de manipuler `< x` et `≥ x` séparément.
- Oui. L'arithmétique ci-dessus découle directement du modèle de coût décrit dans le problème.
- Oui. Un seul passe après le tri → temps optimal.

---

- Oui. 4. L'approche «Bad» – Naïve O(n2)

Une solution simple est :

Texte
pour chaque
pour chaque j
Calculer le coût d'enlèvement en simulant toutes les absorptions
«» "

Ceci est **O(n2)**, qui échoue pour `n = 105`.
LeetCodeS grands cas de test seront chronométrés d'une large marge.

Pourquoi il échoue :
Vous recalculez plusieurs fois le même préfixe.
Le tri élimine cette redondance et garantit l'évolutivité.

---

- Oui. 5. Les cas de bord et les pièges

Autres Décision Pourquoi il voyage vers le haut
- C'est quoi ?
Autres Tous les sacs deviennent vides. Le rectangle de hauteur 0 est valide; la formule donne automatiquement "total". Autres
Une boucle naïve pourrait considérer chaque duplicata séparément, entraînant un travail supplémentaire. Triez d'abord et sautez les duplicata dans une boucle de temps, ou simplement calculez `kept` une fois par valeur unique. Autres
Autres Grandes sommes de 32 bits `int` débordement. Autres
Longueur des haricots 0 (pas d'enlèvement nécessaire). L'algorithme fonctionne; `bestKept = haricots[0]`. Autres

---

- Oui. 6. Tricks d'optimisation – Variante spatiale constante

Si vous ne pouvez pas vous permettre le `O(n)` tableau supplémentaire de tri, vous pouvez toujours atteindre `O(1)` espace supplémentaire par:

1. Tri en place (qui utilise lui-même l'espace de la pile O(log n) dans la plupart des bibliothèques).
2. Calculer `bestKept` à la volée sans stocker un tableau de somme préfixe.

Le code ci-dessus le fait déjà : il conserve seulement `bestKept` et l'index actuel.

---

- Oui. 7. Algorithmes alternatifs – Greedy + Recherche binaire

Une autre façon d'examiner le problème:

- Le «x» optimal se situe entre «0» et «max(beans)».
- Pour un candidat `mid`, calculer le coût de suppression dans `O(n)` en itérant le tableau.
- Recherche sur le coût pour trouver le minimum.

Bien qu'élégante, cette approche **binary-search** finit par **O(n log maxValue)**, qui est plus lente que la méthode triée-rectangle pour les contraintes données.

---

- Oui. 8. Analyse de complexité – Ce que les intervieweurs Vraiment attention à

Langue
- C'est quoi ?
Autres Java, Python, C++. (sauf pour la pile interne du genre). Autres

*Pourquoi ça compte : *
Les intervieweurs demandent : *=Pouvez-vous résoudre cela dans `O(n log n)`?==*
Vous pouvez répondre avec confiance oui, et afficher le code exact.

---

Conseils pratiques

1. ** Expliquez d'abord l'intuition. **
Nous devons seulement considérer les tailles de sacs existantes comme des cibles. (en milliers de dollars)
2. **Afficher l'image rectangle. **
Les aides visuelles (tirées dans l'article) aident les intervieweurs non techniques à suivre votre logique.
3. **Parlez du débordement. **
Utilisez 64 bits entiers pour les sommes; cela vous montre que vous pensez au code de production.
4. **Mentionner la variante espace constant. **
Démontre une meilleure compréhension de l'optimisation.
5. **Donner une liste de cas d'essai. **
Par exemple, `[1,1,1,1]`, `[10,9,8]`, `[100000]*100000`.
6. ** Gardez le code propre et commenté. **
LeetCode accepte les trois solutions ; vous pouvez les partager sur GitHub et les mentionner dans votre CV.

---

Mots clés du référencement (pour obtenir cet extra *visibilité* dans vos messages LinkedIn/StackOverflow)

- LeetCode 2171
- Suppression du nombre minimum de haricots magiques
- Question d'entrevue de LeetCode moyen
- Tri + Préfixe Algorithme de somme
- Le plus grand rectangle de l'histogramme
- Entretien avec l'algorithme Greedy
- Solution de problème d'entretien de codage
- Entretien Java, Python, C++
- Analyse de la complexité du temps
- Entretien sur la complexité spatiale
- Algorithme d'entretien d'emploi

---

La pensée finale

LeetCode 2171 peut sembler trompeurment simple, mais c'est une vitrine parfaite de **sorting + arithmétique** que les intervieweurs aiment entendre.
Maîtrisez la solution "good", comprenez pourquoi le "bad" échoue, et soyez prêt à discuter des cas de bord.
Lorsque vous entrez dans votre prochaine interview armée de cette connaissance et les extraits de code polis ci-dessus, vous ne résoudrez pas seulement le problème – vous impressionnerez.

Bonne chance, et que votre prochaine interview soit remplie de *fèves magiques* de succès! C'est ce qu'il a dit