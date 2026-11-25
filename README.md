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

O Spring Boot aceita as variáveis `SPRING_*` acima como substituições da configuração. A propriedade JWT já consulta `JWT_SECRET`.

```sh
./mvnw spring-boot:run
```

No Windows, use `.\mvnw.cmd spring-boot:run`. O frontend espera a API em `http://localhost:8080`.

## Tecnologias

Java 17, Spring Boot 3.2.5, Spring Data JPA, Spring Security, PostgreSQL, Flyway e Maven.
