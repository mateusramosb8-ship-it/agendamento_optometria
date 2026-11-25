# Agenda de avalia��o visual

Aplica��o de agendamento para consult�rios de optometria. Pacientes escolhem profissional, data e hor�rio sem criar conta; a equipe entra em `/consultorio` para administrar reservas, profissionais, expediente e banner.

> Projeto em desenvolvimento. Este reposit�rio publica o c�digo, n�o hospeda a aplica��o. O endere�o `localhost` s� funciona no computador onde os servidores est�o rodando.

## Tecnologias

| Camada | Tecnologia | Responsabilidade |
| --- | --- | --- |
| Interface | React, TypeScript, Vite e Astryx | Telas, calend�rio, formul�rios e pr�via local |
| API | Node.js (JavaScript, m�dulos ES) | Valida��o, login da equipe e regras das reservas |
| Dados | SQLite (`node:sqlite`) | Consult�rios, profissionais, hor�rios, banner e agendamentos |
| Testes | `node:test` | Regras, autentica��o e separa��o das agendas |

## Executar no Windows

Instale Node.js 22.13 ou superior. No PowerShell, dentro da pasta deste projeto:

```powershell
npm ci
```

Abra **dois terminais** na pasta. No primeiro, configure uma senha administrativa de 12 a 128 caracteres para este computador e ligue a API:

```powershell
$env:ADMIN_PASSWORD='uma-senha-forte-que-voce-escolheu'
$env:CLINIC_ID='fabio-ramos'
npm run api
```

N�o coloque a senha no c�digo, README ou em arquivos enviados ao GitHub. O script `./start-api.ps1` s� funciona no computador que j� possui o arquivo local criptografado `.admin-password.dpapi`; ele n�o � distribu�do pelo reposit�rio.

No segundo terminal:

```powershell
npm run dev
```

Abra [a p�gina de agendamento](http://127.0.0.1:5173/) ou [o painel do consult�rio](http://127.0.0.1:5173/consultorio). No painel, informe o ID definido em `CLINIC_ID` e a senha definida em `ADMIN_PASSWORD`. O ID inicial � `fabio-ramos`.

Se o navegador mostrar erro ao carregar a agenda, confira se **os dois terminais** continuam abertos. Para parar os servidores, pressione `Ctrl+C` em cada terminal.

## Como funciona o agendamento

1. O consult�rio entra em `/consultorio`, cadastra profissionais e ajusta o expediente.
2. O paciente escolhe profissional, data e hor�rio livre; informa nome e telefone com DDD e confirma.
3. A API confere novamente a disponibilidade antes de salvar. Reservas do mesmo hor�rio podem existir para profissionais diferentes; o mesmo profissional n�o pode receber duas reservas no mesmo hor�rio.
4. A equipe pode agendar manualmente, atualizar a lista, cancelar reservas, desativar profissionais sem reservas futuras e editar o banner.

Na atualiza��o de um banco antigo, os agendamentos existentes s�o associados ao profissional principal. Registros anteriores s�o preservados.

## Mais de um consult�rio

Cada execu��o da aplica��o atende **um consult�rio**, identificado por `CLINIC_ID`. Os agendamentos e profissionais s�o marcados com o ID do consult�rio e as opera��es do painel filtram esse ID. Para instalar para outro consult�rio, configure uma implanta��o e banco pr�prios, com outra senha e outro `CLINIC_ID`, e ajuste os dados pelo painel.

Nesta vers�o, o expediente e a dura��o s�o compartilhados pelos profissionais de um mesmo consult�rio, embora as reservas sejam separadas por profissional. Endere�o, telefone e informa��es institucionais ainda est�o fixos para Fabio Ramos na interface. Antes de entregar a outro consult�rio, esses dados precisam ser transformados em configura��es edit�veis. Um painel central para cadastrar consult�rios e um �nico servidor para v�rias cl�nicas ainda n�o est�o implementados.

## Seguran�a e opera��o

- A senha n�o deve ser versionada. A API armazena um hash; a sess�o administrativa usa cookie HttpOnly.
- `data/agenda.sqlite`, vari�veis locais e a senha criptografada deste computador devem ficar fora do Git. O banco cont�m dados pessoais e exige acesso restrito e c�pias de seguran�a.
- O telefone n�o � confirmado por SMS. Cancelamentos de pacientes s�o solicitados ao consult�rio.
- A API local escuta em `127.0.0.1:8787`; Vite encaminha `/api` durante o desenvolvimento. Publicar no GitHub **n�o** disponibiliza o servi�o para pacientes. Produ��o exige HTTPS, servidor, dom�nio, backup e controle de acesso.

## Verificar altera��es

```powershell
npm run build
npm test
```
