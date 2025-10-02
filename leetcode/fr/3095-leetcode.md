---
titre: LeetCode 3095. Subarray le plus court avec OU au moins K I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3095 – Subarray le plus court avec OU au moins K I

**Récapitulation des problèmes* *
Compte tenu d'un éventail d'entiers non négatifs `nums` (longueur ≤ 50, chaque `nums[i]` ≤ 50) et d'un entier `k` (0 ≤ k < 64), trouver la longueur de la sous-tribu la plus courte contiguë dont la OR bitwise est **≥ k**.
Retourner `-1` s'il n'existe pas de sous-tribu.

Comme les contraintes sont minuscules, une solution "O(n2)" fonctionne, mais les intervieweurs adorent voir une approche "Fenêtre de glissement"* + "Tableau de fréquence"* qui s'élève à "n = 105". Vous trouverez ci-dessous le code de production prêt, la langue-agnostique (Java, Python, C++), suivi d'un billet de blog SEO-friendly qui couvre le *bon, le mauvais et le laid* de la solution.

---

- Oui. 1. Code de préparation à la production

> *Les trois implémentations partagent le même noyau algorithmique :*
> * une fenêtre coulissante `[gauche, droite]` qui grandit à droite,
> * une table bit-fréquence `cnt[0...31]` qui garde une trace du nombre de nombres dans la fenêtre courante définie chaque bit,
> * un `orValue` dynamique qui est recalculé à partir de la table chaque fois que la fenêtre est rétrécie.

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe {

// Ajoute x à la fenêtre actuelle
vide privé ajouter(int x, int[] cnt, int[] ouVal) {
pour (int b = 0; b < 32; b++) {
si ((x & (1 << b))) != 0) {
Si (++cnt[b]) 1) // premier numéro avec ce jeu de bits
orVal[0]= 1 << b; // définissez le bit dans la valeur OU
}
}
}

// Supprime x de la fenêtre actuelle
vide privé supprimer(int x, int[] cnt, int[] ouVal) {
pour (int b = 0; b < 32; b++) {
si ((x & (1 << b))) != 0) {
si (--cnt[b]] 0) // plus de nombres avec ce bit
ouVal[0] &= ~(1 << b); // effacer le bit
}
}
}

Int minimumSubarrayLength(int[] nums, int k) {
int n = longueur nums;
int minLen = entier.MAX_VALUE;
int[] cnt = nouvelle int[32]; // fréquence de chaque bit dans la fenêtre
int[] orVal = {0}; // Int enveloppé pour pouvoir la muter

pour (int gauche = 0, droite = 0; droite < n; droite++) {
ajouter(nums[right], cnt, orVal);

alors que (ouVal[0] >= k) { // fenêtre est déjà assez grande
minLen = Math.min(minLen, droite - gauche + 1);
supprimer(nums[left], cnt, ouVal);
gauche++; // rétrécir à gauche
}
}

Retour minLen == Integer.MAX_VALUE ? -1 : minLen;
}
}
«» "

**Complexités* *

Opération Temps Espace
- C'est quoi ?
Autres Fenêtre coulissante + nombre de bits

---

#### 1.2 Python

'`python
Solution de classe:
def minimumSubarrayLength(self, nombres: Liste[int], k: int) -> Int:
n = len(nums)
min_len = flotteur('inf')
cnt = [0] * 32 # table de fréquence
ou_val = 0

gauche = 0
pour droite, val in énumérate(nums):
# agrandir la fenêtre à droite
pour b dans la fourchette(32):
si valeur >> b & 1:
cnt[b] += 1
si cnt[b] 1 :
ou_val= 1 << b

# contrat pendant que le OU satisfait à la condition
pendant que _val >= k et gauche <= droite:
min_len = min(min_len, droite - gauche + 1)

# supprimer les nombres[gauche] de la fenêtre
pour b dans la fourchette(32):
si nombres[gauche] >> b & 1:
cnt[b] -= 1
si cnt[b] 0:
ou_val &= ~(1 << b)
gauche += 1

retourner -1 si min_len == flotter('inf') sinon min_len
«» "

---

*## 1.3 C++

'`cpp
solution de classe {
public:
Length(vecteur <int>& nums, int k) {
BITS = 32;
vecteur<int> cnt(BITS, 0);
int ouVal = 0;
Int minLen = INT_MAX;
Int gauche = 0;

ajouter automatiquement = [&](int x) {
pour (int b = 0; b < BITS; ++b) {
Si (x et (1 << b))) {
Si (++cnt[b]) 1 )
ouVal= 1 << b;
}
}
};

supprimer automatiquement = [&](int x) {
pour (int b = 0; b < BITS; ++b) {
Si (x et (1 << b))) {
si (--cnt[b]] 0)
ouVal &= ~(1 << b);
}
}
};

pour (int right = 0; right < nums.size(); ++right) {
ajouter(nums[right]);

pendant que (ou Val >= k) {
minLen = min(minLen, droite - gauche + 1);
supprimer(nums[left++]);
}
}

retour minLen == INT_MAX ? -1 : minLen;
}
};
«» "

---

- Oui. 2. Billet de blog – *=Le bon, le mauvais et le mauvais de l'OR‐Sliding‐Window*

> ** Mots-clés du référencement* *
> *Shortest sub-array OR LeetCode*, *bitwise OR interview problem*, *array sliding window solution*, *job interview data-structure*, *bit-fréquence table technique*, *Java Python C++ solutions*, *candidate interview conseils*

---

Titre
**Mastering LeetCode 3095: Comment trouver le sous-array le plus court avec OU ≥ k (Java / Python / C++)* *

---

Description de la méta (160 caractères)
Débloquez la solution la plus rapide pour LeetCode 3095 à l'aide d'une fenêtre coulissante + table bit-fréquence. Code Java, Python & C++, plus des explications conviviales.

---

C'est pas vrai. Pourquoi les intervieweurs aiment ce problème

* **Le raisonnement basé sur le bit** – Montrez que vous comprenez la manipulation de bits, un sujet de base CS.
* **Fenêtre coulissante** – Preuves que vous pouvez convertir la force brute en une solution *O(n*).
* ** Optimisation de l'espace** – Le compteur 32-int est un classique *O(1)* tour d'espace supplémentaire.
* **Échelle** – Le même code fonctionne pour `n = 105` et `k = 236`.

Si vous pouvez livrer ce qui précède en trois langues avec un code propre et commenté, vous vous démarquerez des recruteurs et des gestionnaires d'embauche.

---

- Oui. Le Bon – Pourquoi Cette approche Rocks

Pourquoi ça compte ?
-- -- -- -- -- -- -- --
**Temps linéaire**="O(n)" même pour les grands tableaux – les intervieweurs aiment les algorithmes à l'échelle. Autres
**O(1) Extra Space**= 32-int table – pas de mémoire dynamique au-dessus. Autres
**Fenêtre de glissement déterministe**= Garantie que le sous-array *le plus court* est trouvé dès que la condition est remplie. Autres
**Code idiomatique** Autres
Autres **Test-Driven**.Test facile à unit-test de chaque helper (`add`, `remove`, `orVal` update). Autres

> *Astuce:* En Java, enveloppez la valeur OR dans un tableau à élément unique (`int[] orVal = {0}`) afin que les méthodes d'aide puissent la muter – un tour subtil mais crucial qui maintient le code rangé.

---

C'est vrai. Les mauvaises – pièges communs

Comment l'éviter
-- -- -- -- -- -- -- --
**Débordement du compte-bit**= Tous les nombres sont ≤ 50 → seulement moins 6 bits utilisés, mais nous conservons 32 bits pour rester génériques. Autres
**Obligation d'effacer les bits**= Après avoir enlevé un nombre, vérifiez si le nombre de bits atteint 0 **avant**. Autres
**La mauvaise gestion de l'Index**Les limites des fenêtres coulissantes doivent être inclusives à gauche, exclusives à droite dans certaines langues; gardez un œil sur `à droite - à gauche + 1`. Autres
**Off‐by‐one dans la boucle pendante**=== La boucle `while (orVal >= k)` *must* risk avant de mettre à jour `minLen` pour capturer la fenêtre *short*. Autres

---

C'est pas vrai. L'horrible – quand les choses tournent mal

1. **Recomposition OU à partir de zéro**
*La manière naïve est de recalculer la valeur OR en itérant à nouveau sur la fenêtre. *
Cela donne un temps `O(n2)` – acceptable pour `n = 50` mais désastreux pour les gros intrants.

2. **Utiliser une carte des entiers**
*Certains candidats créent une carte entière de bit → compter. *
Bien que correct, le haut de la carte recherche et boxe / désboxe peut être des ordres de magnitude plus lent qu'un éventail de primitifs.

3. **Optimisation excessive pour une petite entrée**
*L'écriture d'une fenêtre coulissante complexe pour `n ≤ 50' est surqualifiée. *
Les intervieweurs apprécient le niveau *droit* de complexité – pas trop simple, ni trop fou.

---

C'est vrai. Points d'entrevue en préparation

Question Réponse suggérée
Il y a un problème.
*Pourquoi la table bit-fréquence au lieu de recalculer OU sur chaque retrait?*= Parce que recalculer OU à partir de zéro serait `O(bits)` pour chaque retrait. La table nous permet de nettoyer les morceaux en temps constant. Autres
*Peut-on faire mieux que `O(n)`?*= Avec ces contraintes, `O(n)` est optimal. Pour la version II, vous avez toujours besoin d'une fenêtre coulissante; `O(n)` reste optimale. Autres
*Qu'en est-il des chiffres négatifs? Le problème garantit des nombres non négatifs. Si les négatifs étaient autorisés, vous devriez traiter le signe séparément. Autres
*Comment l'algorithme se comporte-t-il lorsque k est 0?*=Le OU de tout sous-array non vide est ≥ 0, donc la réponse est toujours 1 (le plus petit sous-array). L'algorithme s'en chargera naturellement. Autres

---

- Oui. 3. SEO-Optimized Blog Post (= 900 mots)

> **Headline** – *=How to Nail LeetCode 3095: Subarray le plus court avec OU ≥ k – Un guide Java/Python/C++ complet*

> ** Limace** – `code de la roue-3095-shortest-subarray-or-at-least-k`

> **Meta Description** – *=Solve LeetCode 3095 avec l'algorithme le plus rapide en Java, Python et C++. Comprendre les avantages et les inconvénients, voir le code propre, et passer votre prochaine entrevue sur la structure des données.

3.1 Introduction (= 150 mots)

«» "
Si vous vous préparez à une entrevue d'ingénierie logicielle, LeetCode 3095 est un problème classique d'ORI qui teste votre pensée de bas niveau et votre capacité à écrire un code propre et évolutif. Dans ce billet, vous trouverez trois solutions prêtes à la production : une base de référence brute O(n2), l'approche évolutive de la fenêtre coulissante + fréquence bit, et comment la même logique se traduit à travers Java, Python et C++. À la fin, vous savez :
- Oui. Ce qui rend le tour de la fenêtre coulissante puissant,
- Lorsque vous pouvez utiliser la solution O(n2) plus simple en toute sécurité,
- Comment éviter les bugs subtils qui font monter beaucoup de candidats.
«» "

#### 3.2 Récapitulation du problème (= 100 mots)

«» "
Compte tenu d'un tableau `arr` et d'un entier `k`, trouver le plus petit sub-array contigu dont OR bitwise est au moins `k`. Tous les nombres sont non-négatifs, donc le signe bit n'est pas pertinent. La solution naïve contrôle chaque sous-arrachage possible, conduisant à O(n2). Nous allons montrer pourquoi cela est insuffisant pour les grands ensembles de données et présenter un algorithme linéaire qui maintient l'utilisation de la mémoire constante.
«» "

#### 3.3 Forte-Force O(n2) (150 mots)

«» "
Bien que cet algorithme soit acceptable pour la contrainte de 50 éléments du problème, il donne un bon contrôle de la folie et vous aide à vérifier vos solutions plus avancées. Voici un petit extrait de Python :

«» "

*(Insérer l'extrait de force brute de Python)*

«» "
La clé est de calculer OR à la volée pendant que vous prolongez la fenêtre, mais lorsque vous la contractez, vous devez recalculer l'OR à nouveau – ce qui tue la performance dans les entrées plus grandes.
«» "

### 3.4 La table de fenestration coulissante + Bit-Fréquence (= 400 mots)

> * Expliquez le concept : la fenêtre coulissante maintient un OR en cours d'exécution ; le tableau bit-count garde la fréquence ; la suppression est un temps constant. *

«» "
Nous commençons par passer par l'algorithme en anglais clair:
1. Initialiser les pointeurs gauche et droite au début du tableau.
2. Élargissez le pointeur de droite, en ajoutant des bits à la table de fréquence et en mettant à jour le OU en cours d'exécution.
3. Pendant que le OU en cours d'exécution satisfait `or_val >= k`, mettez à jour la meilleure réponse et rétrécissez à partir de la gauche.
4. Continuez jusqu'à ce que le pointeur droit atteigne la fin.

La vision critique est que nous ne recalculons jamais la valeur OU de zéro lors de l'enlèvement d'un élément. Au lieu de cela, nous décrémentons la fréquence de chaque bit qui apparaît dans le nombre supprimé et ne l'effacons que si son nombre atteint zéro. Cela maintient chaque opération O(1), donnant un temps d'exécution O(n) global.

Voici le code exact pour chaque langue. Remarquez comment les aides (`add`/`remove`) maintiennent la boucle principale courte et lisible. Pour Java, la valeur OR est enveloppée dans un tableau à un élément afin que les méthodes d'aide puissent la muter. En Python, nous utilisons une compréhension de la liste pour garder la logique concise. En C++, nous utilisons une lambda pour maintenir le code d'aide en ligne.
«» "

*Insérer les extraits de code côte à côte ou utiliser un bloc de code par langue. *

#### 3.5 Cas et conseils de bord (= 150 mots)

«» "
- Oui. 0: Toute sous-entente est valide – la réponse est toujours 1. Votre algorithme retournera 1 naturellement.
- k > max_possible_OR: Si k est plus grand que l'OR du tableau entier, la réponse est -1. L'algorithme sort gracieusement avec INT_MAX / inf.
- Petits tableaux : Alors qu'une fenêtre coulissante est sur-enginée pour n <= 50, les recruteurs apprécient de vous voir écrire une solution optimale de toute façon.
«» "

#### 3.6 Questions d'entrevue courantes (= 150 mots)

«» "
Q: Pourquoi conservons-nous 32 bits même si les valeurs d'entrée n'utilisent que 6 bits?
R: Stocker 32 bits maintient la solution générique et protège contre les changements futurs. Il s'harmonise également avec la plupart des langues.

Q: Et si le tableau contenait des nombres négatifs?
R: Les chiffres négatifs introduisent le signe bit. L'algorithme fonctionnerait encore si nous traitons le signe séparément ou convertissons les nombres en représentations non signées.

Q: Est-il sûr d'utiliser un dictionnaire pour la table de fréquence en Python?
R: Il fonctionne mais introduit les frais généraux. Une gamme de 32 entiers est plus rapide et plus efficace en mémoire.
«» "

#### 3.7 Takeaway & Call‐to‐Action (= 100 mots)

«» "
LeetCode 3095 est un micro-cours de manipulation de bits, de fenêtres coulissantes et de conception d'algorithmes langage-agnostiques. En maîtrisant l'astuce de la table bit-fréquence, vous serez en mesure de s'attaquer à une gamme de problèmes de tableau avec confiance. Utilisez les extraits de code ci-dessous pour pratiquer sur votre machine locale ou les intégrer dans votre repo GitHub pour la préparation d'entrevues prêtes pour le portfolio.

Prêt à relever des défis plus bit-wise? Explorez mes autres messages sur les problèmes de Bitwise et de Sub-array XOR. Bon codage !
«» "

#### 3.8 Clôture (de 50 mots)

«» "
Vous voulez voir la même logique en action ? Découvrez le GitHub Gist avec les implémentations Java, Python et C++. Laissez un commentaire si vous êtes coincé sur un cas de bord particulier – laissez-nous conquérir LeetCode ensemble!
«» "

---

Publier et partager

1. **Post on Medium/Dev.to** – utilisez les mots-clés dans le titre et les balises.
2. **Cross-post à lié Dans** – ajouter un bref extrait et un lien vers l'article complet.
3. **SEO Check** – Assurez-vous que la densité de mots clés est ~1–2%, que les méta tags sont remplis, et que l'article est au moins 800 mots.
4. **Engagement** – Répondre aux commentaires, demander aux lecteurs de fourcher la repo, et offrir une session de révision de code privé pour quelques commentateurs.

---

C'est vrai. Comment ce blog vous aide à obtenir le travail

* **Showcase** – Partagez le blog sur votre CV ou portfolio ; les recruteurs cliqueront sur.
* **Cherchable** – Les chercheurs d'emploi à la recherche de la solution LeetCode 3095 atterriront sur votre page.
* ** Crédibilité** – Démontre une compréhension profonde dans plusieurs langues.
* **Communauté** – L'engagement de commentaires sur le moyen ou le moyen peut conduire à des renvois.

---

- Oui. 4. Liste de contrôle rapide pour votre entrevue

1. *Le code de la fenêtre coulissante est prêt en Java, Python et C++? *
2. *Pouvez-vous expliquer `ajouter`/`supprimer` en moins de 2 minutes? *
3. *Test cas bord: k = 0, k = max(arr), nombres négatifs? *
4. *Préparer des points de discussion pour les questions de pourquoi. *

Si vous cochez toutes les cases, vous ne vous contentez pas de résoudre le LeetCode 3095 – vous le transformez en vitrine de promotion de carrière.

---

> **Bon entretien!**

---

C'est ça – une réponse entièrement autonome qui vous donne du code en trois langues, une explication concise mais profonde, et un billet de blog prêt pour le référencement pour attirer les recruteurs. Bonne chance !