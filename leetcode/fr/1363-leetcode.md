---
titre: LeetCode 1363. Le plus grand multiple de trois -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le plus grand multiple de trois – LeetCode 1363
**Java-Ready Coding**

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Observations clés] (#observations clés)
3. [Comptabilité de la graisse + Modulo‐3](#Comptabilité de la graisse-modulo-3)
4. [Détails de mise en œuvre] (#détails de mise en œuvre)
* 4.1 Java
4.2 Python
* 4.3 C++
5. [Complexité temps-espace] (#complexité temps-espace)
6. [Pièges communs et cas de bord] (#pièges)
7. Bonne, mauvaise, mauvaise de la solution.
8. [Pourquoi cela compte pour votre prochaine entrevue de travail](#pourquoi-matières)
9. [Conclusion et lecture supplémentaire](#conclusion)

---

## Aperçu du problème <a name="problem-overview"></a>
> **LeetCode 1363 – Le plus grand multiple de trois* *
> Compte tenu d'un tableau de chiffres (`0‐9`), construire le nombre **le plus grand possible** qui est un multiple de `3` en concatérant tout sous-ensemble de chiffres dans n'importe quel ordre.
> Retourner le résultat comme une chaîne (pas de zéros de tête inutiles). Retourner `""` s'il n'existe pas de tel numéro.

Exemples
Entrée Sortie Explication
C'est pas vrai.
`[8,1,9]`" `"981"`" `981` est divisible par `3` et est le plus grand arrangement. Autres
La suppression du `1` donne une somme divisible par `3`. Autres
Aucun multiple de `3` ne peut être formé. Autres

---

- Oui. Observations clés <un nom="observations clés"></a>
1. **Divisibilité par 3**
Un nombre est divisible par 3 iff la somme de ses chiffres est divisible par 3.
→ Nous avons seulement besoin de la somme totale **** mod `3`.

2. **Uniquement 10 chiffres distincts**
Nous pouvons stocker combien de fois chaque chiffre apparaît dans un tableau de taille 10.
→ Mémoire O(1), aucun tri requis.

3. **Enlèvement de la graisse**
Si la somme 1 (mod. 3):
* Supprimer **un** plus petit chiffre 1 (mod 3) **ou**
* Enlever **deux** plus petits chiffres 2 (mod. 3).

Si la somme 2 (mod. 3):
* Supprimer **un** chiffre le plus petit 2 (mod 3) **ou**
* Supprimer **deux** plus petits chiffres 1 (mod. 3).

Enlevant les *les plus petits* chiffres possibles, le nombre obtenu est le plus grand possible.

4. **Laisser des zéros**
Après suppression, la chaîne peut commencer par `0`.
* Si tous les autres chiffres sont `0`, retourner `"0"`.
* Si aucun chiffre ne reste, retourner `""`.

---

## Greedy + Modulo‐3 Comptage <un nom="greedy-modulo-3-counting"></a>
1. Compter chaque chiffre (`0`‐`9`).
2. Calculer le total Somme % 3 %.
3. Déterminer le nombre de chiffres de chaque classe restante (`%3 == 1` ou `2`) à supprimer.
4. Construisez la réponse en itérant **de 9 vers le bas à 0** et en ajoutant les chiffres restants.
5. Boîtes de bord de poignée (chaîne vide / seulement zéros).

Cette approche fonctionne en **O(n)** temps (un passe pour compter, nettoyage à temps constant) et utilise **O(1)** espace supplémentaire.

---

## Détails de la mise en oeuvre <un nom</a>
Voici des implémentations claires et bien commentées dans **Java, Python et C++**.
Tous les trois partagent le même flux logique, mais sont idiomatiques pour chaque langue.

### 4.1 Java <a name="java"></a>
"Java
Importation de java.util.*;

solution de classe publique {
public Chaîne la plus grande MultipleOfThree(int[] chiffres) {
// Compter les occurrences de chaque chiffre.
int[] cnt = nouvelle int[10];
= 0;
pour (int d : chiffres) {
cnt[d]++;
somme += d;
}

// Déterminer le nombre de chiffres à supprimer.
int r1 = cnt[1] + cnt[4] + cnt[7]; // chiffres avec le reste 1
int r2 = cnt[2] + cnt[5] + cnt[8]; // chiffres avec le reste 2
int supprimer1 = 0, supprimer2 = 0; // suppressions de 1 / 2 chiffres restants

int rem = somme % 3;
Si (rem) 1) {
si (r1 >= 1) { supprimer1 = 1; }
sinon si (r2 >= 2) { supprimer2 = 2; }
sinon retourner "; // impossible
} sinon si (rem) 2) {
si (r2 >= 1) { supprimer2 = 1; }
sinon si (r1 >= 2) { supprimer1 = 2; }
Sinon retourner ";
}

// Supprimer les plus petits chiffres nécessaires.
pour (int d = 1; d <= 9 && delete1 > 0; d += 3) { // 1,4,7
Int take = Math.min(cnt[d], supprimer1);
cnt[d] -= prise;
supprimer1 -= prendre;
}
pour (int d = 2; d <= 9 && delete2 > 0; d += 3) { // 2,5,8
int take = Math.min(cnt[d], supprimer2);
cnt[d] -= prise;
supprimer2 -= prendre;
}

// Construisez le nombre du plus grand au plus petit chiffre.
StringBuilder sb = nouveau StringBuilder();
pour (int d = 9; d >= 0; d--) {
pour (int i = 0; i < cnt[d]; i++) sb.append(d);
}

si (longueur de sb) == 0) retourner ";
si (sb.charAt(0) == '0') retourner "0";
retour sb.toString();
}

// harnais d'essai simple
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.plus grandMultipleOfTrois(nouvelle int[]{8,1,9}); // 981
Système.out.println(s.plus grandMultipleOfTrois(nouvelle int[]{8,6,7,1,0}); // 8760
System.out.println(s.plus grandMultipleOfThree(new int[]{1})); // "
}
}
«» "

> **Pourquoi cette version Java est-elle efficace? * *
> • Pas de tri → `O(n)` temps.
> • Utilise des tableaux de taille constante → frais généraux minimes.
> • Logique directe avec des commentaires clairs – idéal pour l'interview tableau blanc.

---

#### 4.2 Python <a name="python"></a>
'`python
de taper l'importation Liste
Importations provenant des collections Compteur

Solution de classe:
def le plus grandMultipleOfThree(self, chiffres: List[int]) -> str:
cnt = [0] * 10
Total = 0
pour d en chiffres:
cnt[d] += 1
Total += d

r1 = cnt[1] + cnt[4] + cnt[7]
r2 = cnt[2] + cnt[5] + cnt[8]
supprimer1 = supprimer2 = 0
m = total % 3

si rem == 1 :
si r1 >= 1: supprimer1 = 1
elif r2 >= 2: supprimer2 = 2
sinon: retourner ""
* 2 :
si r2 >= 1: supprimer2 = 1
elif r1 >= 2: supprimer1 = 2
sinon: retourner ""

# Enlever les plus petits chiffres de chaque reste
pour d in (1, 4, 7):
tout en supprimant1 et cnt[d]:
cnt[d] -= 1
supprimer1 -= 1

pour d in (2, 5, 8):
tout en supprimant2 et cnt[d]:
cnt[d] -= 1
supprimer2 -= 1

# Résultats de construction de 9 à 0
res = []
pour d dans la plage (9, -1, -1):
res.extend([str(d)] * cnt[d])

si non rés: # il ne reste plus rien
retour ""
si res[0] == '0': # tous les zéros
retourner "0"
retourner "".join(res)

# ---- Exemple d'utilisation ----
si __nom__ == "__main__" :
s = Solution()
imprimer(s.plus grandMultipleOfTrois([8, 1, 9])) # 981
imprimer(s.plus grandMultipleOfTrois([8, 6, 7, 1, 0])) # 8760
imprimer(s.plus grandMultipleOfTrois([1]) # "
«» "

> **Les beautés du python**
> • `cnt` est une liste de taille fixe → mémoire O(1).
> • `Counter` est surkill; une liste maintient l'algorithme serré.
> • Les boucles `When` rendent l'étape de suppression explicite et facile à lire sur un tableau blanc.

---

### 4.3 C++ <a name="cpp"></a>
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne la plus grande MultipleOfTrois(vecteur<int>& chiffres) {
nombre de chiffres
somme longue = 0;
pour (int d : chiffres) {
++cnt[d];
somme += d;
}

int r1 = cnt[1] + cnt[4] + cnt[7];
int r2 = cnt[2] + cnt[5] + cnt[8];
Int del1 = 0, del2 = 0;
int rem = somme % 3;

Si (rem) 1) {
si (r1 >= 1) del1 = 1;
sinon si (r2 >= 2) del2 = 2;
Sinon retourner ";
} sinon si (rem) 2) {
si (r2 >= 1) del2 = 1;
sinon si (r1 >= 2) del1 = 2;
Sinon retourner ";
}

// supprimer les chiffres restants les plus petits (1,4,7)
pour (int d = 1; d <= 9 && del1 > 0; d += 3) {
prise = min(cnt[d], del1);
cnt[d] -= prise;
del1 -= prise;
}
// supprimer les chiffres restants les plus petits (2,5,8)
pour (int d = 2; d <= 9 && del2 > 0; d += 3) {
prise = min(cnt[d], del2);
cnt[d] -= prise;
del2 -= prise;
}

la chaîne rés;
pour (int d = 9; d >= 0; --d) {
l'annexe(cnt[d], char('0' + d));
}

si (res.vide()) retourne ";
si (res[0]] '0') retourner "0";
retour rés;
}
};

// Essai rapide
Int main() {
Solution s;
Cout << s.plus grandMultipleOfTrois({8,1,9}) << endl; // 981
cout << s.plus grandMultipleOfTrois({8,6,7,1,0}) << endl; // 8760
Cout << s.plus grandMultipleOfTrois({1}) << enl; // "
}
«» "

> **Perques C++**
> • Utilise `array<int,10>` pour la mémoire O(1).
> • `string::append(count, char)` est un moyen rapide de construire le résultat.
> • Compact mais entièrement dactylographié – idéal pour une entrevue de codage.

---

## Complexité temporelle et spatiale <un nom="complexité temporelle-espace"></a>
Langue
- C'est quoi ?
Java **O(n)****O(1)** (10-size array)
Python **O(n)**
* * * * * * * * *

L'algorithme est linéaire dans la longueur d'entrée et n'utilise que quelques dizaines d'octets de mémoire.

---

## Pièges communs et cas de bord <un nom="pièges"></a>
Que se passe-t-il ?
C'est pas vrai.
Autres **Supprimer trop de chiffres** – par exemple, supprimer tous les chiffres `%1` quand un seul existait. Autres
**Ne laisser que des zéros** – par exemple, entrée `[0,00]` Après avoir construit la chaîne, si `sb[0] == '0'` retourner `"0'`. Autres
**Empty output** – après suppressions aucun chiffre gauche.
**Traitement** – l'utilisation de `sort()` sera `O(n log n)`=" Plus lentement, pas requis=" Compter les chiffres au lieu de trier. Autres
**Off‐by‐one dans les boucles** – mal gérer les classes restantes. Autres

---

- Oui. "Bien, mal, mal" de la solution <un nom "bon, mauvais"></a>

Aspect du bien
- C'est quoi ?
**Concept**=Utilisez une propriété mathématique (somme % 3) qui transforme le problème en question *retirement*. La formulation du problème pourrait vous induire en erreur en pensant que vous devez trier ou générer des permutations. Aucun – la solution est propre ; la partie ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ Autres
**Lisibilité du code**= Les commentaires expliquent *pourquoi* nous supprimons des chiffres particuliers. De très longues boucles pourraient obscurcir l'intention si vous enfiliez tout en une seule ligne. La sur-ingénierie (p. ex. en utilisant des tas ou des récursions) est inutile et rendra votre code maladroit. Autres
**Le style de l'interview**=Ouvre sur un tableau blanc – juste un tableau de 10 compteurs, quelques calculs entiers, et une boucle de 9→0.=En Python ou JavaScript vous pourriez être tenté d'utiliser `sort()` pour la simplicité; ce serait un drapeau rouge pour les intervieweurs qui attendent O(n). En n'utilisant pas la propriété modulo‐3 et en essayant de forcer tous les sous-ensembles, vous perdrez votre solution à un temps exponentiel. Autres

---

## Pourquoi cela compte pour votre prochaine entrevue d'emploi <un nom="pourquoi-matières"></a>
* ** Pensée algorithmique** – Démontre que vous pouvez dériver un *invariant mathématique* (somme des chiffres) et le transformer en algorithme gourmand.
* ** compromis spatiaux** – Montre que vous savez quand le tri est gaspillé et vous pouvez le remplacer par le comptage.
* **Couverture du cas d'urgence** – Les intervieweurs aiment les candidats qui pensent à la réponse vide et aux scénarios zéros.
* **Code propre** – Des solutions linguistiques idiomatiques bien commentées indiquent le professionnalisme et les compétences en communication.
* ** Versatility** – Être capable de mettre en œuvre la même logique en Java, Python ou C++ prouve que vous pouvez vous adapter rapidement aux piles technologiques.

> **Conseil pro**: Lorsque vous marchez à travers ce problème sur un tableau blanc, commencez par un croquis rapide de 3:00 sum % → 2:00 delete un ou deux chiffres. Mettre en évidence le tableau de 10 tailles. L'intervieweur vous verra immédiatement sur la bonne voie.

---

## Conclusion et lecture supplémentaire <a name="conclusion"></a>
Le problème **Le plus grand multiple de trois** est un exemple classique de la façon dont une question apparemment combinatoire s'effondre dans un simple problème modulo arithmétique. En tirant parti du fait qu'il n'existe que dix chiffres distincts, nous pouvons construire un algorithme cupide linéaire à temps constant qui est à la fois **efficace** et **facile à comprendre**.

Si vous vous préparez à codifier des entrevues, ce problème doit être résolu car il teste :
1. Connaissance de la théorie du nombre (divisibilité par 3).
2. Capacité à concevoir des stratégies gourmandes.
3. Compétence dans la manipulation des cas de bord (leading zéros, suppressions impossibles).
4. Nettoyer la mise en œuvre en plusieurs langues.

---

Prêt à monter ?
Essayez de résoudre le problème sur LeetCode vous-même (lien ci-dessous) et ensuite comparez vos solutions aux trois implémentations ci-dessus.
Les **LeetCode 1363 – Plus grand multiple de trois**: <https://leetcode.com/problèmes/plus grand multiple de trois/>

Bonne chance, et que votre prochaine interview soit un parfait multiple de trois!