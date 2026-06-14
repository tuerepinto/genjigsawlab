# GenJigsawLab 🧩🧠
**Montagem automática de quebra-cabeças com IA Generativa (VAE, GAN e Difusão)**

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)]()
[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-ee4c2c.svg)]()
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-f37626.svg)]()
[![License](https://img.shields.io/badge/License-MIT-green.svg)]()

> Projeto de pós-graduação em Aprendizado de Máquina e IA focado em reconstrução de imagens a partir de peças embaralhadas, combinando **representações latentes** e **modelos generativos** para melhorar a montagem.

---

## 📌 Visão Geral

O **GenJigsawLab** investiga como redes neurais generativas podem ajudar na solução automática de quebra-cabeças visuais.  
A proposta central é modelar cada peça como uma unidade informacional (análoga a um “pixel semântico”), aprender relações locais entre peças e usar um prior global de imagem para orientar a montagem final.

### Objetivo principal
Reconstruir a imagem original a partir de peças embaralhadas (com e sem rotação), maximizando a fidelidade visual e a consistência estrutural.

---

## 🎯 Objetivos do Projeto

- Aprender embeddings de peças com **VAE / β-VAE**.
- Estimar compatibilidade entre peças adjacentes e orientação relativa.
- Incorporar prior global com **GAN** ou **modelo de difusão**.
- Resolver posição/rotação via otimização combinatória.
- Avaliar qualidade com métricas de puzzle + métricas generativas.
- Produzir análise de interpretabilidade no espaço latente.

---

## 🧪 Metodologia (Pipeline)

1. **Geração de dataset sintético**
   - Recorte de imagens em grade |$N \times N$|
   - Embaralhamento de posições e rotações
   - Ground truth de posição/rotação

2. **Codificação latente por peça (VAE)**
   - Encoder/Decoder para representação compacta
   - Regularização KL (com annealing)

3. **Compatibilidade local**
   - Modelo discriminativo (siamês/transformer) para prever vizinhança

4. **Prior global de imagem**
   - GAN condicional ou difusão para hipótese da cena completa

5. **Montagem**
   - Busca/otimização de posição e rotação (Hungarian/ILP/Beam/Guloso + refinamento)

6. **Avaliação**
   - Métricas de puzzle + métricas de qualidade de imagem

---

## 📏 Métricas

### Métricas de montagem
- **PPA** (Piece Placement Accuracy)
- **RA** (Rotation Accuracy)
- **NA** (Neighbor Accuracy)
- **ESR** (Exact Solve Rate)

### Métricas visuais/generativas
- **SSIM**
- **PSNR**
- **FID / KID**
- (Opcional) **Inception Score**

---

## 🧰 Tecnologias

- Python 3.10+
- PyTorch / TorchVision
- NumPy / Pandas
- OpenCV / Pillow
- Matplotlib / Seaborn
- Scikit-learn
- Jupyter Notebook
- (Opcional) Hugging Face Diffusers

---

## 📂 Estrutura do Repositório

```text
genjigsawlab/
├─ README.md
├─ .gitignore
├─ requirements.txt
├─ environment.yml
├─ src/
│  ├─ data/
│  ├─ models/
│  ├─ training/
│  ├─ evaluation/
│  └─ utils/
├─ notebooks/
│  ├─ 01_dataset_generation.ipynb
│  ├─ 02_vae_training.ipynb
│  ├─ 03_compatibility_baseline.ipynb
│  ├─ 04_global_prior_diffusion.ipynb
│  └─ 05_metrics_and_analysis.ipynb
├─ configs/
│  ├─ vae.yaml
│  ├─ solver.yaml
│  └─ diffusion.yaml
├─ data/
│  ├─ raw/
│  ├─ processed/
│  └─ splits/
└─ results/
   ├─ figures/
   ├─ checkpoints/
   └─ metrics/
```

---

## 🚀 Como Executar

### 1) Clonar repositório
```bash
git clone https://github.com/SEU_USUARIO/genjigsawlab.git
cd genjigsawlab
```

### 2) Criar ambiente virtual
```bash
python -m venv .venv
```

Ativação:

- Linux/macOS:
```bash
source .venv/bin/activate
```

- Windows (PowerShell):
```powershell
.venv\Scripts\Activate.ps1
```

### 3) Instalar dependências
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 4) Rodar notebooks
```bash
jupyter lab
```

---

## ▶️ Quickstart

1. Execute `notebooks/01_dataset_generation.ipynb` para criar puzzles.
2. Treine o VAE em `02_vae_training.ipynb`.
3. Treine baseline de compatibilidade em `03_compatibility_baseline.ipynb`.
4. Integre prior global em `04_global_prior_diffusion.ipynb`.
5. Avalie em `05_metrics_and_analysis.ipynb`.

---

## 🧭 Roadmap

- [x] Estrutura inicial do projeto
- [ ] Gerador de dataset |$N \times N$|
- [ ] Baseline de compatibilidade local
- [ ] VAE para embeddings de peças
- [ ] Solver com rotação
- [ ] Prior global com difusão
- [ ] Benchmark com ablação completa
- [ ] Relatório final e versão para artigo

---

## 🔬 Protocolo Experimental (resumo)

- **Cenário A (MVP):** peças quadradas, rotação discreta, imagens limpas.
- **Cenário B:** ruído, blur e iluminação variável.
- **Cenário C:** peças faltantes e ambiguidades semânticas (céu/água/grama).
- **Ablation:** sem VAE, com VAE, com/sem prior global, com/sem regularização.

---

## 🧠 Interpretabilidade

- Visualização de latentes (UMAP/t-SNE)
- Interpolação no espaço latente de peças
- Heatmaps de compatibilidade
- Análise de erro por classe visual (textura baixa vs alta)

---

## ♻️ Reprodutibilidade

- Seeds fixas para treino/validação/teste
- Configurações centralizadas em `configs/*.yaml`
- Logs de treino e checkpoints em `results/`
- Versionamento de experimentos por commit/tag

---

## 🤝 Contribuição

1. Fork do projeto  
2. Crie uma branch: `feature/minha-feature`  
3. Commit: `feat: descrição da melhoria`  
4. Push da branch  
5. Abra Pull Request

Padrão de commits (sugestão): `feat`, `fix`, `docs`, `refactor`, `test`, `chore`.

---

## 👨‍🎓 Contexto Acadêmico

Projeto desenvolvido no contexto de disciplina de **Redes Neurais Generativas**, cobrindo:
- modelos latentes (VAE),
- modelos adversariais/difusão,
- regularização e estabilidade,
- métricas de avaliação,
- interpretabilidade e análise de desempenho.

---

## 📜 Licença

Este projeto está sob licença **MIT**.  
[veja LICENSE.md](LICENSE.md).

---

## 📣 Citação (opcional)

Se usar este repositório em trabalhos acadêmicos:

```bibtex
@misc{genjigsawlab2026,
  title        = {GenJigsawLab: Automatic Jigsaw Puzzle Solving with Generative AI},
  author       = {Tuerê},
  year         = {2026},
  howpublished = {\url{https://github.com/SEU_USUARIO/genjigsawlab}}
}
```

---

## ⭐ Status

Em desenvolvimento ativo.  
Objetivo: entregar uma pipeline robusta, reprodutível e publicável para montagem de quebra-cabeças com IA generativa.