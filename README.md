# shinyforms - Easily create questionnaire-type forms with Shiny 

#### Versão em português do shinyforms.

Só traduzi o arquivo para o ppt-br. Você devia olhar o pacote original do DEAN ATTALI [https://github.com/daattali/shinyforms](https://github.com/daattali/shinyforms)


```
# install.packages("devtools")
devtools::install_github("DATAUNIRIO/shinyforms")
```


```
library(shiny)
library(shinyforms)

questions <- list(
  list(id = "nome", type = "text", title = "Qual o seu nome?", mandatory = TRUE),
  list(id = "idade", type = "numeric", title = "Qual a sua idade?"),
  list(id = "curso", type = "text", title = "Qual é seu curso (Administração, Ciência Política, Biblioteconomia, Engenharia de  Produção, etc)?"),
  list(id = "terms", type = "checkbox", title = "Concordo com os termos e condições")
)
```


```
formInfo <- list(
  id = "basicinfo",
  questions = questions,
  storage = list(
    type = STORAGE_TYPES$FLATFILE,
    # The path where responses are stored
    path = "responses"
  )
)
```

Essa é toda a informacção que precisamos:

```
ui <- fluidPage(
  formUI(formInfo)
)

server <- function(input, output, session) {
  formServer(formInfo)
}

shinyApp(ui = ui, server = server)
```

Visite o projeto original do DEAN ATTALI: [https://github.com/daattali/shinyforms](https://github.com/daattali/shinyforms)


Aqui em baixo inseri a data no formato do Brasil (dia/mes/ano).

```
library(shinyWidgets)
library(shiny)
library(shinyforms)

questions <- list(
  list(id = "nome", type = "text", title = "Qual o seu nome?", mandatory = TRUE),
  list(id = "idade", type = "numeric", title = "Qual a sua idade?"),
  list(id = "data", type = "date", title = "Qual a sua data de nascimento?"),
  list(id = "curso", type = "text", title = "Qual é seu curso (Administração, Ciência Política, Biblioteconomia, Engenharia de  Produção, etc)?"),
  list(id = "terms", type = "checkbox", title = "Concordo com os termos e condições")
)

formInfo <- list(
  id = "basicinfo",
  questions = questions,
  storage = list(
    type = STORAGE_TYPES$FLATFILE,
    path = "respostas_01_teste"
  )
)

ui <- fluidPage(
  setBackgroundColor(
    color = c("#fff9bf", "#feffd6"),gradient = "linear",
    direction = "bottom"),
  formUI(formInfo)
)

server <- function(input, output, session) {
  formServer(formInfo)
}

shinyApp(ui = ui, server = server)
```

Para tansformar a data do arquivo CSV (de número para data):

```
library("zoo")
as.Date(3692)

format(as.Date(3692),"%d/%m/%Y")

```