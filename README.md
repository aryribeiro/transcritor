<p align="center"><img width="283" height="292" alt="print" src="https://github.com/user-attachments/assets/67e601d6-e4fb-4edd-aaf0-4f1bffc21e45" /></p>

# Transcritor de Aba (Firefox)

Extensão do Firefox que transcreve o áudio da aba atual (aulas e vídeos no YouTube, reuniões no Meet, Teams e Zoom
web, portais de treinamento) e, ao parar, baixa um arquivo `.txt`.

**Objetivo:** criar fontes em `.txt` para alimentar o **[Gemini Notebook](https://notebooklm.google.com)
(antigo NotebookLM)** e estudar com elas depois.

> 🎙️ **O microfone NÃO é transcrito.** Só o áudio que sai da aba entra na transcrição: o professor, o vídeo, os
> outros participantes. A sua voz fica de fora, inclusive a da sua própria imagem numa reunião.

- A transcrição é feita por uma **API gratuita** ([Groq](https://console.groq.com), modelo Whisper
  large-v3-turbo): **sem custo até 8 horas de áudio por dia**, em **português, inglês e espanhol**, com o
  idioma **detectado sozinho**. Você só precisa criar uma chave grátis.
- Funciona na **versão mais atual do Firefox** (testada no Firefox 158; exige Firefox 140 ou mais novo).

**Versão atual: 0.5.1** · arquivo: [`transcritor-de-aba-0.5.1-assinado.xpi`](transcritor-de-aba-0.5.1-assinado.xpi)
(também em [Releases](https://github.com/aryribeiro/transcritor/releases/latest))

> ⚠️ **A transcrição depende de um serviço externo (Groq).** A extensão captura o áudio e monta o `.txt`; quem
> transforma a fala em texto é a API do Groq. Disponibilidade, limites do plano grátis e modelos são definidos pelo
> Groq e podem mudar sem aviso. Se a transcrição parar, veja [Se algo não funcionar](#se-algo-não-funcionar): ali dá
> para saber em um minuto se o problema é a sua chave, a sua internet, o Groq ou a página.

## Assinada pela Mozilla

O `.xpi` deste repositório é **assinado digitalmente pela Mozilla**, pelo serviço oficial de extensões
[addons.mozilla.org](https://addons.mozilla.org) (AMO), no canal **não listado**: a extensão passa pela validação
automática da Mozilla e recebe a assinatura, mas não aparece na loja pública. É essa assinatura que permite instalar
de forma **permanente** no Firefox comum, que recusa extensões sem assinatura. Ela fica dentro do arquivo
(`META-INF/mozilla.rsa` e `META-INF/cose.sig`), e qualquer alteração no `.xpi` a invalida.

## O que você precisa

| Item | Detalhe |
|---|---|
| Firefox | versão 140 ou mais nova, no computador (Windows, macOS ou Linux) |
| Internet | os trechos de áudio vão para a API do Groq durante a transcrição |
| Conta grátis no Groq | para criar a **chave da API** (passo 2) |
| O arquivo da extensão | `transcritor-de-aba-0.5.1-assinado.xpi` (passo 1) |

## Passo a passo (primeira vez)

Leva uns 5 minutos. Depois disso, o uso diário é só **Iniciar** e **Parar**.

### 1. Instalar a extensão

1. Baixe o arquivo **`transcritor-de-aba-0.5.1-assinado.xpi`**: em
   [Releases](https://github.com/aryribeiro/transcritor/releases/latest), clique no nome do arquivo (ou, na lista
   de arquivos deste repositório, clique nele e no botão de download).
2. No Firefox, abra o menu **☰ → Extensões e temas** (ou digite `about:addons` na barra de endereço).
3. Clique na **engrenagem ⚙** ao lado de "Gerenciamento de extensões" e escolha **Instalar de um arquivo…**.
4. Selecione o arquivo baixado.
5. O Firefox mostra o que a extensão pede (acessar os dados dos sites e baixar arquivos). Clique em **Adicionar**.
6. **Fixe o ícone na barra:** clique na peça de quebra-cabeça (**Extensões**) no canto superior direito, na
   engrenagem ao lado de "Transcritor de Aba" e em **Fixar na barra de ferramentas**. O ícone roxo com ondas de
   áudio fica visível.

### 2. Criar a chave grátis da API do Groq

1. Entre em [console.groq.com/keys](https://console.groq.com/keys) e crie a conta ou faça login (Google, GitHub ou
   e-mail).
2. Clique em **Create API Key**, dê um nome (ex.: "Transcritor") e confirme.
3. **Copie a chave** (começa com `gsk_`). O Groq mostra a chave uma vez só; se perder, é só criar outra.

### 3. Configurar a extensão

1. Clique no ícone da extensão e, no rodapé, em **Configurações** (ou em `about:addons` → **⋯** ao lado de
   "Transcritor de Aba" → **Opções**).
2. Cole a chave no campo **Chave da API**.
3. Clique em **Salvar** e depois em **Testar conexão**. Tem de aparecer **"Conexão e chave OK."** Se aparecer
   outra mensagem, veja [Se algo não funcionar](#se-algo-não-funcionar).

Não é preciso mexer em **Avançado**: serviço (Groq), endereço, modelo (`whisper-large-v3-turbo`) e idioma
(**Detectar sozinho**) já vêm prontos.

### 4. Transcrever pela primeira vez

1. Abra o vídeo ou entre na reunião. Se a aba já estava aberta **antes** de instalar a extensão, recarregue (F5).
2. Dê **play**. Clique no ícone da extensão e em **Iniciar transcrição**. O ícone ganha o selo vermelho **REC**.
3. Abra o popup de novo depois de uns 30 segundos e confira: **Fontes** mostra "vídeo/áudio 1" (ou "reunião"),
   **Nível do áudio** se mexe e **Trechos** começa a contar. Isso confirma que está funcionando.
4. Deixe a aba aberta. Pode trocar de aba ou baixar o volume do vídeo: não atrapalha.
5. No fim, clique no ícone e em **Parar e baixar .txt**. O arquivo vai para a pasta **Downloads**:
   `Transcricao_<data>_<hora>_<título do vídeo>.txt`.
6. No Gemini Notebook: abra o caderno → **Adicionar fonte** → **Fazer upload** → escolha o `.txt`.

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

## Se algo não funcionar

**Primeiro teste, sempre:** Configurações → **Testar conexão**.

- Se der **"Conexão e chave OK."**, a chave e o Groq estão funcionando; o problema está na página (veja a segunda
  tabela).
- Se der outra mensagem, o problema está na chave, na internet ou no Groq (primeira tabela), não na extensão.
- Para saber se o Groq está fora do ar ou instável, veja a página oficial de status: **[groqstatus.com](https://groqstatus.com)**.

### Problemas com a API (chave, internet ou Groq)

Aparecem no **Testar conexão**, no popup ("Último erro: …"), como selo **ERR** no ícone, ou dentro do `.txt` como
`[trecho não transcrito: …]`.

| Mensagem | O que significa | O que fazer |
|---|---|---|
| **Chave recusada (HTTP 401)** / "o serviço recusou a chave" / selo **ERR** | a chave está errada, foi apagada ou a conta do Groq foi bloqueada | crie uma chave nova em [console.groq.com/keys](https://console.groq.com/keys), cole em Configurações e **Salvar** |
| **Sem conexão com …** / "sem conexão com o serviço" | sem internet, ou o Groq não respondeu | confira a internet; veja [groqstatus.com](https://groqstatus.com) |
| "tempo esgotado" | o Groq demorou demais para responder | geralmente é instabilidade do Groq; tente de novo mais tarde |
| **limite de uso do serviço atingido (HTTP 429)** | a cota grátis acabou (8 h de áudio por dia, 2 h por hora) | a extensão já espera e tenta de novo sozinha; se continuar, espere a cota renovar |
| **HTTP 500, 502, 503** | o Groq está com problema | veja [groqstatus.com](https://groqstatus.com) e tente mais tarde |
| **HTTP 400 ou 404** citando o modelo (ex.: "model … decommissioned / not found") | o Groq aposentou ou mudou o modelo | veja os modelos atuais em [console.groq.com/docs/models](https://console.groq.com/docs/models) e troque o **Modelo** em Configurações → Avançado (procure um "whisper") |

Se o Groq mudar o plano grátis ou sair do ar por muito tempo, dá para usar outro serviço compatível em
Configurações → **Avançado → Serviço** (ex.: OpenAI, que é pago), com a chave dele.

### Problemas na página (o Groq está OK)

| O que aparece no popup | O que significa | O que fazer |
|---|---|---|
| "A extensão ainda não está nesta página. Recarregue a aba (F5)" | a aba foi aberta antes de instalar a extensão | recarregue a aba (F5) e inicie de novo |
| **Fontes:** "nenhuma ainda (dê play)" | nenhum áudio tocando | dê play no vídeo ou entre na chamada |
| "o Firefox bloqueou o áudio desta página: clique nela uma vez" | o Firefox exige um clique na página antes de liberar o áudio | clique uma vez em qualquer lugar da página |
| "conteúdo protegido (DRM, como Netflix)…" | o Firefox não deixa capturar conteúdo com DRM | não há como transcrever esse conteúdo |
| "um player toca áudio de outro site sem permissão (CORS)…" | o site toca o áudio de um servidor que não autoriza a captura | não há como transcrever esse player |
| "Esta aba não pode ser transcrita (só páginas http/https)" | páginas internas do Firefox (`about:`, `moz-extension:`, arquivos locais) | use numa página da web (http/https) |

## Dicas e limites

- **O microfone não é transcrito** (veja o aviso no topo).
- **YouTube com dublagem automática:** o YouTube pode tocar o vídeo dublado no idioma do seu navegador. A extensão
  transcreve o que está tocando; para o áudio original, escolha a faixa original na **engrenagem ⚙ do player →
  Faixa de áudio**.
- **Reuniões:** avise os participantes antes de transcrever.
- Numa conversa com várias pessoas, as falas saem juntas, sem indicar quem falou.
- Nomes próprios raros (hebraico, árabe) podem sair aproximados.
- **Privacidade:** o áudio vai, em trechos, direto do seu Firefox para o Groq, com a sua chave; não passa por outro
  servidor. A chave fica guardada só no seu Firefox.
- **Atualizar** para uma versão nova: **Instalar de um arquivo…** com o `.xpi` novo, depois **Atualizar**. A chave
  e o histórico continuam.

## Como funciona

O Firefox não tem uma API que entregue o áudio de uma aba. A extensão recolhe o áudio **de dentro da página** (players
de vídeo, áudio de reunião e Web Audio), corta em trechos de 12 a 30 s nas pausas da fala, com 1 s de sobreposição
para nenhuma palavra se perder no corte, e envia cada trecho à API do Groq. Trechos em silêncio não são enviados. O
título da aba vai como contexto para acertar o vocabulário do assunto, e frases que o modelo inventa no silêncio são
removidas. No fim, os trechos viram o `.txt` com carimbos de tempo.

## Licença

MIT — veja [`LICENSE`](LICENSE) e [`NOTICE.md`](NOTICE.md). O Groq é um serviço de terceiros, com termos próprios;
a licença desta extensão não cobre o serviço.

---
Ary Ribeiro · [linkedin.com/in/aryribeiro](https://www.linkedin.com/in/aryribeiro)
