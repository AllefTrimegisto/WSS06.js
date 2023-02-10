# WSS06.js
#Faça um código para implementar o CRUD de algum recurso. Por exemplo: alunos, equipamentos ou vendas. Aponte as rotas e os retornos do status HTTP.

const express = require('express');
const app = express();
const port = 3000;

// Dados fictícios de alunos
let alunos = [
  { id: 1, nome: 'João', idade: 20 },
  { id: 2, nome: 'Maria', idade: 21 },
  { id: 3, nome: 'Pedro', idade: 22 }
];

// Rota para criar um aluno (Criar)
app.post('/alunos', (req, res) => {
  const novoAluno = {
    id: alunos.length + 1,
    nome: req.body.nome,
    idade: req.body.idade
  };
  alunos.push(novoAluno);
  res.status(201).send(novoAluno);
});

// Rota para ler todos os alunos (Ler)
app.get('/alunos', (req, res) => {
  res.status(200).send(alunos);
});

// Rota para ler um aluno específico (Ler)
app.get('/alunos/:id', (req, res) => {
  const aluno = alunos.find(a => a.id === parseInt(req.params.id));
  if (!aluno) {
    res.status(404).send('Aluno não encontrado');
  } else {
    res.status(200).send(aluno);
  }
});

// Rota para atualizar um aluno (Atualizar)
app.put('/alunos/:id', (req, res) => {
  const aluno = alunos.find(a => a.id === parseInt(req.params.id));
  if (!aluno) {
    res.status(404).send('Aluno não encontrado');
  } else {
    aluno.nome = req.body.nome;
    aluno.idade = req.body.idade;
    res.status(200).send(aluno);
  }
});

// Rota para excluir um aluno (Excluir)
app.delete('/alunos/:id', (req, res) => {
  const aluno = alunos.find(a => a.id === parseInt(req.params.id));
  if (!aluno) {
    res.status(404).send('Aluno não encontrado');
  } else {
    const index = alunos.indexOf(aluno);
    alunos.splice(index, 1);
    res.status(200).send(aluno);
  }
});

app.listen(port, () => {
  console.log(`Servidor rodando na porta ${port}`);
});
