# Caravan

Site landing page multi-page que simula o portal de uma agência de viagens chamada Caravan. Construído com HTML estático, componentes Bootstrap e assets otimizados para servir informações institucionais, galerias e formulários de contato/inscrição sem necessidade de backend.

## Visão geral

Caravan oferece uma experiência estática porém rica em interações simples (carousel, acordeões, abas e formulários) para apresentar destinos, planos, eventos e canais de contato. O objetivo é servir como base visual para uma eventual plataforma real: cada página (home, locais, planos, contato, inscrição) reutiliza cabeçalho/rodapé fixos e compartilha estilos e scripts locais, garantindo consistência e fácil manutenção.

## Recursos principais

- **Hero interativo** com carousel Bootstrap mostrando destinos (California, Paris, Dublin) e bloco de destaque com formulário rápido de captura de e-mails.
- **Dropdown “Locais”** no menu superior que aponta para a página `local.html`, exibindo galeria, agenda de eventos e CTA para comprar ingressos.
- **Páginas de planos e inscrição** com cards responsivos, listas de benefícios, selects e abas de pagamento (Cartão vs Boleto).
- **Modal de login** reutilizado em todas as páginas para simular autenticação leve.
- **Seção de FAQ** implementada com colapsos (`collapse`) do Bootstrap para responder dúvidas frequentes.
- **Formulário de contato** com inputs e textarea + mapa ilustrativo.
- **Footer comum** com navegação secundária, contatos e botões sociais.
- **Tooltip global** ativado por `src/scripts/app.js`.

## Tech Stack

- **HTML5 sem frameworks SPA** (páginas `index.html`, `planos.html`, `contato.html`, `inscricao.html`, `local.html`)
- **CSS3 + Bootstrap 4** (arquivos compilados em `src/styles/` e fontes Sass em `src/scss/`)
- **Sass** para gerar `src/styles/bootstrap.css` a partir de `src/scss/bootstrap.scss` (incluídos os módulos `_variables`, `_mixins`, `_grid`, etc.)
- **JavaScript (jQuery 3.2.1 Slim + Popper.js)** para dar suporte a plugins Bootstrap (dropdown, collapse, carousel)
- **Scripts customizados** em `src/scripts/app.js` (ativação global de tooltip)

## Estrutura do projeto

```
/
├── index.html            # Landing home com carousel, CTA e FAQ
├── planos.html          # Página de planos com cards e selects
├── contato.html         # Formulário de contato e dados da agência
├── inscricao.html       # Formulário completo para contratar plano
├── local.html           # Galeria de fotos + tabela de eventos
└── src/
    ├── assets/
    │   └── img/         # Fotos, ícones e SVG do logotipo
    ├── scripts/
    │   ├── app.js        # Inicialização de tooltip
    │   ├── bootstrap.js
    │   ├── jquery-3.2.1.slim.min.js
    │   └── popper.min.js
    ├── scss/            # Fonte Sass do Bootstrap (órgãos e módulos `_*.scss`)
    └── styles/
        ├── bootstrap.css # CSS compilado
        └── style.css     # Customizações da Caravan (rodapé, quotes, listas, responsividade)
```

## Primeiros passos

### Pré-requisitos

- Navegador moderno compatível com CSS Flexbox/Grids.
- Ambiente para servir arquivos estáticos (não há servidor embutido).

### Instalação

1. Clone o repositório:

   ```bash
   git clone https://github.com/<seu-usuario>/Caravan.git
   cd Caravan
   ```

2. Opcional: instale um servidor estático rápido (recomendado `http-server` ou `live-server`):
   ```bash
   npm install -g http-server
   ```

### Variáveis de ambiente

O projeto **não depende de variáveis de ambiente**. Qualquer configuração (URLs, textos, preços) é feita diretamente nos arquivos HTML/ CSS.

### Executando o projeto

Escolha um servidor local para testar:

- Usando `http-server`:

  ```bash
  http-server -c-1 -p 8080
  ```

- Ou com Python:
  ```bash
  python -m http.server 8080
  ```

Depois abra `http://localhost:8080` no navegador. Todas as páginas estão no diretório raiz, assim basta navegar pelos links.

## Exemplos de uso

- **Hero + formulário de e-mail rápido**:

  ```html
  <form>
    <div class="input-group input-group-lg">
      <input type="text" class="form-control" placeholder="Email" />
      <span class="input-group-btn">
        <button class="btn btn-primary" type="button">Inscreva-se</button>
      </span>
    </div>
  </form>
  ```

- **Card de plano** com select e CTA:

  ```html
  <div class="bg-light rounded p-4 box-shadow">
    <h2>Gold</h2>
    <ul class="lista-plano list-unstyled">
      <li>→ 30 dias de viagem</li>
      ...
    </ul>
    <a class="btn btn-primary btn-lg btn-block" href="inscricao.html"
      >Comprar Plano</a
    >
  </div>
  ```

- **FAQ** estruturada com collapse:
  ```html
  <a
    class="lead"
    data-toggle="collapse"
    href="#pergunta1"
    aria-controls="pergunta1"
    >→ É possível cancelar?</a
  >
  ```

## Funcionalidade principal

Apesar de ser um projeto estático, a experiência tenta simular um portal real usando:

- **Componentes Bootstrap pré-configurados** (navbar responsiva, modal, carousel, collapse, tab).
- **Scripts locais** garantindo que o tooltip (`data-toggle="tooltip"`) esteja sempre habilitado.
- **Formulários sem backend** mas com markup semântico para futura integração (inputs com `id`, `label` e placeholders).
- **Reaproveitamento de blocos** (mesmo footer, navbar, modais) em todas as páginas mantendo consistência sem layout duplicado.

## Scripts

- `src/scripts/jquery-3.2.1.slim.min.js` — biblioteca mínima para o Bootstrap.
- `src/scripts/popper.min.js` — gerencia posicionamento de tooltips/dropdowns.
- `src/scripts/bootstrap.js` — módulos JavaScript do Bootstrap 4.
- `src/scripts/app.js` — inicializa `$('[data-toggle="tooltip"]').tooltip()` ao carregar a página.

_Observação_: os arquivos JS já estão incluídos nas páginas via `<script>` no final do `body`.

## Boas práticas e decisões arquiteturais

- **Estrutura multi-page** com layout compartilhado reduz duplicidade: basta editar o cabeçalho/rodapé para que todas as páginas reflitam mudanças.
- **Bootstrap + Sass** permite customizar tema (cores, espaçamentos, tipografia) recompilando `src/scss/bootstrap.scss` sempre que necessário.
- **Assets versionados no repositório** garantem offline mode e deployment simples (sem CDN).
- **Progressive enhancement**: cada funcionalidade depende apenas dos scripts do Bootstrap; o conteúdo principal continua acessível mesmo se o JavaScript falhar.

## Como contribuir

1. Fork e crie sua branch (`git checkout -b minha-melhoria`).
2. Adicione commits claros e descritivos.
3. Abra o Pull Request apontando para a branch principal.
4. Priorize consistência com `Bootstrap 4` e evite quebra de layout em telas menores.
5. Documente novas páginas ou assets diretamente neste README.
