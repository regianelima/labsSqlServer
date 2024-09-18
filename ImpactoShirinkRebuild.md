# Uso do shrink e impacto na desfragmentação dos índices


###### Evite diminuir o tamanho dos seus bancos de dados e files, mas quando o fizer faça em um momento que tenha pouco acesso ou nenhum acesso e jobs rodando. 

###### Não faça a compactação do banco de dados (SHRINKDATABASE), mas sim dos arquivos específicos através do (SHRINKFILES).

###### Logo após faça rebuild de todos os índices ou atualize todas as estatísticas.






1. Crie um banco de dados 

use master
go

CREATE DATABASE DB_Teste
go
ALTER DATABASE DB_Teste SET RECOVERY FULL
go


2. Crie uma tabela com 5 milhões de linhas e um índice para essa tabela 

DROP TABLE IF exists DB_Teste.dbo.Messages
go
SELECT TOP 5000000 o.object_id, m.*
  INTO dbo.Messages
  FROM sys.messages m
  CROSS JOIN sys.all_objects o;
GO
CREATE UNIQUE CLUSTERED INDEX IXnew ON dbo.Messages(object_id, message_id, language_id);
GO

use DB_Teste
go



3. Verifique a fragmentação do índice criado 




4. Olhe para o espaço vazio do meu banco de dados
5. Reduza o banco de dados para se livrar do espaço vazio
6. E então veja o que acontece a seguir.