# Demo do app da Dra. Larissa

Demonstração estática do app de acompanhamento pediátrico: painel da médica (desktop) e app da família (celular).
Sem backend, sem login real, sem dados reais. Todo o conteúdo é fictício e ilustrativo.

## Arquivos

```
index.html      HTML, CSS e JS da demo (tudo embutido)
manifest.json   permite "Adicionar à tela inicial" (sem service worker)
icon-192.png    ícone do app (ursinho)
icon-512.png
assets/         imagens otimizadas: ursinho, logo, ilustrações, Dra. Larissa
.nojekyll       evita processamento do GitHub Pages
```

## Publicar no GitHub Pages

1. Crie um repositório público no GitHub (ex.: `demo-dra-larissa`).
2. Envie o **conteúdo** desta pasta `app-demo` para a raiz do repositório (pelo site: *Add file › Upload files*, arraste tudo, inclusive a pasta `assets`).
3. No repositório: *Settings › Pages › Build and deployment › Source: Deploy from a branch*, branch `main`, pasta `/ (root)`. Salve.
4. Em 1 a 2 minutos o endereço aparece no topo da mesma página (`https://<usuario>.github.io/demo-dra-larissa/`).

As rotas usam hash (`#/painel/...`, `#/familia/...`), então atualizar a página nunca dá erro 404.

Para testar no computador antes de publicar: dentro desta pasta, rode `python -m http.server 8765` e abra `http://localhost:8765`.

## Reiniciar a demonstração

Os dados ficam no `localStorage` do navegador (cada aparelho tem a sua cópia).
Para voltar ao estado inicial, use o botão **Reiniciar demonstração** no canto superior direito.

Observação: o link da família que vai na mensagem do WhatsApp abre a demo, mas em outro aparelho a publicação feita no seu navegador não aparece, porque não há servidor.

## Roteiro sugerido

1. *Sou a Dra. Larissa* › paciente **Helena** › **Publicar após a consulta**.
2. Medidas, marcos ("Todos atingidos"), diagnóstico (carrega o pacote), "Usar recado sugerido", "Usar um documento de exemplo", **Publicar**.
3. Tela "Publicado": mensagem pronta e **Abrir WhatsApp** (`wa.me` sem número).
4. **Ver como a família vê** › PIN (qualquer 6 dígitos ou "Preencher um PIN de exemplo").
5. Na família: *Mais › Vacinas e triagem* › marcar uma vacina › **Voltar ao painel**: o item aparece como **Não verificado** e **Novo**.

## Tema

Cores, fonte, raios e sombras são variáveis CSS no início do `index.html` (bloco `:root`). Para aplicar o projeto gráfico definitivo, basta trocar os valores ali.

Fonte: Plus Jakarta Sans (Google Fonts), com fonte do sistema como alternativa se estiver sem internet.
A Kaleko 205 Round **não** foi embutida: é uma fonte comercial e o repositório é público, o que distribuiria o arquivo da fonte. Se a licença permitir uso web, dá para incluí-la depois via `@font-face`.

## Decisões tomadas onde o prompt ou as telas eram ambíguos

- **Imagens em `assets/`** em vez de base64 dentro do HTML: o `index.html` continua único para código, e o carregamento fica mais leve.
- **Login da médica**: só e-mail preenchido e botão "Entrar como Dra. Larissa", sem campo de senha, para ninguém digitar uma senha real num site público.
- **PIN**: qualquer combinação de 6 dígitos entra; aviso visível na tela.
- **Ver como a família vê** passa pelo PIN na primeira vez (para mostrar a tela de entrada); há atalho "Preencher um PIN de exemplo".
- **Botão do SAMU** não liga de verdade (evita chamada acidental); mostra um aviso.
- **Documentos**: o arquivo escolhido não é lido nem enviado; a família vê uma página ilustrativa marcada como EXEMPLO. Receitas aparecem com o conteúdo omitido (sem doses).
- **Fotos reais**: a foto da Dra. com um bebê não foi usada (a criança é real). Usei o recorte da Dra. sozinha, o ursinho e as ilustrações em aquarela.
- **Curvas de crescimento**: funções suaves inventadas, rotuladas "Curvas ilustrativas". Não usam as tabelas da OMS.
- **Calendário vacinal**: lista ilustrativa por idade, sem doses em ml nem condutas.
- **Fora do escopo** (Novo paciente, Editor de material, Configurações, Revogar link, Novo diagnóstico, Baixar/Compartilhar PDF, WhatsApp do consultório): mostram "disponível na versão completa".
- **Em breve** em *Mais*: Consultas, Dúvidas e Laserterapia, sem telas.
- **Telas Instalar / Consentimento / Link inválido** não foram feitas.
- Removido do wireframe: "Assinatura digital verificada", "Verificação em duas etapas", "protegidos", "Dados e privacidade/LGPD" — a demo não pode sugerir segurança que não existe.

## O que foi testado

Chromium (navegador embutido do Claude Desktop, Windows 10), nos tamanhos 1366×860 (desktop), 768×1024 (tablet) e 375×812 (celular emulado):

- fluxo completo: login › paciente › publicar (medidas, marcos, diagnóstico, recado, documento) › mensagem pronta › visão da família › registrar vacina › painel mostra "Não verificado";
- todas as telas da família para os 5 pacientes e as telas do painel renderizam sem erro de JavaScript;
- sem rolagem horizontal no celular e no tablet;
- botão Reiniciar.

Não testado: Safari/iPhone real, Android real, Firefox, leitor de tela, "Adicionar à tela inicial".
