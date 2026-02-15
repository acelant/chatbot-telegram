# 🤖 Telegram Weather Chatbot com n8n

![n8n](https://img.shields.io/badge/n8n-automation-orange)
![Telegram](https://img.shields.io/badge/Telegram-Bot-blue)
![OpenWeather](https://img.shields.io/badge/OpenWeather-API-yellow)
![Status](https://img.shields.io/badge/status-academic_project-success)

---

## 📌 Sobre o Projeto

Este projeto implementa um chatbot no Telegram utilizando **n8n** para consultar a API da **OpenWeather** e retornar a temperatura atual de uma cidade informada pelo usuário.

O bot realiza:

- Validação do formato da entrada (`Cidade,UF`)
- Tratamento de erros antes e após chamada da API
- Consulta HTTP autenticada via Query Auth
- Extração e arredondamento da temperatura
- Resposta formatada diretamente no Telegram

Este projeto foi desenvolvido para fins acadêmicos e demonstra boas práticas de automação com n8n.

---

## 🏗️ Arquitetura do Workflow

O fluxo do chatbot segue a seguinte estrutura:

Telegram Trigger  
→ FormataCidade  
→ Valida Cidade (IF)  
  ↳ Se inválida → Envia mensagem de erro  
  ↳ Se válida → HTTP OpenWeather  
    → Valida Retorno (IF)  
      ↳ Sucesso → Trata Retorno → Envia mensagem  
      ↳ Erro → Trata Erro → Envia mensagem
      
---

# 🚀 Instalação e Execução

## 1️⃣ Importar o Workflow

1. Abra o painel do **n8n**
2. Vá em **Workflows**
3. Clique em **Import from file**
4. Selecione o arquivo:

workflow-chatbot-telegram.json

---

# 🔑 Configuração de Credenciais

Este projeto requer duas variáveis:

| Variável | Descrição |
|----------|-----------|
| `OPENWEATHER_API_KEY` | Chave da API OpenWeather |
| `TELEGRAM_BOT_TOKEN` | Token do bot Telegram |

---

# 🌤️ Configurar OpenWeather

1. Criar conta:  
   https://home.openweathermap.org/users/sign_up  

2. Gerar API Key:  
   https://home.openweathermap.org/api_keys  

3. Criar credencial no n8n:
   - Tipo: **HTTP Query Auth**
   - Parâmetro: `appid`
   - Valor: sua `OPENWEATHER_API_KEY`

Se utilizar variável de ambiente:

OPENWEATHER_API_KEY=`2764b53397f89e1`

---

# 📲 Configurar Telegram Bot

1. No Telegram, abra **@BotFather**
2. Execute:

/newbot

3. Copie o token gerado

No n8n:

- Vá em **Credentials**
- Criar nova credencial → **Telegram API**
- Inserir `TELEGRAM_BOT_TOKEN`

Ou via variável de ambiente:

TELEGRAM_BOT_TOKEN=`8474231789:AAFnw7fsQqi9f`

---

# ▶️ Como Testar

1. Certifique-se que o workflow está **Active**
2. Abra o Telegram
3. Envie uma mensagem no formato:

Cidade,UF

---

# ✅ Exemplo de Uso

## Entrada

São Paulo,SP

## Saída Esperada

🌤️ Clima em São Paulo: 27°C

*(A temperatura pode variar conforme dados atuais da API)*

---

# ❌ Validação de Formato

## Entrada inválida

São Paulo

## Resposta

❌ Cidade não encontrada. Use o formato Cidade,UF (ex.: São Paulo,SP).

---

# ❌ Cidade Inexistente

## Entrada

CidadeInexistente,SP

## Resposta

❌ Cidade não encontrada. Verifique o nome e tente novamente.

---

# 🧠 Detalhamento Técnico

## 🔹 FormataCidade (Set Node)

- Extrai texto do Telegram
- Divide por vírgula
- Normaliza estado para maiúsculo
- Gera:
  - `queue`
  - `cidadeValida`

---

## 🔹 Valida Cidade (IF Node)

Verifica:

{{$json.cidadeValida}}

Evita chamadas desnecessárias à API.

---

## 🔹 HTTP OpenWeather

### Endpoint

https://api.openweathermap.org/data/2.5/weather

### Parâmetros

- `q` → Cidade formatada
- `units` → metric
- `lang` → pt_br
- `appid` → via Query Auth

---

## 🔹 Tratamento de Retorno

Valida:

- `statusCode === 200`
- `body.main.temp` existe
- `body.name` existe

Arredonda temperatura com:

`Math.round($json.main.temp)`

---

# 📊 Boas Práticas Aplicadas

- ✅ Validação antes da requisição
- ✅ Tratamento estruturado de erros
- ✅ Separação clara de responsabilidades por nó
- ✅ Uso de autenticação segura via credenciais
- ✅ Workflow modular e legível

---

# 🛠️ Tecnologias Utilizadas

- n8n
- Telegram Bot API
- OpenWeather API
- JavaScript (expressions no n8n)

---

# 📄 Licença

Projeto desenvolvido para fins acadêmicos e demonstração técnica.
