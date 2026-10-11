// ==========================================
// MODELAGEM DIMENSIONAL - STAR SCHEMA
// Contexto: Acadêmico / Educacional
// ==========================================

// --- TABELAS DIMENSÃO ---

Table Dim_Professor {
  idProfessor int [pk]
  nome varchar(100)
  departamento varchar(45)
  campus varchar(45)
}

Table Dim_Departamento {
  idDepartamento int [pk]
  Nome varchar(45)
  Campus varchar(45)
  Coordenador varchar(100)
}

Table Dim_Curso {
  idCurso int [pk]
  NomeCurso varchar(45)
  Departamento_idDepartamento int
}

Table Dim_Disciplina {
  idDisciplina int [pk]
  NomeDisciplina varchar(45)
  CargaHoraria int
  PreRequisito varchar(45)
}

Table Dim_Aluno {
  idAluno int [pk]
  NomeAluno varchar(100)
  StatusAluno varchar(20)
}

Table Dim_Tempo {
  idTempo int [pk]
  Data date
  Ano int
  Semestre int
  Mes int
  Dia int
}

// --- TABELAS FATO ---

Table Fato_Matricula {
  idMatricula int [pk]
  idAluno int [ref: > Dim_Aluno.idAluno]
  idDisciplina int [ref: > Dim_Disciplina.idDisciplina]
  idProfessor int [ref: > Dim_Professor.idProfessor]
  idCurso int [ref: > Dim_Curso.idCurso]
  idTempo int [ref: > Dim_Tempo.idTempo]
  
  // Métricas / Indicadores
  nota decimal(5,2)
  frequencia_percentual decimal(5,2)
  status_matricula varchar(30)
}