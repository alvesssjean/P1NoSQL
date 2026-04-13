-  Criando o banco: use escola

-  Criando a collection, inserindo os alunos do modelo:

|   {
|     "nome": "Beatriz Oliveira", 
|     "idade": 22,
|     "curso": "Engenharia de Software",
|     "notas": [9, 8.5, 10],
|     "endereco": {
|       "cidade": "Niterói",
|       "estado": "RJ"
|     }
|   },
|   {
|     "nome": "Marcos Souza",
|     "idade": 19,
|     "curso": "Sistemas de Informação",
|     "notas": [6, 7.5, 8],
|     "endereco": {
|       "cidade": "São Gonçalo",
|       "estado": "RJ"
|     }
|   },
|   {
|     "nome": "Ana Clara Lima",
|     "idade": 21,
|     "curso": "ADS",
|     "notas": [10, 9, 9.5],
|     "endereco": {
|       "cidade": "Rio de Janeiro",
|       "estado": "RJ"
|     }
|   },
|   {
|     "nome": "Ricardo Pereira",
|     "idade": 25,
|     "curso": "Ciência da Computação",
|     "notas": [5.5, 6, 7],
|     "endereco": {
|       "cidade": "Maricá",
|       "estado": "RJ"
|     }
|   },
|   {
|     "nome": "Juliana Costa",
|     "idade": 20,
|     "curso": "ADS",
|     "notas": [8, 8, 8.5],
|     "endereco": {
|       "cidade": "Itaboraí",
|       "estado": "RJ"
|     }
|   }
| ])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('69dcfa895d4d7e224b44ba89'),
    '1': ObjectId('69dcfa895d4d7e224b44ba8a'),
    '2': ObjectId('69dcfa895d4d7e224b44ba8b'),
    '3': ObjectId('69dcfa895d4d7e224b44ba8c'),
    '4': ObjectId('69dcfa895d4d7e224b44ba8d')
  }
}

1) Buscando todos os alunos:

-  db.alunos.find()


2) Buscar alunos do curso "ADS"

-  db.alunos.find({"curso": "ADS"})


3) Buscar alunos com idade maior que 21:

-  db.alunos.find({ "idade": { "$gt": 21 } })


4) Atualizar a idade de um aluno:

-  db.alunos.findOneAndUpdate({"nome": "Beatriz Oliveira"}, {$set: {"idade": 24}})

5) Adicionar uma nova nota a um aluno:

-  db.alunos.updateOne(
|   { "nome": "João Silva" },
|   { "$push": { "notas": 10 } }
| )


6) Remover um aluno: 

-  db.alunos.findOneAndDelete({"nome": "João Silva"})

7) Média de notas por aluno:

-  db.alunos.aggregate([
|   {
|     $addFields: {
|       media: { $avg: "$notas" }
|     }
|   }
| ])



8) Quantidade de alunos por curso:

-  db.alunos.aggregate([
  {
    $group: {
      _id: "$curso",       
      quantidade: { $sum: 1 }
    }
  }
])


