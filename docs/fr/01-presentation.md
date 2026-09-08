# Chapitre 1 — Presentation de Curve

Curve est un teneur de marche automatise specialise dans l'echange d'actifs correles : stablecoins entre eux, ou versions differentes d'un meme actif. Le depot est publie par Curve.Fi, code source en Vyper.

La difference avec un AMM generaliste comme Uniswap est l'invariant : Curve n'utilise pas le produit constant `x*y=k`, mais une formule hybride qui se comporte comme une somme constante `x+y=k` pres de l'equilibre et comme un produit constant loin de l'equilibre. Le resultat : un glissement de prix presque nul pour des echanges entre actifs qui devraient valoir la meme chose, DAI contre USDC par exemple.

Ce depot ne contient pas un pool unique mais une famille de gabarits (`pool-templates`) et des pools deja deployes (`contracts/pools`), chacun genere a partir d'un gabarit avec des constantes propres.

Les contrats sont ecrits en Vyper, un langage plus restreint que Solidity, pense pour limiter les erreurs (pas d'heritage complexe, pas de modificateurs, boucles bornees).

Ce parcours s'appuie sur `contracts/pool-templates/base/SwapTemplateBase.vy`, le gabarit le plus simple, sans logique de pret, et sur les gabarits `meta`, `a`, `y` et `eth` pour les variantes.

Rien n'a ete installe, compile ni execute pour ecrire ces chapitres.

[Chapitre suivant : architecture du depot](02-architecture.md)
