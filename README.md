# TinyML_GestureRecognition_Esp32
Inteligência artificial na borda usando Edge Impulse, Esp32 e MPU6050.

# Descrição
Esse projeto é a implementação de um classificador de gestos usando um modelo de [deep learning](https://pt.wikipedia.org/wiki/Aprendizagem_profunda) e os dados do acelerômetro para classificar quatro gestos, idle, left_right, up_down e circle usando o [Edge Impulse](https://www.edgeimpulse.com/) para amostrar os dados, fazer a analise espectral(FFT e PSD) e criar o modelo. Os dados foram capturados usando a comunicação serial do ESP32 e o recurso [data forwarder](https://docs.edgeimpulse.com/docs/cli-data-forwarder) da CLI do Edge Impulse.
