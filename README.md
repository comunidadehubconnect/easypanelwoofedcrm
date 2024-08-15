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

Va ate final da pagina

![image](https://github.com/comunidadehubconnect/easypanelwoofedcrm/assets/91642837/828a9e88-45f2-4b6b-98f1-ab4f164d2889)

Adicione codigo abaixo dentro do Schema

![image](https://github.com/comunidadehubconnect/easypanelwoofedcrm/assets/91642837/74b97f33-e5d2-495d-aaba-25bb8b433adf)

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
        "password": "woofed-redis"
      }
    }
  ]
}
```

Adicione codigo abaixo dentro do Schema com credenciais Postgres e Redis alteradas

![image](https://github.com/comunidadehubconnect/easypanelwoofedcrm/assets/91642837/74b97f33-e5d2-495d-aaba-25bb8b433adf)

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
        "env":"ENABLE_USER_SIGNUP=true \nRAILS_ENV=production \nRACK_ENV=production \nNODE_ENV=production \nMOTOR_AUTH_USERNAME=admin \nMOTOR_AUTH_PASSWORD=admin \nFRONTEND_URL=https://$(PRIMARY_DOMAIN) \nDATABASE_URL= seu endereçodopostgres \nREDIS_URL=seuenderço do redis \nACTIVE_STORAGE_SERVICE=local \nRAILS_LOG_LEVEL=debug \nDEFAULT_TIMEZONE=Brasilia \nLANGUAGE=pt-BR",
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
        "env":"ENABLE_USER_SIGNUP=true \nRAILS_ENV=production \nRACK_ENV=production \nNODE_ENV=production \nMOTOR_AUTH_USERNAME=admin \nMOTOR_AUTH_PASSWORD=admin \nFRONTEND_URL=https://$(PRIMARY_DOMAIN) \nDATABASE_URL= seu endereçodopostgres \nREDIS_URL=seuenderço do redis \nACTIVE_STORAGE_SERVICE=local \nRAILS_LOG_LEVEL=debug \nLANGUAGE=pt-BR",
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
        "env":"ENABLE_USER_SIGNUP=true \nRAILS_ENV=production \nRACK_ENV=production \nNODE_ENV=production \nMOTOR_AUTH_USERNAME=admin \nMOTOR_AUTH_PASSWORD=admin \nFRONTEND_URL=https://$(PRIMARY_DOMAIN) \nDATABASE_URL= seu endereçodopostgres \nREDIS_URL=seuenderço do redis \nACTIVE_STORAGE_SERVICE=local \nRAILS_LOG_LEVEL=debug \nLANGUAGE=pt-BR",
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

Depois de subir a template preciso subir o comando abaixo na console do Woofed

![image](https://github.com/comunidadehubconnect/easypanelwoofedcrm/assets/91642837/bf3585f0-ae3a-4c58-b1ce-6ba69f2f97bc)


```bash
rails db:migrate 
```

#dentro da do app woofed

Url Cliente

https://seudominio.com.br/users/sign_in

https://seudominio.com.br/motor_admin/

Pronto tudo Funcionando ✅😎

Creditos: Andre Marques
