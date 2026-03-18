# meu-site
FKCIA Vidros e Esquadrias
-

📁 public/index.html

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FKCIA Vidros e Esquadrias</title>
<link rel="stylesheet" href="styles.css">
</head>
<body>
<header>
  <h1>FKCIA Vidros e Esquadrias</h1>
  <a href="admin.html">Login</a>
</header>
<section id="galeria"></section>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore.js"></script>
<script src="firebase-config.js"></script>
<script src="app.js"></script>
<script>
// Mostrar obras públicas
carregarGaleriaPublica();
</script>
</body>
</html>
```

---

📁 public/admin.html

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Admin | FKCIA</title>
<link rel="stylesheet" href="styles.css">
</head>
<body>
<h2>Login Admin</h2>
<input type="email" id="email" placeholder="Email">
<input type="password" id="senha" placeholder="Senha">
<button onclick="login()">Entrar</button>
<div id="painel" style="display:none;">
  <h2>Painel Administrativo</h2>
  <input type="file" id="midiaInput">
  <button onclick="uploadMidia()">Upload</button>
  <button onclick="logout()" style="background:red;">Logout</button>
  <div id="minhaGaleria"></div>
</div>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-storage.js"></script>
<script src="firebase-config.js"></script>
<script src="app.js"></script>
</body>
</html>
```

---

📁 public/styles.css

```css
body {font-family: Arial; margin:20px;}
img, video {width: 200px; margin: 10px;}
button {padding:10px 15px; background:green; color:white; border:none; cursor:pointer;}
input {padding:10px; width:100%; max-width:400px; margin:5px 0;}
#painel {margin-top:20px;}
```

---

📁 public/firebase-config.js

```javascript
// Cole suas chaves do Firebase aqui
const firebaseConfig = {
  apiKey: "SUA_API_KEY",
  authDomain: "SEU_AUTH_DOMAIN",
  projectId: "SEU_PROJECT_ID",
  storageBucket: "SEU_STORAGE_BUCKET",
  messagingSenderId: "SEU_MSG_SENDER_ID",
  appId: "SEU_APP_ID"
};

firebase.initializeApp(firebaseConfig);
const auth = firebase.auth();
const db = firebase.firestore();
const storage = firebase.storage();
```

---

📁 public/app.js

```javascript
// Funções Admin
function login() {
  const email = document.getElementById("email").value;
  const senha = document.getElementById("senha").value;
  auth.signInWithEmailAndPassword(email, senha)
    .then(() => document.getElementById("painel").style.display = "block")
    .catch(err => alert(err.message));
}
function logout() { auth.signOut().then(() => location.reload()); }
function uploadMidia() {
  const file = document.getElementById("midiaInput").files[0];
  const nome = Date.now() + "_" + file.name;
  const ref = storage.ref().child(nome);
  ref.put(file).then(() => {
    ref.getDownloadURL().then(url => {
      db.collection("obras").add({ url, type: file.type.includes("video") ? "video" : "image" });
      alert("Upload feito!"); location.reload();
    });
  });
}

// Mostrar galeria Admin
db.collection("obras").get().then(q => {
  const div = document.getElementById("minhaGaleria");
  q.forEach(d => {
    const data = d.data();
    const item = document.createElement(data.type === "image" ? "img" : "video");
    item.src = data.url;
    if (data.type === "video") item.controls = true;
    div.appendChild(item);
  });
});

// Função pública
function carregarGaleriaPublica() {
  const galeria = document.getElementById("galeria");
  db.collection("obras").get().then(q => {
    q.forEach(doc => {
      const data = doc.data();
      const item = document.createElement(data.type === "image" ? "img" : "video");
      item.src = data.url;
      if (data.type === "video") item.controls = true;
      galeria.appendChild(item);
    });
  });
}
```

---
