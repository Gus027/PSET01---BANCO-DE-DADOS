~~PostgresSQL



QUESTAO 01-

SELECT f.primeiro_nome AS Funcionario,
       d.numero_departamento AS Departamento,
        (SELECT AVG(salario) FROM elmasri.funcionario)
FROM elmasri.funcionario f
LEFT JOIN elmasri.departamento d ON d.numero_departamento = f.numero_departamento;


QUESTAO 02 -

SELECT f.sexo AS sexo,
(SELECT AVG(salario) FROM elmasri.funcionario) AS Media_M_F
FROM elmasri.funcionario f
LEFT JOIN elmasri.departamento d ON d.numero_departamento = f.numero_departamento;


QUESTAO 03 - 


SELECT d.nome_departamento AS departamento,
       d.numero_departamento AS departamento,
       f.primeiro_nome AS funcionario,
       f.nome_meio AS funcionario,
       f.ultimo_nome AS funcionario,
       f.data_nascimento AS Data_nascimento,
       extract(year from age(data_nascimento)) AS idade
FROM elmasri.departamento d
INNER JOIN elmasri.funcionario f ON (f.numero_departamento = d.numero_departamento);



QUESTAO 04 -

SELECT primeiro_nome AS PrimeioNome,
       nome_meio AS NomeMeio,
       ultimo_nome AS UltimoNome,
       data_nascimento AS DataNasc,
       extract(year from age(data_nascimento)) AS idade,
       salario AS Salario,
       salario * 1.2 AS Reajuste,
CASE
   WHEN salario >35000.00 THEN salario * 1.2
   WHEN salario <=35000.00 THEN salario * 1.15
END AS reajuste
FROM elmasri.funcionario ;


QUESTAO 05 -

SELECT f.primeiro_nome AS Gerentes,
       d.cpf_gerente AS Cpf_Gerente,
       d.nome_departamento AS NomeDepartamento,
       f.numero_departamento AS NumeroDepartamento,
       f.primeiro_nome AS funcionarios,
       f.salario AS salario
FROM elmasri.funcionario f
INNER JOIN elmasri.departamento d ON (d.cpf_gerente = f.cpf)
ORDER BY nome_departamento ASC, salario DESC;


QUESTAO 6 - 
    
SELECT w.nome_dependente AS Dependente,
       w.data_nascimento AS DataNascDependente,
       extract(year from age(w.data_nascimento)) AS idade,
       w.sexo AS sexo_Dependente,
       f.primeiro_nome AS Funcionario,
       f.nome_meio AS NomeMeio,
       f.numero_departamento AS departamento,
CASE 
       WHEN w.sexo = 'M' THEN 'Masculino'
       WHEN w.sexo = 'F' THEN 'Feminino'
END 
FROM elmasri.dependente w
INNER JOIN elmasri.funcionario f ON (f.cpf = w.cpf_funcionario);



QUESTÃO 07 -

SELECT  f.primeiro_nome AS funcionario,
        f.nome_meio AS NomeMeio,
        f.ultimo_nome AS UltimoNome,
        f.data_nascimento AS DataNasci,
        f.salario AS salario,
        w.nome_dependente AS Dependentes
FROM elmasri.funcionario f
LEFT JOIN elmasri.dependente w ON (w.cpf_funcionario = f.cpf);



QUESTAO 08 - 

SELECT p.numero_projeto AS Numero_Projeto,
       p.nome_projeto AS Projeto,
       d.nome_departamento AS Departamento,
       f.primeiro_nome AS Funcionario,
       f.nome_meio AS NomeMeio,
       f.ultimo_nome AS UltimoNome,
       t.horas AS horas
FROM elmasri.projeto p
INNER JOIN elmasri.trabalha_em t ON (t.numero_projeto = p.numero_projeto)
INNER JOIN elmasri.departamento d ON (d.numero_departamento = p.numero_departamento)
INNER JOIN elmasri.funcionario f ON (f.numero_departamento = p.numero_departamento)



QUESTAO 09- 

SELECT  d.nome_departamento AS Deparatamento,
        p.nome_projeto AS Projeto,
        SUM(horas) AS Horas_da_Soma
FROM elmasri.departamento d
INNER JOIN elmasri.projeto p ON (p.numero_departamento = d.numero_departamento)
INNER JOIN elmasri.trabalha_em t ON (t.numero_projeto = p.numero_projeto)
GROUP BY nome_departamento, p.nome_projeto 
ORDER BY nome_departamento





QUESTAO 10 - 


SELECT f.primeiro_nome AS Funcionario,
       d.numero_departamento AS Departamento,
        (SELECT AVG(salario) FROM elmasri.funcionario)
FROM elmasri.funcionario f
LEFT JOIN elmasri.departamento d ON d.numero_departamento = f.numero_departamento;


QUESTAO 11 -
  
SELECT DISTINCT 
  CONCAT(f.primeiro_nome, f.nome_meio, f.ultimo_nome) AS Funcionario,
        p.nome_projeto,
        SUM(horas * 50)  AS valor_total
FROM elmasri.funcionario f
INNER JOIN elmasri.projeto p ON (f.numero_departamento = p.numero_departamento)
INNER JOIN elmasri.trabalha_em t ON (p.numero_projeto = t.numero_projeto)
GROUP BY elmasri.funcionario, p.nome_projeto
ORDER BY elmasri.funcionario;


QUESTAO 12 - 

SELECT  d.nome_departamento,
        p.nome_projeto,
        f.primeiro_nome AS nome_funcionario
FROM elmasri.projeto p
INNER JOIN elmasri.departamento d ON (p.numero_departamento = d.numero_departamento)
INNER JOIN elmasri.funcionario  f ON (p.numero_departamento = f.numero_departamento)
INNER JOIN elmasri.trabalha_em  t ON (p.numero_projeto = t.numero_projeto)
WHERE t.horas IS NULL OR t.horas = 0;


QUESTAO 13 - 
 
SELECT 
       CONCAT(f.primeiro_nome,' ', f.nome_meio,' ', f.ultimo_nome) AS Nome_Funcionario,
       sexo AS sexo,
       TIMESTAMPDIFF (YEAR,f.data_nascimento,CURDATE()) AS idade
FROM elmasri.funcionario f
UNION
SELECT CONCAT(w.nome_dependente, ' ', f.ultimo_nome),
       w.sexo AS sexo,
       TIMESTAMPDIFF (YEAR,w.data_nascimento,CURDATE()) AS idade
FROM elmasri.dependente w
INNER JOIN elmasri.funcionario f ON (f.cpf = w.cpf_funcionario);



QUESTAO 14 - 

SELECT  nome_departamento AS departamento,
        COUNT(cpf) AS Funcionarios_Numero
FROM elmasri.funcionario f
INNER JOIN elmasri.departamento d ON (f.numero_departamento = d.numero_departamento)
GROUP BY nome_departamento;


QUESTAO 15 - 
              
SELECT f.primeiro_nome AS Nome, 
       f.nome_meio AS NomeMeio,
       f.ultimo_nome AS UltimoNome,
       d.nome_departamento AS Departamento,
       p.nome_projeto AS Projeto
FROM elmasri.funcionario f 
INNER JOIN elmasri.departamento d ON (d.cpf_gerente = f.cpf)
INNER JOIN elmasri.trabalha_em t ON (t.cpf_funcionario = f.cpf)
INNER JOIN elmasri.projeto p ON (p.numero_projeto = t.numero_projeto);


