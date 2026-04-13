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

-  escola> db.alunos.find()

[
  {
    _id: ObjectId('69dcf8cfe0e998c88d44ba89'),
    nome: 'João Silva',
    idade: 20,
    curso: 'ADS',
    notas: [ 7, 8, 9 ],
    endereco: { cidade: 'Maricá', estado: 'RJ' }
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba89'),
    nome: 'Beatriz Oliveira',
    idade: 22,
    curso: 'Engenharia de Software',
    notas: [ 9, 8.5, 10 ],
    endereco: { cidade: 'Niterói', estado: 'RJ' }
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8a'),
    nome: 'Marcos Souza',
    idade: 19,
    curso: 'Sistemas de Informação',
    notas: [ 6, 7.5, 8 ],
    endereco: { cidade: 'São Gonçalo', estado: 'RJ' }
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8b'),
    nome: 'Ana Clara Lima',
    idade: 21,
    curso: 'ADS',
    notas: [ 10, 9, 9.5 ],
    endereco: { cidade: 'Rio de Janeiro', estado: 'RJ' }
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8c'),
    nome: 'Ricardo Pereira',
    idade: 25,
    curso: 'Ciência da Computação',
    notas: [ 5.5, 6, 7 ],
    endereco: { cidade: 'Maricá', estado: 'RJ' }
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8d'),
    nome: 'Juliana Costa',
    idade: 20,
    curso: 'ADS',
    notas: [ 8, 8, 8.5 ],
    endereco: { cidade: 'Itaboraí', estado: 'RJ' }
  }
]


2) Buscar alunos do curso "ADS"

escola> db.alunos.find({"curso": "ADS"})
[
  {
    _id: ObjectId('69dcf8cfe0e998c88d44ba89'),
    nome: 'João Silva',
    idade: 20,
    curso: 'ADS',
    notas: [ 7, 8, 9 ],
    endereco: { cidade: 'Maricá', estado: 'RJ' }
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8b'),
    nome: 'Ana Clara Lima',
    idade: 21,
    curso: 'ADS',
    notas: [ 10, 9, 9.5 ],
    endereco: { cidade: 'Rio de Janeiro', estado: 'RJ' }
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8d'),
    nome: 'Juliana Costa',
    idade: 20,
    curso: 'ADS',
    notas: [ 8, 8, 8.5 ],
    endereco: { cidade: 'Itaboraí', estado: 'RJ' }
  }
]

3) Buscar alunos com idade maior que 21:

escola> db.alunos.find({ "idade": { "$gt": 21 } })
[
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba89'),
    nome: 'Beatriz Oliveira',
    idade: 22,
    curso: 'Engenharia de Software',
    notas: [ 9, 8.5, 10 ],
    endereco: { cidade: 'Niterói', estado: 'RJ' }
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8c'),
    nome: 'Ricardo Pereira',
    idade: 25,
    curso: 'Ciência da Computação',
    notas: [ 5.5, 6, 7 ],
    endereco: { cidade: 'Maricá', estado: 'RJ' }
  }
]

4) Atualizar a idade de um aluno:

escola> db.alunos.findOneAndUpdate({"nome": "Beatriz Oliveira"}, {$set: {"idade": 24}})
{
  _id: ObjectId('69dcfa895d4d7e224b44ba89'),
  nome: 'Beatriz Oliveira',
  idade: 22,
  curso: 'Engenharia de Software',
  notas: [ 9, 8.5, 10 ],
  endereco: { cidade: 'Niterói', estado: 'RJ' }
}

5) Adicionar uma nova nota a um aluno:

escola> db.alunos.updateOne(
|   { "nome": "João Silva" },
|   { "$push": { "notas": 10 } }
| )
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

6) Remover um aluno: 

escola> db.alunos.findOneAndDelete({"nome": "João Silva"})
{
  _id: ObjectId('69dcf8cfe0e998c88d44ba89'),
  nome: 'João Silva',
  idade: 20,
  curso: 'ADS',
  notas: [ 7, 8, 9, 10 ],
  endereco: { cidade: 'Maricá', estado: 'RJ' }
}

7) Média de notas por aluno:

escola> db.alunos.aggregate([
|   {
|     $addFields: {
|       media: { $avg: "$notas" }
|     }
|   }
| ])
[
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba89'),
    nome: 'Beatriz Oliveira',
    idade: 24,
    curso: 'Engenharia de Software',
    notas: [ 9, 8.5, 10 ],
    endereco: { cidade: 'Niterói', estado: 'RJ' },
    media: 9.166666666666666
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8a'),
    nome: 'Marcos Souza',
    idade: 19,
    curso: 'Sistemas de Informação',
    notas: [ 6, 7.5, 8 ],
    endereco: { cidade: 'São Gonçalo', estado: 'RJ' },
    media: 7.166666666666667
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8b'),
    nome: 'Ana Clara Lima',
    idade: 21,
    curso: 'ADS',
    notas: [ 10, 9, 9.5 ],
    endereco: { cidade: 'Rio de Janeiro', estado: 'RJ' },
    media: 9.5
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8c'),
    nome: 'Ricardo Pereira',
    idade: 25,
    curso: 'Ciência da Computação',
    notas: [ 5.5, 6, 7 ],
    endereco: { cidade: 'Maricá', estado: 'RJ' },
    media: 6.166666666666667
  },
  {
    _id: ObjectId('69dcfa895d4d7e224b44ba8d'),
    nome: 'Juliana Costa',
    idade: 20,
    curso: 'ADS',
    notas: [ 8, 8, 8.5 ],
    endereco: { cidade: 'Itaboraí', estado: 'RJ' },
    media: 8.166666666666666
  }
]


8) Quantidade de alunos por curso:

db.alunos.aggregate([
  {
    $group: {
      _id: "$curso",       
      quantidade: { $sum: 1 }
    }
  }
])


