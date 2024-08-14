# Projeto: Segmentação de clientes baseado no comportamento

Esta é a documentação do projeto de segmentação de clientes, abaixo terá todos os detalhes do projeto.

## 1. Introdução

* Objetivo do Projeto: O objetivo deste projeto é realizar a segmentação de clientes com base em seu comportamento, utilizando uma base de dados que contém informações detalhadas sobre as interações dos clientes com nossos produtos. Através desta segmentação, buscamos identificar grupos distintos de clientes com características e padrões de comportamento semelhantes.

*	Descrição da Base de Dados: A origem da base de dados se encontra disponível gratuitamente no [Kaggle](https://www.kaggle.com/datasets/sahilprajapati143/retail-analysis-large-dataset/data). É um arquivo .csv (de aproximadamente 85MB) com 30 colunas e 302.010 linhas. As colunas contêm:
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

* Coleta e Pré-processamento dos Dados: Para analisar os dados de forma devidamente correta foi necessário tratar os dados em que continham campos nulos, assim tendo que:

Converter o tipo de dados da coluna Data de object para datetime
```
base['Date'] = pd.to_datetime(base['Date'])
```
Conferir o tipo de dado Data após a alteração
```
print(base['Date'].dtype)
```
Excluir os valores nulos de Data
```
base = base.dropna(subset=['Date'])
```
