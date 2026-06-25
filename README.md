# 🌤️ Bot do Clima no Telegram (n8n + IA)

Este repositório contém a exportação de um fluxo de automação desenvolvido no **n8n** que opera um chatbot de previsão do tempo no Telegram. O projeto vai além de uma simples consulta de API, integrando Inteligência Artificial para humanizar as respostas e mecanismos de segurança (fallback) para garantir que o usuário nunca fique sem resposta.

## 🚀 Funcionalidades e Arquitetura

O fluxo foi desenhado com boas práticas de integração e resiliência:

* **Tratamento de Dados:** Sanitização da entrada do usuário, removendo espaços extras, convertendo para letras minúsculas e removendo acentos antes de enviar para a API.
* **Consulta de API Externa:** Integração com a API do OpenWeatherMap via requisição HTTP direta.
* **Roteamento e Tratamento de Erros:** Nó condicional (IF) que avalia o status da requisição HTTP. Caso o usuário digite uma cidade inexistente (Erro 404), o fluxo é desviado para uma ramificação de erro, devolvendo uma mensagem amigável com instruções de uso.
* **Humanização com IA (Google Gemini):** A mensagem padrão de temperatura é enviada para o modelo Gemini 1.5 Flash, que reescreve o texto com um tom mais natural e empático.
* **Arquitetura de Fallback (Plano B):** O sistema possui um mecanismo de segurança programado em JavaScript. Se a API do Google Gemini falhar, demorar a responder, ou retornar dados fora do formato esperado, o fluxo intercepta o erro e entrega a mensagem meteorológica padrão, garantindo estabilidade 100% do tempo.

## 🛠️ Tecnologias Utilizadas

* **[n8n](https://n8n.io/):** Plataforma de automação de fluxo de trabalho.
* **JavaScript:** Para nós de código (Data Parsing e Lógica de Fallback).
* **APIs:** 
  * Telegram Bot API
  * OpenWeatherMap API
  * Google Gemini API

## 📦 Como importar e rodar este projeto

1. Tenha uma instância do [n8n](https://n8n.io/) rodando (local ou nuvem).
2. Baixe o arquivo `workflow-chatbot-telegram.json` deste repositório.
3. No seu n8n, vá em **Workflows**, clique nos três pontos e selecione **Import from File**.
4. Configure as credenciais necessárias dentro do n8n:
   * **Telegram API:** Crie um bot no `@BotFather` do Telegram e insira o Token.
   * **OpenWeatherMap:** Substitua o valor da variável de ambiente ou adicione a sua chave no nó de HTTP Request.
   * **Google Gemini:** Insira sua chave de API no nó de IA.
5. Ative o fluxo e mande o nome de uma cidade para o seu bot no Telegram!

---
*Projeto desenvolvido como parte de um desafio prático de automação.*
