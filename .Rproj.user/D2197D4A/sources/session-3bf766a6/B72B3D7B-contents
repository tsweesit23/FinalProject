library(shiny)
library(cluster)
library(factoextra)
library(tidyverse)
library(ggplot2)

server <- function(input, output, session) {
  # Reactive expression to handle file upload and data cleaning
  dataset <- reactive({
    req(input$file)  # Ensure file is uploaded
    data <- read.csv(input$file$datapath)
    
    # Select relevant features for clustering
    features <- data %>%
      select(user_location_country, posa_continent, orig_destination_distance,
             is_mobile, is_package, channel, srch_adults_cnt, srch_children_cnt, srch_rm_cnt) %>%
      na.omit()
    
    # Normalize numerical columns
    num_cols <- c("orig_destination_distance", "srch_adults_cnt", "srch_children_cnt", "srch_rm_cnt")
    features[num_cols] <- scale(features[num_cols])
    return(features)
  })
  
  # Reactive expression to run clustering
  clustering <- eventReactive(input$runClustering, {
    req(dataset())  # Ensure dataset is ready
    kmeans(dataset(), centers = input$clusters, nstart = 25)
  })
  
  # Plot the clustering result
  output$clusterPlot <- renderPlot({
    req(clustering())
    fviz_cluster(clustering(), data = dataset(), geom = "point", ellipse.type = "convex")
  })
  
  # Show cluster centers
  output$clusterSummary <- renderTable({
    req(clustering())
    as.data.frame(clustering()$centers)
  })
}

