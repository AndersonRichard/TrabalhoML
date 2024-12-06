# 🖼️ **Triplane-Gaussian Splatting (TGS)**  

### 🚀 **Uma Nova Abordagem para Reconstrução 3D a Partir de Imagens**

O **Triplane-Gaussian Splatting (TGS)** é um método inovador que promete revolucionar a reconstrução 3D a partir de imagens 2D. Utilizando um sistema baseado em **transformadores** e uma representação híbrida chamada **Triplane-Gaussian**, ele oferece alta qualidade visual e rapidez incomparável. 

---


## 🖥️ **Introdução**
A reconstrução 3D de objetos ou cenas a partir de uma única imagem é um desafio significativo em **Visão Computacional**. Embora avanços recentes tenham sido feitos com modelos como **Score Distillation Sampling (SDS)** e técnicas de difusão, essas abordagens frequentemente sofrem com processos de otimização lentos e dependentes de renderização iterativa.  

O **TGS** resolve esses problemas utilizando duas redes transformadoras que trabalham juntas:  
1. **Decodificador de Nuvem de Pontos**: Cria uma representação inicial dos objetos em 3D.  
2. **Decodificador Triplane**: Refina a geometria do objeto com uma estrutura tridimensional mais detalhada.  

O resultado é um modelo híbrido que combina velocidade de processamento e qualidade visual, ideal para aplicações em tempo real.  

---

## 📘 **Resumo Técnico**
O **TGS** utiliza uma **representação híbrida Triplane-Gaussian** para reconstruir objetos tridimensionais.  
- **Triplane**: são uma forma de representação explícita de objetos 3D que utiliza três planos ortogonais (XY, XZ e YZ) para armazenar informações espaciais, como densidade ou cor.
- **Gaussian**: é uma técnica mais recente e implícita, que representa uma cena ou objeto como uma coleção de distribuições gaussianas posicionadas em 3D. Essas distribuições são usadas para renderizar diretamente imagens e reconstruir a geometria.

### Principais Características
- **Eficiência**: Reconstrução direta via inferência (feed-forward).  
- **Rapidez**: Elimina otimizações iterativas, reduzindo o tempo de processamento.  
- **Generalização**: Treinado em datasets sintéticos e adaptável a imagens reais.  

---

## 🛠️ **Metodologia**

### 🔄 **Fluxo de Trabalho**
1. **Entrada**:  
   - Imagem 2D e parâmetros da câmera.  
   - A imagem é processada por um **Vision Transformer (ViT)**, extraindo tokens de recursos latentes.  

2. **Decodificação**:  
   - **Nuvem de Pontos**:  
     - Reconstrói pontos 3D com **Projection-Aware Condition (P.C.)** para densificação.  
   - **Triplane**:  
     - Gera três planos (x, y, z) com auxílio de **Geometry-Aware Encoding (G.E.)**.  

3. **Representação Híbrida**:  
   - Combina os resultados da Nuvem de Pontos e do Triplane para formar a **Triplane-Gaussian Representation**.  

4. **Renderização**:  
   - Usa um **Gaussian Decoder** para criar visualizações 3D de alta qualidade.  

### 📊 **Comparação de Desempenho**
- Redução significativa do tempo de processamento em relação a métodos como **NeRF**.  
- Qualidade visual comparável ou superior, adaptando-se tanto a objetos sintéticos quanto reais.  

---

## 📈 **Resultados**

### **Comparações Qualitativas e Quantitativas**
- **Dataset GSO (Google Scanned Objects)**:  
  O TGS supera modelos como **Zero-1-2-3** e **One-2-3-45**, especialmente em detalhes geométricos e texturais.  

### **Estudos de Ablation**
- **Representações Testadas**:  
  - Gaussian, Triplane-NeRF, e Triplane-Gaussian.  
  - Melhor equilíbrio entre qualidade e velocidade foi alcançado com Triplane-Gaussian.  

- **Impacto de Componentes-Chave**:  
  - **Projection-Aware Condition (P.C.)**: Aumenta a densidade e precisão da nuvem de pontos.  
  - **Geometry-Aware Encoding (G.E.)**: Refina a integração entre nuvem de pontos e planos.  

---

## 🛠️ **Como Usar**

### **Requisitos**
- **Linguagem**: Python 3.8 ou superior.  
- **Bibliotecas Necessárias**:  
  - huggingface_hub  
  - pytorch  
  - numpy  
  - matplotlib  

### **Instalação e Execução**

1. Clone este repositório:  
   ```bash
   git clone https://github.com/VAST-AI/TriplaneGaussian.git
   cd TriplaneGaussian

2. Instale as dependências:
   pip install -r requirements.txt

3. Baixe o modelo:
   from huggingface_hub import hf_hub_download
   MODEL_CKPT_PATH = hf_hub_download(
    repo_id="VAST-AI/TriplaneGaussian",
    filename="model_lvis_rel.ckpt",
    repo_type="model"
   )
   
5. Execute o exemplo de reconstrução:
   python demo.py --input_image example.jpg --camera_params params.json

🔗 Links Úteis

* Página do Projeto
* Artigo no ArXiv
* Código Fonte

👥 Autores e Colaborações
Este trabalho foi desenvolvido por:

* Zi-Xin Zou
* Zhipeng Yu
* Yuan-Chen Guo
* Yangguang Li
* Ding Liang
* Yan-Pei Cao
* Song-Hai Zhang
