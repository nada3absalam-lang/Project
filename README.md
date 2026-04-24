import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import pandas as pd  # Ensure you have pandas for `df`

# Create the figure
plt.figure(figsize=(16, 12))

# Compute the correlation matrix, dropping the 'Time' column
corr = df.drop(columns=['Time']).corr()

# Create a mask for the upper triangle
mask = np.triu(np.ones_like(corr, dtype=bool))

# Generate a heatmap
sns.heatmap(
    corr, 
    mask=mask, 
    cmap='coolwarm', 
    center=0, 
    annot=False, 
    linewidths=0.3, 
    vmin=-1, 
    vmax=1
)

# Add title and save the figure
plt.title('Figure 5: Feature Correlation Heatmap')
plt.tight_layout()
plt.savefig('../figures/fig5_correlation_heatmap.png', dpi=150, bbox_inches='tight')

# Display the plot
plt.show()

# Print features most correlated with fraud
print("Features most correlated with fraud (Class):")
print(corr['Class'].abs().sort_values(ascending=False).head(10))
