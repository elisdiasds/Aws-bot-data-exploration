# 🤖 Análise de Dados de Bot com AWS

## 📚 Sobre o projeto
Projeto desenvolvido como trabalho de conclusão do curso **Profissão Analista de Dados** da EBAC.  
O objetivo foi coletar, armazenar e analisar mensagens enviadas por usuários em um grupo do Telegram, utilizando serviços da AWS para ingestão e persistência dos dados.

---

## 🎯 Objetivo
- Construir um pipeline simples de ingestão de dados em tempo real.
- Explorar e analisar os dados para identificar padrões e horários de maior atividade.

---

## 📦 Fonte – Dados Transacionais
Utilizei o método `getUpdates` da API de bots do **Telegram** para capturar mensagens enviadas por usuários em um grupo.

### 📌 Exemplo de dados recebidos (mock):
```json
{
  "update_id": 123456,
  "message": {
    "message_id": 1,
    "from": {
      "id": 111,
      "first_name": "João"
    },
    "chat": {
      "id": -222,
      "title": "Grupo de Teste"
    },
    "date": 1679845561,
    "text": "Olá, tudo bem?"
  }
}
```

---

## ☁ Pipeline de ingestão na AWS

### ✏️ Função Lambda para salvar dados no S3
```python
import json
import boto3
import datetime

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    mensagem = json.loads(event['body'])

    nome_arquivo = f"telegram_data_{datetime.datetime.now().isoformat()}.json"
    s3.put_object(
        Bucket='nome-do-bucket',
        Key=nome_arquivo,
        Body=json.dumps(mensagem)
    )
    return {'statusCode': 200, 'body': json.dumps('Mensagem salva com sucesso!')}
```

Esta função foi acionada via **API Gateway**, recebendo os dados em tempo real e salvando arquivos JSON no bucket S3.

---

## 🔍 Análise exploratória
- Leitura dos arquivos JSON armazenados no S3.
- Limpeza e padronização dos dados para facilitar a análise.

---

## ✨ Principais resultados
- Identificação de períodos com maior volume de mensagens.
- Organização dos dados para análises futuras.
- Experiência prática de integração de APIs com AWS e análise de dados em Python.

---

## 📎 Notebook completo no Kaggle
🔗 [Clique aqui para acessar](https://www.kaggle.com/code/elisdias/an-lise-de-dados-de-bot-com-aws)

---

## 🛠 Tecnologias e ferramentas utilizadas
- AWS (Lambda, API Gateway, S3)
- Python (pandas, boto3)
- Ambiente: Kaggle Notebooks

---

## 📫 Contato
Para saber mais ou colaborar, entre em contato pelo [LinkedIn](https://www.linkedin.com/in/elisangeladias-dados/).

---

✨ *Projeto realizado como parte do curso Profissão Analista de Dados (EBAC).*
