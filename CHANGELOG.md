# Changelog

All notable changes to the Cell Segmentation and Co-localization Analysis Pipeline will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-12-19

### Added
- Initial release of the cell segmentation and co-localization analysis pipeline
- Two-step workflow for image preprocessing and cell counting
- Support for multi-channel .czi microscopy files
- Automated cell segmentation using Cellpose (cpsam model)
- Parameter optimization tools for Cellpose configuration
- ROI-based analysis with boundary cell exclusion
- Co-localization analysis with IoU-based overlap detection
- Export capabilities to CSV and ImageJ-compatible formats
- Comprehensive documentation and usage examples
- Support for 3D analysis (multiple Z-planes)
- GPU acceleration support for faster processing

### Features
- **01_image_preprocessing.ipynb**: Channel extraction and automated segmentation
- **02_cell_counting_analysis.ipynb**: Cell counting and co-localization analysis
- Multi-marker analysis (GFP, c-fos, NeuN)
- Quality control and progress reporting
- Batch processing capabilities
- Error handling and validation

### Dependencies
- Python 3.8+
- Cellpose 2.0+
- NumPy, Pandas, scikit-image
- aicspylibczi for .czi file handling
- roifile for ImageJ ROI compatibility
- Optional GPU support via CuPy

### Documentation
- Comprehensive README with installation and usage instructions
- Step-by-step notebooks with detailed comments
- Configuration examples and troubleshooting guide
- Citation information and license (MIT)

---

## [Unreleased]

### Planned Features
- Support for additional microscopy file formats (.nd2, .lsm)
- Integration with other segmentation models (SAM, StarDist)
- Statistical analysis and visualization tools
- Automated quality control metrics
- Docker containerization for easier deployment
- Command-line interface option
- Integration with image analysis platforms (QuPath, CellProfiler)

---

*For support and feature requests, please open an issue on GitHub.* 