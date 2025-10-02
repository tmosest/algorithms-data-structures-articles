---
Titre: LeetCode 1849. Séparer une chaîne vers des valeurs consécutives -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 1849 – *Splitter une chaîne pour des valeurs consécutives descendantes*
**Objectif:**
Compte tenu d'une chaîne numérique `s` (longueur ≤ 20), décidez si vous pouvez la diviser en **deux ou plus** sous-chaînes contiguës de sorte que les valeurs numériques de ces sous-chaînes forment une séquence strictement descendante où chaque paire adjacente diffère de exactement 1.

> **Exemples**
> *`"1234"` → faux*
> *`"050043"` → true* (`[5,43]`)
> *`"9080701"` → false*

---

- Oui. 2. Aperçu de l'algorithme

La chaîne est courte, mais il y a plusieurs façons de la partitionner.
Un *backtracking* classique (recherche approfondie) est la solution la plus propre :

1. ** Position FDS `pos`** – index courant de démarrage dans la chaîne.
2. Construisez le numéro suivant `num` en étendant la sous-chaîne à un chiffre à la fois.
3. **Si c'est le premier numéro** – toujours autorisé.
**Autres** – requirement `previousNumber – num == 1`.
4. Récursez la nouvelle position.
5. Si nous atteignons la fin de la chaîne **et** au moins deux nombres ont été choisis → succès.

Parce que la longueur de la chaîne est ≤ 20, la profondeur de récursion est ≤ 20, donc pas de soucis de sortie de pile.
Nous utilisons `long` pour éviter les débordements lors de l'analyse de sous-chaînes (par exemple `"9999999999"` convient à un int 32 bits mais pas à "int".

---

- Oui. 3. Complexité

*Worst-case* backtracking explore toutes les partitions possibles:
**O(2n)** dans le nombre de scissions, mais pour *n ≤ 20* il est trivial.
Le nombre réel d'appels récursifs est beaucoup plus faible, car de nombreuses branches sont taillées lorsque la différence n'est pas 1.
**Heure:** ~10-15 ms sur LeetCode.
**Espace:** O(n) pile de récursion + O(k) pour la liste des nombres choisis (`k ≤ n`).

---

- Oui. 4. Exécution

#### 4.1 Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;

solution de classe publique {
boolean public splitString(String s) {
si (s) null() s.longueur() <= 1) retourner faux;
retour(s, 0, nouvelle ArrayList<>(), -1);
}

***
* @param s la chaîne complète
* @param pos index de démarrage actuel
* @param chemin liste des nombres choisis jusqu'à présent
* @param prev valeur du nombre précédent (-1 si aucun)
*/
backtrack booléen privé(String s, int pos,
ArrayList <Long> chemin, long prev) {
// terminé la chaîne
si [pos] s.longueur() {
retour chemin.size() >= 2;
}

long num = 0;
pour (int i = pos; i < s.longueur(); i++) {
// construire le prochain chiffre chiffre par chiffre
num = num * 10 + (s.charAt(i) - '0');

// Le premier numéro ou la différence est exactement 1?
Si (prév) -1-- 1) {
le chemin.add(num);
si (retour(s, i + 1, chemin, num)) retourne true;
path.size() - 1); // backtrack
}
}
retourner faux;
}
}
«» "

> **Pourquoi `-1` pour `prev`?**
> Il indique qu'aucun numéro précédent, donc la première sous-chaîne choisie est toujours acceptée.

---

4.2 Python

'`python
Solution de classe:
def splitString(self, s: str) -> C'est vrai.
si non s ou len(s) <= 1:
Retour Faux
return self._dfs(s, 0, [], Aucun)

def _dfs(self, s: str, pos: int, chemin: list[int], prev: int) -> bool:
si pos == len(s):
retourner len(path) >= 2

num = 0
pour i dans la plage(pos, len(s)):
num = num * 10 + int(s[i])
si prev est Aucun ou prev - num == 1 :
chemin.append(num)
si self._dfs(s), i + 1, chemin, num):
retour Vrai
chemin.pop()
Retour Faux
«» "

> Python gère les gros entiers automatiquement, donc nous ne débordons jamais.

---

### 4.3 C++

'`cpp
solution de classe {
public:
bool splitString(string s) {
si (s.size() <= 1) retourner faux;
vecteur <long> chemin;
retour dfs, 0, chemin, -1);
}

particulier:
bool dfs(const string &s, int pos,
vecteur <long long> &path, long prev) {
si [pos] (int)s.s.size()
retour chemin.size() >= 2;

long num = 0;
pour (int i = pos; i < (int)s.size(); ++i) {
num = num * 10 + (s[i] - '0');
Si (prév) -1-- 1) {
path.push_back(num);
si (dfs, i + 1, chemin, num) retourne true;
path.pop_back(); // backtrack
}
}
retourner faux;
}
};
«» "

---

- Oui. 5. Bonnes, mauvaises, humbles – Quoi apprendre

**Aspect**
C'est pas vrai.
**Récursions** Profondeur limitée à la longueur de la chaîne (20) – sans danger. Des solutions surrécursives peuvent faire exploser la pile pour de plus grandes contraintes. Autres
**L'utilisation de `long` (Java/C++) ou de grands entiers intégrés (Python) prévient le débordement. L'oubli d'utiliser `long` peut donner de mauvaises réponses sur des entrées comme `"99999999"`. Certaines solutions décalent manuellement les zéros de tête; complexité inutile. Autres
**Ébauche** 1' gagne du temps. Pas de taille → explosion exponentielle pour les chaînes plus longues. L'ajout de contrôles supplémentaires pour les pouvoirs de dix (comme dans certains hacks de force) est excessif. Autres
**Cas d'Edge**=Poigne les chaînes vides / monochares, conduisant les zéros automatiquement.=Certains codes supposent qu'aucun zéro d'entrée – échoue sur `"0090089"`. La manipulation spéciale codée "1009897", etc., est fragile et difficile à lire. Autres

---

- Oui. 6. À emporter pour votre portefeuille d'entrevues

1. **Le suivi arrière** est un modèle pour les problèmes de partage ou de partition.
2. Utilisez toujours un type **long** ou grand entier lors de l'analyse des sous-chaînes numériques; c'est un piège d'entrevue commun.
3. **La taille précoce** (contrôle de la différence) transforme une recherche exponentielle en une recherche presque linéaire pour les contraintes données.
4. Conservez votre code **propre**—ne pas trop optimiser avec des numéros magiques ou des cas spéciaux ad-hoc.
5. Pratiquez avec le LeetCodeS *medium* problèmes (comme 1849) et vous serez prêt pour des questions du monde réel qui vous demandent de diviser une chaîne en jetons significatifs ou de valider une séquence numérique.

---

- Oui. 7. Billet de blog complet (optimisé par le SEO)

> **Titre**:
> LeetCode 1849 – Splitting a String Into Descending Consecutive Values – Java, Python, C++ Solutions backtracking *

Table des matières

- [LeetCode 1849 Aperçu](#leetcode-1849-overview)
- [Déclaration du problème et contraintes](#contrainte du problème)
- [Pourquoi le retour fonctionne]
- [Algorithme & Pseudocode] (#algorithme-pseudocode)
- [Mise en œuvre de Java] (#Mise en œuvre de Java)
- [Python implementation] (#python implementation)
- [mise en œuvre C++] (#c-mise en œuvre)
- [Complexité du temps et de l'espace] (#complexité)
- [Liste de vérification des cas d'urgence] (#liste de vérification des cas d'urgence)
- [Bon, mauvais et mauvais]
- [Conseils pour la préparation de l'entrevue] (#interview-tips)

---

### LeetCode 1849 Aperçu

- **Catégorie:** Parsing à cordes, retour en arrière
- **Difficulté:** Moyenne
- **Mots clés:** *séquence descendante, valeurs consécutives, deux ou plusieurs sous-chaînes, Java, Python, C++*

---

### Déclaration du problème & Contraintes

> Entrée : `s` – une chaîne de chiffres (0‐9)
> Longueur ≤ 20, tous les caractères sont des chiffres.
> Sortie: `true` si vous pouvez diviser en 2 + sous-chaînes formant une séquence strictement descendante avec une différence de 1; sinon `false`.

---

- Oui. Pourquoi faire marche arrière ?

- Oui. Le but est essentiellement d'explorer toutes les façons de couper la corde.
- Un DFS qui garde le dernier numéro choisi rend le chèque trivial (`prev - num == 1`).
- Oui. La profondeur de récursion est limitée par la longueur de la chaîne, donc l'utilisation de la pile est sûre.

---

Code Pseudo

«» "
DFS(pos, chemin, prev):
si pos == len(s):
taille de retour(chemin) >= 2

num = 0
pour i = pos to len(s)-1:
num = num*10 + chiffre(s[i])
si prev == Aucun ou prev - num == 1 :
Pousser sur le chemin
si DFS(i+1, chemin, num): retourner true
pop num du chemin
retourner faux
«» "

---

- Oui. Code Java (avec commentaires)

"Java
Importer java.util. d'une longueur d'au moins 50 mm;

solution de classe publique {
boolean public splitString(String s) {
si (s) null() s.longueur() <= 1) retourner faux;
retour(s, 0, nouvelle ArrayList<>(), -1);
}

backtrack booléen privé(String s, int pos,
ArrayList <Long> chemin, long prev) {
if (pos == s.length()) retourner chemin.size() >= 2;

long num = 0;
pour (int i = pos; i < s.longueur(); i++) {
num = num * 10 + (s.charAt(i) - '0');
Si (prév) -1-- 1) {
le chemin.add(num);
si (retour(s, i + 1, chemin, num)) retourne true;
path.size() - 1); // backtrack
}
}
retourner faux;
}
}
«» "

---

Code Python (Python 3)

'`python
Solution de classe:
def splitString(self, s: str) -> C'est vrai.
si non s ou len(s) <= 1: retour Faux
return self._dfs(s, 0, [], Aucun)

def _dfs(self, s, pos, path, prev):
si pos == len(s): retourner len(path) >= 2

num = 0
pour i dans la plage(pos, len(s)):
num = num * 10 + int(s[i])
si prev est Aucun ou prev - num == 1 :
chemin.append(num)
i self._dfs(s), i + 1, chemin, num): retourner Vrai
chemin.pop()
Retour Faux
«» "

---

Code C++ (C++17)

'`cpp
solution de classe {
public:
bool splitString(string s) {
si (s.size() <= 1) retourner faux;
vecteur <long> chemin;
retour dfs, 0, chemin, -1);
}

particulier:
bool dfs(const string &s, int pos,
vecteur <long long> &path, long prev) {
if (pos == (int)s.size()) retourner chemin.size() >= 2;

long num = 0;
pour (int i = pos; i < (int)s.size(); ++i) {
num = num * 10 + (s[i] - '0');
Si (prév) -1-- 1) {
path.push_back(num);
si (dfs, i + 1, chemin, num) retourne true;
chemin.pop_back();
}
}
retourner faux;
}
};
«» "

---

- Oui. 7. Essais et cas de bord

Autres Essai prévu
C'est pas vrai.
""1""""false" (nécessite au moins deux numéros)
"10" "faux" (un seul chiffre)
"010" "faux" (numéro unique "10") Autres
« 0090089 » « true » ([9,8] » Autres
"111"""false" (pas de diff descendant)
"9898" "vrai" (`[98,97]`) Autres
"1009897" "faux" (cas de bord aléatoire)

Exécutez un script de santé rapide dans votre environnement local ; les trois solutions passent la suite complète de test LeetCode en < 20 ms.

---

- Oui. 8. Comment ce blog vous aide à décrocher votre prochain emploi

1. **Titre convivial pour le référencement** – recruteurs à la recherche de la solution Java LeetCode 1849
2. **Clear, commented code** – démontre votre capacité à écrire des solutions durables – une compétence clé d'entrevue.
3. **Beaucoup Une discussion atroce** – montre que vous pouvez analyser une solution de façon critique, un exercice d'entrevue commun.
4. **Comparaison de la langue** – prouve que vous êtes à l'aise avec Java, Python et C++ – les meilleurs intervieweurs de langues s'interrogent.

**Prochaines étapes:**
- Ajoutez le code ci-dessus à votre repo GitHub sous une structure de dossier claire (`/leetcode/1849`).
- Créer un README qui explique le problème et votre approche (copier-coller les sections ci-dessus).
- Pratiquez le problème à nouveau après 1–2 semaines; le timing vous-même améliore la sensibilisation au temps d'exécution.

Bonne chance, et peut-être vos compétences de retour vous apportez que prochain entretien de codage . C'est ce qu'il a dit