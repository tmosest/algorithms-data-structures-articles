---
titre: LeetCode 2468. Message de partage basé sur la limite -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2468. Message de partage basé sur la limite
*Hard – LeetCode*

---

- Oui. 1. Récapitulation des problèmes

Autres Quoi ?
- Oui.
**Input**="message" – une chaîne de lettres minuscules et d'espaces. <br>`limite` – un entier positif. Autres
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * <br>• Lorsque les suffixes sont enlevés et que les pièces sont concaténées, le `message` original est récupéré. Autres
**Output**= Array des cordes – les parties fractionnées. Retourner un tableau vide si impossible. Autres

> **Exemple**
> `message = "message court"`, `limite = 15` →
> `["salon court<1/2>", "âge<2/2>"] "

---

- Oui. 2. Stratégie de haut niveau

1. **Pourquoi la recherche binaire? **
* Le nombre de parties `b` est compris entre 1 et `message.longueur`.
* Pour chaque candidat `b` nous pouvons *déterminer* si une scission valide est possible en temps linéaire.
* En utilisant la recherche binaire, nous trouvons le minimum possible `b` dans les étapes `O(log n)`.

2. ** Essai de faisabilité pour un "b" fixe**
* Pour la partie `i` (`1 ≤ i ≤ b`), la longueur suffisante est
Texte
suffixeLen(i) = 3 + chiffres(i) + chiffres(b)
«» "
(`"<"`, `"/"`, `">"` + chiffres des indices).
* La quantité maximale de *contenu* qui peut s'inscrire dans la partie "i" est
Texte
capacité(i) = limite - suffixeLen(i)
«» "
* Si une `capacité(i) < 0` → impossible.
* Si la somme de toutes les capacités est au moins `message.longueur` → possible.

3. **Reconstruire les pièces* *
* Après la recherche binaire donne le minimum `b`, itérer `i = 1 ... b'
* Pour les premières parties «b‐1», utiliser la pleine capacité («limite – suffixeLen»).
* La dernière partie prend les caractères *restant* (= sa capacité).
* Construisez la chaîne `content + "<i/b>"` pour chaque partie.

4. **Complexité**
* **Time** – `O(n log n)` où `n = message.length`.
* **Espace** – `O(n)` pour stocker la sortie.

---

- Oui. 3. Code de préparation de référence

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

> *Toutes les solutions utilisent la même idée algorithmique. *

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public Chaîne[] splitedMessage(Message de la chaîne, limite int) {
int n = message.longueur();
int lo = 1, hi = n, best = -1;

// Recherche binaire pour un nombre minimal de pièces
pendant que (lo <= bonjour) {
Int milieu = lo + (h - lo) / 2;
si (canSplit(message, limite, milieu)) {
meilleur = milieu;
hé = milieu - 1;
} autre {
lo = milieu + 1;
}
}

si (meilleur == -1) retourner une nouvelle chaîne[0];
retour buildParts(message, limite, meilleur);
}

boîte de booléen privéeSplit(String s, limite int, parties int) {
long total Culot = 0;
int lenB = numDigits(parties);

pour (int i = 1; i <= parties; i++) {
Int cap = limite - (3 + numDigits(i) + lenB); // 3 = "<>/"
si (cap < 0) retourner faux;
Total général Culot += culot;
}
retourner totalCap >= s.longueur();
}

Chaîne privée[] buildParts(String s, int limit, int parts) {
int n = s.longueur();
Int idx = 0;
Chaîne[] res = nouvelle chaîne[parties];
int lenB = numDigits(parties);

pour (int i = 1; i <= parties; i++) {
culot int = limite - (3 + numDigits(i) + lenB);
int take = (i == parties) ? n - idx : chapeau; // la dernière partie peut être plus courte
Contenu des chaînes = s.substring(idx, idx + take);
idx += prise;
res[i - 1] = contenu + "<" + i + "/" + parties + ">;
}
retour rés;
}

Int privé numDigits(int x) {
retour Chaîne.valueOf(x).longueur();
}
}
«» "

3.2 Python

'`python
Solution de classe:
def splitMessage(self, message: str, limit: int) -> list[str]:
n = len(message)
lo, salut, meilleur = 1, n, -1

alors que lo <= bonjour:
milieu = (lo + hi) // 2
si self._can_split(message, limite, milieu) :
meilleure = moyenne
Bonjour = milieu - 1
Sinon:
lo = milieu + 1

Si c'est le mieux == -1:
retour []

return self._build_parts(message, limite, meilleur)

def _can_split(self, s: str, limit: int, parties: int) -> C'est vrai.
_cap total = 0
len_b = len(str(parts))
pour i dans la gamme(1, parties + 1):
maximum = limite - (3 + len(str(i)) + len_b) # 3 = "<>/"
si culot < 0:
Retour Faux
_cap total += cap
retourner total_cap >= len(s)

def _build_parts(self, s: str, limit: int, parts: int) -> list[str]:
n = len(s)
idx = 0
res = []
len_b = len(str(parts))

pour i dans la gamme(1, parties + 1):
culot = limite - (3 + len(str(i)) + len_b)
prendre = n - idx si i == parties d'autre bouchon
res.append(s[idx:idx + take] + f"<{i}/{parts}>")
idx += prise

retour res
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<string> splitMessage(message de chaîne, limite int) {
int n = message.size();
int lo = 1, hi = n, best = -1;

pendant que (lo <= bonjour) {
Int milieu = lo + (h - lo) / 2;
si (canSplit(message, limite, milieu)) {
meilleur = milieu;
hé = milieu - 1;
} autre {
lo = milieu + 1;
}
}
Si (meilleur) -1) retour {};

retour buildParts(message, limite, meilleur);
}

particulier:
bool canSplit(chaîne de caractères Const & s, limite int, parties int) {
long total long Culot = 0;
int lenB = to_string(parts).size();

pour (int i = 1; i <= parties; ++i) {
int cap = limite - (3 + to_string(i).size() + lenB); // "<>/"
si (cap < 0) retourner faux;
Total général Culot += culot;
}
retourner totalCap >= (long)s.size();
}

vector<string> buildParts(cont string& s, int limit, int parts) {
vecteur <string> rés;
int n = s.size(), idx = 0;
int lenB = to_string(parts).size();

pour (int i = 1; i <= parties; ++i) {
culot int = limite - (3 + to_string(i).size() + lenB);
int take = (i == parties) ? n - idx : chapeau; // la dernière partie peut être plus courte
contenu de chaîne = s.substr(idx, prendre);
idx += prise;
res.push_back(content + "<" + to_string(i) + "/" + to_string(parts) + ">");
}
retour rés;
}
};
«» "

> Les trois extraits compilent les dernières normes linguistiques et passent les exemples fournis.

---

- Oui. 4. Plongée profonde de style Blog
> Message partagé sur la base de la limite – le bon, le mauvais, et le mauvais * *

---

4.1 Les bonnes – Pourquoi Ce problème est une masterclass dans l'optimisation

Qu'est-ce qui le rend génial Comment ça vous aide
-- -- -- -- -- -- -- --
**Une contrainte claire sur la longueur de la partie** – vous force à penser à *suffix au-dessus* plutôt qu'au simple message lui-même. Il vous apprend à équilibrer deux facteurs concurrents (contenu + métadonnées). Autres
**Recherche binaire + faisabilité linéaire** – le modèle *canonique* pour le nombre minimal de questions de groupes. Renforce un modèle algorithmique qui réapparaît dans de nombreux problèmes d'entrevue (p. ex., tableau de partage le plus grand montant, minimum le plus grand montant). Autres
**L'échange entre l'espace et le temps est minimal** – vous ne stockez que la réponse, et non aucun énorme tableau intermédiaire. Encourage le codage propre et respectueux de la mémoire. Autres
Autres **L'utilisation élégante du nombre entier de chiffres** – un tour subtil qui transforme le problème de dur à dur dans *polynomial*. C'est une illustration du monde réel de la raison pour laquelle un simple "log10" est important. Autres

---

4.2 Les mauvaises – Pièges communs

Pourquoi ça arrive ?
- Oui.
**Sur-compter la longueur du suffixe** – oubliant que chaque index contribue `digits(i)`= De nombreuses solutions naïves traitent le suffixe comme une constante `<1/1>`. Autres
**En supposant que chaque partie doit être pleine** – négliger la dernière partie peut être plus courte. Dans l'étape de reconstruction, *seulement* la dernière partie peut avoir moins de caractères. Autres
**Utiliser `int` pour les sommes de capacité** – débordement lorsque `n` est grande peut s'élever à > 231 à 1. Autres
**O(n2) cupidité** – coupe à plusieurs reprises jusqu'à impossible. La recherche binaire réduit le facteur de log n.
**Manipulation des numéros à 0 chiffres** retourne incorrectement Définition de « chiffres(0) = 1 » (ou toujours utiliser « String.valueOf(n).length() »). Autres

---

#### 4.3 Les cas de bord qui feront tourner votre tête

Pourquoi ça a l'air bizarre Comment le manipuler
-- -- -- -- -- -- -- -- --
Autres **Message de longueur 1, limite = 1**= Vous devez toujours ajouter un suffixe `<1/1>` → longueur de la partie 5 > 1 → impossible. Notre test de faisabilité capture immédiatement `capacité < 0`. Autres
Autres **Très grande "limite" (p. ex. 109)**La longueur suffixe devient négligeable, mais consomme encore 3 + chiffres. L'algorithme fonctionne indépendamment – la "capacité" peut être énorme, mais nous ne nous soucions que de la somme par rapport à la longueur du message. Autres
**Le message contient de nombreux espaces**Le contenu peut contenir des espaces de guidage, mais ils sont traités comme tout autre caractère. `substring` / `substr` les inclut automatiquement. Autres
** La limite est plus petite que tout suffixe possible** 2` → même `<1/1>` est 4 caractères. Le test de faisabilité le rejette tôt. Autres
** `b` est très grand (proche de `n`)**= Le calcul `digets(i)` pour chaque `i` pourrait sembler coûteux. Le comptage des chiffres par `String.valueOf(i).length()` (ou `to_string`) est O(1) par appel, de sorte que le test global reste O(n). Autres

> **Key Takeaway:** La seule partie vraiment *ugly* est la nécessité de garder une trace de la longueur de suffixe changeante pour chaque partie. Une fois que vous codifiez la formule `suffixLen(i) = 3 + chiffres(i) + chiffres(b)`, le reste tombe en place.

---

- Oui. 5. SEO–Friendly Wrap‐Up

- **Titre Tags** – Message partagé basé sur la limite – Java/Python/C++ Solutions
- **Meta Description** – solution LeetCode 2468, message fractionné avec des parties minimales, recherche binaire, test de capacité, implémentations Java/Python/C++. (en milliers de dollars)
- **Mots-clés en tête** – `split message`, `LeetCode 2468`, `algorithme`, `recherche binaire`, `suffix`, `programmation dynamique`, `codage interview`.

> En structurant l'article avec des rubriques H1–H3, des listes de puces et des blocs de code, nous garantissons une grande lisibilité pour les humains et les moteurs de recherche.

---

## 5.1 Rapide Référence: appelez-le

"Java
// Java
Solution sol = nouvelle solution();
String[] result = sol.splitMessage("short message", 15);
// résultat == ["brouillard court<1/2>", "âge<2/2>"]
«» "

'`python
# Python
sol = Solution()
print(sol.splitMessage("short message", 15))
# ["petit désordre<1/2>", "âge<2/2>"]
«» "

'`cpp
// C++
Solution sol;
auto res = sol.splitMessage("short message", 15);
// res == ["short mess<1/2>", "age<2/2>"]
«» "

---

## 5.2 Dernier départ

*Le problème de "Split Message Based on Limit" est une illustration parfaite de la façon dont une propriété **globale** (parties fewest) peut être réduite à un test de faisabilité **local** (capacités) et résolue efficacement par une recherche binaire.
La clé est de ne jamais sous-estimer le rôle du suffixe – c'est le coût caché qui transforme une scission apparemment simple en un problème d'optimisation non triviale. *

Bon codage – et bonne chance de casser cette prochaine question d'entrevue!