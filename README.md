# FATEC- Grafos e Rotas Ótimas para Transporte Público

## Matéria
- Processamento de Linguagem Natural

## Integrantes
- Gabriel Marcondes dos Santos
- Gustavo Ferreira Gonçalves Lima
- Gustavo Miranda da Silva Araújo
- Mariana Miyuki Suzuki Kobayashi
- Marcelo Sopa 

## Descrição do Projeto

Este projeto desenvolve um sistema de otimização de rotas para transporte público utilizando teoria dos grafos e algoritmos de caminho mínimo. O sistema calcula a rota ótima entre pontos de ônibus em São Paulo, considerando o tempo de viagem como critério de otimização.

## Objetivos

- **Objetivo Principal**: Implementar um sistema de roteamento eficiente para transporte público usando algoritmos de grafos
- **Objetivos Específicos**:
  - Construir um grafo da malha viária urbana usando dados do OpenStreetMap
  - Mapear pontos de ônibus para nós da rede viária
  - Aplicar o algoritmo de Dijkstra para encontrar rotas ótimas
  - Visualizar as rotas calculadas em mapas interativos

## Tecnologias Utilizadas

- **Python 3.11+**
- **OSMnx**: Para baixar e processar dados do OpenStreetMap
- **NetworkX**: Para implementação e manipulação de grafos
- **GeoPandas**: Para manipulação de dados geoespaciais
- **Folium**: Para visualização interativa de mapas
- **Jupyter Notebook**: Para desenvolvimento e apresentação

## Metodologia

### 1. Coleta e Preparação dos Dados
- **Fonte dos Dados**: 
   - Geosampa - https://geosampa.prefeitura.sp.gov.br/PaginasPublicas/_SBC.aspx#
   - Coletamos os dados dos pontos de São Paulo

- **Área de Estudo**: Região central de São Paulo (raio de 5km)
- **Pontos de Ônibus**: Dataset em formato GeoPackage com localização dos pontos

### 2. Construção do Grafo
```python
# Parâmetros utilizados
network_type='drive'    # Rede viária para veículos
dist=5000              # Raio de 5km do centro
simplify=False         # Mantém todos os nós para maior precisão
```

### 3. Modelagem dos Pesos
- **Critério de Otimização**: Tempo de viagem
- **Velocidade Média Assumida**: 20 km/h (típica para trânsito urbano)
- **Cálculo**: `tempo = distância / velocidade_média`

### 4. Algoritmo de Roteamento
- **Algoritmo**: Dijkstra (implementado via NetworkX)
- **Função Objetivo**: Minimizar tempo total de viagem
- **Entrada**: pt_id de origem e destino
- **Saída**: Sequência de nós representando a rota ótima

## Estrutura do Projeto

```
grafos-rotas-otimas-transporte/
├── main.ipynb                 # Notebook principal
├── pontos_onibus.gpkg        # Dataset dos pontos de ônibus
├── cache_graph.graphml       # Cache do grafo (gerado automaticamente)
├── cache_gdf.gpkg           # Cache dos pontos mapeados
├── cache/                   # Cache do OSMnx
└── README.md               # Este arquivo
```

## Como Executar

### Pré-requisitos
```bash
pip install osmnx geopandas networkx folium mapclassify
```

### Execução
1. **Preparação dos Dados**:
   - Execute as células de importação e visualização da base
   - O sistema carregará automaticamente os caches se existirem

2. **Listagem de Pontos Disponíveis**:
   - Execute a célula "Listando todos os pontos de ônibus nesse raio"
   - Anote os `pt_id` disponíveis para teste

3. **Cálculo de Rotas**:
   - Execute a célula "Testando o programa"
   - Insira o `pt_id` de origem e destino quando solicitado
   - O sistema exibirá o mapa com a rota calculada

### Exemplo de Uso
```
Digite o pt_id de origem: 80014567
Digite o pt_id de destino: 800016522
```

## Resultados e Visualização

O sistema gera:
- **Mapa Interativo**: Visualização da rota calculada
- **Marcadores**: Pontos de origem (verde) e destino (vermelho)
- **Rota**: Linha azul mostrando o caminho ótimo
- **Informações**: Distância total e tempo estimado de viagem

## Funcionalidades Implementadas

### Sistema de Cache
- **Cache do Grafo**: Evita redownload dos dados do OSM
- **Cache dos Mapeamentos**: Preserva o mapeamento pontos↔nós
- **Inicialização Rápida**: Carregamento em ~1 segundo após primeira execução

### Tratamento de Erros
- Validação de `pt_id` de entrada
- Detecção de rotas impossíveis
- Correção automática de tipos de dados
- Tratamento de casos especiais (origem = destino)

### Otimizações
- Projeção adequada de coordenadas para cálculos precisos
- Mapeamento eficiente de pontos para nós da rede
- Uso de grafos não-simplificados para maior precisão

## Limitações e Trabalhos Futuros

### Limitações Atuais
- Velocidade constante assumida (não considera trânsito real-time)
- Área limitada a 5km do centro de São Paulo
- Não considera integração entre modais de transporte

### Melhorias Futuras
- Integração com APIs de trânsito em tempo real
- Consideração de horários de pico
- Extensão para múltiplos modais (ônibus + metrô + trem)
- Interface web para uso público

## Aplicações Práticas

Este sistema pode ser aplicado em:
- **Planejamento de Transporte Público**: Otimização de rotas de ônibus
- **Aplicativos de Mobilidade**: Cálculo de melhores rotas para usuários
- **Estudos Urbanos**: Análise de acessibilidade e conectividade
- **Gestão Municipal**: Planejamento de infraestrutura de transporte

## Conclusão

O projeto demonstra com sucesso a aplicação de algoritmos de grafos para otimização de rotas em transporte público. A implementação consegue calcular eficientemente rotas ótimas entre pontos de ônibus, fornecendo uma base sólida para sistemas mais complexos de planejamento de transporte urbano.

A combinação de tecnologias modernas (OSMnx, NetworkX, GeoPandas) permite uma abordagem robusta e escalável para problemas reais de mobilidade urbana, evidenciando a importância da teoria dos grafos em aplicações práticas de engenharia e planejamento urbano.