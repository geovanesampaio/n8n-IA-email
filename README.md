# Projeto: Automação de Envio de Currículo Diário com IA (n8n)

## 📅 Objetivo

Automatizar o envio de um e-mail com o currículo profissional de **Geovane de Moura Sampaio** para uma empresa diferente a cada dia, utilizando IA (GPT/OpenAI) para revisar e variar o texto de forma inteligente e profissional.

---

## 🧰 Visão Geral

* Plataforma de automação: **n8n**
* IA: **OpenAI GPT-3.5 / GPT-4**
* Origem dos dados: **Google Sheets** (lista de empresas e status de envio)
* Destino: **SMTP (E-mail)** com **anexo em PDF** (currículo)

---

## 📂 Estrutura da Planilha (Google Sheets)

Nome sugerido: `Empresas_Contato`

| Empresa   | Email                                                     | Status   |
| --------- | --------------------------------------------------------- | -------- |
| Empresa A | [contato@empresaA.com.br](mailto:contato@empresaA.com.br) | Pendente |
| Empresa B | [rh@empresaB.com.br](mailto:rh@empresaB.com.br)           | Pendente |

* O fluxo busca apenas a primeira empresa com status `Pendente`.
* Após o envio, o status é atualizado para `Enviado`.

---

## 🪧 Componentes do Fluxo (n8n)

1. **Cron**

   * Agendado para executar 1x por dia (ex.: 09:00h).

2. **Google Sheets - Buscar Empresa**

   * Busca uma linha com `Status = Pendente`.

3. **OpenAI - Gerar Texto**

   * Prompt gera:

     * “Assunto”: assunto variado para o e-mail
     * “Corpo”: texto educado e profissional, diferente a cada envio

4. **Enviar Email (SMTP)**

   * Envia o e-mail para o contato da empresa
   * Anexa o currículo `planaltina.pdf`

5. **Google Sheets - Marcar como Enviado**

   * Atualiza o status para "Enviado"

---

## 🧐 Prompt de IA (OpenAI)

```text
Gere um e-mail profissional e curto (3 a 5 linhas) para envio de currículo. Varie o estilo e tom a cada geração. Evite repetir frases anteriores. Não cite nomes de empresa nem pessoas. Gere também um título para o e-mail, diferente a cada vez.

Formato de resposta:
Assunto: <assunto do e-mail>
Corpo: <corpo do e-mail>
```

---

## 💼 Rodapé Padrão no Corpo do E-mail

```text
Em anexo, segue meu currículo.

Geovane de Moura Sampaio
📞 (85) 92145-8536
🔗 www.linkedin.com/in/geovane-sampaio-a7a750372
```

---

## 📥 Currículo em Anexo

* Nome do arquivo: `planaltina.pdf`
* Anexo fixo no node de e-mail ou lido via `Read Binary File` no fluxo

---

## 📆 Agendamento

* Frequência: Diária
* Horário sugerido: 09:00h
* Evita envio para mais de uma empresa por dia

---

## 🚀 Como usar

1. Substituir o ID da planilha nos nodes do Google Sheets
2. Inserir a API Key da OpenAI no node GPT
3. Configurar o e-mail SMTP com credenciais do seu provedor (ex: Gmail)
4. Carregar ou referenciar o PDF do currículo como binário no fluxo
5. Testar com uma empresa fictícia antes de colocar em produção

---

## 📄 Licença

Este projeto pode ser distribuído livremente por Geovane de Moura Sampaio como projeto pessoal no GitHub.

---

## 📏 Créditos

**Autor**: Geovane de Moura Sampaio
**Assistente IA**: ChatGPT (OpenAI)
**LinkedIn**: [www.linkedin.com/in/geovane-sampaio-a7a750372](http://www.linkedin.com/in/geovane-sampaio-a7a750372)
