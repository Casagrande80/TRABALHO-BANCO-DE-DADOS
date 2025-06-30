🏥 Sistema de Gestão de Clínicas Médicas
Banco de dados para agendamento de consultas, gestão de pacientes e médicos

📝 Descrição do Problema
O sistema foi modelado para resolver:

Controle desorganizado de consultas em clínicas médicas.

Dificuldade em rastrear pacientes, convênios e pagamentos.

Falta de relatórios consolidados sobre especialidades médicas e faturamento.

🔍 Modelagem do Banco de Dados
Entidades Principais
Entidade	Atributos Chave	Descrição
PACIENTES	id, nome, cpf, convenio_id	Armazena dados dos pacientes.
MEDICOS	id, nome, erm, especialidade_id	Cadastro de médicos e suas especialidades.
CONSULTAS	id, data, status, paciente_id	Registro de agendamentos.
CONVENIOS	id, nome, cobertura	Planos de saúde vinculados.
Relacionamentos
1 Paciente pode ter N Consultas.

1 Médico atende N Consultas.

1 Convênio pode cobrir N Pacientes.

1 Consulta gera 1 Pagamento.
![Captura de tela 2025-06-30 074417](https://github.com/user-attachments/assets/2e203359-5ed0-4f69-926b-d17adc56b582)


💻 Consultas Exemplo
1. Consultas Agendadas com JOIN
sql
SELECT c.data, p.nome AS paciente, m.nome AS medico  
FROM CONSULTAS c  
INNER JOIN PACIENTES p ON c.paciente_id = p.id  
INNER JOIN MEDICOS m ON c.medico_id = m.id  
WHERE c.status = 'agendada';  
Resultado:

data	paciente	medico
2023-11-10 09:00:00	João Silva	Dr. Roberto Almeida
(Inclua um print real da sua consulta aqui)

2. Subquery: Pacientes com Cobertura > 80%
sql
SELECT nome FROM PACIENTES  
WHERE convenio_id IN (SELECT id FROM CONVENIOS WHERE cobertura > 80);  
Resultado:

nome
Carlos Oliveira
3. View: Faturamento por Clínica
sql
CREATE VIEW vw_faturamento_por_clinica AS  
SELECT cl.nome AS clinica, SUM(pg.valor) AS total  
FROM CLINICAS cl  
JOIN CONSULTAS c ON cl.id = c.clinica_id  
JOIN PAGAMENTOS pg ON c.id = pg.consulta_id  
GROUP BY cl.nome;  
Uso:

sql
SELECT * FROM vw_faturamento_por_clinica;  
Resultado:

clinica	total
Clínica Vida Saudável	250.00
⚙️ Como Executar o Projeto
Clone o repositório:

bash
git clone https://github.com/Casagrande80/TRABALHO-BANCO-DE-DADOS.git .

