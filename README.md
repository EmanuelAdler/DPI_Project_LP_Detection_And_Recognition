# Detecção de placas

## Passo 1

### Buildar o Darknet Framework

Link para o reposistório: https://github.com/pjreddie/darknet.

Basta seguir o tutorial do repositório e estará configurado.

### Carregar configurações e pesos

Ir até a pasta do Darknet e executar os comandos no terminal (dentro da pasta):

wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/fvlpd-net.weights

wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/fvlpd-net.cfg

wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/fvlpd-names.txt

wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/fvlpd.data

wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/lpscr-net.weights

wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/lpscr-net.cfg

wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/lpscr-names.txt

wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/lpscr.data

wget http://inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/data/sample_image.jpg

## Passo 2

### Baixar imagens de exemplo disponibilizadas

Links:
http://www.inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/imgs/sample_image.jpg

http://www.inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/imgs/frontal_view_car2.jpg

http://www.inf.ufrgs.br/~smsilva/real-time-brazilian-alpr/imgs/lp_car2.jpg

### Executar comandos para processamento das imagens

Encontrando a frente do carro: ./darknet detector test fvlpd.data fvlpd-net.cfg fvlpd-net.weights -thresh .4 <<< "sample_image.jpg"

Encontrando a placa: ./darknet detector test fvlpd.data fvlpd-net.cfg fvlpd-net.weights -thresh .2 <<< "frontal_view_car2.jpg"

Pegando a placa em grayscale: convert lp_car2.jpg -colorspace Gray lp_car2_gray.jpg

Detectando caracteres: ./darknet detector test lpscr.data lpscr-net.cfg lpscr-net.weights -thresh .6 <<< "lp_car2_gray.jpg"

## Melhoria a ser feita:

Criar uma etapa de pós processamento com o ituito de melhorar a detecção de caracteres e evitar erros.
