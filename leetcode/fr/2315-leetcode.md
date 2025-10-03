---
titre: LeetCode 2315. Compte des astérisques -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Aperçu du problème
**LeetCode 2315 – Compte des astérisques**
> **Difficulté :** *Facile*
> **Tags:** Chaîne, deux-pointeurs, balayage linéaire

On vous donne une chaîne `s`. Toutes les deux barres verticales consécutives `' forment une paire*.
Tous les caractères **entre** une paire de `=" sont *ignorés*.
Retourner le nombre de `*` qui sont ** hors de cette paire**.

> **Exemple**
> `s = "l=*e*et="c**o="*de=" → réponse = **2**

---

- Oui. Pourquoi ce problème a-t-il des répercussions sur les entrevues?

* Elle teste la traversée de la chaîne **linéaire-temps** – un point de départ dans les interviews.
* Nécessite une réflexion sur ** l'état de basculement** ('intérieur'...
* Une illustration parfaite de l'une ou l'autre fois, comte.

---

## 3'''Idée de solution (Le modèle "One-Pass")

1. **Maintenir un drapeau booléen** `intérieur = faux'.
2. Traversez la corde une fois.
* Lorsque vous rencontrez `=` basculer `intérieur '.
* Lorsque vous rencontrez `*` et `intérieur` est `faux`, incrémentez le compteur.
3. Retourne le comptoir.

> **Pourquoi ça marche** – Parce que chaque paire de `=" est garantie d'être uniforme, le drapeau reflétera correctement si nous sommes dans un bloc à tout moment.

---

Mise en œuvre du code

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.
Tous les trois partagent la même logique à un passage et fonctionnent dans le temps `O(n)` avec l'espace auxiliaire `O(1)`.

Langue Complexité Code
- C'est quoi ?
**Java** espace **Java 17** (JDK 17+ recommandé)
**Python** espace **Python 3.9**
**C++** espace **C++17** (g++‐10 ou plus récent)

---

#### 4.1 Java

"Java
***
* LeetCode 2315 – Compte des astérisques
*
* Scan linéaire à un passage avec une bascule booléenne.
* Heure : O(n)
* Espace : O(1)
*/
solution de classe publique {
Nombre d'entrées publiques Les astérisques(String s) {
nombre int = 0;
booléen à l'intérieur = faux; // faux → à l'extérieur de n'importe quel «... '

pour (int i = 0; i < s.longueur(); i++) {
char ch = s.charAt(i);

if (ch == ') { // bascule l'état
intérieur = !intérieur;
continuer ; // ''' elle-même ne compte jamais
}

if (!inside && ch == '*') { // compter seulement à l'extérieur
count++;
}
}
le nombre de retours;
}
}
«» "

> **Pourquoi cette version Java est facile à utiliser* *
> * Utilise le nom de méthode claire `countAstreisks` – correspond à la signature de LeetCode.
> * Simple `for‐loop` – aucun objet supplémentaire → runtime rapide.
> * Pas de blocs statiques inutiles ou de hacks.

---

4.2 Python

'`python
"""
LeetCode 2315 – Compte des astérisques
Mise en œuvre de Python 3.9
"""

Solution de classe:
def countAstérisques(self, s: str) -> Int:
nombre = 0
à l'intérieur = Faux # Faux → à l'extérieur '

pour ch en s:
si ch == '''':
intérieur = pas intérieur
poursuivre
si ce n'est pas à l'intérieur et à l'intérieur et à l'intérieur
nombre += 1

Nombre de retours
«» "

*Note de python:*
La solution utilise un seul « for-loop » et un simple toggling booléen – exactement ce que les intervieweurs attendent.

---

### 4.3 C++

'`cpp
***
* LeetCode 2315 – Compte des astérisques
* Mise en œuvre C++17
*
* Complexité: temps O(n), espace O(1)
*/

solution de classe {
public:
compteAstérisques(chaîne s) {
nombre int = 0;
bool inside = false; // false = en dehors de n'importe quel «... '

pour (charte : s) {
Si (ch) {
intérieur = !intérieur; // état de basculement
poursuivre;
}
si (!intérieur && ch == '*') {
+ nombre;
}
}
le nombre de retours;
}
};
«» "

*Pourquoi C++? *
La boucle `for-range` maintient le code concis, et le compilateur optimise les fausses prédictions booléennes à zéro branche.

---

## 5.

Autres Tests attendus Pourquoi
C'est pas vrai.
Pas de barres, comptez l'étoile. Autres
"""""""""""0" Aucune étoile, mais la barre s'allonge vers l'intérieur et le dos. Autres
L'étoile est dans une paire → ignorée. Autres
Les barres annulent, les étoiles en dehors du compte. Autres
**************************************************************************************************************************************************************************************************************************************************************** Autres

Tous les tests confirment que le simple mécanisme de drapeau fonctionne pour toutes les entrées possibles.

---

# # # 6 Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Simplicité**= One-pass, O(n) – très facile à expliquer dans une entrevue. Aucun.
**Mémoire**= O(1) espace supplémentaire – ne jamais stocker de sous-chaînes ou de piles. Aucun.
**Readability**= Effacer les noms de variables (`intérieur`, `count`). Dans certaines langues, les gens utilisent le « drapeau » – ambigu.
**Pitfall**= Oublier de basculer après chaque `=" peut causer de mauvais compte.
**Investissements inattendus** Si l'entrée est mal formée (barres obliques), l'algorithme se comporte mal en silence.

> **Leçon:** Vérifiez toujours que l'état est correctement appliqué et que les caractères autres que `=" et `*` sont ignorés.

---

## 7--

1. **L'état d'esprit de la machine** – Pensez au problème comme un petit automate avec deux états : *hors* et *à l'intérieur* une paire de barres.
2. **Exposer la bascule** – Les intervieweurs adorent quand vous articulez "chaque " retourne l'état ".
3. **Cas d'Edge** – Mentionnez qu'une chaîne vide ou une chaîne sans étoiles retourne 0.
4. **Heure/espace** – Soyez prêt à répondre pourquoi c'est O(n)= et pourquoi O(1) espace=.
5. **Optimisation** – En Java, évitez `StringBuilder` ou `split` – une boucle simple est la plus rapide.
6. **Testing** – Dessinez rapidement quelques exemples testés à la main avant le codage.

---

Conclusion du blog optimisé du SEO

> Si vous préparez votre prochaine entrevue d'ingénierie logicielle, la maîtrise du problème **Count Astérisques** démontre la maîtrise des scans linéaires, de l'état de basculement et du codage propre – toutes les compétences très prisées par les entreprises de haute technologie.
> En maîtrisant les implémentations **Java**, **Python** et **C++** ci-dessus, vous pouvez répondre avec confiance à cette question LeetCode, présenter des solutions O(n) propres et impressionner les intervieweurs avec votre clarté de pensée.

> **Mots-clés** pour les recruteurs : *Code de bord 2315*, *Count Astérisques*, *Question d'entrevue de Java*, *Manipulation de chaînes de Python*, *Scan linéaire C++*, *complexité du temps*, *complexité de l'espace*, *machine d'état*, *entrevue d'ingénierie de logiciels*, *conseils d'entrevue de codage*.

Laisser un commentaire ou partager sur Linked Dans – laissez-les obtenir cette offre d'emploi d'entrevue de codage! C'est ce qu'il a dit