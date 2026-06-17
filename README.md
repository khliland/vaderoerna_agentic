# Interactive PCA Visualizer

A single-file web application for exploring data with Principal Component Analysis (PCA) using **PyScript**, **JavaScript**, and **Plotly**.

## Features

- **File Upload**: Load CSV data directly in the browser
- **Automatic PCA Computation**: Standardizes features and computes principal components using scikit-learn
- **Dual Visualization**:
  - **Left**: Parallel coordinates plot showing raw data (features as columns, samples as lines)
  - **Right**: PCA score plot (scatter plot of principal components)
- **Linked Selection**: Select/highlight points in one plot to see them highlighted in the other
- **Choosable Dimensions**: Pick any two principal components (PC1, PC2, PC3, etc.) for the score plot via dropdown selectors
- **Responsive Design**: Works on desktop and tablet sizes

## Quick Start

1. **Open the app**: 
   ```bash
   # Simply open index.html in a modern web browser
   open index.html
   ```
   Or drag `index.html` into your browser.

2. **Load test data**:
   - Click "Choose File" and select `sample_iris.csv` to test with the included Iris dataset

3. **Interact**:
   - In the parallel coordinates plot (left), click/drag to select samples
   - Selected samples highlight in red in both plots
   - Use the dropdowns at the top to change which PCs appear on the score plot axes
   - Click individual points in the score plot to toggle their selection

## Data Format

Provide a **CSV file** with:
- **Header row**: Feature names
- **Numeric columns only**: All data must be numeric
- **At least 2 samples and 2 features**: Required for PCA

Example:
```csv
feature1,feature2,feature3
1.2,3.4,5.6
2.3,4.5,6.7
3.4,5.6,7.8
```

## How It Works

### PyScript Backend
- Reads uploaded CSV into a pandas DataFrame
- Standardizes features (mean=0, std=1) using scikit-learn's `StandardScaler`
- Fits PCA using scikit-learn, computing all possible principal components
- Exposes functions to JavaScript for data retrieval

### JavaScript Frontend
- Handles file upload and triggers PyScript computation
- Manages shared selection state (which samples are selected)
- Uses Plotly to render both plots and handle click/selection events
- Re-renders plots when selection changes or dimension selectors change

### Linked Plots
- **Parallel coordinates plot**: Drag/select samples → updates `selectedIndices`
- **Score plot**: Click/select samples → updates `selectedIndices`
- Both plots re-render with selected samples highlighted in red

## Browser Requirements

- Modern browser (Chrome, Firefox, Safari, Edge)
- JavaScript enabled
- Internet connection (loads libraries from CDN)

## File Structure

```
Agentic_test/
├── index.html              # Complete single-file web app
└── sample_iris.csv         # Test dataset (Iris flower measurements)
```

## Customization

To modify the app:
- **Max PC options**: Edit the `<select>` elements in HTML to change from PC1–PC5 to different ranges
- **Colors/styling**: Modify CSS in the `<style>` block
- **Default selection behavior**: Edit JavaScript event handlers (`handleParallelSelection`, `handleScoreSelection`, etc.)

## Troubleshooting

### "No numeric columns found"
- Ensure your CSV contains only numeric data (no text columns)
- Header row is expected but should contain feature names

### "Plotly is not defined"
- Plotly library failed to load from CDN. Check internet connection.

### PyScript not loading
- PyScript loads from CDN. Check browser console (F12) for network errors.
- First-time load can take 10–30 seconds as it downloads Python runtime.

### Performance with large files
- PyScript is client-side only, so large files (~1000+ samples) may take time
- Standardization and PCA scale with sample count and feature count
- Consider downsampling if your dataset is very large

## License

Free to use and modify.
