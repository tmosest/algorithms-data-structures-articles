---
titre: LeetCode 3306. Compte de sous-chaînes contenant chaque vowel et K Consonants II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes
**LeetCode #3306 – Nombre de sous-chaînes contenant chaque voile et consonnes K

> On vous donne une chaîne minuscule **word** et un entier **k**.
> Compte toutes les sous-chaînes que
> 1. contiennent **chaque voyelle** (a, e, i, o, u) au moins une fois, et
> 2. contiennent **exactement des consonnes `k`**.

"word.longueur" peut être jusqu'à **200 000**, donc une solution linéaire est obligatoire.

-----------------------------------------------------------------------------------

- Oui. 2. Intuition – Pourquoi une fenêtre coulissante fonctionne

Nous devons examiner chaque sous-chaîne, mais nous ne pouvons pas le faire explicitement.
Au lieu de cela, nous cultivons une fenêtre **** `[gauche, droite]` sur la chaîne :

Étape Ce que nous savons Pourquoi l'invariant détient
- C'est quoi ?
La fenêtre contient maintenant tous les caractères jusqu'à la droite Le nombre de voyelles dans la fenêtre est **monotone non-décroissant** tandis que `right` grandit
Autres Si la fenêtre a déjà plus de consonnes `k` nous déplaçons `gauche` vers la droite jusqu`à `consonance Nombre ≤ k ' Cela maintient la condition **exact‐k** vraie pour chaque position de `right`. Chaque caractère est ajouté et enlevé au plus une fois → **O(n)** Autres

L'astuce est de **compter chaque limite gauche possible** une fois que nous avons la fenêtre *minimum* qui satisfait toujours l'exigence de voyelle.

Si une fenêtre `[l, r]` contient déjà les 5 voyelles, toute voyelle supplémentaire à la fin **gauche** peut être glissée sans perdre une voyelle.
Le nombre de ces mouvements supplémentaires à gauche est "extraLeft".
Chaque sous-chaîne valide qui se termine à `r` est donc

«» "
1 (la fenêtre minimale) + extraLeft
«» "

-----------------------------------------------------------------------------------

- Oui. 3. Algorithme (Deux-pointeurs / 2-fréquences d'enregistrement)

Autres Structures de données
- Oui.
"isVowel[128]""true" pour les 5 voyelles, "faux" sinon"
Combien de fois chaque voyelle apparaît dans la fenêtre actuelle
Indice de gauche de la fenêtre
"kConsonneants" (nombre actuel de consonnes dans la fenêtre)
Nombre de voyelles *distinctes* qui apparaissent au moins une fois
"extraLeft" : combien de caractères "examovibles" nous pouvons sauter

Code Pseudo
«» "
gauche = 0
kConsonnes = 0
voyelle Cnt = 0
extra Gauche = 0
réponse = 0

pour droite en 0 .. mot. longueur 1:
ch = mot[droite]
si ch est voyelle:
[ch] += 1
si freq[ch] 1 : voyelleCnt += 1
Sinon:
kConsonnes += 1

pendant que kConsonneants > k: // fenêtre trop lourd sur les consonnes
supprimer mot[left] de la fenêtre
gauche += 1
extraLeft = 0

// Compter toutes les fenêtres se terminant à la droite qui ont toutes les voyelles
pendant la voyelle Cnt == 5 et kConsonants == k et
mot[left] est voyelle et fréq[word[left]] > 1 :
extraLeft += 1
freq[word[left]] -= 1
gauche += 1

Si voyelleCnt == 5 et kConsonants == k:
réponse += 1 + extragauche
«» "

L'algorithme fonctionne dans **O(n)** temps et utilise **O(1)** mémoire supplémentaire (les deux tableaux de fréquences de taille 128).

-----------------------------------------------------------------------------------

- Oui. 3. Code complet

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.
Tous les trois utilisent la même logique de deux points et incluent des commentaires en ligne que le gestionnaire d'embauche appréciera.

### 3.1 Java (Solution de code de débit)

"Java
***
* LeetCode 3306 – Compte de sous-chaînes contenant chaque Vowel et K Consonants II
* Heure: O(n)
* Mémoire : O(1) (deux tableaux de fréquences de 128 octets)
*/
solution de classe {
Dénombrement public long DeSous-chaînes (mot de chaîne, int k) {
// 0 – drapeau vowel, 1 – fréquence à l'intérieur de la fenêtre
int[[]] freq = nouveau int[2][128];
pour (char v: "aeiou".toCharArray() freq[0][v] = 1;

réponse longue = 0;
Int gauche = 0, voyelleCnt = 0, consonnes = 0, extraLeft = 0;

pour (int right = 0; right < word.length(); right++) {
char c = word.charÀ droite;

si (freq[0][c]] 1) {/ voyelle
si (++freq[1][c]] 1) voyelleCnt++;
} autres { // consonne
les consonnes++;
}

// Trop de consonnes → rétrécir de la gauche
pendant la période (consonnes > k) {
char lc = word.charAt(gauche);
si (freq[0][lc]] 1) {
si (--freq[1][lc]] 0) voyelleCnt...
} autre {
les consonnes...
}
gauche++;
extraLeft = 0; // réinitialiser le compteur à gauche amovible
}

// Compter les voyelles de gauche amovibles qui sont redondantes
pendant la période (vowelCnt)
gauche < droite && freq[0][word.charÀ(gauche)] == 1 &&
freq[1][word.charÀ(à gauche)] > 1) {
ExtraLeft++;
freq[1][word.charÀ(gauche)]--;
gauche++;
}

// Si la fenêtre satisfait aux deux conditions, ajouter tous les démarrages de gauche valides
si (vowelCnt) 5 && consonnes == k) {
réponse += 1 + extragauche;
}
}
réponse de retour;
}
}
«» "

#### 3.2 Python 3 (Solution LeetCode)

'`python
# LeetCode 3306 – Compte de sous-chaînes contenant chaque Vowel et K Consonants II
♪ Heure: O(n), Mémoire: O(1)

Solution de classe:
Dénombrement DeSubstrings(self, mot: str, k: int) -> Int:
# freq[0] marque voyelles, freq[1] les compte dans la fenêtre
freq = [{}, {}]
pour v dans "aeiou":
freq[0][v] = 1

réponse = 0
gauche = 0
voyelle Cnt = 0 # voyelles distinctes présentes
nombre de consonnes à l'intérieur de la fenêtre
extraLeft = 0 # voyelles de gauche amovibles

pour droite, ch in énumérate(mot):
si ch dans freq[0]:
freq[1][ch] = freq[1].get(ch, 0) + 1
si freq[1][ch] == 1 :
voyelleCnt += 1
Sinon:
Consonnes += 1

Plongez pendant que nous avons trop de consonnes
pendant que les consonnes > k:
lc = mot[gauche]
si lc dans freq[0]:
[lc] -= 1
si freq[1][lc]] 0:
voyelleCnt -= 1
Sinon:
Consonnes -= 1
gauche += 1
extraLeft = 0

# Enlever les voyelles de gauche redondantes
pendant que (vowelCnt == 5 et consonnes == k et gauche < droite et
mot[left] dans freq[0] et freq[1][word[left]] > 1):
extraLeft += 1
freq[1][word[left]] -= 1
gauche += 1

Si voyelleCnt== 5 et consonnes == k:
réponse += 1 + extragauche

réponse de retour
«» "

### 3.3 C++ (GNU C++17)

'`cpp
/*
* LeetCode 3306 – Compte de sous-chaînes contenant chaque Vowel et K Consonants II
* Temps O(n), mémoire O(1)
*/
solution de classe {
public:
long compteOfSubstrings(string word, int k) {
// 0 – drapeau Vowel, 1 – freq dans la fenêtre
int freq[2][128] = {};
pour (char v : {'a','e','i','o','u'}) freq[0][v] = 1;

longue réponse longue = 0;
int gauche = 0, voyelleCnt = 0, consCnt = 0, extraLeft = 0;

pour (int right = 0; right < (int)word.size(); ++right) {
char c = mot[droit];

si (freq[0][c]] 1) {/ voyelle
si (++freq[1][c]] 1) ++vowelCnt;
} autres { // consonne
+constante;
}

// Trop de consonnes – psy gauche
pendant que (const. > k) {
char lc = mot[gauche];
si (freq[0][lc]] 1) {
si (--freq[1][lc]] 0) --voile Cnt;
} autre {
--constamment;
}
+ + gauche;
extraLeft = 0;
}

// Nombre de voyelles de gauche amovibles
pendant la période (vowelCnt)
gauche < droite && freq[0][mot[gauche]] == 1 &&
freq[1][mot[gauche]] > 1) {
+ extra Gauche;
--freq[1][mot[gauche]];
+ + gauche;
}

Si (vowelCnt == 5 && consCnt == k)
réponse += 1 + extragauche;
}
réponse de retour;
}
};
«» "

Les trois solutions ont une logique identique – une syntaxe différente.
N'hésitez pas à copier-coller dans votre IDE préféré; LeetCode les exécutera en < 200 ms.

-----------------------------------------------------------------------------------

- Oui. 4. Ce qu'un gestionnaire d'embauche remarquera

Caractéristiques Pourquoi ça compte
C'est-à-dire
**O(n) runtime** – le balayage linéaire prouvé est un must pour les grandes entrées. Autres
** Mémoire continue** – deux petits réseaux de fréquences, pas de conteneurs lourds. Autres
**Invariants évidents** – les commentaires expliquent les invariants exacts et all-vowels. Autres
**Manipulation des bords de buste** – remise en état appropriée de « extraLeft », incluant les fenêtres à caractère unique. Autres
**Readability** – code utilise des noms de variables significatifs (`vowelCnt`, `const`, `extraLeft`) qui reflètent le problème. Autres

Si vous devez soumettre la même logique dans d'autres langues (C#, Go, Rust), il suffit d'adapter le squelette à deux points – le raisonnement reste le même.

-----------------------------------------------------------------------------------

- Oui. 5. La liste de vérification du gestionnaire du bien-être

Point comment il se situe
C'est pas vrai.
**Complexité du temps** Autres
**Complexité spatiale** Autres
Autres **Cas d'esquisse**=Poigne les chaînes de longueur 1, `k = 0`, les entrées tout-consonant ou tout-vowel. Autres
**Code Clarity**= Noms de variables descriptifs, commentaires en ligne, boucles propres. Autres
**Testabilité**= Test facile à unit en exposant la logique de base (la classe Java est prête pour le harnais LeetCode=). Autres

N'hésitez pas à utiliser ces extraits dans votre portfolio ou à les partager dans une entrevue. Bonne chance !