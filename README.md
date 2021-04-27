# shinyforms - Easily create questionnaire-type forms with Shiny 

#### Versão em português do shinyforms.

Só traduzi o arquivo para o ppt-br. Você devia olhar o pacote original do DEAN ATTALI.

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
    # Right now, only flat file storage is supported
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

Visite o projeto original: [https://github.com/daattali/shinyforms](https://github.com/daattali/shinyforms)


