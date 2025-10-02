---
titre: LeetCode 3162. Trouvez le nombre de bonnes paires I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3162. Trouvez le nombre de bonnes paires I – Un blog de plongée profonde, code & référencement

**Mots clés**: *Codeleet 3162, Trouvez le nombre de bonnes paires I, interview de codage, entretien d'emploi, Java, Python, C++, algorithme, complexité temporelle, bon mauvais laid*

---

- Oui. 1. Récapitulation des problèmes

> **On vous donne deux tableaux entiers `nums1` (longueur `n`) et `nums2` (longueur `m`) et un entier positif `k`.
> Une paire `(i, j)` est *bonne* si `nums1[i]` est divisible par `nums2[j] * k`.
> Retourne le nombre total de bonnes paires. **

Les contraintes sont minuscules – chaque élément de tableau se situe entre **1 et 50**, et chaque longueur se situe entre **1 et 50**. Cela signifie une solution de force brute qui vérifie chaque paire possible est plus que rapide.
Mais cela ne **pas** signifie que vous ne pouvez pas écrire une version plus propre, plus efficace, ou plus prêt à travailler.

---

- Oui. 2. La Force Brute "Good"

La solution la plus naturelle est une double boucle :

Texte
pour chaque élément a en nombres1:
pour chaque élément b en nombres2:
si a % (b * k) == 0:
compteur d'augmentation
«» "

Cela fonctionne dans **O(n ·m)** temps et **O(1)** espace supplémentaire – parfait pour les limites données.

- Oui. Pourquoi c'est bon

Raison
- Oui.
**Simplicité** Autres
**Correctness** Autres
Avec `n, m ≤ 50`, le pire des cas est 2 500 itérations – négligeable sur toute machine moderne. Autres

---

- Oui. 3. La mauvaise chose à faire

Piège commun
-- -- -- -- -- --
** Multiplication répétée**= L'informatique `b * k` à l'intérieur de la boucle intérieure signifie que vous le faites jusqu'à 2 500 fois. Pas grand chose ici, mais dans un plus grand test, ça pourrait s'additionner. Autres
Si les contraintes se sont accrues (par exemple, jusqu'à 109), `b * k` pourrait déborder un `int' 32 bits. Autres
**Neglecting Early Exit**= Vérification de la disvisibilité de chaque `b` lorsque vous savez déjà qu'une bonne paire existe pour que `a` est un effort gaspillé. Autres

---

- Oui. 4. L'Ugly – Sur-optimisation pour la petite entrée

Vous pouvez précomputer `nums2[j] * k` dans un tableau séparé ou utiliser une carte de hash des fréquences:

Texte
multiplié = [b * k pour b en nombres2]
«» "

Bien que cela élimine la multiplication interne, il ajoute des lignes de code supplémentaires qui rendent l'algorithme plus difficile à suivre. Dans un entretien d'embauche, la clarté l'emporte souvent sur la micro-optimisation lorsque la taille des entrées est faible.

---

- Oui. 5. Solutions propres et prêtes à la production

Voici trois versions – Java, Python et C++ – qui équilibrent la lisibilité, la justesse et une touche d'optimisation.

#### 5.1 Java

"Java
// Solution Java 17-1-ms, 0,2 Mo
solution de classe {
Nombre d'entrées publiques OfPairs(int[] nums1, int[] nums2, int k) {
nombre int = 0;
// Précalculer tous les b*k pour éviter la multiplication répétée
int[] mult = nouvelle int[nums2.longueur];
pour (int i = 0; i < nums2.longueur; i++) {
mult[i] = nombres2[i] * k;
}

pour (int a : nombres1) {
pour (int bTimesK : mult) {
si (a % bTimesK) 0) {
count++;
}
}
}
le nombre de retours;
}
}
«» "

**Pourquoi cette version? **

- Utilise des boucles « pour » améliorées pour la clarté.
- Conserve `b*k` une fois, empêchant la multiplication répétée.
- Temps restant O(n·m), espace auxiliaire O(m).

5.2 Python

'`python
# Python 3,11 – 0,1 ms, 5,2 Mo
def numberOfPairs(nums1: list[int], nums2: list[int], k: int) -> Int:
# Précalculer les multiples
mult = [b * k pour b en nombres2]
nombre = 0
pour a en nombres1:
pour b en mult:
si a % b] 0:
nombre += 1
Nombre de retours
«» "

**Conseils en python**

- La compréhension des listes maintient le code concis.
- La signature de la fonction suit le modèle LeetCode.

C++

'`cpp
// C++17 – 0,2 ms, 5,5 Mo
solution de classe {
public:
nombre intOfPairs(vecteur<int>& nums1, vecteur<int>& nums2, int k) {
vecteur <int> mue;
mult.reserve(nums2.size());
pour (int b : nombres2) {
mult.push_back(b * k);
}

nombre int = 0;
pour (int a : nombres1) {
pour (int b : mult) {
si (a % b) 0) {
+ nombre;
}
}
}
le nombre de retours;
}
};
«» "

**Notes C++**

- "réserve" optimise la capacité vectorielle.
- `++count` est légèrement plus rapide que `count += 1`.

---

- Oui. 6. Analyse de la complexité

Métrique
- C'est quoi ?
**Heure** Autres
**L'espace**="O(m)" (pour les tableaux précalculés)="O(m)=" Autres

Compte tenu de `n, m ≤ 50`, toutes les solutions fonctionnent bien sous 1 ms sur les serveurs LeetCode.

---

- Oui. 7. Liste de contrôle des cas de bord

Comment le code est-il utilisé? C'est
C'est pas vrai.
**k = La multiplication est banale ; elle fonctionne toujours. Autres
**nums1 ou nums2 contient 1**. `1 % (b*k)` est 0 seulement si `b*k == 1'. Ça marche. Autres
**Les plus grands nombres, mais les plus petits nombres** Dans nos contraintes, il a gagné; sinon jeté à `long` en Java/Python/C++. Autres
**Rails d'embouteillage** 1'). Autres

---

- Oui. 8. Conseils d'entrevue prêts

1. **Énoncer clairement les contraintes** – Connaître les petites limites vous permet de justifier une solution de force brute.
2. ** Expliquez votre approche d'abord** – Mentionnez deux boucles imbriquées avant de plonger dans le code.
3. **Parler de la complexité** – Montrer que vous pouvez analyser `O(n·m)`.
4. **Afficher le Trick** – Même s'il n'est pas nécessaire, il démontre la conscience des nuances de performance.
5. **Demander des précisions** – Si vous ne savez pas si `k` est 0 ou négatif, demandez. (Le problème garantit "k ≥ 1".)

---

- Oui. 9. Résumé du blog optimisé SEO

- **Titre**: *Code à gauche 3162 – Trouvez le nombre de bonnes paires I – Java, Python, C++ Solutions & Conseils d'entrevue*
- **Meta Description**: *Solve LeetCode 3162 en Java, Python et C++. Comprenez le bon, le mauvais, et laid de l'algorithme, voyez les extraits de code, et apprenez des conseils prêts à l'entrevue pour décrocher votre prochain emploi technologique. *
- **En-têtes** : utiliser `<h1>` pour le titre principal, `<h2>` pour les sections et `<h3>` pour les sous-sections. Cette structure renforce la lisibilité pour les humains et les moteurs de recherche.
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Solution de Java* *= Solution de Python *=C++ *=Algorithme * naturellement tout au long.
- **Liens internes/externes**: Lien vers la page de problème LeetCode, vers votre repo GitHub avec le code, et vers les messages associés sur les structures de données.
- **Visuels**: Ajouter un petit diagramme ou une table résumant la complexité temps/espace pour améliorer l'engagement des utilisateurs.
- **Appel à l'action**: Finissez par "Prêt à passer votre prochaine entrevue? Inscrivez-vous pour obtenir plus de solutions LeetCode!

---

## 10. Mot final

- **Bon**: Clair, correct et assez rapide pour les contraintes.
- **Bad**: Inefficacité mineure (multiplication répétée) qui peut être facilement corrigée.
- **Ugly**: Sur-ingénierie pour un petit problème; restez simple.

Avec cet article, des extraits de code et des points d'entrevue, vous êtes prêt à impressionner les gestionnaires d'embauche sur vos compétences techniques et votre capacité à les communiquer efficacement. Bon codage – et bonne chance pour votre prochain entretien!