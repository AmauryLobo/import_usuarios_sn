# 🔄 ServiceNow: Automação de Importação de Usuários

Este projeto é uma **Scoped Application** desenvolvida no ServiceNow para automatizar a ingestão e atualização em massa de dados de utilizadores a partir de fontes externas (planilhas), garantindo a integridade dos dados na tabela oficial do sistema.

## 🎯 Objetivo do Projeto
Eliminar a carga manual de utilizadores pelo RH/TI, criando uma rotina automatizada que lê os dados, transforma-os e os insere/atualiza na base de forma segura.

## 🛠️ Tecnologias e Conceitos Aplicados
* **Scoped Application:** Desenvolvimento isolado utilizando o ServiceNow Studio/App Engine Studio.
* **Import Sets & Staging Tables:** Criação de tabelas temporárias (`u_novos_usuarios`) para receber os dados brutos.
* **Table Transform Maps:** Mapeamento de campos da tabela temporária para a tabela alvo (`sys_user`).
* **Data Integrity (Coalesce):** Implementação da regra de *Coalesce* no campo `email`. Isso garante que o sistema verifique se o utilizador já existe:
  * Se existir -> Atualiza os dados (Update).
  * Se não existir -> Cria um novo registo (Insert).
  * Previne a duplicação de dados na instância.
* **Scheduled Data Imports:** Configuração de uma rotina agendada (Scheduler) para executar a importação e transformação automaticamente, simulando uma integração diária na madrugada.

## 🚀 Como funciona o fluxo
1. A planilha externa é carregada no **Data Source**.
2. O **Scheduled Import** inicia o processo no horário definido.
3. Os dados vão para a **Staging Table**.
4. O **Transform Map** entra em ação, validando o *Coalesce* e transportando os dados limpos para a `sys_user`.
