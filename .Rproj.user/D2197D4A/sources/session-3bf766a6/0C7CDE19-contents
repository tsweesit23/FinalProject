options(shiny.maxRequestSize = 30 * 1024^2) 

ui <- fluidPage(
  titlePanel("Customer Behavior Clustering"),
  
  sidebarLayout(
    sidebarPanel(
      fileInput("file", "Upload Dataset", accept = c(".csv")),
      numericInput("clusters", "Number of Clusters:", value = 5, min = 2, max = 10),
      actionButton("runClustering", "Run Clustering")
    ),
    
    mainPanel(
      tabsetPanel(
        tabPanel("Cluster Visualization", plotOutput("clusterPlot")),
        tabPanel("Cluster Summary", tableOutput("clusterSummary"))
      )
    )
  )
)

