# KODA AI

Primeira versão da interface da KODA: chat React/Vite, histórico local, anexos de imagem e função Supabase Edge Function para respostas reais de IA.

## Incluído
- Interface responsiva em português, lista e busca de conversas.
- Histórico salvo automaticamente no navegador e mantido após atualizar a página no mesmo navegador.
- Anexos de imagens de até 8 MB; até três imagens por mensagem são enviadas à função.
- Backend Edge Function que guarda a chave do provedor no servidor.
- Migração SQL que prepara tabelas e políticas RLS para histórico por usuário.
- Mensagens claras de erro; a interface não finge que a IA respondeu.

## Executar localmente
1. Instale Node.js LTS e execute `npm install` e `npm run dev`.
2. Crie um projeto no Supabase e copie `.env.example` para `.env.local`; preencha `VITE_SUPABASE_URL` e `VITE_SUPABASE_ANON_KEY`.
3. Execute `supabase/migrations/202610240001_initial.sql` no SQL Editor do Supabase.
4. Instale a CLI do Supabase, faça login e vincule o projeto.
5. Configure o segredo no servidor: `supabase secrets set OPENAI_API_KEY=sua_chave`. Opcional: `supabase secrets set KODA_MODEL=gpt-4o-mini`.
6. Publique a função com `supabase functions deploy koda-chat` e reinicie o Vite.

## Limitações desta versão
- O histórico está salvo localmente neste navegador/dispositivo. A sincronização entre dispositivos requer ligar autenticação e tabelas ao chat; as tabelas e RLS são apenas a base inicial.
- Imagens são enviadas para análise pelo modelo. Vídeos ainda não são analisados.
- O uso da API pode gerar custos e depende dos limites do provedor.
- Antes de produção, implemente autenticação efetiva na função, limite de requisições e proteção contra abuso.
- Nunca exponha `OPENAI_API_KEY` no frontend nem em variáveis `VITE_`.

Stack: React, TypeScript, Vite, Supabase Edge Functions e API de chat compatível com OpenAI.
