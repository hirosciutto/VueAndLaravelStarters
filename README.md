# 構成

## ネットワーク
■http://api.ofstest.com/  
┗API
┗laravelのindex.php(/vagrant/api/public/index.php)に接続  

■http://vm.ofstest.com/  
┗こっちが本体
┗npm run serveで表示させるときはnode.jsでサーバー起動して、apacheから  
 localhost:8080(vue.jsのデフォルト)にリバースプロキシ  
┗PWAは「npm run build」でビルド&&「localhostでの接続 or SSL接続」の時しか使えないので、ローカルではlocalhost:8000でアクセスして確認する事  


## ディレクトリ構成
/api 以下にAPI(laravel)を構成  
/vue にアプリケーション本体(vueの記述)を仕込む。  
本番実装時は分離して別のサーバーに置けば成立するはず  

## vue.js
### options
●Babel  
●Type Script  
●Progressive Web App (PWA) Support  
●Router  
●Vuex  
●CSS Pre-processors  

●Linter / Formatter  
●Unit Testing  
●E2E Testing  

### talking
? Please pick a preset: Manually select features  
? Check the features needed for your project: Babel, TS, PWA, Router, Vuex, CSS Pre-processors, Linter, Unit, E2E  
? Use class-style component syntax? Yes  
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes  
? Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default): Sass/SCSS (with
 node-sass)  
? Pick a linter / formatter config: Basic  
? Pick additional lint features: Lint on save  
? Pick a unit testing solution: Jest  
? Pick a E2E testing solution: Nightwatch  
? Pick browsers to run end-to-end test on (Press <space> to select, <a> to toggle all, <i> to invert selecti
on)Chrome  
? Where do you prefer placing config for Babel, ESLint, etc.? In package.json  
? Save this as a preset for future projects? Yes  
? Save preset as: .setting  
