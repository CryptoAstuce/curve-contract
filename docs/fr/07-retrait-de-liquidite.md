# Chapitre 7 — Retrait de liquidite

Trois fonctions couvrent trois facons de sortir d'un pool.

`remove_liquidity` retire proportionnellement aux soldes actuels du pool, sans frais : c'est la sortie « neutre », celle qui ne change pas l'equilibre du pool et ne peut donc pas etre exploitee pour arbitrer les autres fournisseurs de liquidite.

`remove_liquidity_imbalance` retire des montants precis choisis par l'appelant, ce qui peut desequilibrer le pool ; des frais identiques a ceux de `add_liquidity` s'appliquent alors, calcules par ecart au solde ideal.

`remove_liquidity_one_coin`, appuyee sur `_get_y_D`, retire la totalite en un seul jeton : cette fonction resout l'invariant a l'envers pour trouver combien d'un seul jeton correspond a la reduction de `D` demandee, puis applique les frais d'echange implicites de cette conversion interne.

Dans les trois cas, le jeton de liquidite est brule via `burnFrom` avant que les jetons sous-jacents ne soient transferes : l'ordre protege contre une double sortie en cas de reentrance.

[Chapitre suivant : le parametre A et son ramping](08-parametre-a.md)
