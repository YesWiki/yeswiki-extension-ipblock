# Extension ipblock

Bloque l'édition depuis les adresses IP de pays choisis, ou depuis des adresses
précises.

La consultation reste ouverte : seuls les accès en écriture sont refusés.

## Configuration

Dans `wakka.config.php`, ou par la roue crantée puis Gestion du site, onglet
« fichier de conf. ».

| Clé | Format | Rôle |
|---|---|---|
| `ipblock_blocked_countries` | tableau de codes pays sur 2 lettres | pays dont les IP ne peuvent pas éditer |
| `ipblock_blocked_ips` | tableau d'adresses IP | adresses précises à refuser |

```php
'ipblock_blocked_countries' => ['ID', 'MY'],
'ipblock_blocked_ips' => ['203.0.113.7', '198.51.100.22'],
```

## Comment la correspondance est faite

L'extension embarque sa propre base de plages d'adresses par pays, d'où sa taille :
c'est de loin le plus gros dépôt d'extension, autour de 60 000 lignes de PHP. Aucun
service externe n'est interrogé, donc rien ne fuite, mais la base vieillit avec le
dépôt et n'est à jour qu'au dernier commit.

## Précaution

Le blocage se fait sur l'IP vue par le serveur. Derrière un proxy ou un CDN, cette IP
est celle du proxy pour tout le monde : vérifier que le serveur web renseigne bien
l'adresse réelle avant de compter sur ce filtrage.
