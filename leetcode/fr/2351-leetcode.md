---
titre: LeetCode 2351. Première lettre pour apparaître deux fois -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2351 – Première lettre pour apparaître deux fois
**Java, Python & C++ Solutions + SEO-Optimized Blog Post**

> **Problème de code 2351** – Première lettre pour apparaître deux fois
> Difficulté : *Facile*
> Mots clés: *String, Hash Table, Deux Pointeurs*

---

## 1-

On vous donne une chaîne de lettres anglaises minuscules.
Retourne le caractère *premier* qui apparaît **deux fois** dans la chaîne.

> **Note**
> Un caractère `a` apparaît deux fois *avant* un autre caractère `b` si le deuxième
> la présence de `a` se produit à un indice inférieur à la seconde présence de `b`.
> `s` contient toujours au moins une lettre répétée.

**Exemples**

Entrée Sortie Raisonnement
C'est quoi ?
""abccbaacz""""" `'c'""" "c'"" La deuxième occurrence (index 3) est avant toute autre occurrence de seconde lettre. Autres
""abcdd" """ `"d'""" Seulement `d` répète, c'est donc la réponse. Autres

**Contrôles* *

- "2 ≤ s. longueur ≤ 100"
- " s " ne contient que des lettres anglaises minuscules.
- Oui. Il y a au moins une lettre répétée.

---

Aperçu de l'approche

La solution la plus simple et la plus simple est de savoir si nous avons déjà vu chaque lettre.
Comme il n'y a que 26 lettres minuscules, nous pouvons utiliser :

1. ** tableau booléen** (taille 26) – espace constant.
2. **HashSet** – fonctionne également mais les frais généraux inutiles.

Nous itérer sur la corde une fois, marquer chaque lettre comme vu la première fois que nous la rencontrons, et le retourner immédiatement quand nous le voyons une deuxième fois.

- Oui. Pourquoi est-ce la solution *bonne*?

Critère Pourquoi il est bon
C'est quoi ?
**Complexité du temps**= `O(n)` – passe sur la chaîne. Autres
**Complexité spatiale**"O(1)" – tableau de taille fixe de 26 booléens. Autres
**Simplicité** Autres
**Pas de collisions de hachage, pas de randomisation. Autres

- Oui. Le mauvais côté

- Oui. Si vous avez utilisé un `HashSet`, vous encourriez des collisions aériennes et des risques supplémentaires dans de très grandes entrées (mais pas ici).
- Le code d'écriture qui renvoie `'\0'` ou `0` comme un retour pourrait confondre les futurs responsables – mais le problème garantit un duplicata, donc il est correct.

- Oui. Les cas du coin

- Chaîne vide (non autorisée par les contraintes).
- Tous les caractères uniques – également interdits.
- Entrée non-ASCII – encore une fois, hors de la portée du problème.

---

# # # # # # Code Snippets

On trouvera ci-dessous des solutions concises prêtes à être copiées dans **Java, Python et C++**.

---

#### 3.1 Java

"Java
// 2351. Première lettre pour apparaître deux fois
solution de classe publique {
publique répétée Caractère(String s) {
// Tableau booléen pour 26 lettres minuscules
booléen[] vu = nouveau booléen[26];

pour [charc : s.toCharArray()) {
si (voir [c - 'a']) {
// Premier personnage qui a été vu deux fois
retour c;
}
vu[c - 'a'] = vrai;
}
// Problème garantit un duplicata, donc cette ligne est inaccessible.
retourner «\0»;
}
}
«» "

---

3.2 Python

'`python
# 2351. Première lettre pour apparaître deux fois
Solution de classe:
def répété Caractère(s: str) -> str:
vu = [Faux] * 26 # 26 lettres minuscules
pour ch en s:
idx = ord(ch) - ord('a')
si vu[idx]:
retour ch # premier caractère répété
vu[idx] = Vrai
# Inatteignable en raison de la garantie de problème
retour '
«» "

---

### 3.3 C++

'`cpp
// 2351. Première lettre pour apparaître deux fois
solution de classe {
public:
char répété Caractère(chaîne s) {
vecteur <bool> vu(26, faux);
pour (charc : s) {
int idx = c - 'a';
si (voir[idx]) retour c;
vu[idx] = vrai;
}
// Inatteignable
retourner «\0»;
}
};
«» "

---

- Oui. Article de blog: *Le Bon, le Mauvais, et le Ugly de LeetCode 2351*

> **Titre**: *Mastering LeetCode 2351 – Première lettre à paraître deux fois : un Java/Python/C++ propre et efficace Guide*
> **Meta Description**: Résolvez le LeetCode 2351 avec une solution en 3 langues. Apprenez la stratégie O(n) optimale, les pièges et les explications prêtes à l'entrevue.

#### 4.1 Pourquoi ce problème se pose pour les entrevues

- **Simplicité**: Il teste la manipulation de base des chaînes et le comptage des fréquences.
- **Découpage temps/espace**: Vous force à choisir entre un espace constant et des structures dynamiques.
- **Analogie du monde réel**: détection des duplicatas dans les fichiers journaux, le traitement de flux ou la validation de l'entrée de l'utilisateur.

### 4.2 Le *Bonne* – Votre solution optimisée

1. **O(n) Temps** – Un scan.
2. **O(1) Espace** – tableau booléen de 26 dimensions.
3. **Zero Hashing** – Évite les collisions et assure le déterminisme.
4. **Code lisible** – Effacer les noms de variables, les boucles courtes.

### 4.3 La mauvaise * – Pièges communs

Pourquoi ça va mal
C'est quoi ?
En utilisant un `HashSet`. Autres
Autres Retour d'une valeur magique (`0`/`\0'`) sans commentaire Les futurs lecteurs pourraient se demander pourquoi cette valeur est retournée. Autres
Autres Ignorer la garantie d'un duplicata rend le code moins robuste dans les cas de bord. Autres

4.4 Les cas de bords rares

- **Unicode ou majuscule**: L'algorithme ne fonctionne que pour les minuscules ASCII.
- **Très grande entrée**: Sans objet parce que « longueur ≤ 100 ».
- **Doublons multiples au même index**: Impossible en raison de la nature des cordes.

4.5 Entretien Points de discussion prêts

- **Expliquer l'indexation du tableau** ('c - 'a').
- **Pourquoi nous revenons immédiatement** sur la deuxième rencontre.
- **Pourquoi la solution est déterministe** – pas de collisions de hachage, pas de hasard.
- **Mention temps / espace échange** et pourquoi l'espace constant est possible.

#### 4.6 SEO & Job‐Hunting Conseils

- **Mots-clés**: LeetCode 2351, La première lettre à apparaître Twice, La chaîne de Java duplicata, Questions d'entrevue de Python, Défi de codage de C++, Conseils d'entrevue d'algorithme, Codage d'entrevue d'emploi.
- **Structure**: Utiliser des rubriques (`h1`, `h2`, `h3`) et des listes de puces pour la lisibilité.
- **Ajouter des blocs de code**: Markdown des blocs de code clôturés avec des spécifiants de langage pour la mise en évidence syntaxique.
- **Show Complexity**: Inclure une section --Time & Space Complexity pour impressionner les recruteurs.

---

C'est pas vrai. Réflexions finales

LeetCode 2351 est un micro-challenge qui regroupe les éléments essentiels de la manipulation des chaînes, du comptage des fréquences et de la conception d'algorithmes efficaces.
La solution optimale utilise un tableau booléen de taille fixe, réalisant un temps linéaire et un espace constant – un modèle que vous verrez dans de nombreuses questions d'entrevue.

Avec les implémentations Java, Python et C++ ci-dessus, vous êtes prêt à soumettre, partager et discuter ce problème avec confiance. Bon codage – et bonne chance pour ce travail!