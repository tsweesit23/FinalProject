# Load libraries
library(tidyverse)
library(cluster)
library(factoextra)

# Load data
data <- read.csv("/Users/tsweesit/Downloads/ClusteringProject/data/travel.csv")

# Data Cleaning
# Select relevant features for customer behavior
features <- data %>%
  select(user_location_country, posa_continent, orig_destination_distance,
         is_mobile, is_package, channel, srch_adults_cnt, srch_children_cnt, srch_rm_cnt) %>%
  na.omit()  # Remove rows with missing values

# Normalize numerical columns
num_cols <- c("orig_destination_distance", "srch_adults_cnt", "srch_children_cnt", "srch_rm_cnt")
features[num_cols] <- scale(features[num_cols])

# Perform Clustering (K-Means Example)
set.seed(123)  # For reproducibility
k <- 5  # Choose number of clusters
kmeans_result <- kmeans(features, centers = k, nstart = 25)

# Add cluster labels to original data
features$cluster <- kmeans_result$cluster

# Visualize Clusters
fviz_cluster(kmeans_result, data = features, geom = "point", 
             ellipse.type = "convex", ggtheme = theme_minimal())

# Analyze cluster centers
print(kmeans_result$centers)

# Save clustered data
write.csv(features, "clustered_customers.csv", row.names = FALSE)

