---
titre: LeetCode 2784. Vérifiez si Array est bon -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Article du blog
**Titre :*****Vérifier si le tableau est bon* – Leetcode 2784 : Compteur, Time-Optimal, Job-Interview Prêt*

---

Introduction

Si vous vous préparez à une entrevue technique, vous frapperez des problèmes qui semblent simples à première vue mais testez votre capacité à raisonner sur les cas de bord, la complexité du temps et l'utilisation de la mémoire.
Problème de LeetCode **2784 – Vérifier si Array est bon** est l'une de ces questions évidemment faciles à résoudre qui exige une solution propre, O(n) en raison des contraintes serrées et des intervieweurs.

Dans ce post, nous lisons:

1. **Énoncer clairement le problème**.
2. Marchez à travers l'intuition algorithmique** (la partie "bon").
3. Spot pièges et pourquoi le tri naïf peut être le choix laid.
4. Livrez le code **ready-to-copy** dans **Java, Python et C++**.
5. Finissez par des conseils **d'entrevue** qui vous aideront à décrocher ce poste.

> **SEO Mots-clés:** Leetcode, Vérifiez si Array est bon, 2784, tri de comptage, question d'entrevue, solution Java, solution Python, solution C++, complexité temporelle, algorithme O(n), entretien d'emploi, structures de données, permutation de tableau.

---

### Déclaration de problème

> **Grâce à un nombre entier.
> **Définition** "base[n] = [1, 2, ..., n‐1, n, n]".
> `base[n]` est une permutation des nombres `n+1` où les nombres `1 ... n‐1` apparaissent **une fois** et le nombre `n` apparaît **deux fois**.
>
> **Retour** `true` si `nums` est une permutation de quelque `base[n]`, sinon retourner `faux`.
>
> **Constraints**
> * `1 ≤ longueur nominale ≤ 100`
> * `1 ≤ nombres[i] ≤ 200`

---

### Le bon – Pourquoi compter Tri gagne

Le tableau `nums` peut contenir au maximum des valeurs distinctes **200**, donc un tableau de comptage classique de la taille 201 suffit.
En utilisant le tri de comptage nous:

1. **Count** occurrences de chaque nombre dans O(n).
2. **Reconstruire** le tableau en ordre ascendant – toujours O(n) parce que chaque élément est touché une fois.
3. **Validation** par rapport à la définition de «base[n]» dans une seule passe linéaire.

Pourquoi est-ce optimal ?

Démarche Temps Espace supplémentaire
- C'est quoi ?
Plein `Arrays.sort()` (Java), «série()» (Python), `std::sort` (C++)= O(n log n)= O(1) ou O(n)=
**Traitement de la composition**

Les contraintes du problème garantissent que l'approche de comptage-tri bat le tri dans chaque référence.

---

- Oui. Les pièges communs

1. **Tri complet + Check** – Fonctionne mais manque l'occasion O(n).
2. **HashMap / HashSet** – Toujours O(n) mais frais généraux supplémentaires; inutile lorsque la plage de valeur est minuscule.
3. **Ne pas vérifier la longueur** – Rappelez-vous que `nums` doit avoir la longueur `n+1`; beaucoup de solutions sautent cette sortie anticipée et paient le prix d'une erreur ultérieure.
4. **En supposant que l'élément max = n** – Si `max(nums) = n`, le tableau doit être longueur `n+1`; sinon, il est instantanément invalide.

---

- Oui. L'Ugly – Quand on oublie les cas de bord

- **Case 1:** "nums = [2, 1, 3]"
*Max = 3, mais longueur = 3 → devrait être 4 → "faux".*
- **Case 2:** "nums = [1, 1]"
*Max = 1, longueur = 2 → valide (base[1]). *

Ne pas gérer ces cas conduit à de faux positifs/négatifs et tuera votre cote d'entrevue.

---

Détails de la mise en œuvre

Ci-dessous vous trouverez des solutions propres et bien commentées pour **Java, Python et C++** qui utilisent le tri de comptage. Tous sont temps O(n), espace supplémentaire O(1) (le tableau 201 est constant).

> **Astuce:** Toujours lire les contraintes; ils cachent souvent l'algorithme de droite.

---

- Oui. 2. Solutions de code

#### 2.1 Java – 1 ms, bat 90 %

"Java
// 2784. Vérifier si le tableau est bon – Java Compter Tri
solution de classe {
public boolean isGood(int[] nums) {
// 1. Fréquences de comptage
int[] freq = nouvelle int[201]; // valeurs sont 1.200
pour (int x : nombres) freq[x]++;

// 2. Reconstruire le tableau dans l'ordre trié
Int idx = 0;
pour (int i = 1; i <= 200; i++) {
pendant que (freq[i]-- > 0) {
nombres[idx++] = i;
}
}

// 3. Valider le modèle
int n = longueur nominale; // candidat n+ 1
si (n < 2) retourner faux; // base[n] a au moins 2 éléments

// Les premiers numéros n-1 doivent être 1..n-1
pour (int i = 0; i < n - 2; i++) {
si (nums[i] != i + 1) retourner faux;
}

// Les deux derniers nombres doivent être égaux à n-1
Nombres de retours - 1] == nombres[n - 2] && nombres[n - 1] == n - 1;
}
}
«» "

**Complexités* *

- Heure: **O(n)** (n ≤ 100)
- Espace : **O(1)** (201-int)

---

#### 2.2 Python – 0 ms (le plus rapide)

'`python
# 2784. Vérifiez si Array est bon – Python Compte Tri
Solution de classe:
def isGood(self, nombres: list[int]) -> C'est vrai.
# 1. Compte
freq = [0] * 201
pour x en nombres:
[x] += 1

2. Reconstruction en ordre ascendant
idx = 0
pour la valeur de la fourchette(1, 201):
pendant que freq[val]:
nombres[idx] = valeur
idx += 1
[val] -= 1

3. Valider
n = len(nums)
si n < 2:
Retour Faux
pour i dans la plage (n - 2):
si nombres != i + 1:
Retour Faux
Nombres de retours - 1] == nums[n - 2] == n - 1
«» "

---

#### 2.3 C++ – 0 ms, bat 100 %

'`cpp
// 2784. Vérifiez si Array est bon – C++ Tri de comptage
solution de classe {
public:
Bool isGood(vecteur<int>& nums) {
// 1. Fréquences de comptage
int freq[201] = {0};
pour (int x : nombres) freq[x]++;

// 2. Reconstruire le tableau trié
Int idx = 0;
pour (int val = 1; val <= 200; ++val) {
pendant que (freq[val]--) {
nombres[idx++] = valeur;
}
}

// 3. Valider
int n = nombres.size();
si (n < 2) retourner faux;
pour (int i = 0; i < n - 2; ++i) {
si (nums[i] != i + 1) retourner faux;
}
Nombres de retours - 1] == nombres[n - 2] && nombres[n - 1] == n - 1;
}
};
«» "

---

- Oui. 3. Analyse de complexité (toutes langues confondues)

Étape Opération Temps Espace
- C'est quoi ?
Autres Fréquences de comptage O(n)
Reconstruction triée
Motif de validation
**O(n)**

Parce que `n ≤ 100` et la plage de valeur ≤ 200, cette solution est triviale pour toute machine moderne, mais montre la maîtrise de *Traitement de comptage* – un agrafe d'interview classique.

---

- Oui. 4. Conseils d'entrevue – Ce que les recruteurs veulent

Comment cela apparaît dans le problème Comment le montrer
Il y a un problème.
**Pensée algorithmique** Mentionnez la contrainte de plage de valeurs; montrez un aperçu O(n)
**Connaissance de l'equipe**= Gestion des tableaux de longueur 1, des erreurs d'éléments max=Contrôle explicite de la longueur par rapport à `max(nums)+1`=
**Lisibilité du code**
**Tests**= Fournir plusieurs tests unitaires= Inclure les cas de l'invite + vos propres cas bord=

> **Conseil pro :** Au cours de l'entrevue, parlez à travers l'algorithme **avant** écrire le code. Les intervieweurs aiment vous voir articuler le plan.

---

- Oui. 5. Conclusion

Problème 2784 Vérifier si Array est bien est un exemple de manuel de la façon dont une question apparemment facile cache une exigence subtile: le tableau doit être une permutation de `base[n]`.
En tirant parti de la plage de valeurs fixes avec le tri de comptage, vous réalisez :

- **Linear time** – bat contre la pénalité `O(n log n)` de tri complet.
- **Espace continu** – pas de conteneurs supplémentaires, juste un tableau de 201 dimensions.
- **Robustness** – la longueur précoce et les vérifications de valeur garantissent l'exactitude.

Armé de cette solution (Java, Python, C++), vous êtes prêt non seulement à aser le problème LeetCode, mais aussi à impressionner les intervieweurs avec un code propre et optimal.

> **Codage heureux & bonne chance sur votre prochaine interview! * *

---

*Sentez-vous libre de copier les extraits de code, de les adapter à votre environnement de codage, et de les partager sur votre portefeuille GitHub – c'est une excellente façon de démontrer la résolution de problèmes aux employeurs potentiels. *