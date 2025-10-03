---
titre: LeetCode 45. Jeu de saut II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La solution "Go-Fast" (Java)
*LeetCode #45 – Moyen*

> Je ne peux pas finir l'interview ? Commencez par l'idée gourmande qui garantit les plus petits sauts! (en milliers de dollars)

Ci-dessous vous trouverez trois solutions polies, prêtes à la production – Java, Python et C++ – qui partagent toutes la même logique gourmande.
Je vais aussi déposer un court **blog post** (friendly SEO, job-chunting-oriented) que vous pouvez copier-coller dans Medium, Dev.to, ou votre propre blog.

---

- Oui. 1. Récapitulation des problèmes

Vous êtes donné un tableau `nums` où chaque élément `nums[i]` est le nombre maximum d'étapes que vous pouvez sauter *forward* de l'index `i`.
Démarrer à l'index "0". Trouvez le nombre minimum de sauts requis pour atteindre le dernier indice (`n‐1`).
L'entrée garantit qu'elle est toujours possible.

«» "
nombres = [2,3,1,1,4] → réponse = 2
^ ^ ^ ^ ^ ^
0 1 2 3 4
«» "

---

- Oui. 2. Regard sur l'avidité – près et loin

L'observation clé :
**Alors que vous êtes des indices de numérisation que vous pouvez atteindre en sauts *k*, vous devez seulement connaître l'index le plus éloigné que vous pouvez atteindre en sauts *k+1*. **

Vous n'avez pas à explorer tous les sauts possibles séparément – il suffit de garder la portée *current* (`far`) et la prochaine portée* (`farthest`).

> ** Près** – le début de la fenêtre actuelle des indices que vous considérez.
> **Far** – la fin de cette fenêtre.
> **Farthest** – l'index le plus éloigné que vous pouvez obtenir de n'importe où dans `[près, loin]`.

Chaque fois que vous faites un saut, vous déplacez la fenêtre vers `[far+1, le plus lointain]`.

---

- Oui. 3. Code – 3 langues

#### 3.1 Java (Java 17+)

"Java
// - Oui. SauterGameII.java -----------------
Importation de java.util.*;

classe publique Jeu de saut {
public statique int jump(int[] nums) {
int n = longueur nums;
si (n <= 1) retourner 0; // déjà à la fin

sauts int = 0;
int proche = 0; // début de la fenêtre actuelle
int far = 0; // fin de la fenêtre actuelle
int farthest = 0; // index le plus accessible

pendant la période (de loin < n - 1) {
// Scanner tous les indices que nous pouvons atteindre avec le nombre actuel de sauts
pour (int i = proche; i <= loin; i++) {
la plus éloignée = Math.max(la plus éloignée, i + nombres[i]);
}

// Préparez-vous au prochain saut
proche = loin + 1;
loin = plus loin;
sauts++;
}

les sauts de retour;
}

// -------------------------------------------------
public statique vide principal(String[] args) {
nombres int[] = {2, 3, 1, 1, 4};
System.out.println("Jumps minimums: " +jump(nums)); // → 2
}
}
«» "

> **Complexité** – temps O(n), espace supplémentaire O(1).

---

3.2 Python 3

'`python
C'est... saut_jeu_ii.py -----------------
def jump(nums):
n = len(nums)
si n <= 1:
retour 0

sauts, près, loin, plus loin = 0, 0, 0, 0

alors que loin < n - 1:
pour i dans la plage (près, loin + 1):
Plus loin = max (plus loin, i + nombres[i])

proche = loin + 1
loin = plus loin
sauts += 1

sauts de retour

♪ -------------------------------------------------
si __nom__ == "__main__" :
nombres = [2, 3, 1, 1, 4]
print(f"Jumps minimum: {jump(nums)}") # → 2
«» "

> **Complexité** – temps O(n), espace supplémentaire O(1).

---

### 3.3 C++ (C++17)

'`cpp
// - Oui. SauterGameII.cpp -----------------
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

int jump(vecteur const<int>& nums) {
int n = nombres.size();
si (n <= 1) retourner 0;

sauts int = 0;
Int proche = 0, loin = 0, plus loin = 0;

pendant la période (de loin < n - 1) {
pour (int i = proche; i <= loin; ++i) {
la plus éloignée = max (la plus éloignée, i + nombres[i]);
}
proche = loin + 1;
loin = plus loin;
+ jumps;
}
les sauts de retour;
}

// -------------------------------------------------
Int main() {
vectorielle<int> nombres = {2, 3, 1, 1, 4};
Cout << "Jumps mineurs: " <<jump(nums) << '\n'; // → 2
retour 0;
}
«» "

> **Complexité** – temps O(n), espace O(1).

---

- Oui. 4. Billet de blog – Le bon, le mauvais, et le lamentable du jeu de saut II

> ** Auditoire cible** : développeurs de front-end / full-stack qui veulent avoir des entrevues techniques.
> **Mots-clés du référencement**: Jump Game II, LeetCode 45, problème de codage d'entretien, algorithme gourmand, solutions d'entretien de codage, Java, Python, C++.

---

Titre
**Jump Game II – Le bon, le mauvais et le mauvais : un guide de 5 minutes pour maîtriser le leetCode 45**

---

Description de la méta
> Crack LeetCode 45 en quelques minutes ! Découvrez la stratégie cupide « Near & Far », comparez les solutions Java/Python/C++ et apprenez pourquoi ce problème est incontournable pour votre prochaine interview de codage.

---

- Oui. 1. TL;DR
Sauter le jeu II est un puzzle d'interview classique qui se résume à un algorithme avide *pass unique*.
- **Bonne**: O(n) temps, O(1) espace – parfait pour les entrevues.
- **Bad**: Pauvres PDD ou tentatives de force brute perdent du temps et la profondeur de la pile.
- **Ugly**: La suringénierie ou les erreurs de vérification des frontières peuvent entraîner des erreurs hors-par-un.

Prenez les extraits de code ci-dessous, choisissez votre langue, et vous êtes prêt à l'entrevue.

---

- Oui. 2. Pourquoi ce problème est-il si populaire?

- ** Facile à dire, difficile à surestimer** – un énoncé de problème propre avec des pièges cachés.
- ** Thème d'entretien commun** – De nombreuses entreprises demandent une variante dans les entretiens sur place.
- **Illustre cupide contre DP** – un grand moment d'enseignement pour les intervieweurs.

---

- Oui. 3. La bonne solution pour l'avidité

L'approche cupide « Near & Far » fonctionne parce que :
1. Tout indice que vous pouvez atteindre en sauts *k* peut seulement améliorer la portée la plus éloignée pour les sauts *k+1*.
2. Vous n'avez jamais besoin de revoir une fenêtre plus tôt – une fois que vous commit un saut, vous avez déjà envisagé toutes les possibilités dans cette fenêtre.

**Étape par étape**
Variable Sens de la mise à jour Règle
- C'est quoi ?
Début de la fenêtre actuelle
Fin de la fenêtre actuelle
"à partir de la fenêtre actuelle" "à partir de la fenêtre actuelle" Autres
Nombre de sauts effectués

> **Heure**: O(n) – nous inspectons chaque index au plus une fois.
> **Espace**: O(1) – seulement une poignée de compteurs entiers.

---

- Oui. 4. Le "Bad" – Ce que vous devriez éviter

Une mauvaise approche
- Oui.
**Brute-Force DFS**.Récursez sur chaque saut possible → O(2n) temps, le risque de débordement de pile. Autres
**Programmation dynamique** (bottom-up)= Fonctionne, mais le temps O(n2) et l'espace O(n) – pas un endroit agréable pour les intervieweurs. Autres
**Bounds entiers non limités**= Utiliser `Integer.MAX_VALUE`/`INT_MAX` puis ajouter aux indices peut déborder. Utilisez une sentinelle comme `farthest = 0` et calculez seulement si nécessaire. Autres

---

- Oui. 5. Les cas de bord et les erreurs courantes

Piège
- Oui.
La boucle doit s'arrêter *après * vous commettez un saut qui vous garantit d'être à ou au-delà du dernier index. Autres
**Off‐by‐one dans la boucle intérieure** (`pour (int i = proche; i <= loin; ++i)`)" Assurez-vous que `far` est inclusive; la fenêtre est `[près, loin]`. Autres
**Les plus grandes valeurs de `nums[i]`**= Pas de débordement en Java/C++ parce que `i + nums[i]` correspond à `int` pour les contraintes de LeetCode. Autres
**Tableau de longueur Retour `0` immédiatement – vous êtes déjà à la cible. Autres

---

- Oui. 6. Les 3 langues – Java, Python, C++

*(Insérer les extraits de code de la section 3.1-3.3. Utilisez des blocs de code avec une syntaxe appropriée.) *

> *Astuce*: Gardez les mêmes noms de variables (`près`, `far`, `farth`, `jumps`).
> *Astuce*: Écrivez un petit `main()`/`__main__` pour tester l'entrée de l'échantillon – qui montre que vous pouvez exécuter la solution localement, un booster de confiance pour l'entrevue.

---

- Oui. 7. Comment parler de ce problème dans une entrevue

1. ** Clarifier la question** : Pouvons-nous sauter *exactement* `k` pas ou au plus `k`? (en milliers de dollars)
2. ** Expliquer la raison d'être cupide** avant d'écrire le code.
3. **Vérifications des limites de concentration**: Et si le tableau a la longueur 1 ? (en milliers de dollars)
4. **Parcourez un exemple simple** sur le tableau blanc (tirez à la main les changements de fenêtre).
5. **Finissez avec le code** – soulignez que vous utilisez O(1) espace et un passage.

---

- Oui. 8. Angle de travail – Pourquoi Ce qui compte

> *Coding interviews ne sont pas juste à propos de la réponse; ils sont sur le récit que vous présentez. *
> - Montrez que vous pouvez penser **greedy** et **efficacement**.
> - Mettre en évidence votre qualité *code* – variables et commentaires concis et bien nommés.
> - Partagez votre solution sur GitHub ou un portfolio ; les recruteurs adorent voir du code propre et commenté.

**Resume Bullet* *
> • Implémenté un algorithme cupide linéaire pour résoudre le LeetCode 45, pour atteindre O(n) runtime et O(1) en Java, Python et C++.

---

- Oui. 9. Dernier départ

*La solution avide Near-Far est un problème parfait pour votre prochain entretien technique. Maîtrisez la logique, possédez le code dans au moins une langue, et vous transformerez un défi de 45 secondes en une victoire d'entrevue de confiance. *

Bonne chance, et que votre prochain recruteur vous voit comme le candidat *fast-moving* qui *jumps* déjà passé la compétition!

---

> * Sentez-vous libre d'adapter les mots-clés SEO ci-dessus dans votre blog. Ajoutez une petite image du diagramme de la fenêtre coulissante, et vous aurez un article à partager que les recruteurs aimeront. *