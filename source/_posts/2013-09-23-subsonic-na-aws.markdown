---
layout: post
title: "Subsonic na AWS"
date: 2013-09-23 01:51
comments: true
categories: [Cloud, AWS, Song, Spotify, Rdio, Private cloud, S3, EC2]
Author: Diogo K.
publish: false
---

Recentemente conheci o Subsonic, um servidor de streaming de mídia. Ele faz streaming de audio e video também.

Ele possui uma versão **Premium** que pagando U$1,00 por mês (ou U$12,00 por ano) ele libera algumas features, sendo a melhor que eu vi é a possibilidade de utilizar players _mobiles_... 

Montei um no meu servidor em casa, entretanto apesar do meu plano de internet ser de 20Mb, meu upload é sofrível. Pensava em fazer um serviço tipo [Spotify](http://www.spotify.com) ou [Rdio](http://www.rdio.com) particular, mas esse meu upload me deixava _buffering_ demais nos meus apps no celular... 

Aí desencanei... 

Eis que tive uma idéia... será que ficaria legal usar uma instância EC2 na Amazon, e colocar as mp3 em um bucket no S3? 
Pensei: Poxa, mas uma EC2 e S3 no Data Center aqui de São Paulo ficaria caro... surgi com uma hipótese - EC2 em SP e um bucket S3 no Data center mais barato, dos EUA? Será que isso seria suficiente? 

Vantagens reais:

1. Não existe cobrança na "intranet" da Amazon, portanto independente de eu criar uma instância EC2 em SP e um Bucket S3 na Ásia, o único problema é a transferência da mp3 para minha EC2 e então o streaming para onde quer que eu esteja. 
1. S3 é mais barato que EBS. 
1. EC2 eu posso deixar _on-demand_.
1. Posso escutar minhas músicas (e ver vídeos também, por que não?) em qualquer lugar do mundo, _backed up_ pela infra da AWS.

Vantagens hipotéticas:

1. A conexão da "intranet" da Amazon é através de backbones super rápidos... ou seja, a latência de objetos na S3 independente de onde estiver deve ser razoável.
1. A "última milha" é entre a EC2 e qualquer dispositivo onde eu estiver escutando a música.
1. O custo pode ser variável, pois posso deixar desligado quando não estiver escutando.

* EC2 Ubuntu 12.04
* sudo apt-get update
* sudo apt-get install openjdk-6-jre
* [Download](http://www.subsonic.org/pages/download.jsp) the Subsonic .deb package and install it: sudo dpkg -i subsonic-x.x.deb
* Criar usuario subsonic: sudo adduser subsonic
* Editar o arquivo de conf do subsonic pra rodar com o novo usuario: sudo vim /etc/default/subsonic
* sudo service subsonic restart 
* Acessar o seu EC2 com a porta 4040 via browser, deve estar funcionando já.

https://code.google.com/p/s3fs/wiki/InstallationNotes
$ sudo apt-get install build-essential libfuse-dev fuse-utils libcurl4-openssl-dev libxml2-dev mime-support

RioFS
```
sudo apt-get install build-essential gcc make automake autoconf libtool pkg-config intltool\
                     libglib2.0-dev libfuse-dev libxml2-dev libevent-dev libssl-dev
``

sudo aptitude update
sudo aptitude install transmission-cli transmission-daemon

