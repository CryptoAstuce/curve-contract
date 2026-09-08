# Chapitre 11 — Les metapools

Un metapool, gabarit `meta` dans `SwapTemplateMeta.vy`, echange un nouveau jeton contre le jeton de liquidite d'un pool de base deja existant, par exemple un stablecoin recent contre le `3Crv` du pool DAI/USDC/USDT.

L'interet est de ne pas fragmenter la liquidite : au lieu de creer un pool a trois jetons pour chaque nouveau stablecoin, on cree un pool a deux « jetons » ou le second est en realite la part d'un pool profond deja etabli.

`exchange` echange directement contre le jeton de liquidite du pool de base ; `exchange_underlying` va plus loin et traverse le pool de base pour livrer un des jetons sous-jacents (DAI, USDC ou USDT) directement, en enchainant deux operations en une seule transaction.

`get_dy_underlying` expose l'estimation correspondante. Le prix relatif entre le nouveau jeton et le panier du pool de base suit le meme invariant StableSwap que n'importe quel autre pool, avec son propre `A` et ses propres frais, independants de ceux du pool de base sous-jacent.

[Chapitre suivant : le jeton de liquidite et le registre](12-jeton-de-liquidite.md)
