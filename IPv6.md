# IPV6

## NAT

Pas besoin de **NAT** en **IPV6** la machine est directement accessible depuis le réseau sans passer par les règles **NAT** de la box. Plus besoin de rediriger les ports du côté de la box...

Il y a donc un grand intérêt de configurer un **pare-feu** avec `ip6tables` sinon tous ce qui écoute depuis votre machine est directement accessible depuis le web.