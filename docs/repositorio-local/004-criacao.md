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
npm install gulp gulp-sass sass \
    gulp-typescript gulp-pug gulp-uglify \
    gulp-clean-css gulp-terser \
    browser-sync gulp-htmlmin --save-dev
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
$primary-color: #3498db;

body {
    background-color: $primary-color;
    font-family: Arial, sans-serif;
}
  ```
</details>

<details>
  <summary>Clique aqui para ver o código TypeScript</summary>
  ```typescript title="./src/scripts/app.ts"
const greeting: string = "Hello, Gulp!";
console.log(greeting);
  ```  
</details>

<details>
  <summary>Clique aqui para ver o código PUG</summary>
  ```text title="./src/templates/index.pug"
doctype html
html
  head
    title Gulp Project
  body
    h1 Semana da Tecnologia Fatec Taubaté
    p This is a template generated with Pug.

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