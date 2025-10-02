---
titre: LeetCode 3591. Vérifiez si un élément a la fréquence primaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3591 – Vérifiez si un élément a une fréquence préférentielle
* (facile)*

Langue Heure Espace
- C'est quoi ?
*Java * O(n)
*Python * O(n)
*C++ * O(n)

> **Pourquoi c'est important:**
> * Dans une interview, on vous demandera de compter les fréquences et ensuite de tester une propriété de ces comptages.
> * Ce problème est une question classique de fréquence + helper qui met en évidence vos connaissances de la structure des données et votre capacité à écrire des fonctions helper propres et efficaces (premier test).

---

1. Référence rapide – Code

### Java

"Java
Importer java.util. HashMap;

solution de classe publique {
contrôle public du booléenPrimeFréquence(int[] nombres) {
// Carte des fréquences
HashMap<entier, entier> freq = nouveau HashMap<>();
pour (int x : nombres) {
freq.put(x, freq.getOrDefault(x, 0) + 1);
}

// Aide à vérifier si un nombre est premier
pour (int count : freq.values()) {
si (isPrime(count)) retourne vrai;
}
retourner faux;
}

booléen privé estPrime(int n) {
si (n <= 1) retourner faux; // 1 et 0 ne sont pas prime
si (n <= 3) retourner true; // 2 et 3 sont prime
si (n % 2 == 0. 0) retourner faux;
pour (int i = 5; i * i <= n; i += 6) {
Si (n % i) = 0,0 n % (i + 2) 0) retourner faux;
}
retour vrai;
}
}
«» "

Python

'`python
Solution de classe:
Contrôle PrimeFrequence(self, nombres: List[int]) -> bool:
du comptoir d'importation des collections
freq = compteur(s)

def is_prime(n: int) -> C'est vrai.
si n <= 1: # 0 et 1 ne sont pas prime
Retour Faux
si n <= 3: # 2, 3
retour Vrai
si n % 2 == 0 ou n % 3 == 0:
Retour Faux
i = 5
alors que i * i <= n:
si n % i == 0 ou n % (i + 2)] 0:
Retour Faux
i += 6
retour Vrai

retourner n'importe quel(is_prime(c) pour c dans freq.values())
«» "

C++

'`cpp
solution de classe {
public:
Vérification de la fréquence des symptômes(vecteur<int>&nums) {
unordered_map<int, int> freq;
pour (int x : nombres) freq[x]++; // Fréquences de comptage

pour (auto &[val, cnt] : freq) {
si (isPrime(cnt)) retourne vrai; // Retour anticipé
}
retourner faux;
}

particulier:
n) {
si (n <= 1) retourner faux;
si (n <= 3) retourner vrai;
si (n % 2 == 0. 0) retourner faux;
pour (int i = 5; i * i <= n; i += 6) {
Si (n % i) = 0,0 n % (i + 2) 0) retourner faux;
}
retour vrai;
}
};
«» "

> **Note :**
> * Les trois implémentations utilisent le même modèle :
> * Construisez un dictionnaire/une carte de fréquence.
> * Scanner les fréquences et tester chaque primalité.
> * Le premier test est une optimisation classique de 6k ± 1.

---

2. Problème

Récapitulation du problème

> **Input** – Un tableau entier «nums» (1 ≤ «nums.longueur» ≤ 100, 0 ≤ «nums[i]» ≤ 100).
> **Output** – `true` si **any** élément dans le tableau apparaît un nombre premier de fois; sinon `false`.

- Oui. Principales observations

1. **Uniquement les fréquences sont importantes** – Les valeurs réelles en "nums" ne sont pas pertinentes une fois que nous savons combien de fois chaque apparaît.
2. **Small array** – Avec une longueur maximale de 100, la solution peut permettre des contrôles O(n2), mais nous visons toujours O(n).
3. ** Plage de test préliminaire** – Les fréquences peuvent varier de 1 à 100 (le pire cas : tous les éléments sont égaux). Donc une liste primaire précalculée ou une simple division d'essai est assez rapide.

Pièges communs

Mauvaise pratique Pourquoi il est mauvais
C'est pas vrai.
**Vérifier tous les entiers possibles en tant que premier** , Travail inutile pour 0‐100 , Utilisez une petite liste statique « {2,35,7} » ou une division d'essai rapide
**Itération à travers le tableau deux fois**
Autres **L'utilisation d'un contrôle primaire récursif**=Risque de débordement de la pile + frais généraux supplémentaires==Utilisez une boucle itérative avec sortie anticipée=

---

3. La rupture de la bonne, de la mauvaise et de la mauvaise

- Oui. Tant mieux. Ce que la solution fait bien

Description
- Oui.
**Temps linéaire**="O(n)" parce que nous traversons le tableau une fois pour compter et une fois pour vérifier. Autres
**Efficacité de l'espace** Autres
La fonction `isPrime()` est générique et peut être utilisée ailleurs. Autres
**Début de la recherche d'une fréquence primaire, nous arrêtons de scanner, ce qui nous permet de gagner du temps. Autres

- Oui. Mauvais – Où la solution pourrait encore s'améliorer

Description
- Oui.
**Liste primaire codée en dur**= Pour les plages d'entrée plus grandes, une liste statique devient insuffisante. Autres
**Ne pas mettre en cache les premiers résultats** Autres
Autres **Pas de validation de l'entrée**=Dans le code de production, vous devez vous garder des longueurs nulles ou négatives. Autres

### # Dégueulasse – Ce qui pourrait mal tourner si nous ignorons les cas de bord

Détail
- Oui.
Les contraintes interdisent cela, mais la programmation défensive retournerait "faux". Autres
**Les valeurs negatives**Les contraintes refusent, mais une vraie entrevue peut tester la robustesse. Autres
Autres **Nombres de fréquences plus grandes (≥105)**= Le test primaire actuel fonctionnerait encore, mais serait plus lent. Un tamis jusqu'à ØmaxFreq pourrait être plus rapide. Autres

---

4. Conseils de préparation à l'entrevue

1. ** Expliquez votre plan d'abord** – les fréquences de comptage -I-ll à l'aide d'une carte de hachage, puis vérifiez chaque nombre pour la primalité. (en milliers de dollars)
2. **Afficher un simple assistant `isPrime`** – Utilisez l'optimisation 6k±1; elle est courte et démontre la pensée algorithmique.
3. **Mention de sortie anticipée** – Dès que nous trouvons une fréquence de pointe, nous pouvons revenir vrai. (en milliers de dollars)
4. **Parler de cas de bord** – Si le tableau est tout distinct, chaque nombre est 1, ce qui n'est pas le premier. (en milliers de dollars)
5. **Si le temps le permet, discutez d'autres approches** – p. ex. pré-comptage d'un tamis de prime jusqu'à 100.

---

5. Bonus : Pourquoi ce problème est un bon CV

* ** Structures de données** – cartes Hash / tables de fréquence.
* ** Théorie du nombre** – Premier contrôle.
* ** compromis dans l'espace temporel** – Sortie anticipée, passage linéaire.
* ** Style de codage** – Fonctions d'aide propres, logique concise.

Lorsque vous discutez de cette solution sur Linked Dans ou pendant une entrevue, vous démontrerez :

- *Une bonne compréhension des algorithmes de base. *
- *Capacité d'écrire un code propre et durable. *
*Résoudre les problèmes pratiques en cas de contraintes. *

---

C'est pas vrai. Article du blog – Le bon, le mauvais et le mauvais problème de LeetCode 3591

Titre
**Le bon, le mauvais et le mauvais de LeetCode 3591 – Un guide prêt à l'emploi**

Description de la méta
Découvrez comment cracker le problème de LeetCode 3591 avec les solutions Java, Python et C++, ainsi que les informations d'entretien et les conseils pratiques pour stimuler votre CV technique.

Aperçu

1. **Hook** – A-t-on vu un problème qui est *presque* trivial mais caché derrière une torsion de nombre premier? (en milliers de dollars)
2. ** Résumé du problème** – Lecture rapide des contraintes et de l'exemple.
3. **Pourquoi ça compte** – Le comptage des fréquences est un point de départ dans les entrevues; les vérifications principales montrent la profondeur algorithmique.
4. **Le bon – Solution efficace** – Discuter algorithme linéaire, temps O(n), espace O(n).
5. **Le «Bad» – Miss communes** – Primes de codage dur, revérification des fréquences, ignorant la sortie anticipée.
6. **L'Ugly – Edge Cases & Defensive Coding** – Tableaux vides, nombres négatifs, grandes entrées.
7. ** Extraits de code complets** – Java, Python, C++ (comme indiqué ci-dessus).
8. **Interview-Ready Narrative** – Comment expliquer votre solution sur un tableau blanc.
9. **Resume Hook** – Mise en œuvre d'un contrôleur principal basé sur la fréquence en temps O(n). (en milliers de dollars)
10. **SEO Mots-clés** – LeetCode 3591, vérifier la fréquence primaire, le codage d'entrevue, l'analyse d'algorithme, les solutions Java Python C++, les conseils de reprise, la préparation d'entrevue de codage.
11. **Appeler à l'action** – Pratiquez ce problème, partagez votre solution et atterrissez ce travail !

- Oui. Extrait de blog

> **Les bonnes** –
> La clé d'une solution rapide est *compte-une, chèque-une.* Nous construisons une carte de hash des fréquences et puis itérer sur les comptes, s'arrêtant immédiatement quand nous avons atteint un premier. Cela nous donne un élégant algorithme O(n) avec des frais généraux minimes. (en milliers de dollars)
>
> **Les mauvais** –
> Beaucoup de candidats tombent dans le piège du codage dur d'une liste de petits premiers (2, 3, 5, 7). Bien que cela fonctionne pour les contraintes de LeetCode, il se casse si le tableau contient 100 fréquences de taille. Un test général est plus sûr et plus évolutif. (en milliers de dollars)
>
> **Les Ugly** –
> Et si le tableau est vide ou contient des nombres négatifs ? Les contraintes de LeetCode disent non, mais une fonction de production doit gérer ces gracieusement. Une vérification défensive au début peut enregistrer des bugs plus tard. (en milliers de dollars)

La pensée finale

> En maîtrisant ce problème de fréquence d'impulsion, vous ne vous contentez pas de résoudre un seul défi LeetCode – vous démontrez des compétences clés en interview : **fluence de la structure des données, optimisation algorithmique et codage défensif**. Combinez cette connaissance avec un CV poli qui met en valeur votre solution O(n), et vous aurez un avantage concurrentiel fort dans votre prochaine interview technique.

---

Référence rapide pour les chasseurs d'emplois

Autres Ce que cherchent les recruteurs
-- -- -- -- -- -- -- -- -- -- -- -- --
**Algorithmes performants**
**Clean code**
**Compréhension des problèmes**
**La communication technique**

Déposer un lien vers ce message sur votre LinkedIn, inclure le code dans une repo GitHub personnelle, et laisser le récit *Bon, mauvais, ugly* transformer votre interview en une histoire de réussite.

---

**Codage heureux, et meilleure de chance atterrissant votre travail de rêve!**

---

*© 2024 Codage Insights, Tous droits réservés. *

---

*Si vous souhaitez une plongée plus profonde dans l'optimisation de 6k ± 1 ou des solutions alternatives (comme un tamis d'Eratosthenes), faites-le moi savoir! *