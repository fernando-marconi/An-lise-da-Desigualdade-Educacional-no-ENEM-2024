# Análise da Desigualdade Educacional no ENEM - Belo Horizonte

Este projeto apresenta uma investigação técnica sobre as disparidades de desempenho entre alunos de escolas públicas e privadas em Belo Horizonte, utilizando os microdados do ENEM 2024. A análise percorre desde a extração e tratamento dos dados até a geração de métricas de elite e distribuição estatística.

## Objetivos
* Comparar o desempenho acadêmico em cinco áreas: Ciências da Natureza, Ciências Humanas, Linguagens, Matemática e Redação.
* Quantificar a desigualdade socioeducacional através da distribuição de alunos em decis de nota.
* Identificar a probabilidade de sucesso (Razão de Elite) conforme a rede de ensino em Belo Horizonte.

## Arquitetura de Dados
O pipeline foi estruturado seguindo a arquitetura de medalhões para garantir a linhagem e integridade da informação:
* **Camada Bronze:** Dados brutos dos microdados nacionais filtrados geograficamente para o município de Belo Horizonte.
* **Camada Prata:** Limpeza, padronização de tipos e mapeamento de categorias administrativas como Federal, Estadual, Municipal e Privada.
* **Camada Ouro:** Modelagem analítica final com binarização de redes (Pública vs. Privada) e cálculo de decis de desempenho padronizados.

## Engenharia e Performance
Para otimizar o fluxo de dados e o armazenamento, utilizou-se o formato Apache Parquet com compressão Gzip.
* **Armazenamento Colunar:** Melhora a performance em consultas de grandes volumes e agregações.
* **Preservação de Tipos:** Garante que as categorias administrativas e os decis (D01 a D10) sejam mantidos sem perda de esquema entre as sessões.
* **Eficiência de Compressão:** Redução significativa do espaço em disco para armazenamento em ambientes de nuvem como Google Drive.

## Análises e Insights
* **Distribuição por Decis:** A utilização de gráficos de barras empilhadas de 100% permite visualizar a predominância acentuada da rede privada nos decis de maior pontuação (D09 e D10).
* **Gargalos por Matéria:** A análise de funil evidencia como o fluxo de alunos para os níveis de excelência varia drasticamente entre as redes pública e privada, especialmente em matérias como Matemática.
* **Métrica de Elite:** Cálculo da razão de chance de um aluno atingir o decil superior, fornecendo um KPI direto da disparidade educacional regional.

## Tecnologias Utilizadas
* **Python 3.12:** Linguagem base para o desenvolvimento do projeto.
* **Pandas e NumPy:** Bibliotecas utilizadas para transformação, limpeza e agregação de dados.
* **Plotly:** Ferramenta para geração de painéis interativos e subplots analíticos.
* **PyArrow:** Motor de processamento utilizado para a manipulação eficiente de arquivos Parquet.

## Estrutura do Repositório
* **projeto_enem_bh.ipynb:** Notebook principal contendo todo o pipeline de processamento e análise.
* **README.md:** Documentação técnica detalhada do projeto.

## Análise Estatística da Desigualdade

A tabela abaixo apresenta a Razão de Elite, métrica que quantifica a disparidade de acesso ao topo da pirâmide de desempenho entre as redes de ensino em Belo Horizonte.

| Matéria | Privada no D10 (%) | Pública no D10 (%) | Razão de Elite |
| :--- | :--- | :--- | :--- |
| Matemática | 21.14% | 2.9% | 7.3x |
| Ciências Natureza | 21.14% | 2.9% | 7.3x |
| Ciências Humanas | 21.59% | 2.8% | 7.7x |
| Linguagens e Códigos | 20.35% | 3.57% | 5.7x |
| Redação | 20.12% | 3.71% | 5.4x |

> **Insight Principal:** A maior desigualdade observada ocorre em [Ciências Humanas], onde um aluno da rede privada possui [7.7] vezes mais chance de estar entre as melhores notas (Decil 10) do que um aluno da rede pública.

Os resultados obtidos nesta análise confirmam a existência de um abismo educacional estrutural em Belo Horizonte, evidenciado pela disparidade nas métricas de Razão de Elite entre as redes pública e privada. A concentração de alunos da rede pública nos decis de menor desempenho e a baixa conversão de talentos para o topo da pirâmide de notas sugerem que a desigualdade no ENEM não é apenas um reflexo do exame em si, mas do acesso desigual a recursos educacionais ao longo da formação.

### Direcionamento para Gestão e Políticas Públicas
Com base nos dados extraídos da Camada Ouro, esta análise sugere os seguintes direcionamentos:

1.  **Foco em Ciências Exatas e da Natureza:** A acentuada Razão de Elite em Matemática e Ciências da Natureza indica a necessidade de investimentos prioritários em laboratórios, tecnologia e reforço pedagógico nestas áreas específicas dentro da rede pública de Belo Horizonte.
2.  **Redução de Gargalos:** O mapeamento por decis permite que gestores identifiquem onde a "fuga" de alunos para as faixas de baixo desempenho é mais crítica, possibilitando intervenções cirúrgicas em escolas ou regiões com indicadores abaixo da média municipal.
3.  **Monitoramento Baseado em Dados:** A implementação de uma arquitetura de dados escalável, como a utilizada neste projeto, permite o monitoramento contínuo da evolução destes indicadores ano após ano, garantindo que as políticas de equidade sejam avaliadas por sua eficácia real.

Este projeto demonstra que a Ciência de Dados é uma ferramenta indispensável para transformar grandes volumes de informação em diagnósticos precisos, capazes de fundamentar decisões que promovam a redução da desigualdade social e educacional.
