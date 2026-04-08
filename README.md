Coluna,Tipo,Restrição
id_profissional,INTEGER,Primary Key (PK)
nome_profissional,VARCHAR(100),NOT NULL
especialidade,VARCHAR(50),NOT NULL
telefone,VARCHAR(15),UNIQUE / NOT NULL

Coluna,Tipo,Restrição
id_servico,INTEGER,Primary Key (PK)
nome_servico,VARCHAR(100),NOT NULL
preco_base,"DECIMAL(10,2)",NOT NULL
duracao_minutos,INTEGER,NOT NULL

Coluna,Tipo,Restrição
fk_id_agendamento,INTEGER,PFK (Primary Foreign Key)
fk_id_servico,INTEGER,PFK (Primary Foreign Key)
valor_aplicado,"DECIMAL(10,2)",NOT NULL
observacao,VARCHAR(255),-

Coluna,Tipo,Restrição
fk_id_profissional,INTEGER,PFK (Primary Foreign Key)
dia_semana,INTEGER,PFK (1 a 7 - Not Null)
hora_inicio,TIME,NOT NULL
hora_fim,TIME,NOT NULL

🔑 Decisões Técnicas de Modelagem
Entidade Fraca (Tb_DISPONIBILIDADE): A agenda não existe sem um profissional vinculado. Utilizamos uma chave primária composta (fk_id_profissional + dia_semana) para garantir que o profissional defina seus horários para cada dia específico.

Entidade Associativa (Tb_AGENDAMENTO_SERVICO): Permite que um único ticket de agendamento contenha múltiplos serviços, registrando o valor cobrado no momento da execução (evitando problemas se o preço do serviço mudar no futuro).

Tipagem de Tempo: Introdução do tipo TIME para controle de horários e INTEGER para duração em minutos, facilitando cálculos matemáticos de agenda.

Nomenclatura: Mantido o padrão Tb_ e snake_case, garantindo que a estrutura seja legível e padronizada para administradores de banco de dados (DBAs)
