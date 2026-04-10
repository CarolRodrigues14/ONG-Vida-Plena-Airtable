# 🤖 Configuração Make.com - ONG Vida Plena

## Visão Geral

Este guia explica como configurar a automação que envia emails automáticos quando um beneficiário se inscreve em um evento.

**Fluxo**: Airtable (Nova Inscrição) → Make.com → Gmail (Confirmação)

---

## ✅ Pré-requisitos

Antes de começar:
- [ ] Conta ativa em [Make.com](https://make.com)
- [ ] Base Airtable "ONG Vida Plena" criada (com tabelas)
- [ ] Conta Gmail (pessoal ou corporativa)
- [ ] Acesso de editor no Airtable
- [ ] Acesso à base ID do Airtable (será fornecido pela plataforma)

---

## 📝 PASSO 1: Criar Scenario no Make.com

### 1.1 Acessar Make.com
1. Vá para [make.com](https://make.com)
2. Faça login com sua conta
3. Clique em **"+ Create a new scenario"**

### 1.2 Nomear o Scenario
1. Clique em **"Scenario"** (canto superior esquerdo)
2. Digite nome: `Notificação de Inscrição ONG Vida Plena`
3. Pressione Enter para salvar

### 1.3 Começar com Trigger
1. Clique no ícone **"+"** (primeiro módulo)
2. Procure por **"Airtable"**
3. Selecione **"Airtable > Watch Records"**
4. Clique em **"Add"**

---

## 🔗 PASSO 2: Configurar Airtable (Watch Records)

### 2.1 Conectar Conta Airtable
1. Em **"Connection"**, clique em **"Add"**
2. Aparecerá pop-up pedindo autorização
3. Clique **"Connect"** (ou **"Authorize"**)
4. Faça login com email Airtable
5. Autorize Make.com a acessar sua base
6. Volta para o Make.com automaticamente

### 2.2 Selecionar Base e Tabela
1. Em **"Base"**: Selecione sua base "ONG Vida Plena"
2. Em **"Table"**: Selecione **"Inscrições"**
3. Em **"View"**: Deixe em branco (pega todos os registros)

### 2.3 Configurações Adicionais
- **Trigger Type**: "New records" (detectar novos registros)
- **Limit**: 100 (máximo de registros por execução)
- **Sort By**: Deixar em branco

### 2.4 Salvar
1. Clique em **"OK"**
2. O módulo fica pronto (azul com ✓)

---

## 🔍 PASSO 3: Adicionar Módulo "Get Record" (Beneficiário)

### 3.1 Adicionar Novo Módulo
1. Clique no **"+"** abaixo do módulo anterior
2. Procure por **"Airtable"**
3. Selecione **"Airtable > Get a Record"**
4. Clique **"Add"**

### 3.2 Configurar Busca do Beneficiário
1. **Connection**: Deve estar já conectado (mesma conta)
2. **Base**: Selecione "ONG Vida Plena"
3. **Table**: Selecione **"Beneficiários"**
4. **Record ID**: Clique no campo e selecione
   - Procure por **"Beneficiário (ID)"** vindo do trigger anterior
   - Ou procure por **"Beneficiário"** (pode vir como link/referência)

### 3.3 Salvar
1. Clique **"OK"**
2. Nome deste módulo muda para "Get Record 1"

---

## 🎯 PASSO 4: Adicionar Módulo "Get Record" (Evento)

### 4.1 Adicionar Novo Módulo
1. Clique no **"+"** novamente
2. Procure por **"Airtable"**
3. Selecione **"Airtable > Get a Record"**
4. Clique **"Add"**

### 4.2 Configurar Busca do Evento
1. **Connection**: Mesma conta
2. **Base**: "ONG Vida Plena"
3. **Table**: Selecione **"Eventos"**
4. **Record ID**: Clique e procure por **"Evento (ID)"** ou **"Evento"**
   - Vem do trigger inicial (tabela Inscrições)

### 4.3 Salvar
1. Clique **"OK"**
2. Nome muda para "Get Record 2"

---

## 📧 PASSO 5: Configurar Gmail (Send Email)

### 5.1 Adicionar Novo Módulo
1. Clique no **"+"** novamente
2. Procure por **"Gmail"**
3. Selecione **"Gmail > Send an Email"**
4. Clique **"Add"**

### 5.2 Conectar Gmail
1. Em **"Connection"**, clique **"Add"**
2. Pop-up de autorização Google
3. Selecione sua conta Gmail
4. Clique **"Allow"** (conceder permissões)
5. Volta automaticamente

### 5.3 Preencher Campos do Email

#### **TO** (Para - Obrigatório)
Clique no campo e procure por:
- Opção 1: **"Email"** (do módulo "Get Record 1 - Beneficiário")
- Campo estará assim: `2. Email`

#### **SUBJECT** (Assunto)
Cole este texto e customize:
```
Confirmação de Inscrição - {{2. Nome Evento}} 🎉
```

Ou simplesmente:
```
Sua inscrição foi confirmada!
```

#### **BODY** (Corpo do Email)
Cole este template (substitua `{{X. Campo}}` pelos dados corretos):

```
Olá, {{2. Nome}}!

Sua inscrição foi confirmada com sucesso! 🎉

📋 DETALHES DO EVENTO:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Evento: {{3. Nome}}
Data: {{3. Data}}
Local: {{3. Local}}
Tipo: {{3. Tipo}}
Vagas Disponíveis: {{3. Vagas}}

📞 CONTATO:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Telefone: (11) 3000-0000
Email: contato@ongvidaplena.org

Contamos com sua presença! 💪

Se tiver alguma dúvida, responda este email ou entre em contato conosco.

Abraços,
ONG Vida Plena
Transformando comunidades através da educação e inclusão digital.
```

### 5.4 Opções Adicionais
- **CC**: Deixar em branco (ou colar email do gestor)
- **BCC**: Deixar em branco
- **REPLY TO**: Pode preencher com email da ONG

### 5.5 Salvar
1. Clique **"OK"**
2. O módulo fica pronto

---

## ⚙️ PASSO 6: Testar Automação

### 6.1 Ativar Scenario
1. No canto superior esquerdo, veja o toggle **ON/OFF**
2. Clique para deixar **ON** (deve ficar azul)

### 6.2 Fazer Teste
1. **Opção 1 - Teste Manual:**
   - Volte para Airtable
   - Tabela "Inscrições"
   - Crie uma inscrição de TESTE
   - Retorne ao Make.com
   - Clique em **"Run once"** para forçar execução

2. **Opção 2 - Teste Automático:**
   - Airtable → Tabela Inscrições
   - Crie inscrição com dados reais
   - Aguarde até 15 minutos (intervalo de check)
   - Verifique inbox do beneficiário

### 6.3 Verificar Resultado
1. **No Make.com:**
   - Vá para **"Execution History"**
   - Procure por execução recente (com ✅ verde)
   - Clique para expandir e ver detalhes

2. **No Gmail:**
   - Acesse inbox do beneficiário
   - Procure por email com assunto "Confirmação de Inscrição..."
   - Verifique se dados estão personalizados
   - Se não chegou, verificar pasta de spam

3. **No Airtable:**
   - Volte para tabela "Inscrições"
   - Confirme que o registro foi criado

✅ **Se tudo funcionou: Automação está 100% operacional!**

---

## 🚨 Troubleshooting

### Problema 1: Nenhum email chega

**Checklist:**
- [ ] Gmail está autorizado no Make.com?
- [ ] Email do beneficiário está correto em Airtable?
- [ ] Automação está ativada (toggle azul)?
- [ ] Airtable e Make.com conectados?

**Solução:**
1. Vá para "Execution History"
2. Procure por erro (❌ vermelho)
3. Clique para ver detalhes do erro
4. Erros comuns:
   - "Invalid email address" → Email inválido no Airtable
   - "Not connected" → Reconectar Gmail

### Problema 2: Email vem em branco ou incompleto

**Causa:** Campo mapping errado

**Solução:**
1. Ir ao módulo "Send an Email"
2. Clique em **"BODY"**
3. Verifique se `{{2. Email}}` está correto
4. Use "Edit" para ver todas as variáveis disponíveis
5. Mude para campo correto

### Problema 3: Automação rodando mas sem dados

**Causa:** Trigger não pegou nenhum novo registro

**Solução:**
1. Vá ao primeiro módulo (Watch Records)
2. Clique em **"Edit"**
3. Clique em **"Determine data structure"**
4. Volte para Airtable
5. Crie um novo registro
6. Retorne ao Make.com
7. Clique em "Determine..." novamente
8. Salve

### Problema 4: Make.com diz "Too many requests"

**Causa:** Limite de operações atingido

**Solução:**
- Plano gratuito: 1.000 operações/mês
- Esperada por ~23 horas
- Ou fazer upgrade para plano pago

---

## 📊 Monitoramento

### Check Lista Semanal

- [ ] Acessar Make.com
- [ ] Verificar "Execution History" (nenhum erro vermelho?)
- [ ] Testar enviando uma inscrição de teste
- [ ] Confirmar email chegou
- [ ] Se houver erro, documentar e resolver

### Métricas a Acompanhar

```
Total de Execuções: 100+
Taxa de Sucesso: 99%+
Emails Enviados: 87
Emails Falhados: 0-1
Tempo Médio: < 5 min
```

---

## 🔐 Segurança

### Boas Práticas

✅ **Fazer:**
- [ ] Manter senha Make.com segura
- [ ] Revisar "Execution History" regularmente
- [ ] Fazer backups das configurações
- [ ] Testar mensalmente

❌ **Não fazer:**
- Compartilhar URL Make.com publicamente
- Expor IDs de base/tabela em lugares públicos
- Armazenar senhas em documentos compartilhados

---

## 💾 Backup das Configurações

### Exportar Scenario do Make.com
1. Clique em **"..."** (menu do scenario)
2. Selecione **"Export Blueprint"**
3. Salve o arquivo JSON
4. Guarde em pasta segura

### Importar Scenario (Se Necessário)
1. Novo Make.com
2. **"+ Create new scenario"**
3. Clique em **"..."**
4. **"Import Blueprint"**
5. Selecione arquivo JSON
6. Reconectar contas (Airtable, Gmail)

---

## 📞 Suporte

### Documentação Oficial
- **Make.com**: https://make.com/docs
- **Airtable**: https://airtable.com/api
- **Gmail**: https://support.google.com/mail

### Comunidade
- Make.com Community Forum
- Stack Overflow (tag: make-com)
- Reddit: r/nocode

### Contato do Projeto
- Email: carol.gui.ro@gmail.com
- GitHub: CarolRodrigues14

---

## ✨ Próximas Melhorias (Futuro)

Quando estiver confortável, explore:
- [ ] Adicionar WhatsApp (via Twilio)
- [ ] Lembrete automático 24h antes
- [ ] Cancelamento automático de inscrição
- [ ] Geração de relatório semanal
- [ ] Integração com Zapier (alternativa Make)

---

**Última atualização**: Janeiro 2026
**Status**: ✅ Testado e funcional
**Manutenção**: Ativa
