---
titre: LeetCode 1234. Remplacer la sous-chaîne pour la chaîne équilibrée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation du problème

> **Remplacer la sous-chaîne pour la chaîne équilibrée* *
> On vous donne une chaîne `s` de longueur `n` qui ne contient que les quatre caractères `Q`, `W`, `E`, `R`.
> Une chaîne est *équilibrée* si chaque caractère apparaît exactement `n / 4` fois.
> Dans une opération, vous pouvez remplacer **toute substring contigu** de `s` par une autre chaîne de la même longueur (la nouvelle chaîne peut être choisie arbitrairement).
> Retournez la longueur **minimum** de la sous-chaîne que vous devez remplacer afin de faire équilibrer `s`.
> Si `s` est déjà équilibré, retourner `0`.

> *Contrôles*
> * `4 ≤ n ≤ 105`
> * `n` est un multiple de `4`
> * `s` contient uniquement `Q`, `W`, `E`, `R`

La solution classique utilise une technique de fenêtre de glissement ** (deux points).

---

- Oui. 2. Algorithme – Fenêtre coulissante

1. **Comparer la fréquence** de chaque personnage dans toute la chaîne.
2. Calculer «requis = n / 4».
Pour chaque caractère `c` nous ne *beed* `freq[c] - required` d'entre eux dans la sous-chaîne nous remplacerons – si la valeur est ≤ 0 le caractère est déjà équilibré ou sous-représenté et nous n'avons pas besoin de le supprimer.
3. Si chaque `freq[c] == requis`, la chaîne est déjà équilibrée → retourner `0`.
4. Initialiser une fenêtre `[l, r)` (inclus à gauche, exclusive à droite).
Déplacez le bout droit d'une étape à la fois, *décrementant* le compteur nécessaire pour le caractère qui entre dans la fenêtre.
5. Alors que la fenêtre contient déjà *au moins* le nombre nécessaire de chaque caractère surreprésenté, essayez de le réduire de la gauche (incrément `l` et *incrément* le compteur pour ce caractère).
Mettre à jour la réponse avec la longueur de la fenêtre actuelle à chaque fois que la fenêtre est « good ».
6. La plus petite fenêtre trouvée est la réponse.

> **Pourquoi ça marche* *
> La fenêtre représente une sous-chaîne de candidats que nous remplacerons.
> Lorsque la fenêtre contient tous les caractères « Excess » , le reste de la chaîne a déjà le bon nombre, donc remplacer la fenêtre peut corriger la chaîne entière.
> En glissant la fenêtre avec cupidité et en la rétrécissant chaque fois que possible, nous garantissons que nous testons les plus petites sous-chaînes possibles.

Complexité

Opération Temps Espace
- C'est quoi ?
Nombre de fréquences Autres
Fenêtre coulissante Autres

Dans l'ensemble: **'O(n)' temps, `O(1)' espace auxiliaire**.

---

- Oui. 3. Mise en œuvre des références

Voici des implémentations propres et bien commentées dans **Java**, **Python** et **C++**.
Chacun contient une petite aide `main`/`solve` qui peut être utilisée pour les tests locaux.

---

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
// caractère de carte pour indexer 0..3
Int idx privé(char c) {
interrupteur de retour (c) {
dossier 'Q' -> 0;
l'affaire W -> 1;
l'affaire «E» -> 2;
par défaut -> 3; // 'R'
};
}

secteur public Chaîne(s) {
int n = s.longueur();
int requis = n / 4;

// 1) fréquences totales
int[] freq = nouveau int[4];
pour (int i = 0; i < n; i++) {
freq[idx(s.charAt(i))]++;
}

// 2) calculer combien de chaque char nous devons enlever
besoin int[] = nouvelle int[4];
booléen équilibré = vrai;
pour (int i = 0; i < 4; i++) {
si (freq[i] > requis) {
besoin[i] = freq[i] - requis;
équilibre = faux;
}
}
si (équilibré) retour 0; // déjà équilibré

// 3) fenêtre coulissante
int gauche = 0, meilleur = n;
pour (int right = 0; right < n; right++) {
int id = idx(s.charAt(right));
need[id]--; // char entre dans la fenêtre

// rétrécir pendant que la fenêtre contient suffisamment de chaque char surreprésenté
pendant que (tous les nonpositifs(besoin)) {
best = Math.min (best, droit - gauche + 1);
need[idx(s.charAt(left))]++; // char quitte la fenêtre
gauche++;
}
}
le meilleur retour;
}

booléen privé tousNonPositive(int[]a) {
pour (int v : a) si (v > 0) retourner faux;
retour vrai;
}

// ----- pour les essais locaux -----
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.equilibredString("QWER")); // 0
Système.out.println(sol.equilibredString("QQWE")); // 1
Système.out.println(sol.equilibredString("QQQW")); // 2
}
}
«» "

---

3.2 Python

'`python
importations

Solution de classe:
et équilibrés Chaîne(s) -> Int:
n = len(s)
Req = n // 4

Nombre de fréquences
freq = {c: 0 pour c dans 'QWER'}
pour ch en s:
[ch] += 1

# combien de chaque char doit être enlevé de la fenêtre
besoin = {c: max(0, freq[c] - req) pour c dans 'QWER'}
si all(v == 0 pour v dans need.values()):
retour 0

# fenêtre coulissante
gauche = 0
meilleure = n
pour droite, ch en énumération(s):
besoin[ch] -= 1 # char entre dans la fenêtre

alors que all(v <= 0 pour v dans need.values()):
best = min (meilleur, droit - gauche + 1)
besoin[s[gauche]] += 1 # char quitte la fenêtre
gauche += 1

le meilleur retour


# ----- tests locaux -----
si __nom__ == "__main__" :
sol = Solution()
print(sol.equilibredString("QWER")) # 0
print(sol.equilibredString("QQWE")) # 1
print(sol.equilibredString("QQQW")) # 2
«» "

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int équilibré Chaîne(s) {
int n = s.size();
la valeur de référence est égale à n / 4;
tableau <int, 4> cnt = {0, 0, 0};
auto id = [](char c) {
interrupteur c) {
case «Q»: retour 0;
case «W»: retour 1;
Cas «E»: retour 2;
par défaut : retourner 3; // 'R'
}
};

pour (charc : s) cnt[id(c)]++;

tableau <int, 4> besoin;
bool équilibré = vrai;
pour (int i = 0; i < 4; ++i) {
si (cnt[i] > req) {
need[i] = cnt[i] - req;
équilibre = faux;
} autre besoin[i] = 0;
}
si (équilibré) retour 0;

int gauche = 0, meilleur = n;
pour (int droite = 0; droite < n; ++ droite) {
need[id(s[right])]--; // window s'étend

pendant que (all_of(need.begin(), need.end(),
[](int v){ retour v <= 0; }) {
best = min (meilleur, droit - gauche + 1);
need[id(s[left])]++; // rétrécir à partir de la gauche
+ + gauche;
}
}
le meilleur retour;
}
};

// ----- test local -----
Int main() {
Solution sol;
Cout << sol.equilibredString("QWER") << endl; // 0
Cout << sol.equilibredString("QQWE") << enl; // 1
cout << sol.equilibredString("QQQW") << enl; // 2
retour 0;
}
«» "

---

- Oui. 4. Article de blog – *Le Bon, le Mauvais, et l'Ugly de Replacer la sous-chaîne pour les cordes équilibrées

> *Publié en 2025‐09‐26] Tags: #LeetCode #CodingInterview #Algorithmes #SlidingWindow #JobSearch*

---

4.1 Pourquoi ce problème est important pour les recruteurs

Les recruteurs aiment les problèmes de LeetCode qui testent **maîtrise de la structure des données + conception d'algorithmes intelligents**.
Ce problème se trouve dans le seau *medium*, mais sa solution nécessite :

1. **Observer la surreprésentation** – un petit tour de la logique qui montre que vous pouvez penser *au-delà* de l'évident compte chaque personnage.
2. **Fenêtre coulissante** – une technique classique à deux points qui apparaît dans de nombreuses interviews (sous-chaînes palindromes, deux séries de 2 d).
3. **Manipulation des caisses** – la chaîne peut déjà être équilibrée, ou la fenêtre peut devoir rétrécir plusieurs fois. Une implémentation propre évite les bugs subtils.

Si vous pouvez expliquer ce problème en 5-10 minutes et écrire l'algorithme à la main en un seul coup, vous êtes déjà à mi-chemin du statut *top-tier candidate*.

---

4.2 Le **Bon** – Simple mais puissant

- **O(n) temps** – pas de boucles imbriquées, juste un balayage linéaire.
- **O(1) espace** – seulement 4 compteurs, même pour 100 000 chaînes de caractères.
- **Technique réutilisable** – le squelette de fenêtre coulissante peut être adapté pour *tout problème* qui demande un segment contigu avec une propriété donnée.

Vous pouvez le présenter dans votre portfolio ou sur un tableau blanc :

«» "
Nombre > requis -> excédent
La fenêtre contient tous les excès -> remplacer la fenêtre
«» "

C'est un grand exemple de **=réduire le problème==**: de =find a substring=== à =find a substring that contains all the excessive===.
Les recrues se demanderont : *=Pourquoi avons-nous soustrait `requis`?=== et vous pouvez dire immédiatement : *= Parce que nous n'avons besoin que de supprimer l'excédent, le reste de la chaîne reste intact.

---

### 4.3 La mauvaise** – Pièges communs

Comment l'éviter
C'est-à-dire
**Calcul des besoins incorrects** (soustraire quand vous devez ajouter)=Utilisez un tableau `need` dédié, et définissez seulement `freq[i] - req` si positif. Autres
**En supposant que la fenêtre doit croître avant de rétrécir**. Autres
**Missing the dready balanced case**.Un "si tout(freq[i] == req)" rapide sauve les cas de bord 0-time. Autres
Autres **L'utilisation d'une carte en Java/Python** (O(1) vs O(4)) : Préférez les tableaux (`int[4]`) pour la vitesse ; les cartes donnent une lisibilité mais un léger survol. Autres

Mettre en évidence ces écueils lors d'une entrevue montre que vous *savez comment déboguer* et que vous pouvez penser défensivement à des cas de bord – une compétence très prisée.

---

4.4 Les grands** – Pourquoi les gens luttent

1. **Replacer toute sous-chaîne** – Certains candidats pensent que vous devez supprimer tous les caractères excédentaires, ne réalisant pas que vous pouvez également *insérer* nouveaux dans le remplacement.
2. **Élargissement de la fenêtre trop optimiste** – Ils laissent le bon pointeur se déplacer jusqu'à la fin avant de rétrécir, provoquant "O(n2)" dans la pratique en raison de contrôles répétés.
3. ** Obsession de la complexité** – Essayer d'éviter les vérifications de deux pointeurs (all-non-positive) et plutôt d'utiliser une file d'attente prioritaire ou un arbre de segment – une *horrible suringénierie* d'une solution simple d'O(n).

Un candidat senior reconnaîtra que la solution *sur-engineered* est simplement **ugly**. Ils diront : « Pas besoin d'un tas ; juste un passage à deux points. (en milliers de dollars)

---

4.5 Feuille d'entrevue rapide

Étape du code
- C'est quoi ?
Autres Fréquences de comptage "pour ch en s: freq[ch] += Un seul passage, O(n). Autres
Autres Excess array=1 `need[ch] = max(0, freq[ch] - req)=1 Seulement supprimer ce dont vous avez réellement besoin. Autres
Élargir la fenêtre Les valeurs négatives signifient que la fenêtre a déjà assez de ce char. Autres
Autres Test de bien-être : « pendant que tous (v <= 0 pour v dans le besoin) » vérifier la peritération. Autres
Rétrécissement de la charge de travail 1; left++`= Déplacer à gauche seulement lorsque la fenêtre est bonne. Autres

Souvenez-vous : la longueur de la fenêtre **rejets** seulement lorsque *chaque* caractère surreprésenté est déjà satisfait.

---

4.6 Comment en parler dans une interview

1. **Énoncez le problème en anglais simple** – assurez-vous que l'intervieweur sait que vous comprenez l'opération de remplacement.
2. ** Expliquez l'observation** – Pourquoi nous soucions-nous de "freq[c] - req`?
→ Cela montre que la chaîne a déjà la bonne quantité de caractères *sous-représentés*.
3. **Fenêtre coulissante – dessinez un diagramme simple sur le tableau blanc.
*Le pointeur droit ajoute, le pointeur gauche supprime, rétrécit pendant que bon*.
4. **Edge-case check** – pointez la réponse `0` pour les chaînes déjà équilibrées.
5. **Complexité** – mention `O(n)` temps et mémoire constante, et commenter optionnellement pourquoi cela bat une recherche naïve `O(n2)` sous-chaîne.

Si vous terminez avec un code *clean, runable, vous aurez convaincu l'intervieweur que vous pouvez écrire **code correct, efficace, prêt à la production**.

---

4.7 Les derniers mots

Le problème *gateway* pour des sujets plus avancés (préfixes, cartes de fréquence, files d'attente monotone).

- **Bon** – Un exercice classique de fenêtre coulissante qui démontre une pensée linéaire.
- **Bad** – Souvent trébuché par ceux qui oublient de soustraire la quantité requise d'abord.
- **Ugly** – Les solutions sur-moteurs qui font exploser la mémoire ou le temps en ajoutant des structures de données inutiles.

Si vous avez ce problème, vous prouvez que vous pouvez voir des modèles, concevoir des algorithmes efficaces, et écrire un code propre – exactement ce que les recruteurs recherchent.

Bon codage et bonne chance avec votre prochaine interview! C'est ce qu'il a dit.

---

- Oui. 5. Comment utiliser cet article pour stimuler votre resume

- **Ajouter une section** intitulée "LeetCode Problème résolu" et lister ce problème avec un lien vers votre solution.
- **Utilisez les points à puce** de la section Pourquoi ce problème est important.
- **Partagez les extraits de code** dans votre GitHub README (p. ex. `BalancedString.java`) – les recruteurs épuisent souvent vos dépôts pour un code propre.

---

- Oui. 6. Liste de contrôle à emporter

- [ ] Comprendre l'astuce **excès-représentation**.
- [ ] Maîtrisez le modèle **gliding window**.
- [ ] Soyez capable d'écrire la solution dans **Java/Python/C++** en 5 min.
- [ ] Préparer une explication orale de 5 minutes qui couvre le *pourquoi* et le *comment*.
- [ ] Ajoutez l'implémentation à votre portfolio pour un examen rapide du recruteur.

Joyeux entretien !

---

- Oui. 7. Références

1. [LeetCode 1694 – Remplacer la sous-chaîne pour les chaînes équilibrées](https://leetcode.com/problèmes/remplace-the-substring-for-equilibred-string/)
2. *Two-Pointer (Fenêtre coulissante) Pattern*, manuel CS 101
3. *HackerRank – contre-coefficient fréquent*

---

- Oui. 8. SEO & Crochets de recherche d'emploi

- Mots-clés: `equilibred string`, `substring subsupplacement`, `LeetCode medium`, `sliding window interview`, `coding interview prep`, `job interview algorithmes`.
- Description de la méta: *Apprenez la solution O(n) la plus rapide à LeetCode 1694 – Remplacer la sous-chaîne pour la chaîne équilibrée par le code de référence en Java, Python et C++. Maîtrisez la technique de la fenêtre coulissante pour impressionner les recruteurs. *

---

** Fin de l'article. **