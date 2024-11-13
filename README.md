# AzureContainerApps_2024-11

Slides e conteúdos de apresentação sobre Azure Container Apps realizada no dia 13/11/2024.

Todas as imagens utilizadas estão no **Docker Hub**.

## Aplicação 

Imagem: **renatogroffe/apicontagem-dotnet8-alpine:4**

Preencher a variável **ConnectionStrings__ApplicationInsights** para habilitar o monitoramento com **Application Insights**.

## Worker

Imagem: **renatogroffe/workertests-dotnet8:2**

Script KEDA utilizado como base:

```yaml
apiVersion: keda.sh/v1alpha1
kind: ScaledObject
metadata:
  name: cron-scaledobject
spec:
  minReplicaCount: 4
  scaleTargetRef:
    name: workertests-cron
  triggers:
  - type: cron
    metadata:
      timezone: America/Sao_Paulo
      start: 55 23 * * *
      end: 58 23 * * *
      desiredReplicas: "10"
```

## Job

Imagem: **renatogroffe/dotnet9-job-notificacao**

Webhook para tratar as requisições: **https://github.com/renatogroffe/ASPNETCore8-REST_API-Logging-MonitoramentoWebhooks**
