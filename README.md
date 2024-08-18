# Projeto: Segmentação de Clientes Baseado no Comportamento

> Esta é a documentação do projeto em grupo da disciplina de **Real Data-Driven Business Project** do **MBA em Data Science & Advanced Analytics** na **Faculdade Impacta Tecnologia**, abaixo terá todos os detalhes do projeto.



## 1. Introdução

* **Objetivo do Projeto:** O objetivo deste projeto é realizar a segmentação de clientes com base em seu comportamento, utilizando uma base de dados que contém informações detalhadas sobre as interações dos clientes com nossos produtos. Através desta segmentação, buscamos identificar grupos distintos de clientes com características e padrões de comportamento semelhantes.

* **Descrição da Base de Dados:** A origem da base de dados se encontra disponível gratuitamente no [Kaggle](https://www.kaggle.com/datasets/sahilprajapati143/retail-analysis-large-dataset/data). É um arquivo .csv (de aproximadamente 85MB) com 30 colunas e 302.010 linhas. As colunas contêm:
	*	ID da transação *(Transaction_ID);*
	*	ID do cliente *(Customer_ID);*
	*	Nome do cliente *(Name);*
	*	Email do cliente *(Email);*
	*	Telefone do cliente *(Phone);*
	*	Endereço do cliente *(Address);*
	*	Cidade do cliente *(City);*
	*	Estado do cliente *(State);*
	*	Zipcode do cliente *(Zipcode);*
	*	Idade do cliente *(Age);*
	*	Gênero do cliente *(Gender);*
	*	Renda do cliente *(Income);*
	*	Segmento do cliente *(Costumer_Segment);*
	*	Data da transação em modelo MM/DD/AAAA *(Date);*
	*	Ano da transação *(Year);*
	*	Mês da transação *(Month);*
	*	Horário da transação em modelo HH:MM:SS *(Time);*
	*	Total de compras *(Total_Purchases);*
	*	Quantidade *(Amount);*
	*	Quantidade total *(Total_Amount);*
	*	Categoria do produto *(Product_Category);*
	*	Marca do produto *(Product_Brand);*
	*	Tipo do produto *(Product_Type);*
	*	Feedback *(Feedback);*
	*	Método de entrega *(Shipping_Method);*
	*	Método de pagamento *(Payment_Method);*
	*	Status do pedido *(Order_Status);*
	*	Nota *(Ratings);*
	*	Produtos *(products);*



## 2. Metodologia

* **Coleta e Pré-processamento dos Dados:** Para analisar os dados de forma devidamente correta foram necessárias algumas ações, como:

	* Importar bibliotecas:
	```
	import warnings
	import numpy as np
	import pandas as pd
	import matplotlib.pyplot as plt
	import seaborn as sns
 	```

	* Identificar possíveis dados nulos:
	```
	base.isnull().sum()
	```

	* Tratar dados nulos:
	```
	> Converter o tipo de dados da coluna Data de object para datetime
	base['Date'] = pd.to_datetime(base['Date'])
	> Conferir o tipo de dado Data após a alteração
	print(base['Date'].dtype)
	> Excluir os valores nulos de Data
	base = base.dropna(subset=['Date'])
	```

* **Ferramentas Utilizadas: TO-DO**
	<!--* Microsoft Power BI;
 	* Python;
  	* -->

* **Métodos de Análise:** Durante o projeto foram utilizadas algumas técnicas de análises, tanto escolhas pessoais como escolhas orientadas pelo professor, estas foram:
 	* Análise Exploratória;
  	* LTV (Lifetime Value);
   	* RFV (Recência, Frequência e Valor).



## 3. Análise e Resultados

* **Análise Exploratória dos Dados (EDA):** Abaixo terão gráficos derivados da análise exploratória do conteúdo da base.
	* Gênero dos clientes do negócio:
 		```
   		plt.figure(figsize=(5, 3))
		base.Gender.value_counts().plot(kind='bar', title='Genero',color = ['#1F77B4', '#FF3333']);
   		```
 		![image](https://github.com/user-attachments/assets/45154e6e-e04b-44fc-9af5-76e520421fbb)

 	* Distribuição do valor total por gênero:
 		```
   		color = ['#FF3333', '#99FF33']
		explode = (0.1, 0)
		
		plt.figure(figsize=(10, 6))
		base.groupby('Gender')['Total_Amount'].sum().plot(kind='pie', autopct='%0.2f%%', colors=color, explode=explode)
		plt.title('Distribuição do VALOR TOTAL por GENERO' , fontweight='bold')
		plt.ylabel('')
		plt.xlabel('')
		plt.show()
   		```
 		![image](https://github.com/user-attachments/assets/42f122ac-2481-4634-8731-19e43c41c882)

  	* Distribuição de idade por gênero:
		```
		plt.figure(figsize=(5, 3))
		sns.violinplot(data=base, x='Age', y='Gender', orient='h', inner='quart')
		plt.title('Distribuição de idade por Genero', fontweight='bold')
		plt.xlabel('Idade')
		plt.ylabel('Genero')
		plt.show()
  		```
  		![image](https://github.com/user-attachments/assets/27fb2d20-5eae-477f-998a-40eab140767a)

  	* Distribuição do valor total por renda:
		```
		color = ['#FF3333', '#99FF33', '#1F77B4']
		explode = (0, 0, 0.1)
		
		plt.figure(figsize=(10, 6))
		base.groupby('Income')['Total_Amount'].sum().plot(kind='pie', autopct='%0.2f%%', colors=color, explode=explode)
		plt.title('Distribuição do VALOR TOTAL por RENDA' , fontweight='bold')
		plt.ylabel('')
		plt.xlabel('')
		plt.show()
  		```
  		![image](https://github.com/user-attachments/assets/2e442458-44e1-403e-a2ef-bf9def00765b)

	* Analíse das variáveis de País:
	  	```
		base.groupby(['Country']).size()
	   	```

	* Distribuição de Clientes por País
 		```
		plt.figure(figsize=(5, 3))
		base['Country'].value_counts().sort_values(ascending=False).plot(kind='bar', color = ['#1F77B4', '#99FF33', '#FF7F0E', '#FF3333', '#FF3333'])
		plt.title('Distribuição de Clientes por País', fontweight='bold')
		plt.xlabel('País')
		plt.ylabel('Frequencia')
		plt.xticks(rotation=45)
		plt.show()
   		```
   		![image](https://github.com/user-attachments/assets/9ae72b4f-ff97-460d-aff2-962ec18a884f)

	* Distribuição do Seguimento de Cliente por país:
	 	```
		color = ['#FF3333', '#FF3333', '#FF7F0E', '#99FF33', '#1F77B4']
		explode = (0, 0, 0, 0.1, 0.1)
		
		plt.figure(figsize=(10, 6))
		base.groupby('Country')['Total_Amount'].sum().plot(kind='pie', autopct='%0.2f%%', colors=color, explode=explode)
		plt.title('Distribuição do Seguimento de Clinete' , fontweight='bold')
		plt.ylabel('')
		plt.xlabel('')
		plt.show()
	  	```
	  	![image](https://github.com/user-attachments/assets/ebdb4a2e-19f9-4144-9e3d-34c4bca9a28c)

	* Analise das variáveis de Seguimento de Cliente:
   		```
		base.groupby(['Customer_Segment']).size()
		```
 		Customer_Segment  
		New         91070  
		Premium     64317  
		Regular    146049  
		dtype: int64

	* Distribuição do Seguimento de Cliente:
 		```
		color = ['#99FF33', '#FF3333', '#1F77B4']
		explode = (0, 0, 0.1)
		
		plt.figure(figsize=(10, 6))
		base.groupby('Customer_Segment')['Total_Amount'].sum().plot(kind='pie', autopct='%0.2f%%', colors=color, explode=explode)
		plt.title('Distribuição do Seguimento de Clinete' , fontweight='bold')
		plt.ylabel('')
		plt.xlabel('')
		plt.show()
   		```
		![image](https://github.com/user-attachments/assets/7b9d5358-7a77-41ca-889c-bae45a7df82e)

   	* Período de Vendas:
		```
   		inicio = pd.to_datetime(base['Date']).dt.date.min()
		fim = pd.to_datetime(base['Date']).dt.date.max()
		print('Período dos dados - De:', inicio, 'Até:',fim)
		```
   		Período dos dados - De: 2023-03-01 Até: 2024-02-29

	* Análise das Variáveis Ano:
		```
		plt.figure(figsize=(5, 3))
		base.Year.value_counts().plot(kind='bar', title='Ano',color = ['#1F77B4', '#FF3333'])
		```
   		![image](https://github.com/user-attachments/assets/d51ac4d7-2f40-4dd1-82fd-51893cb59b61)

	* Análise das Variáveis Mês:
   		```
		base1 = pd.DataFrame(base.groupby(['Month']).size())
		base1
		```
   		![image](https://github.com/user-attachments/assets/d76920f1-ab4c-4661-a052-79ff31af90a3)
		```
  		# Definindo a ordem dos meses
  		month_order = ['March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December', 'January', 'February', ]

		# Convertendo a coluna 'Month' para tipo categórico com a ordem especificada
		base['Month'] = pd.Categorical(base['Month'], categories=month_order, ordered=True)
		
		# Contando os valores e ordenando-os pela ordem dos meses
		month_counts = base['Month'].value_counts().sort_index()
		
		# Plotando o gráfico
		plt.figure(figsize=(5, 3))
		month_counts.plot(kind='bar', color = ['#FF3333', '#1F77B4', '#FF7F0E', '#FF3333', '#99FF33', '#1F77B4', '#FF3333', '#FF3333', '#FF3333', '#FF3333', '#1F77B4'])
		
		plt.title('Distribuição de Compras por Mês', fontweight='bold')
		plt.xlabel('Mês')
		plt.ylabel('Frequência')
		plt.xticks(rotation=45)
		plt.show()
		```
  		![image](https://github.com/user-attachments/assets/7bafb383-ebdc-404e-83c5-38af6174e36f)

	* Análise da variável de Total de Produtos por Transação:
  		```
		base.groupby(['Total_Purchases']).size()
	 	```
		Total_Purchases  
		1.00     31833  
   		2.00     31876  
		3.00     31833  
		4.00     31535  
		5.00     31881  
		6.00     28507  
		7.00     28412  
		8.00     28673  
		9.00     28423  
		10.00    28317  
		dtype: int6
  
		```
  		# Definindo a ordem dos Total_Purchases
		quat_prod = [1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0]

		# Convertendo a coluna 'Total_Purchases' para tipo categórico com a ordem especificada
		base['Total_Purchases'] = pd.Categorical(base['Total_Purchases'], categories=quat_prod, ordered=True)
		
		# Contando os valores e ordenando-os pela ordem de quantidade de produto
		Total_Purchases = base['Total_Purchases'].value_counts().sort_index()
		# Contando os valores e ordenando-os pela ordem quantidade de itens
		prod_counts = base['Total_Purchases'].value_counts().sort_index()
		
		# Plotando o gráfico
		plt.figure(figsize=(5, 3))
		prod_counts.plot(kind='bar', color = ['#1F77B4', '#1F77B4', '#1F77B4', '#99FF33', '#1F77B4', '#FF7F0E', '#FF7F0E', '#FF7F0E', '#FF7F0E', '#FF7F0E', '#FF7F0E'])
		plt.title('Total de Produtos por Transação', fontweight='bold')
		plt.xlabel('Quantidade de Produtos')
		plt.ylabel('Frequência')
		plt.xticks(rotation=45)
		plt.show()
 		```
		![image](https://github.com/user-attachments/assets/acbd03c2-12dd-4eba-bcf2-0ec73b072254)

	* Análise da variável Feedback:
		```
  		plt.figure(figsize=(5, 3))
		base.Feedback.value_counts().plot(kind='bar', title='Avaliações',color = ['#1F77B4', '#99FF33', '#FF7F0E', '#FF3333']);
		```
  		![image](https://github.com/user-attachments/assets/fd7c43e9-0e2b-4490-a0f2-0a54c410ac03)

		```
  		color = ['#FF7F0E', '#FF3333', '#1F77B4', '#99FF33']
		explode = (0, 0, 0.1, 0)
		
		plt.figure(figsize=(10, 6))
		base.groupby('Feedback')['Total_Amount'].sum().plot(kind='pie', autopct='%0.2f%%', colors=color, explode=explode)
		plt.title('FeedBack' , fontweight='bold')
		plt.ylabel('')
		plt.xlabel('')
		plt.show()
		```
  		![image](https://github.com/user-attachments/assets/02f36502-574f-40c3-955c-b2c913406a4b)

   
