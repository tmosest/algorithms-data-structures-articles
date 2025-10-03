---
titre: LeetCode 2855. Minimum de quarts de droite pour trier le tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code de Leet 2855 – Déplacements mineurs à droite pour trier le tableau
- Oui. Un guide rapide, une solution complète et une interview « bon »

---

TL;DR

- **Problème** – Trouvez le plus petit nombre de *correspondance droite* qui transforment un tableau donné en ordre ascendant, ou retournez `-1` si impossible.
- **Core Insight** – Un seul point dans l'ordre trié (une paire descendante) nous indique le point de rotation.
- **Complexité** – temps « O(n) », espace « O(1) ».
- **Langues** – Java, Python, C++ – toutes en un seul bloc de code.
- **Pourquoi ça compte** – Il s'agit d'un exemple de manuel de la logique de rotation d'array qui apparaît sur presque chaque entretien de codage.

---

- Oui. 1. Récapitulation des problèmes (à partir de LeetCode)

> **Given**: `nums` – un tableau 0-indexé d'entiers positifs distincts.
> **Objectif** : Retourner le nombre minimum de quarts de travail qui trieront les « nombres » en ordre non décroissant. Si ce nombre n'existe pas, retourner `-1`.
> **Travail droit**: Déplacer l'élément à l'index `i` vers l'index `(i + 1) % n` pour tous les indices.

> **Exemples**
> *Input*: `[3,4,5,1,2]` → *Output*: `2`
> *Input*: `[1,3,5]` → *Output*: `0`
> *Input*: `[2,1,4]` → *Output*: `-1`

---

- Oui. 2. Insight – Un seul Drop est tout ce dont vous avez besoin

- Oui. Dans un tableau trié, chaque élément est plus petit que son successeur.
- Oui. Si le tableau est un tableau trié en rotation, il aura **exactement un "drop"** – une position où `nums[i-1] > nums[i]`.
- Oui. Si vous trouvez plus d'une goutte, le tableau ne peut être trié par n'importe quel nombre de bonnes rotations.
- Oui. Si vous trouvez zéro goutte, le tableau est déjà trié → réponse `0`.
- Oui. Si vous trouvez une goutte à l'index `i`, le tableau trié commencerait par `i` (le plus petit élément).
- Le nombre de quarts de travail à droite requis est `n - i` (déplacer la queue vers l'avant).
- Vous devez également vérifier que le dernier élément est **pas** plus petit que le premier élément après la rotation; sinon, le tableau se enveloppe dans la mauvaise direction → retourner `-1`.

La logique est **linéaire** et n'utilise que quelques variables entières.

---

- Oui. 3. Le Code

Voici un fichier source unique qui contient **Java, Python et C++** implémentations côte à côte. Chaque implémentation suit le même algorithme, de sorte que vous pouvez copier-coller celui qui correspond à votre langue d'entrevue.

"Java
/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
* LeetCode 2855: Minimum des postes de droite pour trier le tableau
* Auteur: Votre nom
* ------------------------------------------------------------
*
* Langues: Java, Python, C++
* Complexité: temps O(n), espace O(1)
* ------------------------------------------------------------
*/

/* - Oui. JAVÉ ----------- */
classe publique MinimumRightShiftsSolution {
Int minimum public WheatShifts(Liste <entier> nombres) {
int n = nombres.size();
dropIdx = 0; // indice où nombres[i-1] > nombres[i]
int dropCnt = 0; // combien de gouttes nous voyons

pour (int i = 1; i < n; i++) {
si (nums.get(i - 1) > nums.get(i)) {
dropIdx = i;
dropCnt++;
}
}

si (dropCnt > 1) retour -1; // plus d'une goutte → impossible
Si (dropIdx) 0) retour 0; // déjà trié

// Vérifiez que le tableau après la rotation sera toujours trié
si (nums.get(n - 1) > nums.get(0)) retour -1;

retour n - dropIdx; // nombre de quarts de travail à droite nécessaires
}
}

/* - Oui. PYTHON ------------------------- */
classe PythonSolution:
def minimum RightShifts(self, nombres: list[int]) -> Int:
n = len(nums)
drop_idx = 0
drop_cnt = 0
pour i dans la plage (1, n):
si des nombres - 1] > nombres[i]:
drop_idx = i
drop_cnt += 1
si drop_cnt > 1 :
retour -1
si drop_idx == 0:
retour 0
si nombres[-1] > nombres[0]:
retour -1
retour n - drop_idx

/* - Oui. C++ ----------- */
classe CPPSolution {
public:
Int minimumRightShifts(vector<int>& nums) {
int n = nombres.size();
int dropIdx = 0;
Int dropCnt = 0;
pour (int i = 1; i < n; ++i) {
si (nombres [i - 1] > nombres[i]) {
dropIdx = i;
++DropCnt;
}
}
si (dropCnt > 1) retour -1;
Si (dropIdx) 0) retour 0;
si (nums[n - 1] > nombres[0]) retour -1;
retour n - dropIdx;
}
};
«» "

> **Astuce**: Dans les interviews, demandez toujours si le tableau peut contenir des duplicatas. La déclaration LeetCode garantit des entiers distincts, donc nous n'avons pas besoin de traiter les cas d'égalité. Si des duplicatas étaient autorisés, vous changeriez les comparaisons en `>=` en conséquence.

---

- Oui. 4. Le bien, le mal et le mal

Catégorie Qu'est-ce que le bien Qu'est-ce que le mal Quoi ?
- C'est quoi ?
**Simplicité algorithmique**= Un scan linéaire, espace constant. Nécessite un œil vif pour la propriété de la goutte d'one – pas évident à première vue. Une solution naïve qui tourne le tableau `n` fois et vérifie la triabilité (`O(n2)`), conduisant à TLE sur de grandes entrées. Autres
**Robustness**=Poigne tous les boîtiers de bord (panier vide, élément unique, déjà trié). Suppose que tous les numéros sont distincts; doit modifier si des duplicatas sont autorisés. Effacer sur les tableaux qui enveloppent incorrectement parce que la vérification `dernier > premier` est omise. Autres
**Readability**= Effacer les noms de variables (`dropIdx`, `dropCnt`). Certains peuvent préférer `breakPoint` ou `rotationIndex` pour la clarté sémantique. Code obfusqué avec nombres magiques ou commentaires en ligne manquants. Autres
**Temps/Espace**=Temps `O(n)`, espace `O(1)` – optimal. Toujours "O(n)" temps; si les contraintes étaient "107", nous pourrions avoir besoin d'une approche différente. O(n2) ou O(n log n) en raison du tri ou de la rotation répétés. Autres
**Interview Impact** Il a besoin d'expliquer l'invariant d'une goutte. La suringénierie ou l'écriture d'une simulation de force brute montre un manque de pensée algorithmique. Autres

---

- Oui. 5. Pourquoi maîtriser ce problème vous aide à obtenir un emploi

1. **Reconnaissance des cartes** – De nombreux problèmes d'entrevue concernent la reconnaissance de la trialité, des rotations ou des patrons cycliques. Une fois que vous remarquez le truc de la goutte d'eau, vous pouvez l'appliquer à des questions similaires de LeetCode (p. ex., *Rotations d'array circulaire*, *Trouver minimum dans l'array trié rotatif*).
2. **Clean Code** – Votre solution est concise, lisible et exempte de complexité inutile. Les intervieweurs aiment les candidats qui peuvent fournir une solution claire et prête à la production en peu de temps.
3. **Commerce spatial-temps Off** – montrer que vous pouvez le résoudre dans le temps `O(n)` et l'espace `O(1)` démontre une conscience de l'efficacité algorithmique – critique dans les systèmes du monde réel où la performance compte.
4. ** Confiance linguistique** – Fournir des solutions Java, Python et C++ montre une polyvalence. De nombreux gestionnaires d'embauche demandent aux candidats de coder dans une langue de leur choix; vous serez prêt pour n'importe quelle pile.
5. **Storytelling** – Dans la section « Bon – Mauvais – Mauvais », vous expliquez pourquoi une approche particulière est supérieure. Les intervieweurs apprécient la capacité de narrer les compromis, une compétence qui se traduit par des examens de codes et des décisions architecturales.

> * Conseil professionnel* : Dans votre CV ou portfolio, ajoutez une courte section de motifs algorithmiques. Mention :Rotated Tried Array Recognition et lien vers cette solution sur GitHub. Les recruteurs aiment les preuves concrètes de la résolution de problèmes.

---

- Oui. 6. A emporter optimisé par le SEO

- ** Mots-clés principaux**: `leetcode minimum droit sheets`, `array rotation tri`, `minimum droit sheets to tri array solution`, `Java Python C++ solution`, `codage de la rotation du tableau d'entretien`.
- **Description détaillée** (155 caractères) :
Solve LeetCode 2855 en Java, Python et C++ avec un algorithme O(n). Comprendre l'astuce d'une goutte, voir une bonne-mauvaise panne, et stimuler votre préparation d'entrevue. (en milliers de dollars)
- **Alt-text pour les images** (si vous ajoutez des captures d'écran): Code Java pour le LeetCode 2855 minimum à droite.

---

- Oui. 7. Liste de contrôle finale

- Oui. [x] Comprendre l'invariant de la goutte unique.
- Oui. [x] Implémenter un balayage linéaire, espace constant.
- Oui. [x] Valider les cas bord (`n == 1`, déjà triés).
- [x] Inclure un dernier contrôle de sécurité.
- [x] Écrire un code propre et commenté dans les trois langues.
- [x] Préparer un billet de blog concis avec des éléments SEO.
- [x] Télécharger vers GitHub, lier à partir de votre CV, et pratiquer expliquant l'approche dans une interview simulée.

Bonne chance ! C'est ce qu'il a dit