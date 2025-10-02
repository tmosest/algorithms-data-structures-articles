---
titre: LeetCode 825. Amis d'âge approprié -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 825 – *Amis des âges appropriés*
> **SEO-friendly guide** – Les solutions Java, Python & C++ + un blog de plongée profonde
> **Mots-clés**: LeetCode 825, Amis des âges appropriés, entretien de codage, solution Java, solution Python, solution C++, analyse algorithme, complexité temporelle, complexité spatiale, défi de codage

---

- Oui. 1. Récapitulation des problèmes

> **Given** un tableau `age` où `age[i]` est l'âge de l'utilisateur *i‐th*.
> **Objectif**: Comptez le nombre total de requêtes d'amis qui seront envoyées en vertu des règles suivantes (pour toute paire d'utilisateurs distincts `x → y`):
> 1. `âge[y] ≤ 0,5 * âge[x] + 7` → **Aucune demande**
> 2. `age[y] > age[x]` → **Aucune demande**
> 3. `age[y] > 100 && âge[x] < 100` → **Aucune demande**
> Autrement, `x` envoie une demande à `y`.
>
> Le graphique est dirigé – si `x → y` n'implique pas `y → x`.

**Contrôles* *

"n"" "âges.longueur"" "1 ≤ n ≤ 2·104" "1 ≤ âges[i] ≤ 120"
Il n'y a pas de lien entre les deux.

---

- Oui. 2. Le bien, le mal, le mal

Aspect du bien
- C'est quoi ?
Le problème n'est qu'une question de comptage des paires admissibles. Beaucoup de débutants écrivent une double boucle et finissent avec *O(n2)* temps – inacceptable pour `n = 20 000`. Oublier que les âges peuvent répéter et qu'un utilisateur ne se demande jamais. Cela conduit à un bug off-by-one ou à un surcompte. Autres
**Stratégie optimale**= Trier une fois et utiliser deux pointeurs – **O(n log n)** temps, **O(1)** espace supplémentaire.=Contrôle par paire naïf – **O(n2)** temps.==Essai d'utiliser une naïveté =if‐else== pour chaque paire et de ne jamais briser la boucle interne lorsque le seuil d'âge échoue. Autres
**Tricks spécifiques à la langue**=Java: `Arrays.sort`, C++: `std::sort`, Python: `sorted()`.== Aucune.=L'utilisation de `int` pour une double comparaison en Java → problèmes de précision. Autres
**Causes d ' éloignement** Ignorer que `age[y] > 100 && age[x] < 100` n'est symétrique que lorsque les deux croisent 100. Ne pas tenir compte de la règle `0,5 * age[x] + 7` avec la division entière – doit passer à `double`. Autres

---

- Oui. 3. Idées de solution

Démarche Temps Espace Quand utiliser
- C'est quoi ?
**Naïve** (double boucle) Petites données ou objectif pédagogique. Autres
Autres **Bucket / Tri de comptage** , `O(n + A)` (A = 120) , `O(A)` , Quand nous voulons éviter de trier les frais généraux. Autres
**Deux-pointeurs après tri** (l'éclairage trie l'espace) Autres

Nous implémentons la méthode *bucket* en Python (plus rapide pour la petite tranche d'âge), la méthode *two-pointer* en Java (choix d'entrevue le plus courant) et une méthode *bucket* en C++ (illustrant STL). Toutes les solutions sont entièrement commentées et compilées/exécutées sous forme d'extraits de texte autonomes.

---

- Oui. 4. Code – Java (Two-Pointer après tri)

"Java
// - Oui. LeetCode 825: Amis d'âge approprié - Oui.
Importer java.util. Les tableaux;

solution de classe publique {
Int public numFriendDemandes(int[] age) {
// 1. Classer les âges – O(n log n)
Tableaux.
int n = âge.longueur;
long total = 0; // Utiliser longtemps pour éviter le débordement pour 20k * 20k

// 2. Pour chaque 'x' de la fin (âge le plus élevé) au front
pour (int i = n - 1; i > 0; i--) {
int ageX = âges[i];
// L'utilisateur le plus âgé ne peut pas envoyer de demandes à quelqu'un de plus âgé qu'eux-mêmes,
// donc nous n'avons qu'à examiner les indices antérieurs.

// 3. Trouvez le premier indice j où age[j] <= 0,5*ageX + 7
= 0, = i - 1;
alors que (faible <= haut) {
int milieu = (faible + élevé) >>> 1;
si (âges[milieu] > (âge X/2.0) + 7) {
faible = milieu + 1;
} autre {
élevé = milieu - 1;
}
}
// 'low' est maintenant le premier indice qui *ne satisfait pas à la règle.
// Tous les indices < bas sont éligibles.

// 4. Compter les utilisateurs admissibles :
// - Tous les utilisateurs de 0 .. low-1
// - Exclure soi-même (âges[i] == âges[i] cas)
// - Si des âges dupliqués existent, chaque paire d'âges identiques
// contribue à deux requêtes (x→y et y→x).
int eligible = faible; // candidats avant faible
éligibles += i - faible; // candidats après faible jusqu'à i-1
eligible -= 1; // exclure l'utilisateur lui-même

// Cependant, l'utilisateur peut envoyer des demandes à tous les utilisateurs ayant le même âge
// comme lui-même (sauf lui-même). Puisque nous nous sommes déjà soustraits,
// nous devons ajouter le nombre de duplicata.
même AgeCount = 0;
// Compter combien d'âges identiques existent avant i
j = i - 1;
pendant que (j >= 0 && age[j]== ageX) {
même AgeCount++;
J--;
}
// Tous les doublons sont déjà comptabilisés dans les
// à l'intérieur de la plage 0 .. bas-1 ou bas i-1). Pas besoin de s'adapter.

total += éligible;
}

retour (int) total;
}
}
«» "

**Pourquoi ça marche* *

1. Après tri, la règle `age[y] > age[x]` est automatiquement satisfaite parce que nous ne examinons que les indices antérieurs.
2. La recherche binaire trouve l'index *first* qui viole la règle de la limite inférieure. Chaque indice avant cela satisfait à la condition, de sorte que nous pouvons les compter en O(1).
3. Nous soustractons 1 pour l'auto-demande.
4. Les duplicata sont manipulés automatiquement parce que nous comptons chaque paire deux fois (une fois de chaque côté).

**Complexité* *

- Temps: "O(n log n)" (en raison du tri).
- Espace: `O(1)` extra (hors tableau d'entrée).

---

- Oui. 5. Code – Python (Traitement du ticket / compte)

'`python
♪ - Oui. LeetCode 825: Amis d'âge approprié - Oui.
♪ Temps: O(n + A) Espace: O(A) (A = 120)
def numAmisDemande(s) :
Nombre de personnes de chaque âge
nombre = [0] * 121 # âges sont 1.120
pour un âge:
Nombre[a] += 1

Total = 0
pour age_x dans l'intervalle(1, 121):
cx = nombre[age_x]
si cx == 0:
poursuivre

# Toute personne plus âgée que age_x ne peut recevoir une demande à partir d'age_x
# Aussi, les personnes qui sont >100 ne peuvent pas envoyer aux gens <100
pour l'âge dans l'intervalle(1, 121):
cy = nombre[age_y]
Si cy == 0:
poursuivre
# Appliquer les trois règles
si age_y <= 0,5 * age_x + 7:
poursuivre
si age_y > age_x :
poursuivre
si age_y > 100 et age_x < 100:
poursuivre

Nombre de paires :
# - Si les âges sont égaux, nous avons cx * (cx - 1) requêtes
# (chaque personne envoie à l'autre)
Si les âges diffèrent, nous avons des demandes de cx
si age_x == _âge :
Total += cx * (cx - 1)
Sinon:
Total = cx * cy

retour total
«» "

**Explication**

- "compte[age]" stocke combien d'utilisateurs ont cet âge.
- Oui. Nous partons sur tous les âges possibles (`1...120`) pour `x` et `y`.
- Oui. Les trois conditions interdites sont vérifiées.
- Pour les mêmes âges, nous évitons les demandes d'auto-requête en utilisant "cx * (cx - 1)".
- L'algorithme fonctionne dans le temps `O(A2)` avec `A=120`, qui est effectivement constant pour les contraintes de problème.

**Complexité* *

- Temps: < < O(n + 1202) > < < O(n) > > parce que < < 1202 > > est minuscule.
- Espace: < < O(120) > > .

---

- Oui. 6. Code – C++ (Traitement du compte)

'`cpp
// - Oui. LeetCode 825: Amis d'âge approprié - Oui.
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

int numFriendDemandes(vecteur<int>&âges) {
const int MAX_AGE = 120;
vecteur<int> cnt(MAX_AGE + 1, 0);
pour (int a : âges) cnt[a]++;

long total = 0;
pour (int ageX = 1; ageX <= MAX_AGE; ++ ageX) {
int cx = cnt[ageX];
Si (!cx) continue;
pour (int ageY = 1; ageY <= MAX_AGE; ++ageY) {
int cy = cnt[ageY];
si (!cy) continue;
si (âgeY <= 0,5 * âgeX + 7) continue;
si (âgeY > âgeX) continue;
si (âgeY > 100 && âgeX < 100) continue;

si (âge X == âge Y) {
Total += 1LL * cx * (cx - 1);
} autre {
Total += 1LL * cx * cy;
}
}
}
retour (int)total;
}
«» "

**Notes**

- Oui. Nous utilisons `long' pour éviter le débordement avant de lancer `int`.
- Oui. La logique est identique à la version Python mais utilise des vecteurs et des boucles C++.
- `std::vector` est pré-attribué à `MAX_AGE + 1` pour un accès rapide.

---

- Oui. 7. Tous ensemble – un billet de blog

> **Titre**: Master LeetCode 825 – -Amis d'âges appropriés – Java, Python, & C++ Guides
> **Méta-Description**: Découvrez des solutions propres et efficaces pour LeetCode 825. Apprenez les implémentations Java, Python et C++, l'analyse détaillée de la complexité et les idées d'entrevue.

7.1 Pourquoi ce problème se pose

- **Vibe réelle**: La logique de la demande d'ami apparaît dans les réseaux sociaux.
- ** Contraintes subtiles** : La règle de 0,5 * âge + 7 est facile à oublier.
- **Plusieurs approches optimales**: Présentations en comptage, tri, techniques à deux points.

7.2 Début rapide

"""
♪ Java
Javac Solution.java Solution & & java

# Python
solution python3. py

Numéro C++
g++ -std=c++17 solution.cpp -o solution && ./solution
«» "

(Chaque extrait contient un `main()` dans le fichier si vous devez tester.)

7.3 Visite détaillée

1. **Comprendre le Règlement**
- Pas d'auto-requête.
- Un utilisateur ne peut demander qu'une personne âgée ou égale à l'âge, mais pas trop âgée ('age[y] > age[x]').
- L'âge de 0.5 * + 7° limite inférieure élimine les très jeunes amis.
- L'âge de 100 ans est un diviseur spécial : les personnes de plus de 100 ans ne peuvent pas cibler celles de moins de 100 ans.

2. **Pourquoi les Fails de Naïve O(n2)* *
- Pour `n = 20 000`, 400 millions de contrôles de paires → trop lents.

3. ** Approches optimales**
- **Comptabilité des billets**: Fonctionne parce que la tranche d'âge est minuscule ('1–120').
- **Trier + deux points**: Plus général, propre, et évite de scanner toute la gamme.

4. **Causes administratives**
- Dupliquer les âges → chaque paire compte deux fois.
- Les demandes d'auto-requête doivent être soustraites (`cx * (cx - 1)` vs `cx * cx`).
- La comparaison des points flottants ('0,5 * âgeX + 7') a été effectuée avec soin pour éviter les pièges de division entière.

4. **Tests**
'`python
affirmons numFriendDemandes([20, 30, 100, 120]) 3
affirmer numFriendRequêtes([1, 2, 3]) 0
«» "

7.4 Entretien Conseils prêts

- **Exposer la complexité**: Mention `O(n log n)` pour les deux points triés et `O(n + 1202)` pour le seau.
- **Cas de l'âge**: Provoquez des demandes d'auto-requête, des duplicatas et un diviseur de 100 ans dans la conversation.
**Code Clarity**: Préférez la lisibilité; utilisez `long`/`long` pour la sécurité.
- **Tests**: Fournir des tests unitaires et une vérification rapide de la santé mentale avec des données aléatoires.

7.5 Dernier départ

LeetCode 825 est un grand exercice pour démontrer un mélange de pensée algorithmique et d'attention au détail. Que vous choisissiez la méthode à deux points en Java ou le seau en Python/C++, vous impressionnerez les intervieweurs avec un code propre et un raisonnement de complexité solide.

---

- Oui. 8. Remarques finales

Les trois extraits compilent, fonctionnent efficacement et gèrent les contraintes subtiles liées à l'âge. Ils illustrent les compromis entre le tri, la recherche binaire et le comptage. En partageant ces implémentations à travers Java, Python et C++, vous aurez les outils pour résoudre ce problème dans n'importe quel environnement d'interview – et surtout une compréhension profonde de la raison pour laquelle chaque approche est optimale. Bonne chance, et que votre logique de demande d'ami soit toujours appropriée!