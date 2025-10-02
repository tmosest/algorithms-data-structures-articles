---
titre: LeetCode 1618. Police maximale pour mettre une peine dans un écran -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Résoudre la police maximale pour mettre une phrase dans un écran

Langue Autres
Il s'agit d'un projet pilote.
*Java * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres
*Python *Python *Python Autres
*C++**=O (=texte = log=fonts=)===O(1)= Autres

L'idée clé est une recherche binaire sur la taille de la police**.
Comme le tableau des polices est trié et que la largeur/hauteur augmente monotoniquement avec la taille de la police, chaque police plus grande qu'une police viable sera également invalide, et chaque police plus petite sera valide (ou du moins pas plus restrictive).

---

- Oui. 2. Mise en œuvre des références

> **NOTE** – Les trois extraits supposent qu'une classe `FontInfo` (ou une interface en Java) est fournie par l'exécution LeetCode et que vous n'avez qu'à implémenter la fonction `maxFont`/`max_font`/`maxFont`.

### 2.1 Java

"Java
***
* Définition pour FontInfo.
* interface publique FontInfo {
* int getWidth(int police Taille, char ch);
* int getHeight(int fontSize);
*}
*/
solution de classe publique {
public int max Police(String text, int w, int h, int[] fonts, FontInfo fontInfo) {
int gauche = 0, droite = polices.longueur - 1;
int best = -1;

pendant que (gauche <= droite) {
int milieu = gauche + (droite - gauche) / 2;
taille int = polices[mid];

si (peutFit(texte, taille, w, h, fontInfo)) {
meilleur = taille; // un nouveau candidat
gauche = milieu + 1; // essayer une taille plus grande
} autre {
droite = milieu - 1; // rétrécir à plus petites tailles
}
}
le meilleur retour;
}

*** Helper: true if la ligne entière correspond à l'écran */
boîte privée booléenneFit(String text, int size, int w, int h, FontInfo fontInfo) {
si (fontInfo.getHeight(size) > h) retourne false;

= 0;
pour (int i = 0; i < text.length(); i++) {
total += fontInfo.getWidth(size, text.charAt(i));
si (total > w) retourner faux; // sortie anticipée
}
retour vrai;
}
}
«» "

2.2 Python

'`python
# @param text : chaîne
# @param w : Int
# @param h : Int
Polices @param : Liste[int]
Police @param Info : FontInfo
# @retour Int
Solution de classe:
def max_font(self, texte: str, w: int, h: int,
polices : List[int], police Informations: 'FontInfo') -> Int:
lo, hi = 0, len(fonts) - 1
meilleure = -1

alors que lo <= bonjour:
milieu = (lo + hi) // 2
taille = polices[mid]
if self._fits(text, size, w, h, fontInfo):
meilleure = taille
lo = milieu + 1 # essayer plus grand
Sinon:
hi = milieu - 1 # rétrécissement

le meilleur retour

def _fits(self, texte: str, taille: int,
w: int, h: int, police Informations: 'FontInfo') -> C'est vrai.
si fontInfo.getHeight(size) > h:
Retour Faux

largeur = 0
pour ch dans le texte:
largeur += fontInfo.getWidth(size, ch)
si largeur > w:
Retour Faux
retour Vrai
«» "

> **Conseil de python** – La sortie anticipée à l'intérieur de la boucle (`si la largeur > w: retourner False`) permet d'économiser ~50% pour les grandes entrées.

C++

'`cpp
classe FontInfo {
public:
int virtuel getWidth(int police Taille, ch) = 0;
int virtuel getHeight(int fontSize) = 0;
};

solution de classe {
public:
Int max Police(string text, int w, int h, vector<int>& fonts, FontInfo* fontInfo) {
int l = 0, r = polices.size() - 1;
int best = -1;

pendant que (l <= r) {
int milieu = l + (r - l) / 2;
taille int = polices[mid];
si (s'adapte(texte, taille, w, h, fontInfo)) {
meilleure = taille;
l = milieu + 1;
} autre {
r = milieu - 1; // recherche plus petite
}
}
le meilleur retour;
}

particulier:
bool fits(const string& text, int size, int w, int h, FontInfo* fontInfo) {
si (fontInfo->getHeight(size) > h) retourne false;

largeur int = 0;
pour (charte ch : texte) {
width += fontInfo->getWidth(size, ch);
si (largeur > w) retourner faux; // sortie anticipée
}
retour vrai;
}
};
«» "

> **C++ Astuce** – Passer `FontInfo*` par pointeur maintient l'exécution inchangée parce que les méthodes sont `virtual` O(1).

---

- Oui. 3. Billet de blog: Le bon, le mauvais, et le lamentable de trouver la plus grande police

> *Référencement Tags: interview algorithme, recherche binaire, LeetCode 1618, entretien d'emploi, Java, Python, C++ *

---

3.1 Récapitulation du problème

On vous donne une phrase simple, une largeur d'écran ('w') et une hauteur (`h`), un tableau trié des tailles de police disponibles, et une API qui retourne la largeur de chaque caractère et la hauteur commune pour une taille de police donnée.
**Objectif:** choisir la taille de police *la plus grande* qui laisse encore la phrase entière s'adapter.

Les contraintes sont serrées – la phrase peut être longue de 50 000 caractères, et le tableau des polices peut contenir jusqu'à 100 000 entrées. Une approche naïve O(="fonts=" ·="text=") serait trop lente.

---

3.2 Le bon – une solution propre et optimale

1. **Monotonicité** – La principale observation est que la largeur et la hauteur ne diminuent jamais avec la taille de la police.
*Si une certaine taille de police s'adapte, chaque taille plus petite s'adaptera également. *

2. **Binary Search** – Avec la monotonicité, la réponse est un point sur une liste triée.
* La recherche binaire coupe l'espace de recherche dans la moitié de chaque étape, donnant des itérations `log="fonts=". *

3. **O(=text=)** travail par itération – Le calcul de la largeur pour une taille candidate est un seul balayage linéaire sur la chaîne (O(1) appelle à l'API par caractère).
*Début de sortie lorsque la largeur cumulée dépasse déjà "w" économise beaucoup de temps. *

4. **Complexité globale** –
Temps "O(=text=" · log="fonts="), espace auxiliaire "="O(1)".
Cela permet de gérer confortablement les contraintes maximales (soit 50 000 × 17 850 000 opérations).

---

3.3 Les mauvaises – Ce qui peut mal tourner

Pourquoi ça compte ?
- Oui.
**Scan complet sur chaque itération**=Pour une liste de 100 000 caractères, 17 scans complets de 50 000 caractères peuvent encore être lourds. Autres Ajouter une pause précoce lorsque la largeur > `w`. Autres
**La largeur peut atteindre `10^7` par caractère, de sorte que la largeur totale peut dépasser `int`s 2 147 483 647. Autres
**Commande de comparaison de Wong**.Si vous ne vérifiez que la hauteur avant la largeur, vous pouvez à tort rejeter une police possible parce que la vérification de la largeur n'a jamais été effectuée. Effectuez les deux vérifications; la commande n'a pas d'importance tant que vous retournez *faux* si l'un ou l'autre échoue. Autres
**En supposant que les polices sont uniques**=La taille des duplicata briserait la recherche binaire si vous utilisez par erreur la logique `lower_bound`/`upper_bound` qui attend des clés uniques. Le problème garantit l'unicité, mais toujours tester sur des données aléatoires. Autres
**Ne pas manipuler une chaîne vide**= Certains harnais de test peuvent passer une chaîne vide; vous devez retourner la police la plus grande qui convient (c'est-à-dire la police maximale dont la hauteur ≤ `h`). Le cas spécial `text.isEmpty()` ou simplement laisser la boucle de largeur sauter. Autres

---

3.4 Les cas les plus odieux – les cas de bord et la mise en œuvre Triques

1. **Fents dépassant la hauteur de l'écran** –
Une police trop grande ne correspondra jamais, même si sa largeur est minuscule.
*Solution:* Vérifiez tôt `fontInfo.getHeight(size) > h` avant de scanner la chaîne.

2. **Toutes les polices trop petites** –
Si chaque police échoue au test de hauteur, la réponse doit être `-1`.
La recherche binaire donne naturellement `-1` quand aucun candidat ne satisfait aux deux contraintes.

3. **Très grands `w` et `h`** –
L'écran peut être énorme (jusqu'à `10^7' largeur). Les largeurs de grossissement peuvent rester dans les 64 bits, mais ne pas compter sur la sécurité 32 bits.

4. **AIP Overhead** –
Le problème indique que les appels API sont O(1). Dans les paramètres d'entrevue réels, vous pourriez être tenté de pré-calculer toutes les largeurs/hauteurs une fois (O(=fonts== ·=alphabet=)), mais cela peut souffler la mémoire. S'en tenir aux appels à la volée, à moins que l'entrevue ne demande explicitement la mise en cache.

5. ** Taille du jeu de caractères** –
La chaîne ne contient que des lettres anglaises minuscules, vous pouvez donc pré-stocker les valeurs de 26 largeurs pour chaque taille de police. Cela réduirait les appels de l'API de `=text=" à 26 par candidat, mais augmente la mémoire à `=26="fonts=". D'habitude, ça n'en vaut pas la peine.

---

### 3.5 Code de l'échantillon

Laissez passer la solution Java :

"Java
pendant que (gauche <= droite) {
int milieu = gauche + (droite - gauche) / 2;
taille int = polices[mid];

si (peutFit(texte, taille, w, h, fontInfo)) {
meilleur = taille; // un nouveau candidat
gauche = milieu + 1; // essayer plus grand
} autre {
droite = milieu - 1; // rétrécir à plus petites tailles
}
}
«» "

* ** 'canFit '** vérifie la hauteur et la largeur cumulée.
* **Early exit** inside `canFit` (`si (total > w) retourner false;`) économise beaucoup de temps lorsqu'une police est clairement trop large.
* La logique de recherche binaire est classique : si la taille moyenne est réalisable, regardez à droite ; sinon, regardez à gauche.

---

### 3.6 Tendance des entrevues

Question de l'intervieweur Comment répondre
- C'est quoi ?
Autres Comment résoudre ça ? Reconnaître la monotonicité → la recherche binaire
Autres Quelle est la complexité?
Autres *=Pouvez-vous gérer de grandes entrées?== *= Utiliser 64 bits, sortie anticipée== Afficher votre code a `long total` et début de pause==
Autres Et si la chaîne est vide ? La hauteur n'a qu'une importance.

---

3.7 Conclusion

*Le problème est un exemple de manuel d'application de la recherche binaire sur une liste triée avec un prédicat de faisabilité monotonique. *

- **Bien:** Temps linéaire par candidat, échelle logarithmique globale.
- **Bad:** Attention au débordement et aux scans.
- **Ugly:** La hauteur de la poignée d'abord, départ précoce sur la largeur, et se rappeler le problème garanties.

Avec une explication solide et un code propre dans l'une des trois langues principales, vous allez non seulement clouer cette question LeetCode mais aussi démontrer la pensée algorithmique que les intervieweurs aiment. Bon codage, et bonne chance pour votre prochain entretien! *

---

*Sentez-vous libre de laisser un commentaire si vous souhaitez discuter de modèles d'entrevue plus algorithmiques. *

---

> **Note:** Si vous préparez une entrevue de codage, collez le code échantillon dans votre éditeur, exécutez-le contre les tests officiels, et pratiquez expliquer chaque étape à haute voix.

---

Bonne interview !

---

*Fin du blog. *

---

C'est cela – vous avez maintenant le code, les idées de base et un article prêt à poster qui peut doubler comme une entrée de portefeuille pour vos demandes d'emploi. Bon codage !