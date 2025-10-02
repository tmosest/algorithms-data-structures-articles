---
titre: LeetCode 1807. Évaluer les paires de cordes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de solution – 3 langues

Vous trouverez ci-dessous des implémentations propres et prêtes à la production pour **Java**, **Python** et **C++**.
Chacun suit la même idée :

1. Construisez une carte hash (`key → value`) à partir de la liste `knowledge`.
2. Scanner la chaîne `s` une fois.
* Lorsque nous voyons `'('`, nous recueillons les caractères jusqu'à `')'`, cherchons la clé dans la carte et ajoutons la valeur (ou `''?" si elle n'existe pas).
* Tous les autres caractères sont copiés in extenso.
3. Utilisez un constructeur de chaînes efficace (`StringBuilder`, `vector<string>` + `join`, `std::string` + `reserve`) pour maintenir l'exécution linéaire.

---

Java

"Java
Importer java.util. HashMap;
Importer java.util. Liste;
Importer java.util. Carte;

solution de classe publique {
public Évaluation des chaînes(String s, Liste<Liste<String>> connaissances) {
// 1. Construire la carte de recherche
Carte <String, String> carte = nouveau HashMap<>();
pour (Liste <String> paire : connaissance) {
map.put(pair.get(0), pair.get(1));
}

// 2. Scanner la chaîne
StringBuilder ans = nouveau StringBuilder(s.longueur());
i = 0;
pendant que (i < s.longueur()) {
c = s.charAt(i);
si c == '(') {
// Extraire la clé
i + 1;
StringBuilder keyBuilder = nouveau StringBuilder();
(j < s.length() && s.charAt(j) != ')) {
keyBuilder.append(s.charAt(j));
j++;
}
Clé de chaîne = keyBuilder.toString();
as.append(map.getOrDefault(key, "?"));
i = j + 1; // sauter après ') '
} autre {
l'annexe c);
i++;
}
}
retourner les ans.àString();
}
}
«» "

> **Pourquoi c'est rapide* *
> * temps O(n + m), où `n =====`` et `m` est la longueur totale de toutes les clés dans `connaissance`.
> * O(m) espace supplémentaire pour la carte.

---

Python

'`python
de taper l'importation Liste

Solution de classe:
def evalue(self, s: str, knowledge: List[List[str]]) -> str:
1. Construire la carte
recherche = {k: v pour k, v dans la connaissance}

2. Scanner une fois
res = []
i = 0
alors que i < len(s):
si s[i] == '(':
j = i + 1
alors que s[j] != '):
j += 1
clé = s[i+1:j]
res.append(lookup.get(key, '?'))
i = j + 1
Sinon:
res.append(s[i])
i += 1
retour ''.join(res)
«» "

> **Tricks spécifiques au python* *
> * `list` + `''.join()` est plus rapide que la concaténation des chaînes.
> * La compréhension du dictionnaire maintient le code en ordre.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
évaluation de la chaîne (chaîne s, vecteur<vector<string>> et connaissance) {
// 1. Construction de cartes
unordered_map<string, string> mp;
mp.reserve(knowledge.size() * 2); // éviter les rehash
pour (auto& p : connaissance) mp[p[0]] = p[1];

// 2. Scannage d'un seul passage
ficelles et cordes;
as.reserve(s.size()); // accélération
pour (size_t i = 0; i < s.size(); ++i) {
si (s[i] == '(') {
clé de chaîne;
++i; // sauter '('
(i < s.size() && s[i] != ')) {
key.push_back(s[i++]);
}
ans += mp.count(key) ? mp[key] : "?";
} autre {
le nom de l'autorité compétente;
}
}
le retour des an;
}
};
«» "

> **C++ faits saillants* *
> * La réserve réduit les réaffectations.
> * L'utilisation de `unordered_map` donne une recherche O(1) moyenne.

---

Billet de blog – *Le bon, le mauvais et le mauvais de LeetCode 1807*

Récapitulation des problèmes

> **LeetCode 1807 – Évaluer les paires de supports d'une corde**
> On vous donne une chaîne `s` qui contient des clés entre crochets, par exemple `"(name)is(age)yearsold"`.
> Un tableau 2-D `connaissance` contient des paires de clés/valeurs.
> **Objectif** – remplacer chaque ""(clé)" avec sa valeur ou `?` si la clé n'est pas connue.
> Il n'y a pas de crochets nichés.

Pourquoi c'est une question d'entrevue à moyenne difficulté

* **Essayez l'analyse** – pas aussi trivial qu'un régex en raison des délais.
* **L'utilisation de la carte deash** – démontre la compréhension de la recherche O(1).
* ** Manipulation des caisses** – clés manquantes, grandes entrées (longueur de 1e5).
* **Efficiency mindset** – vous ne pouvez pas vous permettre une solution `O(n2)`.

L'approche simple et propre

1. **Construisez une carte de hachage** – `O(m)` où `m` est le nombre de paires de connaissances.
2. **Scan unique** – marcher à travers `s` une fois, construire la réponse à la volée.
3. **O(n + m) temps** et **O(m) espace** – optimal pour les contraintes.

C'est exactement ce que font l'éditorial officiel et la majorité des meilleures solutions. Il est élégant, lisible et passe tous les tests en millisecondes.

### Le "Bad" – Quoi éviter

Une erreur Pourquoi elle est mauvaise
- C'est quoi ?
**Regex** (`re.sub`)= Bien qu'il semble soigné, le moteur regex peut être lent sur les chaînes de longueur `1e5` et peut frapper la limite de récursion de Python=s sur les groupes imbriqués. Le délai dépassé (TLE). Autres
Autres **Placez pour chaque '('**) Vous finirez par pousser la touche entière sur la pile, et vous avez encore besoin d'une recherche de carte de hachage. O(n) espace supplémentaire, aucun avantage de performance. Autres
**Concaténation des chaînes de caractères à répétition**.En Java ou Python, construire une nouvelle chaîne de caractères à chaque fois mène à l'heure O(n2). TLE ou haute utilisation de la mémoire. Autres
**Ignorer la règle de ""**" Certaines solutions oublient de remplacer les clés inconnues, retournant la ""(clé)" brute". Une mauvaise réponse (WA). Autres

### Le "Ugly" – Sur-Ingénierie et pièges

1. ** Programmation dynamique** – Il n'y a pas de récurrence de sous-problème ici; DP ajouterait simplement des frais généraux.
2. **Traitement personnalisé pour les clés** – Non nécessaire; une carte de hachage est plus simple et plus rapide.
3. **L'utilisation intensive d'itérateurs ou de flux** – rend le code plus difficile à lire et peut nuire aux performances en boucles serrées.
4. **Longueur de la chaîne de codage à chaud** – La suroptimisation peut se retourner lorsque les tailles d'entrée changent.

**Ligne de bottom:** S'en tenir à la simple hash‐map + scan linéaire. C'est ce que les intervieweurs attendent et ce qui passe tous les cas d'essai.

Décomposition

Étape Temps Espace
C'est pas vrai.
Construire une carte Autres
Numérisation de `s` (sauf la chaîne de résultats)
**Total** Autres

Avec `n, m ≤ 100 000`, cela correspond facilement à 1 seconde limite de temps et quelques mégaoctets de mémoire.

Conseils du monde réel pour les entrevues

* **Lisez les contraintes d'abord** – elles laissent entendre la complexité du temps nécessaire.
* **Mentionnez votre approche à l'avance** – -I=ll utilise une carte de hachage pour stocker les paires de clés/valeurs, puis scannez la chaîne une fois. (en milliers de dollars)
* **Parler de cas bord** – Si la clé n'est pas trouvée, nous produisons ‘?
* ** Expliquez pourquoi vous évitez le régex** – Bien que le régex soit puissant, il peut être lent pour les grandes entrées et peut dépasser les limites de récursion. (en milliers de dollars)
* **Afficher votre code dans la langue de votre choix** – fournir des extraits clairs et commentés.

Comment cela aide votre chasse à l'emploi

* **Diversité linguistique** – Vous pouvez résoudre le même problème en Java, Python et C++.
* ** Démontrer la compréhension algorithmique** – Le hash‐map + single pass est un modèle d'entrevue classique.
* **Titre convivial pour le référencement** – *CodeLeet 1807 – Évaluer les paires de supports d'une chaîne – Java, Python, C++ Solutions (HashMap Approach)*
* **Partager sur LinkedIn/Twitter** – Utilisez les balises pertinentes (#LeetCode, #CodingInterview, #HashMap, #Java, #Python, #CPlusPlus) pour attirer les recruteurs.
* **Créer un billet de blog** – Inclure l'énoncé du problème, votre solution, et l'analyse de "good/bad/ugly". Les recruteurs aiment lire, expliquer le contenu.

### -Départ final

La solution optimale est *simple* et *fast*: une carte de hachage plus un balayage linéaire.
Évitez le régex, les piles imbriquées et la complexité inutile.
Avec un code propre et une explication claire, vous impressionnerez interviewers et obtenir remarqué par l'embauche des gestionnaires à la recherche de l'expertise LeetCode.

Bon codage ! C'est ce qu'il a dit.

---

> **Auteur** – [Votre nom]
> *Les extraits de code complets sont joints ci-dessus. N'hésitez pas à copier, adapter et poster! *
> **Contact** – courriel@domain.com. Twitter: @votre main

---

Tu veux demander autre chose ?
Laissez un commentaire ou DM me – Je suis ici pour vous aider à as la prochaine interview!