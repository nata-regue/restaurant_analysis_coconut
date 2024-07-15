# Restaurant Data Analysis
by. Luz Nataly Reguerin

## General project information

### Objective: 
Analyze sales data to identify opportunities for growth and optimization

### Defining Goals: 

- How many orders were made within a year, month, week, hour.

- Which product gave more profit

- How were revenues by drink classification . 

- Which drink product gave more profit

- Analyze customer orders pattern (determine which drink was asked more with which product)

- Which delivery company got more sales

### Querying the Data: 
Once the goals were defined, querying was done with Python.

### Visualizing the Results: 
Once obtained the results from queries, data was visualized using charts, graphs, and tables. 

### Drawing Insights: 
Finally there were created draw insights from data. These insights can be used to make better business decisions, identify areas for improvement, or create new opportunities.

## LinkedIn Profile
For any queries regarding about this project contact me.

Link : https://www.linkedin.com/in/luz-nataly-reguerin/

### Data Gathering - Queries in SQL
The data that we will use for the analysis was obtained from a real restaurant.

However confidential information was not included in this dataset.  Information in this dataset is from 2016 until 2022. Data 

There were queries performed in SQL to extract data into a csv format.

/*14/5/2024*/
/*Select which values are going to be taken*/

SELECT 
 ped.id_pedido
,sesped.[fecha_sistema]
,ped.[hora]
,prod.clasificador_grupo
,padre.[nombre] as clasificacion      
,prod.[nombre] as producto      
      ,prod.[state]  
	  ,pedprod.[precio]    
	  ,pedprod.[cantidad]   
	  ,pedprod.[precio] * pedprod.[cantidad] AS a_pagar_xprod    
	  ,pagoped.monto AS pago_pedido_tot
      ,pedprod.[observaciones] as product_observations
      ,pagoped.[tipo_forma_pago]
      ,pagoped.[monto]
      ,pagoped.[observacion] AS observaciones_pedido
      ,pagoped.[pagado_cliente]
      ,pagoped.[cambio]
      ,poslug.[descripcion] AS ubicacion
	  ,ped.[numero_pedido]
      ,ped.[fecha_modificacion]
      ,ped.[motivo_modificacion]
      ,ped.[es_anulado]
      ,ped.[es_cortesia]
      ,sesped.[estado]
      ,sesped.[saldo_inicial]
      ,sesped.[saldo_final]
      ,prod.[state] AS stateprod
FROM [coconut_resto_1].[dbo].[pos_pedido] ped
JOIN [pos_sesion_pedido] sesped ON sesped.id_sesion_pedido = ped.id_sesion_pedido  
JOIN pos_pedido_producto pedprod ON pedprod.id_pedido=ped.id_pedido
JOIN pos_producto prod ON prod.id_producto=pedprod.id_producto
LEFT OUTER JOIN pos_producto padre ON prod.id_producto_padre=padre.id_producto
JOIN pos_pago_pedido pagoped ON pagoped.id_pedido=ped.id_pedido
JOIN [pos_lugar_atencion] poslug ON poslug.id_lugar_atencion= ped.[id_lugar_atencion]
JOIN pos_cajero poscaj ON sesped.id_cajero =poscaj.id_cajero
ORDER BY sesped.[fecha_sistema],ped.id_pedido


## Dataset
![img_1.png](imgs%2Fimg_1.png)

Observation:

• The dataset consists of 26 columns:
 - ‘order_id',
- 'system_date',
- 'time', 
- 'group_classifier',
- 'classification', 
- 'product', 
- 'prod_state', 
- 'price', 
- 'quantity',
- 'to_pay_xprod', 
- 'tot_order_payment', 
- 'product_observations',
- 'type_payment_form', 
- 'amount', 
- 'order_observations', 
- 'customer_pay',
- 'change',
- 'location',
- 'order_number',
- 'modification_date',
- 'modification_reason', 
- 'is_cancelled',
- 'is_courtesy', 
- 'status',
- 'start_balance',
- 'end_balance', 
- 'stateprod'

## Data Cleansing
• Reviewing data types

• Convert strings to lower case

• Delete any space before or after any value in the dataset

## Exploratory Data Analysis (EDA)

• Missing values analized

• Outliers annalyzed by numerical and categorical values

• Spelling correction

### Feature Engineering - data preparation

- Unnecessary columns were dropped
- price column required attention
- delivery column
has been organized in delivery name, there was an analysis of all products to determine which were deliveries and which not, and delivery cost was placed in other column.
- anomalies detection. 
There was seen that there are values which dont correspond to products but to inventory. These have to be treated.
For the purpose of this project products corresponding to inventary wont we taken into consideration. So those will be deleted. It is important to highlight that there were 440 rows of ‘envases’, and 37 of ‘aceite’, with payment done of 2950 for aceite, 15283.5 for envases

### Analysis 1: How many orders were made within a year
![1_orderbyyear.jpg](imgs%2F1_orderbyyear.jpg)

Observations :
- The chart shows that on 2019 there were more orders sold. 

### Analysis 2: How many orders were made within a year, month
![2_ordersbyYandM.jpg](imgs%2F2_ordersbyYandM.jpg)

Observation:
- In 2020 may, were the least orders sold, and 2019, may were the highest.
- This is explained because since march 2020 COVID quarantine. 

### Analysis 3: How many orders were made within an hour.
![3_ordersbyH.jpg](imgs%2F3_ordersbyH.jpg)
Observations:
- In these hours there are more orders sold: 12, 13 , 18, 19, 20, 21.

### Analysis 4: Which product gave more profit
![4_top10prods.jpg](imgs%2F4_top10prods.jpg)

Observation :
- The most product sold has been 'alitas 8 unidades', followed by 'alitas 6 unidades' and 'fingers'.

### Analysis 5: How were revenues by drink classification 
![5_soldbybeberage.jpg](imgs%2F5_soldbybeberage.jpg)
Observation:
- Beberages most sold were 'personal' and 'popular'.

### Analysis 6: Which drink product gave more profit
![6_soldbyprodbeberage.jpg](imgs%2F6_soldbyprodbeberage.jpg)
Observation:
- Among those 'coca cola' and 'fanta' were the most sold beberages. 

### Analysis 7: Analyze customer orders pattern (determine which drink was asked more with which product)
![7_foodbeberage.jpg](imgs%2F7_foodbeberage.jpg)
Observation:
- The product most sold was 'alitas miel mostaza' joined by beberage 'coca cola'

### Analysis 8: Which delivery company got more sales
![8_revenuebydelivery.jpg](imgs%2F8_revenuebydelivery.jpg)
Observation:
- Among deliveries the one which sold was 'pedidos ya'. 
