![Certificate Screenshot](https://raw.githubusercontent.com/Thiago-Protasio/generateCertificate/master/readmeImage.jpg)

# Certificate Generator

Essa é uma aplicação serverless responsável por gerar o certificado de um aluno e também de valida-lo.
- [Gerar certificado](#gerar-certificado)
- [Validar certificado](#validar-certificado)
### Gerar certificado

Para criar um certificado a aplicação deve receber as seguintes propriedades:

| Parâmetro   | Tipo       | Descrição                           |
| :---------- | :--------- | :---------------------------------- |
| `id` | `string` | O `id` do usuário |
| `name` | `string` | O nome do aluno |
| `grade` | `string` | A nota do aluno |

Todas as propriedades devem ser passadas no **corpo** da requisição. Como no exemplo abaixo:

```typescript
{
	"id": "bf2bfc02-059c-48ee-9995-bc830cce73aa", // id do usuário
	"name": "Thiago Protasio", // Nome do aluno 
	"grade": "10.00" // Nota do aluno
}
```

A rota para se criar um certificado é:

```https
  POST /generateCertificate
```


#### Retorno
Retorna um objeto com as seguintes informações: `201`

```typescript
{
	message: "Certificado criado com sucesso!",
	url: "(link).pdf" // Link para acessar o certificado criado, em formato pdf
}
```

### Validar Certificado 

Para validar um certificado o `id` do usuário deve ser recebido na rota (path) da requisição.

```https
  GET /verifyCertificate/{user_id}
```

#### Retorno

Caso o certificado seja válido a resposta será: `200`

```typescript
{
	"message": "Certificado válido!",
	"name": "Thiago Protasio", // Nome do aluno
	"url": "(link).pdf" // Link para o certificado em formato pdf
}
```

Caso o certificado não seja válido a resposta será: `400`

```typescript
{
	"message": "Certificado inválido!"
}
```
