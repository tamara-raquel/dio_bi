# Projeto: Coleta e transformação de dados
Projeto de coleta e transformação de dados e geração de relatório, utilizando o Power BI, Power Query e um banco de dados MySQL na nuvem.

## Preview
**Página 1: Projetos**
<img src="/preview/pg01.PNG">

**Página 2: Colaboradores**
<img src="/preview/pg02.PNG">

## Coleta e carregamento dos dados
### **Criação da base de dados**
- Criei uma base de dados chamada azure_company em um banco de dados MySQL
- Criei as tabelas employee, departament, dept_locations, works_on e dependent, seguindo o script disponibilizado
- Criei as chaves primárias e estrangeiras, estabelecendo os relacionamentos entre as tabelas
### **População da base de dados**
- Fiz a inserção dos dados nas tabelas de acordo com o script disponibilizado, sendo que os inserts na tabela employee tiveram sua ordem modificada para evitar um erro de constraint mostrado.
- Realização de consultas iniciais
- Executei algumas queries a fim de verificar se a base estava funcionando corretamente.
### **Conexão da base com o PowerBI**
- Fiz a instalação do conector
- Fiz a a conexão com o banco de dados via Obter Dados no PowerBI
- Carreguei os dados pelo Power Query para fazer as transformações
## Transformação
### **Verificação dos cabeçalhos**
- Renomeei a tabela departament para department
- Na tabela department, a fim de estabelecer um padrão com a coluna Dept_create_date,, renomeei as colunas Dnumber e Dname para Dept_number e Dept_name
- Na tabela dependent, também para estabelecer um padrão com a coluna Dependent_name, renomeei as colunas Sex, Bdate e Relationship para Dependent_sex, Dependent_birthdate e Dependent_relationship
- Na tabela dept_location, renomeei as colunas Dlocation e Dnumber para Dept_location e Dept_number
- Na tabela employee, renomeei a coluna Bdate para Birthdate
- Na tabela project, renomeei as colunas Pname, Pnumber, Plocation e Dnum para Project_name, Project_number, Project_location e Dept_number
- Na tabela works_on, renomeei a coluna Pno para Project_number
### **Transformação do tipo de dado**
- Na tabela employee, alterei o tipo de dado da coluna Salary, de texto para decimal fixo
### **Exclusão de colunas de metadados**
- Excluí as colunas azure_company.dept_locations, azure_company.employee e azure_company.project da tabela department
- Excluí a coluna azure_company.employee da tabela dependent
- Excluí a coluna azure_company.department da tabela dept_location
- Excluí as colunas azure_company.department, azure_company.dependent, azure_company.employee(Ssn), azure_company.employee(Super_ssn) e azure_company.works_on da tabela employee
- Excluí as colunas azure_company.department e azure_company.works_on da tabela project
- Excluí as colunas azure_company.employee e azure_company.project da tabela works_on
### **Verificação de valores nulos**
- Foi verificado um valor nulo na tabela employee, na coluna Super_ssn e foi verificado que o funcionário em questão é gerente em Headquarters, portanto o registro não foi excluído
### **Separação de colunas**
- Na tabela employee, separei a coluna Address em Number, Street, City e State
### **Mesclar e junções de colunas**
- Na tabela employee, combinei as colunas Fname e Lname em uma coluna única, chamada Name, utilizando Adicionar Coluna Personalizada
- Movi a nova coluna Name para o início da tabela e fiz a exclusão das 2 colunas utilizadas para sua criação e da coluna Minit
- Na tabela employee, fiz a mescla com a tabela department pela chave Dept_number, expandi as colunas e depois removi as colunas desnecessárias, a fim de contar o nome do departamento de cada funcionário
- Criei uma nova consulta e fiz a mescla de department e dept_location, utilizando Dept_number como chave, para trazer o nome do departamento e sua localização. Nomeei como department_query e exclui as colunas desnecessárias
- Criei uma nova consulta e fiz a junção de employee usando a chave Super_ssn para trazer o nome do funcionário e o nome de seu respectivo gerente. Nomeei a tabela como manager_query, excluí as colunas desnecessárias e renomeei a coluna Name como Employee
- Criei uma nova consulta para relacionar os colaboradores e gerentes, utilizei a tabela anterior manager_query, então utilizei a função de Agrupar para contar quantos colaboradores existem por gerente. Renomeei a coluna Contagem para Total_employees e nomeei a consulta como Employees_per_manager
- Criei uma nova consulta para relacionar as horas trabalhadas em projetos por colaborador (tabelas works_on) com a tabela employee, para trazer o nome de cada colaborador
## Construção de relatório
### Página 1: Projetos

**Indicadores:**
- Total de projetos
- Total de localidades
- Total de departamentos

**Gráficos:**
- Projetos por localidade
- Projetos por departamento
- Total de horas trabalhadas por projeto
### Página 2: Colaboradores

**Gráficos:**
- Colaboradores por gênero
- Colaboradores por gerente
- Salários por colaborador
- Colaboradores por cidade
- Horas trabalhadas por colaborador
- Dependentes por colaborador
## Publicação
- Exportação para o Power BI Service
- Github: Relatório (pbix), Relatório (pdf)
