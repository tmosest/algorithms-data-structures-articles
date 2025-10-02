---
titre: LeetCode 2520. Comptez les chiffres qui divisent un nombre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2520. Compte les chiffres qui divisent un nombre
*LeetCode Easy – 100 % de rythme en Java*

### TL;DR
- **Objectif** : Comptez le nombre de chiffres de `num` divisés uniformément `num`.
- **Idée** : Extraire les chiffres un par un de la droite et la disvisibilité du test.
- **Complexité**: temps `O(log10 num)`, espace `O(1)` (constante).
- **Langues**: Java, Python, C++ – tous prêts à passer des extraits.

---

Déclaration de problème

> **Don** un entier "num" (1 ≤ num ≤ 109) qui contient **aucun zéro** chiffres,
> **Retour** le nombre de chiffres dans `num` qui divisent `num` uniformément (`num % chiffre == 0').

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
Autres `7`-1`-7 se divise. Autres
Chiffre `1` apparaît deux fois → 2.
"1248" Tous les chiffres divisent 1248. Autres

---

Pourquoi ce problème est-il une préparation à l'entrevue

- ** Astuce classique de traitement des chiffres** – apprendre à enlever les chiffres avec « % 10 » et « / 10 ».
- **Connaissance de cas** – pas de zéro chiffre → pas de division par zéro.
- **Découpage de l'espace-temps** – simple balayage linéaire, mémoire auxiliaire O(1).
- **Pratique en langage brut** – implémenter une fois, lire en Java, Python, C++.

---

Aperçu de la solution

1. **Tenir une copie** du numéro original (`original = num`).
2. **Loop** alors que `originale > 0'
- `digital = original % 10` – dernier chiffre.
- `original /= 10` – laisser tomber le dernier chiffre.
- Si `num % chiffre == 0`, incrément `count`.
3. Return `count`.

Parce que nous ne construisons jamais de chaîne ou de tableau, l'algorithme est efficace en mémoire.

---

Analyse de complexité

Formule métrique Résultat
C'est quoi, ça ?
Chaque boucle traite un chiffre décimal → `O(log10 num)`=10 itérations pour un int=32 bits
*Space *Seulement une poignée d'entiers Autres

---

Pièges communs & Gotchas

Erreur
- Oui.
*Essayez de convertir le nombre en une chaîne de caractères, puis itératif*. Utilisez des opérations numériques (`% 10`, `/ 10`) – plus rapides et plus idiomatiques. Autres
*Obligation de zéro dans la liste des chiffres*.Le problème ne garantit pas de zéros; si vous codez pour un cas générique, gardez-vous contre `numer == 0` pour éviter la division de zéro. Autres
*L'utilisation d'une approche récursive qui peut faire sauter la pile * , la boucle itérative est plus sûre pour les grands nombres. Autres

---

Numéro de code

Voici des solutions propres, prêtes à coller dans **Java, Python et C++**. N'hésitez pas à les copier, à les courir ou à les adapter pour votre préparation d'entrevue.

### Java

"Java
***
* LeetCode 2520: Comptez les chiffres qui divisent un nombre
* Temps O(log num), espace O(1)
*/
solution de classe {
Int public countDigits(int num) {
int original = num; // conserver le numéro d'origine pour les contrôles de divisibilité
= 0; // accumulateur de résultats

pendant que (original != 0) {
nombre int = origine % 10; // obtenir le dernier chiffre
original /= 10; // supprimer le dernier chiffre

si (num % chiffre) 0) {/ vérifier la disvisibilité
count++;
}
}
le nombre de retours;
}
}
«» "

Python

'`python
# LeetCode 2520: Comptez les chiffres qui divisent un nombre
Temps O(log num), espace O(1)

def countDigits(num: int) -> Int:
originale, nombre = num, 0
alors que original:
chiffre = original % 10
original//= 10
si nombre % chiffre == 0:
nombre += 1
Nombre de retours
«» "

C++

'`cpp
// LeetCode 2520: Comptez les chiffres qui divisent un nombre
// Temps O(log num), espace O(1)
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int countDigits(int num) {
int original = num;
nombre int = 0;
pendant que (original) {
chiffre int = origine % 10;
l'original /= 10;
si (num % chiffre) 0) + nombre;
}
le nombre de retours;
}
};
«» "

---

## C'est une promenade dans l'implémentation Java

1. ** Variables* *
- `original` conserve le `num` original.
- Le compte enregistre la réponse finale.

2. **Loop**
- `digit = original % 10' tire le chiffre le plus droit.
- `original /= 10` déplace le nombre à droite.
- Si le chiffre divise `num`, incrément `count`.

3. **Retour**
La boucle se termine lorsque `original` est zéro; `compte` détient maintenant le nombre de chiffres de division.

---

Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
**Bon**=Scan linéaire; espace constant; pas d'ops à cordes coûteux. Facile à comprendre; parfait pour les questions d'entrevue. Aucune – c'est une solution propre. Autres
Autres Si le nombre était très grand ( > 64 bits), vous auriez besoin de BigInteger. Le problème ne garantit pas de zéros, donc nous sautons zéro-vérification. Autres Si vous divisez accidentellement par zéro, le programme s'écrase. Autres
Le style du code peut être amélioré avec un retour anticipé pour les numéros à un chiffre. S/O S/O S/O

---

Comment ce blog vous aide à chasser votre emploi

- **Références clés**:
`LeetCode`, `Couvercle des chiffres qui divisent un nombre`, `codage interview`, `algorithme`, `Java solution`, `Python solution`, `C++ solution`, `O(log n) time`, `O(1) space`, `interview prep`, `software engineer interview`.
L'inclusion de ces termes dans votre curriculum vitæ ou votre portfolio renforcera la visibilité sur les moteurs de recherche des recruteurs.

- ** Démontrer un code propre** :
Les extraits présentent un code concis et prêt à la production, quelque chose que les recruteurs aiment.

- **Showcase Cross-Language Maîtrise** :
Fournir des solutions en plusieurs langues indique la polyvalence.

- **Discuses sur les causes et la complexité**:
Les intervieweurs apprécient les candidats qui pensent au rendement et aux pièges.

- **Ajouter un appel à l'action**:
Invitez les recruteurs à tester votre code sur LeetCode ou votre dépôt GitHub.

---

Prochaines étapes pour votre voyage d'entrevue

1. **Run le code sur LeetCode** – soumettre, vérifier votre runtime, et étudier la discussion pour plus de trucs.
2. **Créer un GitHub Gist** – coller les trois solutions, ajouter le lien de problème, et mentionner le défi.
3. **Blog About It** – publier un court article (comme celui-ci) sur Medium ou dev.to, tag `#LeetCode`, `#interview`, `#coding`.
4. **Appliquer pour les rôles** – utilisez le lien de blog dans votre Linked Dans le profil ou le curriculum vitæ sous Projet ou technique.

---

Dernier départ

Compter les chiffres qui divisent un nombre est un problème de LeetCode faussement simple qui vous enseigne:
- ** Extraction de division** par modulo/division.
- ** Invariant de boucle** et ** complexité temps/espace**.
- **Codage propre et linguistique**.

En la maîtrisant et en partageant votre solution dans un blog bien structuré, vous n'aurez pas seulement à répondre à cette question, mais aussi à élever votre marque personnelle en tant qu'ingénieur prévenant et prêt à l'entrevue. Bonne chance, et que votre code compile toujours!

---