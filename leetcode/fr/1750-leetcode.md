---
titre: LeetCode 1750. Longueur minimale de la chaîne après avoir supprimé des extrémités similaires -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1750. Longueur minimale de la chaîne après la suppression des extrémités similaires
**Difficulté**: Moyen** "c"**Longueur**: ≤ 105

---

TL;DR

"Java
solution de classe {
Int minimum public Longueur(s) {
int l = 0, r = s.longueur() - 1;
alors que (l < r & s.charAt(l) == s.charAt(r)) {
char ch = s.charAt(l);
pendant que (l <= r && s.charAt(l) == ch) l++;
pendant que (l <= r && s.charAt(r) == ch) r--;
}
retour r - l + 1; // peut être 0 si l > r
}
}
«» "

'`python
Solution de classe:
def minimumLength(self, s: str) -> Int:
l, r = 0, len(s) - 1
alors que l < r et s[l] == s[r]:
ch = s[l]
alors que l <= r et s[l] == ch: l += 1
alors que l <= r et s[r] == ch: r -= 1
retour max(r - l + 1, 0)
«» "

'`cpp
solution de classe {
public:
Int minimum Longueur(chaîne s) {
int l = 0, r = (int)s.size() - 1;
alors que (l < r & s[l] == s[r]) {
char ch = s[l];
pendant la période (l <= r && s[l] == ch) ++l;
pendant que (l <= r && s[r] == ch) --r;
}
retour max(r - l + 1, 0);
}
};
«» "

Les trois extraits utilisent tous la stratégie cupide ** à deux points** – temps O(n), espace supplémentaire O(1).

---

- Oui. Pourquoi ce problème est-il une question d'entrevue de grande envergure

**Beau**
C'est quoi ?
**Simplicité** – L'énoncé est court et sans ambiguïté.** **Pièges à clés** – Erreurs hors-par-un lorsque l > r après les suppressions. Autres
**Learning Value** – Teachs bi-pointer technique, raisonnement avide, et l'analyse de cas de bord. Certains supposent que vous pouvez supprimer *toute* fin égale, ignorant que les préfixes/suffixes doivent être contigus et non-overlaping. Autres
**Cross-Language Transfer** – Même logique en Java, Python, C++ (et plus). **Optimalité non claire** – Les élèves peuvent penser que *toute séquence de suppressions fonctionne, ne se révélant pas minimalité. Autres

---

## Algorithme Parcours

1. **Pointeurs**
* `l` – index du caractère le plus à gauche.
* `r` – index du caractère le plus droit.

2. **Alors que `l < r` et `s[l] == s[r]`**
* Tous les caractères de `l` au premier différent sont les mêmes (`ch`).
* Passez le bloc *entire* de `ch` à partir de `l` → `l++` jusqu'à ce qu'un char différent apparaisse.
* Passez le bloc *entire* de `ch` se terminant à `r` → `r--` jusqu'à ce qu'un char différent apparaisse.
* Ceci simule la suppression du préfixe et du suffixe d'égal à égal maximal en une seule étape.

3. **Termination**
* Soit les deux pointeurs croisés (`l > r`) → chaîne entière supprimé → réponse `0`.
* Ou les caractères à `l` et `r` diffèrent → plus de suppressions possibles → réponse `r - l + 1`.

**Pourquoi l'avidité fonctionne**
Si les extrémités correspondent, supprimer *any* non vide bloc égal de chaque côté ne peut pas augmenter la longueur restante. Prendre les blocs maximaux est sûr et ne réduit jamais les options futures. Par conséquent, la stratégie avide donne la longueur restante minimale possible.

---

Analyse de complexité

Valeur métrique
C'est pas vrai.
Temps **O(n)** – chaque caractère est examiné au plus deux fois. Autres
Espace **O(1)** – seulement deux indices et un char temporaire. Autres

---

## Cas de bord et pièges

Autres Décision Quoi regarder?
-- -- -- -- -- -- --
Un seul char → répond `1`. Autres
`"aa"`= La chaîne entière est le même char → réponse `0`. Autres
"""""""""" Les extrémités diffèrent (`a` "" `a`? En fait égal, mais seulement un `a` de chaque côté, puis le bloc du milieu reste) → longueur finale `2`. Autres
La chaîne vide après les suppressions `l > r` → `max(r-l+1,0)` protège de la longueur négative. Autres
Autres L'algorithme fonctionne toujours parce qu'il ne tient qu'à l'égalité des fins actuelles. Autres

---

## Article de blog optimisé du SEO

> **Titre:** Master LeetCode 1750 – Longueur minimale de la chaîne après suppression des extrémités similaires
> **Meta Description:** Apprenez la solution à deux points gourmande pour LeetCode 1750, avec le code Java, Python et C++. Boostez votre préparation d'entrevue et atterrissez votre travail de rêve.
> **Mots clés:** LeetCode 1750, longueur minimale de la chaîne, deux algorithmes pointeurs, préparation d'entrevue, entretien de codage, algorithme gourmand, solution Java, solution Python, solution C++, entretien d'emploi

---

# Article de blog

> **Comment écraser LeetCode 1750 (longueur minimale de la chaîne après avoir supprimé des extrémités similaires)* *
> *Par votre nom – Ingénieur logiciel et coach d'entrevue*

Présentation

Si vous vous préparez à une entrevue de codage dans des entreprises comme Google, Amazon ou Facebook, vous allez rapidement réaliser que de nombreux problèmes de LeetCode de niveau moyen cachent une astuce simple et élégante. L'une de ces pierres précieuses est **LeetCode 1750 – Longueur minimale de la chaîne après avoir supprimé des extrémités similaires**.

Dans ce post, je vais vous guider dans le problème, expliquer pourquoi l'approche cupide à deux pointeurs est optimale, vous montrer nettoyer Java, Python et C++ implémentations, et couvrir les pièges qui voyagent jusqu'à des candidats aguerris. À la fin, vous comprendrez non seulement ce problème, mais aussi comment présenter une solution concise et prête à la production dans une entrevue.

---

## Rétablissement du problème (court et doux)

On vous donne une chaîne `s` composée uniquement de `'a'`, `'b'` et `'c'`.

Vous pouvez à plusieurs reprises **supprimer un préfixe non vide et un suffixe non vide qui contiennent le même caractère et ne se chevauchent pas**.
Votre objectif : ** Minimiser la longueur de la chaîne** après avoir effectué l'opération n'importe quel nombre de fois (y compris zéro).

---

- Oui. Intuition : Pourquoi un balayage à deux points ?

Considérez la chaîne comme une ligne de caractères. L'opération supprime toujours les caractères égaux des extrémités *deux*.
Si les caractères les plus à gauche et les plus à droite sont différents, vous ne pouvez jamais rien supprimer – la réponse est simplement la longueur actuelle.

Quand ils sont identiques, vous avez deux choix :

1. Supprimer le bloc possible le plus petit* (juste le premier caractère de chaque côté).
2. Supprimer le bloc possible *plus grand* (tous les caractères égaux consécutifs de chaque côté).

Pourquoi ne pas choisir le plus grand bloc ? Parce que prendre plus du même caractère des deux extrémités ne peut pas blesser. Il réduit la chaîne plus rapidement et vous laisse avec le même segment du milieu. Par conséquent, **la stratégie optimale est de toujours supprimer le préfixe égal maximal et suffixe**. C'est exactement ce que fait un scan à deux points.

---

## L'algorithme à deux points de l'avidité

1. **Initialiser** deux indices, `l = 0` et `r = s.longueur() - 1'.
2. **Alors que** `l < r` ** et** `s[l] == s[r]`:
* Laisser `ch = s[l]`.
* Advancez `l` pendant `s[l] == ch`.
* Retraite `r` pendant `s[r] == ch`.
3. **Le résultat** est "max(r - l + 1, 0)".
Le `max` gère le cas où `l` dépasse `r` (chaîne entièrement supprimée).

> **Pourquoi est-ce linéaire? **
> Chaque itération de la boucle extérieure déplace au moins un pointeur au-delà d'un bloc de caractères identiques. Puisque la chaîne a au plus des caractères `n`, le travail total est `O(n)`.

---

Code en trois langues

Voici des solutions propres et prêtes à la production en Java, Python et C++. Chacun suit la même logique et a les mêmes garanties temps/espace.

### Java

"Java
solution de classe {
Int minimum public Longueur(s) {
int l = 0, r = s.longueur() - 1;
alors que (l < r & s.charAt(l) == s.charAt(r)) {
char ch = s.charAt(l);
pendant que (l <= r && s.charAt(l) == ch) l++;
pendant que (l <= r && s.charAt(r) == ch) r--;
}
retour r - l + 1; // sera 0 si l > r
}
}
«» "

Python

'`python
Solution de classe:
def minimumLength(self, s: str) -> Int:
l, r = 0, len(s) - 1
alors que l < r et s[l] == s[r]:
ch = s[l]
alors que l <= r et s[l] == Ch:
l += 1
alors que l <= r et s[r] == Ch:
r -= 1
retour max(r - l + 1, 0)
«» "

C++

'`cpp
solution de classe {
public:
Int minimum Longueur(chaîne s) {
int l = 0, r = (int)s.size() - 1;
alors que (l < r & s[l] == s[r]) {
char ch = s[l];
pendant la période (l <= r && s[l] == ch) ++l;
pendant que (l <= r && s[r] == ch) --r;
}
retour max(r - l + 1, 0);
}
};
«» "

---

## Erreurs courantes et comment les éviter

Pourquoi ça arrive ?
- Oui.
**Utiliser des récursions ou des DP**Les candidats pensent que chaque opération est un sous-problème. L'avidité est suffisante; DP ajoute une complexité inutile. Autres
**Oubliant que `l` et `r` peuvent traverser. Retour `max(r - l + 1, 0)` ou vérifier `si (l > r) retour 0;`. Autres
**Supprimer un seul personnage**= Penser=supprimer n'importe quelle extrémité égale= signifie un char chacun. Toujours supprimer le bloc *entire* de caractères égaux. Autres
**Créer des sous-chaînes dans une boucle** Travailler avec des indices seulement. Autres

---

- Oui. Pourquoi ce problème est-il un savoir-faire pour les entrevues

1. **Two-Pointer Mastery** – Un agrafe pour de nombreuses questions d'entrevue (chaîne inversée, contrôles palindrome, fenêtres coulissantes, etc.).
2. **Greedy Insight** – Démontre la capacité de prouver qu'un choix local optimal conduit à une solution globale optimale.
3. **Edge‐Case Sensibility** – Affiche l'attention au détail (chaîne vide, caractère unique, suppression complète).
4. ** Flexibilité linguistique** – Vous pouvez présenter la même logique en Java, Python, C++ ou même JavaScript, impressionnant les intervieweurs qui apprécient le code propre, multiplateforme.

Si vous pouvez articuler cette solution, vous obtiendrez une question d'interview hors du chemin *alors que vous êtes encore chaud.* Il vous aide également à résoudre d'autres problèmes de niveau moyen qui dépendent de modèles similaires.

---

Les pensées finales

Code du leet 1750 est faussement simple : une chaîne, quelques caractères et un balayage à deux points.
La clé est de reconnaître que les extrémités égales doivent être taillées en vrac, et non pas une à la fois. Cette perspicacité transforme le problème en un seul passage linéaire, vous donnant une solution élégante et efficace.

Utilisez les extraits de code ci-dessus dans votre pratique et dans les entrevues. Mettre en évidence la preuve avide, marcher à travers un exemple rapide, et être prêt à répondre -pourquoi cela fonctionne. Avec ce problème dans votre boîte à outils, vous êtes un pas plus près d'atterrir ce rôle d'ingénierie logiciel de rêve.

---

Codage heureux !**

*Si vous avez trouvé ce message utile, partagez-le sur LinkedIn ou Twitter, et faites-moi savoir dans les commentaires quel problème LeetCode vous êtes s'attaquer à la prochaine. *

---

Conclusion

LeetCode 1750 est un exemple parfait de la façon dont un modèle bien compris – deux pointeurs et une suppression gourmande – peut résoudre un problème apparemment complexe dans le temps linéaire. Maîtrisez ceci, et vous gagnerez non seulement l'insigne « résolution de problèmes » sur votre curriculum vitae, mais aussi démontrerez l'état d'esprit analytique recherché par les recruteurs.

Bonne chance, et n'hésitez pas à contacter si vous souhaitez un-on-one interview coaching ou une plongée plus profonde dans d'autres défis LeetCode!

---

> **Suivez-moi** pour plus de guides de préparation d'entrevues, de tutoriels en algorithme et de conseils en perfectionnement professionnel.

---

* Fin de poste*

---

Conclusion

LeetCode 1750 n'est pas juste un autre problème de manipulation de chaîne; c'est un micro-cours dans la technique avide à deux points. En évitant la suringénierie et en se concentrant sur les suppressions maximales, vous pouvez le résoudre en temps linéaire avec un code minimal.

N'hésitez pas à laisser tomber mes coordonnées si vous voulez un entretien simulé personnalisé ou une analyse plus approfondie de problèmes similaires. Bonne chance – et le codage heureux!