> Especialista Digital Analytics: Caio Gomes<br />
> Documento de Especificação Técnica - Casa Dexco

<br />

## Implementação da Camada de dados
Última atualização: 05/08/2025<br />
Em caso de dúvidas, entrar em contato com: [caio.gomes@dex.co](mailto:caio.gomes@dex.co)

<br />

## Índice
- [Objetivo](#objetivo)
- [Overview e Descrições Técnicas](#overview-e-descrições-técnicas)
- [Especificação de Micro-conversões](#especificação-de-micro-conversões)
- [Jornada de Compra](#jornada-de-compra)
- [Especificação de Conversões](#especificação-de-conversões)
- [Considerações Finais](#considerações-finais)

<br />

## Objetivo
Este documento tem como objetivo instruir a implementação do Google Tag Manager, da camada de dados e de data attributes para utilização de recursos de monitoramento do GA4 referentes ao ambiente do site Casa Dexco.

<br />

## Overview e Descrições Técnicas

### Instalação do Google Tag Manager

> Para instalar o Google Tag Manager no seu site, basta seguir os seguintes passos: 

**Dentro do "head"**<br />
Cole esse código o mais alto possível na tag *head* da página:

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-5L5D6KKS');</script>
<!-- End Google Tag Manager -->
```
<br />

**Início do "body"**<br />
Além disso, cole esse código imediatamente após a tag de abertura *body*:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-5L5D6KKS"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```

<br />

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação. Em caso de dúvidas, consultar a documentação técnica do Google sobre [Camada de Dados](https://developers.google.com/tag-platform/tag-manager/datalayer?hl=pt-br)

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer = [{
		'atributo1': '$valor1$',
		'atributo2': '$valor2$'
	}];
</script>
```

OU

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer.push({
		'atributo1': '$valor1$',
		'atributo2': '$valor2$'
	});
</script>
```

### User ID

> Com o recurso User-ID, você pode associar seus próprios identificadores a usuários específicos para conhecer o comportamento deles em diferentes sessões, dispositivos e plataformas.

**Enviar IDs de usuário**
Etapa 1: atualizar a camada de dados:  <br />
Antes de enviar os IDs do usuário para o Google Analytics, disponibilize o user_id na camada de dados do seu site.

```html
	dataLayer.push({
  	  'user_id': 'USER_ID' //atribuir ID único para o usuário no momento de login
	});
```

2. Feito a implementação na Camada de Dados do site, o Web Analytics ficará responsável por configurar essa tag no GTM. Para mais dúvidas, consulte a documentação do Google sobre [User ID](https://developers.google.com/analytics/devguides/collection/ga4/user-id?hl=pt-br&client_type=gtm)


<br />	 	

## Implementação

A documentação foi descrita para algumas áreas especificas do ambiente Casa Dexco.


### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre `$ $` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar 'nao_disponivel'. 

---

<br />

## Especificação de Micro-conversões:


**1 - Menu:**<br />

- **Quando:** Ao clicar em alguma das opções no Menu;
- **Onde:** Menu Principal e Menu da Loja (ícones); "Submenu" é a lista que carrega ao passar o mouse pelo menu principal

```html
dataLayer.push({
		'event': 'menu',
		'menu_principal': '$item-clicado$',
		'menu_loja': '$item-clicado$',
		'submenu': '$item-clicado$'
	});
```
[Imagem Menu Principal](https://duratexsa.sharepoint.com/:i:/r/sites/drivetimenegciosdigitais/Documentos%20Compartilhados/Web%20Analytics/Tagueamento/Imagens%20Tela/Casa%20Dexco%20IMG/menu-principal.png?csf=1&web=1&e=0fltce)
[Imagem Menu Loja](https://duratexsa.sharepoint.com/:i:/r/sites/drivetimenegciosdigitais/Documentos%20Compartilhados/Web%20Analytics/Tagueamento/Imagens%20Tela/Casa%20Dexco%20IMG/menu-loja_icones.png?csf=1&web=1&e=PF766f)


<br />

| Nome 					| Variável 				| Exemplo 													| Descrição 					|
| :-------------------	| :-------------------	| :---------------------									| :------------------------		|
| menu_principal		| $item-clicado$ 		| 'Nossas marcas', 'Pisos e Revestimentos', 'Ofertas' e etc	| Item do Menu Principal 		|
| menu_loja				| $item-clicado$ 		| 'Todos os Chuveiros', 'Bacias e Sanitários' e etc			| Item do menu da loja (ícones)	|
| submenu_loja			| $item-clicado$ 		| 'Sifoes', 'Cubas',										| Item do menu da loja (ícones)	|



<br />

**2 - Banners:**<br />

- **Quando:** Ao clicar em algum banner da Home;
- **Onde:** Banners principais;

```html
dataLayer.push({
		'event': 'banner',
		'banner': '$nome-banner$'
	});
```

[Imagem Banners](https://duratexsa.sharepoint.com/:i:/r/sites/drivetimenegciosdigitais/Documentos%20Compartilhados/Web%20Analytics/Tagueamento/Imagens%20Tela/Casa%20Dexco%20IMG/banner-principal-01.png?csf=1&web=1&e=fNhZzW)

<br />

| Nome 			| Variável 				| Exemplo 							| Descrição 				|
| :------------	| :-------------------	| :---------------------			| :------------------------	|
| banner		| $nome-banner$ 		| 'Junta Seca', '5% off Pix' e etc	| Nome do banner clicado	|


<br />

**3 - Produtos Mais vendidos - Destaques:**<br />

- **Quando:** Ao clicar em "Ver Detalhes", em um produto Destaque;
- **Onde:** Produtos mais vendidos;

```html
dataLayer.push({
		'event': 'destaques',
		'ver-detalhes': '$nome-produto$'
	});
```

[Imagem Destaques](https://duratexsa.sharepoint.com/:i:/r/sites/drivetimenegciosdigitais/Documentos%20Compartilhados/Web%20Analytics/Tagueamento/Imagens%20Tela/Casa%20Dexco%20IMG/destaques-01.png?csf=1&web=1&e=h2Gfi5)

<br />

| Nome 			| Variável 				| Exemplo 							| Descrição 				|	
| :------------	| :-------------------	| :---------------------			| :------------------------	|
| banner		| $nome-banner$ 		| 'Junta Seca', '5% off Pix' e etc	| Nome do banner clicado	|

<br />

**4 - Navegue por Ambiente:**<br />

- **Quando:** Ao clicar em um ambiente para navegação na loja;
- **Onde:** Ambientes;

```html
dataLayer.push({
		'event': 'ambientes',
		'ambientes': '$nome-ambiente$'
	});
```

[Imagem Ambientes](https://duratexsa.sharepoint.com/:i:/r/sites/drivetimenegciosdigitais/Documentos%20Compartilhados/Web%20Analytics/Tagueamento/Imagens%20Tela/Casa%20Dexco%20IMG/novo-ambiente-01.png?csf=1&web=1&e=bWGDqT)

<br />

| Nome 			| Variável 				| Exemplo 						| Descrição 				|	
| :------------	| :-------------------	| :---------------------		| :------------------------	|
| ambientes		| $nome-ambientes$ 		| 'Cozinha', 'Banheiro' e etc	| Nome do ambiente clicado	|

<br />

**5 - Compre por Cor:**<br />

- **Quando:** Ao clicar no módulo "Compre por Cor";
- **Onde:** Compre por Cor;

```html
dataLayer.push({
		'event': 'tipo-cor',
		'tipo-cor': '$tipo-cor$'
	});
```

[Imagem Compre por Cor](https://duratexsa.sharepoint.com/:i:/r/sites/drivetimenegciosdigitais/Documentos%20Compartilhados/Web%20Analytics/Tagueamento/Imagens%20Tela/Casa%20Dexco%20IMG/compre-por-cor-01.png?csf=1&web=1&e=A7DC37)

<br />

| Nome 			| Variável 			| Exemplo 					| Descrição 				|	
| :------------	| :----------------	| :---------------------	| :------------------------	|
| tipo-cor		| $tipo-cor$ 		| 'Branco', 'Cromado' e etc	| Nome da Cor selecionada	|

<br />

**6 - Marcas Favoritas:**<br />

- **Quando:** Ao selecionar uma marca, no módulo de "Marcas Favoritas";
- **Onde:** Marcas Favoritas;

```html
dataLayer.push({
		'event': 'marcas-favoritas',
		'marcas-favoritas': '$nome-marca$'
	});
```

[Imagem Marcas Favoritas](https://duratexsa.sharepoint.com/:i:/r/sites/drivetimenegciosdigitais/Documentos%20Compartilhados/Web%20Analytics/Tagueamento/Imagens%20Tela/Casa%20Dexco%20IMG/favoritos-01.png?csf=1&web=1&e=JdHJpV)

<br />

| Nome 				| Variável 				| Exemplo 					| Descrição 				|	
| :------------		| :-------------------	| :---------------------	| :------------------------	|
| marcas-favoritas	| $marcas-favoritas$ 	| 'Deca', 'Portinari' e etc	| Nome do Marca escolhida	|

<br />

---

## Jornada de Compra:

<br />

### Lista de Produtos:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento de uma página de lista de produtos.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "view_item_list",
  ecommerce: {
    item_list_id: "related_products",
    item_list_name: "Related products",
    items: [
     {
      	item_id: "SKU_12345",
      	item_name: "Misturador Monocomando de Cozinha Deca",
      	affiliation: "Deca",
      	coupon: "DESCONTO 10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Torneiras",
      	item_category2: "Misturador",
       	item_category3: "Monocomando",
      	item_list_id: "123456",
      	item_list_name: "Misturador Monocomando",
      	item_variant: "cromado",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc123",
      	price: 199.99,
      	quantity: 1
    },
    {
      item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 1,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }]
  }
});</script>
```

<br />

| Nome 					| Variável 					| Exemplo 				| Descrição 							|	
| :-------------------	| :-------------------		| :---------------------| :-----------------------------------  |
| item_name 			| $nome-produto$ 			| 'Cuba de Apoio' 		| Nome do produto 						|
| item_id				| $id-produto$ 				| 'SKU_45678'			| ID do produto 						|
| price					| $preco-produto$ 			| '299.99' 				| Preço do produto						|
| item_brand 			| $marca-produto$ 			| 'Deca'				| Marca do produto 	 					|
| item_category			| $categoria-produto$ 		| 'Cuba'				| Categoria do produto 					|
| item_variant 			| $variacao-produto$ 		| 'branco'				| Variação do produto (tamanho - cor)	|
| item_list_name 		| $lista-produto$ 			| 'Cuba de Apoio'		| Nome da lista de produtos 			|



<br />

### Select Item (Product click):

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no clique em algum produto.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "select_item",
  ecommerce: {
    item_list_id: "related_products",
    item_list_name: "Related products",
    items: [
    {
       	item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});</script>
```

<br />

| Nome 				| Variável 				| Exemplo 			| Descrição 							|
| :--------------	| :-------------------	| :---------------- | :----------------------------	 	 	|
| item_name 		| $nome-produto$ 		| 'Cuba de Apoio' 	| Nome do produto 						|
| item_id			| $id-produto$ 			| 'SKU_45678'		| ID do produto 						|
| price				| $preco-produto$ 		| '299.99' 			| Preço do produto						|
| item_brand 		| $marca-produto$ 		| 'Deca'			| Marca do produto 	 					|
| item_category		| $categoria-produto$ 	| 'Cuba'			| Categoria do produto 					|
| item_variant 		| $variacao-produto$ 	| 'branco'			| Variação do produto (tamanho - cor)	|
| item_list_name 	| $lista-produto$ 		| 'Cuba de Apoio'	| Nome da lista de produtos 			|

<br />

### View Item (Product Detail):

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento da página de um produto.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "view_item",
  ecommerce: {
    currency: "BRL",
    value: 299.99,
    items: [
    {
      	item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});</script>
```

<br />

| Nome 				| Variável 				| Exemplo 			| Descrição 							|
| :---------------	| :-------------------	| :--------------	| :------------------------------  		|
| item_name 		| $nome-produto$ 		| 'Cuba de Apoio' 	| Nome do produto 						|
| item_id			| $id-produto$ 			| 'SKU_45678'		| ID do produto 						|
| price				| $preco-produto$ 		| '299.99' 			| Preço do produto						|
| item_brand 		| $marca-produto$ 		| 'Deca'			| Marca do produto 	 					|
| item_category		| $categoria-produto$ 	| 'Cuba'			| Categoria do produto 					|
| item_variant 		| $variacao-produto$ 	| 'branco'			| Variação do produto (tamanho - cor)	|
| item_list_name 	| $lista-produto$ 		| 'Cuba de Apoio'	| Nome da lista de produtos 			|
<br />

### AddToCart:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no clique do CTA de adição de produto ao carrinho.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "add_to_cart",
  ecommerce: {
    currency: "BRL",
    value: 299.99,
    items: [
    {
      	item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
		in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});
</script>
```

<br />

| Nome 				| Variável 				| Exemplo 			| Descrição 							|
| :---------------	| :-------------------	| :-----------------| :--------------------------  			|
| item_name 		| $nome-produto$ 		| 'Cuba de Apoio' 	| Nome do produto 						|
| item_id			| $id-produto$ 			| 'SKU_45678'		| ID do produto 						|
| price				| $preco-produto$ 		| '299.99' 			| Preço do produto						|
| item_brand 		| $marca-produto$ 		| 'Deca'			| Marca do produto 	 					|
| item_category		| $categoria-produto$ 	| 'Cuba'			| Categoria do produto 					|
| item_variant 		| $variacao-produto$ 	| 'branco'			| Variação do produto (tamanho - cor)	|
| item_list_name 	| $lista-produto$ 		| 'Cuba de Apoio'	| Nome da lista de produtos 			|

<br />

### Remove From Cart:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no clique do botão para remover um produto do carrinho.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "remove_from_cart",
  ecommerce: {
    currency: "BRL",
    value: 7.77,
    items: [
    {
      item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});
</script>
```

<br />

| Nome 				| Variável 				| Exemplo 			| Descrição 							|
| :----------------	| :-------------------	| :---------------	| :--------------------------------  	|
| item_name 		| $nome-produto$ 		| 'Cuba de Apoio' 	| Nome do produto 						|
| item_id			| $id-produto$ 			| 'SKU_45678'		| ID do produto 						|
| price				| $preco-produto$ 		| '299.99' 			| Preço do produto						|
| item_brand 		| $marca-produto$ 		| 'Deca'			| Marca do produto 	 					|
| item_category		| $categoria-produto$ 	| 'Cuba'			| Categoria do produto 					|
| item_variant 		| $variacao-produto$ 	| 'branco'			| Variação do produto (tamanho - cor)	|
| item_list_name 	| $lista-produto$ 		| 'Cuba de Apoio'	| Nome da lista de produtos 			|

<br />

### Adicionar à lista de desejos

- **Onde** O objeto javascript (dataLayer) abaixo deve ser disparado quando o usuário/cliente clicar em "adicionar produto à lista de desejo" ou "favoritar" o produto.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "add_to_wishlist",
  ecommerce: {
    currency: "BRL",
    value: 7.77,
    items: [
    {
      item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});
</script>
```

<br />

### View Cart

- **Onde** O objeto javascript (dataLayer) abaixo deve ser disparado após o usuário/cliente clicar em "ir para o meu carrinho", e carregar a tela "Meu Carrinho". 

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "view_cart",
  ecommerce: {
    currency: "BRL",
    value: 7.77,
    items: [
    {
     item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});
</script>
```

<br />

<br />

### Promotion Impression:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez na visualização de um banner.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "view_promotion",
  ecommerce: {
    creative_name: "Banner 35% Off",
    creative_slot: "outlet",
    promotion_id: "P_12345",
    promotion_name: "Outlet Inverno",
    items: [
    {
      item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
       	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});</script>
```

<br />

### Promotion Click:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado o usuário clicar em um banner.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "select_promotion",
  ecommerce: {
    creative_name: "Banner 35% Off",
    creative_slot: "outlet",
    promotion_id: "P_12345",
    promotion_name: "Outlet Inverno",
    items: [
    {
      	item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});
</script>
```

<br />

---

### Especificação de Conversões:

**Sucesso Compra:**<br />

- **Onde:** No callback de sucesso;

```html
<script>
	dataLayer.push({
		'event': 'conversion',
	});
</script>
```

<br />

### Checkout:

>Meça a primeira etapa do processo de finalização da compra enviando um evento begin_checkout e definindo os campos relevantes para um ou mais itens: Nessa etapa, um cupom pode ser incluído no pedido inteiro ao ser adicionado ao evento. Ele também pode ser aplicado a um determinado item por inclusão em elementos específicos na matriz de items. Para detalhes sobre os parâmetros disponíveis, consulte a Referência de eventos.

****<br />

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no clique em finalizar compra, no carrinho, dando assim início ao processo de checkout.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "begin_checkout",
  ecommerce: {
    currency: "BRL",
    value: 299.99,
    coupon: "Frete10",
    items: [
    {
        item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});
</script>
```

<br />

| Nome 				| Variável 				| Exemplo 			| Descrição 							|
| :----------------	| :-------------------	| :-----------------| :-----------------------------		|
| item_name 		| $nome-produto$ 		| 'Cuba de Apoio' 	| Nome do produto 						|
| item_id			| $id-produto$ 			| 'SKU_45678'		| ID do produto 						|
| price				| $preco-produto$ 		| '299.99' 			| Preço do produto						|
| item_brand 		| $marca-produto$ 		| 'Deca'			| Marca do produto 	 					|
| item_category		| $categoria-produto$ 	| 'Cuba'			| Categoria do produto 					|
| item_variant 		| $variacao-produto$ 	| 'branco'			| Variação do produto (tamanho - cor)	|
| item_list_name 	| $lista-produto$ 		| 'Cuba de Apoio'	| Nome da lista de produtos 			|


<br />

### Shippping Info:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento da página de transação, e se o usuário acessar novamente o link ou atualizar a página, o objeto não deve ser disparado novamente.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "add_shipping_info",
  ecommerce: {
    currency: "BRL",
    value: 10.00,
    coupon: "Frete10",
    shipping_tier: "Sedex10",
    items: [
    {
      	item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
       	item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});

</script>
```
*Descrição :*

<br />

### Add Payment Info:

- **Onde:** o evento add_payment_info deve disparar quando um usuário enviar as informações de pagamento. Se aplicável, inclua payment_type nesse evento para a forma de pagamento selecionada.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "add_payment_info",
  ecommerce: {
    currency: "BRL",
    value: 299.99,
    coupon: "Frete10",
    payment_type: "Credit Card",
    items: [
    {
      	item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
   	    item_brand: "Deca",
       	item_category: "Cuba",
      	item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
      	in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});

</script>
```
*Descrição:*

<br />

### Purchase:

- **Onde:** O objeto javascript (dataLayer) abaixo deve ser disparado uma única vez no carregamento da página de transação, e se o usuário acessar novamente o link ou atualizar a página, o objeto não deve ser disparado novamente.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "purchase",
  ecommerce: {
      transaction_id: "1501233123145-0123", //usar a mesma da VTEX
      value: 295.09,
      tax: 4.90,
      shipping: 0.00,
      currency: "BRL",
      coupon: "Frete10",
      items: [
       {
        item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
        item_brand: "Deca",
     	item_category: "Cuba",
  	    item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
	    in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
      }
]
   });
</script>
```

<br />

*Descrição Produtos:*

| Nome 				| Variável 				| Exemplo 			| Descrição 							|
| :---------------	| :-----------------	| :---------------- | :-----------------------------	  	|
| item_name 		| $nome-produto$ 		| 'Cuba de Apoio' 	| Nome do produto 						|
| item_id			| $id-produto$ 			| 'SKU_45678'		| ID do produto 						|
| price				| $preco-produto$ 		| '299.99' 			| Preço do produto						|
| item_brand 		| $marca-produto$ 		| 'Deca'			| Marca do produto 	 					|
| item_category		| $categoria-produto$ 	| 'Cuba'			| Categoria do produto 					|
| item_variant 		| $variacao-produto$ 	| 'branco'			| Variação do produto (tamanho - cor)	|
| item_list_name 	| $lista-produto$ 		| 'Cuba de Apoio'	| Nome da lista de produtos 			|

<br />

### Reembolso (refund):

- **Onde:** Meça os reembolsos enviando um evento refund com o transaction_id relevante especificado e um ou mais itens definidos com item_id e quantity. Recomendamos incluir informações do item no evento refund para consultar as métricas de reembolso no Google Analytics.

```html
<script>
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "refund",
  ecommerce: {
    currency: "BRL",
    transaction_id: "1501233123145-0123", //usar a mesma da VTEX
    value: 295.09,
    coupon: "Frete10",
    shipping: 0.00,
    tax: 4.90,
    items: [
    {
      	item_id: "SKU_45678",
      	item_name: "Cuba de Apoio Quadrada Deca",
      	affiliation: "Deca",
      	coupon: "Frete10",
      	discount: 10.00,
      	index: 0,
   	    item_brand: "Deca",
       	item_category: "Cuba",
  	    item_category2: "Apoio",
      	item_list_id: "98765",
      	item_list_name: "Cuba de Apoio",
      	item_variant: "branco",
	    in_stock: true, //caso o produto esteja indisponível, colocar como false
      	location_id: "abc12345",
      	price: 299.99,
      	quantity: 1
    }
    ]
  }
});
</script>
```
---

<br />


### Considerações finais: 

>Em caso de dúvidas, podem consultar a documentação técnica oficial do Google: Link(https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?hl=pt-br&client_type=gtm)
