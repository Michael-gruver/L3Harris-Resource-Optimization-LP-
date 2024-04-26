# L3Harris-Resource-Optimization-LP-
For our senior design capstone project we build our sponsor L3 Harris a resource optimization tool that allows them to optimize where workers are allocated given various constrains such as location, security clearance, and skills.


L3Harris Project Scheduler Tool- “How-To” Guide
How to run
1.	Download a compiler
2.	Download AMPL
3.	Get a community edition license
4.	Open code on compiler
5.	Run the following commands:
  a.	# Install Python API for AMPL
  b.	$ python -m pip install amplpy --upgrade
  c.	# Install solver modules (e.g., HiGHS, CBC, Gurobi)
  d.	$ python -m amplpy.modules install highs cbc gurobi
  e.	# Activate your license (e.g., free https://ampl.com/ce license)
  f.	$ python -m amplpy.modules activate <license-uuid>
6.	Run the code
File Requirements
1. Python Code File
●	File Name: “Schedule optimization application - L3Haris capstone project - 2.2”
●	Description: This Jupyter notebook contains the executable code necessary for optimizing the distribution of staff across various projects.
2. Data File
●	File Name: “data.xlsx”
●	Description: This Excel file is a template for you to add all the data inputs the code requires. 
*Note: In this datasheet, the headers in red cannot be altered in any way.*
________________________________________
Variable Guide
People/Projects Tab
●	Name
●	Description: Unique identifier for staff members or projects; these names must be distinct.
●	Requirements: Uniqueness is key for proper assignment and optimization.
●	External? (Projects tab only)
●	Description: Indicates whether a project is external. The program prioritizes completing external projects first
●	Format: Enter “1” for external projects and “0” for internal ones.
●	Value (Projects tab only)
●	Description: Reflects the importance of the project, which influences its priority in the optimization process. The program prioritizes completing higher-value projects first.
●	Format: Assign higher numeric values to more important projects.
●	Clearance
●	Description: The clearance level required for staff to work on a project or the clearance of the staff
●	Format: Staff members must have a clearance level equal to or higher than the project requirement after taking location into account.
●	Values: 
■	0 = unclassified
■	1 = secret
■	2 = top secret
●	Location
●	Description: Indicates the project's work location.
●	Format: Use “0” for remote locations; other numbers should be defined according to specific onsite locations.
●	Values:
■	Remote = 0, can work on unclassified (0)
■	Palm bay = 1, can work on any classification (0,1,2)
■	Northern VA = 2, can work on unclassified (0) and top secret (2)
■	Clifton NJ = 3, can work on unclassified (0) and secret (1)
●	Skills
●	Description: Particular skills required for the project.
●	Format: For staff, skills are usually denoted as binary (1 or 0) indicating whether a staff member possesses that skill or not. For projects, this is linked to the number of hours needed (e.g., 0.5, 1, 3).
*Note: Staff numbers between 0 and 1 would indicate that a person has a skill but work less efficiently (0.5 means it takes that person 2 hours to complete 1 hour of work with that skill) Numbers above 1 mean that the person is more efficient (2 mean they get 2 hours of work done per hour assigned).
Project Management is the only skill header that must be present. All other skills can be added or deleted. The skills headers must match in the People & Projects tab.

Parameters Tab
●	ScheduleChangeWeight
●	Description: Penalty value for trying to change the current schedule.
●	Format: Any positive number
●	MinAlloc
●	Description: The minimum amount of value a person needs to produce per unit of time to be assigned. We don't want to assign people to work if they don't produce any value.
●	Format: Any positive number, best to keep low < 0.1
●	OverTimePenalty
●	Description: Penalty value for use of overtime. 
●	Format: Any positive number
●	ExternalWeight
●	Description: Indicates the weight given to prioritizing external projects before internal projects.
●	Format: Any positive number
*Note: For all parameters, higher values mean the program will give more weight to that consideration. Lower values mean less weight given. A value of zero means the program will ignore that consideration. 

Current Schedule Tab
●	Description: Helps maintain continuity by considering the previous staff allocation to projects.
●	Usage: Paste the output from the previous run to prevent reassignment of staff to new projects, ensuring stability and continuity.
●	Note: It is very important to check spelling, if a person's name is spelled incorrectly on the current schedule tab, the program will think that it is a completely different name and will ignore the data.
 ![image](https://github.com/Michael-gruver/L3Harris-Resource-Optimization-LP-/assets/168142857/1b7cf0a3-0ee4-4f24-9a8f-24cf3bbd6863)

Example of current schedule input, with people as the rows and projects as the columns.
________________________________________
Running the Code
	Load the Jupyter Notebook
●	Open the notebook in an environment that executes Jupyter notebooks (e.g., Anaconda, JupyterLab).
	Setup the Data File
●	Confirm that the data file exists and contains the correct information
	Install Required Packages
●	Follow the notebook instructions to install any necessary packages (e.g., pandas, numpy) that are not pre-installed.
	Execute the Code
●	Run the code. You will be asked to select a filename to read from and then a file name to export results to. 
	Review the Output
●	The final output will be displayed in the last cells of the notebook and in the output Excel file. Check these results to ensure they meet the project's specifications.
●	These numbers are the FTE, meaning if someone has a 1 under Project 2, they work 40 hours/week on Project 2.
________________________________________
Additional Notes
●	The code is designed for flexibility and can be re-run with new data as project parameters or staff availability changes.
●	Ensure all data inputs are complete and correctly formatted to avoid errors, particularly with the 'Current Schedule' if utilized.
●	The maximum overtime allowed is 20% (a person can work up to 1.2 FTE). This can be altered in the code file.
●	The code will not run if there are 0 people to assign.
●	If there are too many project hours than what the workforce can offer, the project will not be fully staffed
