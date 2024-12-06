# Triplane-Gaussian Splatting (TGS)

## 🚀 **Introdução**
A reconstrução 3D a partir de imagens é uma área de pesquisa em rápido desenvolvimento, impulsionada pelos avanços em modelos generativos. O projeto **Triplane-Gaussian Splatting (TGS)** propõe uma abordagem inovadora para reconstrução 3D a partir de uma única imagem. Este método utiliza uma representação híbrida **Triplane-Gaussian**, que combina rapidez e qualidade de renderização, superando limitações de técnicas anteriores, como o **Score Distillation Sampling (SDS)** e modelos de difusão.

---

## ✨ **Resumo**
O **TGS** é baseado em duas redes transformadoras: 
- Um **Decodificador de Nuvem de Pontos**.
- Um **Decodificador Triplane**.

Essas redes geram representações 3D híbridas a partir de tokens de recursos extraídos de imagens 2D e parâmetros de câmera.  
A combinação das saídas das redes, por meio de um **Codificador Gaussiano**, permite a renderização eficiente de visualizações 3D detalhadas.

> **Resultados**: Testes realizados com datasets sintéticos e imagens reais demonstram que o **TGS** alcança maior qualidade e menor tempo de execução em comparação com técnicas de estado da arte.

---

## 🛠️ **Metodologia**
### **Fluxo Geral**
1. **Entrada**:  
   - Imagem 2D e parâmetros de câmera.  
   - A imagem é processada por um **Vision Transformer (ViT)**, gerando tokens latentes.

2. **Decodificadores 3D**:  
   - **Decodificador de Nuvem de Pontos**:  
     - Gera uma nuvem de pontos inicial, densificada com a técnica de **Projection-Aware Condition (P.C.)**.
   - **Decodificador Triplane**:  
     - Cria três planos estruturais (x, y, z), refinados com **Encoding Geometry-Aware (G.E.)**.

3. **Representação Híbrida**:  
   - Combinação da nuvem de pontos com os planos para formar a **Triplane-Gaussian Representation**, otimizando qualidade e velocidade.

4. **Renderização Final**:  
   - Os **Gaussians 3D** são usados para gerar visualizações detalhadas e realistas.

---

## 📊 **Resultados**
### **Qualitativos**  
- **Dataset Google Scanned Objects (GSO)**:  
  Superioridade do **TGS** em relação a métodos como **Zero-1-2-3** e **One-2-3-45**, na precisão geométrica e textural.

### **Quantitativos**  
- **Tempo de Execução**:  
  Redução significativa em comparação a métodos baseados em otimização iterativa, como o **NeRF**, mantendo qualidade visual elevada.

### **Experimentos de Ablation**
- Comparação de Representações 3D:  
  - Gaussian, Triplane-NeRF e Triplane-Gaussian.  
- Avaliação de Componentes:
  - Impacto das técnicas **P.C.** e **G.E.** na densificação e alinhamento geométrico.

---

## 🧩 **Como Utilizar**
Baixe o modelo **model_lvis_rel.ckpt** diretamente do repositório no Hugging Face ou integre-o em seus scripts Python:

```python
from huggingface_hub import hf_hub_download
MODEL_CKPT_PATH = hf_hub_download(
    repo_id="VAST-AI/TriplaneGaussian",
    filename="model_lvis_rel.ckpt",
    repo_type="model"
)

