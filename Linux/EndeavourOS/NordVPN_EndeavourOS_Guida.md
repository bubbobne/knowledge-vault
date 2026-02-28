# NordVPN su EndeavourOS

**Tag:** #linux #vpn #privacy #network

------------------------------------------------------------------------

## Installazione (AUR)

``` bash
yay -S nordvpn-bin
```

------------------------------------------------------------------------

## Abilitare il servizio

``` bash
sudo systemctl enable nordvpnd.service
sudo systemctl start nordvpnd.service
```

Verifica:

``` bash
systemctl status nordvpnd
```

------------------------------------------------------------------------

## Primo accesso (una sola volta)

Se richiesto:

``` bash
sudo groupadd nordvpn
sudo usermod -aG nordvpn $USER
```

Poi fare logout/login o riavviare il sistema.

Login:

``` bash
nordvpn login
```

------------------------------------------------------------------------

# Uso quotidiano

## Connettersi

Automatico:

``` bash
nordvpn connect
```

Paese specifico:

``` bash
nordvpn connect italy
```

Server specifico:

``` bash
nordvpn connect italy #123
```

------------------------------------------------------------------------

## Disconnettersi

``` bash
nordvpn disconnect
```

------------------------------------------------------------------------

## Stato connessione

``` bash
nordvpn status
```

IP pubblico:

``` bash
curl ifconfig.me
```

------------------------------------------------------------------------

# Lista server e filtri

## Lista paesi disponibili

``` bash
nordvpn countries
```

## Lista città di un paese

``` bash
nordvpn cities italy
```

## Lista server disponibili per un paese

``` bash
nordvpn servers italy
```

## Lista gruppi speciali

``` bash
nordvpn groups
```

------------------------------------------------------------------------

# Cosa sono i gruppi speciali?

I gruppi speciali sono categorie di server ottimizzati per scopi
specifici.

Esempi:

-   **P2P** → ottimizzati per traffico peer-to-peer\
-   **Double VPN** → traffico instradato su due server consecutivi\
-   **Onion Over VPN** → traffico passa nella rete Tor dopo la VPN\
-   **Obfuscated Servers** → mascherano il traffico VPN su reti
    restrittive\
-   **Dedicated IP** → IP fisso personale (se acquistato)

Connessione a un gruppo speciale:

``` bash
nordvpn connect p2p
```

Combinato con paese:

``` bash
nordvpn connect italy p2p
```

------------------------------------------------------------------------

# Impostazioni consigliate

## Usare NordLynx (WireGuard)

``` bash
nordvpn set technology nordlynx
```

## Attivare kill switch

``` bash
nordvpn set killswitch on
```

## Attivare auto-connect

``` bash
nordvpn set autoconnect on
```

## Vedere tutte le impostazioni

``` bash
nordvpn settings
```

------------------------------------------------------------------------

# Troubleshooting

Log del servizio:

``` bash
journalctl -u nordvpnd
```

Verificare interfaccia VPN:

``` bash
ip a | grep nord
```

Controllare DNS:

``` bash
cat /etc/resolv.conf
```

------------------------------------------------------------------------

# Note tecniche

-   Il client utilizza il servizio `nordvpnd`
-   NordLynx è basato su WireGuard (più veloce di OpenVPN)
-   La VPN cambia l'IP pubblico ma non garantisce anonimato assoluto
-   La privacy reale è un sistema a strati (VPN + DNS + browser
    configurato bene + buone abitudini digitali)
