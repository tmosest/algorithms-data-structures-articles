---
titre: LeetCode 1437. Vérifiez si tous les 1 sont au moins longueur K Places loin -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code de Leet 1437 – Vérifier si tous les 1s sont au moins longueur K endroits loin

Langue
C'est quoi ?
*Java * O(n) O(1)
*Python * O(n)
*C++ * O(n)

> **Pourquoi ce problème est important** – C'est une question d'entrevue classique qui teste *array traversal*, *edge-case handling* et *time-space compromis*. Mastering il vous donnera un point de discussion solide pour le codage des entretiens à Google, Amazon, Microsoft, et au-delà.

---

- Oui. 1. Exposé des problèmes

> **Given** un tableau binaire `nums` et un entier `k`, retourner **true** si chaque paire de 1s dans `nums` est au moins `k` positions séparées.
> **Retour** faux sinon.

Exemple

Entrée Sortie Explication
C'est pas vrai.
Chaque indice est ≥ 2 à part. Autres
Les deux derniers 1s ne sont qu'un indice à part. Autres

---

- Oui. 2. Intuition

- Oui. La condition ne peut échouer **quand deux 1 consécutives sont trop proches**.
- Oui. Donc nous devons juste nous rappeler **le dernier index où nous avons vu un 1** et, quand nous voyons un nouveau 1, vérifier la distance.

---

- Oui. 3. Algorithme (Scan linéaire)

1. **Initialiser** "dernier = ----" (ou "-1" pour indiquer "no 1 vu encore").
2. **Itérer** sur le tableau avec l'index « i » :
- Si "nums[i] == 1`:
- Si `i - last - 1 < k`, retourner `faux`.
- Réglez "dernier = i".
3. Après la boucle, retourner `true`.

- Oui. Pourquoi ça marche ?

- Oui. Le premier définit la dernière ligne de base.
- Chaque numéro suivant doit être au moins à zéro de k.
- La formule `i - last - 1` compte les zéros entre les deux 1s.
- Oui. Si un écart est plus petit que `k`, la règle est violée.

---

- Oui. 4. Mise en œuvre du code

### Java

"Java
solution de classe {
LenthApart(int[] nums, int k) {
int last = -1; // No 1 vu encore
pour (int i = 0; i < nombres de longueur; i++) {
si (nombres [i]] 1) {
si (i - dernier - 1 < k) { // Trop près ?
retourner faux;
}
dernier = i; // Dernière mise à jour vue 1
}
}
retour vrai; // Toutes les lacunes sont comblées
}
}
«» "

Python

'`python
Solution de classe:
def kLengthApart(self, nombres: List[int], k: int) -> C'est vrai.
dernier = -1 # Pas encore vu
pour i, val dans l'énumération(nombres):
si val == 1 :
i - last - 1 < k: # Gap trop petit
Retour Faux
dernier = i # Souvenez-vous de ceci 1
retour Vrai
«» "

C++

'`cpp
solution de classe {
public:
bool kLengthApart(vector<int>& nums, int k) {
int last = -1; // No 1 vu encore
pour (int i = 0; i < nums.size(); ++i) {
si (nombres [i]] 1) {
Si (i - la dernière - 1 < k) // Trop près
retourner faux;
dernier = i; // Dernière mise à jour vue 1
}
}
retour vrai; // Tous les écarts sont bons
}
};
«» "

Les trois solutions fonctionnent dans **O(n)** temps et utiliser **O(1)** espace supplémentaire.

---

- Oui. 5. Cas de bord et essais

Autres Essai
- C'est quoi ?
"[0,00,0]", `k=5`-No 1s → toujours `true`. Autres
"[1]", `k=0`. Autres
"[1,1]", `k=0`=1s adjacents autorisés (`k=0`) → `true`. Autres
= 1 < 2 → = « faux ». Autres

---

- Oui. 6. Variations et extensions

- **Variable k** – Le même code traite tout `k` (y compris 0).
- **Types de données multiples** – L'algorithme fonctionne avec n'importe quel tableau de valeurs 0/1.
- **Streaming input** – Seul le dernier index d'un 1 est nécessaire ; vous pouvez streamer le tableau si il est trop grand pour la mémoire.

---

- Oui. 7. Tendance des entrevues

C'est bien C'est mal
- C'est quoi ?
**Temps linéaire** – O(n) est le meilleur que vous pouvez faire pour un seul passage.** **Off‐by‐one erreurs** – N'oubliez pas de soustraire 1 en comptant les zéros.** **Sur-ingénierie** – Certains candidats ajoutent une file d'attente ou une liste de 1s, ce qui est inutile et augmente l'espace. Autres
** Variable unique** – "dernier" garde l'état ; mémoire minimale. N'oubliez pas les tableaux vides ou `k=0`. Autres
**Noms de variables clairs** – `lastSeenOne` ou `last` aide à la lecture. **Complexité confusion** – Soyez explicite que l'algorithme est O(n), pas O(n2). **Code dur à lire** – Des boucles trop imbriquées ou des fonctions d'aide inutiles peuvent confondre les intervieweurs. Autres

---

- Oui. 8. Article de blog optimisé SEO

> **Titre:** *Master LeetCode 1437: -Vérifier si tous les 1 , sont au moins longueur K Places à l'écart – Java, Python, C++ Solutions + Interview Insights*
> **Meta Description:** Découvrez comment résoudre LeetCode 1437 en Java, Python et C++ avec un algorithme O(n) rapide. Comprendre l'intuition, les cas de bord, et les conseils d'entrevue pour obtenir votre prochain travail de technologie.

---

Aperçu du problème

Le défi consiste à déterminer si chaque paire de 1s dans un tableau binaire est séparée par au moins `k` zéros. C'est un problème classique qui apparaît dans de nombreuses entrevues de codage.

> **Pourquoi c'est une chose à savoir* *
> • Droite mais profonde : teste votre compréhension des indices, des lacunes et de la manipulation des caisses.
> • Idéal pour le codage de tableau blanc parce qu'il peut être résolu en une seule boucle.
> • Démontre un style de codage propre – un point plus dans les entrevues.

---

La solution linéaire pour l'analyse

1. **Traitement du dernier 1**
- Initialiser `dernier = -1`.
- Lorsque vous rencontrez un 1 à l'index `i`, comparez `i - last - 1` à `k`.

2. ** Sortie précoce**
- Si l'écart est inférieur à `k`, retourner `faux` immédiatement.
- Sinon, régler `dernier = i` et continuer.

3. **Retour vrai** après la boucle si aucune violation n'a été constatée.

**Complexité temporelle:** `O(n)` – une passe sur le tableau.
**Complexité spatiale:** – un seul entier est stocké.

---

Les extraits de code

C'est vrai. Java

"Java
solution de classe {
LenthApart(int[] nums, int k) {
int last = -1;
pour (int i = 0; i < nombres de longueur; i++) {
si (nombres [i]] 1) {
si (i - dernier - 1 < k) retourner faux;
dernier = i;
}
}
retour vrai;
}
}
«» "

Python

'`python
Solution de classe:
def kLengthApart(self, nombres: List[int], k: int) -> C'est vrai.
Dernier = -1
pour i, val dans l'énumération(nombres):
si val == 1 :
i - dernier - 1 < k:
Retour Faux
dernier = i
retour Vrai
«» "

C++

'`cpp
solution de classe {
public:
bool kLengthApart(vector<int>& nums, int k) {
int last = -1;
pour (int i = 0; i < nums.size(); ++i) {
si (nombres [i]] 1) {
si (i - dernier - 1 < k) retourner faux;
dernier = i;
}
}
retour vrai;
}
};
«» "

---

Stratégie d'entrevue

- ** Expliquez votre intuition d'abord**: Nous ne nous soucions que de la distance entre les 1s consécutifs.
- **Afficher le code étape par étape** sur un tableau blanc, en mettant l'accent sur le décalage `-1`.
- **Discuss edge cases**: tableau vide, tous zéros, `k = 0`, élément unique.
- ** Analyse du temps et de l'espace**: Mettre en évidence le temps linéaire et l'espace constant.
- **Twist optionnel**: Demandez comment gérer l'entrée de streaming ou si le tableau est trop grand.

---

Conseils de bonus

Pourquoi ça aide ?
C'est quoi ?
**Utiliser des noms significatifs** ('lastOneIdx` vs `c`) Améliorer la lisibilité de l'intervieweur. Autres
**Début de la sortie**= Affiche que vous pouvez vous arrêter à la première panne, en économisant du temps. Autres
**Tests de l ' unité** Autres
**Mention les écueils de l'Aviation** Autres

---

Référence Mots clés

- LeetCode 1437
- Vérifiez si tous les 1 sont au moins longueur K endroits loin
- Solution Java LeetCode 1437
- Solution Python LeetCode 1437
- Solution C++ LeetCode 1437
- problème d'entretien de codage
- codage de la préparation des entretiens
- algorithme d'espacement des tableaux
- question d'entretien de tableau binaire

---

- Oui. 9. Pensée finale

LeetCode 1437 peut sembler simple, mais il s'agit d'un *micro-maîtrise* dans la manipulation de réseau, et le codage propre. Maîtrisez-le, écrivez quelques tests unitaires, et vous serez prêt à répondre à la question dans toute entrevue de codage. Bon codage ! C'est ce qu'il a dit