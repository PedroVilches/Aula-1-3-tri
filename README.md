# Aula-1-3-tri
#Importar TXT
getwd()
dados1 <- read.table("DadosAula1.txt", header=T)
dados1
write.table(dados1, file="NovoDados1.txt")
write.table(dados1, file="NovoDados1.txt",row.names=FALSE)
write.table(dados1, file="NovoDados1.txt",row.names=FALSE, col.names=FALSE)
write.table(dados1, file="NovoDados1.txt",row.names=FALSE, col.names=FALSE, quote=FALSE)
#Exportar TXT:
write.table(dados1, file="NovoDados1.txt",row.names=FALSE, col.names=FALSE, sep=",")
#Importar CSV 
dados2 <- read.csv2("DadosAula1.csv")
dados2
write.table(dados2, file="NovoDados2.csv")

#Criando uma base de dados
dados3 <- data.frame(Nome = c("João", "Maria","Pedro"), Idade = c(30, 28, 25), Cidade = c("São Paulo", "Rio de Janeiro","Belo Horizonte"))
dados3

#Exportando XLSX:
wb <- createWorkbook()
addWorksheet(wb, "Dados")
writeData(wb, sheet = "Dados", x = dados3)

saveWorkbook(wb,"“meus_dados3.xlsx")

#Visualização de dados com R (tidyverse)
data(iris)
ggplot(iris, aes(x=Petal.Length, y=Petal.Width))
ggplot(iris, aes(x=Petal.Length, y=Petal.Width)) +
  geom_point()
ggplot(iris, aes(x=Petal.Length, y=Petal.Width)) +
  geom_point(aes(colour=Species))
ggplot(iris, aes(x=Petal.Length, y=Petal.Width)) +
  geom_point(aes(colour=Species)) +
  labs(x="Comprimento da Pétala", y="Largura da
Pétala", title="Iris") + theme_excel()

ggplot(iris, aes(x=Petal.Length, y=Petal.Width)) +
  geom_point(aes(colour=Species)) +
  labs(x="Comprimento da Pétala", y="Largura da
Pétala", title="Iris", colour="Espécies")
ggplot(iris, aes(x=Petal.Length, y=Petal.Width)) +
  geom_point(aes(colour=Species)) +
  labs(x="Comprimento da Pétala", y="Largura da
Pétala", title="Iris", colour="Espécies") +
  scale_colour_brewer(palette="Dark2")
#Exemplo 2 
ggplot(iris, aes(x=Petal.Length))
ggplot(iris, aes(x=Petal.Length)) +
  geom_histogram(bins=20)
ggplot(iris, aes(x=Petal.Length)) +
  geom_histogram(bins=20) +
  labs(x="Comprimento da Pétala",
       y="Frequência", title="Iris")
ggplot(iris, aes(x=Petal.Length)) +
  geom_histogram(bins=20) +
  labs(x="Comprimento da Pétala",
       y="Frequência", title="Iris") +
  facet_grid(~ Species)

ggplot(iris, aes(x=Petal.Length, colour=Species,
                 fill=Species)) +
  geom_histogram(bins=20) 
labs(x="Comprimento da Pétala",
     y="Frequência", title="Iris",fill = "Espécies") + 
  
  #Exemplo 3 
  ggplot(iris, aes(x=Species, y=Petal.Length,
                   colour=Species, fill=Species)) +
  geom_boxplot() +
  labs(x="Espécie", y="Comprimento da Pétala",
       title="Iris") + 
  theme_bw()
#Exemplo 4 
ggplot(iris, aes(x=Species)) + geom_bar()
ggplot(iris, aes(x=Species, colour=Species,
                 fill=Species)) + geom_bar() +
  labs(x="Espécie", y="Frequência", title="Iris")+ 
  
  #Exemplo 5 
  #coletando o valor total de cada tipo de planta 
  iris_summary <- iris %>% group_by(Species) %>%
  summarise(count = n())
#convertendo o valor total de cada tipo de planta para porcentagem
ris_summary <- iris_summary %>%
  mutate(percent = count / sum(count) * 100)
#gerando gráfoco de setores:
iris_summary <- iris %>% group_by(Species) %>%
  summarise(count = n())
iris_summary <- iris_summary %>%
  mutate(percent = count / sum(count) * 100)
ggplot(iris_summary, aes(x = "", y = percent, fill = Species)) + geom_bar(stat = "identity") +
  geom_text(aes(label = paste0(round(percent, 1),"%")), position = position_stack(vjust = 0.5)) +
  coord_polar("y") + theme_minimal() +
  labs(title = "Contagem de Espécies de Flores no Conjunto Iris", fill = "Espécie") +
  theme(axis.text.x = element_blank())
