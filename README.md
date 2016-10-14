# ProjetoBD
#DATABASE TABLES SCHEMAS...


       Table "public.pessoa"
 Column |     Type     | Modifiers 
--------+--------------+-----------
 cpf    | integer      | not null
 nome   | text         | 
 sexo   | character(1) | 
 cel    | integer      | 
 email  | text         | 
 senha  | text         | 
Indexes:
    "pessoa_pkey" PRIMARY KEY, btree (cpf)
Referenced by:
    TABLE "aula" CONSTRAINT "aula_cpf_prof_fkey" FOREIGN KEY (cpf_prof) REFERENCES pessoa(cpf)
    TABLE "turma" CONSTRAINT "turma_cpf_aluno_fkey" FOREIGN KEY (cpf_aluno) REFERENCES pessoa(cpf)


                                     Table "public.aula"
  Column   |            Type             |                     Modifiers                     
-----------+-----------------------------+---------------------------------------------------
 id        | integer                     | not null default nextval('aula_id_seq'::regclass)
 materiaid | integer                     | 
 cpf_prof  | integer                     | 
 time      | timestamp without time zone | 
 preço     | real                        | 
 local     | integer                     | 
Indexes:
    "aula_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "aula_cpf_prof_fkey" FOREIGN KEY (cpf_prof) REFERENCES pessoa(cpf)
    "aula_local_fkey" FOREIGN KEY (local) REFERENCES local(id)
    "aula_materiaid_fkey" FOREIGN KEY (materiaid) REFERENCES materia(id)
Referenced by:
    TABLE "turma" CONSTRAINT "turma_id_aula_fkey" FOREIGN KEY (id_aula) REFERENCES aula(id)
    
                         Table "public.materia"
 Column |  Type   |                      Modifiers                       
--------+---------+------------------------------------------------------
 id     | integer | not null default nextval('materia_id_seq'::regclass)
 nome   | text    | 
Indexes:
    "materia_pkey" PRIMARY KEY, btree (id)
Referenced by:
    TABLE "aula" CONSTRAINT "aula_materiaid_fkey" FOREIGN KEY (materiaid) REFERENCES materia(id)

      Table "public.turma"
  Column   |  Type   | Modifiers 
-----------+---------+-----------
 id_aula   | integer | not null
 cpf_aluno | integer | not null
Indexes:
    "turma_pkey" PRIMARY KEY, btree (id_aula, cpf_aluno)
Foreign-key constraints:
    "turma_cpf_aluno_fkey" FOREIGN KEY (cpf_aluno) REFERENCES pessoa(cpf)
    "turma_id_aula_fkey" FOREIGN KEY (id_aula) REFERENCES aula(id)

                         Table "public.local"
 Column |  Type   |                     Modifiers                      
--------+---------+----------------------------------------------------
 id     | integer | not null default nextval('local_id_seq'::regclass)
 nome   | text    | 
Indexes:
    "local_pkey" PRIMARY KEY, btree (id)
Referenced by:
    TABLE "aula" CONSTRAINT "aula_local_fkey" FOREIGN KEY (local) REFERENCES local(id)



