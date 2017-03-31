.. title: Minar ethereum
.. slug: minar-ethereum
.. date: 2017-03-30 12:00:00 UTC-06:00
.. tags: cryptomoneda, minar, ethereum, jaquerespeis
.. author: Alvaro Segura Del Barco
.. link:
.. description: Como minar ethereum facilmente
.. category: guias

# Requerimientos

* Minardor
* Ubuntu 16.04
* Opcional(tarjeta de video)

# Instalación

Instalar ubuntu 16.04

Un vez que se tiene instalado el sistema operativo, activar el ppa de ethereum

```
sudo add-apt-repository ppa:ethereum/ethereum
sudo apt-get update
```

Instalar cpp-ethereum

clonar el repositorio de eth-proxy

Crear un wallet con geth o parity

Instalar los drivers de video, en el caso de una radeon rx 480.

modificar el archivo de configuración de eth-proxy para usar el wallet.

ejecutar ethminer a localhost

ethminer -F http://127.0.0.1:8080/minador -G

# Referencias
https://github.com/paritytech/parity
https://github.com/Atrides/eth-proxy
https://launchpad.net/~ethereum/+archive/ubuntu/ethereum


