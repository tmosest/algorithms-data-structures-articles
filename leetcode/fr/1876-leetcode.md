---
titre: LeetCode 1876. Sous-chaînes de taille trois avec caractères distincts - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1876. Sous-chaînes de taille trois avec caractères distincts
### Un guide étape par étape – Java, Python & C++ – avec un article de blog prêt à travailler

> **Objectif :** Compter combien de sous-chaînes contiguës de longueur 3 dans une chaîne contiennent *trois caractères distincts* (pas de répétitions).

> **Pourquoi ça compte :**
> - LeetCode #1876 est une question d'entrevue commune.
> - Le problème teste votre compréhension de *fenêtres coulissantes* et *temps-espace compromis*.
> - La maîtrise augmente votre score sur les plateformes de codage-entrevue et vous donne un point de conversation pour les recruteurs.

Ci-dessous vous trouverez:

1. La déclaration du problème** (en anglais).
2. Une solution **sliding-window** dans **Java, Python et C++**.
3. A **blog-style write-up** qui explore le bon, le mauvais, et le laid du problème – SEO-optimisé pour les recruteurs.

N'hésitez pas à copier-coller le code dans votre IDE, à lancer les cas de test et à utiliser le brouillon du blog pour présenter votre processus de résolution de problèmes sur LinkedIn, Medium ou un portfolio personnel.

---

- Oui. 1. Exposé des problèmes (en français)

> **Input** – une chaîne de caractères en caractères anglais minuscules, longueur 1 ≤ ≤ 100.
> ** Sortie** – le nombre de sous-chaînes de longueur 3 qui ont *trois caractères uniques*.
> Chaque fenêtre recoupante compte séparément, même si le texte de la sous-chaîne est identique.

**Exemple**

«» "
Entrée : "xyzzaz"
Sous-chaînes de longueur 3 : ["xyz", "yzz", "zza", "zaz"]
Bonnes (pas de répétitions) : ["xyz"] → réponse = 1
«» "

---

- Oui. 2. Solution de fenêtre coulissante

Parce que la taille de la fenêtre est *fixée à 3*, nous pouvons déplacer une fenêtre coulissante sur la corde une fois.
Pour chaque fenêtre, nous effectuons trois comparaisons à temps constant :

Texte
si s[l] != s[m] et s[l] != s[r] et s[m] != s[r]
«» "

Si le test passe, nous incrémentons le compteur.
Nous coulissons la fenêtre en incrémentant les trois indices (ou simplement en itérant `i` de 0 à `len(s)-3` et en cochant `s[i]`, `s[i+1]`, `s[i+2]`).

Complexité

**Exploitation**
- C'est quoi ?
Illération sur toutes les fenêtres

`n` = longueur de `s`.
L'algorithme est linéaire et utilise une mémoire supplémentaire constante.

---

- Oui. Mise en œuvre Java

"Java
// Java 17
solution de classe publique {
Nombre d'entrées publiques Sous-chaînes Good(String s) {
nombre int = 0;
// Pas besoin de copier la chaîne dans un tableau de caractères – charAt est O(1).
pour (int i = 0; i + 2 < s.longueur(); i++) {
char a = s.charAt(i);
char b = s.charAt(i + 1);
char c = s.charAt(i + 2);
si (a != b && a!= c && b!= c) {
count++;
}
}
le nombre de retours;
}
}
«» "

> **Pourquoi pas de tableau? **
> La conversion en un `char[]` est *O(n)* travail et mémoire supplémentaires.
> L'utilisation de `charAt()` maintient la solution maigre.

---

Mise en œuvre de Python

'`python
# Python 3
Solution de classe:
def countGoodSubstrings(self, s: str) -> Int:
nombre = 0
pour i dans la plage(len(s) - 2):
a, b, c = s[i], s[i+1], s[i+2]
si a != b et a != c et b != c:
nombre += 1
Nombre de retours
«» "

> Le slice Python's pourrait être utilisé (`s[i:i+3]`), mais il alloue une nouvelle chaîne à chaque fois – on évite cela pour la mémoire O(1).

---

C++ Mise en œuvre

'`cpp
// C++17
solution de classe {
public:
Int countGoodSubstrings(string s) {
nombre int = 0;
pour (size_t i = 0; i + 2 < s.size(); ++i) {
Char a = s[i];
char b = s[i + 1];
c = s[i + 2];
si (a != b && a!= c && b!= c) {
+ nombre;
}
}
le nombre de retours;
}
};
«» "

> L'utilisation de `size_t` empêche les avertissements non signés et gère avec grâce la taille maximale d'entrée.

---

- Oui. 3. Écrire un blog En haut : le bon, le mauvais, et le mauvais

> **Titre (friendly SEO):** *Maîtrise du LeetCode 1876 – Compter de bonnes sous-chaînes de longueur trois (Java/Python/C++) – Un guide d'entrevue complet*
> **Méta—Description:** * Apprenez à résoudre le LeetCode #1876 – Sous-chaînes de taille trois avec des caractères distincts. Trouvez des solutions Java, Python et C++, comprenez les fenêtres coulissantes, et augmentez votre score d'entrevue de codage. *

---

Introduction

Dans le monde des interviews techniques, *LeetCode 1876* est un problème préféré de "quick-fire".
Malgré sa simplicité, il révèle des nuances subtiles : il faut penser à *des fenêtres de taille fixe*, *des sous-chaînes de recouvrement* et *des comparaisons de temps constants*.

Ci-dessous, nous disséquons le problème, présentons une solution propre dans trois langues principales, et partageons les compromis cachés recruteurs aiment sonder.

---

C'est vrai. Le problème en coque

Compter le nombre de sous-chaînes contiguës de **exactement trois** caractères qui contiennent **pas de caractères en double**.

Pourquoi 3 ? *
Comme la taille de la fenêtre est fixe, nous pouvons utiliser une approche *gliding-window* qui fonctionne dans le temps linéaire.

---

### Le "Bien" – Ce qui fait Ce problème est grand

1. **Clarté des contraintes**
- Petite taille d'entrée (= 100) signifie que nous pouvons nous permettre O(n2) si nécessaire, mais la solution optimale O(n) est triviale.
- La taille fixe de la fenêtre élimine le besoin de programmation dynamique ou de boucles imbriquées.

2. **Focus sur les concepts fondamentaux* *
- *La technique de la fenêtre coulissante* est un élément essentiel des entrevues.
- *Set* utilisation vs *index comparaison* présente deux façons de vérifier l'unicité.

3. **Essais précis**
- Facile à créer des essais de cas de bord (`"aaa"`, `"abc"`, `"abcd"`).
- Résultats reproductibles dans les langues.

---

- Oui. Les pièges qui peuvent vous faire monter

Pourquoi ça arrive ?
C'est ce qu'on dit.
Autres Conversion en un `char[]` Utiliser `charAt()` (Java) ou l'indexation directe (Python/C++) Autres
Oubliez que le dernier index de démarrage valide est `len-3`" `pour (i = 0; i + 2 < len; ++i)`"
En supposant qu'un jeu est nécessaire , utiliser un jeu pour chaque fenêtre est surkill , comparaison simple par paire est O(1) ,
Oublier les sous-chaînes recoupantes En comptant seulement les sous-chaînes uniques manque des duplicatas Chaque fenêtre compte séparément

---

- Oui. La complexité cachée

Numéro d'information Impact d'information Meilleures pratiques
- C'est quoi ?
**Offre de l'espace-temps** O(n) espace.
Même si les contraintes sont petites, un entretien peut demander ""s" ≤ 105" Toujours linéaire, mais veillez à ce que le nombre d'entiers déborde (`int` vs `long`) Autres
**Language-specific quirks**=Python=s sliceing alloue de nouvelles chaînes==Utilisez l'indexation ou `memoryview` si la performance compte==

---

Code Passage

> Les versions Python & C++ suivent la même logique.

"Java
solution de classe publique {
Nombre d'entrées publiques Sous-chaînes Good(String s) {
nombre int = 0;
// Fenêtre coulissante: index de démarrage i, fenêtre est s[i], s[i+1], s[i+2]
pour (int i = 0; i + 2 < s.longueur(); i++) {
char a = s.charAt(i);
char b = s.charAt(i + 1);
char c = s.charAt(i + 2);
// Trois vérifications distinctes par paire
si (a != b && a!= c && b!= c) {
count++;
}
}
le nombre de retours;
}
}
«» "

**Qu'est-ce qui se passe? **

1. ** Limites de boucle** – `i + 2 < s.longueur()` garantit que la fenêtre ne sort jamais des limites.
2. **Accès direct au char** – `charAt` est O(1) en Java.
3. **Trois comparaisons** – chacune d'elles est une opération à temps constant; aucune recherche de réglage ou de hachage.
4. ** Compteur d'encre** – chaque bonne sous-chaîne est comptée, même si elle est identique.

La même logique s'applique dans Python (`s[i]`, `s[i+1]`, `s[i+2]`) et C++ (`s[i]`, `s[i+1]`, `s[i+2]`).

---

D'autres approches (pour s'amuser)

L'approche La complexité Quand utiliser
C'est pas vrai.
**HashSet par fenêtre** Si la taille de la fenêtre est variable ou plus grande; moins efficace pour fixe 3
**Bitmask**. O(n) time, O(1) space.
** Expression régulière**= O(n) temps, espace O(1) (si le moteur regex est linéaire)=Hack rapide dans les langages de script=

---

Ce que les recruteurs recherchent

Compétence
C'est quoi ?
**La pensée algorithmique** Autres
**Attention au détail**
**Codage du style**
**Analyse des problèmes**

> *Astuce:* Dans une interview, après avoir présenté le code, expliquer brièvement le *pourquoi* derrière chaque décision. Les recruteurs aiment les candidats qui peuvent justifier leurs choix.

---

Les pensées finales

LeetCode 1876 est trompeurment simple mais emballe les thèmes d'entrevue essentiels:

- **Fenêtre coulissante** (taille fixe).
- ** Contrôles d'utilité** sans structures de données lourdes.
- **Conscience d'Edge-case** (overlaps, cordes à caractère unique).

La maîtrise de ce problème démontre votre capacité à traduire une exigence claire en code propre et efficace – exactement ce que veulent les gestionnaires d'embauche.

> **Prochaine étape :** Variantes de pratique :
> - Sous-chaînes de taille K avec caractères distincts (généraliser à n'importe quel K).
> - Count les sous-chaînes avec au plus des caractères K distincts. (en milliers de dollars)
> - Trouver la plus longue sous-chaîne avec des caractères distincts. (en milliers de dollars)

Bonne chance, et le codage heureux!

---

- Oui. 4. Article de blogue prêt à publier (Marquage)

```markdown
# Mastering LeetCode 1876 – Compte de bonnes sous-chaînes de longueur trois (Java/Python/C++)

**LeetCode #1876** – *Sous-chaînes de taille trois avec caractères distincts*
_Un guide d'entrevue complet avec des solutions, des compromis et des idées favorables au référencement._

---

Aperçu du problème

- **Input**: chaîne `s` (1 ≤ ≤ ≤ 100), lettres minuscules.
- **Output** : nombre de sous-chaînes **contituelles** 3 caractères qui contiennent **pas de duplicata**.
- Pourquoi ? Parce que la taille de la fenêtre est fixe → nous pouvons la glisser dans le temps O(n).

---

Solution optimale: Fenêtre coulissante

Langue
- C'est quoi ?
Java O(n)
Python O(n)
O(n)

**Idée clé**: Pour chaque indice de départ `i`, examiner `s[i]`, `s[i+1]`, `s[i+2]`.
Si les trois sont séparés par paire, incrémentez le compteur.

---

Numéro de code

### Java

"Java
solution de classe publique {
Nombre d'entrées publiques Sous-chaînes Good(String s) {
nombre int = 0;
pour (int i = 0; i + 2 < s.longueur(); i++) {
char a = s.charAt(i);
char b = s.charAt(i + 1);
char c = s.charAt(i + 2);
si (a != b && a != c && b != c) nombre++;
}
le nombre de retours;
}
}
«» "

Python

'`python
Solution de classe:
def countGoodSubstrings(self, s: str) -> Int:
nombre = 0
pour i dans la plage(len(s)-2):
a, b, c = s[i], s[i+1], s[i+2]
si a != b et a != c et b != c:
nombre += 1
Nombre de retours
«» "

C++

'`cpp
solution de classe {
public:
Int countGoodSubstrings(string s) {
nombre int = 0;
pour (size_t i = 0; i + 2 < s.size(); ++i) {
char a = s[i], b = s[i+1], c = s[i+2];
si (a != b && a != c && b!= c) ++compte;
}
le nombre de retours;
}
};
«» "

---

## -Offs d'échange et conseils d'entrevue

- Utiliser **indexage direct**; éviter les copies inutiles de «char[]».
- Souvenez-vous des limites de boucle : le dernier index de démarrage est "len-3".
- Les comparaisons par paires (`a!=b && a!=c && b!=c`) sont plus rapides que l'utilisation d'un ensemble.
- Discuter des cas de bord: `"aaa"` → 0, `"abc"` → 1, `"abcd"` → 2.

---

Liste de contrôle du recruteur

Compétence Ce que veulent les recruteurs
-- -- -- -- -- ------------------ -- -- --
Identifier la fenêtre coulissante
Autres Lisibilité du code
Explication des cas de bord, temps/espace

---

Les variations dans la pratique

1. Sous-chaînes de taille `K` avec caractères distincts.
2. Sous-chaînes avec *au maximum* `K` caractères distincts.
3. La plus longue sous-chaîne avec tous les caractères distincts.

---

> * Conseil pro* : Après le codage, passez par la logique : pourquoi avez-vous choisi cette approche ? Comment ça va ? Les recruteurs aiment les justifications.

---

Mot final

LeetCode 1876 est un **micro-problème** qui présente les macro-compétences.
Résolvez-le efficacement, expliquez votre raisonnement, et vous brillerez dans votre prochain entretien technique.

Bon codage ! C'est vrai.

---

*Auteur: [Votre nom] – Ingénieur logiciel, Interview Prep Enthusiast
«» "

> Enregistrez le balisage ci-dessus dans un fichier `.md` ou collez dans votre plateforme de blog. Il est déjà optimisé pour **mots-clés** comme *LeetCode 1876*, *bonnes sous-chaînes*, *solution Java*, *solution Python*, *solution C++*, *guide d'entrevue*.

---

- Oui. 5. Cas d ' épreuve rapide

Texte
Produit prévu
Autres
"aaa"
"abc" 1
"abcd" 2
"abca" 1
"abcaab" 2
"abcdefghijklmnopqrstuvwxyz"
«» "

Les trois implémentations produisent des résultats identiques.

---

> **Wrap-up**: Gardez les extraits de code prêts dans votre IDE, pratiquez l'explication du *Why*, et utilisez le billet de blog comme une pièce de portfolio pour votre site Web personnel ou des articles LinkedIn. Joyeux entretien !
«» "

---

** Félicitations!**
Vous avez maintenant :

1. ** Solutions linguistiques optimisées** pour LeetCode 1876.
2. **Un billet de blog prêt à être publié** qui est convivial pour le SEO et le recruteur.
3. **Insights** dans les pièges subtils recruteurs aiment tester.

Allez et as cette interview ! C'est ce qu'il a dit.
«» "

---

* Fin du document*