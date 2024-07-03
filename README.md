<p align="center">
<img src="https://cwmkt.com.br/wp-content/uploads/2024/04/logo_github.png" width="240" />
<p align="center">Seja bem-vindo ao Guia de Instalação EasyPanel WoofedCRM 🚀</p>
</p>
  
<p align="center"> 
<a href="https://hubconnect.top" target="_blank">👉 Participe da Comunidade HubConnect 👈</a>
</p>

<hr />
<hr />

## Comando para Instalar EasyPanel

```bash
curl -sSL https://get.easypanel.io | sh
```

Adicione nome de Project

![48098522-0c485df00f5cadb0d329061c35fee46c](https://github.com/cwmkt/easypanelevotypebot/assets/91642837/b72c1359-91ca-4bf6-9fb1-32525ba5747b)

Clique na aba Templates

![48098535-90f9b4f370bb8b06cfd7e4acf0ee0f97](https://github.com/cwmkt/easypanelevotypebot/assets/91642837/03c1830c-621c-40b3-94ee-93eb568c8d2e)

```bash
{
  "services": [
    {
      "type": "postgres",
      "data": {
        "projectName": "woofed-db",
        "serviceName": "woofed-db",
        "image": "ramsrib/pgvector:latest"
      }
    },
    {
      "type": "redis",
      "data": {
        "projectName": "woofed",
        "serviceName": "woofed-redis",
        "password": "senha redis"
      }
    }
  ]
}
```


```bash
{
  "services": [
    {
      "type": "app",
      "data": {
        "projectName": "woofed",
        "serviceName": "woofed",
        "source": {
          "type": "image",
          "image": "douglara/woofedcrm:latest"
        },
        "domains": [
          {
            "host": "$(EASYPANEL_DOMAIN)",
            "port": 3000
          }
        ],
        "env":"ENABLE_USER_SIGNUP=true \nRAILS_ENV=production \nRACK_ENV=production \nNODE_ENV=production \nMOTOR_AUTH_USERNAME=admin \nMOTOR_AUTH_PASSWORD=admin \nFRONTEND_URL=https://$(PRIMARY_DOMAIN) \nDATABASE_URL= seu endereço do postgres \nREDIS_URL=seu enderço do redis \nACTIVE_STORAGE_SERVICE=local \nRAILS_LOG_LEVEL=debug",
        "mounts": [
          {
            "type": "volume",
            "name": "woofedcrm_data",
            "mountPath": "/app"
          }
        ]
      }
    },
    {
      "type": "app",
      "data": {
        "projectName": "sidekiq",
        "serviceName": "sidekiq",
        "source": {
          "type": "image",
          "image": "douglara/woofedcrm:latest"
        },
        "deploy": {
          "command": "bundle exec sidekiq -C config/sidekiq.yml"
        },
        "env":"ENABLE_USER_SIGNUP=true \nRAILS_ENV=production \nRACK_ENV=production \nNODE_ENV=production \nMOTOR_AUTH_USERNAME=admin \nMOTOR_AUTH_PASSWORD=admin \nFRONTEND_URL=https://$(PRIMARY_DOMAIN) \nDATABASE_URL=postgres://postgres:senhapostgres0@hubconnect_woofed-db:5432/hubconnect \nREDIS_URL=redis://default:senha redis@hubconnect_woofed-redis:6379 \nACTIVE_STORAGE_SERVICE=local \nRAILS_LOG_LEVEL=debug",
        "mounts": [
          {
            "type": "volume",
            "name": "woofedcrm_data",
            "mountPath": "/app"
          }
        ]
      }
    },
    {
      "type": "app",
      "data": {
        "projectName": "good_job",
        "serviceName": "good_job",
        "source": {
          "type": "image",
          "image": "douglara/woofedcrm:latest"
        },
        "deploy": {
          "command": "bundle exec good_job"
        },
        "env":"ENABLE_USER_SIGNUP=true \nRAILS_ENV=production \nRACK_ENV=production \nNODE_ENV=production \nMOTOR_AUTH_USERNAME=admin \nMOTOR_AUTH_PASSWORD=admin \nFRONTEND_URL=https://$(PRIMARY_DOMAIN) \nDATABASE_URL=postgres://postgres:senhapostgres0@hubconnect_woofed-db:5432/hubconnect \nREDIS_URL=redis://default:senha redis@hubconnect_woofed-redis:6379 \nACTIVE_STORAGE_SERVICE=local \nRAILS_LOG_LEVEL=debug",
        "mounts": [
          {
            "type": "volume",
            "name": "woofedcrm_data",
            "mountPath": "/app"
          }
        ]
      }
    }
  ]
}
```

#Apois subir a template preciso subir o comando 

```bash
rails db:migrate 
```

#dentro da do app woofed

Pronto tudo Funcionando ✅😎
