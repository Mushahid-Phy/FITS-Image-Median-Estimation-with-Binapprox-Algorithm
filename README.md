# FITS-Image-Median-Estimation-with-Binapprox-Algorithm
This repository provides an efficient approach to estimating the median pixel values from a collection of 2D astronomy images in FITS files. The median is approximated using the binapprox algorithm, which optimizes memory usage and computation time. The algorithm processes pixel values across multiple images without the need to store or sort the entire dataset, making it suitable for large-scale astronomical data analysis.

Features

    1.Approximate Median Calculation: Efficiently calculates an approximation of the median pixel values across multiple FITS files using histogram binning.
    2.2D Array Support: Processes 2D arrays, which are common in astronomical image data.
    3.Running Mean and Standard Deviation: Utilizes a helper function that calculates the mean and standard deviation in a single pass using Welford’s method.
    4.Scalable: Designed to handle large datasets with multiple high-resolution FITS images.

Files and Functions
1. median_bins_fits(filenames, B)

This function processes a list of FITS files and creates bins for each pixel across the images based on a user-defined number of bins (B). It returns the mean, standard deviation, left bin, and histogram bins for each pixel location.

    Arguments:
        filenames: List of FITS file paths.
        B: Number of bins for the histogram.
    Returns:
        mean: The running mean of pixel values.
        std: The running standard deviation of pixel values.
        left_bin: Count of pixel values below the mean minus the standard deviation.
        bins: The binned counts of pixel values for each bin.

2. median_approx_fits(filenames, B)

Uses the output of median_bins_fits to compute an approximate median for each pixel across all FITS files. The function accumulates the bin counts until it reaches the midpoint, which represents the median.

    Arguments:
        filenames: List of FITS file paths.
        B: Number of bins for the histogram.
    Returns:
        median: The approximate median for each pixel.

3. running_stats(filenames)

Helper function that computes the running mean and standard deviation for the stack of FITS files using Welford’s method. This avoids the need to hold the entire dataset in memory and ensures numerical stability.

    Arguments:
        filenames: List of FITS file paths.
    Returns:
        mean: The mean of pixel values.
        std: The standard deviation of pixel values.

        This approach is optimized for memory usage and large datasets. The binapprox algorithm provides an approximation of the median without sorting or storing the full dataset. The use of Welford’s method in running_stats ensures that the computation of mean and standard deviation is both accurate and memory-efficient.
