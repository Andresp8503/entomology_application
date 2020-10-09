# entomology_application
application tools of  statistical analysis for entomology research 


#Counts of 554 aphids of the species Sitobion avenae, sampled on 28 June 1996
#' in a 250 x 180-m field of winter wheat near Wimborne, Dorset, UK. The 63
#' sampling units, made of the inspection of five tillers each, were located on
#' a 9 x 7 rectangular grid at intervals of 30 m.
#' 
#' #' @format A data frame with 63 rows and 3 variables:
#' \tabular{lll}{
#'     [, 1:2] \tab x,y   \tab Grid spatial coordinates. \cr
#'     [, 3:4] \tab xm,ym \tab Metric spatial coordonates. \cr
#'     [, 5]   \tab i     \tab Counts of aphids. \cr
#'     
#'     Perry JN, Winder L, Holland JM, Alston RD. 1999. Red-blue plots for
#'     detecting clusters in count data. Ecology Letters 2, 106-13.
#'     \href{https://doi.org/10.1046/j.1461-0248.1999.22057.x}{doi:10.1046/j.1461-0248.1999.22057.x}

#install.packages("epiphy")
library(epiphy)
#install.packages("statsr")
#library(MASS)
#para cargardatos de ejemplo 
#aphids, arthropdscodling_moths" conteo
#citrus_ctv incidencia del virus de la trizteza
#"tobacco_viruses"" "tomato_tswv"" incidencia de virus

# cargue de datos
as.data.frame('aphids')

#imprmir los datos en la cosola
aphids


#CREACION DEL VECTOR
aphids<-aphids

#indicide Fischer# #diferentes formas de ejecutar#

#Forma 1 
aphids_Fisher_agr1<-agg_index(aphids$i,method=c("fisher"), flavor = c("count"))

#agg_index(x, method = c("fisher", "lloyd", "morisita"), flavor = c("count",
#"incidence"), n, ...)

#imprimir en la consola 
aphids_Fisher_agr1

#Forma 2 
aphids_Fisher_agr2<-agg_index(aphids$i)
#aphids_Fisher_agr2<-agg_index(aphids[,5])
#aphids_Fisher_agr2<-agg_index(aphids [,'i'])

#Forma 3 
aphids_Fisher_agr3<-agg_index(count(aphids))
aphids_Fisher_agr3

#Indice de Lloyd
aphids_lloyd_agr1<-agg_index(aphids$i,method=c("lloyd"), flavor = c("count"))

aphids_lloyd_agr1


#values of Fisher's and Lloyd's indices can be interpreted as follows:

#index < 1: uniform pattern;

#index = 1: random pattern;

#index > 1: aggregated pattern.

#The following table gives information about the applicability of the various methods.

#count fisher	lloyd morisita
#incidence fisher	 morisita
#severity   ninguno

#Indice de Lloyd
aphids_lloyd_agr1<-agg_index(aphids$i,method=c("lloyd"), flavor = c("count"))
aphids_lloyd_agr1
aphids_lloyd_agr2<-agg_index(aphids$i,method="lloyd")
aphids_lloyd_agr2
#indice de Lloyd coo agregación
aphids_lloyd_agr2_1<-agg_index(aphids$i,method="lloyd", type = "mean-crowding")
aphids_lloyd_agr2_1
#indice morisita

aphids_morisita_agr1<-agg_index(aphids$i,method=c("morisita"), flavor = c("count"))

aphids_morisita_agr1
####################################################################################
#Distribucion binomial-B
calpha.test(aphids_Fisher_agr1)

chisq.test(aphids_Fisher_agr1)

#creando el vector del objeto

count_aphids<-count(aphids, mapping(x=xm, y =ym))

#calculo indice de  Perry                  

result_aphids <-sadie(count_aphids)
result_aphids
summary(result_aphids)
#grafica de indice absoluto  y de umbral 
plot(result_aphids)

plot(result_aphids, isoclines=TRUE)
