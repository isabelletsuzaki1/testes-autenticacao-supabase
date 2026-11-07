# Introdução

**Atividade individual — Testes de Caixa Cinza em API de Autenticação**  
**Aluna:** Isabelle Naomi Tsuzaki  
**Curso:** Análise e Desenvolvimento de Sistemas — FACENS  
**Data de execução:** 07/11/2026

Este repositório contém a documentação e os artefatos utilizados na avaliação da API de autenticação do Supabase, usando Postman Desktop. Os resultados e capturas de tela 

# Objetivo da Atividade

Configurar autenticação por e-mail e senha no Supabase, preparar requisições HTTP no Postman, executar cinco cenários de caixa cinza e documentar respostas, status HTTP, tokens e falhas observadas.

# Configuração do Supabase

1. Criar uma conta e um projeto em https://supabase.com/dashboard.
2. Selecionar um nome de projeto e a região; configurar a senha do banco de dados (não compartilhar).
3. Em **Authentication > Providers**, confirmar que o provedor **Email** está habilitado.
4. Em **Authentication > Users**, criar um usuário de teste com e-mail e senha próprios. Caso a confirmação de e-mail esteja exigida, confirmar o usuário antes de testar o login.
5. Copiar a **Project URL** e uma chave adequada em **Settings > API Keys**; para esta coleção, usar **legacy anon (JWT)**, pois o header `Authorization: Bearer {{api_key}}` não aceita uma chave moderna `sb_publishable_...` como bearer.
6. Salvar a URL e as credenciais **apenas no Environment local do Postman**.

**Finalidade:** disponibilizar uma API real de autenticação para validação controlada de entradas válidas e inválidas.

**Dados não sensíveis do ambiente:**  
- Projeto: `PREENCHER`
- Região: `PREENCHER`
- URL de API: `https://SEU_PROJETO.supabase.co` (substituir)
- Autenticação: e-mail + senha

**Dados do ambiente:**
- Projeto: testes-autenticação
- Região: Leste dos EUA (Virgínia do Norte)
- URL da API: https://wjkoxtrufvsobopbjrhk.supabase.co
- Autenticação: E-mail + senha
- Usuário de teste: teste.login01@gmail.com

# Configuração do Postman

1. Instalar o **Postman Desktop** e criar um Workspace para a atividade.
2. Importar `postman/supabase-auth.postman_collection.json`.
3. Importar `postman/supabase-modelo.postman_environment.json`.
4. Preencher localmente `base_url`, `api_key`, `email` e `password`; selecionar esse Environment.
5. Verificar que o endereço `base_url` não termina com `/` e que o usuário está confirmado.
6. Executar cada requisição individualmente e analisar o código HTTP, o corpo JSON e os testes da aba **Test Results**.

| Variável | Finalidade |
|---|---|
| `base_url` | URL do projeto Supabase |
| `api_key` | Chave **legacy anon JWT** usada em `apikey` e `Authorization` |
| `email` | E-mail do usuário de teste |
| `password` | Senha do usuário de teste |
| `access_token` | Token armazenado no ambiente após login válido; não exportar |

**Evidências reais:**
- ![Workspace](prints/06-workspace.png)
- ![Environment](prints/07-environment.png)
- ![Organização da collection](prints/08-collection.png)

# Configuração das Requisições

**Método:** `POST`  
**Endpoint:** `/auth/v1/token?grant_type=password`  
**URL completa:** `{{base_url}}/auth/v1/token?grant_type=password`

### Headers

| Header | Valor |
|---|---|
| `apikey` | `{{api_key}}` (valor real oculto) |
| `Authorization` | `Bearer {{api_key}}` (chave **legacy anon JWT**) |
| `Content-Type` | `application/json` |

> Atenção: a chave moderna `sb_publishable_...` não deve ser enviada como Bearer. Se o projeto só disponibilizar chaves modernas, será necessário adaptar a estratégia do header de Authorization e validar o comportamento com a documentação atual do Supabase.

### Body JSON — exemplo ilustrativo

```json
{
  "email": "usuario@email.com",
  "password": "123456"
}
```

A collection substitui o exemplo por `{{email}}` e `{{password}}` no cenário de sucesso. Nos outros cenários, manipula os campos para simular entradas incorretas. As credenciais ilustrativas não representam usuários reais.

**Evidências reais:**
- ![Endpoint POST](prints/09-endpoint.png)
- ![Headers](prints/10-headers.png)
- ![Body JSON](prints/11-body.png)

# Execução dos Testes

Os testes devem ser executados **pelo aluno** no Postman Desktop. A coleção já contém cinco requisições, cada uma com verificações automatizadas em JavaScript. Não há resultados preenchidos antecipadamente.

| ID | Cenário | Entrada utilizada | Resultado esperado | Resultado obtido | Status |
|---|---|---|---|---|---|
| TC01 | Login válido | E-mail e senha corretos | HTTP 200 e `access_token` | PENDENTE | Não executado |
| TC02 | Senha incorreta | E-mail válido e senha modificada | Erro de autenticação, sem token | PENDENTE | Não executado |
| TC03 | Usuário inexistente | E-mail não cadastrado | Acesso negado, sem token | PENDENTE | Não executado |
| TC04 | Campos vazios | E-mail e senha vazios | Erro de validação, sem token | PENDENTE | Não executado |
| TC05 | Credenciais inválidas | E-mail e senha incorretos | Mensagem de erro, sem token | PENDENTE | Não executado |

**Observação:** os códigos exatos das respostas inválidas podem variar conforme a configuração da API; registrar o código efetivamente observado. Os scripts aceitam códigos usuais de rejeição e exigem que não seja retornado token.

**Evidências reais:**
- ![Login válido: status e corpo sem mostrar token completo](prints/12-login-valido.png)
- ![Senha incorreta](prints/13-senha-incorreta.png)
- ![Usuário inexistente](prints/14-usuario-inexistente.png)
- ![Campos vazios](prints/15-campos-vazios.png)
- ![Credenciais inválidas](prints/16-credenciais-invalidas.png)

# Registro dos Testes

Os cinco testes são documentados na planilha `planilha/registro-testes.xlsx`, com os campos ID, Cenário, Entrada, Resultado esperado, Resultado obtido, Status e Observações. Após cada requisição, preencher resultados e observações a partir do Postman.

A planilha fornece rastreabilidade, permite identificar divergências entre o comportamento esperado e o observado e comprova a cobertura dos cenários. Não registrar senhas ou tokens completos.

**Evidência real:**
- ![Planilha preenchida](prints/17-planilha-preenchida.png)

# Resultados Obtidos

**Total de cenários previstos:** 5  
**Cenários executados:** PREENCHER  
**Cenários aprovados:** PREENCHER  
**Cenários reprovados:** PREENCHER

**Resultados e mensagens de erro observados:**  
PREENCHER APÓS A EXECUÇÃO.

**Falhas técnicas identificadas:**  
PREENCHER APÓS A EXECUÇÃO. Respostas de erro esperadas **não** significam, por si só, defeito da API.

# Conclusão

**Execução e funcionamento:** PREENCHER APÓS A EXECUÇÃO.  
**Dificuldades encontradas:** PREENCHER.  
**Falhas identificadas:** PREENCHER.  
**Melhorias propostas:** considerar tratamento de erros consistente, políticas de senha, autenticação multifator, limites de tentativas e logs apropriados.  
**Importância dos testes caixa cinza:** permitem verificar comportamento funcional e contratos HTTP com conhecimento parcial da implementação, sem depender de uma interface gráfica.

## Referências

- https://supabase.com/docs/guides/auth/passwords
- https://supabase.com/docs/guides/getting-started/api-keys
- https://supabase.com/docs/guides/getting-started/migrating-to-new-api-keys

## Segurança do repositório

Não publicar senha de usuário, credenciais administrativas, `service_role`, `sb_secret_...`, tokens de acesso ou respostas que contenham tokens visíveis. O arquivo de Environment do repositório é apenas um **modelo com valores vazios**. 
