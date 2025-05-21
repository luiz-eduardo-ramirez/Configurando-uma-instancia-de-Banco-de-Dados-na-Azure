🛠️ Como Criar uma Instância Gerenciada de SQL no Azure (Windows e Linux)

Este guia mostra como criar uma Instância Gerenciada de SQL do Azure (Azure SQL Managed Instance) usando o Portal do Azure e como conectar-se a ela tanto do Windows quanto do Linux. Ideal para quem quer praticar ou testar soluções em ambientes isolados com alta compatibilidade com SQL Server local.

    💡 Recomendado para fins educacionais ou laboratórios. Para produção, revise políticas de rede, backup e segurança.

📌 O que é o Azure SQL Managed Instance?

Uma Instância Gerenciada de SQL combina os benefícios do SQL Server com a gestão automatizada do Azure: alta disponibilidade, backups automáticos, atualizações, escalabilidade e rede virtual segura.
✅ Pré-requisitos

    Uma conta no Portal do Azure
    Um grupo de recursos (ou criar um novo durante o processo)
    Permissão para criar recursos em rede (VNet e sub-rede gerenciada)
    Uma máquina com SQL Server Management Studio (Windows) ou Azure Data Studio (Linux/macOS)

🧱 Etapa 1: Criar a Instância Gerenciada de SQL

    🔒 Essa etapa exige que você tenha permissão de rede para criar uma VNet e delegar sub-rede.

    Acesse o Portal do Azure.
    Na barra de pesquisa, digite Instância Gerenciada de SQL e clique em Criar.
    Preencha os seguintes campos:

Campo 	Valor Exemplo
Assinatura 	Sua assinatura ativa
Grupo de Recursos 	sql-mi-demo-rg
Nome da Instância 	sqlmi-demo
Região 	Brazil South (ou próxima)
Camada de Preço 	General Purpose (teste/lab)
Autenticação 	SQL Authentication
Usuário Admin 	sqladmin
Senha 	[senha segura]
🌐 Configuração de Rede:

    Crie uma nova Rede Virtual (VNet).
    Em Sub-rede gerenciada, crie uma nova com delegação para Microsoft.Sql/managedInstances.

📸 Adicione aqui um print da tela de criação com todos os campos preenchidos.

    Clique em Avançar > Avançar > Criar após a validação.

⏳ Etapa 2: Aguardar a Provisão

    🚧 Pode levar 30–60 minutos para a criação da instância. Durante esse tempo, você pode preparar a conexão do lado cliente.

🔗 Etapa 3: Conectar-se à Instância SQL
⚙️ Configurar firewall e rede

    Após criada, vá até a instância e clique em Configurações > Conectividade.
    Anote o endpoint de conexão.
    Confirme se sua máquina cliente pode acessar a VNet (via IP público ou peering de rede).

📸 Adicione aqui um print da tela de conectividade mostrando o nome DNS da instância.
💻 Etapa 4: Conectando via Cliente SQL
🪟 Windows (SSMS - SQL Server Management Studio)

    Abra o SSMS.
    No campo Server name, insira o nome DNS da instância (ex: sqlmi-demo.public.xxx.database.windows.net).
    Método de autenticação: SQL Server Authentication.
    Usuário: sqladmin
    Senha: [senha definida]

✅ Clique em "Connect".

📸 Adicione aqui print da tela do SSMS com os campos preenchidos.
🐧 Linux (Azure Data Studio ou sqlcmd)
🛠️ Usando Azure Data Studio:

    Abra o app.
    Clique em "Nova Conexão".
    Preencha:

Campo 	Valor
Server 	sqlmi-demo.public.xxx.database.windows.net
Authentication 	SQL Login
Username 	sqladmin
Password 	[senha definida]

✅ Clique em "Connect".

📸 Adicione aqui print da conexão no Azure Data Studio.
🖥️ Usando sqlcmd no terminal:

sqlcmd -S sqlmi-demo.public.xxx.database.windows.net -U sqladmin -P "SuaSenhaAqui"


🧪 Etapa 5: Testar com uma Query
SELECT name, create_date FROM sys.databases;


🛡️ Considerações de Segurança

    Não exponha a instância publicamente sem controle de IP ou túnel VPN.

    Use Azure Private Link e grupos de segurança para ambientes reais.

    Ative auditoria e políticas de retenção conforme necessário.


🧠 Conclusão

Você agora tem uma Instância Gerenciada de SQL no Azure conectada com cliente local, pronta para uso com segurança e alta disponibilidade.

