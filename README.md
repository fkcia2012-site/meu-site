# FKCIA Vidros e Esquadrias - Site

Website para galeria de projetos da empresa FKCIA Vidros e Esquadrias.

## 📋 Estrutura do Projeto

```
public/
├── index.html           # Página principal
├── admin.html          # Painel administrativo
├── styles.css          # Estilos CSS
├── app.js              # Lógica JavaScript
└── firebase-config.js  # Configuração Firebase
```

## 🚀 Como Publicar no GitHub Pages

### Passo 1: Acessar as Configurações do Repositório
1. Vá para **Settings** do repositório: https://github.com/fkcia2012-site/meu-site/settings
2. Procure por **Pages** no menu lateral esquerdo

### Passo 2: Habilitar GitHub Pages
1. Em "Source", selecione a branch **main**
2. Selecione a pasta **/public**
3. Clique em **Save**

### Passo 3: Aguardar o Deploy
- GitHub Pages irá processar seu site (leva 1-2 minutos)
- Você verá uma mensagem verde quando estiver pronto
- Seu site estará disponível em: https://fkcia2012-site.github.io/meu-site/

## 🔧 Configuração do Firebase

Antes de usar o painel admin, você precisa:

1. Criar um projeto Firebase em https://console.firebase.google.com/
2. Copiar suas credenciais de configuração
3. Atualizar o arquivo `public/firebase-config.js` com suas chaves

## 📝 Funcionalidades

- ✅ Galeria pública de projetos
- ✅ Painel administrativo com login
- ✅ Upload de imagens e vídeos
- ✅ Armazenamento em Firebase
- ✅ Responsive design