## Table of Contents
- [Introduction](#introduction)
   - [Requirements](#requirements)
   - [Analysis Modes](#analysis-modes)
      - [RAxML](#raxml)
      - [File Converter](#file-converter)
      - [MS Comparison](#ms-comparison)
      - [D Statistic](#d-statistic)
    - [Figures](#figures)
    - [Output Files](#output-files)
- [Installation](#installation)
   - [Common Installation Errors](#common-installation-errors)
- [How To Use](#how-to-use)
- [Contributors](#contributors)
- [References](#references)

## Introduction

Automated Local Phylogenomic Analyses, or ALPHA, is a python-based application that provides an intuitive user interface for phylogenetic analyses and data visualization. It has four distinct modes that are useful for different types of phylogenetic analysis: RAxML, File Converter, MS Comparison, and D Statistic.

<img src="https://user-images.githubusercontent.com/6343193/28720952-4041d668-7374-11e7-829e-0fd22521cfc8.png" alt="Welcome" width="400">

RAxML mode gives users a front-end to interact with RAxML (STAMATAKIS 2014a) for Maximum Likelihood based inference of large phylogenetic trees. ALPHA’s RAxML mode allows one to use RAxML to automatically perform sliding window analysis over an inputted alignment. Users are able to select from a plethora of options in performing their analysis, including: window size, window offset, and number of bootstraps. In this mode, users are able to produce a variety of graphs to help understand their genomic alignment and interpret the trees outputted by RAxML. These graph options include: a tree visualization of the top topologies, scatter plot of windows to their topologies, frequency of top topologies, a line graph of windows to the percent of informative sites, and a heat map of the informative sites. RAxML mode also provides support for calculating two statistics based on the trees produced within each window as compared to an overall species tree: Robinson-Foulds distance and the probability of a gene tree given a species tree.

The file converter in ALPHA provides a user interface for a Biopython AlignIO file converter function. It allows users to convert between twelve popular genome alignment file types. RAxML mode only accepts phylip-sequential format.
MS Comparison mode allows users to perform an accuracy comparison between a “truth file” and one or more files in MS format or the results of RAxML mode.
With D Statistic mode, users can compute Patterson’s D Statistic for determining introgression in a four taxa alignment. D Statistic mode produces a scatter plot of the value of the D Statistic across sliding windows as well as the value of the D Statistic across the entire alignment.

### Requirements

ALPHA currently runs on both Mac and Windows operating systems and selects the proper operating system automatically. Python 2.7.13 and Java are required for this GUI, along with the additional libraries: [BioPython](http://biopython.org/wiki/Documentation), [DendroPy](https://www.dendropy.org/), [ETE](http://etetoolkit.org/), [Matplotlib](https://matplotlib.org/), [natsort](https://pypi.python.org/pypi/natsort), [PIL](http://www.pythonware.com/products/pil/), [PyQt4](http://pyqt.sourceforge.net/Docs/PyQt4/), [ReportLab](https://pypi.python.org/pypi/reportlab), [SciPy](https://www.scipy.org/), and [SVGUtils](https://pypi.python.org/pypi/svgutils). [RAxML](https://github.com/stamatak/standard-RAxML) is also required for performing analysis in RAxML mode.

Avoid special characters, such as diacritics, spaces, and punctuation other than dots (“.”) and underscores (“_”)  in the names of the ALPHA folder and all input files. 

### Analysis Modes

#### RAxML
In RAxML mode, there are two analysis sections containing preferences for adjusting the statistics. In the Run RAxML section, the user selects a file in phylip-sequential format and modifies the options within the Standard or Advanced RAxML settings to fit their preferences. 

In standard mode, the window size, window offset, and the number of top topologies to be analyzed can be inputted manually as integers greater than one. The model type can be selected from six popular types. Bootstrapping can also be selected; if it is, the user can input the confidence level and the number of bootstraps to be performed. The user can also choose to root the tree at a specific outgroup in the input file.

<img src="https://user-images.githubusercontent.com/6343193/28720944-3af69d42-7374-11e7-8c19-7fc336c5e428.png" alt="RAxML-Standard" width="400">

In advanced mode, the user can input a custom RAxML command in which the -s and -n flags are handled internally. A rooted or unrooted species tree can also be generated in this mode using a custom RAxML command or by simply clicking Generate, which runs RAxML on the entire alignment.

<img src="https://user-images.githubusercontent.com/6343193/28720942-396f2304-7374-11e7-8548-85dd6c7b2e1d.png" alt="RAxML-Advanced" width="400">

For more information regarding RAxML and its commands see the [RAxML manual](https://sco.h-its.org/exelixis/resource/download/NewManual.pdf).

After running RAxML, the user can enter the Generate Figures section and select any of the following: Top Topologies Tree Visualization, Windows to Top Topologies Scatter Plot, Top Topology Frequency Donut Plot, Windows to Informative Sites Line Graph, Informative Sites Heat Map, the weighted and/or unweighted Robinson-Foulds Distance Scatter Plot, and the Probability of a Gene Tree given the Species Tree Scatter Plot. The user can also specify how many top toplogies they want to analyze and input a species tree file or string in Graph Options.

The Top Topologies Tree Visualization generates an image containing the most frequently occuring local phylogenies generated by running RAxML on windows of the previously specified size. The visualization also includes the number of times each topology occurs. 

The Windows to Top Topologies Scatter Plot shows the windows at which each local phylogeny occurs and depicts the x-axis as the window number and the y-axis as the topology.

The Top Topology Frequency Donut Plot is a graph showing the number of times each topology occurs; topologies differing from the top topologies are lumped together and categorized as “Other.” 

Generate the Top Topologies Tree Visualization, Windows to Top Topologies Scatter Plot, and Top Topology Frequency Donut Plot at the same time to ensure that the colors of the topologies correspond with the colors used within the plots.

The Windows to Informative Sites Line Graph shows how the percent of informative sites differs across each window. Windows are on the x-axis, and the Percent of Informative Sites is on the y-axis. 

The Informative Sites Heat Map depicts the informativeness of each site in the data. If a site is informative, there is a black line. The more informative the site, the thicker the line in the heat map.

The Robinson-Foulds Distance Scatter Plot depicts the Robinson-Foulds distance between the local phylogeny and the species tree. The user can choose to generate the Weighted Robinson-Foulds Distance Scatter Plot, which takes branch lengths into account, or they can generate both the weighted and unweighted plots by not checking the Weighted option.

The Probability of A Gene Tree Given the Species Tree Scatter Plot shows the probability of the local phylogeny at a window actually occurring given the inputted species tree.

<img src="https://user-images.githubusercontent.com/6343193/28720932-3598db9e-7374-11e7-92c8-31397aedc637.png" alt="RAxML-Graph-Options" width="400">

#### File Converter
File Converter mode allows the user to select a file containing DNA alignments in one of twelve popular formats and convert them to a different file format. After selecting the input file and its format, the user must specify the output file’s name and location along with the desired format.

<img src="https://user-images.githubusercontent.com/6343193/28720928-349f1898-7374-11e7-86ee-86a1abcc9341.png" alt="File-Converter" width="400">

For more information regarding file types see [BioPython AlignIO](http://biopython.org/wiki/AlignIO).

#### MS Comparison
In MS Comparison mode, the user can specify an MS truth file and the RAxML directory and/or other MS files to compare it to . This mode has options to generate figures for Robinson-Foulds Distance From MS Truth Bar Plot, Percent Matching Sites Bar Plot, and TMRCA Line Graph.

When comparing against the RAxML directory, the user has the option to input the directory containing the RAxML files and choose the window size and offset. This function is meant to be used after performing sliding window analysis in ALPHA’s RAxML mode. 

When comparing the truth file to other MS files, the user can input multiple MS files for comparison.

The Robinson-Foulds Distance from MS Truth Bar Plot depicts the total difference between the trees in the truth file and other files chosen for comparison. 

The Percent Matching Sites Bar Plot shows the percentage of sites in the comparison file(s) that contain trees that match the truth file for both weighted and unweighted analyses. The Robinson-Foulds distance is used to determine if a tree is considered a match or not.

The TMRCA Line Graph shows the tree height over each site when comparing the truth files and other files. This figure is meant to depict to the differences in the time to most recent common ancestor (TMRCA) between each file.

<img src="https://user-images.githubusercontent.com/6343193/28720938-38044bf2-7374-11e7-890a-f711b3a31983.png" alt="MS-Comparison" width="400">

#### D Statistic
D Statistic mode allows the user to input an alignment file in phylip-sequential format, choose the window size and offset, and select the location of each outgroup in the tree visual. This mode then generates the overall D Statistic and a scatter plot in which the x-axis is the window number, and the y-axis is the D Statistic value computed for that window.

<img src="https://user-images.githubusercontent.com/6343193/28720924-30c81a4e-7374-11e7-88b6-cdf02d169af1.png" alt="D-Statistic" width="400">

For further reading on the D Statistic and its usage see: \
[Green et al. (2010)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5100745/#SD1), 
[Durand et al. (2011)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3144383/),
[Martin et al. (2014)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4271521/) 

### Output Files

All output files are automatically saved in various folders in ALPHA. Windows that are created by RAxML are outputted into the “windows” folder, and are saved as “window0.phylip”, “window1.phylip”, etc. Files outputted by running RAxML are found in the “RAxML_Files” directory. When bootstrap analysis is chosen these files are saved under “RAxML_bestTree”, “RAxML_bipartitions”, “RAxML_bipartitionsBranchLabels”, “RAxML_bootstrap”, and “RAxML_info”. When bootstrapping is not chosen these files are named “RAxML_bestTree”, “RAxML_randomTree”, “RAxML_result”, “RAxML_log”, and “RAxML_info”. Each of these files has “.0”, “.1”, “.2”, etc. extensension corresponding to the index of the window that RAxML was run on. All graphs and images are automatically saved into the plots folder under the name of the image.

For more information regarding the RAxML output files see the [RAxML manual](https://sco.h-its.org/exelixis/resource/download/NewManual.pdf).
 
## Installation

### Mac Instructions
1) Install [RAxML](https://github.com/stamatak/standard-RAxML)
    - Download the [RAxML](https://github.com/stamatak/standard-RAxML) source code in a zip folder. 
    - Unzip the directory 
    - Open a terminal window and 'cd' into the directory
    - In terminal run:
    
        ```
        make -f Makefile.gcc
        rm *.o
        make -f Makefile.SSE3.gcc
        rm *.o
        make -f Makefile.PTHREADS.gcc
        rm *.o
        make -f Makefile.PTHREADS.gcc
        ```
    - Check that RAxML runs with the following command:
        
        ```
        ./raxmlHPC -v
        ```
        
    - 'cd' out of standard-RaxML-master and run:
        
        ```
        cp raxmlHPC* /usr/local/bin/
        raxmlHPC -v
        ```
    - If the last command shows the version, proceed. Otherwise, check the Common Errors section below. 
    
2) Install [Python 2.7.13](https://www.python.org/downloads/)
    - In terminal run::
    
        ```
        python --version
        ```
    - If the command returns "Python 2.7.13" skip to step 3. Otherwise proceed.
    - Download and Install [Python 2.7.13](https://www.python.org/downloads/)
    

3) Install [Homebrew](https://brew.sh/)
    - In terminal run:
    
        ```
        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
        ```


4) Install [SIP and PyQt4](https://www.riverbankcomputing.com/software/pyqt/download)
    - In terminal run:
    
        ```
        brew install sip
        brew install cartr/qt4/pyqt
        ```

5) Install [PIP](https://pip.pypa.io/en/stable/installing/):
    - In terminal run:  
       
        ```
        sudo easy_install pip
        ```

6) Install remaining dependencies with PIP:
    - In terminal run:
    
        ```
        pip install matplotlib pillow scipy natsort reportlab svgutils ete3 dendropy biopython
        ```

7) Install ALPHA:
    - Download the source code of this repo as a zip
    - Unzip the directory
    - 'cd' into the directory
    - To open ALPHA, run the following command in terminal:
    
        ```
        python main.py
        ```

### Common Installation Errors

#### Installing Xcode 
If prompted, install the latest verson of [Xcode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12).

#### Python 2.7.13 Installation
If the command in Step 2 does not return "Python 2.7.13" after you have installed it, run:
    
        
        export PATH="/path/to/your/python2.7.13/bin:${PATH}"
        
        
The command in Step 2 should now return "Python 2.7.13".

#### No module named SIP
If you receive this error after running the command in Step 7, run this command:
    
        mkdir -p /Users/owner/Library/Python/2.7/lib/python/site-packages echo 'import site; site.addsitedir("/usr/local/lib/python2.7/site-packages")'

## How To Use
After installing and opening ALPHA, you can use the drop down menu on the main page to select the mode you'd like to use. Once you enter any of these modes, you can use the "Mode" drop down menu in the upper left corner to enter a different one. 

Here, we use the provided example files (see the folder "exampleFiles" in the ALPHA directory) to show how to use the software.

### RAxML Mode
#### Run RAxML
For Standard Mode:
- Input the desired window size and offset, and select the desired model.
- If you select the Bootstrap option, input the desired confidence level and number of bootstraps to be run.
- To root the tree, select the Rooted option. Use the drop down menu to select the desired outgroup. 

For Advanced Mode:
- If you select the Custom RAxML Command option, input your desired command without the -s and -n flags.
- To generate a species tree:
  - If you select the Custom RAxML Command option, use the same parameters as above to input your command.
  - To root your species tree, select the Rooted option and select your desired outgroup with the drop down menu on the right.
  - Click the Generate button to create your species tree file.

After modifying these options to your preferences, click the Run RAxML button. The Generate Figures options will be available after you run RAxML.

#### Generate Figures
Select any number of the eight figures to generate. Some of the figures require inputs in the Graph Options and Species Tree sections, so their necessary parameters are defined below.

For Top Topologies Tree Visualization, Windows to Top Topologies Scatter Plot, and Top Topologies Frequency Donut Plot:
- To ensure that the color coding for these visuals is correct, generate the three figures together.
- Input the number of most frequently occurring topologies that you want to generate figures for in the Number of Top Topologies section under Graph Options.

For Robinson-Foulds Distance Scatter Plot:
- Input the species tree by selecting a file or inputting a newick string under the Species Tree section. You can generate a species tree for this by following the steps in the Advanced mode of Run RAxML. It is not necessary that the species tree is rooted.
- If you select the Weighted option, ALPHA will generate the weighted Robinson-Foulds Distance Scatter Plot. Otherwise, it will generate both the weighted and unweighted graphs.

For p(GT|ST) Scatter Plot:
- Input the Input the species tree by selecting a file or inputting a newick string under the Species Tree section. You can generate a species tree for this by following the steps in the Advanced mode of Run RAxML. The tree must be rooted to generate this plot.

Once you have selected the desired figures to be generated, click the Generate Figures button. 

To resize and manipulate the figures:
- All figures generated in ALPHA use a Matplotlib output interface, allowing users to customize figures to their liking. Hovering one’s cursor over the icons at the bottom of each figure’s output window provides a short description of each icon’s usage. The following describes each button from left to right.
 
- The home button reformats the plot to the default view. 
- The left arrow button changes the plot to its previous view.
- The right arrow button changes the plot back to its former view if the previous view is selected. 
- The arrow cross button allows users to change the view of the figure by panning across the plot.
- The magnifying glass button allows users to zoom to a rectangle on the plot. 
- The sliders button allows users adjust the spacing and borders of their plots. 
- The tight layout button gets rid of the border around the plot. 
- The plot button allows users to customize the axes and curves of the figure. 
  - The axes tab allows users to change the min, max and scale of the axes, along with the title and axes labels. This tab also allows users to automatically generate a legend. 
  - The curves tab allows users to select each curve on the plot and alter its label, line style and color. Both the sliders button and plots button can be accessed by the “Configure Plot” menu at the top of the window; they can be found under “Configure Subplots” and “Configure Axis and Curves” respectively. 

To save figures as images:
- The save button allows users to save and export the figure window to a specified location. This functionality can also be accessed under “Save As…” in the “File” menu at the top of the output window.
- All images can be exported to a desired save location, renamed and saved as one of the following file types: pdf, png, jpeg, tiff, svg, eps, rgba, pgf, and ps.


For more information on RAxML Mode and the figures it can generate, see the [RAxML](#raxml) section above.

### File Converter Mode
To use the file converter, first select the input file and its format. 
Then, specify the desired filename, location, and format of the output file. 
Click the convert button to create your new file. 


For more information on the File Converter and its formats, see the [File Converter](#file-converter) section above.

### MS Comparison Mode
First, select the MS Truth File that you want to analyze. Then, select either the Compare Against RAxML Directory option or the Compare Against MS File(s) option.

#### Compare Against RAxML Directory
To compare against a RAxML directory:
- Select the desired folder of RAxML files.
- Input the preferred window size and offset.

#### Compare Against MS File(s)
To select more than one MS file to compare against, simply click the + button to add the number of files you want to compare. Then, select one MS file per box. To remove a file, click the - button on the left side of the file input box.

#### Graphs
Select any number of the three graphs to generate them.
Click the Compare button to run MS Comparison and generate the desired figures.


For more information on MS Comparison and the graphs it generates, see the [MS Comparison](#ms-comparison) section above.

### D Statistic
To compute the D Statistic, first input the desired alignment in phylip-sequential format. 

Then, input the preferred window size and offset. 

Using the provided four taxa tree, select your desired topology. Click the Run button to generate the D Statistic and the Windows to D Statistic Scatter Plot.


For more information on the D Statistic and what it outputs, see the [D Statistic](#d-statistic) section above.

## Contributors
- [Chabrielle Allen](https://github.com/chaballen)
- [Travis Benedict](https://github.com/travisbenedict)
- [Peter Dulworth](https://github.com/PeterDulworth)
- [Leo Elworth](https://www.linkedin.com/in/chilleo/)
- [Luay Nakhleh](https://www.cs.rice.edu/~nakhleh/)

## References

Cock PJA, Antao T, Chang JT, et al. Biopython: freely available Python tools for computational molecular biology and bioinformatics. Bioinformatics. 2009;25(11):1422-1423. doi:10.1093/bioinformatics/btp163.

Durand EY, Patterson N, Reich D, Slatkin M. Testing for Ancient Admixture between Closely Related Populations. Molecular Biology and Evolution. 2011;28(8):2239-2252. doi:10.1093/molbev/msr048.

ETE 3: Reconstruction, analysis and visualization of phylogenomic data. Jaime Huerta-Cepas, Francois Serra and Peer Bork. Mol Biol Evol 2016; doi: 10.1093/molbev/msw046

Green RE, Krause J, Briggs AW, et al. A Draft Sequence of the Neandertal Genome. Science (New York, NY). 2010;328(5979):710-722. doi:10.1126/science.1188021.

Richard R. Hudson; Generating samples under a Wright–Fisher neutral model of genetic variation. Bioinformatics 2002; 18 (2): 337-338. doi: 10.1093/bioinformatics/18.2.337

Hunter, John D. "Matplotlib: A 2D Graphics Environment." Computing in Science & Engineering 9.3 (2007): 90-95. 10.1109/MCSE.2007.55

Martin SH, Davey JW, Jiggins CD. Evaluating the Use of ABBA–BABA Statistics to Locate Introgressed Loci. Molecular Biology and Evolution. 2015;32(1):244-257. doi:10.1093/molbev/msu269.

Stamatakis A. 2014a. RAxML version 8: a tool for phylogenetic analysis and post-analysis of large phylogenies. Bioinformatics 30, 1312–1313. DOI: 10.1093/bioinformatics/btu033.

Stamatakis A. 2014b. The RAxML v8.0.X Manual

Sukumaran, J. and Mark T. Holder. 2010. DendroPy: A Python library for phylogenetic computing. Bioinformatics 26: 1569-1571.

Than C, Ruths D, Nakhleh L (2008) PhyloNet: a software package for analyzing and reconstructing reticulate evolutionary relationships. BMC Bioinformatics 9: 322

Yu Y, Degnan JH, Nakhleh L. The Probability of a Gene Tree Topology within a Phylogenetic Network with Applications to Hybridization Detection. Felsenstein J, ed. PLoS Genetics. 2012;8(4):e1002660. doi:10.1371/journal.pgen.1002660.
