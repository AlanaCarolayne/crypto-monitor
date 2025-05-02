# 📈 Crypto Monitor

### 📌 Sobre o Projeto

O **Crypto Monitor** é um aplicativo Android desenvolvido em Kotlin que exibe a cotação atual do **Bitcoin**, utilizando dados da API oficial do [Mercado do Bitcoin](https://www.mercadobitcoin.net/api/BTC/ticker/).  
Esse projeto foi desenvolvido durante as aulas do curso **Android Kotlin Developer**, ministrado pelo professor [Ewerton Carreira](https://github.com/carreiras), para colocar em prática os conceitos sobre funcionamento de uma API Rest, retrofit, componentização de layouts e etc.
---

### ⚙️ Funcionalidades

- 📊 Exibição da cotação atual do Bitcoin  
- 🕒 Exibição da data e hora atual  
- 🔄 Atualização manual dos dados por meio do botão "Atualizar"  

---
### 📌 Sobre o Projeto

#### O **Crypto Monitor** é um aplicativo Android desenvolvido em Kotlin que exibe a cotação atual do **Bitcoin**, utilizando dados da API oficial do [Mercado do Bitcoin](https://www.mercadobitcoin.net/api/BTC/ticker/).
#### Esse projeto foi desenvolvido durante as aulas do curso **Android Kotlin Developer**, ministrado pelo professor [Ewerton Carreira](https://github.com/carreiras), para colocar em prática os conceitos sobre funcionamento de uma API Rest, retrofit, componentização de layouts e etc.
---

### ⚙️ Funcionalidades

- 📊 Exibição da cotação atual do Bitcoin
- 🕒 Exibição da data e hora atual
- 🔄 Atualização manual dos dados por meio do botão "Atualizar"

---
### 📸 Telas do projeto
Tela inicial:
![Tela Inicial]()

#### Tela atualizada: A mudança do estado da tela apos o clique no botão "Atualizar".
![Tela Atualizada]()
---

### 🛠 Tecnologias e ferramentas utilizadas

<div align="center">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/androidstudio/androidstudio-original-wordmark.svg" width="90" align="center"/>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/kotlin/kotlin-original-wordmark.svg" width="90" align="center"/>

</div>

---
### 🔌 Como é a comunicação com a API?
A comunicação com a API é feita atraves do Retrofit, que usa o protocolo HTTP para fazer a comucação com o servidor da API, e após obter uma resposta da API do mercado do bitcoin, converte os dados obtidos para um JSON, que é a classe oficial da arquitetura REST.
Nesta aplicação é usado apenas a requisição do tipo GET, ou seja, queremos apenas obter dados.

Quando obtemos os dados da aplicação, usamos a classe TickerResponse para modelar e arquivar as informações na aplicação:
```kotlin
class TickerResponse(
    val ticker: Ticker
)

class Ticker(
    val high: String,
    val low: String,
    val vol: String,
    val last: String,
    val buy: String,
    val sell: String,
    val date: Long
)
```
A comunicação com a API é feita através da create() na classe MercadoBitcoinServiceFactory, que herda de MercadoBitcoinService:
```kotlin
class MercadoBitcoinServiceFactory {
    fun create(): MercadoBitcoinService {
        val retrofit = Retrofit.Builder()
            .baseUrl("https://www.mercadobitcoin.net/")
            .addConverterFactory(GsonConverterFactory.create())
            .build()

        return retrofit.create(MercadoBitcoinService::class.java)
    }
}
```
A interface MercadoBitcoinService define ação que será feita (GET) e o endpoint da API (api/BTC/ticker/), utiliza uma função suspensa do Coroutines indicando que a chamada pode ser pausada/resumida, por fim retorna um objeto Response contendo um TickerResponse.
```kotlin
interface MercadoBitcoinService {
    @GET("api/BTC/ticker/")
    suspend fun getTicker(): Response<TickerResponse>
}
```
---

### 📦 Dependências

Retrofit 2.9.0 e Gson converter: retrofit para fazer comunicação com a API externa  e o Gson, uma biblioteca do Google para converter os dados em JSON
```kotlin
implementation("com.squareup.retrofit2:retrofit:2.9.0")
implementation("com.squareup.retrofit2:converter-gson:2.9.0") 
```
Coroutines 1.5.2: Para fazer as chamadas assíncronas
```kotlin
implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.5.2")
   ```
AppCompact 1.7.0: Para adicionar as toolbars ()
```kotlin
implementation("androidx.appcompat:appcompat:1.7.0")
   ```
### 🔐 Permissões:
Para que o sistema consiga acessar a API para obter a cotação atual, é necessario adicionar a permissão de acesso a internet no arquivo AndroidManifest.xml:
```kotlin
<uses-permission android:name="android.permission.INTERNET" />
```
### 🤝 Contribuição
Contribuições são bem-vindas! Se você tem alguma ideia ou encontrou um bug, sinta-se à vontade para abrir uma issue ou enviar um pull request.
" align="center" alt="Tela inicial">


