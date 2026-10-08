![[Pasted image 20261008112506.png]]
When setting up a standard planning business process, either configure settings or use an existing snapshot as a starting point
![[Pasted image 20261008112525.png]]

Key note:
	the planning business process in the EPM standard Cloud Service does not support:
		custom applications that allow advance customization to meet specific business requirements. 
		Nor does it support [[FreeForm application]] applications that enable flexible planning deployments without dimensions requirements or the use of Essbase outline files
		Groovy scripting also not available 

Application type:
Standard: are ideal to build advance applications for any business process:
	Create a sample application for demo, or
	New application which allow to build an advance, custom application that can be tailored to specific requirements

Enterprise: Builds custom applications or use predefined business processes to create application for Financials, Workforce, Capital, and Projects. Can also build a Strategic Modeling solution

Reporting: Builds a basic application that serve for reporting and analysis purposes

# Best Practices 
# Planning dimensions:

1. Dimensions order should follow a modified hours-glass format
	1. Beginin with densest dimensions followed by less dense one, then
	2. Aggregate sparse dimensions before non-aggregating sparse dimensions
		1. within sparse dimensions, place the densest first
		2. In Hybrid BSO #BSO , ensure non-dynamic sparse dimensions order before dynamic ones
2. Keep block sizes optimal
		1. ideally between 8KB to 500KB by:
			1. limiting number of dense dimensions to a max of 3, and
			2. setting higher level members in dense dimensions as Label Only or Dynammic Calc
3. Text, Smart List, Date and Store Percetage type accounts should be set to **Never** for consolidation property
4. All Generation 2 members, which are root members, should be set to Ignore since they cannot be secured or included in forms and aggregating them increases the block count
5. Long or flat dimensions will lead to an issue with the performance of aggregation -> Add intermediate parents  for structure with more than 200 children under a single parent to improve aggregation perf
6. Avoid enabling dimension members for multiple cubes to prevent dynamic X-ref which can degrade perf. Instead, leverage the **HSB_NOLINKUDA** and leverage [[Data Maps]] or [[Smart Push]] for data movement instead
7. When possible, avoid single child members as they lead to implied shares or duplicated data blocks, especially if set to never share
8. For simple calculations, leverage outline math (calculate account C as account A minus account B) instead of writing custom member formulas 
9. Aggregate large dimensions in [[ASO cubes]] instead of BSO cube whenever possible to enhance perf during process like cube refrehses
10. Store historical data beyond two years in [[ASO cubes]] instead of BSO cube

# Required Dimensions

**Entity Dimensions** : 
	Groupd cost center into roll-ups or parent memebers such as by BU or division to reflect the organization structure
	Create alternate hierachies for different reporting needs
**Account Dimensions**: 
	Upper level members should be set to Dynamic Cals or Lable Only
	When calculating ratios or KPIs using member formulas, use the Dynamic Calc, Two Pass settings to ensure calculations at upper levels aggregate percetanges correctly
Version: 
	Working version to develop Plan and Forecast
	1st Pass to maintain iterations of your Plan
	What if for scenarios analysis
Currentcy:
	Limit the reporting currentcy to 1 (normally set to USD)
	Enter exchange rates for each valid scenario and year
Period:
	Use Substitution Variables such as *prior MTH*  or *MTH* to streamline reporting and calculations 
	Use Dynamic Time Series to calculate time periods such as YTD, QTD
	Set Summary Time periods using Dynamic Calc for peformance
Year:
	Use Subsitution Variables for each year that is included in process
Scenario
	Limit the number of Scenarios
	Align Scenarios Structure with Reporting Needs

# User-Defined [[Dimensions]]

Limit the Number of User-Defined Dimensions to less than 12 (can add upto 32 dims but less than 12 is much better)
Seperate dimensions into buckets for planning and reporting categories. For examples:
	Product/ Market/ Channels should be under Planning
	Product segment/ Customer segment should be under Reporting
Avoid Overlapping with Standard Dimensions
Continue to review and validate to make sure it aligns with evolving business requirements

# Cubes: 
Keeps Block size between 8K and 200KB: Oversize blocks increase memory usage
Minimize the number of blocks: Large number of blocks can degrade performance and increase calculation time and disk usage
Limit dense dimensions: Too many dense dimensions expand block size and slow down performance
Limit number of children undera single dynamic parent #dynamicparent: Too many childrens can degrade query performance due to complex calculation at run time
Limit number of children under a single store parent: excessive children can still impact data load and retrieval speeds 
Avoid parents with one child member for level 1 and above of divementsions: waste resources and complicate calculations