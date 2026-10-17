# Transcritor de Aba (Firefox)

Extensão do Firefox que transcreve o áudio da aba atual (aulas e vídeos no YouTube, reuniões no Meet, Teams e Zoom
web, portais de treinamento) e, ao parar, baixa um arquivo `.txt`.

**Objetivo:** criar fontes em `.txt` para alimentar o **[Gemini Notebook](https://notebooklm.google.com)
(antigo NotebookLM)** e estudar com elas depois.

> 🎙️ **O microfone NÃO é transcrito.** Só o áudio que sai da aba entra na transcrição: o professor, o vídeo, os
> outros participantes. A sua voz fica de fora, inclusive a da sua própria imagem numa reunião.

- O idioma é **detectado sozinho** (português, inglês, espanhol e outros): nada a configurar ao trocar de vídeo.
- A transcrição usa o [Groq](https://console.groq.com), **grátis até 8 horas de áudio por dia**, com a sua chave.
- Funciona na **versão mais atual do Firefox** (testada no Firefox 158; exige Firefox 140 ou mais novo).

**Versão atual: 0.5.1** · arquivo: [`transcritor-de-aba-0.5.1-assinado.xpi`](transcritor-de-aba-0.5.1-assinado.xpi)

## Assinada pela Mozilla

O `.xpi` deste repositório é **assinado digitalmente pela Mozilla**, pelo serviço oficial de extensões
[addons.mozilla.org](https://addons.mozilla.org) (AMO), no canal **não listado**: a extensão passa pela validação
automática da Mozilla e recebe a assinatura, mas não aparece na loja pública. É essa assinatura que permite instalar
de forma **permanente** no Firefox comum, que recusa extensões sem assinatura. Ela fica dentro do arquivo
(`META-INF/mozilla.rsa` e `META-INF/cose.sig`), e qualquer alteração no `.xpi` a invalida.

## Primeiros passos

### 1. Instalar

1. Baixe o arquivo **`transcritor-de-aba-0.5.1-assinado.xpi`** deste repositório (clique nele e em **Download**).
2. No Firefox, abra o menu **☰ → Extensões e temas** (ou digite `about:addons` na barra de endereço).
3. Clique na **engrenagem ⚙** ao lado de "Gerenciamento de extensões" e escolha **Instalar de um arquivo…**.
4. Selecione o arquivo baixado.
5. O Firefox mostra o que a extensão pede (acessar os sites e baixar arquivos). Clique em **Adicionar**.
6. **Fixe o ícone na barra:** clique na peça de quebra-cabeça (**Extensões**) no canto superior direito, na
   engrenagem ao lado de "Transcritor de Aba" e em **Fixar na barra de ferramentas**. O ícone roxo com ondas de
   áudio fica visível.

> **Atualizar** para uma versão nova é igual: **Instalar de um arquivo…** com o `.xpi` novo, depois **Atualizar**.
> A chave do Groq e o histórico continuam.

### 2. Criar a chave grátis do Groq (uma vez só)

1. Entre em [console.groq.com/keys](https://console.groq.com/keys) e faça login (Google, GitHub ou e-mail).
2. Clique em **Create API Key**, dê um nome (ex.: "Transcritor") e confirme.
3. **Copie a chave** (começa com `gsk_`). O Groq mostra a chave uma vez só.

### 3. Configurar

1. Clique no ícone da extensão e, no rodapé, em **Configurações** (ou em `about:addons` → **⋯** ao lado de
   "Transcritor de Aba" → **Opções**).
2. Cole a chave no campo **Chave da API**.
3. Clique em **Salvar** e depois em **Testar conexão**. Deve aparecer **"Conexão e chave OK."**

Não é preciso mexer em **Avançado**: serviço (Groq), endereço, modelo (`whisper-large-v3-turbo`) e idioma
(**Detectar sozinho**) já vêm prontos.

### 4. Usar

1. Abra o vídeo ou entre na reunião. Se a aba já estava aberta **antes** de instalar a extensão, recarregue (F5).
2. Dê play. Clique no ícone da extensão e em **Iniciar transcrição**. O ícone ganha o selo vermelho **REC**.
3. Deixe a aba aberta. Pode trocar de aba ou baixar o volume do vídeo: não atrapalha. No popup você acompanha o
   tempo, o nível do áudio, as fontes encontradas, os trechos transcritos e o último texto.
4. No fim, clique no ícone e em **Parar e baixar .txt**. O arquivo vai para a pasta **Downloads**:
   `Transcricao_<data>_<hora>_<título do vídeo>.txt`.
5. No Gemini Notebook: abra o caderno → **Adicionar fonte** → **Fazer upload** → escolha o `.txt`.

Se o download falhar ou você quiser o arquivo de novo, o popup mostra **Últimas transcrições** com o botão
**Baixar**. Se a aba for fechada no meio, a extensão entrega o que já foi transcrito.

### O que vem no `.txt`

```
Transcrição: <título do vídeo ou da reunião>
Fonte: <endereço da página>
Data: 16/10/2026, das 21:59 às 22:00 (1 min)
Transcrito por: Groq / whisper-large-v3-turbo, idioma: Detectar sozinho

[00:00] Primeiro trecho da fala…
[00:13] Segundo trecho…
```

## Dicas e limites

- **O microfone não é transcrito** (veja o aviso no topo).
- **YouTube com dublagem automática:** o YouTube pode tocar o vídeo dublado no idioma do seu navegador. A extensão
  transcreve o que está tocando; para o áudio original, escolha a faixa original na **engrenagem ⚙ do player →
  Faixa de áudio**.
- **Reuniões:** avise os participantes antes de transcrever.
- **Não funciona** em conteúdo protegido por DRM (Netflix, Prime Video) nem em players que tocam áudio de outro site
  sem permissão (CORS); o popup avisa nesses casos.
- Numa conversa com várias pessoas, as falas saem juntas, sem indicar quem falou.
- Nomes próprios raros (hebraico, árabe) podem sair aproximados.
- **Cota grátis do Groq:** 8 h de áudio por dia e 2 h por hora. Se estourar, a extensão espera o tempo que o Groq
  pede e tenta de novo; se ainda assim falhar, o trecho aparece no `.txt` como `[trecho não transcrito: …]`.
- **Privacidade:** o áudio vai, em trechos, direto do seu Firefox para o Groq, com a sua chave; não passa por outro
  servidor. A chave fica guardada só no seu Firefox.

## Como funciona

O Firefox não tem uma API que entregue o áudio de uma aba. A extensão recolhe o áudio **de dentro da página** (players
de vídeo, áudio de reunião e Web Audio), corta em trechos de 12 a 30 s nas pausas da fala, com 1 s de sobreposição
para nenhuma palavra se perder no corte, e envia cada trecho ao Groq. Trechos em silêncio não são enviados. O título
da aba vai como contexto para acertar o vocabulário do assunto, e frases que o modelo inventa no silêncio são
removidas. No fim, os trechos viram o `.txt` com carimbos de tempo.

## Licença

MIT — veja [`LICENSE`](LICENSE) e [`NOTICE.md`](NOTICE.md).

---
Ary Ribeiro · [linkedin.com/in/aryribeiro](https://www.linkedin.com/in/aryribeiro)
