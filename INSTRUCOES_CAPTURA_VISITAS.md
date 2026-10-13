# Captura de visitantes do CV — como finalizar a configuração

> **STATUS (13/10/2026): CONCLUÍDO.** A opção **A (Web3Forms)** foi escolhida e
> configurada. O envio funciona direto do navegador (o Web3Forms não permite
> envio pelo servidor no plano gratuito). Deploy publicado e testado.
> Você deve ter recebido um e-mail com assunto **"[CV] Teste de integracao"**
> na caixa de ccpjr8@gmail.com. Os próximos e-mails terão assunto
> **"[CV] Visita de ..."**. As instruções abaixo ficam como referência.

**Data:** 13/10/2026
**Site:** https://claudinepintocvinterativo4.vercel.app
**E-mail de destino:** ccpjr8@gmail.com

---

## O que já está feito (não precisa fazer nada)

- Criado o endpoint `api/visit.js` no projeto (função serverless do Vercel).
- Adicionado o script de coleta no site (`index.html`).
- Deploy já publicado em produção.
- O site captura automaticamente:
  - IP do visitante + cidade/estado/país + provedor (ISP/ASN)
  - Página visitada, origem (de onde veio), idioma, fuso horário
  - Duração da visita
  - Tempo de permanência em cada seção (Perfil, Experiência, Projetos, etc.)
  - Interações (cliques no telefone, no e-mail, no WhatsApp)
  - Pesquisas feitas no chat
- Envia **1 e-mail por visita**, com proteção contra spam (máximo 1 e-mail a cada 10 minutos por IP).
- Testado: o endpoint responde corretamente (status 503 = "falta configurar o e-mail").

## O que falta (escolha UMA das duas opções abaixo)

O Vercel não envia e-mail sozinho. É preciso escolher como os dados chegam ao
seu Gmail. Basta seguir os passos de uma das opções e me passar o que for
gerado.

---

## OPÇÃO A — Web3Forms (mais fácil, sem mexer na conta do Google) — RECOMENDADA

1. Abra **https://web3forms.com**
2. Clique em **Get Free Access** (botão azul)
3. Informe o e-mail **ccpjr8@gmail.com** e clique em continuar
4. Abra o e-mail que chegar na sua caixa de entrada e clique no link de confirmação
5. O painel mostra uma chave chamada **Access Key**, com 32 caracteres,
   parecida com: `8f3c2a1b-4d5e-...` ou `a1b2c3d4e5f6...`
6. **Copie essa chave e me envie no chat**

O que eu faço depois:
- Troco o endpoint do site para `https://api.web3forms.com/submit`
- Configuro a chave, faço o deploy e testo o envio
- Você recebe o primeiro e-mail de teste na caixa

Limite grátis: 250 e-mails por mês.
Não precisa de senha do Google. Não muda a URL do seu site.

---

## OPÇÃO B — Gmail com senha de app (usa o próprio SMTP do Google)

Requer que a **verificação em duas etapas** esteja ativa na sua conta Google.

1. Ative a verificação em duas etapas:
   https://myaccount.google.com/signinoptions/two-step-verification
   (clique em **Começar** e siga as instruções com o celular)

2. Gere a senha de app:
   https://myaccount.google.com/apppasswords
   - No campo *Nome do app* digite: `CV Vercel`
   - Clique em **Criar**
   - Aparece uma caixa com **16 letras** no formato `xxxx xxxx xxxx xxxx`

3. **Copie as 16 letras e me envie no chat**

   Observação: se a página disser que "senhas de app não estão disponíveis",
   é porque a verificação em duas etapas do passo 1 ainda não foi ativada.

O que eu faço depois:
- Guardo a senha como variável secreta no Vercel (`GMAIL_APP_PASSWORD`)
- Faço o deploy e envio um e-mail de teste para ccpjr8@gmail.com

Atenção: **não envie a senha normal da sua conta Google** (a que você usa para
entrar). Só a senha de app de 16 letras, que serve apenas para esse fim e pode
ser revogada a qualquer momento.

---

## Onde o projeto está

- Código: `C:\Projetos\CV` (repositório GitHub: `claudine08/CV`)
- Arquivos principais:
  - `index.html` e `Claudine_Pinto_CV_Interativo4.html` (site + script de coleta)
  - `api/visit.js` (função que formata e envia o e-mail)
  - `package.json` (dependência: nodemailer)
- Projeto no Vercel: `homeland1/claudine_pinto_cv_interativo4`
- Comandos de deploy (executar na pasta `C:\Projetos\CV`):
  - `vercel deploy --prod --yes`

## Privacidade

O site coleta dados de visitantes e envia apenas para o seu e-mail. Não foi
adicionado aviso no site, conforme sua escolha. Recomendo revisar isso sob a
ótica da LGPD caso o site venha a ser divulgado publicamente.

---

## Resumo rápido

| Opção | O que você faz | O que me envia |
|---|---|---|
| A — Web3Forms | Criar conta gratuita em web3forms.com | A Access Key (32 caracteres) |
| B — Gmail | Gerar senha de app em myaccount.google.com | As 16 letras da senha de app |
