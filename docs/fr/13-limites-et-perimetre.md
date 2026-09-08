# Chapitre 13 — Limites connues et perimetre de ce parcours

L'invariant StableSwap suppose des actifs correles. Applique a des jetons dont la parite se rompt reellement (un stablecoin qui decroche, par exemple), le pool amplifie la perte pour les fournisseurs de liquidite compares a un simple detenteur : c'est le prix a payer pour le glissement quasi nul en conditions normales.

`ramp_A` reste un pouvoir du proprietaire ; meme borne et retarde, il change les conditions du pool sans consentement individuel des fournisseurs de liquidite, qui ne peuvent que retirer leurs fonds pendant le delai de trois jours s'ils desapprouvent.

Les jetons a commission sur transfert ou a rebasement non standard peuvent desynchroniser `balances` (le solde interne comptable) du solde ERC-20 reel detenu par le contrat, un ecart que seule `donate_admin_fees` peut resorber manuellement.

Ce depot ne contient ni les jauges de recompense en CRV, ni le registre on-chain des pools, ni la gouvernance du protocole (DAO, vote-escrowed CRV) : ces pieces vivent dans d'autres depots de l'organisation Curve.Fi et sortent du perimetre de ce parcours.

Rien n'a ete installe, compile, deploye ni execute pour ecrire ces chapitres. Aucun test n'a ete lance. Ces chapitres decrivent ce que le code source Vyper dit faire, en renvoyant aux fichiers. Pour verifier par vous-meme, le depot fournit une suite de tests Brownie, decrite dans le `README` racine.
