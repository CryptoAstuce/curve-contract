# Chapitre 12 — Le jeton de liquidite et le registre des pools

`contracts/tokens/` contient trois versions successives du jeton de liquidite : `CurveTokenV1`, `V2` et `V3`. Chaque pool deploie sa propre instance, dont seul le contrat du pool associe peut appeler `mint` et `burnFrom` — c'est cette restriction qui garantit que l'offre du jeton reflete exactement les depots nets dans le pool.

Chaque pool deploye est decrit par un `pooldata.json` dans `contracts/pools/<nom>/`, qui fixe l'adresse du pool, celle du jeton de liquidite, et pour les pools plus recents une liste `gauge_addresses` : les jauges sont des contrats externes a ce depot qui distribuent des recompenses en jeton CRV aux fournisseurs de liquidite qui y deposent leur jeton, mais leur logique n'est pas dans `curve-contract`.

`integrations.md` documente comment un contrat externe est cense dialoguer avec un pool : lire les adresses via `coins`, estimer un echange via `get_dy` ou `get_dy_underlying`, puis executer via `exchange` avec un `min_dy` de protection.

Cette separation entre le pool (ce depot), le registre des pools et les jauges de recompense (ailleurs) permet a chaque piece d'evoluer independamment sans redeployer les pools existants.

[Chapitre suivant : limites et perimetre](13-limites-et-perimetre.md)
