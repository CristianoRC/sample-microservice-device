# Sample - Microservice Device
[![Build Status](https://dev.azure.com/NerdAllDebug/PalestraMVP/_apis/build/status/Sample-Microservice-Device-CI?branchName=master)](https://dev.azure.com/NerdAllDebug/PalestraMVP/_build/latest?definitionId=1&branchName=master)

Criado como um exemplo pr�tico, este microsservi�o envia eventos para o Event Hub da Microsoft quando feito uma chamada POST no endpoint ***api/manager***.

Macro fun��o:

1. Enviar uma mensagem para a fila do Event Hub.

## Vis�o geral macro para esse microsservice

![Nerd All Debug GitHub - Overview of macros for this microservice (Manager Device)](macro-sample-microservice-device.png)

### Enviar uma mensagem para a fila do Event Hub

Receber um est�mulo via HTTP POST, enviando assim a mensagem para o Event Hub.
\
_Configura��o do Event Hub [clique aui](#event-hub)_

## Configuration
Usando o design pattern options, as configura��es s�o gravadas no arquivo de configura��o ***appsettings.json***.
\
Seguem as configura��es para cada se��o do arquivo de configura��o:

### ConnectionStrings
Esse microservice usa o MySql como banco de dados.
\
Nesta se��o voc� deve colocar a connectionstring que corresponde ao MySql.
```json
{
  "ConnectionStrings": {
    "DefaultConnectionConfiguration": "MySql ConnectionString"
  }
}
```
### Globalization
Por padr�o, a globaliza��o do microservice est� em ingl�s.
```json
{
  "Globalization": {
    "DefaultEnvironmentCulture": "en-US",
    "DefaultRequestCulture": "en-US",
    "SupportedCultures": [ "en-US", "pt-BR" ],
    "SupportedUICultures": [ "en-US", "pt-BR" ]
  }
}
```
### Host
O Host representa a identifica��o do microservice, importante para a rastreabilidade e seguran�a das APIs.
* ApplicationHost: endere�o onde o microservice est� hospedado;
* ApplicationName: nome do microservice;
* AuthorizationToken: GUID gerado para limitar o acesso ao microsservi�o. Os ambientes t�m tokens diferentes, portanto, para acessar as APIs, voc� precisar� obter o token do ambiente que est� acessando.
```json
{
  "Host": {
    "ApplicationHost": "https://sample-microservice-device.azurewebsites.net/",
    "ApplicationName": "Sample - Microservice Device",
    "AuthorizationToken": "c71310fa00d949368c7e845fbdb641b6"
  }
}
```

### Logs
Todas as aplica��es devem ter logs registrados no Reposit�rio de Log. Aqui temos a se��o de log, *Erro*.
```json
{
  "Logs": {
    "Error": {
	}
  }
}
```
#### Error
O log de erros � capturado automaticamente pelo host e enviado ao Reposit�rio de Log sempre que o microservice lan�a uma exce��o.
* ViewDetailsOnResponse: true para exibir o erro na resposta da API, caso contr�rio, false. 
```json
{
  "Logs": {
    "Error": {
      "ViewDetailsOnResponse": true
    }
  }
}
```

### Event Hub
Configura��es do producer ou consumer do event hub.

#### Producers
As configura��es para enviar objetos ao event hub.
* Name: nome que identifica o producer na inje��o de depend�ncia;
* ConnectionString: conex�o do producer;
* EventHubName: nome que identifica o event hub na nuvem.
```json
{
  "EventHubs": {
    "Producers": [
      {
        "Name": "TransactionFlow",
        "ConnectionString": "Endpoint=<ENDPOINT>;SharedAccessKeyName=<SHARED_ACCESS_KEY_NAME>;SharedAccessKey=<SHARED_ACCESS_KEY>;EntityPath=<ENTITY_PATH>",
        "EventHubName": "<EVENT_HUB_NAME>"
      }
    ]
  }
}
```

## API REST
Para ver o release pipeline [clique aqui](https://dev.azure.com/NerdAllDebug/PalestraMVP/_release?_a=releases&view=mine&definitionId=1).

#### Apresenta��o 
* [![Build Status](https://vsrm.dev.azure.com/NerdAllDebug/_apis/public/Release/badge/98c93b17-e3bd-4372-97ce-9b2b54909071/1/1)](https://vsrm.dev.azure.com/NerdAllDebug/_apis/public/Release/badge/98c93b17-e3bd-4372-97ce-9b2b54909071/1/1)
* Para ver a documenta��o swagger [clique aqui](https://sample-microservice-device.azurewebsites.net/swagger/index.html).
