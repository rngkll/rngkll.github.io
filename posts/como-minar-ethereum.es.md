.. title: Minar ethereum
.. slug: minar-ethereum
.. date: 2017-03-30 12:00:00 UTC-06:00
.. tags: cryptomoneda, minar, ethereum, jaquerespeis
.. author: Alvaro Segura Del Barco
.. link:
.. description: Como minar ethereum facilmente
.. category: guias

# Requerimientos

* Minador
* Ubuntu Server 16.04
* Opcional(tarjeta de video)
* Python y python-twisted
* Ethereum
* cpp-ethereum

_**NOTA:** Se considera Ubuntu Server, en caso de Ubuntu Desktop algunos requerimientos ya vienen instalados en el sistema._

# Instalación

1. Instalar ubuntu 16.04

1. Instalar python y python-wisted

```bash
sudo apt-get install python
sudo apt-get install python-twisted
```

1. Un vez que se tiene instalado el sistema operativo, activar el ppa de ethereum

```bash
sudo add-apt-repository ppa:ethereum/ethereum
sudo add-apt-repository ppa:ethereum/ethereum-qt
sudo add-apt-repository ppa:ethereum/ethereum-dev
sudo apt-get update
```

1. Instalar ethereum

```bash
sudo apt-get install ethereum
```

1. Instalar cpp-ethereum
```bash
sudo apt-get install cpp-ethereum
```

1. Clonar el repositorio de [eth-proxy](https://github.com/Atrides/eth-proxy).

1. Crear un wallet con [geth](https://github.com/ethereum/go-ethereum/wiki/geth) o [parity](https://github.com/paritytech/parity).

1. Instalar los drivers de video, en el caso de usar una tarjeta de video.

1. Modificar el archivo de configuración de eth-proxy para usar el wallet.

1. En el directory de eth-proxy, ejecutar `eth-proxy.py`

```bash
sudo python eth-proxy/eth-proxy.py
```

1. Ejecutar `ethminer` apuntando a localhost

```bash
ethminer -F http://127.0.0.1:8080/minador -G
```
_**NOTA:** La opción `-G` indica a ethminer que utilice GPU para minar, en caso de no contar con GPU utilice `--allow-opencl-cpu`._

# Referencias
https://github.com/paritytech/parity
https://github.com/Atrides/eth-proxy
https://launchpad.net/~ethereum/+archive/ubuntu/ethereum


