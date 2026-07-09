# Site — André Calazans Advocacia

Site institucional + blog, pronto para hospedar no GitHub Pages, com o blog
gravado no Supabase (banco de dados já criado e configurado).

## Estrutura

```
index.html          → página principal
blog/index.html      → listagem de artigos
blog/post/index.html → artigo individual (?slug=...)
admin/index.html      → painel para publicar artigos (uso restrito seu)
assets/css/style.css  → estilos
assets/js/            → scripts e configuração do Supabase
```

## 1. Publicar no GitHub Pages

1. Crie um repositório novo no GitHub (ex: `andre-calazans-advocacia`).
2. Suba todos os arquivos desta pasta para a raiz do repositório.
3. No GitHub, vá em **Settings → Pages** → em "Source", escolha a branch
   `main` e a pasta `/ (root)`. Salve.
4. Em alguns minutos o site estará em
   `https://SEU-USUARIO.github.io/andre-calazans-advocacia/`.
5. Se quiser um domínio próprio (ex: `www.andrecalazans.adv.br`), configure em
   **Settings → Pages → Custom domain** e aponte o DNS do domínio para o
   GitHub Pages.

## 2. Criar seu usuário de acesso ao painel (/admin)

O banco de dados e a tabela do blog já estão prontos. Falta só criar o seu
login:

1. Acesse [supabase.com](https://supabase.com/dashboard) e entre no projeto
   **andre-calazans-advocacia**.
2. Vá em **Authentication → Users → Add user**.
3. Cadastre seu e-mail e uma senha forte (marque "Auto Confirm User").
4. Pronto — acesse `seusite.com/admin/` e entre com esse e-mail e senha.

Pelo painel você consegue: escrever um artigo novo, escolher a categoria
(Direito do Trabalho ou Direito de Família), publicar ou deixar como
rascunho, e editar o status de artigos já existentes (publicar,
despublicar ou excluir).

Já deixei 2 artigos de exemplo publicados, um de cada área, para o blog não
começar vazio — pode editá-los ou excluí-los quando tiver os seus.

## 3. Antes de publicar, ajuste

- **Endereço completo do escritório**: no momento o site só diz "Barra da
  Tijuca — RJ". Se quiser, me passe o endereço completo e eu insiro no rodapé
  e na seção de contato.
- **E-mail profissional**: se você tiver um e-mail (ex:
  contato@andrecalazans.adv.br), me avise e eu adiciono ao lado do WhatsApp.
- **Redes sociais**: se usar Instagram/LinkedIn profissional, também posso
  incluir ícones no rodapé.

## 4. Um ponto de atenção sobre publicidade de advogados

A OAB tem regras específicas para publicidade e captação de clientela
(Provimento 205/2021 do Conselho Federal, que regulamenta o Código de Ética).
Em linhas gerais, evite no site: promessas de resultado, comparações com
outros advogados, superlativos ("o melhor", "o mais eficiente") e
depoimentos de clientes reais nomeados. Escrevi o conteúdo já pensando nisso
— com foco em clareza, transparência e confiança, sem essas práticas — mas
vale revisar com calma antes de publicar oficialmente, especialmente se
pretende impulsionar o site em redes sociais ou anúncios pagos.

## 5. Configuração técnica (Supabase)

- Projeto: `andre-calazans-advocacia` (região São Paulo — `sa-east-1`)
- Tabela: `public.blog_posts`
- Segurança (RLS): visitantes só enxergam artigos com `published = true`;
  só usuários logados (você, via `/admin`) podem criar, editar ou excluir.
- A chave usada no site (`assets/js/supabase-config.js`) é a chave pública
  ("publishable key"), segura para ficar exposta no código — quem protege os
  dados são as políticas de RLS, não o segredo da chave.
