---
titre: LeetCode 780. Atteindre les points -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
N° 780 – Atteindre des points
**A Deep- Dive Blog Post (Java + Python + C++)**
> *Le bon, le mauvais, et le laid de ce puzzle d'interview classique. *

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Pourquoi ce problème fait-il des interrogations] (#pourquoi ce problème fait-il des interrogations)
3. [L'approche naïve et ses pièges] (#l'approche naïve)
4. [L'algorithme de retour optimal] (#le suivi de retour optimal)
5. [Mise en oeuvre étape par étape] (#Mise en oeuvre étape par étape)
6. [Code: Java, Python, C++](#code)
7. [Complexité temporelle et spatiale](#complexité)
8. [Défauts et erreurs courantes] (#cas de référence)
9. [Le bon, le mauvais, le mauvais]
10. [Reflexions finales et conseils d'entrevue] (#pensées finales)
11. [Références et lectures supplémentaires](#références)

---

## Aperçu du problème <a name="problem-overview"></a>

> **LeetCode 780 – Atteindre des points**
> **Difficulté:** Dur
> **URL:** <https://leetcode.com/problèmes/preview-points/>

Compte tenu des entiers `sx, sy, tx, ty`, déterminez si vous pouvez transformer le point `(sx, sy)` en `(tx, ty)` en utilisant uniquement les opérations:
- `(x, y) → (x, x + y) "
- `(x, y) → (x + y, y) "

Toutes les valeurs sont dans la plage `1 ... 10^9`.

---

## Pourquoi ce problème est-il un problème?

1. **Mathématical Insight** – Nécessite de reconnaître un modèle d'ingénierie inverse.
2. **Connaissance des cas** – Vous devez penser au débordement, à la disvisibilité et aux sorties précoces.
3. **Efficacité spatiale** – Doit être résolu sans récursion pour éviter les débordements de la pile sur les grandes entrées.
4. **Conception algorithmique claire** – Démontre la capacité de transformer un processus avant en un processus rétrograde.

> * Les chercheurs d'emploi qui clouent ce problème montrent une forte compréhension de la pensée algorithmique. *

---

## L'approche naïve et ses pièges <un nom></a>

Une recherche simple sur l'étendue et la première portée (BFS) de `(sx, sy)` explorera tous les mouvements possibles explosera de façon exponentielle.
- **Temps:** Non consolidé; peut frapper des millions d'États avant de frapper `10^9'.
- **Espace:** Ingérable pour les grandes plages d'entrée.
- **Pratique :** Faire face aux tests officiels ; erreurs TL/ML.

> *Éviter le BFS – c'est le point fort de ce problème. *

---

## L'algorithme de retour optimal <un nom d'algorithme de retour optimal></a>

Idée de base

Au lieu de pousser de `(sx, sy)` vers l'extérieur, diminuer de `(tx, ty)` vers l'arrière à `(sx, sy)`.

- Si `tx > ty`, l'étape précédente doit avoir été `(tx - ty, ty)` parce que la seule façon d'augmenter `x` est d'ajouter `y`.
- Symmétriquement, si `ty > tx`, l'étape précédente était `(tx, ty - tx)`.

### Utiliser Modulo pour sauter les étapes redondantes

La soustraction répétée de la plus petite valeur est équivalente à "tx %= ty` (ou "ty %= tx`) lorsque la plus petite valeur est encore plus petite que la contrepartie de la cible.
Cela s'effondre en plusieurs étapes et maintient la boucle efficace.

Conditions de résiliation

1. ** Succès :** `tx == sx && ty == sy "
2. **Impossible :** `tx < sx` ou `ty < sy "
3. **Vérification rapide:** Si `tx == ty`, nous ne pouvons arrêter que si les deux coordonnées de démarrage sont égales à la cible ou si l'autre dimension correspond après réduction modulaire.

---

## Mise en oeuvre étape par étape <un nom></a>

Texte
alors que tx >= sx et ty >= Oui.
si tx == ty: # ne peut pas aller plus loin; vérifier la disvisibilité
pause
si tx > ty:
si ty > sy:
tx %= ty # sauter plusieurs soustractions à la fois
Autrement : # ty == sy → une seule dimension peut grandir
retour (tx - sx) % ty == 0
Autre: # ty > tx
si tx > sx:
ty %= tx
Sinon:
retour (ty - sy) % tx == 0
retour tx == sx et ty == sy
«» "

---

## Code: Java, Python, C++ <a name="code"></a>

### Java (espace O(1))

"Java
// LeetCode 780 - Atteindre des points
solution de classe publique {
le booléen public atteignantPoints(int sx, int sy, int tx, int t ty) {
(tx >= sx && ty >= sy) {
si (tx) ty) rupture;
si (tx > ty) {
si (ty > sy) tx %= ty;
Sinon, retourner (tx - sx) % ty == 0;
} autre {
si (tx > sx) ty %= tx;
sinon retourner (ty - sy) % tx == 0;
}
}
retour tx == sx && ty == sy;
}
}
«» "

### Python (Python 3)

'`python
# LeetCode 780 - Atteindre des points
Solution de classe:
def atteindrePoints(self, sx: int, sy: int, tx: int, ty: int) -> C'est vrai.
alors que tx >= sx et ty >= Oui.
si tx == ty:
pause
si tx > ty:
si ty > sy:
tx %= ty
Sinon:
retour (tx - sx) % ty == 0
Sinon:
si tx > sx:
ty %= tx
Sinon:
retour (ty - sy) % tx == 0
retour tx == sx et ty == sy
«» "

### C++ (C++17)

'`cpp
// LeetCode 780 - Atteindre des points
solution de classe {
public:
pointes (int sx, int sy, int t tx, int t ty) {
(tx >= sx && ty >= sy) {
si (tx) ty) rupture;
si (tx > ty) {
si (ty > sy) tx %= ty;
Sinon, retourner (tx - sx) % ty == 0;
} autre {
si (tx > sx) ty %= tx;
sinon retourner (ty - sy) % tx == 0;
}
}
retour tx == sx && ty == sy;
}
};
«» "

---

## Complexité temporelle et spatiale <un nom=complexité></a>

Langue Heure Espace
- C'est quoi ?
Java **O(log (max(tx,ty)))
Python **O(log (max(tx,ty)))**
C++. **O(log (max(tx,ty)))**. **O(1).**.

*Le facteur logarithmique provient des opérations modulo répétées, qui réduisent considérablement les coordonnées de la cible. *

---

## Cas de bord et erreurs courantes <un nom="cas de bord"></a>

Pourquoi ça compte ?
- Oui.
"sx" == tx && sy == ty`-
`tx < sx` ou `ty < sy`=Impossible de grandir en arrière= Loop se terminera; la vérification finale retourne `false` Autres
Ty' mais pas égal au début Aucun autre déplacement possible.
Grandes entrées près de `10^9`= Débordement potentiel en utilisant la soustraction=Utiliser modulo pour éviter de nombreuses soustraction=

---

## Le bon, le mauvais, l'horrible <un nom "bon-mauvais"></a>

Aspect du bien
- C'est quoi ?
**Idées algorithmiques**
**Complexité du code**=20 lignes de code propre et lisible== Aucune Autres
**Performance**
L'arithmétique modulaire est intuitif pour les codeurs expérimentés.

> *L'équation ici est principalement l'erreur initiale d'essayer BFS. Une fois que vous inversez la voie, la solution devient une joie à lire. *

---

## Pensées finales et conseils d'entrevue <un nom="pensées finales"></a>

1. ** Expliquez d'abord le raisonnement inverse.** Les intervieweurs aiment entendre le processus de pensée.
2. **Montrer le tour du modulo.** Il démontre la maturité algorithmique.
3. **Cas de bord des discussions.** Parlez de quand `tx == ty`, ou quand une coordonnée égale sa valeur de départ.
4. **La complexité des peines.** Soyez prêt à expliquer pourquoi votre solution est `O(log n)` et non exponentielle.

> *La maîtrise de ce problème est un solide «proof-of-concept» que vous pouvez résoudre des questions d'entrevue difficile avec un code propre et efficace. *

---

## Références & Lecture supplémentaire <un nom="références"></a>

- Problème de LeetCode 780 : <https://leetcode.com/problèmes/preaching-points/>
- Éditorial & Solutions (Java/Python/C++):
- <https://leetcode.com/problèmes/reaching-points/solutions/114732/java-simple-solution-with-explanation-by-vb8h/>
- <https://leetcode.com/problèmes/reaching-points/solutions/1774665/best-and-évidence-solutions-by-singhjp006-i2vk/>
- <https://leetcode.com/problèmes/reaching-points/solutions/5204364/java-beats-100-by-suppléted_user-aif0/>

---

Améliorer votre score d'entrevue
> Prêt à impressionner vos gestionnaires d'embauche? Pratiquez ce problème, partagez votre solution sur GitHub, et marquez-le avec **#LeetCode780 #AlgorithmDesign**. Bonne chance !

---

*Référence Mots-clés: LeetCode 780, Reaching Points solution, Java, Python, C++, interview algorithmique, interview technique, conseils d'entrevue, interview de codage, BFS vs back-tracking. *