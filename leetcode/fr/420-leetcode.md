---
Titre: LeetCode 420. Vérification de mot de passe forte -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# C'est la maîtrise de Leetcode 420 – Vérification de mot de passe forte
> Le bon, le mauvais et le laid** de résoudre un problème d'interview difficile

---

TL;DR

- **Problème**: Étapes minimales pour faire un mot de passe fort (longueur 6-20, 1 inférieure, 1 supérieure, 1 chiffre, no 3-in-a-row).
- **Idée de solution**:
1. Compter les types de caractères manquants.
2. Trouver des séquences répétitives (`len >= 3`) et noter combien de remplacements ils ont besoin.
3. Traiter **longueur** comme la principale contrainte :
- Si trop court → insertions dominent.
- Si trop longtemps → suppressions aident à réduire les répétitions.
4. Fusionner les trois compte de façon optimale.
- **Résultat**: O(n) temps, O(1) espace supplémentaire.

Ci-dessous vous trouverez **implémentations complètes** dans **Java, Python, et C++**, suivi d'un article **blog-ready** qui explique la logique, discute des pièges, et montre comment clouer l'interview.

---

- Oui. 1. Mise en œuvre Java

"Java
solution de classe {
secteur public PasswordChecker(Mot de passe fixe) {
int n = mot de passe.longueur();
booléen hasLower = false, hasUpper = false, hasDigit = false;

// 1. Identifier les types de caractères manquants
pour (int i = 0; i < n; i++) {
char c = mot de passe.charAt(i);
si (Caracter.isLowerCase(c)) hasLower = true;
sinon si (Caracter.isUpperCase(c)) aUpper = true;
sinon si (Caracter.isDigit(c)) hasDigit = true;
}
Int manquant Types = (hasLower ? 0 : 1) + (hasUpper ? 0 : 1) + (hasDigit ? 0 : 1);

// 2. Trouver des séquences répétées et combien de remplacements ils ont besoin
remplacement int = 0; // remplacements totaux nécessaires pour les répétitions
int[] len = nouveau int[n / 3 + 1]; // nombre de répétitions mod 3 (0,1,2)
pour (int i = 0, nombre = 1; i < n; i++) {
i (i + 1 < n && mot de passe. CharAt(i) == mot de passe.charAt(i + 1)) {
count++;
} autre {
si (compter >= 3) {
remplacer += nombre / 3;
len[compte % 3]++;
}
nombre = 1;
}
}

si (n < 6) {
// Trop court – les insertions dominent
retour Math.max(types manquants, 6 - n);
} sinon si (n <= 20) {
// Longueur OK – remplacements uniquement nécessaires
retour Math.max(MissingTypes, remplacer);
} autre {
// Trop longtemps – les suppressions aident à réduire les remplacements
int sur = n - 20;
// Utiliser les suppressions sur les répétitions avec le mod 0 d'abord
Int del = Math.min(over, len[0]);
remplacer -= del;
-= del;
// Puis sur mod 1 répète
del = Math.min(over, len[1] * 2) / 2;
remplacer -= del;
-= del * 2;
// Enfin sur les répétitions du mod 2
del = Math.min(over, len[2] * 3) / 3;
remplacer -= del;
-= del * 3;
// Après toutes les suppressions
retour (n - 20) + Math.max(types manquants, remplacer);
}
}
}
«» "

> ** Points clefs**
> * `len[0]`, `len[1]`, `len[2]` conserver combien de répétitions donnent un reste de 0, 1, 2 quand divisé par 3.
> * Supprimer un caractère d'une répétition de la longueur `k` réduit le nombre de remplacements requis par `=k/3=".
> * Supprimer sagement (d'abord ceux avec 0 restant, puis 1, puis 2) donne le plus de bang pour chaque suppression.

---

- Oui. 2. Mise en œuvre de Python

'`python
Solution de classe:
def strongMot de passeChecker(self, mot de passe: str) -> Int:
n = len(mot de passe)
has_lower = has_upper = has_digit = False

1. Vérifier les types manquants
pour ch dans le mot de passe:
si ch.islower(): has_lower = Vrai
elif ch.isupper(): has_upper = Vrai
elif ch.isdigit(): has_digit = Vrai

manquant = (non hash_lower) + (non hash_upper) + (non hash_numer)

2. Répétitions de balayage
remplacer = 0
mod_cnt = [0, 0, 0] # combien de répétitions donnent (en milliers de dollars)
i = 0
alors que i < n:
j = i
alors que j < n et mot de passe[j] == mot de passe[i]:
j += 1
l = j - i
si l >= 3 :
remplacer += l // 3
mod_cnt[l % 3] += 1
i = j

si n < 6:
retour max. 6 - n)

si n <= 20:
retour max(manquant, remplacer)

# n > 20
sur = n - 20
# Utilisez les suppressions sur les répétitions de manière optimale
pour k dans la plage(3):
utilisation = min(over, mod_cnt[k] * (k + 1))
remplacer -= utiliser // (k + 1)
sur -= utilisation

retour (n - 20) + max (manquement, remplacement)
«» "

> **Pourquoi la même logique? **
> La version Python reflète celle de Java : nous comptons les types manquants, nous scannons les répétitions, puis nous ajustons la longueur.
> La brièveté de Python fait les mêmes pas algorithmiques.

---

- Oui. 3. Mise en œuvre C++

'`cpp
solution de classe {
public:
Int forte PasswordChecker(chiffre de passe) {
int n = mot de passe.size();
bool hasLower = false, hasUpper = false, hasDigit = false;

// 1. Types de caractères manquants
pour (charc : mot de passe) {
si (inférieur(c)) aLower = vrai;
sinon si (isupper(c)) aUpper = true;
sinon si (isdigit(c)) hasDigit = true;
}
int manquant = (hasLower ? 0 : 1) + (hasUpper ? 0 : 1) + (hasDigit ? 0 : 1);

// 2. Répéte
remplacement int = 0;
int modCnt[3] = {0, 0, 0};
pour (int i = 0; i < n;) {
j = i;
pendant que (j < n && password[j] == password[i]) ++j;
int len = j - i;
si (lent >= 3) {
remplacer += len / 3;
modCnt[len % 3]++;
}
i = j;
}

si (n < 6) retour max (permis, 6 - n);
si (n <= 20) retour max(retirer, remplacer);

// n > 20
int sur = n - 20;
pour (int k = 0; k < 3; ++k) {
utilisation int = min(over, modCnt[k] * (k + 1));
remplacer -= utilisation / (k + 1);
-= utilisation excessive;
}
retour (n - 20) + max (manquement, remplacement);
}
};
«» "

---

- Oui. 4. Article du blog – Le bon, le mauvais, et le mauvais de Leetcode 420

> *Mots-clés*: Contrôleur de mot de passe fort, Leetcode 420, entretien de codage, force de mot de passe, entretien d'algorithme, entretien d'emploi

---

Introduction

Quand les intervieweurs demandent Combien d'étapes pour faire un mot de passe fort ?**, ils sont non seulement tester votre saisie de la manipulation de chaîne, mais aussi votre capacité à **optimiser** sous de multiples contraintes. Leetcode 420 est connu pour être *hard* mais *essentiel* pour de nombreux rôles d'ingénierie logicielle. Ci-dessous est une plongée profonde dans le problème, une solution O(n) robuste, et les pièges communs que vous devriez éviter.

---

C'est pas vrai. Le problème en coque

Précision
C'est pas vrai.
6 ≤ "len(mot de passe)" ≤ 20
Type de caractères au moins 1 minuscule, 1 majuscule, 1 chiffre
Répétition Aucun trois chars identiques dans une rangée

**Objectif:** Retourner le nombre minimum* de **insérer**, **supprimer** ou **remplacer** les opérations pour satisfaire les trois.

---

C'est vrai. Le point de vue de base – Trois pièces mobiles

Autres Partie Ce qu'il fait Comment il affecte la réponse
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Types manquants**
Chaque groupe de caractères identiques `k` a besoin de remplacements `'aaa''
L'insertion peut résoudre les types manquants et les répétitions; la suppression réduit les répétitions

L'équilibre de ces trois parties donne les étapes minimales totales.

---

C'est vrai. La solution Élégante O(n)

1. **Scan une fois**
- Tracer les types manquants.
- Détecter les exécutions de caractères répétés; enregistrer `len / 3` et `len % 3`.
2. **Case 1 – Court mot de passe (`len < 6`)* *
- L'insertion domine.
- "étapes = max(missing, 6 - len)".
3. **Cas 2 – Longueur acceptable («6 ≤ len ≤ 20»)* *
- Des remplacements.
- "étapes = max (défaut, total des remplacements)".
4. **Case 3 – Long mot de passe ('len > 20')**
- **Supprimer** d'abord pour réduire la longueur.
- Utiliser des suppressions sur les répétitions où elles réduisent le plus efficacement le nombre de remplacements nécessaires :
* Supprimer 1 char d'un groupe où "len % 3" 0` → réduire un remplacement.
* Supprimer 2 caractères d'un groupe où "len % 3" 1` → réduire un remplacement.
* Supprimer 3 caractères d'un groupe où "len % 3" 2` → réduire un remplacement.
- Après toutes les suppressions: `étapes = suppressions + max(manquement, remplacements restants)`.

La logique ci-dessus est **exactement** ce que l'implément Java/Python/C++ code snippets.

---

C'est pas vrai. Bon – ce qui rend cette solution excellente

Explication
C'est pas vrai.
**Temps linéaire**=On passe sur la chaîne → O(n) (n ≤ 50)=
**L'espace continu** Autres
**Déterministe**
** Logique claire ** Chaque cas gère un régime de longueur distinct, rendant l'algorithme facile à raisonner environ

---

C'est vrai. Mauvais – Erreurs communes à éviter

Erreur de correction
- Oui.
*Track "len % 3" groupes et ajuster "replace" après chaque suppression
*Maintenant les mots de passe courts en insérant seulement*. poignées à la fois
*Ignorer l'ordre des suppressions.*=Supprimer une répétition de longueur 5 avant une longueur 4 peut gâcher des opérations. 0 → 1 → 2)
*Utiliser la récursion ou la rétro-traque*

---

#### 6--Cas d'Edge qui emportent même les codes intelligents

Pourquoi c'est Tricky?
- C'est quoi ?
Autres **Toutes les répétitions et trop longues** (`"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa)``) Vous devez supprimer pour réduire la longueur *et* corriger les répétitions.
Autres **Type manquant mais pas de répétition** (`"aaaaaa"`)
**Longueur exactement 20 mais avec de nombreuses répétitions**
**Longueur exactement 6 mais toujours des types manquants**

---

Comment cela aide votre jeu d'entrevue

- **Shows pensée algorithmique**: Vous équilibrez trois contraintes simultanément.
- ** Démontre l'optimisation** : Les suppressions Greedy vs. remplacements montrent que vous pouvez réduire les opérations.
- **Mettre en évidence la prise de conscience des causes**: L'examen des cas de mauvais ou de mauvais traitements montre qu'ils sont approfondis.

> **Conseil pro**: Dans une entrevue, commencez par expliquer la stratégie de haut niveau avant de plonger dans le code. Cela indique la clarté de la pensée et maintient l'intervieweur engagé.

---

### # 8-

- **Titre**: *Chereur de mot de passe fort – Leetcode 420 expliqué (Java, Python, C++)*
- **Meta Description**: *Master Leetcode 420 avec des solutions étape par étape en Java, Python et C++. Apprenez l'algorithme O(n), les pièges communs et les conseils d'entrevue. *
- **Mots-clefs**: "Strong Password Checker", "Leetcode 420", "Java password strength checker", "Python password checker solution", "C++ Leetcode 420", "coding interview password", "job interview algorithme".

---

#### 9--

Leetcode 420 peut sembler intimidant, mais avec une stratégie avide claire, vous pouvez le résoudre efficacement et avec confiance. Rappelez-vous : **équilibrer les types manquants, les répétitions et la longueur**. Le code est simple – il suffit de traduire la logique dans votre langue de choix.

Si vous avez réussi ce problème, vous êtes prêt à ** apparaître dans n'importe quel entretien d'ingénierie logiciel** avec confiance. Bon codage – et bonne chance d'atterrir ce travail de rêve! C'est ce qu'il a dit.

---

* Se sentir libre de signet ce post, le partager sur votre Linked Dans le profil, et déposez un commentaire avec tout autre défi de Leetcode que vous aviez expliqué. *


---



Cela complète la réponse complète ****: code en trois langues et un article de blog complet.