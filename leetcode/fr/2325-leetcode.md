---
titre: LeetCode 2325. Décoder le message -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Solutions 3-Langue pour **Code de débit 2325 – Décoder le message**

Code de la langue
C'est quoi, ça ?
**Java** Cliquez pour agrandir</sommary>``java
Importation de java.util.*;

solution de classe publique {
chaîne publique décodeMessage(clé de chaîne, message de chaîne) {
// 1/ 1/ Rédiger le tableau de substitution – Chiffre de 26 lettres
Carte <caractère, caractère> chiffre = nouveau HashMap<>();
char nextPlain = 'a';

pour (char ch : key.toCharArray()) {
si (ch == ') continuer; // ignorer les espaces dans la clé
si (!cipher.contientKey(ch)) { // première apparition seulement
chiffre.put(ch, nextPlain++);
}
}

Décoder le message
StringBuilder décodé = nouveau StringBuilder();
pour (char ch : message.toCharArray()) {
i (ch] ') {
décodé.annexe(');
} autre {
décodé.append(cipher.get(ch));
}
}

retour décodé.àString();
}
}
```</details> Autres
**Python**= <details><sommaire>Cliquez pour agrandir</sommaire>``python
def decodeMessage(key: str, message: str) -> str:
# Construire la cartographie du chiffre
chiffre = {}
next_plain = ord('a')
pour ch en clé:
if ch == ': # sauter les espaces dans la clé
poursuivre
si ch n'est pas dans le chiffre: # première apparition seulement
chiffre[ch] = chr(prochain_plain)
next_plain += 1

# Décoder
retourner ''.join(' si ch == '' autre chiffre[ch] pour ch dans le message)
```</details> Autres
**C++** Cliquez pour agrandir</sommary>``cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
décoder la chaîneMessage(clé chaîne, message chaîne) {
Carte_non ordonnée<char,char> chiffre;
char next_plain = 'a';

// 1. Construire une table de chiffrement
pour (char ch : clé) {
if(ch == ') continuer; // ignorer les espaces
if(cipher.find(ch) == chiffre.end(){
chiffre[ch] = next_plain++;
}
}

// 2. Décoder
chaîne décodée;
décodé.reserve(message.size());
pour(char ch : message) {
if(ch == ') décodé.push_back(');
autrement décodé. push_back(cipher[ch]);
}
retour décodé;
}
};
```</details> Autres

> **Complexité temporelle**:
> `O(=key== +=message==)` – chaque chaîne est traversée une fois.
> **Complexité spatiale**:
> `O(1)` – la carte enregistre au plus 26 entrées, espace constant.

---

- Oui. 2. Article de blog – Décoder le message: le bon, le mauvais, le mauvais

> **Méta-titre:**
> Décoder le message – Java, Python, C++ Solutions & Conseils d'entrevue
> **Méta—Description:**
> Master LeetCode 2325 avec des solutions propres, prêtes à l'entretien en Java, Python et C++. Comprendre l'algorithme, les pièges et comment impressionner les recruteurs.
> **Mots clés:** décoder le message, leetcode 2325, hash map, chiffre de substitution, préparation d'entrevue, solution Java, solution Python, solution C++

---

2.1 Le problème en bref

> **Objectif:** Avec une chaîne *key* qui contient chaque lettre de l'alphabet au moins une fois, construisez une table de substitution en prenant l'occurrence **premier** de chaque lettre. Puis décodez une chaîne *message* en utilisant cette table (les espaces restent comme des espaces).

> **Pourquoi cela compte dans les entrevues :**
> * Affiche la familiarité avec les cartes / dictionnaires de hachage.
> * Teste la manipulation des caisses (espaces, lettres répétées).
> * donne un aperçu des compromis entre l'espace temporel et l'algorithme.

---

2.2 La bonne – Pourquoi l'approche fonctionne

Pourquoi c'est bon Détails
C'est pas vrai.
**La clé et le message sont traités en un seul balayage linéaire – optimal pour les contraintes données (`<= 2000` chars). Autres
**Constant— Carte de l'espace**. Seulement 26 entrées sont stockées quelle que soit la longueur de la clé – l'utilisation de la mémoire est négligeable. Autres
Autres **Simple Logic**=Construisez la cartographie *once* et réutilisez-la; pas besoin de structures de données complexes ou de tri. Autres
**Language-agnostic** ► Fonctionne de la même façon en Java, Python et C++ – idéal pour les intervieweurs en plusieurs langues. Autres
**Readability**= Séparation claire des étapes *building* et *decoding*, ce qui rend le code facile à raisonner. Autres

---

#### 2.3 Les mauvaises – Pièges communs et cas de bord

Pourquoi ça arrive ?
- Oui.
**Ignorer les espaces dans les clés**= Certaines solutions naïves traitent les espaces comme des clés valides. "Supprimez-les (si (ch) ") continue; "). Autres
**Réattribution de lettres dupliquées**=Une apparition ultérieure écrase la première cartographie. Vérifier si la clé existe déjà dans la carte avant d'insérer ('si (!cipher.contientKey(ch)'). Autres
Autres **Message Contient de l'char non macassé**= Si le message contient un caractère qui n'est pas dans la clé (probablement en raison de contraintes), il s'écrase. Ajouter un garde ou par défaut ('cipher.getOrDefault(ch,'?)'). Autres
Autres L'utilisation de `+=` dans une boucle peut mener à un temps quadratique. Construire une liste et `''.join()` à la fin. Autres
Autres **Grande plage alphabétique (extensions futures)**= Si l'alphabet a grandi, il pourrait être préférable de construire un tableau de taille fixe. Utiliser un tableau `char[26]` pour l'indexation O(1). Autres

---

2.4 L'horrible – Ce qui pourrait mal tourner

Réparer la situation
- Oui.
**Sur-ingénierie avec Trie ou Suffix Trees** Collez à une carte de hachage / dictionnaire. Autres
**Utilisation de la récursion sur un problème linéaire** Préférez les boucles itératives. Autres
**Codage dur de l'alphabet** Calculer dynamiquement `next_plain` en utilisant `ord('a')` / `'a' + i`.
**Éviter de tester les cas d'Edge**. Par exemple, une clé avec les 26 lettres répétées plusieurs fois. Écrire des tests unitaires pour les scénarios extrêmes. Autres

---

### 2.5 Liste de contrôle de l'entrevue-rédaction

1. ** Expliquer l'idée d'abord**
- Nous allons scanner la clé, mapper chaque nouvelle lettre à la lettre d'alphabet suivante, puis utiliser cette carte pour décoder le message. (en milliers de dollars)

2. **Discussion de la complexité**
- Temps "O(n)", espace "O(1)".

3. **Cas de bord à la main* *
- Afficher ce qui se passe si la clé a des espaces, des lettres répétées, ou si le message est vide.

4. **Parler des compromis* *
- Pourquoi une carte de hachage est plus simple qu'un tableau, mais un tableau peut être un peu plus rapide (temps constant sans hachage au-dessus).

5. **Afficher une mise en œuvre propre**
- Préférez les noms de variables claires (`cipher`, `nextPlain`).
- Éviter les branches "si" inutiles dans les boucles.

---

2.6 Essai d ' échantillon

Texte
Key : le renard brun rapide saute sur le chien paresseux
Message : vkbs bs t suepuv
Sortie : c'est un secret
«» "

La solution construit la cartographie:

«» "
V->t, k->h, b->i, s->s, ...
«» "

... et décode la phrase correctement.

---

2.7 A emporter

- **Soyez simple**: Un passe à construire, un passe à décoder.
- **Utilisez la bonne structure de données**: Une carte de hachage (ou tableau) donne une recherche O(1).
- **Cas de bord de test**: Espaces, duplicata, messages vides.
- **Exposer clairement**: Dans une interview, *comment * vous pensez est aussi important que *ce que * vous écrivez.

---

- Oui. 3. Clôture

Maîtrise Décodez le message non seulement vous donne une solide victoire LeetCode, mais démontre également votre capacité à:

- Traduire une exigence du monde réel en code propre.
- Choisir les structures de données appropriées.
- Optimisez le temps et l'espace.

Ce sont les compétences exactes que les recruteurs recherchent chez les ingénieurs logiciels. Bon codage – et bonne chance d'obtenir cette entrevue!