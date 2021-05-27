# SBPay

## Descrição do Projeto

WebService de pagamentos para ser utilizado no <a href="https://github.com/augustobellinaso/bluefood">Projeto Bluefood</a> desenvolvido durante a <a href="https://www.softblue.com.br/site/page/id/FMD_3_Vendas">Formação Master Developer </a> da <a href="https://www.softblue.com.br/">Softblue</a>.

---

<p align="center">
 <a href="#executando-o-projeto">Executando o projeto</a> •
 <a href="#como-utilizar">Como utilizar</a> •
 <a href="#tecnologias">Tecnologias</a> •
 <a href="#deploy">Deploy</a>
</p>

--- 

## Executando o Projeto

### Pré-requisitos

- Ter instalado alguma IDE ([Eclipse](https://www.eclipse.org/), [IntelliJ](https://www.jetbrains.com/pt-br/idea/) ou [Spring Tools Suite](https://spring.io/tools))
  - Observações:
    -  Se utilizar o Eclipse, deve-se ter instalado o plugin Spring Tools 4;
    -  Se utilizar o IntelliJ, é necessário ser a versão Ultimate para ter o suporte ao Java Web

### Fazendo download do código e inserindo na IDE

- Fazer o download do código fonte no formato `.zip` e extrair o mesmo para a pasta de destino.

#### Abrindo o projeto com IntelliJ

- Ir no menu `File > Open` e selecionar a pasta do arquivo descompactado.
- A IDE irá identificar que o projeto possui o gerenciador de dependências `Gradle` e irá solicitar a importação das dependências, basta colocar para importar. Caso aparecer a mensagem `Trust Gradle Project`, clique no botão `Trust Project` para que seja possível editar o projeto.
- Após fazer isso basta esperar alguns momentos até que todas as dependendências sejam carregadas e indexadas ao projeto.
  - Pode ser necessário informar a JDK que a IDE deve usar para executar o projeto. Como o projeto foi desenvolvido com Java na versão 11, selecione qualquer JDK que tenha suporte à essa versão.
- Antes de executar é necessário adicionar no arquivo `application.properties` o seguinte comando: `spring.profiles.active=dev` para que seja identificado que está sendo executado no perfil de desenvolver e ser executado no servidor local.
- Após todas as configurações é possível executar a aplicação clicando na setinha verde que aparece ao lado da declaração da classe dentro do arquivo `SbpayApplication`.  

#### Abrindo o projeto com Eclipse e/ou Spring Tools Suite
- Ir no menu `File > Import > Gradle > Existing Gradle Project`, apertar `Next` e fazer o mesmo na tela de boas vindas do `Gradle`. Na tela seguinte, no campo `Project root directory`, clique em `Browse` e selecione a pasta descompactada do projeto e então clique em `Finish`.
- Aguarde o Eclipse inserir o projeto e as suas dependências e antes de executar o projeto, adicione ao arquivo `application.properties` o seguinte comando: `spring.profiles.active=dev` e depois salve o mesmo.
- Para executar, clique com o botão direito em cima da pasta do projeto no `Package Manager`, vá até `Run As` e selecione `Spring Boot Application`.

---

## Como Utilizar

- O aplicativo é uma API que aceita requisições do tipo `POST` na seguinte URL: `http://localhost:8081/sbpay/pay`.
- As requisições podem ser feitas via qualquer aplicativo para isso, tal como [Postman](https://www.postman.com/) ou [Insomnia](https://insomnia.rest/download), por exemplo.
- Para fazer as requisições é preciso informar dois parâmetros no `Header` da requisição:
  - `Content-Type`: `application/json`
  - `Token`: `r2d2`
    - Caso o token passado não seja esse, será retornada a mensagem de token inválido ao fazer a requisição.]
- A requisição é feita passando o seguinte objeto:

```
{
	"numCartao": "1111222233334444"
}
```
  - Algumas observações sobre a requisição:
    - A requisição retorna o `status code 200` se for passado o token correto, mas a resposta da requisição varia conforme o número do cartão informado:
      - Se o número informado tiver menos (ou mais) de 16 caracteres, retorna a mensagem de cartão inválido;
      - Se tiver 16 caracteres e não começar exatamente com 1111, retorna cartão inválido;
      - Se tiver 16 caracteres e começar com 1111 retorna a mensagem de Autorizado.
      - Essa validação é em função da maneira como o programa foi desenvolvido, e posteriormente outros valores serão inseridos para tornar mais opções válidas.
--- 

## Tecnologias

Ferramentas Utilizadas para construir o projeto:
- [Spring](https://spring.io/)
  - Spring Web
  - Spring Validation
  - Spring DevTools

---

## Deploy

- Aplicação está hospedada no Heroku: https://sbpay-augustobellinaso.herokuapp.com/
- Possível fazer o teste da requisição `POST` com o link da aplicação no Heroku adicionando o `path` `sbpay/pay` ao final do link.


