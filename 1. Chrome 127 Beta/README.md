# Chrome 127 Beta

Salvo indicação em contrário, as alterações a seguir se aplicam à versão mais recente do canal beta do Chrome para Android, ChromeOS, Linux, macOS e Windows. Saiba mais sobre os recursos listados aqui por meio dos links fornecidos ou da lista em [ChromeStatus.com](https://www.chromestatus.com/). O Chrome 127 está na versão beta em 12 de junho de 2024. Você pode baixar a versão mais recente em [Google.com](https://www.google.com/chrome/) para desktop ou na [Google Play Store](https://play.google.com/store/apps/details?id=com.android.chrome) para Android.

## Novos Recursos CSS

### Ajuste do Tamanho da Fonte CSS

A propriedade `font-size-adjust` fornece uma maneira de modificar o tamanho das letras minúsculas em relação ao tamanho das letras maiúsculas, o que define o tamanho geral da fonte. Esta propriedade é útil para situações em que pode ocorrer fallback de fonte.

#### Exemplo

```css
body {
  font-size: 16px;
  font-size-adjust: 0.58;
}
```

### Texto Alternativo com Vários Argumentos em Conteúdo Gerado por CSS

A propriedade CSS `content` permite especificar texto alternativo para acessibilidade com a seguinte sintaxe:

```css
.has-before-content::before {
  content: url("cat.jpg") / "A cute cat";
}
```

A partir do Chrome 127, o texto alternativo pode ser dado por um número arbitrário de elementos, que além de strings podem ser `attr()` funções ou contadores.

#### Exemplo

```css
.has-before-content::before {
  content: url("cat.jpg") / "A cute " attr(data-animal);
}
```

### Suporte para Transições de Visualização em Iframes

A partir do Chrome 127, transições simultâneas de visualização do mesmo documento em um quadro principal e iframe de mesma origem estarão disponíveis.

#### Exemplo

```javascript
document.startViewTransition(() => {
  // Código de transição
});

iframeDocument.startViewTransition(() => {
  // Código de transição no iframe
});
```

## APIs da Web

### Adições ao Relatório de Atribuição

O Chrome 127 inclui dois recursos adicionais para relatórios de atribuição:

- **Relatórios de Depuração Agregada**: Permite que os chamadores da API continuem recebendo informações de depuração mesmo após a descontinuação de cookies de terceiros.
- **Escopos de Atribuição**: Fornece mais controle sobre a filtragem de atribuição.

### Configuração Automática de Conteúdo em Tela Cheia

Uma nova configuração de conteúdo de “tela cheia automática” permite que os administradores corporativos permitam que os sites entrem em tela cheia sem um gesto do usuário. 

#### Exemplo

```html
<button onclick="enterFullscreen()">Entrar em Tela Cheia</button>

<script>
function enterFullscreen() {
  if (document.documentElement.requestFullscreen) {
    document.documentElement.requestFullscreen();
  }
}
</script>
```

### Documentar Picture-in-Picture: Propagar a Ativação do Usuário

Isso torna as ativações do usuário em uma janela picture-in-picture de documento utilizáveis dentro da janela de abertura e vice-versa.

#### Exemplo

```javascript
const pipWindow = document.querySelector('video').requestPictureInPicture();

// Permitir que a ativação do usuário seja propagada
pipWindow.document.addEventListener('click', () => {
  // Ação a ser realizada na janela de abertura
});
```

### Integridade do Mapa de Importação

Este recurso adiciona uma `integrity` seção para importar mapas, permitindo que os desenvolvedores mapeiem URLs de módulos ES para seus metadados de integridade.

#### Exemplo

```json
{
  "imports": {
    "example": {
      "url": "https://example.com/module.js",
      "integrity": "sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/ux/h51dP1s"
    }
  }
}
```

### Contêineres de Rolagem com Foco no Teclado

Os scrollers são focalizáveis por clique e programaticamente por padrão. Scrollers sem filhos focalizáveis são focalizáveis pelo teclado por padrão.

#### Exemplo

```css
.scroll-container {
  overflow: auto;
  outline: none;
}

.scroll-container:focus {
  border: 2px solid blue;
}
```

## Suporte No-Vary-Search para Pré-renderização

Estende o suporte No-Vary-Search para pré-renderização além do suporte de pré-busca anterior.

#### Exemplo

```http
HTTP/1.1 200 OK
No-Vary-Search: *
```

## Capítulo de Vídeo em MediaMetadata

Agora você pode adicionar informações de capítulos individuais, como o título da seção, seu carimbo de data/hora e uma imagem de captura de tela aos metadados de mídia.

#### Exemplo

```javascript
navigator.mediaSession.metadata = new MediaMetadata({
  title: 'Podcast Title',
  chapters: [
    { start: 0, title: 'Introduction' },
    { start: 300, title: 'Main Content' }
  ]
});
```

## WebGPU: Atributo de Informações do GPUAdapter

Adiciona um atributo de informações GPUAdapter síncrono para recuperar as mesmas informações sobre o adaptador físico que o método `requestAdapterInfo()` assíncrono.

#### Exemplo

```javascript
const adapter = await navigator.gpu.requestAdapter();
console.log(adapter.info);
```

## Testes de Origem em Andamento

No Chrome 127, você pode ativar os seguintes novos testes de origem:

- **Transporte de Dicionário de Compactação com Shared Brotli e Shared Zstandard**

#### Exemplo

```http
HTTP/1.1 200 OK
Content-Encoding: br
X-Brotli-Shared-Dictionary: /path/to/dictionary
```

## Depreciações e Remoções

### Eventos de Mutação

O suporte a eventos de mutação será desativado por padrão a partir do Chrome 127. O código deve ser migrado antes dessa data para evitar quebras do site.

#### Exemplo

**Antes:**

```javascript
document.addEventListener('DOMNodeInserted', callback);
```

**Depois:**

```javascript
const observer = new MutationObserver(callback);
observer.observe(document, { childList: true });
```

### Restringir "Solicitações de Rede Privada" para Sub-recursos de Sites Públicos para Contextos Seguros

Requer que as solicitações de rede privada para sub-recursos de sites públicos só possam ser iniciadas a partir de um contexto seguro.

#### Exemplo

```http
Referrer-Policy: strict-origin-when-cross-origin
```

### Remover a Antiga Sintaxe de Estado Personalizado CSS

A pseudoclasse de estado personalizado CSS está sendo renomeada de `:--foo` para `:state(foo)`.

#### Exemplo

**Antes:**

```css
:--example {
  color: red;
}
```

**Depois:**

```css
:state(example) {
  color: red;
}
```

---

Essa documentação cobre as principais mudanças e adições no Chrome 127 beta. Para mais detalhes, visite [ChromeStatus.com](https://www.chromestatus.com/).