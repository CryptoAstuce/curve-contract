# Chapitre 10 — Pools de pret et pools ETH

Les gabarits `a` et `y` echangent des versions porteuses d'interet des jetons plutot que les jetons bruts : cTokens de Compound, aTokens d'Aave, yTokens de yearn.

La difference tient a la maniere dont l'interet se manifeste. Dans le style « a » (Aave), l'interet fait croitre directement le solde du jeton detenu : le taux de conversion reste fixe, mais la quantite augmente avec le temps. Dans le style « y » (yearn), c'est l'inverse : la quantite de jetons reste fixe, mais leur taux de change vers l'actif sous-jacent grimpe.

Ces gabarits recalculent `RATES` a chaque operation via un appel au protocole de pret sous-jacent, au lieu d'utiliser la constante figee du gabarit `base`. C'est ce taux dynamique qui permet a `_xp` de continuer a exprimer des soldes correctement compares, meme quand un jeton du panier accumule silencieusement de l'interet.

Le gabarit `eth` gere un cas particulier : l'un des jetons du pool est l'ETH natif de la chaine, qui n'est pas un ERC-20 et doit etre recu et envoye via des transferts natifs plutot que `transferFrom`.

[Chapitre suivant : les metapools](11-metapools.md)
