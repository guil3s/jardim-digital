---
{"dg-publish":true,"permalink":"/na-escuta/minha-vps/","created":"2026-06-25T21:09:39.774-03:00","updated":"2026-06-25T21:15:15.846-03:00","dg-note-properties":{}}
---

Contratei uma VPS há menos de uma semana. Por enquanto, a brincadeira rendeu isso aqui:

---

# Infraestrutura Pessoal – VPS

## Ambiente

- VPS Linux (Ubuntu Server 24.04 LTS)
    
- Docker
    
- Docker Manager
    
- Nginx Proxy Manager
    
- Rede Docker compartilhada para os serviços


---

# Domínios

## Domínio institucional

- migliorini.cloud


Subdomínios em operação:

- base.migliorini.cloud
    
- nuvem.migliorini.cloud
    
- cofre.migliorini.cloud


   

---

# Serviços implantados

## Nginx Proxy Manager

Utilizado para:

- Proxy reverso
    
- Certificados TLS/SSL (Let's Encrypt)
    
- Gerenciamento de subdomínios
    
- Redirecionamentos HTTPS


---

## BookStack

Sistema de documentação técnica utilizado para:

- Manuais
    
- Procedimentos
    
- Documentação da infraestrutura
    
- Base de conhecimento


---

## Nextcloud

Ambiente de nuvem privada para:

- Arquivos
    
- Compartilhamento
    
- Sincronização entre dispositivos


Integrado com:

- MariaDB
    
- Redis


---

## Vaultwarden

Gerenciador de senhas auto-hospedado.

Configuração atual:

- Cadastro público desabilitado
    
- HTTPS
    
- Proxy reverso
    
- Backup incluído na rotina da VPS


---

## Backrest

Interface gráfica para Restic.

Responsável por:

- Agendamento de backups
    
- Execução de backups
    
- Monitoramento
    
- Restauração


---

## Restic

Motor de backup utilizado para:

- Backups incrementais
    
- Deduplicação
    
- Compressão
    
- Criptografia


---

## Google Drive

Repositório remoto de backup.

Armazena:

- Snapshots da VPS
    
- Backups incrementais


---

## Uptime Kuma

Monitoramento dos serviços.

Utilizado para:

- Disponibilidade
    
- Status dos serviços
    
- Alertas


---

## Fail2Ban

Proteção contra ataques de força bruta.

---

# Banco de dados

MariaDB

Utilizado por:

- BookStack
    
- Nextcloud


---

# Cache

Redis

Utilizado pelo Nextcloud.

---

# Backup

Sistema implantado:

```
Containers
   │
   ▼
Backrest
   │
   ▼
Restic
   │
   ▼
Google Drive
```

Além disso:

- restauração testada;
    
- recuperação validada;
    
- backup dos volumes Docker;
    
- backup dos dumps dos bancos.


---

# Backup local

Rotina criada para:

- sincronizar o repositório Restic do Google Drive para SSD externo;
    
- backup do computador pessoal para SSD externo utilizando rclone.


---

# Segurança

Implementado:

- autenticação HTTPS
    
- certificados Let's Encrypt
    
- login SSH endurecido
    
- desativação do login direto do root
    
- firewall
    
- Fail2Ban
    
- gerenciamento centralizado de senhas


---

# Monitoramento

Monitoramento contínuo de:

- disponibilidade dos serviços;
    
- backups;
    
- containers Docker.


---

# Organização

Separação entre:

- infraestrutura interna;
    
- serviços públicos;
    
- domínio profissional;
    
- documentação técnica.


---

# Estrutura tecnológica

Atualmente a infraestrutura utiliza:

- Ubuntu Server
    
- Docker
    
- Docker Manager
    
- Nginx Proxy Manager
    
- BookStack
    
- Nextcloud
    
- MariaDB
    
- Redis
    
- Vaultwarden
    
- Restic
    
- Backrest
    
- Google Drive
    
- rclone
    
- Uptime Kuma
    
- Fail2Ban


---

# Próximas implantações previstas

- Homepage institucional
    
- E-mail profissional
    
- ONLYOFFICE
    
- Paperless-ngx
    
- Cal.com
    
- Chatwoot
    
- AnythingLLM
    
- Open WebUI


---

## Considerações

O objetivo da infraestrutura é concentrar, em ambiente próprio e sob controle do usuário.


---

