# Demo do app da Dra. Larissa

Demonstração estática do app de acompanhamento pediátrico: painel da médica (desktop, também responsivo) e app da família (celular).
Sem backend, sem login real, sem dados reais de pacientes. Todo o conteúdo clínico é fictício e ilustrativo.

## Arquivos

```
index.html      HTML, CSS e JS da demo (tudo embutido)
manifest.json   permite "Adicionar à tela inicial" (sem service worker)
icon-192.png    ícone do app (ursinho)
icon-512.png
assets/         imagens: ursinho, logo, ilustrações e a foto da Dra. Larissa
.nojekyll       evita processamento do GitHub Pages
```

## Publicar no GitHub Pages

1. Crie um repositório público no GitHub (ex.: `demo-dra-larissa`).
2. Envie o **conteúdo** desta pasta `app-demo` para a raiz do repositório.
3. No repositório: *Settings › Pages › Build and deployment › Source: Deploy from a branch*, branch `main`, pasta `/ (root)`.
4. Em 1 a 2 minutos o endereço aparece no topo da mesma página.

As rotas usam hash (`#/painel/...`, `#/familia/...`), então atualizar a página nunca dá erro 404.

Para testar no computador: dentro desta pasta, rode `python -m http.server 8765` e abra `http://localhost:8765`.

## Reiniciar a demonstração

Os dados ficam no `localStorage` do navegador (chave `larissa-demo-v2`; cada aparelho tem a sua cópia).
O botão **Reiniciar demonstração** (canto superior direito) volta tudo ao estado inicial: crianças, agenda, resumos, caderneta, diagnósticos frequentes e publicações.
Se o navegador tiver dados de uma versão anterior da demo, eles são descartados e a demo recomeça sozinha.

O link da família que vai na mensagem do WhatsApp abre a demo, mas em outro aparelho a publicação feita no seu navegador não aparece, porque não há servidor.

## Imagens

### Foto da Dra. Larissa
- `assets/dra-foto.webp` (812×1600, tela de entrada e login) e `assets/dra-avatar-foto.webp` (160×160, avatar circular).
- Origem: `Landing Page/Imagens/IMG_0188-Edit.png` (de jaleco, de frente, fundo transparente).
- **A foto só pode ir para o repositório público depois da autorização da Dra. Larissa.**

### Capa da caderneta (vacinas e triagem)
- `assets/caderneta-topo.jpg` (1200×600): ilustração do ursinho de jaleco com a caderneta, recortada do original quadrado.
- Se o arquivo faltar, aparece um degradê com nuvem, estrela e coração, e a tela funciona normalmente.
- Para trocar: salve a nova imagem com esse nome exato dentro de `assets/`. Não é preciso mexer no código. O enquadramento usa o terço de cima da imagem (`object-position` em `.cad-top img.ph`).

## Tema

Cores, fonte, raios e sombras são variáveis CSS no início do `index.html` (bloco `:root`), incluindo as cores das modalidades da agenda (`--m-on`, `--m-co`, `--m-do`).
Fonte: Plus Jakarta Sans (Google Fonts). A Kaleko 205 Round não foi embutida por ser fonte comercial num repositório público.

Constantes fáceis de mudar no código:
- `DUR`: duração de cada modalidade da agenda (Online 40 min, Consultório 60 min, Domicílio 90 min).
- `VAC` e `TRIAGEM`: lista de exemplo da caderneta.
- `FAQ` e `SINAIS`: perguntas frequentes e sinais de alerta de exemplo da aba Chat.

## Roteiro de verificação (8 passos)

1. **Entrada no celular**: no navegador, use a largura de 360px ou 390px e abra a primeira tela. Nenhum enfeite passa por trás do texto; a foto da Dra. fica ao lado do texto no cartão "Sou a Dra. Larissa".
2. **Lista e blocos**: entre como Dra. Larissa. No celular, a tabela de crianças vem logo abaixo da saudação e os blocos de números somem. No desktop (1280px), os blocos "pacientes acompanhados", "registros novos" e "links não abertos" ficam numa coluna ao lado da tabela.
3. **Acordeão**: toque em **Helena**. A área se abre logo abaixo da linha, com fundo e recuo diferentes, resumo clínico auxiliar e atalho "Agendar". Abrir outra criança fecha a anterior.
4. **Diagnóstico livre**: em "Publicar após a consulta", no item 3, escreva "Otite média", marque dois materiais da biblioteca e publique. Volte a publicar para a Helena: a tag "Otite média" aparece entre os mais usados. Escrever "Bronquiolite" carrega o pacote pronto.
5. **Caderneta**: em "Ver como a família vê" › PIN de exemplo › Início › **Vacinas e triagem**:
   - o aviso de controle compartilhado aparece no topo;
   - marque o "Teste da orelhinha" e a "Pentavalente · 1ª dose": os itens ficam verdes e os contadores mudam ("2/5", "1/4");
   - volte ao painel: Helena aparece com **Novo registro**, que some ao abrir a linha dela.
6. **Conflito de horário**: em **Agenda** › "Adicionar agendamento", escolha Helena, dia 21 deste mês, **Online**, 10:00. Salvar mostra o conflito com Maria Cecília (Domicílio, 09:00 às 10:30) e sugere horários livres. Escolha um.
7. **Família com contagem regressiva**: volte ao app da família da Helena. No Início aparece "Sua próxima consulta" com "faltam N dias"; na aba **Consultas**, o cartão "Agendamento confirmado".
8. **Materiais da consulta**: no Início, toque em **Ver materiais**. Abre "Materiais desta consulta", só com os materiais daquela publicação, data e botão "Voltar".

## Decisões tomadas onde o pedido era ambíguo

- **Diagnóstico com pacote**: o texto digitado é comparado com o nome dos diagnósticos que têm pacote, sem diferenciar maiúsculas nem acentos. Se coincidir, o pacote é carregado; se não, a biblioteca inteira aparece para escolha manual.
  - Diagnósticos novos viram tag ao serem publicados, mas não criam pacote sozinhos.
- **Desmarcar na caderneta**: só pelo botão "Desfazer", que pede confirmação.
- **Origem no painel**: as marcações dos pais aparecem como "Registrado pela família em dd/mm", mais a tag "Novo" enquanto a médica não abriu a criança.
- **Status sem novidade**: um traço neutro (com texto para leitor de tela "Sem novidades da família"). "Em dia" não foi usado porque poderia sugerir vacinação em dia.
- **Contador ao lado de "Criança"**: é só um contador estilizado, sem ação.
- **Conflito de agenda**: vale entre todas as modalidades, sem tempo de deslocamento.
- **Agendar pela família**: o botão abre o WhatsApp com pedido de horário. Quem registra o agendamento é a médica.
- **Resumo clínico**: há um único resumo por criança, e editar sobrescreve, sem histórico de versões. A gravação passa por uma só função (`saveResumo`), para facilitar acrescentar versões depois.
- **WhatsApp do consultório**: abre `wa.me` sem número, porque o repositório é público.
- **Itens que estavam em "Mais"**:
  - Vacinas e triagem: botão no Início.
  - Sinais de alerta: aba Chat.
  - "Dúvidas": virou as perguntas frequentes do Chat.
  - "Consultas": virou aba.
  - "Falar com a Dra.": aba Chat.
  - "Laserterapia (em breve)": rodapé do Início.
  - Não existia item de "dados e privacidade" na demo.
- **Documentos da publicação** (receita, atestado, orientações): continuam no passo 4 de "Publicar". Não são prontuário, e não há upload na área do resumo clínico.

## O que foi testado

Chromium (navegador embutido do Claude Desktop, Windows 10), com tamanhos emulados de 360×780, 390×844, 768×1024 e 1280×860:

- todas as rotas do painel e da família, para as 5 crianças, sem erro de JavaScript;
- sem rolagem horizontal em 360, 390, 768 e 1280;
- fluxo completo do roteiro acima (passos 1 a 8), mais:
  - cadastro de criança pelo agendamento;
  - "manter assim mesmo" no conflito;
  - criar e sobrescrever resumo;
  - desfazer marcação da caderneta;
  - reinício;
  - descarte automático de dados antigos;
- a família não lê o resumo clínico: com um texto-marcador inserido nos resumos, nenhuma tela da família o exibiu.

Não testado: Safari/iPhone real, Android real, Firefox, leitor de tela e "Adicionar à tela inicial".
As animações (expansão com rebote e brilho, confete) não puderam ser vistas em movimento: o painel do navegador estava oculto durante os testes, e nesse estado o navegador pausa as animações. Só os estados final e inicial foram conferidos.
