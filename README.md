# GenJigsawLab 🧩🧠
**Montagem automática de quebra-cabeças com IA Generativa (VAE, GAN e Difusão)**

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)]()
[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-ee4c2c.svg)]()
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-f37626.svg)]()
[![License](https://img.shields.io/badge/License-MIT-green.svg)]()

> Projeto de pós-graduação em Aprendizado de Máquina e IA focado em reconstrução de imagens a partir de peças embaralhadas, combinando representações latentes e modelos generativos para melhorar a montagem.

---

## 👥 Membros do Grupo

- Gabriel Moscatel Fevrier  
- Pedro Henrique Alves dos Santos  
- Samuel Fernando Tavela Julio  
- Tuerê Pinto  

---

## 📌 Visão Geral

O **GenJigsawLab** investiga como redes neurais generativas podem apoiar a solução automática de quebra-cabeças visuais.  
A proposta central é modelar cada peça como uma unidade informacional (análoga a um “pixel semântico”), aprender relações locais entre peças e usar um prior global de imagem para orientar a montagem final.

### Objetivo principal
Reconstruir a imagem original a partir de peças embaralhadas (com e sem rotação), maximizando fidelidade visual e consistência estrutural.

---

## 🧩 Definição do Problema

### 1) Contexto do problema (onde ele acontece)
A montagem automática de quebra-cabeças aparece em cenários de visão computacional e reconstrução visual, como:
- organização de fragmentos digitais de imagem;
- restauração parcial de conteúdo visual danificado;
- tarefas acadêmicas de raciocínio espacial e inferência estrutural;
- benchmark de métodos que combinam percepção local e coerência global.

### 2) Quem é afetado pelo problema
- Pesquisadores e estudantes de IA/Visão Computacional que precisam de benchmarks controláveis e reprodutíveis;
- equipes que trabalham com reconstrução de imagem e composição de fragmentos;
- usuários finais de aplicações educacionais/analíticas que dependem de reconstruções consistentes.

### 3) Impacto do problema (o que acontece hoje sem solução)
Sem uma abordagem robusta:
- métodos locais erram em regiões ambíguas (céu, água, grama, texturas repetidas);
- a taxa de erro cresce com rotação, ruído e peças faltantes;
- há descontinuidade visual entre peças, reduzindo qualidade da imagem final;
- soluções ficam pouco generalizáveis e difíceis de reproduzir em novos cenários.

### 4) Por que esse problema é relevante para o trabalho final
Este problema é relevante porque integra, de forma prática, os principais temas da disciplina:
- modelagem generativa e espaços latentes (VAE);
- prior global com GAN/difusão;
- avaliação quantitativa com métricas de qualidade;
- interpretabilidade e análise de falhas;
- engenharia de experimentos reprodutíveis.

---

## 🚀 Solução Proposta

### 1) Ideia central da solução
Construir um pipeline híbrido com três camadas:
1. **Compatibilidade local (discriminativa):** aprende quem pode ser vizinho de quem e orientação relativa;
2. **Regularização global (generativa):** usa modelo pré-treinado para reforçar coerência da cena completa;
3. **Otimização combinatória:** posiciona e rotaciona peças maximizando compatibilidade local + consistência global.

### 2) Técnica principal
**Inpainting guiado (img2img/inpainting)** para refinar regiões ambíguas após uma montagem inicial.

Motivação:
- o quebra-cabeça já oferece conteúdo parcial;
- inpainting é adequado para completar lacunas e suavizar transições de borda;
- integração prática com ecossistema `diffusers`.

### 3) Modelo base pretendido (Hugging Face)
- **`runwayml/stable-diffusion-inpainting`**

Uso planejado:
- **entrada:** montagem parcial + máscara de incerteza;
- **saída:** hipótese visual global para orientar refinamento do arranjo final.

### 4) Resultado esperado para o usuário final
- reconstrução automática mais estável da imagem;
- ganho de acurácia em posição/rotação versus baseline sem prior generativo;
- menos artefatos de borda e melhor coerência visual global;
- relatório final com métricas objetivas de desempenho.

---

## 🎯 Objetivos do Projeto

- Aprender embeddings de peças com **VAE / β-VAE**;
- Estimar compatibilidade entre peças adjacentes e orientação relativa;
- Incorporar prior global com **GAN** ou **modelo de difusão**;
- Resolver posição/rotação via otimização combinatória;
- Avaliar qualidade com métricas de puzzle + métricas generativas;
- Produzir análise de interpretabilidade no espaço latente.

---

## 🧪 Metodologia (Pipeline)

1. **Geração de dataset sintético**
   - recorte de imagens em grade |$N \times N$|;
   - embaralhamento de posições e rotações;
   - armazenamento de ground truth de posição/rotação.

2. **Codificação latente por peça (VAE)**
   - encoder/decoder para representação compacta;
   - regularização KL (com annealing).

3. **Compatibilidade local**
   - modelo discriminativo (siamês/transformer) para prever vizinhança.

4. **Prior global de imagem**
   - GAN condicional ou difusão para hipótese da cena completa.

5. **Montagem**
   - busca/otimização de posição e rotação (Hungarian/ILP/Beam/Guloso + refinamento).

6. **Avaliação**
   - métricas de puzzle + métricas de qualidade de imagem.

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

Stack-alvo do projeto: **Python 3.10+**, **PyTorch 2.x**, **Jupyter Notebook**, licença **MIT**.<sources>[1]</sources>

Bibliotecas planejadas:
- PyTorch / TorchVision
- NumPy / Pandas
- OpenCV / Pillow
- Matplotlib / Seaborn
- Scikit-learn
- (Opcional) Hugging Face Diffusers

---

## 📂 Estrutura do Repositório

```text
genjigsawlab/
├─ README.md
├─ LICENSE
├─ .gitignore
├─ pyproject.toml
├─ uv.lock
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

## 🚀 Como Executar (com `uv`)

### 1) Clonar repositório
```bash
git clone <repo_git_url>
cd genjigsawlab
```

### 2) Criar ambiente e instalar dependências
```bash
uv sync
```

### 3) Executar notebooks
```bash
uv run jupyter lab
```

---

## ▶️ Quickstart

1. Execute `notebooks/01_dataset_generation.ipynb` para criar puzzles;
2. Treine o VAE em `02_vae_training.ipynb`;
3. Treine baseline de compatibilidade em `03_compatibility_baseline.ipynb`;
4. Integre prior global em `04_global_prior_diffusion.ipynb`;
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

## 🧠 Interpretabilidade

- Visualização de latentes (UMAP/t-SNE);
- Interpolação no espaço latente de peças;
- Heatmaps de compatibilidade;
- Análise de erro por classe visual (textura baixa vs alta).

---

## ♻️ Reprodutibilidade

- Seeds fixas para treino/validação/teste;
- Configurações centralizadas em `configs/*.yaml`;
- Logs de treino e checkpoints em `results/`;
- Versionamento de experimentos por commit/tag.

---

## 🤝 Contribuição

1. Fork do projeto  
2. Criar branch: `feature/minha-feature`  
3. Commit: `feat: descrição da melhoria`  
4. Push da branch  
5. Abrir Pull Request

Padrão de commits sugerido: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`.

---

## 👨‍🎓 Contexto Acadêmico

Projeto desenvolvido na disciplina de **Redes Neurais Generativas**, cobrindo:
- modelos latentes (VAE),
- modelos adversariais/difusão,
- regularização e estabilidade,
- métricas de avaliação,
- interpretabilidade e análise de desempenho.

---

## 📜 Licença

Este projeto está licenciado sob a **MIT License**.  
Consulte o arquivo `LICENSE` na raiz do repositório.

---

## ⭐ Status

Em desenvolvimento ativo.  
Objetivo: entregar uma pipeline robusta, reprodutível e publicável para montagem de quebra-cabeças com IA generativa.