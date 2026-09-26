# Classificação de Hemorragia Intracraniana via Aprendizado de Máquina Clássico

**Projeto Prático 1 (TP1) — Equipe G1**  
*Desafio RSNA 2019 Intracranial Hemorrhage Detection*

Este repositório contém o código, experimentos e documentação para a detecção automática de hemorragia intracraniana em exames de Tomografia Computadorizada (TC) no formato DICOM, utilizando descritores de características tradicionais e classificadores de Aprendizado de Máquina.

---

## 📌 Visão Geral do Pipeline

1. **Pré-processamento & Janelamento:** Aplicação de janela de cérebro (*Brain Window*: $WC=40, WW=80$) sobre os dados brutos de TC para realce de contraste do tecido cerebral e sangue.
2. **Particionamento sem Vazamento:** Amostragem e divisão congelada por paciente (*StratifiedGroupKFold*) para evitar contaminação (*data leakage*) entre conjuntos de treino e teste.
3. **Extração de Características:**
   - **LBP** (*Local Binary Patterns*): Textura local.
   - **HOG** (*Histogram of Oriented Gradients*): Gradientes de borda e forma.
   - **Hu Moments**: Momentos invariantes de forma global.
4. **Classificação & Validação:** Comparativo empírico entre *SVM (RBF)*, *Random Forest* e *k-Nearest Neighbors (kNN)* ajustados via *GridSearchCV*.

---

## 📊 Principais Resultados

| Descritor | Modelo | Acurácia Balanceada | F1-Score | AUC-ROC | AUC-PR |
| :--- | :--- | :---: | :---: | :---: | :---: |
| *Baseline Trivial* | DummyClassifier | 0.5000 | 0.6463 | 0.5000 | — |
| Hu Moments | SVM (RBF) | 0.5817 | 0.6351 | 0.6227 | 0.5722 |
| LBP | SVM (RBF) | 0.6600 | 0.6905 | 0.7097 | 0.6398 |
| HOG | kNN | 0.6594 | 0.6565 | 0.6867 | 0.6334 |
| HOG | SVM (RBF) | 0.7001 | 0.7000 | 0.7298 | 0.6502 |
| **HOG** | **Random Forest** | **0.7207** | **0.7227** | **0.7572** | **0.6959** |

---

## 🚀 Como Reproduzir o Experimento

O pipeline foi projetado para rodar no ambiente de nuvem do **Kaggle Notebooks** para acesso nativo ao dataset sem necessidade de download local dos arquivos DICOM.

### Passos:
1. Abra um novo notebook no Kaggle.
2. Adicione o dataset da competição **RSNA Intracranial Hemorrhage Detection** via painel lateral (*Add Input*).
3. Importe ou copie o código contido no notebook `.ipynb` deste repositório.
4. Instale as dependências com:
   ```bash
   pip install -r requirements.txt
