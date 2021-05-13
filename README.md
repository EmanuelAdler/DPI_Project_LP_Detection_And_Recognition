# Detecção e reconhecimento de placas veiculares

Este projeto é baseado no artigo "Real-Time Brazilian License Plate Detection and Recognition Using Deep Convolutional Neural Networks", de Sergio Montazzolli Silva e Claudio Rosito Jung, disponível em http://www.inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/.

O projeto utiliza a linguagem Python e o framework Darknet, implementação Open Source da rede neural YOLO. O objetivo deste trabalho é fazer uma melhoria no OCR utilizado para detecção dos caracteres presentes no antigo modelo brasileiro de placas de veículos, inserindo uma etapa de pós-processamento para minimizar eventuais erros.

## Instruções para rodar o projeto

### Passo 1: Instalar o framework Darknet

Link para o reposistório: https://github.com/pjreddie/darknet.

Basta seguir as instruções presentes no repositório para concluir a instalação.

### Passo 2: Fazer download dos arquivos de configuração e dos pesos da rede treinada

De dentro da pasta do Darknet, executar seguintes comandos no terminal:

```sh
$ wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/fvlpd-net.weights

$ wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/fvlpd-net.cfg

$ wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/fvlpd-names.txt

$ wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/fvlpd.data

$ wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/lpscr-net.weights

$ wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/lpscr-net.cfg

$ wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/lpscr-names.txt

$ wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/lpscr.data

$ wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/sample_image.jpg
```

### Passo 3: Baixar as imagens de exemplo disponibilizadas

```sh
$ wget http://www.inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/imgs/sample_image.jpg

$ wget http://www.inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/imgs/frontal_view_car2.jpg

$ wget http://www.inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/imgs/lp_car2.jpg
```

### Passo 4: Executar os comandos para detecção

Encontrando a frente do carro:

```sh
$ ./darknet detector test fvlpd.data fvlpd-net.cfg fvlpd-net.weights -thresh .4 <<< "sample_image.jpg"
```

Encontrando a placa:

```sh 
$ ./darknet detector test fvlpd.data fvlpd-net.cfg fvlpd-net.weights -thresh .2 <<< "frontal_view_car2.jpg"
```

Convertendo a placa para grayscale:

```sh 
$ convert lp_car2.jpg -colorspace Gray lp_car2_gray.jpg
```

Detectando caracteres da placa: 

```sh
$ ./darknet detector test lpscr.data lpscr-net.cfg lpscr-net.weights -thresh .6 <<< "lp_car2_gray.jpg"
```

## Status atual do trabalho:

Foi feita uma apresentação do projeto como descrito pelo artigo, bem como o objetivo deste trabalho, para a turma de Processamento de Imagens 2020.1. Sugestões foram feitas pelo professor. Técnicas de OCR estão sendo estudadas pela equipe no momento. 
