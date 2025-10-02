---
Titre: LeetCode 3662. Filtre de caractères par fréquence -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3662 – **Caractéristiques d'entretien par fréquence**
*(Facile – 1 ≤ longueur ≤ 100)*

Langue Heure Espace
- C'est quoi ?
*Java * O(n)
*Python * O(n)
*C++ * O(n)

> **Pourquoi ce problème se pose pour un entretien d'embauche* *
> Il teste la manipulation des chaînes de base + le comptage des fréquences.
> Vous pouvez discuter des solutions *deux-pass* vs *un-pass* et des compromis.
> Elle ouvre des portes pour parler de *complexité du temps/de l'espace*, *cas de corner*, *test* et *littérabilité du code*—tous les sujets d'entrevue doivent savoir.

---

Réévaluation des problèmes

Étant donné une chaîne `s` de lettres anglaises minuscules et un entier `k`, construisez une nouvelle chaîne qui contient **chaque caractère** de `s` dont la fréquence totale dans `s` est ** strictement inférieure** à `k`.
Les caractères du résultat doivent conserver leur ordre original.
Si aucun caractère n'est admissible, retourner une chaîne vide.

> **Exemple**
> `s = "aadbbcccca", k = 3`
> Fréquences → a:3, d:1, b:2, c:4 → seulement `d` et `b` sont < 3
> Résultat → `"dbb"`

---

Idée de base – Compte de la fréquence de deux passes

1. ** Première passe** – Comptez chaque lettre de fréquence (pour mémoire de taille 26).
2. **Deuxième passe** – itérer à nouveau la chaîne originale et ajouter seulement ceux
les lettres dont la fréquence `< k`.

Parce que l'alphabet est fixe et petit, le tableau de fréquence est *O(1)* espace, tandis que
la chaîne elle-même est `O(n)`.

---

Solutions de code

Java (O(n) Temps, O(1) Espace supplémentaire)

"Java
Importation de java.util.*;

solution de classe publique {
public Filtre à cordes Caractères(String s, int k) {
// Tableau de fréquence pour 26 lettres minuscules
int[] freq = nouveau int[26];
pour [charc : s.toCharArray()) {
freq[c - 'a']++;
}

StringBuilder sb = nouveau StringBuilder();
pour [charc : s.toCharArray()) {
si (freq[c - 'a'] < k) {
sb.annexe c);
}
}
retour sb.toString();
}
}
«» "

Python (Comptoir Pythonique + Compréhension de la Liste)

'`python
Importations provenant des collections Compteur
de taper l'importation *

Solution de classe:
def filtre Caractères(self, s: str, k: int) -> str:
freq = Compteurs # O(n)
retour ''.join(c pour c dans s si freq[c] < k) # O(n) bâtiment
«» "

> **Note:** Utiliser `Counter` maintient le code concis et exprime clairement l'intention.

C++ (Fast & Explicit)

'`cpp
#incluez <string>
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
filtre à cordes Caractères(chaîne s, int k) {
vecteur <int> freq(26, 0);
pour (char c : s) freq[c - 'a']++; // premier passage

la chaîne rés;
pour (charc : s) // deuxième passage
si (freq[c - 'a'] < k) res += c;

retour rés;
}
};
«» "

---

Cas de bord et pièges communs

Qu'est-ce que regarder ?
- C'est quoi ?
Chaque caractère qualifie → retourner `s` inchangé. La vérification `< k` gère naturellement cela. Autres
Autres Tous les caractères apparaissent `>= k` times. Retour `""` après la boucle. Autres
Empty string (longueur) == Les contraintes de problème interdisent, mais le code défensif renvoie """. Autres
Autres Lettres majuscules Le problème dit minuscules seulement; autrement, ajuster la taille du tableau. Soit valider soit convertir en minuscule. Autres

---

C'est un problème.

Aspect du bien
- C'est quoi ?
Description et contraintes très claires. Aucun.
**Difficulté**= Facile – bon pour la première ronde de projection. Aucun.
Autres **Complexité du temps**= O(n) – optimum.
Autres **Complexité de l'espace**= O(1) (tableau fixe 26-int). L'utilisation de la carte de hachage augmenterait l'espace. La suringénierie avec le régex ou les bibliothèques lourdes est une surcompétence. Autres
**Questions d'entrevue potentielles**= Pourrions-nous le faire en un seul passage? <br>• Et si l'alphabet est plus grand ? • Demandez au sujet de la gestion de cas de bord. • Demandez d'expliquer l'empreinte mémoire si `s` étaient énormes et `k` dynamique. Autres

---

Comment parler Dans une interview

1. ** Expliquez l'approche à deux passages** – montrez que vous comprenez pourquoi nous avons besoin de la fréquence en premier.
2. **Mention O(1) espace** – mettre en évidence l'avantage du tableau 26-int.
3. **Cas de bord de discussion** – donner au moins deux exemples (par exemple, tous les caractères >= k, k=1).
4. **Afficher des solutions alternatives** – p.ex. un seul passage avec `HashMap` + file d'attente, ou en utilisant `Counter` dans Python.
5. **Parlez des cas d'essai** – écrivez quelques-uns pour démontrer votre compréhension.
6. ** Expliquez pourquoi nous conservons l'ordre** – soulignez que nous itérerons à nouveau la chaîne originale.

---

Suite d'essai d'échantillons

Autres Test d'entrée Résultats attendus
- C'est quoi ?
"Aadbbcccca", 3 ""Dbb"
"xyz", "xyz"
"Aaaa", 5 """""""
""Bacadae", 2 ""Bde"
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

---

Clôture du blog optimisé du SEO

Si vous vous préparez à des entrevues techniques, **Filter Caracters by Frequency** est un problème incontournable de LeetCode.
- Les solutions **Java** et **C++** sont ultra-rapides, tandis que **Python** le garde rangé avec des "collections". Compteur.
- Comprendre l'astuce **de deux passages** démontre une pensée algorithmique solide.
- Oui. Vous pouvez discuter en toute confiance ** des compromis entre le temps et l'espace**, ** du traitement des cas** et ** des approches alternatives** – exactement ce que les intervieweurs recherchent.

Déposez le code ci-dessus dans votre IDE préféré, exécutez les cas de test, et vous serez prêt à aser ce problème.

** Bonne chance, et codage heureux!**

---

**Mots-clés:** LeetCode 3662, Filter Characters by Frequency, Java solution, Python solution, C++ solution, problème de codage d'entrevue, manipulation de chaîne, comptage de fréquence, entretien d'emploi, pensée algorithmique.