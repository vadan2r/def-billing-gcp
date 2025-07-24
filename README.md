# Definição de Orçamento de Billing na Google Cloud Platform (GCP)

Este documento detalha o processo passo a passo para configurar um orçamento de billing na Google Cloud Platform (GCP).  Os orçamentos de billing ajudam você a controlar e monitorar seus gastos na GCP, garantindo que você seja notificado quando seus custos se aproximarem ou excederem o limite definido.

## Pré-requisitos

*   Você precisa ter uma conta de billing ativa na GCP.
*   Você precisa ter permissões para criar e gerenciar orçamentos de billing. Geralmente, o papel `billing.budgets.editor` é suficiente.

## Passo 1: Acessando a página de Billing

1.  **Acesse o Console do Google Cloud:** Abra seu navegador e vá para [https://console.cloud.google.com/](https://console.cloud.google.com/).
2.  **Selecione sua organização ou projeto:** Certifique-se de ter selecionado a organização ou projeto correto no seletor na parte superior da tela.
3.  **Navegue até Billing:** No menu de navegação à esquerda, clique em "Billing".  Se a opção "Billing" não estiver visível, clique em "Mais Produtos" e procure por ela.

## Passo 2: Criando um Orçamento

1.  **Selecione a Conta de Billing:** Na página de Billing, selecione a conta de billing para a qual você deseja criar o orçamento (se você tiver mais de uma).
2.  **Acesse a seção de Orçamentos & Alertas:** No menu de navegação à esquerda da página de Billing, clique em "Orçamentos & Alertas".
3.  **Crie um Novo Orçamento:** Clique no botão "+ CRIAR ORÇAMENTO".

## Passo 3: Configurando o Orçamento

1.  **Nomeie o Orçamento:** Forneça um nome descritivo para o seu orçamento (ex: "Orçamento Desenvolvimento - Janeiro 2024").
2.  **Defina o Escopo:**
    *   **Conta de Billing:** Por padrão, o orçamento se aplica à conta de billing selecionada.
    *   **Projetos:** Se desejar, você pode especificar projetos específicos para incluir no orçamento.  Clique em "Selecionar projetos" e escolha os projetos relevantes.
    *   **Serviços:** Você também pode restringir o orçamento a serviços específicos (ex: Compute Engine, Cloud Storage).  Clique em "Selecionar serviços" e escolha os serviços desejados.
    *   **Outros Filtros:** Você pode adicionar outros filtros como etiquetas (labels), pastas ou créditos.
3.  **Defina o Montante do Orçamento:**
    *   **Especificar montante:**  Escolha se deseja definir um montante fixo para o orçamento ou baseá-lo nos gastos do período anterior.
    *   **Montante Fixo:** Insira o valor do orçamento no campo "Montante do orçamento".  Por exemplo, se você deseja um orçamento de $1000, digite `1000`.
    *   **Gasto do período anterior:** O GCP calculará automaticamente o gasto do período anterior e usará como base para o orçamento atual.  Você pode ajustar esse valor conforme necessário.
4.  **Defina o Período:**
    *   **Mensalmente:** O orçamento é redefinido no início de cada mês.  Esta é a opção mais comum.
    *   **Trimestralmente:** O orçamento é redefinido no início de cada trimestre.
    *   **Anualmente:** O orçamento é redefinido no início de cada ano.
    *   **Personalizado:** Defina um período de tempo específico para o orçamento.
5.  **Configure os Limites de Alerta:**
    *   Adicione regras para receber alertas por e-mail quando seus gastos atingirem determinados percentuais do orçamento.
    *   **Limite Percentual:** Insira uma porcentagem do orçamento (ex: `50`, `80`, `100`, `120`).
    *   **Ações:** Selecione as ações que serão realizadas quando o limite for atingido:
        *   **Enviar alertas por e-mail:**  O GCP enviará um e-mail para os endereços especificados (você pode adicionar vários endereços de e-mail).  É recomendado adicionar seu e-mail e o e-mail do responsável financeiro.
        *   **Publicar uma mensagem no Cloud Pub/Sub:**  Essa opção permite automatizar ações programáticas (ex: desativar VMs, reduzir o uso de recursos) quando o limite for atingido. Requer configuração adicional do Pub/Sub.
6.  **Vincule o Orçamento à Regra do Pub/Sub (Opcional):** Se você configurou alertas Pub/Sub, vincule o orçamento à regra do Pub/Sub para que as notificações sejam enviadas quando os limites forem atingidos.
7.  **Clique em "CRIAR":** Salve o orçamento.

## Passo 4: Gerenciando Orçamentos Existentes

1.  **Acesse a seção de Orçamentos & Alertas:** Novamente, navegue até a seção "Orçamentos & Alertas" na página de Billing.
2.  **Visualize os Orçamentos:** Você verá uma lista de todos os orçamentos configurados para a conta de billing.
3.  **Edite um Orçamento:** Clique no nome do orçamento que deseja editar.  Você pode modificar o nome, escopo, montante, período, limites de alerta e outras configurações.
4.  **Exclua um Orçamento:** Selecione o orçamento que deseja excluir e clique no botão "EXCLUIR".

## Exemplo de Configuração

Suponha que você queira criar um orçamento mensal de $500 para todos os projetos na sua conta de billing e receber alertas quando os gastos atingirem 80%, 100% e 120% do orçamento:

*   **Nome:** "Orçamento Geral - Mensal"
*   **Escopo:** Todos os projetos na conta de billing.
*   **Serviços:** Todos os serviços (deixe em branco para incluir todos).
*   **Montante:** $500 (Montante Fixo).
*   **Período:** Mensalmente.
*   **Alertas:**
    *   80%: Enviar e-mail para `seu-email@example.com` e `financeiro@example.com`.
    *   100%: Enviar e-mail para `seu-email@example.com` e `financeiro@example.com`.
    *   120%: Enviar e-mail para `seu-email@example.com` e `financeiro@example.com`.

## Dicas e Boas Práticas

*   **Monitore seus gastos regularmente:**  Verifique a página de Billing com frequência para acompanhar seus gastos e garantir que você esteja dentro do orçamento.
*   **Use alertas Pub/Sub para automatizar respostas:**  Se você precisar tomar ações automatizadas quando seus gastos atingirem certos limites (ex: desligar instâncias, reduzir a escala de serviços), configure alertas Pub/Sub.
*   **Use etiquetas (labels) para categorizar seus recursos:**  As etiquetas permitem segmentar seus gastos e criar orçamentos mais específicos.
*   **Revise seus orçamentos periodicamente:**  À medida que suas necessidades de negócios mudam, revise seus orçamentos para garantir que eles ainda sejam relevantes e eficazes.
*   **Configure vários orçamentos:**  Você pode criar vários orçamentos para diferentes projetos, serviços ou equipes, permitindo um controle de custos mais granular.
*   **Entenda os custos da GCP:**  Familiarize-se com os modelos de preços da GCP e os fatores que afetam seus gastos.  Isso ajudará você a criar orçamentos mais realistas e evitar surpresas desagradáveis.

## Solução de Problemas

*   **Não estou recebendo alertas:**
    *   Verifique se os endereços de e-mail estão corretos.
    *   Verifique sua pasta de spam.
    *   Certifique-se de que as permissões do Pub/Sub estejam configuradas corretamente (se você estiver usando alertas Pub/Sub).
*   **Meu orçamento não está funcionando como esperado:**
    *   Verifique se o escopo do orçamento está correto (projetos, serviços, etc.).
    *   Certifique-se de que o montante do orçamento esteja correto.
    *   Verifique se o período do orçamento está correto.
*   **Não consigo criar um orçamento:**
    *   Verifique se você tem as permissões necessárias (o papel `billing.budgets.editor` é geralmente necessário).

Seguindo este guia, você poderá configurar orçamentos de billing eficazes na GCP e controlar seus gastos na nuvem.
```

**Observações importantes:**

*   **Pub/Sub:** A integração com Pub/Sub é um tópico avançado e requer configuração adicional. Este README fornece apenas uma visão geral.
*   **Monitoramento Contínuo:** Definir um orçamento é apenas o primeiro passo. O monitoramento regular é crucial para garantir que você esteja dentro do orçamento e tomar medidas corretivas, se necessário.
*   **Personalização:** Adapte os exemplos e dicas às suas necessidades específicas.

Este README deve fornecer um guia completo para configurar orçamentos de billing na GCP. 

Lembre-se de revisar a documentação oficial da GCP para obter informações mais detalhadas e atualizadas.
