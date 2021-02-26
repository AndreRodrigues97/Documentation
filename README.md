<h1><b>Program</b></h1>
<h3><b>End points</b></h3>

<ul>
    <li>View/Program/Create.aspx</li>
</ul>

<h3><b>Relacionamentos</b></h3>

<ul>
    <li>Possui relacionamento direto com a entidade tag</li>
</ul>
*Tag*
![](./imagens/ListaGrupoFaturamento.PNG)

<ul>
    <li>Possui relacionamento indireto com a entidade Grupo de faturamento(tb_project_group) e a entidade Etapas do projeto(tb_project)</li>
</ul>
*Grupo de faturamento*
![](./imagens/ListaGrupoFaturamento.PNG)

_Etapas do projeto_
![](./imagens/ListaEtapasProjetos.PNG)

<h3><b>Estrutura de dados</b></h3>

<b>tb_Program</b>
Entidade | Tipo | Tamanho | Chave primaria | Chave estrangeira | Nulo
-------- | ---- | ------- | -------------- | ----------------- | ----
Program_ID | INT | - | Sim | Não | Não
Program_Name | VARCHAR | 50 | Não | Não | Não
Program_Description | VARCHAR | 800 | Não | Não | Sim
Operation_ID | INT | - | Não | Sim | Sim
Disabled | INT | - | Não | Não | Sim
BusinessUnit_ID | INT | - | Não | Sim | Sim
Portfolio_Manager_ID | INT | - | Não | Sim | Sim
Program_Type_ID | INT | - | Não | Sim | Sim
Product_Stage_ID | INT | - | Não | Sim | Sim
Funding_Investment_ID| INT | - | Não | Sim | Sim
BusinessFocusArea | Varchar | 150 | Não | Não | Sim
Program_Cost_Type_ID | INT | - | Não | Sim | Sim
ObjetivoGeral | Varchar | Max | Não | Não | Sim
ProblemaTecnico | Varchar | Max | Não | Não | Sim
Program_Alcance_ID | INT | - | Não | Sim | Sim
Program_Nivel_ID | INT | - | Não | Sim | Sim
BU_Name | Varchar | 50 | Não | Não | Sim

<b>tb_tag</b>
Entidade | Tipo | Tamanho | Chave primaria | Chave estrangeira | Nulo
-------- | ---- | ------- | -------------- | ----------------- | ----
ID | INT | - | Sim | Não | Não
Class_ID | INT | - | Não | Sim | Não
Name | VARCHAR | 50 | Não | Não | Não

<b>Obs.: </b>Verificar se os dados são inseridos ou cadastrados.

<b>tb_tag_class</b>
Entidade | Tipo | Tamanho | Chave primaria | Chave estrangeira | Nulo
-------- | ---- | ------- | -------------- | ----------------- | ----
ID | INT | - | Sim | Não | Não
Name | VARCHAR | 50 | Não | Não | Não

<b>Obs.: </b>Verificar se os dados são inseridos ou cadastrados.

<b>tb_tag_program</b>
Entidade | Tipo | Tamanho | Chave primaria | Chave estrangeira | Nulo
-------- | ---- | ------- | -------------- | ----------------- | ----
tag_ID | INT | - | Não | Sim | Não
program_ID | INT | - | Não | Sim | Não

<b>Obs.: </b>Verificar se dependencia esta sendo usada pela aplicação, por que hoje não tinha nenhuma tag cadastrada.

<h3><b>Regras de negocio</b></h3>

<b>Create</b>

_Campo Bu.Name deve ser preenchido com o nome do programa quando este for vazio._
![](./imagens/BuName.PNG)

<b>Edit</b>
<b>OBS.: </b>Verificar se é possivel cadastrar um programa com o mesmo nome.

```
protected void valExistingName_ServerValidate(object source, ServerValidateEventArgs args)
{
    Model.Protrack2000.ProgramSet ps = new Model.Protrack2000.ProgramSet();
    int ID = Int32.Parse(ViewState["ID"].ToString());
    args.IsValid = !ps.existsProgram(txtName.Text, ID);
}
```

<ul>
    <li>Quando o programa possuir projetos e grupo de faturamento não deve ser possivel desabilitar o mesmo.</li>
</ul>

![](./imagens/Desabilitado.PNG)

_É mostrado as etapas referente ao programa._

![](./imagens/Etapas.PNG)

_É mostrado os grupos de faturamento referente a programa._

![](./imagens/GrupoFaturamento.PNG)

<b>Delete</b>

<ul>
    <li>
        Não deve permitir deletar um programa que esteja sendo usado.
    </li>
</ul>

<b>A tela de edit possui uma relação direta com a tag e duas relações indiretas com grupo de faturamento e etapa</b>
