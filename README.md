# Cell Segmentation and Co-localization Analysis Pipeline

A comprehensive Python pipeline for automated cell counting and co-localization analysis in fluorescence microscopy images. This toolkit processes multi-channel confocal microscopy data (.czi files) to quantify cell populations and analyze marker co-expression patterns.

## 🔬 Overview

This pipeline consists of two main components:

1. **Image Preprocessing** (`01_image_preprocessing.ipynb`): Extracts individual channels from multi-channel microscopy files and performs automated cell segmentation
2. **Cell Counting Analysis** (`02_cell_counting_analysis.ipynb`): Counts cells in each channel and analyzes co-localization patterns between fluorescence markers

## 🚀 Features

### Image Preprocessing
- **Multi-channel extraction**: Splits .czi files into individual channel/Z-plane images
- **Automated segmentation**: Uses Cellpose (cpsam model) for accurate cell boundary detection
- **Parameter optimization**: Tools to find optimal segmentation parameters for your dataset
- **Batch processing**: Handle multiple files efficiently
- **Quality control**: Progress reporting and error handling

### Cell Counting Analysis
- **Multi-marker analysis**: Supports 3-channel analysis (GFP, c-fos, NeuN)
- **ROI-based counting**: Process user-defined regions of interest
- **Co-localization detection**: Identifies cells expressing multiple markers
- **3D analysis**: Handles multiple Z-planes independently
- **Export capabilities**: Generates CSV reports and ImageJ-compatible ROI files
- **Boundary exclusion**: Removes edge artifacts for accurate counting

## 📋 Prerequisites

- Python 3.8+
- CUDA-compatible GPU (optional, for faster Cellpose segmentation)
- Sufficient RAM (8GB+ recommended for large images)

## 🛠 Installation

1. **Clone the repository:**
```bash
git clone https://github.com/yourusername/cell-segmentation-pipeline.git
cd cell-segmentation-pipeline
```

2. **Create a virtual environment (recommended):**
```bash
python -m venv cell_analysis_env
source cell_analysis_env/bin/activate  # On Windows: cell_analysis_env\Scripts\activate
```

3. **Install dependencies:**
```bash
pip install -r requirements.txt
```

4. **GPU Setup (optional but recommended):**
   - For CUDA 11.x: Uncomment `cupy-cuda11x>=9.0.0` in requirements.txt
   - For CUDA 12.x: Uncomment `cupy-cuda12x>=12.0.0` in requirements.txt
   - Then run: `pip install -r requirements.txt`

## 📖 Usage

### Step 1: Image Preprocessing

1. Open `01_image_preprocessing.ipynb` in Jupyter Lab/Notebook
2. Update file paths in Cell 1 to point to your .czi files
3. Run all cells to:
   - Extract individual channels
   - Perform automated segmentation
   - Generate training data for analysis

**Optional: Parameter Optimization**
- Uncomment and run Cell 4 to test different Cellpose parameters
- Choose optimal settings based on your cell types and imaging conditions

### Step 2: Cell Counting Analysis

1. Open `02_cell_counting_analysis.ipynb`
2. Update the sample configuration in Cell 2:
   ```python
   sample_list = [
       ("path/to/your/file.czi", "path/to/roi_file.zip", "path/to/cellpose_output/"),
       # Add more samples as needed
   ]
   ```
3. Run all cells to:
   - Process all ROIs and Z-planes
   - Count cells in each fluorescence channel
   - Analyze co-localization patterns
   - Generate comprehensive reports

## 📊 Output Files

### From Image Preprocessing:
- `filename_C{channel}_Z{z-plane}.ome.tif`: Individual channel images
- `filename_C{channel}_Z{z-plane}_mask.tiff`: Segmentation masks
- `filename_C{channel}_Z{z-plane}.zip`: ROI coordinates for detected cells

### From Cell Counting Analysis:
- `cell_counting_results.csv`: Comprehensive cell count table
- `filename_ROI{X}_final.zip`: Co-localized cell coordinates for ImageJ

## 📁 File Structure

```
cell-segmentation-pipeline/
│
├── 01_image_preprocessing.ipynb       # Step 1: Channel extraction & segmentation
├── 02_cell_counting_analysis.ipynb   # Step 2: Cell counting & co-localization
├── requirements.txt                   # Python dependencies
├── README.md                         # This file
│
└── example_data/                     # (Optional) Example datasets
    ├── sample.czi                   # Example microscopy file
    └── sample_rois.zip              # Example ROI file
```

## 🔧 Configuration

### Channel Mapping
By default, the pipeline expects:
- **Channel 0 (C0)**: GFP - Specific cell population marker
- **Channel 1 (C1)**: c-fos - Neuronal activation marker  
- **Channel 3 (C3)**: NeuN - General neuronal marker

Modify the channel assignments in `read_channels_z()` function if your setup differs.

### Segmentation Parameters
Key Cellpose parameters you can adjust:
- `diameter`: Expected cell diameter in pixels (None = auto-detect)
- `flow_threshold`: Quality threshold for flow (0.4 default, range 0-1)
- `cellprob_threshold`: Cell probability threshold (0.0 default, range -6 to 6)

### Co-localization Analysis
- `threshold`: IoU overlap threshold for co-localization (0.8 default)
- Adjust in `count_overlaps()` function calls

## 🧪 Example Workflow

1. **Prepare your data:**
   - Multi-channel .czi files from confocal microscopy
   - Manually defined ROIs saved as .zip files (using ImageJ/FIJI)

2. **Run preprocessing:**
   ```bash
   jupyter lab 01_image_preprocessing.ipynb
   ```

3. **Analyze cell counts:**
   ```bash
   jupyter lab 02_cell_counting_analysis.ipynb
   ```

4. **Review results:**
   - Check `cell_counting_results.csv` for quantitative data
   - Import ROI files into ImageJ for visual validation

## 📈 Results Interpretation

The analysis generates a CSV table with columns:
- `Z`: Z-plane number
- `ROI`: Region of interest identifier  
- `GFP`: Count of GFP+ cells
- `c-fos`: Count of c-fos+ cells
- `NeuN`: Count of NeuN+ cells
- `GFP+ NEUN+`: Count of cells expressing both GFP and NeuN
- `FOS+ NEUN+`: Count of cells expressing both c-fos and NeuN
- `GFP+ FOS+ NEUN+`: Count of cells expressing all three markers

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [Cellpose](https://github.com/MouseLand/cellpose) for cell segmentation
- Uses [aicspylibczi](https://github.com/AllenCellModeling/aicspylibczi) for .czi file handling
- Inspired by the need for reproducible microscopy analysis workflows

## 📚 Citation

If you use this pipeline in your research, please cite:

```bibtex
@software{cell_segmentation_pipeline,
  title = {Cell Segmentation and Co-localization Analysis Pipeline},
  author = {Your Name},
  year = {2024},
  url = {https://github.com/yourusername/cell-segmentation-pipeline}
}
```

## 🐛 Issues and Support

If you encounter any problems or have questions:

1. Check the [Issues](https://github.com/yourusername/cell-segmentation-pipeline/issues) page
2. Create a new issue with detailed description of the problem
3. Include sample data and error messages when possible

## 📧 Contact

For questions or collaborations, please contact: your.email@institution.edu

---

*This pipeline was developed to standardize and automate fluorescence microscopy analysis workflows, making quantitative cell biology more accessible and reproducible.* 