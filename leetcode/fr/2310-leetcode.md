---
titre: LeetCode 2310. Somme des nombres avec unités Digit K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2310. Somme des nombres avec unités Digit K
**Une solution complète et prête à l'interview en Java, Python et C++ + un billet de blog -- *

> * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *Solution Java*, *Solution Python*, *Solution C++*, *Entretien de codage*, *Ingénieur logiciel*, *Programmation dynamique*, *Greedy*, *Temps-complexité O(1)*

---

- Oui. 1. Exposé des problèmes

> On vous donne deux entiers `num` (0 ≤ num ≤ 3000) et `k` 0 ≤ k ≤ 9).
> Vous devez former un ensemble de **positif** entiers qui satisfait
> * chaque entier se termine par le chiffre `k` (chiffre des unités), et
> * la somme de tous les entiers est égale à "num".
> L'ensemble peut contenir des numéros dupliqués.
> Retourner la taille **minimum possible** d'un tel ensemble.
> Si un tel ensemble n'existe pas, retourner `-1`.
> Un jeu vide n'est autorisé que lorsque `num=0` (sa somme est 0).

---

- Oui. 2. Pourquoi ce problème est l'entrevue-Amis

Pourquoi ça compte ?
-- -- -- -- -- --
Autres **Simple Math + Observation**= Vous permet de tester le raisonnement sans structures de données lourdes. Autres
**Fixed Bound (10) ** Vous apprenez à exploiter la périodicité numérique pour effectuer la recherche. Autres
Autres **Edge-Case Heavy**=Entraîne la programmation défensive ( `k=0`, `num=0`, etc.). Autres
**Langues multiples**= Montres que vous pouvez traduire la logique entre Java, Python, C++. Autres

---

- Oui. 3. Aperçu de haut niveau

Pour tout entier qui se termine par le chiffre `k`, il peut être écrit `10 × x + k`.
Si nous choisissons `i` tels entiers, leur somme est `i × k + 10 × S` pour certains entiers `S`.
La seule chose qui compte est le nombre d'unités** de la somme: elle doit correspondre à "num % 10".
C'est pourquoi nous n'avons qu'à vérifier le plus petit "i"

«» "
i * k ≤ num (nous ne pouvons pas dépasser la somme cible)
i * k % 10 == num % 10 (unités correspondant au chiffre)
«» "

Parce que le chiffre des unités de `i × k` répète toutes les 10 valeurs de `i`, nous n'avons jamais besoin de
vérifier au-delà de «i = 10».
Ainsi, tout le problème se résume à une boucle à temps constant d'au plus 10 itérations.

---

- Oui. 4. Esquisse de preuve d'exactitude

1. **Si `num=0`** – l'ensemble vide satisfait à toutes les conditions; la taille 0 est minimale.
2. **Si une solution existe** avec la taille `i`, alors évidemment `i × k ≤ num` et les chiffres des unités correspondent, ainsi notre boucle le trouvera (ou un `i` plus tôt qui fonctionne aussi, donnant le vrai minimum).
3. **Si aucun `i` ≤ 10 ne satisfait aux deux conditions**, alors aucun `i` ≥ 11 ne peut non plus, car le motif des unités se répète toutes les 10 étapes. Ainsi, la réponse est `-1`.

Par conséquent, l'algorithme retourne la taille minimale lorsqu'elle existe, sinon `-1`.

---

- Oui. 5. Analyse de la complexité

Résultats
C'est quoi ?
**Heure**="O(1)" – au plus 10 itérations. Autres
**Espace** – seulement quelques variables entières. Autres

---

- Oui. 6. Cas de bord

Scénario Ce qui se passe
C'est pas vrai.
- Oui. 0 '' Retour `0 '. Autres
- Oui. Seuls les multiples de 10 sont réalisables. La boucle fonctionne toujours; elle retourne `1` si `num % 10 == 0`, sinon `-1`. Autres
La condition de boucle `i * k <= num` échoue immédiatement; répondez `-1`. Autres
"num > 3000" Non autorisé par les contraintes. Autres
5 ' et ' num ' 5 '' Fonctionne; retourne `1'. Autres
"k" et "num" 1 '' Aucune solution → `-1 '. Autres

---

- Oui. 7. Code (Java, Python, C++)

### Java

"Java
solution de classe {
Nombres (int num, int k) {
Si (nombre) 0) retour 0; // Ensemble vide
pour (int i = 1; i * k <= num && i <= 10; i++) {
si (k * i) % 10 == num % 10) {
retour i; // Plus petit i qui fonctionne
}
}
retour -1; // Pas de jeu valide
}
}
«» "

Python

'`python
Solution de classe:
def minimumNumbers(self, num: int, k: int) -> Int:
si num] 0:
retour 0
pour i dans la plage (1, 11): # 1..10
i k * i % 10 == num % 10 et i * k <= num:
retour
retour -1
«» "

C++

'`cpp
solution de classe {
public:
int minimumNombres(int num, int k) {
Si (nombre) 0) retour 0;
pour (int i = 1; i * k <= num && i <= 10; ++i) {
si (k * i) % 10 == num % 10) retourne i;
}
retour -1;
}
};
«» "

---

- Oui. 8. Le bon, le mauvais, le mauvais

Aspect du bien
- C'est quoi ?
**Simplicité algorithmique**=1 boucle O, pas de DP, pas de structures de données==Peut sembler trivial, mais manquant de subtils chiffres-périodicité peut conduire à une solution O(num)===0.
Autres **Couverture d'un cas par l'Edge** 0` fonctionne toujours quand `num % 10 == Ne pas vérifier `i * k <= num` peut produire des réponses incorrectes (sur-summing)
**Readability**= Effacer les noms de variables (`i`, `k`, `num`) et les commentaires===Le surcommentage peut encombrer le code=== Écriture d'une seule ligne `si (k*i%10==num%10 && i*k<=num) retourne i===' semble intelligent mais cache l'intention===
**Les quirks spécifiques à la langue**

---

- Oui. 9. Conseils d'entrevue

1. ** Expliquez la périodicité** – dites pourquoi 10 suffit.
2. **Discuss ledge case first** – `num=0`, `k=0`.
3. ** Temps/espace** explicitement – l'intervieweur aime les revendications O(1).
4. **Afficher l'alternative** – une approche rapide ou gourmande (pour montrer la profondeur).
5. **Parler des tests** – donner des exemples de `num=58,k=9`, `num=37,k=2`, `num=0,k=7`.

---

- Oui. 10. Conclusion

Ce problème de Leetcode démontre comment une question apparemment ouverte peut être résolue en temps constant en exploitant la nature périodique des chiffres décimales.
La clé à emporter : ** chercher toujours des motifs cachés** qui peuvent réduire un espace de recherche potentiellement grand à une petite boucle fixe.
Maîtriser cette astuce non seulement vous permet de trouver une solution correcte, mais montre aussi aux intervieweurs que vous pouvez repérer des raccourcis élégants – un trait à chaque convoitise d'ingénieur senior.

Bon codage, et que votre prochaine entrevue soit aussi lisse que cette boucle 10-itération!