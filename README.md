# Motiva + FIAP — Dynamic Programming

## Projeto
Priorização de escadas rolantes e roteirização de manutenção da ViaQuatro, alinhada ao Project Charter CP3 do grupo.

**Integrantes:** Vinicius Kozonoe Guaglini (567264); João Victor Melo Santos (566640); Yan Lucas Gonçalves da Silva (567046); Murilo Jeronimo Ferreira Nunes (560641); Gustavo Macedo Daniel (567594).

## Status dos dados — importante
**Execução demonstrativa.** Os dados reais da Motiva não estavam anexados. `dados/ocorrencias_demo.csv`, `dados/escadas_estacoes.csv` e os minutos de `dados/rede_estacoes.csv` são **ilustrativos**. Os nomes das estações correspondem à Linha 4-Amarela, mas os tempos de deslocamento, a localização da base e a associação das escadas não foram validados. **Não apresente rankings como resultados reais.**

O Charter descreve histórico SAP (notas, IW47, MB51) sem sensores de vibração, temperatura, corrente, óleo ou velocidade. A função de degradação pedida no enunciado foi adaptada para **pontuação acumulada de manutenção**, exigindo aprovação do professor.

## Executar
1. Instale Python 3.10+ e `pip install -r requirements.txt`.
2. Abra `notebook.ipynb` com Jupyter ou VS Code, a partir da pasta do projeto.
3. Execute todas as células em ordem. O notebook entregue contém saídas demonstrativas executadas.
4. Para usar os dados reais, normalize o SAP no CSV `dados/ocorrencias_reais_tratadas.csv` e altere `ARQUIVO_OCORRENCIAS` na primeira célula Python. Mantenha os arquivos originais privados se houver dados pessoais.

## Esquema obrigatório para os dados normalizados
`escada_id,data,tipo_ocorrencia,horas_indisponibilidade,horas_mao_obra,reincidente_30d` (tipo: `corretiva`/`preventiva`, reincidência 0/1). O mapeamento do SAP precisa ser validado e documentado. Atualize `escadas_estacoes.csv` com vínculo real e `rede_estacoes.csv` com tempos fundamentados antes de alegar aplicabilidade.

## Algoritmos e interpretações
- **Recursão pura, memoização, tabulação:** somatório de pesos por evento. A implementação pura recalcula os prefixos (tempo total O(n²)); memoização e tabulação O(n). Os resultados são numericamente equivalentes; as medições variam conforme máquina.
- **Ranking:** ordena pela pontuação acumulada. Comparar janelas equivalentes para não favorecer escadas com mais registros.
- **BFS:** menos trechos; **Dijkstra:** menos minutos, usando grafo não direcionado com pesos positivos.
- **A*:** heurística nula (admissível e consistente); resultados iguais aos de Dijkstra, sem promessa de melhoria. Para ganho real, obter heurística baseada em distâncias/limites de deslocamento fundamentados.
- **Plano de turno:** heurística gulosa por criticidade, com tempo de ida, serviço e retorno à base. Não garante ótimo global.

## Limitações e recomendações
Os pesos de risco e 30 minutos de atendimento são hipóteses de demonstração. O escopo não prevê diagnóstico físico de componentes, previsão exata de falhas nem alteração automática de manutenção. Considerar mudança de registros em 2023, reincidência, duplicatas, confidencialidade, janelas de operação, segurança e validação da engenharia.



