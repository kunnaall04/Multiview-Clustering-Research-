# Multi-View Clustering Research: Feature Extraction and DBSCAN Analysis

## 📋 Project Overview

This repository contains a comprehensive research project on **multi-view clustering** using various feature extraction methods and DBSCAN clustering algorithm. The research focuses on analyzing the effectiveness of different feature combinations for clustering tasks on two benchmark datasets: **COIL-20** and **Caltech-7**.

## 🎯 Research Objectives

- **Primary Goal**: Investigate the performance of multi-view clustering using different feature extraction methods
- **Secondary Goal**: Compare clustering algorithms (K-Means vs DBSCAN) and optimize parameters
- **Research Question**: Which combination of features provides the best clustering performance for image datasets?

## 📊 Datasets Used

### 1. Caltech-7 Dataset (Primary Focus)
- **Source**: Subset of Caltech-101 dataset
- **Classes**: 7 categories with varying image counts
- **Total Images**: 1,474 images
- **Classes Breakdown**:
  - Faces: 435 images
  - Motorbikes: 798 images
  - Dollar-Bill: 52 images
  - Garfield: 34 images
  - Snoopy: 35 images
  - Stop-Sign: 64 images
  - Windsor-Chair: 56 images

### 2. COIL-20 Dataset (Secondary Analysis)
- **Source**: Columbia Object Image Library
- **Cars Subset**: 144 images (objects 10 and 14)
- **Full Dataset**: 1,440 images (20 objects × 72 rotations each)
- **Purpose**: Validation and comparative analysis

## 🔧 Feature Extraction Methods (Views)

Our research implements **6 different feature extraction techniques** to create multiple views of the data:

### 1. LBP (Local Binary Pattern)
- **Purpose**: Texture analysis and local pattern recognition
- **Parameters**: 
  - Radius: 3
  - Number of points: 24
  - Method: 'uniform'
- **Feature Dimension**: 26 features
- **Advantage**: Robust to illumination changes, captures local texture patterns

### 2. HOG (Histogram of Oriented Gradients)
- **Purpose**: Shape and edge detection
- **Parameters**:
  - Pixels per cell: (8,8)
  - Cells per block: (2,2)
  - Orientations: 9
- **Feature Dimension**: 8,100 features
- **Advantage**: Captures shape information and spatial relationships

### 3. WM (Wavelet Moments)
- **Purpose**: Multi-resolution analysis
- **Method**: Haar wavelet decomposition
- **Feature Dimension**: 8 features (mean & std of 4 coefficients)
- **Advantage**: Captures both frequency and spatial information

### 4. CENTRIST (Census Transform)
- **Purpose**: Texture description using census transform
- **Implementation**: LBP-based with 'uniform' method
- **Feature Dimension**: 26 features
- **Advantage**: Computationally efficient, good for texture classification

### 5. Gabor Features
- **Purpose**: Edge and texture detection at different orientations
- **Feature Dimension**: 48 features
- **Advantage**: Mimics human visual system, good for texture analysis

### 6. GIST Features
- **Purpose**: Global scene descriptors
- **Feature Dimension**: 512 features
- **Advantage**: Captures global scene properties and spatial layout

## 🤖 Clustering Approaches

### K-Means Clustering
- **Usage**: Initial clustering experiments and baseline comparison
- **Parameters**: n_clusters=2-5, random_state=42
- **Evaluation**: Silhouette scores, cluster visualization
- **Limitations**: Requires predefined number of clusters, sensitive to initialization

### DBSCAN Clustering (Primary Method)
- **Usage**: Advanced clustering with automatic noise detection
- **Parameter Tuning**: Systematic eps optimization (0.1-2.0 range)
- **Advantages**: 
  - No need to specify number of clusters
  - Handles noise and outliers effectively
  - Discovers clusters of arbitrary shapes
- **Evaluation**: Silhouette scores, NMI, Rand Index

## 📈 Performance Evaluation Metrics

### 1. Silhouette Score
- **Purpose**: Measures cluster cohesion and separation
- **Range**: -1 to 1 (higher is better)
- **Interpretation**: Measures how similar an object is to its own cluster vs other clusters

### 2. Normalized Mutual Information (NMI)
- **Purpose**: Measures cluster-label agreement
- **Range**: 0 to 1 (higher is better)
- **Interpretation**: Quantifies the mutual information between true and predicted clusters

### 3. Rand Index (RI)
- **Purpose**: Overall clustering accuracy
- **Range**: 0 to 1 (higher is better)
- **Interpretation**: Measures the percentage of correct decisions made by the algorithm

## 🔬 Research Methodology

### Phase 1: Data Preparation
1. **Image Loading**: Load images from directory structure
2. **Preprocessing**: Convert to grayscale, normalize pixel values
3. **Label Extraction**: Extract true labels from directory structure
4. **Data Organization**: Organize files for systematic processing

### Phase 2: Feature Extraction
1. **Individual Feature Extraction**: Extract each feature type separately
2. **Feature Standardization**: Apply StandardScaler for normalization
3. **Dimensionality Reduction**: Apply PCA to reduce to 2D for visualization
4. **Feature Combination**: Create various combinations of features

### Phase 3: Clustering Experiments
1. **Parameter Tuning**: Systematic optimization of DBSCAN parameters
2. **Multiple Runs**: Test different feature combinations
3. **Performance Evaluation**: Compute multiple evaluation metrics
4. **Statistical Analysis**: Compare results across different configurations

### Phase 4: Analysis & Visualization
1. **2D Visualization**: PCA plots showing cluster distributions
2. **Performance Comparison**: Tabular comparison of results
3. **Statistical Significance**: Analysis of performance differences
4. **Result Interpretation**: Draw conclusions from experimental data

## 📊 Key Research Findings

### Best Performing Configuration
- **Feature Combination**: LBP + WM + CENTRIST (60 features total)
- **Clustering Method**: DBSCAN (eps=1.1, min_samples=20)
- **Performance Metrics**:
  - NMI: 0.320
  - Rand Index: 0.720
  - Silhouette Score: 0.454
- **Clusters Discovered**: 2 main clusters with 245 outliers

### Performance Comparison Table

| Feature Combination | Best EPS | Clusters | NMI | Rand Index | Silhouette Score |
|-------------------|----------|----------|-----|------------|------------------|
| LBP only | 0.7 | 2 | 0.299 | 0.708 | 0.412 |
| WM only | 0.2 | 3 | 0.282 | 0.665 | 0.096 |
| CENTRIST only | 0.7 | 2 | 0.299 | 0.708 | 0.412 |
| LBP + WM | 0.6 | 2 | 0.289 | 0.673 | 0.305 |
| WM + CENTRIST | 0.6 | 2 | 0.289 | 0.673 | 0.305 |
| LBP + CENTRIST | 1.0 | 2 | 0.302 | 0.710 | 0.415 |
| **LBP + WM + CENTRIST** | **1.1** | **2** | **0.320** | **0.720** | **0.454** |

### Key Insights

1. **Feature Complementarity**: 
   - LBP and CENTRIST show similar individual performance
   - WM features provide complementary information when combined
   - Three-feature combination achieves optimal performance

2. **Clustering Algorithm Performance**:
   - DBSCAN outperforms K-Means due to noise handling
   - Parameter sensitivity is critical for DBSCAN performance
   - eps parameter optimization is essential for good results

3. **Dataset Characteristics**:
   - 2-3 clusters optimal for Caltech-7 dataset
   - Significant number of outliers present (245 out of 1474)
   - Feature standardization crucial for multi-view clustering

## 🗂️ Repository Structure

```
caltech/
├── README.md                           # This comprehensive documentation
├── requirements.txt                    # Python dependencies
├── .gitignore                         # Git ignore file
├── CALTECH7_DB-SCAN.pdf              # Detailed results and analysis
│
├── notebooks/                         # Jupyter notebooks
│   ├── CALTECH7LBP-checkpoint.ipynb  # LBP analysis on Caltech-7
│   ├── finalcal7-checkpoint.ipynb    # Comprehensive Caltech-7 analysis
│   ├── DBSCAN-checkpoint.ipynb       # DBSCAN parameter optimization
│   ├── car_coil20-checkpoint.ipynb   # COIL-20 car subset analysis
│   ├── COIL20_Image_Processing-checkpoint.ipynb  # Full COIL-20 processing
│   ├── combined_class_coik_correct-checkpoint.ipynb  # Combined features
│   ├── dbscan_car-checkpoint.ipynb   # DBSCAN on car subset
│   ├── hog_class_coil_correct-checkpoint.ipynb  # HOG feature analysis
│   ├── lbp_class_coil_correct-checkpoint.ipynb  # LBP feature analysis
│   ├── fileCALTECH7-checkpoint.ipynb # Dataset organization
│   └── filesharing-checkpoint.ipynb  # File management utilities
│
├── data/                              # Dataset information
│   ├── caltech7_info.md              # Caltech-7 dataset details
│   └── coil20_info.md                # COIL-20 dataset details
│
├── results/                           # Results and analysis
│   ├── performance_summary.csv       # Performance metrics table
│   ├── clustering_visualizations/    # PCA plots and cluster visualizations
│   └── parameter_analysis/           # Parameter tuning results
│
└── src/                              # Source code modules
    ├── feature_extraction.py         # Feature extraction functions
    ├── clustering.py                 # Clustering algorithms
    ├── evaluation.py                 # Evaluation metrics
    └── visualization.py              # Visualization functions
```

## 🚀 Getting Started

### Prerequisites
- Python 3.7+
- Jupyter Notebook
- Required Python packages (see requirements.txt)

### Installation
1. Clone the repository:
```bash
git clone https://github.com/yourusername/caltech-multiview-clustering.git
cd caltech-multiview-clustering
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Download datasets:
   - Caltech-7: Place in `data/caltech7/`
   - COIL-20: Place in `data/coil20/`

### Usage
1. **Run individual experiments**:
   - Open any notebook in the `notebooks/` directory
   - Follow the execution order in each notebook

2. **Reproduce results**:
   - Start with `finalcal7-checkpoint.ipynb` for comprehensive analysis
   - Use `DBSCAN-checkpoint.ipynb` for parameter optimization

3. **Custom experiments**:
   - Modify feature extraction parameters in `src/feature_extraction.py`
   - Adjust clustering parameters in `src/clustering.py`

## 📝 Notebook Descriptions

### Core Analysis Notebooks
- **`finalcal7-checkpoint.ipynb`**: Main research notebook with comprehensive analysis
- **`CALTECH7LBP-checkpoint.ipynb`**: LBP feature analysis on Caltech-7
- **`DBSCAN-checkpoint.ipynb`**: DBSCAN parameter optimization and analysis

### Feature-Specific Notebooks
- **`hog_class_coil_correct-checkpoint.ipynb`**: HOG feature extraction and clustering
- **`lbp_class_coil_correct-checkpoint.ipynb`**: LBP feature extraction and clustering
- **`combined_class_coik_correct-checkpoint.ipynb`**: Combined feature analysis

### Dataset-Specific Notebooks
- **`car_coil20-checkpoint.ipynb`**: COIL-20 car subset analysis
- **`COIL20_Image_Processing-checkpoint.ipynb`**: Full COIL-20 dataset processing

### Utility Notebooks
- **`fileCALTECH7-checkpoint.ipynb`**: Dataset organization and preparation
- **`filesharing-checkpoint.ipynb`**: File management and organization

## 🔬 Technical Implementation Details

### Feature Extraction Pipeline
1. **Image Preprocessing**: Grayscale conversion, normalization
2. **Feature Computation**: Parallel extraction of multiple feature types
3. **Feature Standardization**: Z-score normalization
4. **Dimensionality Reduction**: PCA for visualization (2D)

### Clustering Pipeline
1. **Parameter Optimization**: Grid search for optimal eps values
2. **Clustering Execution**: DBSCAN with optimized parameters
3. **Performance Evaluation**: Multiple metrics computation
4. **Visualization**: 2D PCA plots with cluster assignments

### Evaluation Pipeline
1. **Metric Computation**: Silhouette score, NMI, Rand Index
2. **Statistical Analysis**: Performance comparison across configurations
3. **Visualization**: Cluster plots, performance charts
4. **Interpretation**: Results analysis and insights

## 📚 Research Context and Motivation

### Why Multi-View Clustering?
Multi-view clustering leverages multiple representations (views) of the same data to improve clustering performance. Each feature extraction method captures different aspects of the data:
- **LBP**: Local texture patterns
- **HOG**: Shape and edge information
- **WM**: Multi-resolution characteristics
- **CENTRIST**: Census transform features

### Why DBSCAN?
DBSCAN was chosen over K-Means because:
1. **No need to specify cluster count**: Automatically discovers optimal number of clusters
2. **Noise handling**: Identifies and handles outliers effectively
3. **Shape flexibility**: Can find clusters of arbitrary shapes
4. **Parameter robustness**: Less sensitive to parameter variations

### Why These Datasets?
- **Caltech-7**: Provides diverse object categories with varying complexity
- **COIL-20**: Offers controlled rotation variations for validation
- **Combined analysis**: Allows for comprehensive evaluation across different data characteristics

## 🎓 Research Contributions

1. **Systematic Evaluation**: Comprehensive comparison of 6 different feature extraction methods
2. **Multi-View Analysis**: Investigation of feature combination effectiveness
3. **Parameter Optimization**: Systematic DBSCAN parameter tuning methodology
4. **Performance Benchmarking**: Detailed evaluation using multiple metrics
5. **Reproducible Research**: Complete code and data organization for reproducibility

## 🔮 Future Work and Extensions

### Potential Improvements
1. **Additional Feature Types**: Include more advanced features (CNN features, SIFT, etc.)
2. **Advanced Clustering**: Test other clustering algorithms (Spectral Clustering, Gaussian Mixture Models)
3. **Multi-View Fusion**: Implement advanced multi-view fusion techniques
4. **Larger Datasets**: Extend analysis to larger image datasets
5. **Deep Learning Integration**: Incorporate deep learning-based feature extraction

### Research Directions
1. **Theoretical Analysis**: Mathematical analysis of multi-view clustering performance
2. **Scalability**: Optimization for large-scale datasets
3. **Real-world Applications**: Apply to practical computer vision problems
4. **Comparative Studies**: Compare with state-of-the-art multi-view clustering methods

## 📖 References and Citations

### Key Papers
1. Ester, M., et al. (1996). "A density-based algorithm for discovering clusters in large spatial databases with noise." KDD.
2. Ojala, T., et al. (2002). "Multiresolution gray-scale and rotation invariant texture classification with local binary patterns." TPAMI.
3. Dalal, N., & Triggs, B. (2005). "Histograms of oriented gradients for human detection." CVPR.

### Datasets
1. Fei-Fei, L., et al. (2004). "Learning generative visual models from few training examples." CVPR.
2. Nene, S. A., et al. (1996). "Columbia object image library (COIL-20)." Technical Report.

## 👥 Authors and Acknowledgments

- **Primary Researcher**: [Your Name]
- **Institution**: [Your Institution]
- **Year**: 2023-2024

### Acknowledgments
- Thanks to the creators of the Caltech-101 and COIL-20 datasets
- Appreciation for the open-source libraries used in this research
- Special thanks to the machine learning community for inspiration and resources

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## 📞 Contact and Support

For questions, suggestions, or collaboration opportunities, please contact:
- **Email**: kunalsali04@gmail.com
- **GitHub**: kunnaall04

---

**Note**: This research represents a comprehensive investigation into multi-view clustering for image data. The results demonstrate the effectiveness of combining multiple feature extraction methods and the importance of proper parameter optimization in clustering algorithms.
