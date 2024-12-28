# AWS-Service-Manager-via-Web
Este projeto oferece uma interface web simples para gerenciar os seguintes serviços da AWS:  Route 53: Gerenciar Zonas Hospedadas. CloudFront: Configurar Distribuições. ELB (Elastic Load Balancer): Gerenciar Load Balancers.
### Aqui está o README atualizado com as mudanças solicitadas e o código HTML diretamente inserido:

---

# AWS Service Manager - Gerenciamento de Serviços AWS

Este projeto oferece uma interface web simples para gerenciar os seguintes serviços da AWS:

- **Route 53**: Gerenciar Zonas Hospedadas.
- **CloudFront**: Configurar Distribuições.
- **ELB (Elastic Load Balancer)**: Gerenciar Load Balancers.

---

## ⚙️ Pré-requisitos

1. **Conta AWS** com permissões apropriadas para acessar Route 53, CloudFront e ELB.
2. **Identity Pool ID** do Amazon Cognito para autenticação.
3. **Servidor Web** para servir o arquivo `index.html` (opcional para visualização local).

---

## 🚀 Instruções para Uso

1. Clone ou baixe o repositório.
2. Abra o arquivo `index.html` diretamente no navegador.
3. O código para a página inicial está descrito abaixo.

---

## 2. Página Web Inicial

Aqui está o código completo com **HTML**, **CSS**, e **JavaScript** para a página funcional:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AWS Service Manager</title>
  <script src="https://sdk.amazonaws.com/js/aws-sdk-2.1354.0.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f9f9f9;
      color: #333;
      margin: 0;
      padding: 0;
    }

    .container {
      max-width: 800px;
      margin: auto;
      padding: 20px;
      background: #fff;
      border-radius: 8px;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2);
    }

    h1, h2 {
      color: #007BFF;
      text-align: center;
    }

    button {
      margin: 10px 0;
      padding: 10px 15px;
      background: #007BFF;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background: #0056b3;
    }

    div {
      margin: 20px 0;
    }

    #route53-output, #cloudfront-output, #elb-output {
      background: #e9ecef;
      padding: 10px;
      border-radius: 5px;
      margin-top: 10px;
      white-space: pre-wrap;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🌐 AWS Service Manager</h1>
    <p>Gerencie seus serviços AWS diretamente nesta interface.</p>

    <div>
      <h2>📌 Route 53: Gerenciar Domínios</h2>
      <button onclick="listHostedZones()">Listar Zonas</button>
      <div id="route53-output"></div>
    </div>

    <div>
      <h2>🚀 CloudFront: Configuração de Distribuições</h2>
      <button onclick="listDistributions()">Listar Distribuições</button>
      <div id="cloudfront-output"></div>
    </div>

    <div>
      <h2>⚖️ ELB: Gerenciar Load Balancers</h2>
      <button onclick="listLoadBalancers()">Listar Load Balancers</button>
      <div id="elb-output"></div>
    </div>
  </div>

  <script>
    // Configuração do AWS SDK
    AWS.config.update({
      region: "us-east-1", // Substitua pela sua região
      credentials: new AWS.CognitoIdentityCredentials({
        IdentityPoolId: "IDENTITY_POOL_ID", // Substitua pelo seu Identity Pool ID
      }),
    });

    // Route 53: Listar Zonas Hospedadas
    function listHostedZones() {
      const route53 = new AWS.Route53();
      route53.listHostedZones({}, (err, data) => {
        const output = document.getElementById("route53-output");
        if (err) {
          console.error("Erro Route 53:", err);
          output.textContent = `❌ Erro ao listar zonas: ${err.message}`;
        } else {
          output.textContent = `✅ Zonas Hospedadas:\n${data.HostedZones.map(
            (zone) => `- ${zone.Name} (${zone.Id})`
          ).join("\n")}`;
        }
      });
    }

    // CloudFront: Listar Distribuições
    function listDistributions() {
      const cloudFront = new AWS.CloudFront();
      cloudFront.listDistributions({}, (err, data) => {
        const output = document.getElementById("cloudfront-output");
        if (err) {
          console.error("Erro CloudFront:", err);
          output.textContent = `❌ Erro ao listar distribuições: ${err.message}`;
        } else {
          output.textContent = `✅ Distribuições Encontradas:\n${data.DistributionList.Items.map(
            (dist) => `- ID: ${dist.Id}, Domínio: ${dist.DomainName}`
          ).join("\n")}`;
        }
      });
    }

    // ELB: Listar Load Balancers
    function listLoadBalancers() {
      const elb = new AWS.ELBv2(); // Usar ELBv2 para ALB e NLB
      elb.describeLoadBalancers({}, (err, data) => {
        const output = document.getElementById("elb-output");
        if (err) {
          console.error("Erro ELB:", err);
          output.textContent = `❌ Erro ao listar Load Balancers: ${err.message}`;
        } else {
          output.textContent = `✅ Load Balancers Encontrados:\n${data.LoadBalancers.map(
            (lb) => `- ${lb.LoadBalancerName}, DNS: ${lb.DNSName}`
          ).join("\n")}`;
        }
      });
    }
  </script>
</body>
</html>
```

---

## 📚 Funcionalidades

- **Interface intuitiva**: Botões simples para listar recursos.
- **Visualização de resultados**: Exibe os dados diretamente na página.
- **Integração direta com AWS SDK**.

---

# 🌐  A imagem da Página Web como ficará com todos sos serviços inseridos 

![Descrição da Imagem](caminho/para/minha_imagem.png)


## 🛠️ Customização

- Substitua `IDENTITY_POOL_ID` pelo seu **ID do Cognito Identity Pool**.
- Atualize a região (`region`) de acordo com a localização dos seus serviços AWS.

---

## 🧪 Testes

- Certifique-se de que as credenciais do AWS Cognito são válidas.
- Teste cada funcionalidade acessando a página e clicando nos botões para garantir que a comunicação com os serviços AWS esteja funcionando corretamente.

--- 

Agora você pode gerenciar seus serviços AWS de maneira simples e eficaz diretamente do navegador! 🚀
