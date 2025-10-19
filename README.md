# repository-cerejinha
const express = require("express");
const app = express();

app.use(express.json());

// Usuário fixo (login simples)
const usuario = { user: "admin", pass: "senha123" };

// Lista de tarefas
let tarefas = [
  { id: 1, titulo: "Estudar Node.js" },
  { id: 2, titulo: "Fazer a tarefa de Desenvolvimento Web II" },
];

// Login
app.post("/login", (req, res) => {
  const { user, pass } = req.body;

  if (user === usuario.user && pass === usuario.pass) {
    res.json({ token: "seu-token-simples" });
  } else {
    res.status(401).json({ erro: "Usuário ou senha incorretos" });
  }
});

// Middleware para verificar token
function autenticar(req, res, next) {
  const token = req.headers.authorization;
  if (token === "seu-token-simples") {
    next();
  } else {
    res.status(403).json({ erro: "Acesso negado. Token inválido ou ausente." });
  }
}

// Listar tarefas (rota protegida)
app.get("/tasks", autenticar, (req, res) => {
  res.json(tarefas);
});

// Adicionar tarefa (rota protegida)
app.post("/task", autenticar, (req, res) => {
  const nova = { id: tarefas.length + 1, titulo: req.body.titulo };
  tarefas.push(nova);
  res.json({ mensagem: "Tarefa adicionada!", tarefa: nova });
});

// Iniciar servidor
app.listen(3000, () => {
  console.log("Servidor rodando em http://localhost:3000");
});{
  "titulo": "Praticar autenticação"
}git init
git add .
git commit -m "Projeto de autenticação simples"
git branch -M main
git remote add origin https://github.com/seunome/autenticacao.git
git push -u origin main
