# Automatic Clustering of Coordinates
# Selection  Number of Clusters Using BIC Score from GMM

This project demonstrates a method to automatically choose the number of clusters for clustering geographical coordinates using Gaussian Mixture Models (GMM) and K-means algorithm. It provides visualizations of the cluster distribution and cluster visualization on a map.

## Requirements

- pandas
- matplotlib
- scikit-learn
- numpy
- scipy

## Usage

1. Ensure that the `coordinates.pkl` file is present in the same directory as the code file.

2. Run the code to perform clustering on the coordinates.

3. The method will automatically select the optimal number of clusters based on Bayesian Information Criterion (BIC).

4. The resulting clusters will be added to the `coordinates` dataframe.

5. The number of clusters will be displayed.

6. The distribution of clusters will be plotted in a bar chart.

7. The clusters will be visualized on a map.
## References
https://scikit-learn.org/stable/modules/generated/sklearn.mixture.GaussianMixture.html

## Example

```python
# Load the coordinates data from the pickle file
coordinates = pd.read_pickle('coordinates.pkl')

# Cluster the coordinates and automatically choose the number of clusters
coordinates, num_clusters = cluster_coordinates(coordinates)

# Display the number of clusters
print(f"Number of clusters: {num_clusters}")

# Plot the distribution of clusters
cluster_counts = coordinates['cluster'].value_counts()
plt.figure(figsize=(10, 6))
cluster_counts.plot(kind='bar')
plt.xlabel('Cluster')
plt.ylabel('Frequency')
plt.title('Distribution of Clusters')
plt.show()

# Visualize the clusters on a map
colors = ['green', 'blue', 'red', 'yellow']
plt.figure(figsize=(8, 8))
for cluster_id in range(num_clusters):
    cluster_points = coordinates[coordinates['cluster'] == cluster_id]
    plt.scatter(cluster_points['Composite:GPSLongitude'], 
                cluster_points['Composite:GPSLatitude'],
                color=colors[cluster_id], label=f'Cluster {cluster_id}')

plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.title('Cluster Visualization')
plt.legend()
plt.grid(True)
plt.show()

