# Propuesta TP DSW

## Grupo

### Integrantes
- 51742 - Quaglia, Mateo

### Repositorios
- [Frontend](https://github.com/Enderking81/frontendDiscoverIt)
- [Backend](https://github.com/Enderking81/backendDiscoverIt)

## Tema

### Descripción
DiscoverIt es una plataforma para descubrir lugares de Rosario: restaurantes, museos, bares, parques y más. Cualquier visitante puede explorar los lugares, filtrarlos por categoría, buscarlos por nombre o dirección y verlos en un mapa. Los usuarios registrados recomiendan lugares con un puntaje de 1 a 5 y una opinión, y con esas recomendaciones se calcula el rating de cada lugar. También pueden guardar lugares en favoritos. Un administrador gestiona las categorías y los lugares publicados.

### Modelo

```mermaid
classDiagram
    direction LR

    class User {
        id
        nickname
        email
        password (hash)
        isAdmin
    }
    class Profile {
        id
        bio
        avatar
        location
        birthdate
    }
    class Category {
        id
        name
        description
    }
    class PlaceProduct {
        id
        name
        description
        location
        image
        averageRating
        latitude
        longitude
    }
    class Recommendation {
        id
        points (1 a 5)
        description
        createdAt
    }

    User "1" -- "1" Profile : tiene
    Category "1" -- "0..*" PlaceProduct : clasifica
    User "1" -- "0..*" Recommendation : escribe
    PlaceProduct "1" -- "0..*" Recommendation : recibe
    User "0..*" -- "0..*" PlaceProduct : favoritos
```

## Alcance Funcional

### Alcance Mínimo

Regularidad:
|Req|Detalle|
|:-|:-|
|CRUD simple|1. CRUD Category|
|CRUD dependiente|1. CRUD PlaceProduct {depende de} CRUD Category|
|Listado<br>+<br>detalle|1. Listado de lugares filtrado por categoría y por texto (nombre o dirección) => detalle con descripción, ubicación en el mapa, rating promedio y recomendaciones|
|CUU/Epic|1. Recomendar un lugar|

Adicionales para Aprobación:
|Req|Detalle|
|:-|:-|
|CRUD|1. CRUD Category<br>2. CRUD PlaceProduct<br>3. CRUD User (registro, perfil, edición y baja de la cuenta)<br>4. CRUD Profile<br>5. CRUD Recommendation {depende de} CRUD User y CRUD PlaceProduct|
|CUU/Epic|1. Publicar un lugar (administrador)<br>2. Recomendar un lugar (usuario)<br>Están relacionados: el lugar que publica el administrador es lo que el usuario recomienda, y cada recomendación recalcula el rating del lugar.|

### Alcance Adicional Voluntario

|Req|Detalle|
|:-|:-|
|Listados|1. Mis favoritos<br>2. Panel de administración con estadísticas del sistema|
|CUU/Epic|1. Guardar un lugar en favoritos|
|Otros|1. Mapa interactivo de los lugares<br>2. Moderación: el administrador puede eliminar cualquier recomendación<br>3. Modo oscuro|

## Niveles de acceso

|Nivel|Puede|
|:-|:-|
|Invitado|Explorar, filtrar y ver el detalle de los lugares|
|Usuario|Lo anterior, más recomendar lugares, editar o borrar sus recomendaciones, gestionar favoritos y su perfil|
|Administrador|Lo anterior, más gestionar categorías y lugares, ver estadísticas y moderar recomendaciones|
