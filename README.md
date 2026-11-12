
# Manual Oficial e Operacional do Bot Jukinha

**Descrição:** Guia de referência técnica e instruções de manutenção para o bot de automação do Telegram integrado ao n8n.

## 1. Visão Geral do Projeto

- **Objetivo:** Automatizar o atendimento e processamento de mídias (áudio e texto) via Telegram, integrando Inteligência Artificial (Groq), planilhas de gerenciamento (Google Sheets) e ferramentas de criação de conteúdo.
- **Ecossistema:** n8n Cloud (orquestração), Telegram (canal de entrada e saída), Groq (transcrição de áudio e modelo de linguagem), Google Sheets (banco de ideias e memória).
- **Workflow:** "Bot Jukinha" (ID: fkaG1kihABqJFs72), ativo, com 50 nós no total.

## 2. Mapeamento dos Blocos Ativos e Funções

- **Gatilho:** `Telegram Trigger` — escuta mensagens e áudios enviados pelos usuários no Telegram.
- **Triagem de entrada:** `Tipo de mensagem` — separa o que chega como texto do que chega como áudio.
- **Processamento de Áudio:** `Baixar áudio Telegram` → `Renomear áudio OGA para OGG` → `Transcrever áudio Groq` → `Preparar texto do áudio` (baixa, ajusta formato e transcreve a voz em texto).
- **Roteamento de Comandos:** `Detectar comando falado` (interpreta a intenção do usuário) e `Switch` (direciona o fluxo para o agente ou tarefa correspondente) + `Filtro Estilo antes do IA` (filtro específico para pedidos de estilo musical).
- **Agentes Especializados (IA):**
  - `AI Agent` — assistente principal/geral.
  - `Agente Suno` — cria pacotes musicais prontos para o Suno.
  - `Agente Estilo Musical` — sugere estilo musical.
  - `Agente canva` — cria briefings visuais para o Canva.
  - `Agente Projeto` — monta planejamentos de campanha completos.
  - `Agente Video` — cria roteiros/prompts para geração de vídeo.
  - `Agente Legendas Jukinha` e `Agente Legenda` — criam legendas para redes sociais.
  - `Agente Roteiro` — escreve roteiros para locução/vídeo.
  - `Agente Publicar` — monta pacotes de divulgação (legenda, hashtags, CTA).
  - `Groq Chat Model` — motor de IA usado por todos os agentes acima.
- **Memória e Bancos de Dados:** `Simple Memory` (memória de conversa do AI Agent) e integrações com Google Sheets: `Planilha-1`, `Planilha-2`, `Get row(s) in sheet`, `Obter linhas 2`.
- **Respostas:** nós do tipo `Responder... Telegram` (um para cada agente) devolvem o resultado formatado ao usuário no Telegram.
- **Blocos inativos/desconectados:** `ElevenLabs Voz Jukinha`, `Gerar voz gratis`, `Enviar Áudio Telegram`, `Send an audio file` — testes de resposta em áudio não finalizados, atualmente desligados.

## 3. Regras de Ouro e Instruções para o Claude (Manutenção)

Sempre que o usuário (Chocolate Batera) solicitar ajustes, criações ou manutenções neste fluxo, siga estritamente estas diretrizes:

1. **Linguagem:** Explique tudo de forma simples, direta, passo a passo e sem jargões técnicos pesados. O usuário trabalha com blocos visuais e prefere instruções claras.
2. **Segurança:** Nunca exponha chaves de API ou senhas em texto puro (como ocorreu no bloco ElevenLabs). Sempre alerte sobre o uso de credenciais seguras antes de ativar qualquer bloco com chave exposta.
3. **Dinâmica de Trabalho:** O usuário opera com duas abas — Aba 1 (Claude, para pedir tarefas pesadas em português) e Aba 2 (painel visual do n8n, para conferir, inserir credenciais e testar). Ao finalizar qualquer alteração estrutural no fluxo, avise sempre no final da resposta: "Pode atualizar a página do n8n agora" (Command + R).
