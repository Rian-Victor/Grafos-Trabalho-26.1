# Análise de Grafos – ArXiv HEP-TH Citation Network

Trabalho prático de análise de grafos usando o dataset **cit-HepTh** (Stanford SNAP), uma rede de citações de artigos de física de alta energia publicados no ArXiv entre janeiro de 1993 e abril de 2003.

---

## 📊 Sobre o Dataset

| Propriedade | Valor |
|---|---|
| Fonte | [Stanford SNAP – cit-HepTh](https://snap.stanford.edu/data/cit-HepTh.html) |
| Tipo | Grafo dirigido (rede de citações) |
| Nós (artigos) | 27.400 |
| Arestas (citações) | 352.504 |
| Período | Jan/1993 – Abr/2003 |

---

## 📁 Estrutura do Repositório

```
.
├── cit_HepTh_analise.ipynb   # Notebook principal com toda a análise
├── data/                     # Arquivos do dataset (gerado automaticamente)
│   ├── cit-HepTh.txt.gz
│   └── cit-HepTh-dates.txt.gz
├── distribuicao_graus.png    # Distribuição de graus (histograma + log-log)
├── evolucao_temporal.png     # Evolução do número de artigos por ano
├── lei_potencia.png          # Ajuste de lei de potência (γ ≈ 1.77)
├── visualizacao_grafo.png    # Visualização de amostra de 300 nós
├── tabela_metricas_parte1.csv
├── tabela_algoritmos_parte2.csv
└── README.md
```

---

## ⚙️ Requisitos

- Python 3.8+
- Jupyter Notebook ou JupyterLab

### Bibliotecas Python

Instale todas as dependências com:

```bash
pip install networkx matplotlib numpy pandas scipy tqdm
```

Ou, se preferir usar um arquivo de requirements:

```bash
pip install -r requirements.txt
```

<details>
<summary>Conteúdo do requirements.txt</summary>

```
networkx
matplotlib
numpy
pandas
scipy
tqdm
```

</details>

---

## 🚀 Como Executar

### 1. Clone o repositório

```bash
git clone https://github.com/<seu-usuario>/<nome-do-repo>.git
cd <nome-do-repo>
```

### 2. (Opcional) Crie um ambiente virtual

```bash
python -m venv venv
source venv/bin/activate        # Linux/macOS
venv\Scripts\activate           # Windows
```

### 3. Instale as dependências

```bash
pip install networkx matplotlib numpy pandas scipy tqdm
```

### 4. Abra o notebook

```bash
jupyter notebook cit_HepTh_analise.ipynb
```

### 5. Execute as células em ordem

O próprio notebook faz o download automático do dataset na **Seção 1**. Não é necessário baixar nenhum arquivo manualmente — basta ter conexão com a internet na primeira execução.

> ⚠️ **Atenção:** Alguns algoritmos (especialmente Floyd-Warshall e verificação de Eulerianidade) são computacionalmente pesados e foram executados sobre subgrafos amostrados. O tempo total de execução completa do notebook pode levar de **15 a 30 minutos** dependendo da máquina.

---

## 🔬 O que o Notebook Analisa

### Tratamento dos Dados
- Leitura do grafo dirigido bruto
- Remoção de auto-loops
- Remoção de arestas duplicadas (multigrafo → grafo simples)
- Extração da maior componente fracamente conexa (WCC)

### Parte I – Análise Estrutural

| Métrica | Valor |
|---|---|
| Grau mínimo | 1 |
| Grau máximo | 2.468 |
| Grau médio | 25.69 |
| Densidade | 0,00047 |
| Número de WCCs | 1 |
| Número de SCCs | 19.716 |
| Tamanho da maior SCC | 7.464 nós |
| Diâmetro estimado | 31 |
| Raio estimado | 5 |
| Comprimento médio dos caminhos | 9,76 |
| Coeficiente de clusterização médio | 0,314 |
| Número de triângulos | 1.478.698 |

### Parte II – Algoritmos Implementados

| Algoritmo | Complexidade | Tempo médio |
|---|---|---|
| BFS | O(V+E) | 57,1 ms |
| DFS | O(V+E) | 37,8 ms |
| Verificação de Eulerianidade | O(V+E) | 1.481 ms |
| Dijkstra | O((V+E) log V) | 89,2 ms |
| Bellman-Ford* | O(V·E) | 148,7 ms |
| Floyd-Warshall** | O(V³) | 14.771,9 ms |
| Tarjan (SCCs) | O(V+E) | 234 ms |
| Prim (MST) | O(E log V) | 1.358,9 ms |
| Kruskal (MST) | O(E log E) | 1.331,2 ms |

\* Executado em subgrafo amostrado  
\** Executado em subgrafo pequeno (alta complexidade)

### Análises Adicionais
- Distribuição de graus com ajuste de lei de potência (γ ≈ 1,77)
- Análise de propriedade de mundo pequeno (*small-world*)
- Evolução temporal do número de artigos publicados por ano
- Análise de robustez da rede

---

## 📈 Principais Resultados

A rede cit-HepTh exibe características típicas de **redes livres de escala**:

- A distribuição de graus segue uma lei de potência com expoente **γ ≈ 1,77**, indicando a presença de hubs (artigos altamente citados).
- O coeficiente de clusterização médio alto (**0,314**) combinado com o comprimento médio de caminhos curto (**9,76**) confirma a propriedade de **mundo pequeno**.
- A maior componente fortemente conexa abrange apenas **~27%** dos nós, refletindo a natureza temporal das citações (artigos mais antigos tendem a ser mais citados, mas não necessariamente citam os mais recentes).

---

## 📄 Referências

- J. Leskovec, J. Kleinberg and C. Faloutsos. *Graph Evolution: Densification and Shrinking Diameters*. ACM TKDD, 2007.
- Stanford SNAP Dataset: https://snap.stanford.edu/data/cit-HepTh.html
- NetworkX Documentation: https://networkx.org/documentation/