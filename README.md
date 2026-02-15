# 🤖 Chatbot Telegram com N8N + OpenWeather

Este projeto implementa um chatbot no Telegram utilizando **n8n** que consulta a API da **OpenWeather** para retornar a temperatura atual de uma cidade informada pelo usuário.

---

## 📌 Funcionalidades

- Recebe mensagem via Telegram
- Valida formato da cidade (Cidade,UF,País)
- Consulta API OpenWeather
- Retorna temperatura arredondada
- Trata erros (cidade inválida / erro de API)
- Responde diretamente no Telegram

---

## 🛠️ Tecnologias Utilizadas

- n8n (self-hosted)
- Telegram Bot API
- OpenWeather API

---


# 🧠 Explicação do Workflow

O workflow segue a seguinte estrutura:

Telegram Trigger

↓

FormataCidade

↓

Get - API OpenWeather

↓

Valida Retorno (IF)

↓ TRUE  → Trata Retorno → Envia mensagem

↓ FALSE → Trata Erro → Envia mensagem

---

# 🚀 Como importar o workflow no n8n

1. Acesse seu painel do n8n
2. Clique em **Workflows**
3. Clique em **Import from File**
4. Selecione o arquivo: workflow-chatbot-telegram.json
5. Clique em **Import**

---

# 🔑 Configuração das Credenciais

Este projeto utiliza duas variáveis de ambiente obrigatórias:

- `OPENWEATHER_API_KEY`
- `TELEGRAM_BOT_TOKEN`

---

## 🌤️ 1. Configurar OpenWeather

### Criar conta:
https://home.openweathermap.org/users/sign_up

### Criar API Key:
1. Vá em **API Keys**
2. Gere uma nova chave
3. Aguarde ativação (pode levar até 60 minutos)
