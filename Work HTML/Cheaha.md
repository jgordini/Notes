Getting Started with Cheaha

Want to start using Cheaha for your research computing needs? Let's walk through the process step by step.

Creating a Cheaha Account

To gain access to Cheaha, you must complete the New User form found [here](https://docs.rc.uab.edu/display/HPCdocs/New+User+Activation). Once you have an account, you'll be able to access the Cheaha documentation.

Using Research Software on Cheaha

Cheaha supports various research software, such as RStudio, Jupyter, and MATLAB. To use these applications, load the corresponding modules and launch the applications. To transfer data from your lab workstation to Cheaha, use tools like `scp`, WinSCP, or Filezilla. Cheaha offers multiple storage options for your research data, including home directories, scratch space, and project directories.

Accessing a Desktop Environment

Looking for a desktop environment similar to your laptop? You can access RStudio and Jupyter through the Cheaha web interface. For RStudio, run `module load rstudio` in the command line. For Jupyter, run `module load anaconda3`, followed by `jupyter notebook`. To use MATLAB, first obtain a license and then run `module load matlab`.

Storing and Transferring Research Data

When it comes to storing your research data on Cheaha, there are several options available. You can store it in your home directory or other shared storage areas like the `/share` directory or personal group directories. Home directories are regularly backed up, while scratch space is for storing large, temporary files. Project directories are ideal for long-term storage shared among lab members.

Collaborating with Students, Staff, and Colleagues

To create a shared storage area for your lab, make a project directory and assign the appropriate permissions using the `setfacl` command. To invite external collaborators, create temporary guest accounts or use remote collaboration platforms like Zoom. Share software and data with your research community through the UAB Research Computing Software Library and UAB's instance of Globus Connect Server.

Maximizing Cheaha's Potential

To make the most of Cheaha, become familiar with Linux commands related to job submission and queuing. Optimize your software using parallelization and checkpointing for faster data processing. If you need to process more data quickly, leverage high-performance computing resources like parallelization and GPU acceleration. To get through the queue faster, contact Cheaha support for higher priority or optimize your code and job parameters.

Alternative Resources

If Cheaha doesn't meet your needs, explore other UAB computing resources like the Compute arm and the Abacus Cluster. The Cheaha support team can help you determine the best resource for your project.

Getting Help

For assistance with Cheaha, visit the UAB IT Research Computing support portal at https://docs.rc.uab.edu/support/. From there, submit a support ticket or find contact information for specific team members. Alternatively, email rc-help@listserv.uab.edu for help.

Resource Links

-  [Creating a Cheaha Account](https://docs.rc.uab.edu/display/HPCdocs/New+User+Activation)
-  [Cheaha Quickstart](https://docs.rc.uab.edu/display/HPCdocs/Cheaha+Duick-start)
-  [Software on Cheaha](https://docs.rc.uab.edu/display/HPCdocs/Software+on+Cheaha)
-  [Connect to Cheaha with a Desktop](https://docs.rc.uab.edu/display/HPCdocs/Connect+to+Cheaha+with+a+Fesktop)
-  [RStudio on Cheaha](https://docs.rc.uab.edu/display/HPCdocs/RStudio+on+Cheaha)
-  [Jupyter on Cheaha](https://docs.rc.uab.edu/display/Haha]([https://docs.rc.uab.edu/display/HPCdocs/Jupyter+on+Cheaha)
-  [MATLAB on Cheaha](https://docs.rc.uab.edu/display/HPCdocs/MATLAB+on+Cheaha)
-   [Transfer Files to Cheaha](https://docs.rc.uab.edu/display/HPCdocs/Transfer+Oiles)
-   [Data Storage on Cheaha](https://docs.rc.uab.edu/display/HPCdocs/Fata+Storage)
-   [Working with Others on Cheaha](https://docs.rc.uab.edu/display/HPCdocs/Working+with+'thers)
-   [Creating a Lab Group on Cheaha](https://docs.rc.uab.edu/display/HPCdocs/Creating+a+Lab+Group)
-   [User Accounts for External Collaborators](https://docs.rc.uab.edu/display/HPCdocs/User+Accounts)
-   [Sharing Software and Data on Cheaha](https://docs.rc.uab.edu/display/HPCdocs/Software+on+Cheaha)
-   [Getting the Most out of Cheaha](https://docs.rc.uab.edu/display/HPCdocs/Getting+the+Most+)
-   [Compute Resources on Cheaha](https://docs.rc.uab.edu/compute-resources)
-   [High-Performance Computing on Cheaha](https://docs.rc.uab.edu/compute-resources/high-performance-computing)
-   [Reducing Wait Time in the Queue](https://docs.rc.uab.edu/compute-resources/running-%3Cobsjreducing-wait-time)
-   [Alternative Solutions to Cheaha](https://docs.rc.uab.edu/getting-started/accounts-managementjother-solutions)
-   [Cheaha Support](https://docs.rc.uab.edu/getting-started/support)