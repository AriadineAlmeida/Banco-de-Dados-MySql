# Banco-de-Dados-MySql
ADS Unicesumar ATV Mapa 


create table TIPO_PROD(
id integer not null primary key,
descricao varchar (10) not null
);

create table TIPO_PAGTO(
id integer not null primary key,
descricao varchar(10) not null
);
create table PRODUTOS(
id integer not null primary key,
descricao text,
valor decimal(5,2) unique,
id_tipo_prod integer,
foreign key (id_tipo_prod) references TIPO_PROD (id)
);

create table PEDIDOS(
id integer not null primary key,
data_pedido date,
id_tipo_pagto integer,
valor_total decimal (10,2),
foreign key (id_tipo_pagto) references TIPO_PAGTO (id) 
);

create table PEDIDO_PROD(
id integer not null primary key,
id_pedido integer not null,
id_prod integer,
qtde int not null,
valor_unit decimal(5,2),
valor_total decimal (5,2),
foreign key (id_pedido) references PEDIDOS (id),
foreign key (id_prod) references PRODUTOS (id),
foreign key (valor_unit) references PRODUTOS (valor)
);

select qtde, valor_unit,(qtde*valor_unit) as valor_total from PEDIDO_PROD;

insert into tipo_prod values 
(1, 'consumo'),
(2, 'venda');

insert into tipo_pagto values
(1, 'a vista'),
(2, 'a prazo');

insert into pedidos values
(1, '27/7/2020', 1, '16.00'),
(2, '05/08/2020', 2, '27.00'),
(3, '06/08/2020', 1, '13.50');

insert into produtos values
(1, 'Sabão em Pó 2 KG', '17.00', 1),
(2, 'Coxinha', '5.00', 2),
(3, 'Empadinha', '6.99', 2),
(4, 'Bolo Pedaço', '7.50', 2),
(5, 'Detergente 5 Litros', '8.00', 1),
(6, 'Pastel', '6.00', 2),
(7, 'Pizza Pedaço', '7.00', 2),
(8, 'Suco', '7.01', 2);

insert into pedido_prod values
(1, 1, 2, 2, '5.00', '10.00'),
(2, 1, 6, 1, '6.00', '6.00'),
(3, 2, 3, 3, '6.99', '21.00'),
(4, 2, 6, 1, '6.00', '6.00'),
(5, 3, 4, 1, '7.50', '7.50'),
(6, 3, 6, 1, '6.00', '6.00');

delete from produtos
where id = 1;

delete from pedido_prod;
