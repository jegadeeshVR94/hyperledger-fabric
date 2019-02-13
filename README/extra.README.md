crypto-config.yaml

Peers can be present in diff network or diff physical machine but they are organised logically in the same org . peers can work only if they are in the same org. they can discover each other, they can share data but only if they are in same org


peers from other org can not comminicate to other orgs peers directly

certificates tells peer and orderers from which org they belong

cert gives identity to each participant on nw


certeficates are tied to specific domain.

so even if somebody outsied the network gets the cert of a peer that is a part of some org and he/she starts this peer on completely diff n/w. and as the peer is in the same org he/sheis able to find other peers, sync with them but as this peer is outsied the nw. and cert are tied to a specifig domain, connection gets refused & data lekage is prevented.

so domain name is important
