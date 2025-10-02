---
titre: LeetCode 2743. Compter les sous-chaînes sans répéter le caractère -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2743. Comptez les sous-chaînes sans répéter les caractères – -Le bon, le mauvais, et le mauvais

> **Problème**
> Compter toutes les sous-chaînes *spéciales* – celles qui ne contiennent pas de caractère répétitif**.

> **Exemples**
> • `abcd` → 10
> • `ooo` → 3
> • `bab` → 7

> **Objectif**
> Fournissez une solution **O(n)** dans **Java, Python et C++**, un message concis **blog** avec des mots-clés SEO-friendly, et un coup d'œil aux pièges (les .

---

Pourquoi ce problème est une question d'entrevue dorée

**Aspect**
- C'est pas vrai.
**Fenêtre coulissante**=Le modèle classique à deux points; chaque sous-chaîne candidate est inspectée exactement une fois. Autres
**Complexité temporelle**= O(n) est optimal; toute approche plus lente est un drapeau rouge. Autres
Autres **Complexité spatiale**= O(1) (seulement 26 int) – démontre une connaissance des compromis entre l'espace et le temps. Autres
Autres **Cas d'Edge** Autres

> **Mots clés**: *sous-chaînes, fenêtre coulissante, deux pointeurs, traitement des chaînes, problème d'entretien, algorithme O(n), Java, Python, C++*

---

Le bon : une mise en œuvre propre de la fenêtre coulissante

Intuition

Nous étendons une fenêtre `[gauche ... droite]` tandis que les caractères à l'intérieur sont uniques.
Quand un duplicata apparaît, nous réduisons la fenêtre de gauche jusqu'à ce que le duplicata disparaisse.
Toutes les sous-chaînes qui se terminent à `droite` et commencent n'importe où entre `gauche` et `droite` sont valides, nous ajoutons `(droite - gauche + 1)` à la réponse.

- Oui. Structures de données de base

**Taille**
- C'est quoi ?
Autres Java, C++-int[26]-Constante
Liste de Python

> Le tableau indexe le nombre de chaque lettre minuscule; 26 est une constante, donc l'espace est **O(1)**.

Code Pseudo

«» "
nombre[26] = {0}
gauche = 0
réponse = 0

pour droite dans 0 ... n-1:
nombre[s[droit]] += 1

pendant le compte[s[droit]] > 1: # duplicata trouvé
nombre[s[gauche]] -= 1
gauche += 1

réponse += droite - gauche + 1

réponse de retour
«» "

La boucle tourne **once** par caractère pour les deux pointeurs – **O(n)** time.

---

Code

Voici des solutions idiomatiques pour les trois langues demandées.

- Oui. **Java**

"Java
solution de classe {
Nombre d'entrées publiques de sous-chaînes spéciales (chaînes s) {
int[] freq = nouveau int[26];
int gauche = 0, ans = 0;

pour (int droite = 0; droite < s.longueur(); droite++) {
freq[s.charAt(right) - 'a']++;

pendant que (freq[s.charAt(à droite) - 'a'] > 1) {
freq[s.charA (à gauche) - 'a']--;
gauche++;
}

ans += droite - gauche + 1;
}
le retour des an;
}
}
«» "

> **Complexités**
> * Heure* : **O(n)* *
> *Espace*: **O(1)**

---

- Oui. **Python**

'`python
Solution de classe:
def numberOfSpecialSubstrings(self, s: str) -> Int:
freq = [0] * 26
gauche = 0
ans = 0

pour droite, ch en énumération(s):
idx = ord(ch) - 97
freq[idx] += 1

pendant que freq[idx] > 1 :
freq[ord(s[gauche]) - 97] -= 1
gauche += 1

ans += droite - gauche + 1
retour et
«» "

> **Complexités**
> * Heure* : **O(n)* *
> *Espace*: **O(1)**

---

- Oui. **C++**

'`cpp
solution de classe {
public:
Numéro int DeSpecialSubstrings(string s) {
tableau <int, 26> freq{};
int gauche = 0, ans = 0;

pour (int droite = 0; right < (int)s.size(); ++right) {
freq[s[right] - 'a']++;

pendant que (freq[s[right] - 'a'] > 1) {
freq[s[gauche] - 'a']--;
+ + gauche;
}

ans += droite - gauche + 1;
}
le retour des an;
}
};
«» "

> **Complexités**
> * Heure* : **O(n)* *
> *Espace*: **O(1)**

---

Les mauvaises: pièges communs

Pourquoi il fait défaut
- C'est quoi ?
Utiliser `String.contient()` ou regex pour vérifier les duplicatas.
Autres Oubliant de réinitialiser `freq` lors de la réduction de la fenêtre. avant de déplacer "gauche"
En utilisant `HashSet` pour chaque pointeur droit (réinsérer tous les caractères)

Exemple

"Java
pour (int right = 0; right < n; right++) {
Set<Caracter> vu = nouveau HashSet<>();
pour (int i = droite; i >= 0; i--) {
si (!see.add(s.charAt(i))) pause;
as++;
}
}
«» "

> **Complexité**: O(n2) – inacceptable pour n = 105.

---

La folie : Pièges

1. **Tous les caractères identiques** ("aaaaa").
*Expecté* : le nombre correspond à la longueur de la chaîne (seulement les sous-chaînes de longueur-1).
*Bogue commune* : le fait de ne pas réduire correctement la fenêtre entraîne un surcompte énorme.

2. **Longueur maximale** (`n = 105`).
* Limite de mémoire* : Un tableau 2-D ou une liste de listes est trop lourd.
*Solution* : Gardez le tableau de fréquences de taille constante.

3. **Mix de majuscules et minuscules** (bien que le problème garantisse les minuscules).
*Bug*: le calcul de l'indice `s[i] - 'a' devient négatif.
*Check*: Valider l'entrée ou utiliser `Caracter.toLowerCase`.

4. **Input non-ASCII** (rare).
*Fix*: Utiliser des points de code Unicode ou limiter `a``z`.

---

Résumé optimisé du SEO

- **Titre**: 2743 Sous-chaînes de comptage sans répétition de caractères – O(n) Guide de fenêtre coulissante (Java, Python, C++)
- **Description de la Meta**: LeetCode 2743 de Master avec une solution de fenêtre coulissante O(n) propre. Apprenez les pièges, les cas de bord et comment aser les problèmes d'interview de chaîne en Java, Python et C++. (en milliers de dollars)
- **Mots-clés principaux**: *LeetCode 2743, sous-chaînes de compte, fenêtre coulissante, chaîne sans duplicatas, algorithme d'entretien, solution Java, solution Python, solution C++
- **Mots-clés secondaires**: *deux pointeurs, carte de hachage, O(n) temps, espace constant, cas de bord, conseils d'entrevue*

---

Plan d'étude rapide (30 minutes)

Étape
- Oui.
Autres 1. Lire l'énoncé du problème (5 min)
Autres 2. Pensez à la fenêtre coulissante, projet de pseudocode (5 min)
Autres 3. Écrire le code Java, exécuter des tests (10 min)
Autres 4. Traduire en Python & C++ (5 min)
Autres 5. Examen des pièges, des cas de bord (5 min)

> **Résultat**: Une solution polie et prête à l'entrevue + un billet de blog que vous pouvez copier dans LinkedIn, Medium ou un site personnel.

---

À emporter

- **Bon**: Une fenêtre coulissante, espace constant, calcul clair.
- **Bad**: Approches quadratiques, mauvaise maintenance des fenêtres.
- **Ugly**: Mauvais traitement des dossiers, suringénierie.

> **Si vous pouvez expliquer les trois colonnes ci-dessus et coller l'un des extraits de code, vous impressionnerez n'importe quel gestionnaire d'embauche. * *

Bon codage, et bonne chance avec votre prochaine interview! C'est ce qu'il a dit