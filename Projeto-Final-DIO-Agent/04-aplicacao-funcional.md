# 4. Aplicação Funcional

Desenvolva um protótipo funcional do seu agente:

* **Interface:** Chat UI interativo (sugestão: Streamlit, Gradio ou similar)
* **LLM:** Integração com LLM (via API ou modelo local)
* **Base:** Conexão com a base de conhecimento

---

## 5. Avaliação e Métricas

Descreva como você avaliará a qualidade do seu agente:

### Métricas Sugeridas:
* **Precisão/assertividade das respostas**
* **Taxa de respostas seguras (sem alucinações)**
* **Coerência com o perfil do cliente**

Template: `docs/05-metricas.md`

---

## 6. Pitch

Grave um pitch de **3 minutos** (estilo elevador) apresentando:

* Qual problema seu agente resolve?
* Como ele funciona na prática?
* Por que essa solução é inovadora?

import json
import requests
import pandas as pd
import streamlit as st

# ================= CONFIGURAÇÃO =================
OLLAMA_URL = "http://localhost:11434/api/generate"
MODELO = "llama3"

# ================= CARREGAR DADOS =================
perfil = json.load(open('data/perfil_investidor.json', encoding='utf-8'))
transacoes = pd.read_csv('data/transacoes.csv')
historico = pd.read_csv('data/historico_atendimento.csv')
produtos = json.load(open('data/produtos_financeiros.json', encoding='utf-8'))

# ================= MONTAR CONTEXTO =================
contexto = f"""
DADOS DO CLIENTE E PERFIL:
- Nome: {perfil['nome']} | Idade: {perfil['idade']} anos | Perfil: {perfil['perfil_investidor']}
- Objetivo: {perfil['objetivo_principal']}
- Patrimônio: R$ {perfil['patrimonio_total']} | Reserva: R$ {perfil['reserva_emergencia_atual']}

TRANSAÇÕES RECENTES:
{transacoes.to_string(index=False)}

ATENDIMENTOS ANTERIORES:
{historico.to_string(index=False)}

PRODUTOS DISPONÍVEIS:
{json.dumps(produtos, indent=2, ensure_ascii=False)}
"""

# ================= SYSTEM PROMPT =================
SYSTEM_PROMPT = f"""
Você é o Finny, um educador financeiro amigável e didático.
Seu objetivo é ensinar conceitos de finanças pessoais de forma simples, usando os dados do cliente como exemplos práticos.

REGRAS:
1. NUNCA recomende investimentos específicos, apenas explique como funcionam.
2. JAMAIS responda a perguntas fora do tema de finanças pessoais.
3. Quando ocorrer, responda lembrando o seu papel de educador financeiro.
4. Use os dados fornecidos para dar exemplos personalizados.
5. Linguagem simples, como se explicasse para um amigo.
6. Se não souber algo, admita: "Não tenho essa informação, mas posso explicar...".
7. Sempre pergunte se o cliente entendeu.
8. Responda de forma sucinta e direta, com no máximo 3 parágrafos.

CONTEXTO DO CLIENTE:
{contexto}
"""

# ================= CHAMAR OLLAMA =================
def perguntar(msg):
    prompt = f"""
{SYSTEM_PROMPT}

Pergunta: {msg}
"""
    r = requests.post(OLLAMA_URL, json={"model": MODELO, "prompt": prompt, "stream": False})
    return r.json()['response']

# ================= INTERFACE STREAMLIT =================
st.title("💡 Finny, seu Educador Financeiro")

if pergunta := st.chat_input("Sua dúvida sobre finanças..."):
    st.chat_message("user").write(pergunta)
    with st.spinner("Finny está analisando..."):
        resposta = perguntar(pergunta)
        st.chat_message("assistant").write(resposta)
