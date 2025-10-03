---
titre: LeetCode 158. Lire N caractères Donné lu4 II - Appelez plusieurs fois -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 158 – Lire N caractères Donné Read4 II (Appeler plusieurs fois)
### Les bons, les mauvais et les méchants – maîtriser un problème d'entrevue difficile

> **Meta‐Description** – Vous voulez obtenir cet entretien technique?
> Apprenez à cracher le LeetCode 158 avec des solutions Java, Python et C++ claires, une analyse approfondie des pièges, et l'astuce "buffer" qui facilite ce problème difficile.

---

- Oui. 1. Récapitulation des problèmes

Détails
C'est quoi ?
**Titre** Donné Read4 II – Appelez plusieurs fois
Difficulté
Source
**Constraints**
**But**= Implémenter `read(char[] buf, int n)` qui lit *up to* `n` caractères d`un fichier, mais vous ne pouvez lire le fichier que par le biais de `read4(char[] buf4)` API. La fonction `read` peut être appelée plusieurs fois. Autres

L'API `read4` conserve un pointeur de fichiers en interne, tout comme `FILE *fp` en C. Il lit au plus quatre caractères, les écrit dans `buf4`, et renvoie le nombre de caractères effectivement lus.

La partie dure : **`read` peut être appelée à plusieurs reprises** – vous devez garder les caractères non lus entre les appels.

---

- Oui. 2. Approche naïve et pourquoi elle échoue

"Java
public int read(char[] buf, int n) {
char[] temp = nouveau char[4];
Int read = 0;
pendant la période (lire < n) {
int cnt = lecture4(temp);
Si (cnt) 0) pause; // EOF
au lieu de (int i = 0; i < cnt && lire < n; i++) {
buf[read++] = temp[i];
}
}
retour lu;
}
«» "

*Travaille sur le premier appel*, mais sur les appels suivants vous **perdu tous les caractères qui ont été lus au-delà `n`**.
Si la mention `lecture(4)` lit 4 chars et vous n'avez besoin que de 2, les 2 restants sont rejetés – en violation de l'exigence de plusieurs appels.

---

- Oui. 3. Le Trick de Buffer – Le Bon

L'idée est de **stocker les caractères excédentaires** de `read4` dans un *petit tampon temporaire* qui persiste entre les appels. Pensez-y comme une fenêtre coulissante sur le fichier:

«» "
[Bouffé 4-char morceaux] ← buf4
^ ↑
C'est vrai.
bufPtr bufCnt
«» "

* `bufPtr` – index dans le morceau stocké (combien des 4 chars ont déjà été consommés).
* `bufCnt` – nombre de caractères valides actuellement stockés (= 4).

Algorithme (code pseudo):

«» "
Total général Lire = 0
alors que total Lire < n:
Si bufPtr == 0: // Besoin de données nouvelles
bufCnt = lecture4(buf4)
si c'est le cas. 0: pause // EOF

// Copier depuis le morceau stocké vers le buffer de l'appelant
alors que totalLire < n et bufPtr < bufCnt:
Total général Read++] = buf4[bufPtr++]

si bufPtr == bufCnt: // Fuite épuisée
bufPtr = 0
total de retourLire
«» "

Les points clés:

* ** État permanent**: `buf4`, `bufPtr`, `bufCnt` sont *variables d'intensité*, pas local à `read()`.
* **O(1) espace supplémentaire**: seulement 4 caractères sont stockés indépendamment de la taille du fichier.
* **O(n) temps**: chaque char demandé est traité une fois.

---

- Oui. 4. Code – Java, Python, C++

> **NOTE**: Sur LeetCode, la fonction `read4` est *déjà* définie; il suffit d'étendre `Reader4` (ou `Reader4` est une classe d'aide dans la plate-forme).
> Les trois extraits ci-dessous sont prêts à coller dans l'éditeur en ligne.

##### 4.1 Java

"Java
// Java 17
public class Solution étend Reader4 {

// tampon temporaire de taille 4 (le seul stockage dont nous avons besoin)
char[] buf4 = nouveau char[4];
Int privé bufPtr = 0; // Combien d'ombles dans le buf4 ont été consommés
Int privé bufCnt = 0; // Combien de caractères valides sont en buf4

@Override
public int read(char[] buf, int n) {
= 0;

alors que (total < n) {
// Si nous avons consommé tous les chars tamponnés, aller chercher un nouveau morceau
Si (bufPtr) 0) {
bufCnt = lecture4(buf4);
si (bufCnt) 0) pause; // Atteint EOF
}

// Copie du tampon vers la destination
alors que (total < n& bufPtr < bufCnt) {
buf[total++] = buf4[bufPtr++];
}

// Si nous avons lu le morceau entier, réinitialisez le pointeur
Si (bufPtr == bufCnt) {
bufPtr = 0;
}
}

le total des retours;
}
}
«» "

4.2 Python

'`python
# Python 3.10
solution de classe(Reader4):
def _init_(self):
Super().__init_()
auto.buf4 = [0] * 4
auto.ptr = 0
auto.cnt = 0

def read(self, buf: Liste[str], n: int) -> Int:
Total = 0
alors que total < n:
si self.ptr == 0:
self.cnt = self.read4(self.buf4) # read4 écrit en soi. buf4
si self.cnt == 0:
C'est pas vrai.

alors que total < n et auto.ptr < auto.cnt:
buf.append(self.buf4[self.ptr])
Total += 1
auto.ptr += 1

si self.ptr == self.cnt:
auto.ptr = 0

retour total
«» "

> LeetCodeS Python editor passe le `buf` comme une *list*, donc nous `ajoutons` dedans.

*### 4.3 C++

'`cpp
// C++17
class Solution : public Reader4 {
public:
la teneur en soufre de l'huile d'olive,
bufPtr = 0;
bufCnt = 0;

int read(char *buf, int n) surcharge {
= 0;

alors que (total < n) {
Si (bufPtr) 0) {
bufCnt = lecture4(buf4);
Si (bufCnt) 0) pause; // EOF
}

alors que (total < n& bufPtr < bufCnt) {
buf[total++] = buf4[bufPtr++];
}

si (bufPtr) bufPtr = 0;
}

le total des retours;
}
};
«» "

---

- Oui. 5. Liste de contrôle des cas de bord

Pourquoi c'est important Comment le truc du tampon le gère
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Le FEO a atteint le milieu de la lecture** Nous brisons quand `bufCnt == 0`. Autres
**`n` est 0**. L'état de boucle externe échoue immédiatement, renvoie 0.
**Plusieurs petits appels** (`lecture(1)` puis `lecture(1)`...) `bufPtr` garde l'état à travers les appels. Autres
**Large `n` > taille du fichier** La boucle s'arrête quand `bufCnt == 0`. Autres
Autres **Le code Leet crée un nouvel objet `Solution` par cas de test, donc les variables d'instance sont réinitialisées automatiquement. Aucune manipulation particulière n'est requise. Autres

---

- Oui. 6. Complexité

Valeur métrique
C'est pas vrai.
**Temps** **O(n)** – chaque caractère demandé est traité exactement une fois. Autres
**Extra Space** **O(1)** – seulement 4 caractères supplémentaires sont stockés. Autres

---

- Oui. 7. Pourquoi ce problème se pose dans les entrevues

1. ** API d'état** – Il teste votre compréhension de *état persistant* à travers les appels de méthode, un piège d'entrevue commun.
2. **Buffering** – Démontre la capacité de penser dans *sliding windows* et *small fixated buffers* – un modèle qui apparaît dans les problèmes réels d'OI, de réseautage et de streaming.
3. **L'espace contre les compromis temporels** – Montre que vous pouvez répondre à l'espace strict O(1) tout en restant linéaire dans le temps – une contrainte d'entrevue classique.
4. **Connaissance des cas** – Vous allez discuter `EOF`, `n > reste chars`, et comment les gérer avec grâce.

---

- Oui. 8. Conseils d'entrevue

- **Demander des éclaircissements** : "Lecture" n'est-elle garantie qu'avec un nouveau tampon à chaque fois ? Et la remise en état ? (en milliers de dollars)
- ** Expliquez votre plan d'abord**: Décrivez l'approche tampon avant d'écrire le code; les intervieweurs aiment voir un processus de pensée clair.
- **Discussion de la complexité**: Ma solution lit au plus des caractères `n`, utilise seulement un tampon 4-char, donc le temps est linéaire et l'espace est constant. (en milliers de dollars)
- **Les cas de test de Mention**: montrez un exemple rapide (`file = "abcd"`, `read(2) → [ab]`, puis `read(3) → [cd]`).

---

- Oui. 9. Tendances finales

C'est bien, c'est mal.
C'est pas vrai.
**Bon** – Solution d'espace à passe unique et constante utilisant un tampon 4-char persistant. **Bad** – Les solutions naïves qui rejettent les caractères non lus brisent la règle des appels multiples. Autres

Rappelez-vous : ** État permanent + logique de copie prudente = victoire**.

---

10 ans. Conduisez votre entrevue au niveau suivant

- *Show the buffer trick** – c'est la solution la plus élégante et démontre une profonde compréhension de l'état d'OI.
- **Discuss complexité** – les intervieweurs s'attendent à un temps O(n) clair, O(1) espace répondre aux problèmes difficiles.
- Dans un fichier 7-char, essayer `read(2)` puis `read(5)` dans un fichier 7-char, ou `read(4)` puis `read(4)` dans un fichier 3-char.
- **Explain réinitialise** – soulignez que LeetCode crée une nouvelle instance `Solution` par cas de test, donc les variables d'instance réinitialisent naturellement.

---

Nombre d'échantillons de code complet (Ready for LeetCode)

"Java
// Java – coller directement dans l'éditeur
public class Solution étend Reader4 {
char[] buf4 = nouveau char[4];
Services privés Ptr = 0;
Int privé bufCnt = 0;

@Override
public int read(char[] buf, int n) {
= 0;
alors que (total < n) {
Si (bufPtr) 0) {
bufCnt = lecture4(buf4);
Si (bufCnt) 0) pause;
}
alors que (total < n& bufPtr < bufCnt) {
buf[total++] = buf4[bufPtr++];
}
si (bufPtr) bufPtr = 0;
}
le total des retours;
}
}
«» "

'`python
# Python – coller dans l'éditeur
solution de classe(Reader4):
def _init_(self):
Super().__init_()
auto.buf4 = [0]*4
auto.ptr = 0
auto.cnt = 0

def read(self, buf: Liste[str], n: int) -> Int:
Total = 0
alors que total < n:
si self.ptr == 0:
Self.cnt = self.read4(self.buf4)
si self.cnt == 0:
pause
alors que total < n et auto.ptr < auto.cnt:
buf.append(self.buf4[self.ptr])
Total += 1
auto.ptr += 1
si self.ptr >= Self.cnt:
auto.ptr = 0
retour total
«» "

'`cpp
// C++ – coller dans l'éditeur
class Solution : public Reader4 {
public:
la teneur en soufre de l'huile d'olive,
bufPtr = 0;
bufCnt = 0;

int read(char *buf, int n) surcharge {
= 0;
alors que (total < n) {
Si (bufPtr) 0) {
bufCnt = lecture4(buf4);
Si (bufCnt) 0) pause;
}
alors que (total < n& bufPtr < bufCnt) {
buf[total++] = buf4[bufPtr++];
}
si (bufPtr) bufPtr = 0;
}
le total des retours;
}
};
«» "

---

11 ans. Mot final

LeetCode 158 est un problème classique *stateful IO*.
- L'astuce **buffer** transforme une exigence d'appel multiple en une solution d'espace constant trivial.
- Maître ce modèle et vous serez prêt pour toute une famille de questions d'entrevue impliquant *streaming*, *buffering* et *lits partiels*.

Bonne chance – et rappelez-vous, la solution *right* semble toujours propre, explique clairement l'état, et gère chaque cas de bord sans espace supplémentaire. Bon codage !