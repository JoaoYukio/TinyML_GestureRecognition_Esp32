# TinyML_GestureRecognition_Esp32
Inteligência artificial na borda usando Edge Impulse, Esp32 e MPU6050.

# Descrição
Esse projeto é a implementação de um classificador de gestos usando um modelo de [deep learning](https://pt.wikipedia.org/wiki/Aprendizagem_profunda) e os dados do acelerômetro para classificar quatro gestos, idle, left_right, up_down e circle usando o [Edge Impulse](https://www.edgeimpulse.com/) para amostrar os dados, fazer a analise espectral(FFT e PSD) e criar o modelo. Os dados foram capturados usando a comunicação serial do ESP32 e o recurso [data forwarder](https://docs.edgeimpulse.com/docs/cli-data-forwarder) da CLI do Edge Impulse. O projeto feito no Edge Impulse pode ser acessado [aqui](https://studio.edgeimpulse.com/public/36985/latest).

<p align="center">
  <img src="https://github.com/JoaoYukio/TinyML_GestureRecognition_Esp32/blob/main/Fotos/IMG_20210622_203240944.jpg" height ="500" width ="450">
  
# Criação do Impulso
Um impulso no Edge Impulse é o conjunto do processo de aquisição, processamento e criação da rede neural de um sinal.
  ![image](https://user-images.githubusercontent.com/74123993/124301829-bf5a1180-db36-11eb-9f21-db2fc0507320.png)

  
## Data acquisition
Os dados foram coletados usando o acelerômetro do MPU6050, foram coletadas 4 classes com 4 amostras de 10 segundos de duração em cada classe.
  ![image](https://user-images.githubusercontent.com/74123993/124302048-06480700-db37-11eb-8f15-8c2570cc201d.png)

Podemos observar quais foram os dados adquiridos pela serial do computador para a classe 'circle'.
 
## Spectral Features
Os dados adquiridos no domínio do tempo são filtrados com um filtro passa-baixas e analisados usando a FFT para analisar uma janela do movimento no domínio da frequência e o PSD mede a densidade de energia nesse intervalo, essas características do dado que vão ser a "entrada" da nossa rede neural.
  ![image](https://user-images.githubusercontent.com/74123993/124302611-d1887f80-db37-11eb-95fe-1a28a05af3d0.png)
  ![image](https://user-images.githubusercontent.com/74123993/124302666-e1a05f00-db37-11eb-9cfe-26490d4bf38e.png)

## Neural Network
A rede neural usada é composta por duas camadas densas com 20 neurons na primeira e 10 na segunda:
  ![image](https://user-images.githubusercontent.com/74123993/124302944-3348e980-db38-11eb-808f-2e89b9c3504b.png)
  
Dados de validação:    
  ![image](https://user-images.githubusercontent.com/74123993/124302979-422f9c00-db38-11eb-9191-2b8ab1d773ac.png)

Com isso podemos usar o [TensorFlow Lite Micro](https://www.tensorflow.org/lite/microcontrollers?hl=pt-br) e o Edge Impulse para converter nosso modelo em um arquivo com formato Hexa e o EI em conjunto com o tensorFlow lite transforma isso em uma biblioteca para a IDE do Arduino.

#Inferência
O código usado está disponível e a saída é apresentada na serial da seguinte forma:
  ## Idle
  
  <img src="https://github.com/JoaoYukio/TinyML_GestureRecognition_Esp32/blob/main/Fotos/image.png" height ="300" width ="800">
  
  ## Left_right
  
  <img src="https://github.com/JoaoYukio/TinyML_GestureRecognition_Esp32/blob/main/Fotos/image%20(1).png" height ="300" width ="800">
  
  ## Up_down
  
  <img src="https://github.com/JoaoYukio/TinyML_GestureRecognition_Esp32/blob/main/Fotos/image%20(2).png" height ="300" width ="800">

  ## Circle 
  
  <img src="https://github.com/JoaoYukio/TinyML_GestureRecognition_Esp32/blob/main/Fotos/image%20(3).png" height ="300" width ="800">
  
# Conclusão
  Foi possível implementar um exemplo simples de TinyML usando um MCU barato e um sensor simples, de forma rápida e descomplicada usando o Edge Impulse, esse mesmo conceito pode ser extendido para identificação de anomalias em motores elétros à KWS para controlar dispositivos com voz.
