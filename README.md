# TimeSync Backend

API do TimeSync para gestão de agendamentos e serviços. A interface web está no [repositório do frontend](https://github.com/MatheusHVM/time-sync-frontend).

## Funcionalidades

- Consulta de agendamentos por empresa, criação, edição, reagendamento e cancelamento.
- Cadastro, edição, exclusão e consulta de serviços vinculados a empresas e usuários.
- Indicadores de agendamentos por mês, serviços mais realizados e faturamento semestral, com filtro por empresa e funcionário.
- Autenticação com Spring Security e JWT, além de envio de e-mails por SMTP.

## Executar localmente

Use Java 17 e uma instância PostgreSQL. Crie um banco local e conceda ao usuário da aplicação permissões para aplicar as migrações Flyway. As migrações estão em [src/main/resources/db/migration](src/main/resources/db/migration).

Configure as variáveis no ambiente da JVM antes de iniciar. Use `jdbc:postgresql://localhost:5432/time_sync?currentSchema=public` como exemplo de URL local.

| Variável | Finalidade |
| --- | --- |
| `SPRING_DATASOURCE_URL` | URL JDBC do PostgreSQL |
| `SPRING_DATASOURCE_USERNAME` | Usuário do PostgreSQL |
| `SPRING_DATASOURCE_PASSWORD` | Senha do PostgreSQL |
| `JWT_SECRET` | Segredo de assinatura JWT |
| `SPRING_MAIL_USERNAME` | Conta usada na autenticação SMTP |
| `SPRING_MAIL_PASSWORD` | Credencial SMTP |

Defina as variáveis acima no ambiente do processo antes de iniciar a API. O banco, a autenticação JWT e o SMTP não têm credenciais padrão. Use credenciais próprias para desenvolvimento e mantenha os valores fora do Git. Os parâmetros do servidor SMTP podem ser ajustados com `SPRING_MAIL_HOST` e `SPRING_MAIL_PORT`.

```sh
./mvnw spring-boot:run
```

No Windows, use `.\mvnw.cmd spring-boot:run`. O frontend espera a API em `http://localhost:8080`.

## Migrações e testes

O Flyway aplica automaticamente as migrações ao iniciar. Elas incluem contas de demonstração, inclusive uma conta administrativa, além de empresas, serviços e agendamentos de exemplo. Use um banco descartável para desenvolvimento e testes. Antes de usar a aplicação em um ambiente compartilhado, revise o provisionamento dessas contas e desative ou redefina as credenciais de demonstração. Preserve as migrações já aplicadas para manter os checksums do Flyway.

Execute `./mvnw test` (Windows: `.\mvnw.cmd test`) com a mesma configuração de ambiente apontando para o banco de teste. O teste de contexto Spring inicializa a aplicação e aplica as migrações nesse banco.

## Tecnologias

Java 17, Spring Boot 3.2.5, Spring Data JPA, Spring Security, PostgreSQL, Flyway e Maven.
