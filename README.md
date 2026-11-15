# atomicwebai.github.io

Esta é a página principal do meu site.

## Subprojetos

* base64
* unicode
* contador

## Deploy no GitHub Pages

Há duas formas de publicar, dependendo de como o site é construído. Nos dois casos, o workflow publica após um push para a branch `main` e também pode ser iniciado manualmente pela aba **Actions**.

### 1. HTML estático

Use esta opção para páginas HTML, CSS e JavaScript que já estão prontas no repositório e não precisam de compilação. O exemplo está em [`static.yml`](doc/static.yml).

O workflow faz checkout do repositório, configura o Pages e envia o conteúdo da raiz (`.`) como artefato. Não instala dependências nem executa um build; os arquivos publicados precisam estar prontos no próprio repositório.

### 2. React + Vite

Use esta opção quando o site precisa ser compilado. O exemplo está em  [`vite.yml`](doc/vite.yml).

O workflow configura o Node.js 20, instala as dependências com `npm ci`, executa `npm run build` e envia somente o diretório `dist/` como artefato para o Pages. Assim, a saída compilada é publicada em vez dos arquivos-fonte.

Para que o build funcione, o `package.json` deve definir os scripts e dependências necessários, incluindo o script `build`. O lockfile (por exemplo, `package-lock.json`) deve estar versionado, pois `npm ci` o utiliza.

#### Base do Vite

Em projetos publicados em `https://<usuario>.github.io/<repositorio>/`, configure `base` no `vite.config.js` ou `vite.config.ts` com o caminho do repositório:

```javascript
export default defineConfig({
  // ...
  base: '/<repositorio>/',
})
```

Para um site de usuário/organização publicado na raiz (`https://<usuario>.github.io/`), use `base: '/'`. O campo `homepage` no `package.json` não é necessário para configurar o caminho base do Vite; use a opção `base`.

### Configuração do repositório

Para qualquer uma das opções, em **Settings → Pages → Build and deployment**, defina **Source** como **GitHub Actions**. O workflow do repositório precisa estar em `.github/workflows/`.

### Diferença principal

| Tipo de site | Etapas do workflow | Artefato publicado |
| --- | --- | --- |
| HTML estático | Envia os arquivos existentes, sem build | Raiz do repositório (`.`) |
| React + Vite | Instala dependências e executa `npm run build` | Saída do Vite (`dist/`) |
