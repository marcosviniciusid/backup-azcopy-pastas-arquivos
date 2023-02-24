# backup-azcopy-pastas-arquivos
Backup de pastas/arquivos do servidor Linux para o Storage Account no Azure.

`Criar arquivo.sh`

```
#!/bin/bash

# ===========================================
# Backup externo para pastas/arquivos
# version 1, atualizado em 24 fev, 2023
# copyright 2023 Marcos Vinicius @empresa
# ============================================

# Data de Hoje
data=$(date +\%-d-\%-m-\%-Y)

# Site/Sistema
site='glpi'

# Arquivo (Exemplo)
path='/var/www/html/glpi/sound/'

# Variaveis do Blob/Container
blob='nome-storage-account'
container='nome-container-blob'
token='sas-do-container-blob'

# Token SAS
sas="https://$blob.blob.core.windows.net/$container/$site/files/?$token"

# AzCopy -> Storage Account (stowebapp)
/home/az_copy/azcopy cp --recursive $path "$sas"
```
# Agendar no Crontab o backup
`crontab -e`
```
# CRONTAB - backup externo
0 23 * * * bash /home/scripts/azcopy_db_glpi.sh
```
