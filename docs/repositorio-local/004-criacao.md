---
id: repo-intro-aprendizagem-criacao
title: Mão na massa
sidebar_label: Mão na massa
sidebar_position: 4
---

# Etapas para criacao do projeto e conceitos de versionamento

## Vamos criar nosso projeto

Reproduca os seguintes comandos para criar o diretório da nossa aplicação de exemplo

```bash
cd <diretorio_base>
mkdir controle-biblioteca
cd controle-biblioteca
```

### Definindo o nome do nosso branch principal

```bash
git config --global init.defaultBranch main
```

### Iniciando o versionamento

```bash
git init
```

### Criando o nosso projeto node

```bash
npm init -y
```

### Adicionando as nossas dependências

```bash
npm install gulp gulp-sass sass gulp-typescript gulp-pug gulp-uglify gulp-clean-css gulp-terser browser-sync gulp-htmlmin --save-dev
```

### Criando nosso arquivo gulpfiles

<details>
  <summary>Clique aqui para ver o código do Gulp</summary>
```javascript title="gulpfile.js"
const gulp = require('gulp');
const sass = require('gulp-sass')(require('sass'));
const ts = require('gulp-typescript');
const pug = require('gulp-pug');
const uglify = require('gulp-terser');
const cleanCSS = require('gulp-clean-css');
const htmlmin = require('gulp-htmlmin');
const browserSync = require('browser-sync').create();

// Configurações dos caminhos dos arquivos
const paths = {
  styles: {
    src: 'src/styles/**/*.scss',
    dest: 'dist/css/'
  },
  scripts: {
    src: 'src/scripts/**/*.ts',
    dest: 'dist/js/'
  },
  templates: {
    src: 'src/templates/**/*.pug',
    dest: 'dist/'
  }
};

// Compilar Sass para CSS
function styles() {
  return gulp.src(paths.styles.src)
    .pipe(sass().on('error', sass.logError))
    .pipe(cleanCSS()) // Minificar CSS
    .pipe(gulp.dest(paths.styles.dest))
    .pipe(browserSync.stream()); // Atualizar o browser
}

// Compilar TypeScript para JavaScript
function scripts() {
  return gulp.src(paths.scripts.src)
    .pipe(ts())
    .pipe(uglify()) // Minificar JS
    .pipe(gulp.dest(paths.scripts.dest))
    .pipe(browserSync.stream()); // Atualizar o browser
}

// Compilar Pug para HTML
function templates() {
  return gulp.src(paths.templates.src)
    .pipe(pug())
    .pipe(htmlmin({ collapseWhitespace: true })) // Minificar HTML
    .pipe(gulp.dest(paths.templates.dest))
    .pipe(browserSync.stream()); // Atualizar o browser
}

// Servir o projeto e assistir mudanças
function serve() {
  browserSync.init({
    server: {
      baseDir: './dist' // Servir arquivos da pasta dist
    }
  });

  // Observar mudanças nos arquivos e recompilar
  gulp.watch(paths.styles.src, styles);
  gulp.watch(paths.scripts.src, scripts);
  gulp.watch(paths.templates.src, templates);
}

// Tarefa build apenas executa os passos de build e termina
const build = gulp.series(styles, scripts, templates);

// Definir tarefas padrão
exports.styles = styles;
exports.scripts = scripts;
exports.templates = templates;
exports.serve = serve;
exports.build = build;
exports.default = build;

```
</details>

### Nossos artefatos de código

<details>
  <summary>Clique aqui para ver o código SCSS</summary>
  ```css title="./src/styles/main.scss"
$red: #d32f2f;
$black: #000;
$white: #fff;
$gray: #f5f5f5;
$light-gray: #e0e0e0;

body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background-color: $gray;
  color: $black;
}

.navbar {
  background-color: $light-gray;
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);

  .logo img {
    width: 100px;
  }

  nav ul {
    list-style: none;
    display: flex;
    gap: 20px;

    a {
      color: $black;
      text-decoration: none;
      font-weight: bold;

      &:hover {
        color: $red;
      }
    }
  }
}

.hero {
  background-color: $red;
  color: $white;
  text-align: center;
  padding: 80px 20px;

  h1 {
    font-size: 48px;
    margin-bottom: 20px;
  }

  p {
    font-size: 24px;
    margin-bottom: 40px;
  }

  .btn-primary {
    background-color: $black;
    color: $white;
    padding: 15px 30px;
    border: none;
    text-decoration: none;
    font-size: 18px;
    border-radius: 5px;

    &:hover {
      background-color: $white;
      color: $black;
    }
  }
}

.features,
.about,
.contact {
  background-color: $white;
  padding: 50px 20px;

  .container {
    max-width: 1200px;
    margin: 0 auto;
    text-align: center;

    h2 {
      color: $red;
      font-size: 36px;
      margin-bottom: 30px;
    }

    .feature-box {
      margin: 20px;

      i {
        font-size: 50px;
        color: $black;
      }

      h3 {
        margin-top: 10px;
        font-size: 24px;
      }
    }
  }
}

footer {
  background-color: $black;
  color: $white;
  text-align: center;
  padding: 20px 0;

  p {
    margin: 0;
  }
}

  ```
</details>

<details>
  <summary>Clique aqui para ver o código TypeScript</summary>
  ```typescript title="./src/scripts/app.ts"
document.addEventListener("DOMContentLoaded", () => {
    const nav = document.querySelector(".navbar nav");
    const toggleNav = () => nav?.classList.toggle("active");

    document.querySelector(".navbar")?.addEventListener("click", toggleNav);
    
});
  ```  
</details>

<details>
  <summary>Clique aqui para ver o código PUG</summary>
  ```text title="./src/templates/index.pug"
doctype html
html(lang="pt-BR")
  head
    title Sistema de Gestão da Biblioteca | Fatec Taubaté
    meta(charset="UTF-8")
    meta(name="viewport" content="width=device-width, initial-scale=1.0")
    link(rel="stylesheet" href="css/main.css")


  body
    header.navbar
      .logo
        img(src="https://jcristiano.github.io/doc-oficina-git-fatec/img/fatec_logo.png", alt="Logo Fatec Taubaté")
      nav
        ul
          li: a(href="#features") Funcionalidades
          li: a(href="#about") Sobre
          li: a(href="#contact") Contato

    section.hero
      .container
        h1 Sistema de Gestão da Biblioteca
        p A solução completa para o gerenciamento da sua biblioteca.
        a.btn.btn-primary(href="#features") Explore as funcionalidades

    section#features.features
      .container
        h2 Funcionalidades
        .feature-box
          i.icon-book
          h3 Gestão de Livros
          p Controle total sobre o acervo da biblioteca.
        .feature-box
          i.icon-user
          h3 Controle de Usuários
          p Gestão eficiente de alunos e professores.
        .feature-box
          i.icon-calendar
          h3 Empréstimos e Devoluções
          p Sistema de empréstimos ágil e fácil.

    section#about.about
      .container
        h2 Sobre
        p O Sistema de Gestão da Biblioteca da Fatec Taubaté foi desenvolvido para atender as necessidades de gerenciamento de bibliotecas acadêmicas com tecnologia avançada e acessível.

    section#contact.contact
      .container
        h2 Contato
        p Para mais informações, entre em contato pelo e-mail: contato@fatectaubate.edu.br

    footer
      .container
        p &copy; 2024 Fatec Taubaté. Todos os direitos reservados.
    script(src="scripts/main.js")


  ```  
</details>

### Ajuste do arquivo package.json

Ajuste o arquivo para ter a seguinte entrada.

```js title="package.json"
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "gulp build",
    "watch": "gulp watch",
    "serve": "gulp serve"
},

```
