# Como usar GraphQL com Quarkus

Tudo que está nesse projeto pode ser encontrado no repositório [GitHub](https://github.com/luizleite-hotmart/quarkus-graphql).

Para criar o projeto utilizamos o próprio site de bootstrap do quarkus para criar o seu pode acessar [aqui](https://code.quarkus.io/).

## Dependências adicionadas

As dependências que vamos usar podem ser encontradas diretamente pelo bootstrap. São as seguintes:

 - JSON-B  _Utilizada para fazer json bind automático_
 - REST Cliente _Utilizada para criar chamada rest_
 
 Para quem usa maven as dependencias vão ficar assim:
 
 ```xml
     <dependency>
       <groupId>io.quarkus</groupId>
       <artifactId>quarkus-resteasy-jsonb</artifactId>
     </dependency>
     <dependency>
       <groupId>io.quarkus</groupId>
       <artifactId>quarkus-rest-client</artifactId>
     </dependency>
 ```

e em gradle:

```
io.quarkus:quarkus-rest-client
io.quarkus:quarkus-resteasy-jsonb
```

## Background do projeto 
Para facilitar a utilização do projeto vamos usar uma api já pronta que retorna usuários aleatórios, ela pode ser encontrada no site [randomuser.me](https://randomuser.me/)

Para ele vamos utilizar uma chamada no endpoint https://randomuser.me/api/

Quando fazemos um get nesse endpoint recebemos um usuário aleatório no formato de json como o a seguir:

```json
{
  "results": [
    {
      "gender": "male",
      "name": {
        "title": "mr",
        "first": "brad",
        "last": "gibson"
      },
      "location": {
        "street": "9278 new road",
        "city": "kilcoole",
        "state": "waterford",
        "postcode": "93027",
        "coordinates": {
          "latitude": "20.9267",
          "longitude": "-7.9310"
        },
        "timezone": {
          "offset": "-3:30",
          "description": "Newfoundland"
        }
      },
      "email": "brad.gibson@example.com",
      "login": {
        "uuid": "155e77ee-ba6d-486f-95ce-0e0c0fb4b919",
        "username": "silverswan131",
        "password": "firewall",
        "salt": "TQA1Gz7x",
        "md5": "dc523cb313b63dfe5be2140b0c05b3bc",
        "sha1": "7a4aa07d1bedcc6bcf4b7f8856643492c191540d",
        "sha256": "74364e96174afa7d17ee52dd2c9c7a4651fe1254f471a78bda0190135dcd3480"
      },
      "dob": {
        "date": "1993-07-20T09:44:18.674Z",
        "age": 26
      },
      "registered": {
        "date": "2002-05-21T10:59:49.966Z",
        "age": 17
      },
      "phone": "011-962-7516",
      "cell": "081-454-0666",
      "id": {
        "name": "PPS",
        "value": "0390511T"
      },
      "picture": {
        "large": "https://randomuser.me/api/portraits/men/75.jpg",
        "medium": "https://randomuser.me/api/portraits/med/men/75.jpg",
        "thumbnail": "https://randomuser.me/api/portraits/thumb/men/75.jpg"
      },
      "nat": "IE"
    }
  ],
  "info": {
    "seed": "fea8be3e64777240",
    "results": 1,
    "page": 1,
    "version": "1.3"
  }
}
```

