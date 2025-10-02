biblioteca 


create table cliente (
cod_cliente int auto_increment primary key,
email varchar(30),
tel1 char(20),
tel2 char(20),
cep varchar(20),
numero varchar(14),
complemento varchar(70),
endereco varchar(60),
nome varchar(60)
);


create table pessoa_fisica (
    cod_cliente int primary key,
    cpf char (11) not null,
    rg varchar(15),
    foreign key (cod_cliente) references cliente(cod_cliente)
);


create table pessoa_juridica (
    cod_cliente int primary key,
    cnpj char(14) not null,
    ie varchar(20),
    foreign key (cod_cliente) references cliente(cod_cliente)
);


create table pedido (
    cod_pedido int primary key,
    cod_cliente int,
    data date,
    valor decimal(10,2),
    foreign key (cod_cliente) references cliente(cod_cliente)
);


create table editora (
    cod_editora int primary key,
    email varchar(100),
    tel_editora varchar(20),
    contato1 varchar(100),
    contato2 varchar(100)
);


create table livros (
    cod_livro int primary key,
    titulo varchar(200),
    categoria varchar(100),
    isbn char(13) unique,
    ano date,
    valor decimal(10,2),
    editora varchar(100),
    autor varchar(100),
    cod_editora int,
    foreign key (cod_editora) references editora(cod_editora)
);


create table estoque (
    cod_livro int,
    cod_editora int,
    qtd_estoque int,
    primary key (cod_livro, cod_editora),
    foreign key (cod_livro) references livros(cod_livro),
    foreign key (cod_editora) references editora(cod_editora)
);


create table itens_pedido (
    cod_pedido int,
    cod_livro int,
    qtd int,
    primary key (cod_pedido, cod_livro),
    foreign key (cod_pedido) references pedido(cod_pedido),
    foreign key (cod_livro) references livros(cod_livro)
);
