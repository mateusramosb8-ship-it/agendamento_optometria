# Agenda de avalia\u00e7\u00e3o visual

Projeto de agendamento para consult\u00f3rios de optometria. O paciente escolhe um profissional, uma data e um hor\u00e1rio sem criar conta. A equipe administra os agendamentos em \u0060/consultorio\u0060.

> O GitHub guarda o c\u00f3digo e este README. Ele ainda n\u00e3o coloca o site online para seus clientes.

## Tecnologias

- **React e TypeScript:** telas e intera\u00e7\u00f5es do site.
- **Node.js e JavaScript:** API que valida e registra as reservas.
- **SQLite:** banco local usado nesta vers\u00e3o.
- **Astryx:** componentes visuais.
- **Vite:** servidor de desenvolvimento local.

## Abrir no seu computador

Instale Node.js 22.13 ou superior e depend\u00eancias com \u0060npm ci\u0060. Abra dois terminais PowerShell nesta pasta.

No primeiro terminal, inicie a API:

\u0060\u0060\u0060powershell
$env:ADMIN_PASSWORD='sua-senha-local'
$env:CLINIC_ID='fabio-ramos'
npm run api
\u0060\u0060\u0060

No segundo terminal, inicie o site:

\u0060\u0060\u0060powershell
npm run dev
\u0060\u0060\u0060

Depois, no navegador, abra http://127.0.0.1:5173/ para ver o agendamento ou http://127.0.0.1:5173/consultorio para abrir o painel administrativo. O ID inicial do consult\u00f3rio \u00e9 \u0060fabio-ramos\u0060.

**Para mostrar ao cliente:** se ele estiver ao seu lado, abra a p\u00e1gina de agendamento neste computador. O endere\u00e7o local n\u00e3o abre no computador ou celular dele. Para enviar um link remoto, primeiro precisamos hospedar o site e a API em um servi\u00e7o online com banco de dados e HTTPS.

## Profissionais

O paciente escolhe um profissional antes de selecionar hor\u00e1rio. Cada profissional tem seus pr\u00f3prios hor\u00e1rios ocupados. O painel permite cadastrar, renomear e desativar profissionais. O expediente \u00e9 compartilhado entre profissionais do mesmo consult\u00f3rio.

## V\u00e1rios consult\u00f3rios

Esta vers\u00e3o configura um consult\u00f3rio por instala\u00e7\u00e3o usando \u0060CLINIC_ID\u0060. Ainda n\u00e3o existe um painel central para cadastrar contas de clientes, e alguns contatos e textos s\u00e3o espec\u00edficos do Fabio Ramos. Antes de vender o servi\u00e7o para outros consult\u00f3rios, ser\u00e1 preciso tornar esses dados edit\u00e1veis e preparar uma hospedagem segura. A migra\u00e7\u00e3o para Supabase ser\u00e1 planejada em outra conversa.

## Senhas e dados

N\u00e3o publique senhas, arquivos locais ou o banco de pacientes. O arquivo de senha local e a pasta \u0060data\u0060 ficam fora do Git. A senha administrativa deve ser configurada no computador ou no servi\u00e7o de hospedagem, nunca escrita no c\u00f3digo.

## Verificar

\u0060\u0060\u0060powershell
npm run build
npm test
\u0060\u0060\u0060
