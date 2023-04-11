# **Desafio Alura Power B.I I**

### 🔥 **O Desafio**

O desafio consiste em desenvolver um dashboard utilizando o power B.I, considerando as bases de dados disponibilizadas pela alura e aplicar os conhecimentos de elaboração de dashboards, fórmulas DAX, relação entre tabelas e criação de medidas. O Desafio é divido em 4 Semanas:

Semana 01: Desafio de logística - Alura Log  ✅

Semana 02: Desafio de marketing - Alura Shop ⌛

Semana 03 e 04: Desafio financeiro - Alura Store ⌛

### 🚀 Semana 01: Desafio de logística - Alura Log

### **O Problema**

A pessoa que gerencia a área de logística da Alura Log, está enfrentando algumas mudanças em sua área por conta do aumento da demanda dos serviços de logística no período da pandemia. Ela quer manter a qualidade de seu serviço, mas para isso precisa acompanhar constantemente as métricas do seu departamento para tomar as melhores decisões. Quando nos contou isso, analisamos que para auxiliar nesse desafio precisaremos fazer um dashboard para logística. Para isso, vamos visualizar algumas métricas muito importantes para a área.

***O Dashboard***

![Untitled](https://user-images.githubusercontent.com/123482943/231204531-28ec8e2d-c145-4e97-9ed4-6c34220d2bb9.png)

![Untitled2](https://user-images.githubusercontent.com/123482943/231204664-2265ffa4-b802-4fb0-a6cf-9723d6a9ba3b.png)

Link para acesso: https://app.powerbi.com/view?r=eyJrIjoiYjEwMTEzNTgtZGZkNC00ZGFhLWJlZmMtNzMyNjBmNzU0NGRhIiwidCI6IjFmOWVjYWZlLWFiM2YtNDBhNS05ODc5LWJjZTRkYTdhMjU5NyJ9



💾 ***Carregamento e Transformação dos Dados***

Como início do projeto as bases da dados em csv foram importadas para o  Power B.I, realizando os devidos ajustes nas bases considerando o formato correto dos dados de data, localidade, números e valores, assim como definindo as relações entre as tabelas. As tabelas foram vinculadas considerando as colunas de “ID do Produto” e “ID do Veículo”.

![Untitled3](https://user-images.githubusercontent.com/123482943/231205136-8d9d7d4d-a656-4175-ac97-a74e33dd99c2.png) ![Untitled4](https://user-images.githubusercontent.com/123482943/231205192-f7cabc3b-8205-4f19-a8f0-9285a1a626d7.png)

📐 ***Tabela de Medidas*** 

| Medida | Fórmula DAX |
| --- | --- |
| Faturamento | Faturamento = SUMX('Tabela - Pedidos',[Total Produtos Vendidos] * RELATED('Tabela - Produtos'[preço])) |
| Faturamento Acumulado | Faturamento Acumulado = CALCULATE([Faturamento], filter(ALL('Tabela - Pedidos'), 'Tabela - Pedidos'[Data da compra] <=MAX('Tabela - Pedidos'[Data da compra]))) |
| Nível de Serviço Acordado | Nível de Serviço Acordado = divide([Pedidos Entregues no Prazo],[Total de Pedidos]) |
| Pareto | Pareto = VAR FaturamentoTotal = CALCULATE([Faturamento],ALLSELECTED('Tabela - Pedidos')) VAR TotalAtual = [Faturamento] Var tbResumo = SUMMARIZE(ALLSELECTED('Tabela - Pedidos'),'Tabela - Produtos'[Descrição Produto],"Total",[Faturamento])Var TotalAcumulado = SUMX(FILTER(tbResumo, [Total] >= TotalAtual),[Total]) Return TotalAcumulado/FaturamentoTotal |
| Pedidos Atrasados | Pedidos Atrasados = calculate(count('Tabela - Pedidos'[Status do pedido]),filter('Tabela - Pedidos', 'Tabela - Pedidos'[Status Entrega] = "Entrega Atrasada")) |
| Pedidos Entregues no Prazo | Pedidos Entregues no Prazo = calculate(count('Tabela - Pedidos'[Status do pedido]),filter('Tabela - Pedidos', 'Tabela - Pedidos'[Status Entrega] = "Entrega no Prazo")) |
| Rank da Categoria | Rank da Categoria = RANKX(ALLSELECTED('Tabela - Produtos'),[Faturamento]) |
| Total de Pedidos | Total de Pedidos = count('Tabela - Pedidos'[ID Pedido]) |
| Total de Produtos Vendidos | Total Produtos Vendidos = SUM('Tabela - Pedidos'[Quantidade]) |
| Status da Entrega | Status Entrega = if(and('Tabela - Pedidos'[Data previsão]>'Tabela - Pedidos'[Data de entrega],'Tabela - Pedidos'[Status do pedido]="Entregue"),"Entrega no Prazo","Entrega Atrasada") |
| Ship to Date | S2D = DATEDIFF('Tabela - Pedidos'[Data da compra],'Tabela - Pedidos'[Data de entrega],DAY) |

🧑‍💼 ***Visualizações e Insights de Negócio***

🚚 **Acompanhamento das Entregas**

No primeiro dashboard construído o objetivo é apresentar dados conectados que apoiem a gestão em tempo real para a tomada de decisão a respeito do acompanhamento das entregas. Para isso, alguns indicadores são apresentados:

- Veículos disponíveis - apresenta o número de veículos que não estão sendo utilizados
- Total de Pedidos - apresenta o número total de pedidos no período
- Pedidos atrasados - apresenta o número total de pedidos atrasados
- Pedidos entregues no prazo - pedidos entregue dentro do prazo
- Nível de Serviço Acordado - Apresenta o percentual de pedidos que foram entregues dentro do prazo em relação ao número total de pedidos
- Média S2D - Tempo médio entre o pedido realizado pelo cliente e a entrega do pedido

![Untitled5](https://user-images.githubusercontent.com/123482943/231206822-63580c3b-5d93-4f71-9cc4-5f8d235728ef.png)     ![Untitled6](https://user-images.githubusercontent.com/123482943/231206847-93ebba0d-9bd0-438a-a4b8-f2fe284f770f.png)


A partir desse dashboard e os indicadores citados os gestores podem, de forma sistemática:

1. Criar sistemática de acompanhamento dos pedidos
2. Avaliar cumprimento do SLA e ajustar processos conforme necessário
3. Identificar pedidos que estão atrasados
4. Identificar disponibilidade de veículos e estimar limite de pedidos versus prazo de entrega

💰 **Acompanhamento Financeiro**

No Dashboard “Financeiro” é possível realizar a análise financeira dos dados no tempo considerando os dados apresentados:

- Faturamento - apresenta o faturamento no período selecionado
- Total de Produtos vendidos - apresenta o total de produtos vendidos
- Gráfico ABC (Pareto) dos produtos vendidos - apresenta os produtos com maior representatividade de venda
- Faturamento Acumulado por Mês e Ano - apresenta o faturamento acumulado no período


![Untitled8](https://user-images.githubusercontent.com/123482943/231207139-ec9a749c-a4fb-48a5-8deb-8e18404f5689.png)       ![Untitled7](https://user-images.githubusercontent.com/123482943/231207115-3116e4f2-4c14-438b-a32d-17160a1537ca.png)

A partir disso é possível identificar em nível de gestão, para a tomada de decisão

1. Crescimento do faturamento no período
2. Produtos mais vendidos - Análise da Curva ABC
3. Definir estratégia de vendas e posicionamento de produto
