# Chapitre 6 — L'echange entre jetons

`exchange` echange un montant `_dx` du jeton `i` contre le jeton `j`. Le calcul repose sur `_get_y`, qui resout la meme equation d'invariant que `_get_D`, mais cette fois pour trouver le nouveau solde du jeton de sortie qui maintient `D` constant apres l'ajout du jeton d'entree.

`_get_y` reformule l'equation StableSwap comme un polynome du second degre en `y` et la resout, la aussi par iteration de Newton, avec les memes garanties de convergence que `_get_D`.

Le montant recu brut est `dy = xp[j] - y - 1`, le `-1` etant une marge de securite contre les erreurs d'arrondi en faveur du pool plutot que de l'appelant. Les frais du pool sont ensuite retranches : `fee = self.fee * dy / FEE_DENOMINATOR`.

`get_dy` expose la meme estimation en lecture seule, pour construire une transaction avec un `_min_dy` de protection contre le glissement. `exchange` verifie `_dx` transfere reellement recu (pas seulement declare) avant de calculer, ce qui neutralise les jetons a commission sur transfert.

[Chapitre suivant : retrait de liquidite](07-retrait-de-liquidite.md)
