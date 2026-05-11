# Sopra Gestao - Contexto

App single-file HTML em https://rmichelon79.github.io/sopra-gestao/

Stack: HTML/JS vanilla, Supabase (banco + Storage), GitHub Pages.

## Deploy
cd ~/Desktop/sopra-gestao-repo
git add index.html
git -c user.email=ricardo@michelon.com -c user.name=Ricardo commit -m msg
git push

Arquivo de trabalho: ~/Desktop/sopra-gestao.html (espelho de index.html no repo).

## Supabase
URL: https://cgnuelmiacweybmvlbcm.supabase.co
Chaves em ~/bin/sopra-backup.py
Tabela dados (jsonb payload, id=sopra). Bucket Storage documentos com policies para anon.

## Estrutura D
- objetivos, kpis (89 - NOME do KPI eh ind nao nome), empreendimentos
- rituais, cadencias, docs (5 fixos + customizados)
- pessoas, usuarios (sync para Supabase desde 04/2026)

## Usuarios
- admin: ricardo (sopra2026)
- gestor: suelen, wagner, paloma
- viewer: mateus, roberta

## Documentos
- doc1 Orcamento Empresarial (anual)
- doc2 DRE Mensal (mensal, key=Mes/YY)
- doc3 Fluxo de Caixa (mensal)
- doc4 Metas Comerciais (multiplo)
- doc5 Metas de Marketing (multiplo)

Upload: POST primeiro, PUT se 400/409. So admin pode editar (renderDocs ce=role==admin).

## Sincronizacao
saveData -> sbSave (serializado, merge com servidor antes do PATCH).
renderDocs faz refresh do servidor 1x por sessao (_docsRefreshed) para evitar cache stale.
D._deletedDocEntries protege delecoes por 5 min.

## Conventions
Cores: #1D9E75 ok, #EF9F27 warn, #E24B4A risk, #999 sem dados.
Tipografia: DM Sans, DM Serif Display, DM Mono.
Background: #F7F5F0.
DATA_KEY: sopra-data-v14. Datas com T12:00:00.

## Bugs ja resolvidos (nao repetir)
- TDZ em abrirMapaOkrs: declarar helpers ANTES de let html=
- avgDisplay undefined no Dashboard: cada render funcao precisa suas proprias vars
- Upload mensal sem seletor: modal pede mes+ano
- Docs nao aparecem para nao-admin: refresh do servidor em renderDocs
- Usuarios se perdendo: agora em D.usuarios sincronizado
- Delecao de doc restaurada: sistema _deletedDocEntries 5min
- RLS Storage: 4 policies para anon (SELECT/INSERT/UPDATE/DELETE)

## Tarefas pendentes
- Atualizar redirect Squarespace /estrategia para github.io URL
- Avisar usuarios da nova URL
- Definir criterios GO/NO-GO dos 2 gates do ciclo empreendimentos
- Padroes operacionais Administrativo/Procurement/Construcao
- Continuar Codigo Sopra v2

## Backup
~/Documents/sopra-backups/YYYY-MM-DD_HH-MM/ diario (30 dias). Logs em _last_run.log.

## Estilo
Ricardo prefere mensagens curtas, decisao por decisao. Push-back honesto bem-vindo. Trabalha geral -> particular.
