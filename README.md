# ibmec_computer_vision
# Análise de Bordas em Imagem com Filtros Sobel e Canny

![Python](https://img.shields.io/badge/python-3.8-blue.svg)
![OpenCV](https://img.shields.io/badge/OpenCV-4.5.1-red)
![License](https://img.shields.io/badge/license-MIT-green)

## 📜 Autores
- Ian Amoedo
- Maria Mello
- Larissa Nobrega
- Carolina Cruz
- Fernanda Moyses
- Bruno Pilão
- Giovanna Amaral

---

## 🚀 Resumo

Neste trabalho, foi proposto um estudo sobre a **detecção de bordas** em imagens utilizando filtros clássicos da Visão Computacional. Os filtros **Sobel** e **Canny** foram aplicados sobre uma imagem de uma bola de futebol, após uma etapa de suavização com **filtro Gaussiano**. A análise comparativa entre os métodos permitiu observar diferenças na precisão das bordas extraídas, contribuindo para o entendimento das características de cada abordagem.

---

## 🛠️ Descrição do Sistema

O sistema desenvolvido possui a seguinte funcionalidade:

- **Entrada**: Imagem em tons de cinza.
- **Saída**: Representação das bordas extraídas da imagem.

O problema abordado é identificar as bordas de uma imagem de forma eficaz, eliminando ruídos e mantendo as informações relevantes.

---

## 📈 Métodos Utilizados

### 🔹 Pré-processamento
1. **Escala de cinza**: A imagem foi convertida para tons de cinza.
2. **Filtro Gaussiano**: Aplicado para reduzir ruídos.

### 🔹 Filtros de Detecção de Bordas
1. **Sobel**: Aplicado nos eixos X e Y, seguido do cálculo da magnitude do gradiente.
   - O filtro Sobel detecta bordas em direções específicas (horizontal e vertical).
   
2. **Canny**: Utilizando limiares de 30 e 100, seguido de limiarização binária para destacar as bordas.
   - O Canny é conhecido pela sua precisão e remoção de ruídos.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Carregar imagem em tons de cinza
image = cv2.imread('imagem_futebol.jpg', cv2.IMREAD_GRAYSCALE)

# Aplicar filtro Gaussiano
blurred_image = cv2.GaussianBlur(image, (5, 5), 0)

# Detecção de bordas com Sobel
sobel_x = cv2.Sobel(blurred_image, cv2.CV_64F, 1, 0, ksize=3)
sobel_y = cv2.Sobel(blurred_image, cv2.CV_64F, 0, 1, ksize=3)
sobel_edges = np.hypot(sobel_x, sobel_y)

# Detecção de bordas com Canny
canny_edges = cv2.Canny(blurred_image, 30, 100)

# Exibir os resultados
plt.subplot(121), plt.imshow(sobel_edges, cmap='gray')
plt.title('Sobel Edges'), plt.xticks([]), plt.yticks([])
plt.subplot(122), plt.imshow(canny_edges, cmap='gray')
plt.title('Canny Edges'), plt.xticks([]), plt.yticks([])
plt.show()
