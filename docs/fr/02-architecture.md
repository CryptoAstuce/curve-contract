# Chapitre 2 — Architecture du depot

`contracts/pool-templates/` est le coeur du depot. Chaque sous-dossier est un gabarit : `base` (pool minimal sans pret), `a` (pret style Aave, l'interet fait monter le solde), `y` (pret style yearn, l'interet fait monter un taux de change), `eth` (pool avec l'ETH natif) et `meta` (pool adosse a un autre pool).

`contracts/pools/` contient les pools reellement deployes : chaque dossier (`3pool`, `compound`, `busd`, `aave`...) porte un `pooldata.json` qui fixe les constantes du gabarit correspondant pour ce pool precis.

`contracts/tokens/` contient les trois versions du jeton de liquidite, `CurveTokenV1` a `V3` : c'est le jeton que recoit un fournisseur de liquidite en echange de son depot.

Les gabarits utilisent des variables « triple-underscore », par exemple `___N_COINS___` ou `___RATES___`, remplacees a la compilation par les valeurs du `pooldata.json`. Un meme fichier `.vy` sert donc de source a plusieurs pools distincts.

`contracts/testing/` fournit des jetons factices pour les tests ; ils ne font pas partie du protocole publie.

[Chapitre suivant : l'invariant StableSwap](03-invariant-stableswap.md)
