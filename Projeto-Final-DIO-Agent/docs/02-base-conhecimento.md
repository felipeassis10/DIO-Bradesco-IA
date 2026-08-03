# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Para que serve no Finny? |
|---|---|---|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores, ou seja, dar continuidade ao atendimento de forma mais eficiente. |
| `perfil_investidor.json` | JSON | Personalizar as explicações sobre as dúvidas e necessidades de aprendizado do cliente. |
| `produtos_financeiros.json` | JSON | Conhecer os produtos disponíveis para que eles possam ser ensinados e recomendados ao cliente. |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente e usar essas informações de forma didática. |

---

## Adaptações nos Dados

Mantivemos a estrutura padrão dos arquivos disponibilizados na pasta `data/`, apenas ajustando os valores e perfis para garantir simulações realistas e direcionadas para educação financeira e controle de orçamento.

---

## Estratégia de Integração

### Como os dados são carregados?
Os arquivos `.csv` e `.json` localizados na pasta `data/` são lidos localmente pelo script Python na inicialização da aplicação usando as bibliotecas `pandas` e `json`.

python
# Exemplo de carregamento
import pandas as pd
import json

# CSVs
historico = pd.read_csv('data/historico_atendimento.csv')
transacoes = pd.read_csv('data/transacoes.csv')

# JSONs
with open('data/perfil_investidor.json', 'r', encoding='utf-8') as f:
    perfil = json.load(f)

with open('data/produtos_financeiros.json', 'r', encoding='utf-8') as f:
    produtos = json.load(f)

    Como os dados são usados no prompt?
Os dados extraídos dos arquivos são sintetizados e injetados diretamente no system prompt no início de cada sessão. Dessa forma, o modelo compreende o contexto do usuário antes de responder a qualquer mensagem.

Exemplo de Contexto Montado  
O exemplo de contexto montado abaixo se baseia nos dados originais da base de conhecimento, mas os sintetiza deixando apenas as informações mais relevantes, otimizando assim o consumo de tokens:

DADOS DO CLIENTE:
- Nome: Felipe Assis
- Perfil: Alto
- Objetivo: Construir reserva de emergência
- Reserva atual: R$ 10.000 (meta: R$ 15.000)

RESUMO DE GASTOS:
- Moradia: R$ 1.380
- Alimentação: R$ 570
- Transporte: R$ 295
- Saúde: R$ 188
- Lazer: R$ 55,90
- Total de saídas: R$ 2.488,90

PRODUTOS DISPONÍVEIS PARA EXPLICAR:
- Tesouro Selic (risco baixo)
- CDB Liquidez Diária (risco baixo)
- LCI/LCA (risco baixo)
- Fundo Imobiliário - FII (risco médio)
- Fundo de Ações (risco alto)
