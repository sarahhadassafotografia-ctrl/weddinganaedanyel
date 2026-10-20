# Galeria de casamento · Ana & Danyel

Galeria responsiva para celular e computador, criada com Next.js. A página inclui a dedicatória, fotos em ordem cronológica, download individual, link para a pasta do Google Drive e painel privado em `/admin` para alterar a mensagem e ocultar/restaurar fotos na prévia.

## Publicar no GitHub e no Vercel

1. Crie um repositório no GitHub e envie para ele o conteúdo desta pasta.
2. No Vercel, escolha **Add New → Project** e importe o repositório.
3. O Vercel detecta Next.js e pnpm pelo `pnpm-lock.yaml`. Se necessário, configure **Install Command** como `pnpm install --no-frozen-lockfile` e **Build Command** como `pnpm build`.
4. Em **Storage**, crie um armazenamento **Blob** e conecte-o ao projeto. Isso disponibiliza `BLOB_READ_WRITE_TOKEN`, usado para salvar a mensagem e as fotos ocultadas no painel.
5. Em **Settings → Environment Variables**, adicione:

   | Nome | Valor |
   | --- | --- |
   | `ADMIN_PASSWORD` | Crie uma senha privada para o painel `/admin`. |
   | `ADMIN_SESSION_SECRET` | Gere uma chave longa, por exemplo com `openssl rand -base64 32`. |
   | `BLOB_READ_WRITE_TOKEN` | Criada e adicionada ao conectar o Blob ao projeto. |

6. Salve as variáveis e faça um novo deploy. Abra `/admin` e entre com a senha escolhida.

O arquivo `.env.example` mostra os nomes das variáveis sem conter credenciais. Não publique tokens nem senhas no GitHub.

## Atualizar a lista de fotos

As 226 fotos desta prévia e seus horários estão listados em `data/gallery.json`. Os arquivos de foto continuam no Google Drive; o site usa os IDs dessa lista para mostrar miniaturas e oferecer downloads. O link do Drive permite abrir a pasta completa.

Adicionar ou remover arquivos no Drive **não altera automaticamente** `data/gallery.json`. Para atualizar a galeria, edite essa lista e envie as alterações ao GitHub; o Vercel fará um novo deploy. O painel `/admin` permite ocultar e restaurar fotos da prévia sem removê-las do Drive.

## Desenvolvimento local

Requer Node.js 22 ou mais recente e pnpm:

```bash
pnpm install
pnpm dev
```

Crie `.env.local` a partir de `.env.example` e preencha as variáveis para testar o painel e o salvamento localmente. Para compilar:

```bash
pnpm build
```
