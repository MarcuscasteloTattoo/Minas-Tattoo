# Minas Tattoo

Site do tatuador Anderson, o Minas: tatuagem realista de alto padrão. A página tem o banner, os projetos recentes em carrossel, o portfólio, o "Quem sou", a nota no Google, o valor médio de uma tatuagem e os botões de orçamento pelo WhatsApp.

É um site estático: um `index.html` e a pasta `assets/` com as fotos. Não precisa de build nem de instalação. As fontes vêm do Google Fonts.

## Testar no computador

Abra o `index.html` no navegador (dois cliques no arquivo).

## Publicar

Funciona em qualquer hospedagem de site estático. Envie o `index.html`, os ícones (`favicon-minas.png`, `apple-touch-icon-minas.png`, `favicon.png` e `apple-touch-icon.png`) e a pasta `assets/` juntos, mantendo a estrutura.

- **GitHub Pages:** neste repositório, vá em Settings → Pages → *Deploy from a branch* → `main` / `(root)`.
- **Vercel ou Netlify:** importe este repositório; não há comando de build.
- **Hostinger, Locaweb e similares:** envie os arquivos para a pasta `public_html`.

## Idiomas

O site abre sempre em português. Os botões no canto superior direito (PT, EN, ES) traduzem a página inteira, inclusive a mensagem do WhatsApp. Um link terminado em `?lang=en` ou `?lang=es` já abre em inglês ou espanhol.

Os textos em inglês e espanhol ficam no objeto `I18N`, no fim do `index.html`. Ao mudar um texto em português, mude também nas duas traduções.

## Onde editar

No fim do `index.html`, dentro do `<script>`, o objeto `site` guarda o conteúdo que muda com frequência:

- `estilos`: os cards do carrossel "Projetos recentes" (título, texto, foto e descrição da foto).
- `portfolio`: as fotos do portfólio, na ordem em que aparecem. Todas aparecem de uma vez. Para mostrar só as primeiras e esconder o resto no botão "Ver portfólio completo", troque `PF_VISIVEIS` no `<script>` por um número (ex.: 12). Para acrescentar, coloque a foto em `assets/` e adicione `{ src: "assets/nome.webp", alt: "descrição" }`.
- `avaliacoes`: avaliações do Google (nome, tempo, avatar, texto), mostradas em carrossel abaixo da nota (5,0, 41 avaliações). O `avatar` é a foto do cliente (quadrada, em `assets/`); sem ela aparecem as iniciais do nome. Cada avaliação precisa da tradução em `I18N.en.avaliacoes` e `I18N.es.avaliacoes`. Sem nenhuma avaliação, a seção mostra só a nota e o link para o Google; as que têm `foto` aparecem primeiro e abrem ampliadas ao toque. A nota e o total ficam no HTML e nas traduções (`avNota`, `avTotal`).
- `whatsappBase` e `mensagemWhatsApp`: número do WhatsApp e mensagem inicial do formulário de orçamento.
- `webhookUrl`: link do webhook que recebe os pedidos de orçamento. Enquanto estiver vazio, o formulário só abre o WhatsApp.

## Formulário de orçamento

Na seção de valores, o visitante preenche nome, telefone (com máscara brasileira, `(31) 99999-9999`) e quando quer tatuar (de imediato, em até 15 dias, em até 30 dias ou só pesquisando). Ao enviar:

- **Webhook** (`webhookUrl`): recebe um POST `application/x-www-form-urlencoded`, cada informação em um campo separado: `nome`, `telefone` (ex.: `(35) 99710-9309`), `telefone_whatsapp` (ex.: `+5535997109309`), `quando_tatuar`, `data` (`dd/mm/aaaa`), `hora` (`hh:mm`, horário de Brasília), `data_hora`, `idioma`, `origem` e `pagina`.
- **WhatsApp**: abre a conversa só com a mensagem de orçamento, o nome e quando quer tatuar. O telefone vai apenas para o webhook.

As opções de "quando quer tatuar" ficam no HTML (`<select id="f-quando">`); o valor enviado ao webhook é sempre em português, mesmo com o site em inglês ou espanhol.

Ficam direto no HTML: textos do banner, do "Quem sou" e do valor médio e o link do Instagram.

## Fotos

Os nomes das fotos descrevem a tatuagem e terminam em `-minas-tattoo`, para ajudar a busca do Google.

- `assets/tatuador-minas-tattoo-banner.webp`: foto do banner
- `assets/anderson-minas-tattoo-quem-sou.webp`: foto do "Quem sou"
- `assets/tatuagem-*-minas-tattoo.webp`: fotos do carrossel "Projetos recentes" e do portfólio

As fotos de tatuagem têm versões menores com `-480` e `-360` no nome, e o banner e o "Quem sou" têm versões `-420` e `-720`. O celular carrega a versão menor e o computador a maior. Ao trocar uma foto, troque todas as versões e mantenha o nome descritivo, começando por `tatuagem-` (é o que liga as versões menores no código).

O texto alternativo (`alt`) de cada foto fica no objeto `site` e nas traduções `I18N`, sempre citando o tipo de tatuagem e o Minas Tattoo.

## SEO

No `<head>` ficam o título da página, a descrição, as palavras-chave, os dados para redes sociais (`og:`) e um bloco `application/ld+json` que apresenta o estúdio ao Google, com WhatsApp, Instagram e faixa de preço. Quando tiver o endereço do estúdio e o domínio do site, acrescente um `address` (cidade, rua e CEP) nesse bloco e troque os caminhos das imagens por endereços completos.

## Desempenho

`_headers` (Netlify e Cloudflare Pages) e `vercel.json` (Vercel) mandam o navegador guardar as fotos em cache por 1 ano. Por isso, ao trocar uma foto, use um nome de arquivo novo em vez de substituir o arquivo com o mesmo nome. No GitHub Pages esses arquivos não têm efeito.

O ícone do site usa os arquivos `favicon-minas.png` e `apple-touch-icon-minas.png`. Ao trocar o ícone, use um nome de arquivo novo e atualize as duas linhas `<link rel="icon">` e `<link rel="apple-touch-icon">` no `index.html`, porque o navegador guarda o ícone antigo por até uma semana.
