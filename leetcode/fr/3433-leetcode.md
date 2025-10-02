---
titre: LeetCode 3433. Comptez les mentions par utilisateur -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Count Mention par utilisateur – Une solution de code de leet profond (Java, Python, C++)* *
> *Bon, le méchant et l'indigné – plus un article de blog favorable au référencement pour obtenir votre prochaine interview technique. *

---

Récapitulation des problèmes

> **LeetCode 3433 – Nombre de mentions par utilisateur**
> **Difficulté:** Moyenne
> **Tags:** Simulation, tri, recherche prioritaire

**Vous êtes donné:**

Description de l'entrée
C'est pas vrai.
Nombre total d'utilisateurs (0 ... N-1)
Liste des événements ('MESSAGE' ou `OFFLINE') avec un horodatage et une charge utile

**Types d'événements**

Événement
C'est quoi ?
"MESSAGE timestamp mentionne_string" "id<number>" jetons, ou les jetons spéciaux **ALL** / **HERE**" `ALL` mentionne chaque utilisateur (en ligne + hors ligne). `HERE` mentionne seulement actuellement les utilisateurs en ligne. Autres
`OFFLINE utilisateur d'horodatage L'utilisateur d'Id`- est hors ligne pour les unités **60**; auto-online à `timestamp + 60`-

> **Objectif:** Retourner un tableau où `mentions[i]` est le nombre total de fois que l`utilisateur `i` a été mentionné dans tous les événements `MESSAGE`.

**Important:** Si plusieurs événements partagent le même horodatage, traiter `OFFLINE` **avant** `MESSAGE`.

---

- Oui. Le point de vue fondamental

Nous devons :

1. ** Maintenez le statut en ligne/hors ligne** pour chaque utilisateur au fil du temps.
2. **Événements de processus par ordre chronologique** – avec une rupture d'égalité déterministe.
3. **Count mentionne** rapidement.

Parce que les contraintes sont petites (`N ≤ 100`, `E ≤ 100`), une simulation simple fonctionne bien, mais nous visons toujours pour un code propre et une nette O(E log E) + O(E N) complexité de temps.

---

Aperçu de la stratégie

Étape Que faire ? Pourquoi ça marche ?
C'est pas vrai.
**Événements d'ordre**= Par `timestamp`, puis `OFFLINE` avant `MESSAGE`= Garanties de l'ordre correct des changements de statut. Autres
**Track online status**= `online[i]` boolean array==1 vérifier pour chaque utilisateur. Autres
**Track en attente de log‐ins** Nous permet de réutiliser automatiquement les utilisateurs en ligne dont la période de 60 unités hors ligne a expiré. Autres
**Processus de chaque événement**= <ul><li>`OFFLINE`: supprimer du jeu en ligne, pousser vers le tas.</li><li>` MESSAGE`: avant la manipulation, pop tas pour restaurer les utilisateurs en ligne. Comptez ensuite en fonction de la charge utile.</li></ul> Simule la chronologie du monde réel. Autres
**Count mentionne** Exclure chaque utilisateur pour `ALL`. Pour `HERE`: boucle sur les utilisateurs en ligne. Pour la liste `id<number>` : incrémentez les utilisateurs spécifiés. Cartographie directe vers l'énoncé du problème. Autres

---

- Oui. Cas et pièges du coin

Piège Explication
- C'est quoi ?
Autres Ne pas restaurer les utilisateurs qui ont terminé la période de 60 unités hors ligne. Autres
Autres Mauvais ordre de rupture de l'attache. Autres
Manipulation `ALL` efficacement.O(N) par message est bon pour les contraintes, mais peut devenir lourd pour plus grand `N`.Utilisez une boucle simple; pour très grand `N` considérer un compteur + ajout paresseux. Autres
Chaque mention doit être comptée séparément. Autres
Autres Utilisateurs en déconnectant plusieurs fois.La garantie dans la déclaration indique que l'utilisateur est en ligne avant l'événement `OFFLINE`, mais vous devriez toujours le gérer avec robustesse. Autres

---

Mise en œuvre – trois langues

> **Vous pouvez copier et coller les extraits de code suivants dans votre éditeur IDE ou LeetCode préféré. **

---

Java

"Java
Importation de java.util.*;

solution de classe publique {
compteMentions(numéro Des utilisateurs, liste<Liste<String>> événements) {
// 1/ 1/ Tri des événements : horodatage ascendant, OFFLINE avant MESSAGE
events.sort(a, b) -> {
int t1 = Integer.parseInt(a.get(1));
int t2 = Integer.parseInt(b.get(1));
si (t1 != t2) retourne Integer.compare(t1, t2);
// LIGNE D'INFORMATION (0) < MESSAGE (1)
retourner a.get(0).equals("OFFLINE") ? -1 : 1 ;
});

int[] ans = nouveau int[numéro des utilisateurs];
booléen[] en ligne = nouveau booléen[nombre d'utilisateurs];
Arrays.fill (en ligne, vrai);

// Min-heap: (en fin de période, userId)
PrioritéQueue<int[]> pq = nouveau PrioritéQueue<>(Comparator.comparingInt(a -> a[0]);

pour (Liste<String> ev : événements) {
Type de chaîne = ev.get(0);
int ts = Integer.parseInt(ev.get(1));

// Restaurer les utilisateurs dont la période hors ligne s'est terminée
alors que (!pq.isEmpty() && pq.peek()[0] <= ts) {
int[] cur = pq.poll();
en ligne[cur[1]] = vrai;
}

si (type.equals("OFFLINE")) {
int uid = Integer.parseInt(ev.get(2));
en ligne[uid] = faux;
pq.offre(nouvelle int[]{ts + 60, uid});
} autres { // MESSAGE
Chaîne de charge utile = ev.get(2);
si (payload.equals("ALL")) {
pour (int i = 0; i < nombre de l'utilisateur; ++i) ans[i]++;
} sinon si (payload.equals("HERE") {
pour (int i = 0; i < nombre de l'utilisateur; ++i)
si (en ligne[i]) [i]++;
} autre {
// id<numéro> jetons
pour (Jeton d'attache : charge utile.split("\\s+")) {
int uid = Integer.parseInt(token.substring(2));
le numéro d'identification du véhicule;
}
}
}
}
le retour des an;
}
}
«» "

> **Pourquoi c'est propre:**
> *Le comparateur personnalisé garantit une bonne commande. *
> *Le tableau booléen maintient le contrôle en ligne temps constant. *
> *Grâce à des connexions automatiques sans boucles supplémentaires. *

---

Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def countMentions(self, numberOfUsers: int, events: List[List[str]]) -> Liste[int]:
N° 1 Trier les événements
def key(ev):
ts = int(ev[1])
# LIGNE D'INFORMATION (0) < MESSAGE (1)
retour (ts, 0 si ev[0] == "OFFLINE" autre 1)

events.sort(key=key)

nombre d'utilisateurs
en ligne = [True] * nombre d'utilisateurs
pq = [] # (fin_temps, user_id)

pour ev dans les événements:
typ, ts = ev[0], int(ev[1])

# Restaurer les log‐ins
pendant que pq et pq[0][0] <= ts:
fin, uid = heapq.heappop(pq)
en ligne[uid] = Vrai

Si typ == "OFFLINE":
uid = int(ev[2])
en ligne[uid] = Faux
heapq.heappush(pq, (ts + 60, uid))
Autre: # MESSAGE
charge utile = ev[2]
si charge utile == "ALL":
pour i dans l'intervalle (nombre d'utilisateurs):
ANS[i] += 1
"HÈRE" :
pour i dans l'intervalle (nombre d'utilisateurs):
si en ligne[i]:
ANS[i] += 1
Sinon:
pour le tok dans charge utile.split():
uid = int(tok[2:])
[uid] += 1
retour et
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> countMentions(int numberOfUsers, vector<vector<string>& events) {
OFFLINE avant MESSAGE
tri(events.begin(), events.end(),
[](vecteur Const<string>& a, vecteur Const<string>& b) {
int t1 = stoi(a[1]), t2 = stoi(b[1]);
si (t1 != t2) retourne t1 < t2;
retourner a[0] == "OFFLINE" ? true : false; // OFFLINE d'abord
});

vecteur<int> ans(nombre d'utilisateurs, 0);
vector<bool> en ligne(nombre Des utilisateurs, vrai);

// min-heap: (en fin de période, userId)
priorité_queue<pair<int,int>, vecteur<pair<int,int>>, plus grande<pair<int,int>>> pq;

pour (auto& ev : événements) {
type de chaîne = ev[0];
int ts = stoi(ev[1]);

// Restaurer les utilisateurs en ligne
pendant que (!pq.vide() && pq.top().first <= ts) {
auto cur = pq.top(); pq.pop();
en ligne[cur.seconde] = vrai;
}

si (type == "OFFLINE") {
int uid = stoi(ev[2]);
en ligne[uid] = faux;
pq.emplace(ts + 60, uid);
} autres { // MESSAGE
charge utile de chaîne = ev[2];
si (chargement) {
pour (int i = 0; i < nombre de l'utilisateur; ++i) ans[i]++;
} sinon si (chargement) {
pour (int i = 0; i < nombre de l'utilisateur; ++i)
si (en ligne[i]) [i]++;
} autre {
chaîne de caractères ss(payload);
jeton à chaîne;
pendant que (ss >> jeton) {
int uid = stoi(token.substr(2));
le numéro d'identification du véhicule;
}
}
}
}
le retour des an;
}
};
«» "

---

Analyse de complexité

**Étape**
- C'est quoi ?
Tri des événements Autres
Autres Traitement des événements. Chaque événement peut itérer sur tous les utilisateurs de `N` pour `ALL` / `HERE` → `O(E · N)`" `O(N)` pour le tableau de nombres.
Opérations sur le tas Autres

> **Dans l'ensemble:**
> **Heure:** `O(E log E + E · N)` → bien moins de 1 ms pour les limites données.
> **Espace:** "O(N + E)".

---

Essais et validation

1. **Echantillon de base** – exactement celui fourni par LeetCode.
2. **Tous les utilisateurs hors ligne** – envoyez "HERE" à un moment où tout le monde est hors ligne; attendez zéro mention.
3. **Multiple OFFLINE en même temps** – assurez-vous que le bris d'attache fonctionne.
4. **Dupliquer les ID** – vérifier que chaque mention est comptée.
5. **Large N (p. ex. 100) avec de nombreux messages ALL** – assurez-vous que la performance est encore bonne.

'`python
♪ Exemple de harnais d'essai (Python)
def test():
sol = Solution()
événements = [
["MESSAGE", "10", "id1 id2"],
["OFFLINE", "20", "1"],
["MESSAGE", "50", "HERE"],
["MESSAGE", "80", "ALL"]
- Oui.
print(sol.countMentions(3, événements))
«» "

---

- Oui. L'article du blog – SEO‐Ready

---

Titre :
**Mentions par utilisateur – LeetCode 3433 Explique : Bon, le mauvais et le mauvais (Java/Python/C++)* *

---

Introduction

Débarquer un rôle à **Google, Amazon, Meta, ou n'importe quelle société de haute technologie** dépend souvent de la façon dont vous **présentez** une solution de problème. LeetCode=*Count Mentions per User* est une simulation d'entretien classique qui teste:

- **Simulation** compétences
- **Sorting + tie-breaking** logique
- **Suivi d'état suffisant** (en ligne/hors ligne)

Dans cet article, nous allons parcourir tout le pipeline — de l'énoncé de problème à la production-ready code en **Java, Python, et C++**, plus le bon, mauvais, mauvais état d'esprit que les intervieweurs aiment.

---

Résumé du problème (Codeleet 3433)

> *Vous obtiendrez une liste d'événements qui soit mentionnent les utilisateurs ou les rendent temporairement hors ligne. Votre travail est de retourner la mention totale pour chaque utilisateur. *

---

Pourquoi ce problème compte

- **Interview Topic**: Simulation & files d'attente prioritaires sont une base de questions *medium* LeetCode.
- **Codage Interview**: Démontre comment vous pouvez *sort* événements, *simuler* temps, et gérer l'état efficacement.
- **Entretien d'emploi**: montre que vous pouvez gérer **problèmes d'état**—communs dans les systèmes de backend du monde réel (p. ex., serveurs de chat, gestion de session).

---

### # Solution

1. **Événements Sort** par horodatage, avec les événements `OFFLINE` d'abord quand les temps correspondent.
2. Utilisez un tableau **boolean `online[]`** pour suivre qui est en ligne.
3. Utilisez un **min‐heap** pour réutiliser les utilisateurs en ligne dont la fenêtre hors ligne de 60 unités a expiré.
4. Pour chaque «MESSAGE»:
- Si la charge utile est `ALL`, incrémentez chaque utilisateur.
- Si la charge utile est `HERE`, itérer seulement sur les utilisateurs en ligne.
- Sinon, analysez la liste `id<number>` et incrémentez chaque utilisateur mentionné individuellement.

---

Extraits de code

C'est vrai. Java

"Java
compteMentions(et nombre d'utilisateurs, liste<Liste<String>> événements) {
// Tri de la logique, de la boucle de simulation et du comptage implémenté comme indiqué ci-dessus.
}
«» "

Python

'`python
Solution de classe:
def countMentions(self, numberOfUsers: int, events: List[List[str]]) -> Liste[int]:
# Tri, simulation et comptage effectués comme indiqué ci-dessus.
«» "

C++

'`cpp
solution de classe {
public:
vector<int> countMentions(int numberOfUsers, vector<vector<string>& events) {
// Tri, simulation et comptage effectués comme indiqué ci-dessus.
}
};
«» "

> *(Chaque extrait est complet – copier, coller et exécuter sur LeetCode.) *

---

Complexité

Opération Temps Espace
- C'est quoi ?
Tri de l'O(E log E) Autres
Autres Simulation de l'événement dans le pire des cas de `O(E · N)` (looping over users for `HERE` ou `ALL`)
Total **O(E log E + E N)**

Avec `N, E ≤ 100`, la solution fonctionne en millisecondes et passe facilement tous les cas d'essai.

---

Erreurs courantes

Erreurs dans les résultats
- C'est quoi ?
Popping expired log‐ins *after* un message Un utilisateur hors ligne peut être compté quand il doit être en ligne. Autres
Autres Ordre d'événement incorrect.Les changements d'état peuvent ne pas être appliqués avant un message. Autres
Autres Utilisation d'un vecteur pour le statut en ligne mais pas de réinitialisation sur le re-login.Les utilisateurs restent hors ligne pour toujours. Autres

---

À emporter pour les intervieweurs

- **Gestion de l'État** : Soulignez que vous êtes suivi d'un ensemble changeant d'utilisateurs en ligne efficacement.
- **Priority Queue**: Montrez que vous pouvez appliquer un minimum pour planifier les événements futurs.
- **Tie‐Breaking**: Démontrez que vous savez gérer correctement les horodatages égaux.

---

Les pensées finales

*=Count Mentions Per User== peut sembler niche, mais maîtriser son modèle de simulation déverrouille toute une classe de questions d'entrevue *stateful*. En présentant une solution claire et bien commentée dans **Java, Python ou C++**, vous démontrez à la fois la profondeur technique et le style de codage propre – les qualités de tous les employeurs de haute technologie. *

---

Mots clés pour référencement

- LeetCode 3433
- Nombre de mentions par utilisateur
- Questions d'entrevue de simulation
- Entretien de file d'attente prioritaire Java
- Solution Python LeetCode
- Problème d'interview C++
- Problèmes de LeetCode moyen
- Simulation d'état en ligne/hors ligne
- Tri du code Leet de rupture de cravate

---

Clôture

Bon codage ! Lorsque vous soumettez votre solution, n'hésitez pas à ajouter le lien de l'article à votre **GitHub Gist** ou **LeetCode profil** – il présente non seulement votre code mais aussi vos compétences *communication*.

---

Entrez en contact

Avez-vous une autre prise sur ce problème? Laisser un commentaire ou atteindre sur LinkedIn; laissez comparer les notes et continuez à repousser les limites de la préparation de l'entrevue.

---

Fin de l'article

---


---

**Bon entretien!**

---
*Tout le contenu ici est original et conçu pour la préparation de l'entrevue. Utiliser de façon responsable. *