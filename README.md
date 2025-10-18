# Descarga_podcast

# create database if not exists podcast_dib;
# use podcast_dib;

create table usuarios(
id int auto_increment primary key,
nombre varchar(100) not null,
email varchar(150) unique not null
);

create table podcast(
id int auto_increment primary key,
titulo varchar(150) not null,
description text,
autor varchar(100),
fecha_publicacion date 
);

create table descargas(
id int auto_increment primary key,
id_usuario int not null,
id_podcast int not null,
fecha_descarga DATETIME default CURRENT_TIMESTAMP(),
foreign key (id_usuario) references usuarios(id),
foreign key (id_podcast) references podcast(id)
);

insert into usuarios(nombre, email) values
("José Fernadez", "j.fernandez@email.com"),
('Pedro Martínez',"p.martinez@email.com"),
('Luisa Díaz', "l.diaz@email.com");

insert into podcast (titulo,description, autor, fecha_publicacion) values
("El futuro de la IA", "Acerca de la IA", "David Sanchez", "2024-05-12"),
("Viajes y aventuras", "Podcast de viajes por el mundo", "Lucía Gómez","2024-06-01"),
("Historias de código", "Experiencias de desarrolladores", "Carlos Pérez","2024-06-15");

insert into descargas (id_usuario, id_podcast, fecha_descarga) values
(1,1,NOW()),
(2,1,NOW()),
(2,2,NOW()),
(1,3,NOW());

select*from descargas d
join usuarios u on d.id_usuario =u.id 
join podcast p on d.id_podcast =p.id
where u.nombre ="Pedro Martínez";

select d.fecha_descarga , u.nombre , p.titulo from descargas d
join usuarios u on d.id_usuario =u.id 
join podcast p on d.id_podcast =p.id
where u.nombre ="Pedro Martínez";

select p.titulo, COUNT(*) as total_descargas
from descargas d 
join podcast p on d.id =p.id 
group by p.titulo;
